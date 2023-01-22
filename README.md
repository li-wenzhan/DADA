# DADA
This repository stores the code for our dual-alignment domain adaptation method.

## Model
### Setup
**Environment**
All models were trained and tested on Ubuntu 18.04 with Python 3.7.0 and PyTorch 1.11.0 with CUDA 11.3.
You can start by creating a conda virtual environment:
```
conda create --name dada python=3.7 -y
source activate dada
pip install -r requirements.txt
```

**Dataset**
<br>Preprocessed [ETH](https://web.archive.org/web/20190715200622/https://vision.ee.ethz.ch/datasets_extra/ewap_dataset_full.tgz) and [UCY](https://graphics.cs.ucy.ac.cy/research/downloads/crowd-data) datasets are included in this repository, under `./datasets`. 
Among these datasets, `train_origin`, `val` and `test` are obtained directly from the ETH and UCY datasets, and `train` is obtained after the DLA processing.

### Training
**Data-alignment**
First, the DLA network needs to be trained: 
```
python train_DLA.py  --subset <task_S2T>
```
For example:
```
python train_DLA.py  --subset A2B
```

**Data process for FLA**
Next, you need to do pre-processing on the transformed data for FLA :
```
cd tools/FLA/experiments/pedestrian
python process_data.py
```

**Feature-alignment**
Finally, the FLA network training is run through the following:
```
python train_FLA.py --subset <task_S2T>
```
For example:
```
python train_FLA.py --subset A2B
```

### Pretrained Models
We have included pre-trained models in `./tools/FLA/experiments/saved_models/` folder that can be directly used to evaluate models.

### Evaluation
You can simply view the evaluation results for a certain task by running:
```
python test.py --subset <task_S2T>
```
For example, you can obtain the evaluation results for the A2B task this way:
```
python test.py --subset A2B
```

### Acknowledgement
Part of our code is borrowed from [Trajectron++](https://github.com/StanfordASL/Trajectron-plus-plus). 
We thank the authors for releasing their code and models.