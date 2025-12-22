# Docker Tools Collection

A curated collection of Docker images and configurations for development tools, remote access, and network utilities. Each image is optimized for specific use cases with clear documentation.

## 🛠️ Available Docker Images

### 1. debian-xfce4-novnc
A Debian-based desktop environment accessible via web browser using noVNC.

**Features:**
- Full XFCE4 desktop environment
- Web-based access (noVNC)
- Lightweight Debian base
- Pre-configured for remote development

**Usage:**
```bash
docker build -t debian-xfce4-novnc ./debian-xfce4-novnc
docker run -p 8080:80 debian-xfce4-novnc
```

### 2. ssh-socks-proxy
A secure SSH SOCKS5 proxy for tunneling network traffic.

**Features:**
- SOCKS5 proxy over SSH
- Secure encrypted tunneling
- Lightweight Alpine Linux base
- Easy configuration

**Usage:**
```bash
docker build -t ssh-socks-proxy ./ssh-socks-proxy
docker run -p 1080:1080 ssh-socks-proxy
```

### 3. v2ray-proxy
V2Ray proxy server for secure network communications.

**Features:**
- V2Ray core implementation
- Configurable routing rules
- Multiple protocol support
- Optimized for performance

**Usage:**
```bash
docker build -t v2ray-proxy ./v2ray-proxy
docker run -p 10086:10086 v2ray-proxy
```

## 🚀 Quick Start

1. **Clone the repository:**
```bash
git clone https://github.com/qaderizadeh/docker-tools-collection.git
cd docker-tools-collection
```

2. **Choose an image directory and build:**
```bash
cd [image-directory]
docker build -t [image-name] .
```

3. **Run the container:**
```bash
docker run -p [host-port]:[container-port] [image-name]
```

## 📋 Requirements

- Docker 20.10+
- Docker Compose (optional, for multi-container setups)
- Git for cloning the repository

## 🏗️ Project Structure

```
docker-tools-collection/
├── debian-xfce4-novnc/
│   └── Dockerfile
├── ssh-socks-proxy/
│   └── Dockerfile
├── v2ray-proxy/
│   └── Dockerfile
└── README.md
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit your changes using conventional commit messages
4. Push to the branch (`git push origin feature/your-feature`)
5. Open a Pull Request

## 📝 Commit Guidelines

This project follows [Conventional Commits](https://www.conventionalcommits.org/). Example commit messages:
- `feat: add new web-based terminal image`
- `fix: resolve port conflict in ssh-socks-proxy`
- `docs: update README with usage examples`

## 🔒 Security Notes

- Always change default credentials before production use
- Review Dockerfile configurations for your specific security requirements
- Keep base images updated with security patches

## 📄 License

MIT

## ⭐ Support

If you find this project useful, please consider giving it a star on GitHub!
