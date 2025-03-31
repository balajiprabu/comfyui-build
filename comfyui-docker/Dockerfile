FROM pytorch/pytorch:2.0.1-cuda11.7-cudnn8-devel

# System deps
RUN apt-get update && apt-get install -y git wget build-essential ninja-build && rm -rf /var/lib/apt/lists/*

WORKDIR /app
ENV CUDA_HOME=/usr/local/cuda-11.7

# Clone ComfyUI
RUN git clone https://github.com/comfyanonymous/ComfyUI.git .

# Install ComfyUI dependencies
RUN echo "📦 Installing ComfyUI Python dependencies..."
RUN pip install -r requirements.txt

# Custom Nodes
RUN echo "🔧 Cloning custom nodes..."
RUN git clone https://github.com/kijai/ComfyUI-Hunyuan3DWrapper /app/custom_nodes/ComfyUI-Hunyuan3DWrapper

WORKDIR /app/custom_nodes/ComfyUI-Hunyuan3DWrapper
RUN pip install -r requirements.txt

WORKDIR /app

RUN git clone https://github.com/ltdrdata/ComfyUI-Manager /app/custom_nodes/ComfyUI-Manager
RUN git clone https://github.com/chrisgoringe/cg-use-everywhere /app/custom_nodes/ComfyUI-UseEverywhere-nodes
RUN git clone https://github.com/giriss/comfy-image-saver.git /app/custom_nodes/comfyui-save-image-with-meta
RUN git clone https://github.com/cubiq/ComfyUI_IPAdapter_plus /app/custom_nodes/ComfyUI_IPAdapter_plus
RUN git clone https://github.com/pythongosssss/ComfyUI-Custom-Scripts.git /app/custom_nodes/ComfyUI-Custom-Scripts
RUN git clone https://github.com/kijai/ComfyUI-KJNodes.git /app/custom_nodes/ComfyUI-KJNodes
RUN git clone https://github.com/cubiq/ComfyUI_essentials.git /app/custom_nodes/ComfyUI_essentials
RUN git clone https://github.com/Kosinkadink/ComfyUI-Advanced-ControlNet.git /app/custom_nodes/ComfyUI-Advanced-ControlNet
RUN git clone https://github.com/un-seen/comfyui-tensorops.git /app/custom_nodes/ComfyUI-tensorop
RUN git clone https://github.com/kijai/ComfyUI-segment-anything-2.git /app/custom_nodes/ComfyUI-segment-anything-2

# Log in to Docker Hub
RUN echo "${DOCKERHUB_TOKEN}" | docker login -u "${DOCKERHUB_USERNAME}" --password-stdin

# Tag and push to Docker Hub
RUN docker tag comfyui-custom docker.io/${DOCKERHUB_USERNAME}/comfyui-custom:latest
RUN docker push docker.io/${DOCKERHUB_USERNAME}/comfyui-custom:latest

EXPOSE 8188
CMD ["python", "main.py", "--listen"]
