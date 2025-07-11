# Sử dụng image crawlab gốc làm base
ARG CRAWLAB_BASE_IMAGE=crawlabteam/crawlab
FROM ${CRAWLAB_BASE_IMAGE}
# HOẶC NẾU BẠN ĐÃ CÓ IMAGE TÙY CHỈNH VỚI CHROME (ví dụ: my-custom-crawlab-worker:latest)
# FROM my-custom-crawlab-worker:latest

# Chuyển sang user root để cài đặt phần mềm
USER root

# === PHẦN CÀI ĐẶT CHROME VÀ CÁC PHỤ THUỘC (LẶP LẠI TỪ DOCKERFILE CŨ NẾU BASE IMAGE CHƯA CÓ) ===
# Nếu FROM image của bạn ở trên chưa có Chrome, hãy sao chép phần cài đặt Chrome từ Dockerfile của worker1 vào đây.
# Ví dụ:
RUN apt-get update && apt-get install -y \
    wget \
    gnupg \
    libglib2.0-0 \
    libnss3 \
    libgconf-2-4 \
    libfontconfig1 \
    # ... (và các phụ thuộc khác cho headless Chrome) ...
    --no-install-recommends && \
wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | apt-key add - && \
sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list' && \
apt-get update && \
apt-get install -y google-chrome-stable --no-install-recommends && \
rm -rf /var/lib/apt/lists/*
# === KẾT THÚC PHẦN CÀI ĐẶT CHROME ===

# Cài đặt các thư viện Python cơ bản (nếu chưa có trong base image) và các thư viện mới
RUN pip install --no-cache-dir \
    selenium \
    webdriver-manager \
    crawlab-sdk \
    beautifulsoup4 \
    python-dotenv

# Chuyển về user mặc định (nếu cần)
# USER crawlab