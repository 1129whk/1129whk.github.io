---
title: "Chirpy 블로그-Ruby업데이트와 Jekyll 설치"
date: 2025-01-25 20:36:00 +0800
categories: [Blogging, Jekyll]
tags: [Blogging, Jekyll]
---
## Problem
<br>1. 맥북에서는 이미 ruby가 설치되어 있는데, 'ruby 2.6.10' 버전이라서 버전이 낮아 Jekyll 시 오류가 났습니다.
<br>따라서 ruby를 더 높은 버전(ruby 3.3.6)으로 업데이트하고, Jekyll를 설치했습니다.
<br><br>2. assets/js/dist/ 폴더가 생기지 않는 문제
<br><br>3. Deply 안 되는 오류
<hr>

## Solution
공식문서를 참고했고, 공식문서에서는 도커에서 하라고 하는데, 저는 도커에서 폴더 안의 파일을 만들어서 가지고 왔습니다.<br>
블로그 생성 자체가 오류도 많이 나고 어려운 나머지, 그냥 티스토리로 다시 갈까 하다가, 도전해본 결과, 오류를 모두 해결했습니다.
<hr>

### Reference
<https://jekyllrb.com/docs/installation/macos/>
<hr>

## Ruby 버전 업데이트
<br>맥북에 원래 내장되어 있는 Ruby 버전이 2.x로 낮아서 오류가 났습니다. 따라서 버전 업데이트를 진행하게 되었습니다.
<br>아래의 명령어들을 해당 프로젝트 폴더에서 실행하면 됩니다.

<br>`brew install rbenv ruby-build`
<br>루비의 여러 버전을 설치할 수 있도록 플러그인 ‘rbenv ruby-build’을 설치

<br>```rbenv install -l```
<br>설치할 수 있는 ruby 버전을 확인. 그 중에서 3.3.6을 선택하겠음.

<br>```rbenv install 3.3.6 && rbenv rehash```
<br>ruby의 gem 명령어가 새로 설치된 ruby버전의 gem 명령어로 해시되도록 해준다.
<br>이때 시간이 좀 걸리니 기다려야 함.

<br>```rbenv global 3.3.6```
<br>기본 ruby 버전을 3.3.6로 선택

<br>```ruby -v```
<br>ruby의 버전을 확인했더니, 아직 ‘ruby 2.6.10’ 버전이라고 나온다. 아래와 같이 사항을 한줄씩 차례대로 적용시키면 해결된다.


    vi ~/.zshrc
    export PATH="HOME/.rbenv/bin:$PATH"
    eval "$(rbenv init -)"
    source ~/.zshrc

변경사항 적용. 'ruby -v'로 확인해보니, ‘ruby 3.3.6’로 변경사항이 적용되었다.
<hr>

## Install Jekyll
```gem install jekyll```

<br>```npm install && npm run build```
<br>설치 하지 않으면, assets/js/dist/*.min.js Not Found 에러 발생.
<br>그런데 dist폴더가 설치되지 않아서, 결국 공식문서를 보고 도커에서 진행하여 만들어진 dist폴더를 로컬에 가지고 왔다.
<br>이 과정은 공식문서에 자세히 있는데, <https://chirpy.cotes.page/posts/getting-started/>
<br>VS Code에 'Dev Containers'확장팩을 설치하고 도커에서 진행했었다.
<br>다른 블로그들을 참고해보니, 'bash tools/init.sh'명령어도 실행되지 않아서, 이 2단계를 수동으로 처리하는 분들도 있는데, 결국 dist폴더를 만든 걸 가지고 왔고,
<br>'bash tools/init.sh'명령어는 뒤에 실행하니 실행되었다.

```bundle```
번들 설치

<br>```bash tools/init.sh```
<br>초기화. 더 앞순서에서 시도하니 실행이 되지 않았다. 이 과정을 통해 _posts폴더에 있었던 예시 파일이라든지 기타 필요없는 파일들은 정리하게 된다.

<br>```bundle exec jekyll serve```
<br>: 로컬에서 실행시킨다. 'http://127.0.0.1:4000/'로 확인.
<hr>


## Deply Error
<br>로컬에서 실행은 되었지만, 깃허브에 deply시 오류가 났습니다. 깃허브 프로젝트의 Action탭에서 확인해보니 아래와 같은 문제였습니다.

        Jekyll 4.3.3   Please append `--trace` to the `build` command for any additional information or backtrace.
        Can't find stylesheet to import.
        /assets/css/jekyll-theme-chirpy.scss

요약하자면 위와 같은 오류가 생겼는데, 아래와 같이 .github폴더 안에 있는 workflows폴더의 'pages-deploy.yml'파일에 아래의 코드를 추가하니 해결됨.

    - name: npm build
      run: npm install && npm run build

