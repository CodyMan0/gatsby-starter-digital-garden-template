# 1. 운영 서버와 아키텍쳐

---

## 1-1. 운영 서버란?

애플리케이션을 개발할 때에는 주로 로컬 환경에서 개발 혹은 테스트를 진행합니다. 이렇게 로컬 환경에서 실행되는 애플리케이션은 사용자에게 서비스를 제공할 수 없습니다.  
  

운영 서버는 개발이나 테스트 목적이 아닌 실제 사용자들을 대상으로 서비스하는 서버를 말합니다. 개발 및 테스트 목적의 서버라면 많은 요청이 발생할 일도 없고 장애가 발생하더라도 큰 문제가 생기지 않습니다. 운영 서버는 그와 다르게 트래픽 대응도 해야 하고 빠른 응답 속도와 높은 가용성을 보장해 안정적으로 제품이 서비스될 수 있도록 해야 합니다.  
  

그러기 위해서는 ==운영 서버는 로컬 환경의 개발 및 테스트 서버와 다르게 서버 환경을 구성해야 합니다==. 서비스의 특성에 따라 알맞은 서버 환경 구성이 다르겠지만, 대부분의 서비스에 적용할 수 있는 범용적인 운영 서버 구축 및 관리 방법에 대해서 알아보겠습니다.  
  

## 1-2. 운영 서버 아키텍쳐

운영 서버의 아키텍쳐를 다음과 같이 나누어 볼 수 있습니다.  
  

### 1-2-1. 단일 서버

단일 서버는 단순한 만큼 가장 기본적인 서버라고 볼 수 있습니다. 환경을 구축하기 쉽기에 테스트 서버나 간단한 애플리케이션을 서비스 할 때 많이 사용합니다. 그리고 데이터베이스와 애플리케이션이 같은 서버에서 실행 되고 있기 때문에 별도의 네트워크 설정을 할 필요가 없습니다.  
  

하지만 아래와 같은 단점들도 있습니다.  
  

첫 번째, 전체 서비스의 장애 발생 가능성이 높습니다. 같은 자원을 공유하고 있기에 애플리케이션과 DB 둘 중 하나라도 장애가 발생할 경우 전체가 다운 될 수 있습니다.  
  

두 번째, 서버 자원을 효율적으로 사용하기가 어렵습니다. 서비스의 속성에 따라 필요하거나 최적의 OS(운영체제) 설정과 리소스의 종류(CPU, 메모리 ..)가 다를 수 있기 때문입니다.  
  

세 번째, 보안성이 떨어집니다. 데이터베이스는 보안상 IP 주소나 포트 등 접속 지점을 최소화해야 합니다. 그러나 간단한 애플리케이션이라고 할지라도 그 특성상, 여러 불특정한 IP주소나 포트에 대해 요청을 받아야 하기에, 애플리케이션과 데이터베이스가 한 서버에 구축되어 있다면 DB 보안에 취약합니다.  
  

네 번째, ==서버의 수를 여러개로 늘려 자원을 확장하는 방식인 Scale-out==이 어렵습니다. 단일 서버의 구조처럼 애플리케이션과 데이터베이스가 하나의 서버로 구성되면 똑같은 데이터를 여러 서버에 복제해야 하므로 관리가 매우 힘들어집니다.  
  

### 1-2-2. 애플리케이션과 데이터베이스 서버를 분리

단일 서버 구성에서 하나로 이루어져 있던 애플리케이션과 데이터베이스를 각각의 서버로 구성하는 방법입니다. 두 서버가 다른 자원을 사용하고 있기 때문에 위에서 언급한 단일 서버의 단점을 어느 정도 해소해 주지만, 하나의 서버가 아닌 두개의 서버를 관리하므로 구성은 다소 복잡해지고, 애플리케이션 서버와 DB 서버 사이의 지연 시간과 네트워크 보안을 고려해야 합니다.  
  

또한 클라이언트는 여전히 하나의 애플리케이션 서버를 바라보고 있기 때문에 Scale-out은 여전히 어렵습니다.  
  

### 1-2-3. 서버 단위의 로드 밸런서

