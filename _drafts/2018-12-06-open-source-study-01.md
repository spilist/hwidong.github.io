---
title: "오픈소스 스터디: AWS에 첫 PR을 날리기까지"
tags: ["Open Source", "Study", "AWS Codedeploy Agent"]
---

8월 3일부터 전 직장 동료이자 절친인 [김정훈님](https://wonderer80.github.io/), [이지민님](http://americanopeople.tistory.com/)과 함께 매주 수요일 저녁에 스터디를 하고 있다. 첫 10주동안에는 [제랄드 와인버그](https://en.wikipedia.org/wiki/Gerald_Weinberg) 옹의 [Quality Software Management](https://www.amazon.com/Quality-Software-Management-Systems-Thinking/dp/0932633722)(QSM)라는 고전을 함께 읽으며 토론하는 스터디였다. 그 다음 6주는 오픈소스 스터디였는데, [AWS CodeDeploy](https://aws.amazon.com/ko/codedeploy/)라는 아마존의 코드 배포 서비스의 버그 하나를 분석해서 [Pull Request](https://github.com/aws/aws-codedeploy-agent/pull/199)를 올리는 데 성공했다. 

스터디 참여자 모두 오픈소스 프로젝트를 사용만 해봤지, 소스코드를 깊게 파보거나 제대로 기여를 해본 경험은 없었다. 그러나 좌충우돌하며 첫 PR을 날리게 되기까지는 꽤나 흥미로웠다. 다만 한 달이 지난 지금까지도 우리의 PR이 머지는 커녕 댓글 하나 달리지 않았다는 게 안타까울 따름이다.

### 주제 선정 ###

QSM Volume 1-1 스터디를 끝내고 회고를 하며 다음 스터디는 어떤 주제로 할지 논의했다. 여러가지 후보가 있었는데:

1. QSM, 또는 와인버그의 다른 책을 비슷한 방식으로 이어서 읽기
2. 백엔드 기술 전문성을 높이는 활동 (커리어 선택의 폭 넓히기)
3. 공동으로 글쓰기 (팀블로그)
4. 공동으로 스택오버플로우 답변달기
5. 퍼실리테이션, 팀빌딩 액티비티 실습
6. 오픈소스 프로젝트 만들어서 개밥먹기로 학습
7. 강의자료, 학습자료 만들기
8. **기존의 오픈소스 프로젝트 코드 분석해서 코멘트 남기고 PR 올려보기. + 이슈 답변 달아주기**

카페에서 즐겁게 얘기만 하다 보니 정확히 여기서 어떻게 오픈소스로 결정됐는지는 기억나지 않지만, 책으로 스터디를 해봤으니 다른 쪽으로 스터디를 해보자는 것에는 빠르게 합의했던 것 같다. 특히 모두 백엔드 개발자였기에, 백엔드 프로그래밍과 관련된 것으로 해보고 싶었다.

### 대상 프로젝트 선정 ###

각자 몇가지 github 저장소를 후보로 가져왔다. [elasticsearch](https://github.com/elastic/elasticsearch), [AWS code deploy agent](https://github.com/aws/aws-codedeploy-agent), [rspec](https://github.com/rspec/rspec) , [redis](https://github.com/antirez/redis), [git](https://github.com/git/git), [pytest](https://github.com/pytest-dev/pytest), [redash](https://github.com/getredash/redash), [django oscar](https://github.com/django-oscar/django-oscar). 스터디 참여자들이 주로 다뤄왔던 언어가 Ruby였던 관계로, C로 구현된 프로젝트는 모두 순식간에 제외되었다. 그래도 여전히 후보가 많아서 선택하기 어려웠는데, 선택의 폭을 좁혀준 것은 이 기준이었다. `커밋 수가 가장 적은 프로젝트`. 

우리는 실제 문제를 푸는 데 기여하고 싶었고, 너무 많은 시간을 투자하기는 원치 않았기에, 레거시가 적고 파악해야 하는 코드의 양이 적은 프로젝트를 선택하고자 했다. `AWS code deploy agent`는 커밋 수도 적고 역사도 깊지 않았으며, 최근까지도 활발하게 개발이 이루어지고 있었다. 소스코드도 Ruby로 되어있었고 우리 모두 AWS에 관심이 있었으니 훌륭한 선택이라고 생각했다. (~~최근까지도 활발하게 개발이 이루어지고 있었다~~ → 지난 몇 달간 아무 반응 없이 방치된 PR도 많다는 사실은 몰랐다.)

### 스터디에서 기대하는 바 공유 ###

살짝 사족을 달자면 스터디든 미팅이든, 둘 이상이 함께하는 활동에서는 (어쩌면 혼자라도) 각 구성원이 이 활동에서 무엇을 기대하는지 함께 명시적으로 공유하는 게 무척 중요하다고 생각한다. 공동의 목표를 정할 때는 물론이고 각자의 말과 행동, 생각을 이해하는 데에도 큰 도움이 된다. 

기대하는 바, 또는 목표는 모임이 진행되고 구성원의 이해도가 높아지면서 바뀌기 마련인데, QSM 스터디에서도 처음 목표는 꽤 단순했다. 그러다가 중간회고를 하면서 우리가 스터디에서 기대하는 바가 훨씬 멋진(?) 방향으로 바뀌었다는 걸 깨닫고, 이후에는 바뀐 기대를 매 스터디마다 달성하려고 노력했다.

> 1회차: 그저 완독! 각자의 경험을 토대로 이야기하기. 영어로 된 소프트웨어 서적 하나를 끝까지 읽기.
> → 6회차: 시야를 넓히고, 통찰력을 얻기. 책에서 학습한걸 시도해볼 수 있는 에너지를 충전하기.

이번 오픈소스 스터디에서는 각자 기대하는 바가 이러했다. 결과가 어땠는지는 **회고**에서 적어보겠다.

- 정훈
  -  `codedeploy-agent`에 기여하기. (코드 상태 자체가 별로 안좋아서 쉽게 기여할 여지가 있어 보인다)
  - 코드 이해도를 높여서 `codedeploy-agent`에서 웬만한 이슈를 대응할 수 있는 상태가 되기.
  - 레일즈가 아닌 환경에서 도는 복잡한 데몬 스크립트에 대한 이해 높이기.
- 지민
  - 오픈소스를 분석해본다는 자부심 얻기. 
  - codedeploy 소개, 설정시 고려할 점 등을 정리해서 블로그 글 하나 쓰기.
  - 데몬 띄우고, 서비스 실행하는 등의 패턴을 이용하는 프로그램을 더 이해할 수 있는 기반 쌓기
- 휘동	
  - 오픈소스에 작은 기여를 하는 경험을 통해, 나도 오픈소스에 기여할 수 있다는 자신감 얻기.
  - 기존에 내가 생각하고 일하는 패턴을 오픈소스에도 적용해보는 경험 해보기.

### 스터디 환경과 도구 준비 ###

**Github 저장소 생성**

codedeploy agent를 `fork`해서 작업하기 위해 [what-is-quality](https://github.com/what-is-quality/)라는 이름으로 organization을 만들어 스터디 멤버들을 초대했다. 참고로 "What is quality?"는 우리의 1차 스터디 대상이었던 QSM에 나오는 [인상적인 문구](http://secretsofconsulting.blogspot.com/2016/08/what-is-quality-why-is-it-important.html)다.

> What is quality? Quality is value to some person.
> 품질이란 무엇인가? 품질이란 누군가에게 가치가 되는 것이다.

**Fork & Slack integration**

스터디는 1주일에 한 번씩 모이기 때문에, 각자가 스터디 외 시간에 하는 활동이 서로에게 지속적으로 전달되는 게 중요했다. 적절한 동기부여도 되고, 다른 사람이 한 일을 보면서 학습하여 이어서 작업할 수도 있으니까. 

책 스터디 때에는 구글 스프레드시트 문서를 공유해서, 각자가 그 주의 챕터를 읽으며 인상적이었던 문구와 그에 대한 생각을 정리했었다. 하지만 이번 오픈소스 스터디는 주로 github에서 이루어질 것이기 때문에 공유 문서만으로는 충분하지 않았다. 그래서 [slack integration](https://github.com/integrations/slack) 을 추가하여, fork한 저장소에서 각자 생성하는 이슈, 댓글, 커밋, 푸시 등이 `#hooks` 채널에 올라오도록 설정했다.

**위키와 이슈를 이용한 정보 정리 및 공유**

각자 조사해온 정보를 정리하기 위해서 [wiki](https://github.com/what-is-quality/aws-codedeploy-agent/wiki)를 설정했는데 곧 문제가 생겼다. 위키는 잘 정리된 정보를 기록해두는 용도로는 좋았지만, 특히 스터디 초반에는 우리의 이해도가 높지 않아서 정제된 결과물을 만들어내기 어려웠다. 

**모각코: 모여서 각자 코딩하기**