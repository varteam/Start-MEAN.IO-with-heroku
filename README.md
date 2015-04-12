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
* 폴더명과 프로젝트명이 다를경우에는 폴더명으로 먼저 생성후 프로젝트명 입력창에서 입력가능 (이후에는 환경설정 파일에서 수정)
* mean-cli가 구버젼에서는 grunt를 기본 빌드툴로 사용하고 이후 버젼에서는 grunt와 gulp의 선택가능한 버젼이 있으며 현재는 gulp가 기본 빌드툴로 확인된다
* 이후 명령어는 화면에 출력되는 메세지에 따라 작성하면 되지만 기본적으로는 다음과 같다
```bash
cd AppName
npm install && bower install
```
* npm install 이나 bower install 을 실행할 경우 해당 디렉토리에 존재하는 package.json bower.json을 각각 참조하여 필수라이브러리를 설치하게 된다.
* 위의 명령어는 반드시 sudo를 제거하고 실행해야하며 sudo 옵션을 주고 설치 또는 관리자 권한으로 설치시 bower는 설치가 되지 않으며 추후 라이브러리 설치 및 참조시 에러를 발생시키는 경우가 많다.



###heroku 연동
* 1차로 heroku 가입을 먼저 해야하며 위의 명령어로 툴벳을 설치한 이후에 작업한다.

```bash
cd AppName
heroku login
heroku keys:add 
heroku git:remote -a "heroku app name"
git fetch --unshallow 
git push heroku master
```

* 기본 설치후에 heroku로 바로 push 할 경우 이상하게 문제 생기는 케이스가 있는데 2가지 해결법이 있다.
* 1. rm -fr .git 으로 기존의 git 저장된 내역을 다 날리고 git init 이후 처음부터 생성한 git을 커밋한다
* 2. git fetch --unshallow 로 전체 내역을 새로 업데이트 이후에 push를 한다

 TODO : 이부분 원인에 대해서 추가로 조사가 필요.


###Mongolab 설치
* heroku 문서를 찾아보면 mongohq 관련 자료가 많은데 예전에는 기본플랜이 무료로 제공되었으나 2015-04-12기준으로 무료플랜은 찾을수가 없었다.
* 따라서 Mongolab을 기준으로 설치한다.
```bash
heroku addons:add mongolab
```
* 설치가 완료되면 heroku 관리콘솔에서 add-ons 항목에 mongolab이 추가된 것을 볼 수 있다. (명령어가 아닌 웹상에서 추가해도 상관없다)
* 설치된 애드온 항목을 클릭해보면 해당 애드온의 관리화면을 볼 수 있는데 여기서 실제 연결할 database 계정을 추가해준다.
* 추가후에는 상단에 db 연결용 string을 기억/복사 해둔다.

####
기본적으로 설치되는 mean.io는 localhost의 db를 사용하게 되어있다
이부분은 config/env 폴더내의 원하는 환경의 설정 파일을 수정해서 db connection string 을 수정해준다.
```bash
vim config/env/production.js
```
* 4번라인에 보면 db연결용 string이 있는데 위에 mongolab 환경설정시 표시되었던 string으로 수정해준다.


TODO : heroku 변경 사항이 많아서 최종 테스트가 충분히 된 후 업데이트 예정



