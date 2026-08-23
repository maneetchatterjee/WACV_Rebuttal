The above repo can be run by installing the requirements.txt as attached. 

ENVIRONMENT INFORMATION
------------------------------------
OS                : Linux-5.15.0-160-generic-x86_64-with-glibc2.35
Architecture      : x86_64
Kernel            : 5.15.0-160-generic
Python            : 3.10.12 [GCC 11.4.0]
NVIDIA-SMI 535.274.02             
Driver Version: 535.274.02   
CUDA Version: 12.2 
PyTorch           : 2.5.1+cu121
PyTorch CUDA      : 12.1

--- Python packages ---
torchvision       : 0.20.1+cu121
torchaudio        : 2.5.1+cu121
timm              : 1.0.28
numpy             : 1.23.5
Pillow            : 12.2.0
OpenCV            : 4.11.0
scikit-image      : 0.25.2
scikit-learn      : 1.7.2
scipy             : 1.10.1
transformers      : 4.49.0
einops            : 0.8.2
fairscale         : 0.4.13
Augmentor         : 0.2.12

--- pip ---
pip 26.1.2 

--- Conda ---
conda 4.14.0

To run the repo/individual codebases for PipNet, ProtoConcept and TesNet do the following:

1. PipNet:

DATASET=<dataset_name>

DATA_PATH=<path_to_dataset>

export PYTORCH_CUDA_ALLOC_CONF=expandable_segments:True

DATASET=<dataset_name> DATA_DIR=<path_to_dataset> GPU=0 \
RUN_NAME=pipnet_colon_dino_vitb16_224_ep30 \
EPOCHS=30 EPOCHS_PRETRAIN=5 FREEZE_EPOCHS=5 BATCH_SIZE=48 NUM_WORKERS=12 \
EXTRA_ARGS="--no_redirect_output --tf32 --skip_pretrain_vis" \
  nohup bash run_pipnet_dino.sh > pip_colon_ep30.log 2>&1 &

2. ProtoConcepts:

DATASET=<dataset_name>

DATA_PATH=<path_to_dataset>

export PYTORCH_CUDA_ALLOC_CONF=expandable_segments:True

DATASET=<dataset_name> DATA_DIR=<path_to_dataset> GPU=1 \
PC_TF32=1 PC_VIS_SAVE_IMAGES=0 PC_SAVE_TARGET_ACCU=0.0 \
PC_TRAIN_BATCH=48 PC_TEST_BATCH=64 PC_NUM_WORKERS=8 PC_PREFETCH=2 \
PC_EPOCHS=30 PC_WARM_EPOCHS=5 PC_LR_STEP=8 \
  nohup bash run_protoconcepts_dino.sh > pc_colon_ep30.log 2>&1 &

3. TesNet:

DATASET=<dataset_name>

DATA_PATH=<path_to_dataset>

export PYTORCH_CUDA_ALLOC_CONF=expandable_segments:True

DATASET=<dataset_name> DATA_DIR=<path_to_dataset> GPU=2 TIMES=ep30 \
TN_EPOCHS=30 TN_WARM_EPOCHS=5 TN_PUSH_START=10 TN_PUSH_EVERY=10 \
TN_LR_STEP=8 TN_TRAIN_BATCH=48 TN_SAVE_TARGET_ACCU=0.0 \
  nohup bash run_tesnet_dino.sh > tn_colon_ep30.log 2>&1 &


