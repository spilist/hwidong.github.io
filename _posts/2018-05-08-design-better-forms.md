---
title: "(번역)더 나은 폼 디자인을 위해"
tags: ["Design", "UX", "Product Design", "Usability", "Interaction Design"]
---

[원문 링크](https://uxdesign.cc/design-better-forms-96fadca0f49c)

입력 폼을 디자인할 때 흔히 하는 실수들과, 그걸 어떻게 고칠 수 있는지 보여주는 글을 요약 정리했다.

---

### 좌우 대신 위아래로

- 폭이 짧다고 여러 column으로 폼을 만들지 말라. 유저가 위에서 아래로 자연스럽게 이동하려고 하는 모멘텀을 방해한다.![img](https://cdn-images-1.medium.com/max/2000/1*XhzxeTnAuWoaeJmlPBP0bw.jpeg)
- 폼의 레이블을 입력 옆에 두지 말고 위에 두어라. 단, 위아래 길이가 짧아짐으로써 입력이 한 눈에 들어오게 해서 얻는 이득이 크다면 옆에 두는 것을 고려해보라.![img](https://cdn-images-1.medium.com/max/2000/1*tnR_OXAKMJW8S9cqRy416A.jpeg)
- 체크박스와 라디오를 좌우가 아닌 위아래로 두라. 유저가 스캔하기 훨씬 쉽다.![img](https://cdn-images-1.medium.com/max/2000/1*VLqTEZP8OrH24FooksePbQ.jpeg)

### 정보를 묶어서 보여주기

- 레이블이 입력과 묶여서 인지될 수 있도록, `레이블과 입력 사이`의 간격을 `입력과 다음 입력의 레이블` 사이의 간격보다 충분히 좁게 하라.![img](https://cdn-images-1.medium.com/max/2000/1*obwyjb54NCWy3sOPfm2WEg.jpeg)
- 관련된 입력들은 묶어서 인지할 수 있게 그룹으로 묶어라. 유저의 인지 부하를 줄여줄 수 있다.![img](https://cdn-images-1.medium.com/max/1600/1*1mPIcYr9ZMmZ4g2Ayf5BPA.jpeg)

### 숨기지 말고 명확하게 보여주기

- 유저가 선택할 수 있는 옵션이 6개 미만이라면 드롭다운으로 숨기지 말고 다 보여줘라. 드롭다운을 사용할 때에도, 옵션이 25개 이상이라면 단순히 스크롤로 선택하는 게 아닌 자동완성되는 검색 기능을 고려해보라.![img](https://cdn-images-1.medium.com/max/2000/1*VvQeOFsY57NJxtZmKyRnHA.jpeg)
- 플레이스홀더를 레이블 대신 사용하지 말라. 이게 좋지 않은 선택인 이유는 [여기](https://www.nngroup.com/articles/form-design-placeholders/)에 잘 정리되어 있다.![img](https://cdn-images-1.medium.com/max/2000/1*XvUnJwHtQhJ3Wl8Apj9lhQ.jpeg)
- 콜 투 액션, 즉 폼의 `제출` 버튼에서 `제출` 대신 의도가 드러나는 텍스트를 사용하라. 이 폼을 제출했을 때 유저는 어떤 경험을 겪는가? 회원가입이라면 애초에 버튼 텍스트를 `회원가입`으로 써라.![img](https://cdn-images-1.medium.com/max/2000/1*VzlN4tj2hQRUel2iNzM9dw.jpeg)
- 유저 입력에 오류가 있을 때는 해당 입력을 강조하고 무엇이 잘못되었는지 알려주어라.![img](https://cdn-images-1.medium.com/max/2000/1*-NXH_4cKK_ngIgrcqShTbg.jpeg)
- 필수 입력 필드에 * 를 넣는 대신, 선택적 필드를 명시적으로 보여줘라.![img](https://cdn-images-1.medium.com/max/2000/1*riNfOVAxTChvaQ29n-6IPQ.jpeg)

### 생각하기

- 입력 필드의 길이는 유용한 힌트가 된다. Zip 코드나 전화번호 등 길이가 정해져있는 필드는 그에 맞는 길이를 사용하는 게 사용자에게 어포던스를 줄 수 있다.![img](https://cdn-images-1.medium.com/max/2000/1*3rOjyzcj68Dm7badROWuxg.jpeg)
- 필수 입력 필드가 아니라면 다른 수단으로 그 데이터를 추론하거나, 입력받기를 미루거나, 아니면 아예 안받을 수는 없는지 생각해보라. 요즘은 SNS 등 정보를 가져올 수 있는 출처도 많다.
- 인생은 짧고 누구도 입력하기를 좋아하지 않는다. 대화형으로, 재미있게, 점진적으로 입력하게 하라. 유저를 (즐겁게) 놀라게 만들고, 브랜드를 드러내라.