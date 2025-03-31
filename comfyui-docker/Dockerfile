FROM pytorch/pytorch:2.0.1-cuda11.8-cudnn8-runtime

# System deps
RUN apt-get update && apt-get install -y git wget && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Clone ComfyUI
RUN git clone https://github.com/comfyanonymous/ComfyUI.git .

# Install ComfyUI dependencies
RUN echo "📦 Installing ComfyUI Python dependencies..."
RUN pip install -r requirements.txt

# Custom Nodes
RUN echo "🔧 Cloning custom nodes..."
RUN git clone https://github.com/kijai/ComfyUI-Hunyuan3DWrapper /app/custom_nodes/ComfyUI-Hunyuan3DWrapper && \
    echo "🔧 Cloning custom nodes..." && \
    git clone https://github.com/ltdrdata/ComfyUI-Manager /app/custom_nodes/ComfyUI-Manager

EXPOSE 8188
CMD ["python", "main.py", "--listen"]
