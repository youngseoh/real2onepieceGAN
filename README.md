## Project 소개

Cartoon GAN을 활용하여 실제 사진을 ‘OnePiece’ Cartoon 스타일의 이미지로 변환 

## Contributors

BITamin 12기 김재원, 송용호, 황영서

## Reference Paper

Paper :

[openaccess.thecvf.com](https://openaccess.thecvf.com/content_cvpr_2018/papers/Chen_CartoonGAN_Generative_Adversarial_CVPR_2018_paper.pdf)

Paper Review : 

[[Paper Review] CartoonGAN: Generative Adversarial Networks for Photo Cartoonization](https://velog.io/@youngseoh6/Paper-Review-CartoonGAN-Generative-Adversarial-Networks-for-Photo-Cartoonization)

## Image Data 수집

### 1. Real Image (10,000장)

- **Flick 30k Dataset 에서 10k장만 추출해서 사용**

[Flick 30k Dataset](https://www.kaggle.com/datasets/adityajn105/flickr30k)

- Center crop ( 1280x840 → 256x256 )

### 2. Cartoon Image (9,728장)

- Movie 1 - One Piece: The Movie ( 50m ) , Movie 2 - One Piece: Clockwork Island Adventrue (55m) ,
Movie 3 - One Piece: Chopper Kingdom of Strange Animal Island (55m) , 
Movie 8 - One Piece: Adventure In Alabasta (90m) , 
Movie 9- One Piece: Episode of Chopper Plus (113m) ,
Movie 10 - One Piece: Strong World (115m) , Movie 12 - One Piece: FilmZ (107m) , 
Movie 14: One Piece: Stampede (101m)
→ 총 681m ( 약 11hr 30min ) 에서 scenedetect 를 활용하여, 장면 당 3개의 이미지 총 9,728장 추출

[Watch One Piece: The Movie 12 - Film Z English Sub/Dub online Free on HiAnime.to](https://hianime.to/watch/one-piece-the-movie-12-film-z-299?ep=58165)

- Center crop ( 1280x840 → 256x256 ) , Edge Smoothing

## Experiments

### 1. CartoonGAN 변형

- Generator에 사용되는 ResNet Block에서 batchnoramalization 도입 과 residual connection 이후에 ReLU가 적용되는 구조로 변경
- Generator Upsampling 에서, blurring 과 batch normalization 사용
- Content Loss 에서 , VGG19 -> VGG16 로 변경하고, VGG16 의 24번째 layer 까지만 가져와서 feature extractor로 사용

### 2. Train

- Real image 의 content 를 유지하기 위해서 Generator를 pretrained 함
- 1) Discriminator cartoon image에 대하여 1, generate image 0, cartoon edge smooth 0, 나오게 train 시킴
  2) Generator generator image 를 Discriminator 에 나온 결과가 1이 되도록 + real image 의 content 를 유지하도록 train 시킴

## Results
![image](https://github.com/youngseoh/real2onepieceGAN/assets/100707876/73b73a28-7f25-47a1-b067-78aace12cb1d)
