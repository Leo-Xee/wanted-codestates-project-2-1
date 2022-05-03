# 원티드 프리온보딩 프론트엔드 코스 - 페이히어

✨[결과물 보러가기](https://wanted-codestates-project-2-1.vercel.app/)✨

## 사용 스택


<p>
  <img src="https://img.shields.io/badge/react-%2320232a.svg?style=for-the-badge&logo=react&logoColor=%2361DAFB" />
  <img src="https://img.shields.io/badge/styled--components-DB7093?style=for-the-badge&logo=styled-components&logoColor=white" />
</p>


## 요구사항

- [x] 1. Repository명을 입력해서 Repository를 검색할 수 있다.
- [x] 2. 검색된 Public Repository를 등록할 수 있다.
  - 등록 개수는 최대 4개로 제한하며, 최대 개수 초과 등록 시 이를 사용자에게 알려준다.
  - LocalStorage로 데이터 저장
- [x] 3. 등록된 Repository를 삭제할 수 있다.
- [x] 4. 등록된 각각의 Public Repository의 issue를 한 페이지에서 모아서 볼 수 있다.
  - 각 issue 마다 제목, Repository 명은 필수로 표현되어야 한다. 그 이외의 데이터 중 필요하다고 생각되는 부분은 추가한다.
  - 해당 issue를 클릭하면 Github의 상세 페이지로 이동할 수 있다.
  - 페이지네이션을 통해서 계속해서 issue를 모아서 볼 수 있다.

## 기능 설명

### Home page

- 요구사항 1, 2, 3 번에 대한 기능을 하고 있습니다.
- Repository 검색 및 리스트 출력 ([박상우](https://github.com/SangWoo9734), [허민](https://github.com/hhhminme))
- Repository LocalStorage 등록 및 삭제 ([신항민](https://github.com/ssinking91), [강동진](https://github.com/jinn2u))

**Repository 검색 및 리스트 출력**

![ezgif com-gif-maker (7)](https://user-images.githubusercontent.com/54930877/155452598-24be39b4-af66-40d7-9214-f96bc94a6438.gif)

Repository 검색은 [Axios](https://axios-http.com/docs/intro)를 활용한 비동기 통신으로 구현을 하였습니다. 검색창에 검색하고자 하는 내용을 param으로 받아 해당 내용에 대해 구현을 하였습니다.
Enter 키와 검색 버튼을 통하여 검색을 실행할 수 있도록 구현하였습니다. 이때 input 내에 글자를 입력할 경우 다른 컴포넌트가 렌더링되는 것을 방지하고자 [useRef](https://reactjs.org/docs/hooks-reference.html#useref)를 사용하여 해당 검색 창의 내용을 가져오도록 구현하였습니다.

통신 후 응답받은 데이터를 출력하기 전에 [react-loader-spinner](https://mhnpd.github.io/react-loader-spinner/)를 활용한 로딩을 구현하였습니다. 출력된 목록은 전체 목록이 출력되어 페이지가 길어진다는 문제점이 있어 처음 10개만 보여지고 사용자가 더보기 버튼을 누르게 될 경우 이후의 30개가 보여지도록 구현하였습니다.

🔥**Repository LocalStorage 등록 및 삭제**
<br/><br/> 
<img src="https://user-images.githubusercontent.com/89959952/155449060-11be1939-8e47-4745-a689-6399b9afdaa7.gif" width="500px" height="300px" title="local" alt="local"></img>
<br/>
- **구현한 방법과 이유**
> 1. 검색된 Public Repository를 **등록**할 수 있다.
>    - 등록 개수는 최대 4개로 제한하며, 최대 개수 초과 등록 시 이를 사용자에게 알려준다.
>    - 웹은 **LocalStorage**, 앱은 Async Storage 등 로컬 저장소를 활용한다. (웹 혹은 앱 선택)
> 2. 등록된 Repository를 **삭제**할 수 있다. 
 
<br/> 

![ezgif com-gif-maker (6)](https://user-images.githubusercontent.com/54930877/155452605-db89f1d1-7e3f-4b1c-b731-9212da1356bf.gif)

사용자 경험을 고려하여 기존 알럿창으로 뜨는 경고창을 모달창으로 변경하여 구현을 하였습니다. 

🔥**Repository LocalStorage 등록 및 삭제([신항민](https://github.com/ssinking91), [강동진](https://github.com/jinn2u))**
<br/><br/> 
<img src="https://user-images.githubusercontent.com/89959952/155350582-76cedb0d-67bb-4770-ab23-024e9ca44dd5.gif" width="500px" height="300px" title="local" alt="local"></img>
<br/>

- 브랜치 전략
    - Feature-RepoAddAndDelete를 Feature 브랜치로 설정
    - Feature-TitleComponent와 Feature-useLocalStorage 두 개의 브랜치를 기능별로 분리
    - rebase merge로 Feature 브랜치에 병합
    -이유
      - rebase merge를 하게 된다면 feature branch에서 보았을 때 일반 merge보다 더 히스토리를 보기 용이하다고 생각했습니다.
      - 또한 단순한 기능을 분리한 브랜치이기 때문에 커밋 내용이 많지 않다고 생각했습니다. 따라서 squash merge를 사용하지 않았습니다.

- 코드 작성시 생각한 점
  - 하나의 함수는 하나의 기능만을 가져간다.
  - 재사용성을 고려한다.
  - early return을 통해 가독성을 고려한다.

- useLocalStorage 구현한 방법과 이유 [pr1](https://github.com/hhhminme/wanted-codestates-project-2-1/pull/9),[pr2](https://github.com/hhhminme/wanted-codestates-project-2-1/pull/10)
    - 구현하기 앞서 어떠한 것을 만들어야 하는지 정의하였습니다.
      1. Public Repository를 등록하기 위해서는 localStorage를 사용한다.
      2. 다른 기능에서도 localStorage를 사용할 수 있으므로 추상화한다.
      3. localStorage는 App에서 사용할 떄 state에 보관한다.
      4. 따라서 useLocalStorage훅을 만들어 localStorage에서 아이템을 가져오고 state에 저장하는 중복작업을 최소화한다.
- titleComponent 구현 방법과 이유 (이 기능은 1팀에서 만든 컴포넌트와 중복 되었기 때문에 논의 후 develop에는 반영하지 않았습니다.)[pr](https://github.com/hhhminme/wanted-codestates-project-2-1/pull/11)
    1. localStorage에 추가하는 부분과 삭제하는 부분은 버튼의 내용만 다르다. 따라서 재사용 가능하게 구현한다.
    2. api에서 데이터가 pagenation되지 않고 한번에 가져오기 때문에 useInterSectionObserver 훅을 만든다.
    3. threshold와 lazy속성을 통해 어느 시점에서 렌더링 할 것인지 정할 수 있다.

- [최종 feature 브랜치](https://github.com/hhhminme/wanted-codestates-project-2-1/tree/Feature-RepoAddAndDelete)
  
 

### Issue page

- 요구사항 4번에 대한 기능을 하고 있습니다. ([전호용](https://github.com/lmooroom), [이장민](https://github.com/leo-xee), [오카무라카에](https://github.com/kaehehehe))
- 각 issue마다 제목, Repository명을 포함한 추가적인 데이터 출력
- 페이지네이션을 통해 issue 모아보기 
- 해당 issue 클릭 시에 Github의 상세 페이지로 이동

#### 🔥 각 issue마다 제목, Repository명을 포함한 추가적인 데이터 출력과 페이지네이션을 통한 issue 모아보기

![payHere_demo1](https://user-images.githubusercontent.com/21965795/155453090-bd07558c-8d5d-49df-8966-22be85caf863.gif)


#### 🔥 해당 issue 클릭 시에 Github의 상세 페이지로 이동

![payHere_demo2](https://user-images.githubusercontent.com/21965795/155453111-3ce602c8-37ca-4d55-8c2f-50ef4c1bd806.gif)


<br />

## 팀원 소개

| 이름         | 깃허브                                        |
| ------------ | --------------------------------------------- | 
| 강동진       | [jinn2u](https://github.com/jinn2u)           | 
| 박상우       | [SangWoo9734](https://github.com/SangWoo9734) | 
| 신항민       | [ssinking91](https://github.com/ssinking91)   | 
| 이장민       | [leo-xee](https://github.com/leo-xee)         | 
| 오카무라카에 | [kaehehehe](https://github.com/kaehehehe)     | 
| 허민         | [hhhminme](https://github.com/hhhminme)       |
| 전호용       | [mooroom](https://github.com/mooroom)         | 
