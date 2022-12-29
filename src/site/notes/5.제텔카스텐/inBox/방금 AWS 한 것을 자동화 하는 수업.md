# 1. CI/CD with GitHub Actions
-> 지속 통합 ,지속 베포! 
-> 자동화, 베포  효율적인 작업, 빠르고 자주 베포를 진행할 수 있게 된다. 

## CI
합쳐지는 것이 아닌 제대로 합쳐진 후 기능하는지를 말하는 것. merge하고 테스트까지 해주는 것을 말하는 것!!! CI 과정에서 테스트를 실행하고 코드가 유효한지 검사하고 문제가 발생했을 경우 즉각적으로 피드백을 통해서 개발자가 문제를 확인하고 수정할 수 있게 만들어준다.
==코드를 테스트해주는 것을 CI라고 한다,== 

## CD 
CI 과정을 통해서 된 코드들을 베포까지 자동화 한것. (개발 환경까지? continuous Delivery / production 환경? continuous Deployment)


## CI/CD 플랫폼 종류 
CI/CD는 일련의 과정을 처리하는 파이프 라인을 구축함으로서 자동화한다. CI/CD 파이프 라인을 플랫폼으로 제공! 
- 설치형 : 컴퓨터 하나 구하고 그 위에 플랫폼 하나 받아 설치하는 것. 대표적으로 **Jenkins**
	방법 : EC2 를 사용해서 설치해야한다. 
	장:
	단: 
- 클라우드형 : 플랫폼 운영할 컴퓨터를 provider 입장에서 제공을 해준다. 
	장:
	단: 환경을 많이 타는 베포.. 제어권이 부족함. 

## 왜 CI/CD가 각광받는 이유 
장점만 있는 것이 아닌 단점도 있다. CI/CD를 구축하고 운영하면 노력도 필요하고 플랫폼 비용, 서버 비용과 돈이 더 든다. 근데 왜? 회사는 CI/CD를 구축하려고 하는가? 그 이유는 ==효율==!!! 
소프웨어는 하드웨어에 비해 상대적으로 변경하기 쉽고 유저의 피드백을 받아 수정하는 주기를 빠르게 하기 위해

[[무중단 베포]]를 하기 위해서 
[[프론트에서의 성능 최적화란 유저에게 좋은 형태로 보여주려고 한다. 컴퓨팅 자원을 아끼자라는 것이 아니다]]

## Github Actions
왜? CI/CD 클라우드형이어서 쉽고 GitHub repo와 연동이 쉽다. 레포 안에서 CI/CD까지 함께 구축하고 관리하기 쉽다.
빠르게 베포하고 코어한 기능에 집중하기 위해서 클라우드형 관리하기 좋고 비용적인 측면도 퍼블릭에 한해서는 무료이기에 도입했다.
처음 CI/CD를 잘 모르는 상황에서 사용해보기 좋았을 것 같다고 판단했습니다. 

- workflow
workflow는 YAML형식의 파일을 통해서 workflow를 설정한다. 
- Event 
실행은 레포 안에서 발생하는 이벤트나 예약된 스케줄에 의해서 가능. 혹은 수동으로 실행도 가능.
- jobs
하나의 러너 안에서 실행될 여러 step들의 모음! 
step은 실행가능한 하나의 shell script 또는 action을 의마한다. 
job 안의 step 들은 순차적으로 실행 
workflow의 job들은 기본적으로 병렬적으로 실행된다. 
일부 job의 경우에는 다른 job에 의존성을 설정해서 실행하도록 할 수 있다. 
- Actions
github workflow에서 자주 사용되는 기능들을 모아둔 커스텀 애플리케이션! 
라이브러리로 만들어놨다가 사용하는 것 .
GitHub marketplace에서 Action들을 검색하고 활용할 수 있다.
- Runner
제공해주는 컴퓨터가 runner이다. 

## CI/CD로 구축할 목표 
매번 CRA의 dependencies를 설치하고 build script를 실행하고 AWS에 로그인해서 S3 버킷에 들어간 뒤에 기존 버킷 삭제하고 새로운 파일들을 업로드 하는것은 번거롭다. 그래서 자동화

1. 마스터 브랜치에서 push or Pull Request Merge가 발생 -> workflow
2. 필요한 dependencies들을 설ㅊ치
3. build script를 실행합니다.
4. aws에 접속한 후 s3 bucket에 build 한 결과물을 

CI/CD 코드 작성 (연욱 멘토님)
```jsx
//num install
//npm run test
//npm run build

```

```jsx
//.github/workflows/cicd.yml

name: CI/CD 

on: 
	push: 
		branches:
		 - master 
	- workflow_dispatch: 

jobs: 
	cicd:
	 runs-on: ubuntu-latest (최신 버전쓸거야)
	 steps: 
	 - uses: actions/checkout@master (미리 만들어진 모음)
	 - run: npm ci 
	 - run: npm run test
	 - run: npm run build (빌드해야지)
	 - name: deploy to s3 (이름을 따로 지정해서 베포해야지) 
		 uses: jakejarvis/s3-sync-action@master(github market place가면 있다. )
		 with:
		  args: --delete (파라미터 넘기듯)
		 env: AWS_S3_BUCKET: ${{ secrets.AWS_S3_BUCKET }} {레포 세팅에 들어가면 secrets이라는 것이 있다. 깃허브 secret에 들어가서 만들고 버켓 이름을 환경 변수 세팅으로 해준다. 아래에 있는 키를 제목으로 넣고 value를 넣어주어 만들어준다.}
		 AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }} 
		 AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
		 AWS_REGION: 'ap-northeast-2' 
		 SOURCE_DIR: 'build'

```

![[스크린샷 2022-10-29 오후 1.00.22.png |500]]