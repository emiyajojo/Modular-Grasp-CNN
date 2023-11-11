# Modular Anti-noise Deep Learning Network for Robotic Grasp Detection Based on RGB Images
[Paper](https://doi.org/10.48550/arXiv.2310.19223)

<img 
    src="Pics\Figure2.png"
    alt="The architecture of the whole network"/>
This repository is the implementation of the network in this [paper](https://doi.org/10.48550/arXiv.2310.19223).
## Setup and install
This project was tested on Linux and Windows and they are both feasible for this porject. The main system requirements I used are as followed:
- CUDA 11.7
- Linux(Ubuntu 20.04.1) with GCC 9.4.0
- Pytorch 1.13.1

To setup the whole network:
```shell
git clone https://github.com/emiyajojo/Modular-Grasp-CNN.git
cd Modular-Grasp-CNN
pip install -r requirements.txt
python setup.py install
```

## Test and train
All the model files, pretrained models(ResNet) and data with different noises could be downloaded throught this link: https://pan.baidu.com/s/1ohesaTpXwUcn3TYcxc1lfA?pwd=15kh.

There are three kinds of noises in the datasets(`All_DATA.zip`). DATA is the one with no noise, DATA_Gau is the one with Guassian noise and DATA_SP is the one with salt-and-pepper noise. Unzip the All_DATA.zip and choose one of datasets below the project directory(`MODULAR-GRASP-CNN/`) and **rename the dataset you choose as 'DATA'**(instead of DATA_SP or DATA_Gau). 

Put the pretrained ResNet models(unzip the `weights_pretrained.zip` and you can see) in the `weights_pretrained/` directory.

Put the checkpoint files of the network(unzip `ckpt_files_OCID.zip` and you can see) in the `ckpt_files_OCID/` directory.
### Test
```shell
cd .\scripts
python -m torch.distributed.launch --nproc_per_node=1 test.py
--local_rank=0 --log_dir log
--config grasp_det_seg\config\defaults\det_seg_OCID.ini
--model ckpt_files_OCID\pretrained\model_last.pth.tar
--data DATA\data_split
--out_dir results
```

### Train
```shell
cd .\scripts
python -m torch.distributed.launch --nproc_per_node=1 train.py
--local_rank=0 --log_dir log
--config grasp_det_seg\config\defaults\det_seg_OCID.ini
--pre_train ckpt_files_OCID\pretrained\model_last.pth.tar
--data DATA\data_split
--out_dir results
```

## Citation
```latex
@misc{li2023modular,
      title={Modular Anti-noise Deep Learning Network for Robotic Grasp Detection Based on RGB Images}, 
      author={Zhaocong Li},
      year={2023},
      eprint={2310.19223},
      archivePrefix={arXiv},
      primaryClass={cs.CV}
}
```




