# 피부색 베이지안 분류기

#### 기간 : 2018년 10월 (약 1개월) <br/>목적 : '컴퓨터응용확률' 수업 과제<br/>인원/역할 : 개인<br/>의의 : k-fold cross validation 구현, 베이지안 분류기 구현, Open CV 사용<br/>


#### 사용 언어 : Python <br/>구현 환경 : Visual Code 1.29.1

## Detail
#####  Data : 🔗[MIT 제공 사진, 얼굴 타원 좌표 text](http://vis-www.cs.umass.edu/fddb/index.html#download)
![Alt text](/20210304202153.png)
##### 얼굴 위치의 타원 좌표를 이용하여 타원 내의 RGB 값을 추출하고, 베이지안 공식을 이용하여 피부색인지 아닌지를 판단하는 프로그램
##### K-fold cross validation 기법을 이용하여 정확도 테스트, open CV 사용

##### partB_a,b는 베이지안 공식을 이용한 코드이고 <br/> partB_2_a,b는 가우시안 공식을 이용한 코드이다. <br/> partC는 k-fold crossvalidation으로 테스팅한 결과이다.


### 📌Cross Validation
##### Cross Validation은 교차검증으로 설계한 모델에 다른 데이터들이 잘 들어맞는지에 대한 성능을확인하는 방법이다. K-hold 교차검증은 데이터셋을 k로 나눠서 k개 중 한 개의 데이터셋을 testing 데이터로 사용하고 나머지 (k-1)/k 만큼의 데이터셋을 training 데이터로 사용한다. Training 데이터 셋을 분석하여 모델을 만들고 그 모델에 testing 데이터 셋을 대입하여 그 모델의 정확성에 대해 평가한다. 이런 시행을 k로 나눴을 때 k개의 각각의 데이터를 모두 testing 데이터로 사용하는 것이다.
##### 해당 프로젝트에서 K 값은 5로 설정했다.

### 📌Red 값으로만 판단한 결과
##### Precison : 0.2977716... <br/> Recall : 0.668312... <br/> Accuracy : 0.53851992... <br/> F1 : 0.411966...

### 📌RGB 값을 모두 사용하여 판단한 결과 
##### Precison : 0.70232092... <br/> Recall : 0.6887562... <br/> Accuracy : 0.7569198... <br/> F1 : 0.69546877...

### 📌베이지안 공식 사용
<pre><code>result1= reds1[int(sline[0])]*greens1[int(sline[1])]*blues1[int(sline[2])]*(count1/(count1+count2))
result2= reds2[int(sline[0])]*greens2[int(sline[1])]*blues2[int(sline[2])]*(count2/(count1+count2))
</code></pre>

##### result1은 피부색이고 red값이 해당 값(reds1[int(sline[0])])일 때, green와 blue 가 해당 값을 가질 확률<br/>result2는 피부색이고 red값이 해당 값(reds2[int(sline[0])])일 때, green와 blue 가 해당 값을 가질 확률<br/> result1이 result2보다 크면 피부색이라고 판단, result2가 더 크면 피부색이 아니라고 판단
