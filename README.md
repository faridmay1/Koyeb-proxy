import os
from http.server import BaseHTTPRequestHandler, HTTPServer

# المنفذ يقرأ من متغير البيئة الذي توفره Koyeb
PORT = int(os.environ.get("PORT", 8080))

class SimpleProxyHandler(BaseHTTPRequestHandler):
    def do_GET(self):
        self.send_response(200)  # OK
        self.send_header('Content-type', 'text/plain')
        self.end_headers()
        self.wfile.write(b"✅ Proxy is working from Koyeb!")

    def log_message(self, format, *args):
        # إيقاف طباعة السجلات في كل طلب لتقليل الضوضاء
        return

if __name__ == "__main__":
    server_address = ("", PORT)
    httpd = HTTPServer(server_address, SimpleProxyHandler)
    print(f"Serving at port {PORT}")
    httpd.serve_forever()
