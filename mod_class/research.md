## Data set의 Amplitude가 다른경우 test 정확도가 많이 차이나는가?

- 데이터 성능이 확연하게 차이났었다고 한다.
- Resizing  하면서 학습하는 내용을 추가적으로 적용할 필요가 있어보인다.
- Test data set의 amplitude가 Default Amplitude에 비해 차이가 많이 날수록 
정확도가 급격히 떨어진다.

IQ_0.25 : 0.17235615849494934  
IQ_0.5  : 0.17553584277629852  
IQ_0.75 : 0.2656000256538391  
**IQ_1 : 0.8030917644500732**  
IQ_1.25 : 0.6942843198776245  
IQ_1.5  : 0.6181277632713318  
IQ_1.75 : 0.5138458013534546  
IQ_2    : 0.3804713785648346

### Test files
- radioml_IQ_power_test.ipynb
- radioml_IQ_power_test_re.ipynb

---

## Channel이 Impulse일 경우 데이터 생성 후 성능 평가

**Impuse channel 환경**

18db로 데이터로  training  => 18db 데이터로 test  = 0.8
0db로 데이터로  training  => 0db데이터로 test  = 0.63
18db로 데이터로  training  => 0db 데이터로 test  = 0.74

**default channel 환경**

18db로 데이터로  training  => 18db 데이터로 test  = 0.65


---

## 6dB data set 만 가지고 Training하고 전체 dB에 대해서 test 할경우 성능 확인

6db dataset -> training
6db dataset test result :[loss, accuracy] = [0.78, 0.69]

6db dataset -> training
[-20,20] db dataset -> test
[-20,20] dataset test result :[loss, accuracy] = [5.01, 0.31]

### Test files
- radioml_IQ_power_test.ipynb

---

