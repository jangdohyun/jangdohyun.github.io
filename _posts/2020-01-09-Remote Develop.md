# Visual Studio Code & Remote Development

![enter image description here](https://user-images.githubusercontent.com/58260252/71954430-9b12c280-3228-11ea-8536-3cd6222060be.png)


Visual Studio Code의 Remote Development를 이용하면 __하나의 에디터로(visual studio code)로 여러가지 작업(컨테이너 관리, light sail, ubuntu 등)을 원격으로 관리__ 할 수가 있습니다. 여러 환경에 대한 설명과 함께 원격 환경을 조성하는 방법을 간단히 소개해 보겠습니다.

## Visual Studio Code
![enter image description here](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQGF2Gql1WTNVkDolEwO7lTBH81oeROyyjobddqAUb3vwYhGOr4QQ&s)


__Visual Studio Code__ 는 마이크로 소프트에서 2015년 출시한 에디터 중 하나로, 개발 툴들 가운데 최초로 크로스 플랫폼을 지원하는 에디터 입니다.

IDE가 아니므로, 빌더가 내장되어 있지 않아 VS Code에서 빌드를 하려면 별도의 컴파일 환경을 구축 해야한다는 특징이 있지만, 수 많은 추가기능들을 VS Code 내부의 검색을 통해서 한 번의 클릭으로 쉽게 다운 받을 수 있다는 장점이 있습니다.

### 기능
▶ 멀티 커서 에디팅 - 볼록 선택, 모든 항목 선택 등

▶ 인텔리센스 - 코드, 외부 모듈에 대한 코드 지원 및 매개변수 제안

▶ 추출 리팩터링 - 공통 코드를 함수나 상수로 빠르게 추출

▶ 스니펫 - 반복 타이핑 시간 단축

▶ 포매팅 - 내장된 문서 및 선택 서식을 이용한 깔끔한 코드 유지

## Windows Subsystem for Linux

![enter image description here](https://i.ytimg.com/vi/Cvrqmq9A3tA/maxresdefault.jpg)





추가로 나중에 소개될 원격 제어목록 중 하나인 WSL에 대해서도 기본 개념만 잠깐 살펴 보고 가겠습니다.

WSL은 오직64bit 윈도우10에서만 가능한 것으로 윈도우 환경에서 리눅스 명령을 cmd, powershell 등을 통해 직접 실행할 수 있는 새로운 기능입니다. 즉, 다시말해 리눅스용 프로그램과 도구들을 윈도우에서도 사용 할 수 있게되어 __윈도우에서 리눅스 환경에서의 개발과 유사한 느낌__ 을 낼 수 있게 해주는 기술 이라고 정리 할 수 있습니다. 이와 비슷한 기능을 하는 가상화 머신과 비교하였을때또한 훨씬 적은 자원을 소모한다는 장점이 있습니다.

## Amazzon Lightsail

![enter image description here](https://t1.daumcdn.net/cfile/tistory/997FCA345C5F377012)



__Amazon Lightsail__ 이란 작은 비용으로 시작 할 수 있는 작은 가상서버 서비스로 관리가 어렵고 비용이 많이드는 서버들을 작은 돈으로 작은 부분만 떼어서 빌려쓰는 개념입니다.

 작은 서버지만 서버라는 사실은 변함이 없기 때문에 추후에 큰 서버관리능력이 필요할 때를 대비해 연습 할 수 있는 입문용 서비스라고도 할 수 있습니다.

 ## Docker
 ![enter image description here](https://subicura.com/assets/article_images/2017-01-19-docker-guide-for-beginners-1/docker-logo.png)



도커는 기존 리눅스 컨테이너에 여러가지 기능을 추가하여 쉽고 빠른 컨테이너 사용이 가능하게 한 __오픈소스__ 입니다. 
기존 가상화기술은 모든 작업이 하이퍼바이저를 반드시 거치기 때문에 일반 호스트에 비해 성능 손실이 발생합니다. 

또한 게스트 OS를 위한 라이브러리, 커널등을 전부 다운받아야하기 때문에 이미지 크기또한 커지게 됩니다. 반면에 Docker는  chroot, namesapce, cgroup을 이용해 __프로세스 단위 격리 환경__ 을 만들어 성능 손실을 줄이고, 컨테이너에 필요한 __커널을 호스트와 공유__ 하여 사용하기 때문에 __이미지 용량 또한 대폭 감소__ 된다는 장점이 있습니다. 

![enter image description here](https://cdn-images-1.medium.com/max/1000/1*wOBkzBpi1Hl9Nr__Jszplg.png)



### Docker Images & Container

_Images_: 컨테이너 생성및 실행 시 **읽기전용** 으로 사용됩니다.
**이미지**는 도커 명령어로 다운받을 수 있으므로 별도 설치가 필요없으며, 기본 형식은 [저장소 이름]/[이미지 이름]:[태그] 입니다.

_Container_: 이미지에서 **변경된 사항만을 저장**하기때문에 컨테이너에서 무엇을 하든지 원본 이미지는 영향을 받지 않습니다. 또한 각 컨테이너는 **독립된 파일 시스템**을 제공받고 호스트와 분리되어 있기 때문에 컨테이너간 독립이 되어 있습니다.

![enter image description here](https://subicura.com/assets/article_images/2017-02-10-docker-guide-for-beginners-create-image-and-deploy/create-image.png)


## 원격 제어 환경 조성

- WSL Targets

1. Microsoft store에서 WSL 프로그램을 다운 받습니다. (본인은 ubuntu를 받았습니다)
2. Ubuntu에 접속하여 "code ." 을 입력합니다.
3. VS code와 ubuntu가 연결이 된 code창이 뜹니다.
4. 원격 관리 준비 끝!

- SSH Targets

1. AWS의 Lightsail sever를 엽니다. 
2. 서버의 ip를 고정 시킨 후, 서버에 입장합니다.
3. config 설정에 들어가 아래의 항목을 No에서 yes로 바꿔주면 비밀번호를 입력 시 원격제어권을 가져 올 수가 있습니다.

![enter image description here](https://user-images.githubusercontent.com/58260252/71954734-8daa0800-3229-11ea-9b49-9f8218de3072.png)

4. VS Code에서 F1키를 눌러 검색창을 띄우고 Remote-SSH:Connect to Host...를선택합니다.
5. Configure SSH Hosts를 선택합니다.
6. 파일을 업데이트 할 경로를 선택합니다.
7. 들어간 config 페이지에 아래의 그림과 같은 양식으로 입력해 줍니다.

![enter image description here](https://user-images.githubusercontent.com/58260252/71954783-bf22d380-3229-11ea-985a-3d420b4cc7b0.png)

8. 원격 관리 준비 끝!

- Container Targets

1. VS Code의 EXTENSIONS로 들어가 REMOTE-Containers를 다운 받습니다.
2. VS Code 에서 F1를 눌러 검색창을 띄우고 Remote-Containers:Attach to Running Container...를 선택합니다.
3. 원격제어할 콘테이너를 선택합니다.
4. 원격 관리 준비 끝!

# Git 
