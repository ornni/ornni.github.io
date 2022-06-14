---
layout: single
title:  "SVM multiclass OvR, OvO code"
---

```python
# import libraries
from sklearn.datasets import fetch_openml
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score, confusion_matrix
from sklearn.svm import SVC
import matplotlib.pyplot as plt
```

MNIST datset을 불러온 후 각각의 방법으로 적용해보자<br>

MNIST datset을 훈련데이터:테스트데이터=7:3으로 분류한다.


```python
# data import, preprocessing
mnist=fetch_openml('mnist_784', version=1)
print(list(mnist))
x, y=mnist['data'], mnist['target']

x_train, x_test, y_train, y_test = train_test_split(x, y, train_size=0.7)
```

    ['data', 'target', 'frame', 'categories', 'feature_names', 'target_names', 'DESCR', 'details', 'url']
    

---
### OvR


```python
# OVR
from sklearn.multiclass import OneVsRestClassifier

ovr_model=OneVsRestClassifier(SVC())
ovr_model.fit(x_train, y_train)

ovr_y_pred=ovr_model.predict(x_test)
ovr_y_true=y_test
```


```python
# OVR accuracy
ovr_acc=accuracy_score(ovr_y_true, ovr_y_pred)
ovr_acc
```




    0.9780952380952381




```python
# OVR confusion matrix
ovr_con_mat=confusion_matrix(ovr_y_true, ovr_y_pred)
ovr_con_mat
```




    array([[2022,    0,    2,    0,    1,    2,    7,    0,    4,    1],
           [   0, 2295,    8,    2,    5,    0,    1,    2,    2,    2],
           [   6,    2, 2067,    6,    7,    0,    0,   14,    8,    2],
           [   2,    1,   24, 2075,    0,   15,    0,   12,    9,    7],
           [   1,    7,    2,    0, 2042,    1,   14,    4,    6,   21],
           [   7,    2,    4,    9,    4, 1843,   11,    1,    9,    5],
           [   2,    0,    2,    0,    4,    8, 2000,    0,    1,    0],
           [   2,   11,   11,    1,    9,    1,    2, 2134,    4,   10],
           [   2,   10,    4,   12,    4,    4,    8,    0, 2029,    8],
           [   8,    3,    2,   13,   15,    6,    0,   21,   10, 2033]],
          dtype=int64)




```python
plt.matshow(ovr_con_mat, cmap=plt.cm.gray)
plt.show()
```


    
![OvR](https://github.com/ornni/Classification/blob/main/SVM/image/output_7_1.png?raw=true)
    


---
### OvO


```python
# OVO
from sklearn.multiclass import OneVsOneClassifier

ovo_model=OneVsOneClassifier(SVC())
ovo_model.fit(x_train, y_train)

ovo_y_pred=ovo_model.predict(x_test)
ovo_y_true=y_test
```


```python
# OVO accuracy
ovo_acc=accuracy_score(ovo_y_true, ovo_y_pred)
ovo_acc
```




    0.9774761904761905




```python
# OVO confusion matrix
ovo_con_mat=confusion_matrix(ovo_y_true, ovo_y_pred)
ovo_con_mat
```




    array([[2017,    0,    3,    0,    2,    2,    8,    1,    5,    1],
           [   0, 2295,    7,    3,    5,    0,    1,    1,    3,    2],
           [   5,    2, 2065,    6,    7,    1,    2,   15,    7,    2],
           [   2,    4,   23, 2062,    2,   17,    0,   11,   16,    8],
           [   3,    5,    3,    0, 2042,    1,   11,    3,    6,   24],
           [   5,    2,    4,   11,    3, 1846,   11,    0,    9,    4],
           [   3,    0,    3,    0,    4,   10, 1995,    0,    2,    0],
           [   1,    8,    9,    0,    9,    1,    2, 2141,    5,    9],
           [   2,    9,    3,   10,    6,    9,    7,    0, 2025,   10],
           [   6,    3,    1,    6,   18,    7,    0,   20,   11, 2039]],
          dtype=int64)




```python
plt.matshow(ovo_con_mat, cmap=plt.cm.gray)
plt.show()
```


    
![OvO](https://github.com/ornni/Classification/blob/main/SVM/image/output_12_1.png?raw=true)
    
