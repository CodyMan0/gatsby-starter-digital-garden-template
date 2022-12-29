## 서버란 :  무언가를 제공해주는 컴퓨터

- 서버가 터졌다? 
1. 수강 신청 대기열이 뜨는 이유 : ==CPU의 사양==이 초당 100번의 계산 이상의 계산이 이루어질때!!! 
2. 실행 중이던 프로그램이 의도치 않게 종료되어 운영이 안되는 상황
3. 접근을 할 수 없는 상황등을 의미합니다. 

- 서버를 운영하는 두가지 방법 
1. 전통적인 방식 : 온 프레미스
	직접 하드웨어 관리를 하다보면 문제가 많다. 천재지변에 약하고 비용측면에 약하고 교체가 어렵다 . 그래서 **클라우드 컴퓨텅의 환경**으로 변경
2. 핫한 : 클라우드 컴퓨팅 
	직접 관리하지 않고 클라우드 컴퓨팅을 사용하는 것. 하지만 이것도 온 프레미스 기반이다. 

## 클라우드 컴퓨팅의 구분 
1. IaaS (Infrasturcture as a Service)
	쉽게 말하면 그냥 컴퓨터 한대 빌린 것 . 제어권 높지만 일일이 구성하고 관리해줘야 한다는 단점.
	ex) EC2
2. PaaS (Platform as a Service)
	infra위에 플랫폼을 얹으면 paaS, 플랫폼에 종속적이 될 수 있다는 단점!!!
	ex) AWS Elastic beanStalk, Heroku, Github Pages
3. SaaS


CRA도 CSR이어서 정적인 파일! 
Next.js 는 SSR는 동적인 파일!! 


-> CRA를 S3로 베포하는 과정! 
### 버킷 정책
sid: id 부여 

Principal : "*",  //아무나
Action : "s3:GetObject", //s3를
Resource : "" //버킷 안에 있는 모든 파일

```
{ "Version": "2012-10-17", "Statement": [ { "Sid": "PublicReadGetObject", "Effect": "Allow", "Principal": "*", "Action": "s3:GetObject", "Resource": "arn:aws:s3:::<bucket-name>/*" } ] }
```