# Anchal-Pathak-VTO
 Leverage existing virtual try-on models like CAT-VTON or IDM-VTON to create a simple virtual  try-on application using a dataset from Hugging Face. The goal is to understand the  implementation of state-of-the-art virtual try-on models and adapt them using publicly available  datasets
# Clone repo for IDM-VTON #
%cd /content
!git clone -b dev https://github.com/camenduru/IDM-VTON-hf
%cd /content/IDM-VTON-hf

!apt -y install -qq aria2
!aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/camenduru/IDM-VTON/resolve/main/densepose/model_final_162be9.pkl -d /content/IDM-VTON-hf/ckpt/densepose -o model_final_162be9.pkl
!aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/camenduru/IDM-VTON/resolve/main/humanparsing/parsing_atr.onnx -d /content/IDM-VTON-hf/ckpt/humanparsing -o parsing_atr.onnx
!aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/camenduru/IDM-VTON/resolve/main/humanparsing/parsing_lip.onnx -d /content/IDM-VTON-hf/ckpt/humanparsing -o parsing_lip.onnx
!aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/camenduru/IDM-VTON/resolve/main/openpose/ckpts/body_pose_model.pth -d /content/IDM-VTON-hf/ckpt/openpose/ckpts -o body_pose_model.pth

!pip install -q diffusers==0.25.0 accelerate==0.26.1 einops==0.7.0 onnxruntime==1.16.2 cloudpickle omegaconf gradio==4.24.0 fvcore av config
!pip install -r requirements.txt
# Clone repo for Cat-VTON #
!git clone https://github.com/Zheng-Chong/CatVTON.git
%cd CatVTON
!pip install -r requirements.txt

#Clone the VITON Dataset #
%cd /content
!git clone https://github.com/shadow2496/VITON-HD.git
%cd VITON-HD

#  Install Dependencies
!pip install opencv-python torchgeometry

#  Download the VITON-HD dataset from DropBox
!wget https://www.dropbox.com/s/10bfat0kg4si1bu/zalando-hd-resized.zip?dl=0 -O zalando-hd-resized.zip

