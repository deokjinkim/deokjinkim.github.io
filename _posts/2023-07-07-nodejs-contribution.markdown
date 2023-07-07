---
layout: post
title: Node.js 오픈소스 기여하기
date: 2023-07-08 00:40:00 +0900
category: sample
---

# 로컬 환경 설정하고 PR(Pull Request) 만들기

## Step 1: Fork 하기

Github에서 프로젝트를 Fork하고 로컬에 Clone 하기

```
git clone git@github.com:username/node.git
cd node
git remote add upstream https://github.com/nodejs/node.git
git fetch upstream
```

Git에서 사용자 설정하기

```
git config user.name "Deokjin Kim"
git config user.email "deokjin81.kim@gmail.com"
```

## Step 2: 로컬 Branch 생성하기

```
git checkout -b my-branch -t upstream/HEAD
```

## Step 3: 코드 수정하기

- `src` 디렉토리: C/C++ 코드
- `lib` 디렉토리: JavaScript 코드
- `doc/api` 디렉토리: 문서
- `test` 디렉토리: Test 코드

코드를 수정하였다면, `make lint` 명령으로 Code Style을 체크한다.

## Step 4: Commit 하기

```
git add my/changed/files
git commit
```

### Commit 메시지 가이드라인 (중요)

1. 첫번째 라인은 subsystem과 imperative verb로 시작해야 한다. </br>
   예제:
   - `net: add localAddress and localPort to Socket`
   - `src: fix typos in async_wrap.h`

2. 두번째 라인은 비워둔다.

3. 모든 다른 라인은 72열을 넘지 않아야 한다.(긴 URL 제외)

4. 오픈된 이슈를 위한 패치는 `Fixes:`를 사용하고, 다른 레퍼런스는 `Refs:`를 사용한다. </br>
   예제:
   - `Fixes: https://github.com/nodejs/node/issues/1337`
   - `Refs: https://eslint.org/docs/rules/space-in-parens.html`
   - `Refs: https://github.com/nodejs/node/pull/3615`

## Step 5: Rebase 하기

필요하다면 main repo와 동기화하기 위해 `git rebase` 한다.

```
git fetch upstream HEAD
git rebase FETCH_HEAD
```

## Step 6: Test 하기

```
./configure && make -j6 test
```

## Step 7: Push 하기

```
git push origin my-branch
```

## Step 8: PR(Pull Request) 열기

## Step 9: 토론 및 업데이트

## Step 10: Landing

- 2명 이상의 Node.js Collaborator로부터 승인을 받은 경우: 2일 후에 Merge
- 1명의 Node.js Collaborator로부터 승인을 받은 경우: 7일 후에 Merge
- 문서 외의 코드 수정이 있다면 Jenkins CI(Continuous Integration) 테스트가 필요하다. </br>
  승인을 받은후, Node.js Collaborator에게 Jenkins CI 테스트 실행을 요청한다.