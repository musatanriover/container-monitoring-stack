# 🐳 Container Monitoring Stack (Docker + Grafana + Prometheus + HTTPS)

Bu proje, Docker container'larınızı ve sunucunuzu gerçek zamanlı olarak izleyebileceğiniz bir **monitoring çözümüdür**.

## 🚀 İçerik

- [x] 🔍 Prometheus → metrik toplar
- [x] 📈 Grafana → grafik & dashboard arayüzü
- [x] 🐳 cAdvisor → container metrikleri (CPU, RAM, ağ)
- [x] 🖥️ node_exporter → sunucu (host) metrikleri
- [x] 🔐 NGINX → Basic Auth ile şifre koruması
- [x] 🔒 HTTPS → Self-signed SSL ile şifreli bağlantı
- [x] 🐳 Tamamı Docker Compose ile ayağa kalkar

## 📂 Klasör Yapısı

```bash
monitoring-stack/
├── docker-compose.yml
├── prometheus/
│   └── prometheus.yml
├── nginx-proxy/
│   ├── default.conf
│   ├── .htpasswd
│   └── certs/ (ignore edilir)
└── .gitignore

 ⚙️ Kurulum

 1. Repo'yu klonla
git clone https://github.com/musatanriover/container-monitoring-stack.git
cd container-monitoring-stack

 2. Gerekli sertifikayı oluştur (eğer yoksa)
openssl req -x509 -nodes -days 365 \
  -newkey rsa:2048 \
  -keyout nginx-proxy/certs/selfsigned.key \
  -out nginx-proxy/certs/selfsigned.crt \
  -subj "/CN=localhost"

 3. Docker Compose ile başlat
docker compose up -d

 🔐 Erişim Bilgileri

| Servis        | Adres                                          | Giriş           |
| ------------- | ---------------------------------------------- | --------------- |
| Grafana       | [https://localhost](https://localhost)         | `root` / şifren |
| Prometheus    | [http://localhost:9090](http://localhost:9090) | -               |
| cAdvisor      | [http://localhost:8080](http://localhost:8080) | -               |
| Node Exporter | [http://localhost:9100](http://localhost:9100) | -               |

Tarayıcı sertifika uyarısı verir, çünkü sertifika self-signed'dır. Devam etmek güvenlidir (şifrelenmiş bağlantıdır).

 📊 Grafana Dashboard

Data Source:
Prometheus olarak eklenmelidir → http://prometheus:9090

Hazır Dashboard'lar:
Node Exporter Full (ID: 1860)
Docker Monitoring (ID: 193)