우선 ==로드 밸런서==란 무엇인지에 대해 간단하게 짚고 넘어가겠습니다. 애플리케이션 서버에 요청을 보내는 클라이언트가 몇 명 정도가 아닌 수만, 수십만 혹은 그 이상이라면 하나의 애플리케이션 서버로 그 많은 요청을 감당하기 힘들어집니다. 이 때는 앞서 나왔던 Scale-out 방식을 통해 서버를 여러 대로 늘릴 수 있는데, 로==드밸런스는 이렇게 들어오는 수많은 요청들을 앞서 늘린 여러대의 서버에 적절히 나눠주는 네트워크 장치 혹은 프로세스==라고 볼 수 있습니다.  
  

클라이언트는 애플리케이션 서버와 직접 통신하는게 아닌 로드 밸런서 서버와 통신하며, 그 뒤에 여러대의 애플리케이션 서버를 두는 방식입니다.  
  

이러한 ==로드 밸런서를 두면서 Scale-out을 통한 확장이 가능해지고 특정 서버에 장애 발생시, 로드 밸런서가 정상 서버에 요청을 넘기면 되므로 서버 다운을 최소화== 할 수 있습니다. 단, 모든 요청을 먼저 받는 로드 밸런서에 장애가 생기면 전체 서비스에 장애가 생길 수 있는 단점이 있습니다.  
  

### 1-2-4. 서버 내 앱 단위의 로드 밸런서

기존에 하나의 로드 밸런서가 여러개의 서버로 요청을 분산해주었던 방식에서, 서버 내에 앱 단위의 로드 밸런서가 추가 된 방식입니다. 기존의 애플리케이션 서버 안에서 똑같은 애플리케이션을 여러 프로세스로 만들어 실행 해놓고 외부에서 들어온 요청을 프로세스 중 하나로 보내주는 방식입니다.  
  

하나의 서버에 여러 개의 프로세스를 실행해 하나의 서버에서 여러 개의 요청을 동시에 처리 할 수 있습니다.  
  

또한 서버의 자원을 최대한으로, 효율적으로 사용할 수 있습니다.  
  

이렇게 점점 복잡해지고 체계적으로 구축되는 운영 서버를 구축하기 위해서는 자체 ==데이터 센터를 운영하는 방법과 클라우드 컴퓨팅 기술을 이용하여 클라우드 환경에 만드는 방법이 있습니다==. 이어서 ==운영 서버를 구축하는 두 방법==에 대해서 알아보겠습니다.

# 2. 온프레미스(On-premise)

---

