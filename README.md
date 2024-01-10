### ✦ 목적
* 프로젝트 주제 : 이미지 인식을 통한 위조지폐 구별하기
* `딥러닝`, `CNN`, `이미지 인식 분류`
-----
### ✦ 과정 1
>* 프로젝트 기간 : 2023.12.06 ~ 2024.01.04 (1달) _ 과정 2 (개인 보완 기간) : 2024.01 ~ (wip)
>* 팀 인원 : 2인

* 데이터 수집
  * 직접 촬영 (원화 10,000권 진폐 6(180장) : 위폐 4(120장))
  * 진폐 (다양한 각도 & 접힘 활용) <br>
    <img width="867" alt="image" src="https://github.com/sooohyeonkim/Real-Fake-banknote/assets/146702973/ac96ae5c-fbd3-4ca5-a55b-ad2bbff4df9d">
  * 위폐 (조건 6종)<br>
    <img width="1076" alt="image" src="https://github.com/sooohyeonkim/Real-Fake-banknote/assets/146702973/4a5844b4-7b2c-486c-8108-c81c4cad93c7">
* 데이터 라벨링 : 0-위폐, 1-진폐
* 이미지 전처리<br>
  `ImageDataGenerator(rescale=1. / 256)`
* `CNN` 모델 학습<br>
  > `Xception`,`InceptionV3`,`InceptionResnetV2`,`EfficientNetB7`,`앙상블(VGG19,Resnet101,EfficientNetB7')`<br>
  
  <br>* `Xception`<br>
    이미지 증강 진행, Adam, lr=0.0001, Dropout=0.2, Earlystop=10
   ```python
   # 이미지 증강
  datagen = ImageDataGenerator(
    rotation_range=20, 
    width_shift_range=0.2, 
    height_shift_range=0.2,
    shear_range=0.2, 
    zoom_range=0.2, 
    horizontal_flip=True,
    fill_mode='nearest' 
    )
   ```
  <br>* `EfficientNetB7`<br>
    이미지 증강 진행(상동), Adam, lr=0.03, Dropout=0.2 & 0.5, Earlystop=20

  <br>* `앙상블(VGG19,Resnet101,EfficientNetB7')`<br>
    이미지 증강 진행(상동), Adam, lr=0.001, Dropout=0.5, Earlystop=10
-----
### ✦ 결과 1
> 전반적으로 예측을 잘하지 못함<br>
> 진폐 데이터와 위폐 데이터를 동일한 환경으로 다시 맞추고 진행 할 것<br>
> 데이터에서 지폐만 인식하는 OPEN CV로 데이터 전처리 추가 진행할 것

* `Xception`
  * Training Acc,Loss<br>
    <img width="300" alt="image" src="https://github.com/sooohyeonkim/Real-Fake-banknote/assets/146702973/2b094b9f-164f-4d84-b762-ec1d0f83a01d">
    <img width="300" alt="image" src="https://github.com/sooohyeonkim/Real-Fake-banknote/assets/146702973/6531618a-feaf-43e3-b9f2-c832a6150548">
  * Test<br>
    * ROC : 0.5443478260869565<br>
      <img width="300" alt="image" src="https://github.com/sooohyeonkim/Real-Fake-banknote/assets/146702973/443cdcb7-5767-4299-b326-54f55a511c52">
    * Report <br>
       <img width="300" alt="image" src="https://github.com/sooohyeonkim/Real-Fake-banknote/assets/146702973/d1e0a1aa-c170-4e2a-8114-878c0ec23e7a">

* `EfficientNetB7`<br>
  >위폐 인식률 0%<br>
    * Training Acc,Loss<br>
      <img width="300" alt="image" src="https://github.com/sooohyeonkim/Real-Fake-banknote/assets/146702973/d7117707-00e1-41ea-a99f-0be6622a0df9">
      <img width="300" alt="image" src="https://github.com/sooohyeonkim/Real-Fake-banknote/assets/146702973/c4e9bfd9-fd6f-4e4d-a04e-6932a81cece5">
  * Test<br>
    * ROC : 0.5<br>
      <img width="300" alt="image" src="https://github.com/sooohyeonkim/Real-Fake-banknote/assets/146702973/5271ac85-3364-48f3-9e47-c786b04aaef1">
    * Report<br>
      <img width="300" alt="image" src="https://github.com/sooohyeonkim/Real-Fake-banknote/assets/146702973/37375055-4e59-47b0-bdda-c65ce1f0e693">

* `앙상블(VGG19,Resnet101,EfficientNetB7')`<br>
  * Training Acc,Loss<br>
    <img width="600" alt="image" src="https://github.com/sooohyeonkim/Real-Fake-banknote/assets/146702973/fdb248f7-3a27-47ee-a25d-7d6569bc8cb8">
  * Test
    * ROC : 0.70 <br>
    <img width="300" alt="image" src="https://github.com/sooohyeonkim/Real-Fake-banknote/assets/146702973/eb6db5a2-a182-4bb0-8b05-72301d7b5b13"><br>
    * Report<br>
    <img width="300" alt="image" src="https://github.com/sooohyeonkim/Real-Fake-banknote/assets/146702973/99458f0e-643b-4f97-a557-9827ebe9145a">
-----
### ✦ 참고
- Fake Cards Detection using CNN (https://www.kaggle.com/code/maelbe/fake-cards-detection-using-cnn)
