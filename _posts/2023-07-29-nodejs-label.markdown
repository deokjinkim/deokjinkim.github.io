---
layout: post
title: Node.js 주요 Label 설명
date: 2023-07-29 16:25:00 +0900
category: Opensource
---

# Node.js 주요 Label
- `author ready`  
  적어도 1개 이상의 승인을 받았고, 추가 변경 요청이 없을 경우.  
  PR Author는 추가로 할일이 없으며 PR이 Land되기를 기다리면 된다.  

- `commit-queue`  
  Github Action을 사용하여 PR을 Land.  
  2명 이상의 승인을 받은 경우 Collaborator에 의해서 해당 Label이 붙으면, 48시간(PR 생성 시간 기준) 이후에 Land 된다.  

- `commit-queue-failed`  
  Github Action을 사용하여 PR을 Land하려다 실패한 경우.  
  Bot이 PR Land를 시도했으나, 승인 또는 CI 수행 조건 등이 만족되지 않아 실패한 경우, bot이 해당 Label을 붙인다.  

- `commit-queue-squash`  
  PR의 모든 commit을 하나로 Squash.  
  첫번째 commit이 commit message guideline을 맞추어 작성된 경우, 추가 commit을 squash하기 위해 붙인다.  

- `fast-track`  
  PR을 Land하기 위해 48시간을 기다릴 필요가 없는 경우.  
  Collaborator가 thumb up 버튼을 2개 이상 누르면, bot이 PR을 Land한다.  

- `needs-ci`  
  JS, C++ 코드가 변경되어 Jenkins CI 수행이 필요한 경우.  
  Collaborator(또는 Triager)가 아닌 경우 권한이 없기 때문에, 권한을 가진 사람에게 CC(Ex. cc @deokjinkim)하여 부탁한다.

- `semver-major`  
  Breaking Change를 포함하고 있어 다음 Major Release에 포함되어야 하는 경우.  
  다른 PR과 달리 TSC 멤버 2명 이상의 승인이 필요하며, 승인을 받아도 다음 Major Release에 포함된다.  

- `notable-change`  
  Changelog에 포함되어야 하는 PR인 경우.  

- `dont-land-on-v18.x`  
  v18 버전에 Land되면 안되는 PR인 경우.  
