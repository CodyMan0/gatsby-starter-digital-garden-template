지금까지 앞에서 설명한 내용은 로컬 환경에서 개발을 말했습니다. 즉, 로컬 환경에서의 개발은 어디까지나 기능 구현과 테스트가 목적입니다. 실제로 개발한 API 시스템을 사용자들이 사용할 수 있게 만들기 위해서는 24시간 전원이 꺼지지 않고 안정성이 보장된 환경에서 실행될 수 있어야 합니다.  
  
`5.Advanced API system and Deployment` 과정에서는 실무에 가까운 형태의 API를 개발하고 **Amazon Web Service라는 Cloud Provider**를 활용해서 자체 보안 향상을 고려한 네트워크 설계와 서버를 구축해 서비스를 배포하게 됩니다. 애플리케이션 배포 뿐만 아니라 API 시스템에 테스트 전략(Unit Test)과 컨테이너 가상화 기술(Docker)을 접목시켜 더욱 안정적인 시스템을 구축합니다.

-   **Node.js / Express.js / TypeORM** 기반의 실무에 적합한 **API 구조**를 디자인하고 서버 세팅하는 방법을 학습합니다.
-   다양한 서비스 경험을 통해서 실무 수준의 **RESTful API를** 구현합니다.
-   코드 전반적으로 programming best practices 적용합니다.
-   **적절한 자료구조와 알고리즘을 적용**하여 최적화된 코드를 작성합니다.

#jest (자바스크립트 프레임워크)

#docker : -   Docker는 **컨테이너 가상화(Container Virtualization)** 기술입니다. Docker는 가상화 컨테이너에 application (예, Node.js based application) 배포를 자동화 시켜주는 오픈소스 엔진입니다.

-   Docker는 container 가상화 실행 환경 위에 application 배포 엔진을 더함으로서 사용자의 코드를 어디서든 빠르고 가볍게 실행시킬수 있는 기술을 제공합니다.
-   개발한 API를 도커를 활용해서 이미지를 만드는 방법과 실행하는 방법에 대해서 학습합니다.

5-4. Deploy to Amazon Web Services (AWS)
-   AWS(Amzaon Web Service)란 아마존에서 제공하는 클라우드 서비스로, 시스템 배포 및 운영을 하기 위해 필요한 서버, 데이터베이스, 네트워크 등의 물리적 장치를 설치 걱정하지 않고 클라우드 서비스 제공자의 사이트 혹은 인터페이스(interface)를 통해서 쉽게 설정하고 사용할 수 있도록 해주는 서비스입니다.
-   AWS를 기반으로 API를 배포 및 운영하기 위한 **인프라스트럭처(Infrastucture)를 직접 디자인하고 배포**하는 방법을 학습합니다.
-   AWS에서 핵심 서비스인 **IAM**, **EC2(Elastic Compute Cloud)**, **RDS(Relational Database Service**), **S3(Simple Storage Service**), **VPC(Virtual Private Cloud**)에 대해서 학습합니다.
-   실제로 API 코드를 Github에 올리고, RDS 서비스의 MySQL을 데이터베이스로 사용하여 EC2 서버에 API를 배포하는 실습을 진행합니다.

#CICD 시스템 = github action 이점 : 테스트와 배포의 많은 부분을 **자동화** 할 수 있습니다.
-  CICD는 **Continuous Integration**과 **Continuou Deployment**로 나뉩니다.
-   Continuous Integration은 개발자가 커밋과 푸쉬를 한 후, 빌드 부터 테스트 그리고 develop 브랜치로 merge되는 과정을 자동화가 하여 개발자가 코드를 커밋하고 푸쉬하는 만큼 지체 없이 바로 테스트와 merge가 (하루에도 여러번) 지속적으로 이루어 질 수 있도록 하는 것을 말합니다.
-   Continuous Deployment는 CI 다음 과정들을 자동화하여, 개발자가 개발을 끝내고 커밋 및 푸쉬를 하면 그대로 모든 테스트를 자동으로 거치고 바로 production 배포까지 완료되는 것을 이야기 합니다.

-   AWS에서 제공하는 **ALB**나 **ELB**를 사용하여 쉽게 구현할 수 있지만, **Nginix**라는 **Proxy** 서버를 직접 구현하여 Load Balancing의 개념 및 부하 분산 알고리즘을 학습하고 실제로 구현합니다.