![session img](https://api-media-storage.s3.amazonaws.com/session-media/6047164c86cb44eeae9337a257ebf8a3?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIASTLUR2MMSOMANKHU%2F20220813%2Fap-northeast-2%2Fs3%2Faws4_request&X-Amz-Date=20220813T133246Z&X-Amz-Expires=60&X-Amz-SignedHeaders=host&X-Amz-Security-Token=IQoJb3JpZ2luX2VjECUaDmFwLW5vcnRoZWFzdC0yIkgwRgIhAKmpMjnV9WgQAwsM5HMkJxxvrqbC7%2BrMW8KAX3XHzSpfAiEAjkPDf6ReF6C81%2B%2BozJHF9enLDmiDw4XT3TFmY6jOyQsq9AIIjv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAEGgwxNzkwMjI0NTE0ODEiDNYKfcwB43RwKYnuGCrIAkQiicq8NX93OjjTSgy1BhzZTjFIOQNGjCB2xQihH8QFSuC9a%2FSPskV9joNcSYJse36JEujn%2F70M%2FLHdSMDyoxpCPVVa56Qk5UvnHXGqM6XCwwuK4%2FduRGZqf8gkH3MExOd8fQTtlJpapZ%2F2D1izH%2BpGwaNuuMDTXtf0VFrnISPT4ghXj9w1wzVlbG%2BtXdMoGu1jMYGmLXLyyoDigWgV1hliQpsZG6UvBl4yLGLh%2BefiwrrfIpfL%2FhAXgiSga88sy2NSHO1Eh48GX4x0v8X732YxZOaDucy7fGCGQ%2BsTp8nu%2BtjCvGOUg%2BpRBYnGfR83G5fopsdbPft3jy0NepomPafUupwVwOdGZ7lkmXTBAY5%2FWDczJYsR8ztLbHA6mB56IHwGI3hLxmTbZZomWZUaGeNDcKSm2%2FpyuoowtmYp%2BH7m99KRrndgkJww9MnelwY6nQEfJ%2FGCGv%2B3RvEediyKXuTpDCmJwhSb3jhbf5NZ8n5YYcRvgxGm1idIJfSDiSvWYy2bfBZ3fWUjRGV%2FF7bGCZCzJre7T2lsQYDMpnHwYTNBhPT344Z4lhTlqM1k6hFxJ94vVkeFSWIFb%2BWi8jAo%2F%2Fl5X35crkrkrCNl%2FE%2FVeT5JVyax1QR6jlN2GCyiLfIybo71xdN3EH4%2FZH4v5Sk1&X-Amz-Signature=4af81ecd50a060b682a6c24f182b99d9a798fee986d0cb8083a96e0ea2e6ce86)

[그림 2-1] 온프레미스(On-premise)  
  

## 2-1. 온프레미스란?

==온프레미스란 IT 서비스를 기업이 자체적으로 보유한 물리적인 서버에 직접 설치해 운영하는 방식을 뜻합니다==. 이러한 방식은 클라우드 컴퓨팅 기술이 나오기 전까지 기업들이 사용하던 일반적인 인프라 구축 방식이기도 합니다.

## 2-2. 온프레미스의 특징

인프라를 물리적으로 직접 구축하여 운영하는 방식이므로 프로젝트에 필요한 시스템을 구축하기 위해서 기업이 직접 구성에 맞게 하드웨어를 구입하여야 합니다. 보통 프로젝트에 필요한 자원을 예측하여 인프라 기술자가 물리적인 구성을 설계하는데, 이때 물리적인 구성은 최대 사양을 기준으로 구성되기 때문에 예측과 실제 프로젝트가 많이 다를 수 있으며 이로 인해 불필요한 비용이 사용될 수 있습니다. 또한 구축 후에도 문제가 발생하지 않는지 지속적인 모니터링이 필요하며 필요에 따라 구성을 변경하는 등 유지, 보수가 필요합니다.  
  

위와 같은 이유로 많은 기업들이 클라우드 컴퓨팅 서비스를 사용하고 있지만, 보==안에 민감한 조직(군대, 보안 회사)의 경우 자체적으로 강력한 보안 시스템 개발하거나 외부망과의 단절을 위해 여전히 온프레미스 환경으로 구축하곤 합니다.==

# 3. 클라우드 컴퓨팅(Cloud Computing)

---

![session img](https://api-media-storage.s3.amazonaws.com/session-media/c54b27ceb07548728e3851b74f6b96f9?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIASTLUR2MMSOMANKHU%2F20220813%2Fap-northeast-2%2Fs3%2Faws4_request&X-Amz-Date=20220813T133246Z&X-Amz-Expires=60&X-Amz-SignedHeaders=host&X-Amz-Security-Token=IQoJb3JpZ2luX2VjECUaDmFwLW5vcnRoZWFzdC0yIkgwRgIhAKmpMjnV9WgQAwsM5HMkJxxvrqbC7%2BrMW8KAX3XHzSpfAiEAjkPDf6ReF6C81%2B%2BozJHF9enLDmiDw4XT3TFmY6jOyQsq9AIIjv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAEGgwxNzkwMjI0NTE0ODEiDNYKfcwB43RwKYnuGCrIAkQiicq8NX93OjjTSgy1BhzZTjFIOQNGjCB2xQihH8QFSuC9a%2FSPskV9joNcSYJse36JEujn%2F70M%2FLHdSMDyoxpCPVVa56Qk5UvnHXGqM6XCwwuK4%2FduRGZqf8gkH3MExOd8fQTtlJpapZ%2F2D1izH%2BpGwaNuuMDTXtf0VFrnISPT4ghXj9w1wzVlbG%2BtXdMoGu1jMYGmLXLyyoDigWgV1hliQpsZG6UvBl4yLGLh%2BefiwrrfIpfL%2FhAXgiSga88sy2NSHO1Eh48GX4x0v8X732YxZOaDucy7fGCGQ%2BsTp8nu%2BtjCvGOUg%2BpRBYnGfR83G5fopsdbPft3jy0NepomPafUupwVwOdGZ7lkmXTBAY5%2FWDczJYsR8ztLbHA6mB56IHwGI3hLxmTbZZomWZUaGeNDcKSm2%2FpyuoowtmYp%2BH7m99KRrndgkJww9MnelwY6nQEfJ%2FGCGv%2B3RvEediyKXuTpDCmJwhSb3jhbf5NZ8n5YYcRvgxGm1idIJfSDiSvWYy2bfBZ3fWUjRGV%2FF7bGCZCzJre7T2lsQYDMpnHwYTNBhPT344Z4lhTlqM1k6hFxJ94vVkeFSWIFb%2BWi8jAo%2F%2Fl5X35crkrkrCNl%2FE%2FVeT5JVyax1QR6jlN2GCyiLfIybo71xdN3EH4%2FZH4v5Sk1&X-Amz-Signature=299808588abe0cefde348fe7690a92a270ca375c83ee4abea9765f1957751cfa)

[그림 3-1] 클라우드 컴퓨팅(Cloud Computing)  
  

## 3-1. Compute란?

==컴퓨팅==은 스토리지 및 네트워킹과 함께 클라우드 컴퓨팅 인프라 계층의 ==핵심 컴포넌트== 중에 하나입니다. 기본적으로 compute란 Linux, Ubuntu, Debian, Window, MacOS와 같은 운영 체제를 실행하는 데 필요한 ==CPU, Memory, Storage와 일부 가상화된 네트워크 기능으로 구성된 물리적인 서버(컴퓨터)==를 말합니다.  
  

여기서, **CPU**(Central Processing Unit)는 ==컴퓨터의 두뇌==이며 프로그램의 명령을 수행합니다. **RAM**(Random Access Memory)은 초고속 임시 저장 장치로 CPU와 저장장치 사이에서 처리 속도를 향상시켜주기 위해서 데이터를 임시로 저장하는 역할을 수행합니다. **Storage**는 운영체제 파일 또는 모든 소스코드 및 데이터가 저장되는 저장소입니다. **Network**는 보통 인터넷을 통해서 다른 서버와의 연결할 수 있도록 만들어주는 ==네트워크 인터페이스 카드(NIC)==를 의미합니다.  
  

정리하면, Compute란 ==CPU, RAM, Storage, Network 기능으로 구성된 물리적인 서버==를 의미합니다.

## 3-2. 클라우드 컴퓨팅이란?

클라우드 컴퓨팅은 현재 IT 분야에서 가장 빠르게 발전하는 기술 중 하나입니다.  
  

만약에 사용자에게 compute(물리적 서버)에 대한 요구가 들어올 때 마다 시스템 엔지니어가 CPU, RAM, Storage, Network를 담은 물리적인 서버를 설치한 후에 이를 대여해 준다면 시간이 오래 걸릴 뿐더러 분명 비효율적일 것 입니다.  
  

그래서 클라우드 컴퓨팅 서비스를 제공하는 업체는 서로 다른 물리적 위치에 존재하는 컴퓨팅 자원을 가상화 기술로 통합하여 인터넷에서 제공합니다. 즉, 사용자는 이러한 IT 리소스를 인터넷을 통해 온디맨드로 제공받고 사용한 만큼만 비용을 지불하면 됩니다.  
  

위에서 말씀드린 것과 같이 서로 다른 위치에 존재하는 컴퓨팅 자원을 제공하는 것이 클라우드 컴퓨팅 서비스입니다. 클라우드 컴퓨팅 서비스를 제공하는 업체는 흔히 **`서버 팜`** 이라고 불리는 곳에 엄청난 수의 물리적 서버를 갖추고 있습니다. 서버 팜은 전 세계에 흩어져 있고, 우리는 이곳에 데이터를 저장하게 됩니다.

## 3-3. 클라우드 컴퓨팅의 특징

온프레미스와는 다르게 직접 서버 장비를 구매하지 않고도, 요청하는 즉시 컴퓨팅 자원을 제공해주는 기술로 원하는 시간동안 원하는 만큼의 컴퓨팅 자원을 언제 어디서나 이용할 수 있습니다. 따라서 불필요한 절차 없이 쉽게 프로젝트를 구성할 수 있습니다. 이는 프로젝트 초기 구성 시 사용되는 비용을 줄이는 효과를 가져옵니다.  
  

그리고 위에서 설명한 것과 같이 인터넷을 통해 온디맨드로 IT 리소스를 제공합니다. 사용자는 사용한 만큼의 비용만 지불하면 됩니다.  
  

또한 서비스의 규모에 따라 리소스를 확장하거나 축소할 필요가 있는데, 대부분의 클라우드 컴퓨팅 서비스는 이러한 기능을 기본적으로 지원하기 때문에 손쉽게 서비스를 확장 및 축소할 수 있습니다.

## 3-4. 클라우드 컴퓨팅의 주요 기능 3가지

==클라우드 컴퓨팅은 관리 주체와 수준에 따라 3가지로 구분==하여 설명할 수 있습니다.  
  

### 3-4-1. 서비스형 인프라스트럭처(IaaS)

클라우드 컴퓨팅의 가장 기본적인 계층은 ==IaaS(Infrasturcture as a Service)==입니다. 비즈니스 운영에 필요한 스토리지, 네트워킹 및 컴퓨팅 자원을 제공합니다. 다른 모델들과 비교하여 ==사용자가 관리할 수 있는 영역이 가장 넓습니다==. 사용자가 직접 OS, Middleware, Runtime 등을 직접 구성하고 관리할 수 있습니다.  
  

IaaS는 사용자가 직접 많은 부분을 구성하고 관리할 수 있다는 ==장점==이 있지만, ==인프라 운영에 대한 지식, 경험이 준비되지 않은 경우 활용이 어려울 수 있습니다.==  
  

예) AWS Elastic Compute Cloud (EC2), Microsoft Azure Virtual Machines, Google Compute Engine..  
  

### 3-4-2. 서비스형 플랫폼(PaaS)

PaaS(Platform as a Service)는 애플리케이션 및 서비스를 구축할 수 있는 플랫폼을 제공합니다. OS, Middleware, Runtime 등 개발 환경을 미리 구축해 서비스 형태로 제공하기 때문에 관리적인 측면에서 IaaS보다 자유도가 낮습니다. 사==전에 구축된 환경에서 개발하기 때문에 의존성이 생기기 때문==입니다.  
  

하지만 서비스를 제외한 외적인 부분을 신경쓸 필요가 없기 때문에 오로지 ==개발, 비즈니스에만 집중할 수 있으며 인프라를 운영하는 인력이 필요하지 않으므로 유지 및 보수 비용을 절약할 수 있습니다.==  
  

예) AWS Elastic Beanstalk, Heroku, Redhat OpenShift  
  

