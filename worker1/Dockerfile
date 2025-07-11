# Sử dụng image crawlab gốc làm base
ARG CRAWLAB_BASE_IMAGE=crawlabteam/crawlab
FROM ${CRAWLAB_BASE_IMAGE}

# Chuyển sang user root để cài đặt phần mềm
USER root

# Cài đặt wget, gnupg và các phụ thuộc cần thiết khác
RUN apt-get update && apt-get install -y \
    wget \
    gnupg \
    # Các phụ thuộc cho headless Chrome (quan trọng)
    libglib2.0-0 \
    libnss3 \
    libgconf-2-4 \
    libfontconfig1 \
    libx11-6 \
    libx11-xcb1 \
    libxcb-dri3-0 \
    libxcb-icccm4 \
    libxcb-image0 \
    libxcb-keysyms1 \
    libxcb-randr0 \
    libxcb-render-util0 \
    libxcb-render0 \
    libxcb-shape0 \
    libxcb-shm0 \
    libxcb-sync1 \
    libxcb-util1 \
    libxcb-xfixes0 \
    libxcb-xinerama0 \
    libxcb-xkb1 \
    libxcomposite1 \
    libxcursor1 \
    libxdamage1 \
    libxext6 \
    libxfixes3 \
    libxi6 \
    libxrandr2 \
    libxrender1 \
    libxss1 \
    libxtst6 \
    ca-certificates \
    fonts-liberation \
    lsb-release \
    xdg-utils \
    --no-install-recommends

# Thêm Google Chrome PPA và cài đặt Google Chrome stable
RUN wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list' \
    && apt-get update \
    && apt-get install -y google-chrome-stable --no-install-recommends \
    && rm -rf /var/lib/apt/lists/*

# (Tùy chọn nhưng khuyến nghị) Cài đặt các thư viện Python cần thiết cho Selenium và Crawlab
# Điều này giúp image tự chứa hơn, mặc dù Crawlab cũng có thể cài từ requirements.txt
RUN pip install --no-cache-dir selenium webdriver-manager crawlab-sdk

# Chuyển về user mặc định của image Crawlab (thường là crawlab hoặc root tùy phiên bản)
# Nếu image gốc chạy với user 'crawlab', hãy dùng dòng sau:
# USER crawlab
# Nếu không chắc, bạn có thể bỏ qua dòng USER này, hoặc kiểm tra user của image gốc.
# Nhiều image crawlab chạy mặc định bằng root.

# Thiết lập thư mục làm việc (nếu cần, thường image gốc đã có)
# WORKDIR /app

# Lệnh CMD/ENTRYPOINT sẽ được kế thừa từ image base `crawlabteam/crawlab`