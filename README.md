# PQ-NET
This repository provides PyTorch implementation of our paper:

[PQ-NET: A Generative Part Seq2Seq Network for 3D Shapes](https://arxiv.org/abs/1911.10949),

[Rundi Wu](https://chriswu1997.github.io), [Yixin Zhuang](http://www.yixin.io/), [Kai Xu](https://kevinkaixu.net/), [Hao Zhang](https://www2.cs.sfu.ca/~haoz/), [Baoquan Chen](http://cfcs.pku.edu.cn/baoquan/)

CVPR 2020



## Prerequisites

- Linux
- NVIDIA GPU + CUDA CuDNN
- Python 3



## Dependencies

Install python package dependencies through pip:

```bash
pip install -r requirements.txt
```

Compile the extension module brought from [Occupancy_Networks](https://github.com/autonomousvision/occupancy_networks):

```bash
python setup.py build_ext --inplace
```



## Data

TBA.



## Training

Example training scripts can be found in `scripts` folder. 

To train the main model:

```bash
# train part auto-encoder following multiscale strategy 16^3-32^3-64^3
sh scripts/lamp/train_lamp_partae_multiscale.sh # use two gpus 

# train seq2seq model
sh scripts/lamp/train_lamp_seq2seq.sh
```

For random generation task, further train a latent GAN:

```bash
# encode each shape to latent space
sh scripts/lamp/enc_lamp_seq2seq.sh

# train latent GAN (wgan-gp)
sh scripts/lamp/train_lamp_lgan.sh
```



## Testing

Example testing scripts can also be found in `scripts` folder. 

- __Shape Auto-encoding__

  After training the main model, run the model to reconstruct all test shapes:

  ```bash
  sh scripts/lamp/rec_lamp_seq2seq.sh
  ```

- __Shape Generation__

  After training the latent GAN, run latent GAN and the main model to do random generation:

  ```bash
  # run latent GAN to generate fake latent vectors
  sh scripts/lamp/test_lamp_lgan.sh
  
  # run the main model to decode the generated vectors to final shape
  sh scripts/lamp/dec_lamp_seq2seq.sh
  ```



## Pre-trained models

TBA.



## Cite

Please cite our work if you find it useful:

```
@misc{wu2019pqnet,
    title={PQ-NET: A Generative Part Seq2Seq Network for 3D Shapes},
    author={Rundi Wu and Yixin Zhuang and Kai Xu and Hao Zhang and Baoquan Chen},
    year={2019},
    eprint={1911.10949},
    archivePrefix={arXiv},
    primaryClass={cs.CV}
}
```

