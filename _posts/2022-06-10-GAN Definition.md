---
layout: single
title:  "GAN 개념정리"
---


GAN을 처음 접할 때 아래와 같은 그림을 이용해서 이해하면 편하다.

[![img](https://postfiles.pstatic.net/MjAyMjA2MDJfODUg/MDAxNjU0MTYxMjMzODI5.uaAv9CYcTj51b_zcJ4Vzb0oZvt1VEaFVaow9BBuRRuwg.uk8AXiTfTsH0sy7NLA4MW1Wp0oxuFrz4ylVFz9PIXi4g.JPEG.wogus951632/GAN.jpg?type=w773)]()

0과 1로 구성된 노이즈가 있다.

해당 노이즈를 갖고 위조지폐범이 위조지폐를 만든다.

경찰은 위조지폐와 실제 지폐를 구분한다. (위조지폐: 0, 실제 지폐: 1 출력)

이렇게 한번 경찰이 지폐를 구분하는 것이 하나의 epoch이 된다.



첫번째 epoch에서는 경찰이 위조지폐와 진짜 지폐를 잘 구분할지 몰라도 점차 위조지폐범은 더욱 비슷하게 생긴 위조지폐를 만들 것이고 경찰도 더 잘 구분하기 위해 노력할 것이다.

어느 순간 완벽한 위조지폐가 만들어지면 경찰은 해당 지폐를 잘 구분할 수 없어서 찍기 시작할 것이다.

확률은 진짜 혹은 가짜 중 하나이므로 50%가 되고 학습이 끝나게 된다.



위의 개념에서 아래와 같은 문자로 이해하면 된다.

노이즈: z

위조지폐범: Generator

경찰: Discriminator (위조지폐는 D(G(z))=0, 실제지폐는 D(G(z))=1 출력)



Discriminator 모델은 어떤 input 데이터가 들어갔을 때 해당 input 값이 어떤 것인지 classify하므로 지도학습이고 Generator 모델은 어떤 잠재적인 코드를 가지고 해당 데이터를 학습 데이터가 되도록 학습하는 과정이므로 비지도 학습이다.

------

이제 Discriminator와 Generator 입장에서 각각 GAN을 설명하도록 한다.

D의 입장

[![img](https://postfiles.pstatic.net/MjAyMjA2MDJfMjc2/MDAxNjU0MTYzNjM0MDA1.Va0q4P3oo6MBzbfJBHWXV6AwV9qcWfZI-fHrfZFLXvIg.Nn06nKNnQhHnjive_4nxkYk73niisa40X8YqmbE7WC0g.JPEG.wogus951632/D.jpg?type=w773)]()

Discriminator 모델이 진짜 이미지와 가짜 이미지를 가지고 진짜 가짜 여부를 구분하도록 학습한다.

따라서 들어가는 input은 G(z)와 x의 차원은 이미지의 경오와 같은 고차원 벡터가 들어갈지 몰라도 결국 나오는 output은 0과 1의 값을 가지게 된다.

(sigmoid 함수를 사용)

[![img](https://postfiles.pstatic.net/MjAyMjA2MDJfMzYg/MDAxNjU0MTYzNjYwMDA1.LZ0TlA_4EJHhltymyIevnIb5dibYIFbldZY1jEs2cN4g.tT4Cbyp5FVZ8S0zWI04eKL_4xOSZjBukAkw7ZeC_o-0g.JPEG.wogus951632/%EC%8B%9C%EA%B7%B8%EB%AA%A8%EC%9D%B4%EB%93%9C.jpg?type=w773)]()

G의 입장

[![img](https://postfiles.pstatic.net/MjAyMjA2MDJfMjEg/MDAxNjU0MTYzNzM1OTMx.jgP07hWj9ir7j4xPNUz3QqE0RmES133yyBFhs80f98wg.SxlVNrEvrObpmuAnv9HYCURiI9a0CyhHfEXuj_hvb8Yg.JPEG.wogus951632/G.jpg?type=w773)]()

Generator 입장에서는 Discriminator가 진짜 이미지를 잘 맞추는지는 관심이 없다.

단지 본인이 만든 이미지가 얼마나 Discriminator를 잘 속일 수 있는지가 중요하다.(D(G(z))=1이 되도록 함)

------

**목적함수(Objective function, Loss function)**

[![img](https://postfiles.pstatic.net/MjAyMjA2MDJfMjQz/MDAxNjU0MTYzNzQ5NDcz.lW2yf4dbstKw9o3TtR8sCQXs_-0mC4mKTV_FiD-snJog.XGJDe4_egJSWdJED_zBW3ik96QZ8Fajd4KWok7ZDpLcg.PNG.wogus951632/F.png?type=w773)]()

G는 V(D, G)가 최소가 되려고 하고 D는 V(D, G)가 최대가 되려고 한다.

---

D의 입장

[![img](https://postfiles.pstatic.net/MjAyMjA2MDJfODkg/MDAxNjU0MTYzNzYzODUx.FcUPab8pfULO3VBJqhTnFBmWvRRCvQFK6aIlxCdPmYAg.5C44XmzCOZBDSX9-b4xStosVnuhJVEArolapicOZF-0g.JPEG.wogus951632/DD.jpg?type=w773)]()

D는 경찰이다. 가짜 데이터에 0, 진짜 데이터에 1을 출력해야 한다.

x는 진짜 데이터이고 G(z)는 G가 z를 가지고 만든 가짜 데이터이다.

따라서 D(z)=1이 되어야 하며, D(G(z))=1이 되도록 하는 것이 목표이다.



G의 입장

[![img](https://postfiles.pstatic.net/MjAyMjA2MDJfMjMy/MDAxNjU0MTYzNzc1ODU1.yZCvENQYmD6Lr9IEusF1EdiDXeonbQxyPBYMSJrXg4Eg.kjZSgskp5IDVaqHA0EetZSBRDhafE4ksziZTxZu8hTcg.JPEG.wogus951632/GG.jpg?type=w773)]()

G는 위조지폐범이다. 경찰과 반대로 G는 D가 가짜 데이터에 대해 1을 출력하게 해야 한다.

D가 진짜 데이터를 제대로 구별하는지는 관심이 없다.

x는 진짜 데이터이고 G(z)는 G가 z를 가지고 만든 가짜 데이터이다.

따라서 D(x)=0이 되어야 하며, D(G(z))=1이 되도록 해야 한다.
