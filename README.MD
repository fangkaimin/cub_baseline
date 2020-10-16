# CUB_200_2011 FGCV baseline

# pretrain model
resnest50 -> 75.58%


数据增强方法:
```
transforms.Resize((self.BASE_RESIZE_SIZE, self.BASE_RESIZE_SIZE), Image.BILINEAR),
                transforms.RandomCrop(self.INPUT_SIZE),
                transforms.RandomHorizontalFlip(),
                transforms.RandomRotation(degrees=15),
                transforms.ColorJitter(brightness=self.BRIGHTNESS, contrast=self.CONTRAST, hue=self.HUE, saturation=self.SATURATION),
                transforms.ToTensor(),
                self.imagenet_normalization_paramters
```

学习率:
> 0.1初始化，不进行warmup 90个epoch，0.3, 0.6, 0.9 * epoch 按ratio=0.1进行线性衰减

### performance

|model|accuracy|
|:---:|:---:|
|resne50(baseline)256->224|76.47%|
|resnet50(baseline)512->448|84.55%|
|efnet-b0 256->224| 77.93%|
|efnet-b1 272->240| 79.63%|
|efnet-b2 292->260| 81.22%|
|efnet-b3 352->300| 83.12%|
|efnet-b4 416->380| 84.45%|
|efnet-b5 512->456| 85.64%|
|efnet-b6 600->528| 87.05%|
|efnet-b7 640->600| 88.11%|
<!-- |resnest50 256->224|| -->



### training
```bash train.sh```
其中，horovod可以指定几个node，对应的就是几块GPU

### test
```CUDA_VISIBLE_DEVICES=0 python test.py```


### pretrain download link

[cub_resnet50_08456](https://drive.google.com/file/d/1cl1GgHNaFzF9KNfGAkgaGveLinO-Yr9x/view?usp=sharing)



#### accvbaseline
|model|test acc|
|:---:|:---:|
|efnetb2 260| 41.975|
|resnet50 224|36.11|
|efnetb2+resnet50_224 ensemble1|43.105|
|efnetb3 300|	42.395|
|resnet50 448|	41.63|
|efnetb3+resnet50_448 ensemble2|	47.05|
|ensemble1+ensemble2|47.395|