### 3-4-3. 서비스형 소프트웨어(SaaS)

SaaS(Software as a Service)는 클라우드 컴퓨팅 서비스의 주요 기능 3가지 중 가장 완성된 형태의 서비스입니다. 즉 해당 서비스의 제공 업체가 대부분의 기능을 구축한 뒤 제공하기 때문에 사용자가 직접 관리해야 하는 영역이 가장 좁습니다. 기본적인 클라우드 인프라와 소프트웨어를 함께 제공하는 형태로, 소프트웨어 업데이트, 버그 픽스 등의 서비스를 업체가 직접 도맡아 제공합니다. 사용자는 별도의 라이센스를 구매할 필요 없이 이미 구축된 소프트웨어를 무료 혹은 비용 지불을 통해 이용합니다.  
  

하지만 제공 업체가 이미 만들어 놓은 소프트웨어를 그대로 활용하기 때문에 사용자가 필요하지 않은 기능에 대해서도 비용을 지불해야 할 수도 있습니다.  
  

예) Google Drive, iCloud, Slack, Zoom, Dropbox

# 4. Summary

---

-   운영 서버는 개발이나 테스트 목적이 아닌 실제 사용자들을 대상으로 서비스하는 서버를 말합니다.
-   운영 서버의 아키텍쳐로는 크게 ==단일 서버==, ==애플리케이션 / 데이터베이스 서버 분리==, ==서버 단위 로드 밸런서==, ==서버 내 앱 단위 로드밸런서==의 네가지로 분류 할 수 있습니다.
-   이러한 운영 서버를 구축하기 위해서는 자체 데이터 센터를 운영하는 방법(On-premise)과 클라우드 컴퓨팅 기술을 이용하여 클라우드 환경에 만드는 방법(Cloud Computing)이 있습니다.
-   ==온프레미스==란 I==T 서비스를 기업이 자체적으로 보유한 물리적인 서버에 직접 설치해 운영하는 방식을 뜻==합니다.
-   ==클라우드 컴퓨팅==이란 ==IT 리소스를 인터넷을 통해 온디맨드로 제공하고 사용한 만큼만 비용을 지불하는 것을 말합니다.==