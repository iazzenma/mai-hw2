## Install Dependencies

```bash
pip install --extra-index-url https://download.pytorch.org/whl/cu118 torch torchvision torchaudio --upgrade
pip install transformers peft torchinfo tqdm matplotlib seaborn numpy scikit-learn datasets accelerate huggingface_hub ipykernel 
pip install ipywidgets>=8.0.0 notebook
```

## Task 1 Zero-Shot

Execute the `Task1.ipynb` notebook to perform zero-shot classification on the Oxford Flowers102 dataset and CUB-200-2011 dataset using the CLIP model.

## Task 2 Fine-Tuning CLIP

Execute the `Task2.ipynb` notebook to fine-tune the CLIP model on the Oxford Flowers102 dataset and CUB-200-2011 dataset. There are two fine-tuning methods implemented: linear probing and LoRA.

## Task 3 CoOp Training

First, clone the CoOp repository:

```bash
git clone https://github.com/KaiyangZhou/CoOp.git
cd CoOp
```

Then, install Dassl following the instructions [here](https://github.com/KaiyangZhou/Dassl.pytorch#installation). Also make sure to align the dataset structure as mentioned in the readme.

To train CoOp on the Oxford Flowers102 dataset using the ViT-L/14 model with full data, paste the files in `hw2_B11902008_code/CoOp/` into the `CoOp/` directory. The destination paths are as follows:

* `oxford_flowers_torchvision.yaml`  -> `configs/datasets/oxford_flowers_torchvision.yaml` 
* `vit_l14_fulldata.yaml` -> `configs/trainers/CoOp/vit_l14_fulldata.yaml`
* `oxford_flowers_torchvision.py` -> `datasets/oxford_flowers_torchvision.py`
* `train_fulldata_vit_l14.sh` -> `scripts/coop/train_fulldata_vit_l14.sh`
* `clip.py` -> `clip/clip.py`
* `coop.py` -> `trainers/coop.py`
* `train.py` -> `train.py`
* `plot_training_curve.py` -> `plot_training_curve.py`

Finally, run the training script:

```bash
bash scripts/coop/train_fulldata_vit_l14.sh
```

After training, you can plot the training curves by running:

```bash
python plot_training_curve.py
```

### Some Possible Issues

Following the instructions in Dassl's readme, I had encountered a issue where pytorch installation is the CPU-only version. To fix this:

```bash
pip uninstall -y torch torchvision
conda install -y pytorch torchvision pytorch-cuda=11.8 -c pytorch -c nvidia
```