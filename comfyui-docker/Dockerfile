FROM python:3.10-slim

# System deps
RUN apt-get update && apt-get install -y git wget && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Clone ComfyUI
RUN git clone https://github.com/comfyanonymous/ComfyUI.git .

# Install PyTorch + torchvision (CUDA 11.8)
RUN pip install --upgrade pip && pip install torch==2.0.1 torchvision==0.15.2 --index-url https://download.pytorch.org/whl/cu118

# Install ComfyUI dependencies
RUN pip install -r requirements.txt

# Custom Nodes
RUN git clone https://github.com/kijai/ComfyUI-Hunyuan3DWrapper /app/custom_nodes/ComfyUI-Hunyuan3DWrapper && \
    git clone https://github.com/ltdrdata/ComfyUI-Manager /app/custom_nodes/ComfyUI-Manager

# Copy model list and download them into appropriate folders
COPY models.txt /app/models.txt
RUN mkdir -p /app/models && \
    while IFS=' ' read -r folder url; do \
        mkdir -p "/app/models/$folder" && \
        wget -P "/app/models/$folder" "$url"; \
    done < /app/models.txt

EXPOSE 8188
CMD ["python", "main.py"]
