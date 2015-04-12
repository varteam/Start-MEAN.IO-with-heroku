# Start-MEAN.IO-with-heroku
아래의 모든 사항은 모두 ubuntu 14.04 Desktop 환경에서 설치되었습니다.


##필수 설치 요소
* git
* nodejs
* heroku


### git 설치
```bash
sudo apt-get install git -y
```
git 설치시 1.3 (?)이하 버젼의 경우 https 인증이 되지 않는 것으로 기억하며 이경우 https인증을 통해 github를 사용시 인증에러가 나온다. 
가급적이면 2.0 이상의 버젼을 사용하며 ubuntu14.04환경에서는 기본 제공하는 git 버젼을 사용하더라도 1.9까지 사용되므로 큰 문제는 발생하지 않는다.

### nodejs 최신 버젼으로 PPA추가 및 설치
npm 의 경우 구버젼 에서 사용시 nodejs와 npm을 각각 설치하였으나 특정 버젼 이후로는 통합되어져서 같이 설치된다.
운영체제 배포판에 따라 조금씩 포함 패키지가 다르니 ubuntu14.04를 제외한 곳에서는 확인이 필요하다
실제로는 nodejs와 nodejs 패키지를 관리해주는 npm 둘다 설치가 되어야 한다.
* node와 npm이라는 패키지를 설치해야 하는 배포판 존재
* nodejs와 npm을 각각 설치해줘야하는 배포판 존재
* nodejs만 설치하면 되는 배포판 존재

```bash
sudo add-apt-repository ppa:chris-lea/node.js -y
sudo apt-get update && sudo apt-get install nodejs -y
```


### heroku toolbelt install
* https://toolbelt.heroku.com/
```bash
sudo wget -qO- https://toolbelt.heroku.com/install-ubuntu.sh | sh
```



### mean.io 설치
```bash
sudo npm install -g mean-cli
```
* npm install 을 -g 옵션을 주고 설치하게 될 경우 전역으로 설치되며 설치 경로는 npm의 설치경로에 참조를 하게 되며 전체 프로젝트에서 참조할 수 있다.
* 전역 옵션을 주지 않고 각각의 패키지에 특정 버젼을 지정하여 설치도 가능하며 실제 프로그램 실행시 참조하는 순위에서는 후순위로 참조된다.

### mean.io로 기본 앱 생성
```bash
mean init "AppName"
```
* 이후 명령어는 화면에 출력되는 메세지에 따라 작성하면 되지만 기본적으로는 다음과 같다
```bash
cd AppName
npm install && bower install
```
* npm install 이나 bower install 을 실행할 경우 해당 디렉토리에 존재하는 package.json bower.json을 각각 참조하여 필수라이브러리를 설치하게 된다.
* 위의 명령어는 반드시 sudo를 제거하고 실행해야하며 sudo 옵션을 주고 설치 또는 관리자 권한으로 설치시 bower는 설치가 되지 않으며 추후 라이브러리 설치 및 참조시 에러를 발생시키는 경우가 많다.



###heroku 연동
* 1차로 heroku 가입을 먼저 해야하며 위의 명령어로 툴벳을 설치한 이후에 작업한다.



TODO : heroku 변경 사항이 많아서 최종 테스트가 충분히 된 후 업데이트 예정



