# 01. Bcrypt (단방향키의 한계를 합쳐서 사용하는 대표적 예가 bcrypt)

---

## 1-1. Salting & Key Stretching

단방향 암호화에 사용되는 해시 알고리즘은 동일한 평문에 대해서 항상 동일 해시값을 갖습니다. 따라서 특정 해시 알고리즘에 대해서 어떠한 평문이 어떤한 해시값을 갖는지 알 수가 있습니다.  
  

또한 해시 함수의 본래 빠르게 데이터를 검색하기 위해서 탄생 되었습니다. 따라서 공격자는 매우 빠른 속도로 임의의 문자열의 해시값과 해킹할 대상의 해시값을 비교하여 대상자를 공격할 수 있습니다.  
  

이런한 문제를 보안하기 위해 단방향 암호화를 진행할 때 솔팅(Salting)과 키 스트레칭(Key Stretching)을 적용 시킵니다.  
  

### 1-1-1. 솔팅(Salting)

솔팅은 단방향 해시 함수를 통해 암호화를 진행 할 때 본래 데이터에 추가적으로 랜덤한 데이터를 더하여 암호화를 진행하는 방식입니다. 원래 데이터에 추가 데이터가 포함 되었기 때문에 원래 데이터의 해시값과 다르게 됩니다.  
  

### 1-1-2. 키 스트레칭(Key Stretching)

단방향 해쉬값을 계산 한 후, 그 해쉬값을 또 다시 해시하고 또 이를 반복하는 방식입니다.

최근에는 일반적인 장비로 1초에 50억 개 이상의 해시값을 비교할 수 있지만, 키 스트레칭을 적용하여 동일한 장비에서 1초에 5번 정도만 비교할 수 있습니다. GPU(Graphics Processing Unit)를 사용하더라도 수백에서 수천 번 정도만 비교할 수 있습니다.

![session img](https://api-media-storage.s3.amazonaws.com/session-media/50c6a94af23e4c1eaa32a082acab38a4?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIASTLUR2MM6KMJSBGX%2F20220808%2Fap-northeast-2%2Fs3%2Faws4_request&X-Amz-Date=20220808T013554Z&X-Amz-Expires=60&X-Amz-SignedHeaders=host&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEKL%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaDmFwLW5vcnRoZWFzdC0yIkcwRQIgar9A3ptbIR7HYb85W%2Bun2vwh4FuellMys%2Fq1LNzviL8CIQCZx%2BeU1HZUUkpMvwjuSlMODeccAJBfGFuNKAEa1kEjuSr0Agj7%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAQaDDE3OTAyMjQ1MTQ4MSIMdJtiy5MUq5qaU2DKKsgChSMbre6sbojLHfHnD9dc0cYu6Tq9Sqw7gB4T9YnSVsw%2F95uvC49O4eD9Icupl50V9YELpadFVn%2B9zslnR39wk2ehLQ7BCb9KevM0Ucqr9scneW2E55YpoIpZcUpKrO7RWnKG7jQ5aWJSUB7d0yWDO4jsobTPKM9GU%2FI8Cudeivn%2BP5aLLtGTANbhRGl%2FyIdo926yrgTH2aw8wExr%2BOD7erJ79ei2J3nsUo17QgYpRlE7LiEH9rq0V8hjPWWEJtODi%2ByhGpEg5UsWXkdfR8idrX55%2B1xuclYRtF0QfNiHv0beKfZ%2BaJ%2Bq7LnQby1S0w%2FbRWbKPZ4xiYWlBRG5Iq9a9fKKN2miyTnAo9N2uQ%2B8G7uWtYDodTUxM8wQ1eFZLI9KU3Sm5fciQnM9xpBBycs1scbHx9G8Ik0ba5YgbDroVQX2uM7GK0hqNDDL0MGXBjqeAQ0jDD2tqZOgbkNmkf5%2Ftp5fOSV6Ms5uUGwALaq2Xgg4S%2BW3A1lKFMLNhWT2fHtCr6SEqIs41M4JXBCW2dkkgxz99Tz2lmbTDYbbCERBgcXw5P6AsDkXQ5UTheDCcv40E1je6GgKSlGDJbFrMNpD1CNwTbRx9Jb3t6zimL%2F7zM8d2njn35gnXpZUdOr81jzHE2isvZlxY4cCJ2oUhy52&X-Amz-Signature=53ceec705162c64d052cb068e09b3154136166a99235d5eaa12c382faa38f2f2)

[그림 1-1] Salting & Key Stretching  
  

## 1-2. Bcrypt 란?

**Bcypt**는 브루스 슈나이어가 설계한 키(key) 방식의 대칭형 블록 암호에 기반을 둔 암호화 해시 함수로서 Niels Provos 와 David Mazières가 설계했습니다. ==Bcrypt는 레인보우 테이블 공격을 방지하기 위해 솔팅과 키 스트레칭을 적용한 대표적인 예== 입니다.  
  

### 1-2-1. 구조

`$2b$12$76taFAFPE9ydE0ZsuWkIZexWVjLBbTTHWc509/OLI5nM9d5r3fkRG  \/ \/ \____________________/\_____________________________/ Alg Cost       Salt                        Hash`

-   `2b` : 해시 알고리즘 식별자
-   `12` : Cost Factor로 Key Stretching의 수 (2의 12승번)
-   `76taFAFPE9ydE0ZsuWkIZe` : 16Byte 크기의 Salt, Base64로 인코딩된 22개의 문자
-   `xWVjLBbTTHWc509/OLI5nM9d5r3fkRG` : 24Byte의 해시 값, Base64로 인코딩된 31개의 문자  
      
    

### 1-2-2. 검증

Bcrypt는 ==단방향 해시 알고리즘 입니다. 따라서 복호화가 불가능 합니다.== Bcrypt의 검증은 암호화된 값이 가지고 있는 알고리즘, Cost Factor, Salt를 이용 합니다. 비교하고 싶은 평문을 암호화된 값이 가지고 있는 알고리즘, Cost Factor, Salt을 이용하여 해시를 진행한 후 암호화된 값과의 비교를 통해 검증을 진행 합니다.

# 2. Summary

---

-   단방향 암호화는 해시 알고리즘을 기반으로 만들어졌습니다.
-   해시 알고리즘의 단점을 보완하기 위해 단방향 암호화에 솔팅(Salting)과 키 스트레칭(Key Stretching) 기술을 적용 시킵니다.
-   Bcrypt는 레인보우 테이블 공격을 방지하기 위해 솔팅과 키 스트레칭을 적용한 대표적인 예 입니다.
-   Bcrypt는 단방향 해시 알고리즘이기 때문에 복호화가 불가능 합니다. 따라서 비교하고 싶은 평문을 암호화된 값이 가지고 있는 알고리즘, Cost Factor, Salt을 이용하여 해시를 진행한 후 암호화된 값과의 비교를 통해 검증을 진행합니다

[[crypt]],[[단방향키]]