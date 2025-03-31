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
RUN git clone https://github.com/TMElyralab/comfyui-save-image-with-meta /app/custom_nodes/comfyui-save-image-with-meta
RUN git clone https://github.com/ltdrdata/ComfyUI_IPAdapter_plus /app/custom_nodes/ComfyUI_IPAdapter_plus
RUN git clone https://github.com/WASasquatch/ComfyUI-Custom-Scripts /app/custom_nodes/ComfyUI-Custom-Scripts
RUN git clone https://github.com/ltdrdata/ComfyUI-Impact-Pack /app/custom_nodes/ComfyUI-Impact-Pack
RUN git clone https://github.com/Kosinkadink/ComfyUI-KJNodes /app/custom_nodes/ComfyUI-KJNodes
RUN git clone https://github.com/givenchan/ComfyUI_essentials /app/custom_nodes/ComfyUI_essentials
RUN git clone https://github.com/dustysys/ComfyUI-Advanced-ControlNet /app/custom_nodes/ComfyUI-Advanced-ControlNet
RUN git clone https://github.com/ltdrdata/ComfyUI-Impact-Subpack /app/custom_nodes/ComfyUI-Impact-Subpack
RUN git clone https://github.com/BadCafeCode/ComfyUI-tensorop /app/custom_nodes/ComfyUI-tensorop
RUN git clone https://github.com/Kijai/ComfyUI-Florence2 /app/custom_nodes/ComfyUI-Florence2
RUN git clone https://github.com/Fannovel16/comfyui_controlnet_aux /app/custom_nodes/comfyui_controlnet_aux
RUN git clone https://github.com/rgthree/rgthree-comfy /app/custom_nodes/rgthree-comfy
RUN git clone https://github.com/Thr33HeadedMonkey/ComfyUI-segment-anything-2 /app/custom_nodes/ComfyUI-segment-anything-2

EXPOSE 8188
CMD ["python", "main.py", "--listen"]
