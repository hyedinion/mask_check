# mask detect device
건물 출입구에 있는 마스크 감지 및 온도측정 카메라를 구현한다.

### 컴포넌트
- yoloV5
- raspberryPi
- AMG8833 (열화상 센서)
- camera

### clone
- yoloV5 -> `git clone https://github.com/ultralytics/yolov5.git`<br>
- AMG8833 -> `https://m.youtube.com/watch?v=rqdTx0AKroE&feature=emb_logo&ab_channel=DeviceMart`

### 디렉토리 설명
1. mask_check
> `thermal_sensor와 yolov5를 합친 최종 코드`
2. thermal_sensor
> `열화상 카메라 테스트`
3. yolov5
> `yolov5 테스트`

### 실행방법
mask_check > Adatruit_AMG88xx_python > examples <br>
```python
python3 detect.py --source 0 --weights Sbest.pt --conf 0.5 --img 160
```
----
## yoloV5 속도 높이기
1. yoloV5 모델 중 FPS(초당프레임 수)가 제일 작은 YOLOv5s모델로 학습을 한다.
- s모델이 제일 빠른대신 제일 정확도가 떨어진다.
- L모델과 비교했을 경우 12s -> 3s
2. 

----
# yoloV5 학습하는법

### kaggle dataSet
1. https://www.kaggle.com/andrewmvd/face-mask-detection/code
   에서 데이터 다운로드
2. 압축풀기
3. https://roboflow.com/convert/pascal-voc-xml-to-yolov5-pytorch-txt
   여기에 압축푼 폴더 넣어서 yolov5 dataset 만들기
4. 결과 
   !curl -L "https://app.roboflow.com/ds/GRqhDN6JhF?key=rSVNqFuNPu" > roboflow.zip; unzip roboflow.zip; rm roboflow.zip

### yoloV5 학습하기

### best.pt 성능 test
1. git clone https://github.com/ultralytics/yolov5.git
2. pip install -r requirements.txt
3. 압축푼 best.pt 파일 yolov5밑에 넣기
4. python detect.py --source 0 --weights best.pt --conf 0.5

---
# Git 충돌
git 폴더 안에 git clone을 했거나 다른 git 폴더가 들어있을 경우<br>
`You've added another git repository inside your current repository`<br>
라는 경고가 뜬다<br>

### 해결법
1. 충돌이 나는 폴더로 들어가 `ls -a` 로 .git 파일이 있는지 확인한다.
2. `rm -rf .git` .git 파일을 지운다
3. `git rm --cached . -rf` 스테이지에 있는 파일을 지운다.
4. add commit push 한다
5. 만약 github에서 화살표모양의 디렉토리가 보이고 클릭이 되지 않는다면 그 폴더에서 다시 위 단계를 반복한다.

### 1MB이상 파일 올리기
에러메세지
- `fatal: The remote end hung up unexpectedly`
개별 파일의 최고 용량을 늘려준다.
- `git config --global http.postBuffer 20971520`
출처: https://crmn.tistory.com/58 [크롬망간이 글 쓰는 공간]
