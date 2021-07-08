# 리액트로 구현하는 블록체인 이더리움 ERC721(NFT)


## 1. 이더리움 Dapp 구성과 토큰 표준 (ERC721)

### 1.1 이더리움 Dapp
   - ![image](https://user-images.githubusercontent.com/58179041/124739207-9e3d5a80-df54-11eb-8d11-7ec616316c7e.png)
   - 백앤드 로직에 해당하는 부분이 스마트 컨트랙으로 구현이 가능하고, 화면은 프론트 앤드 개발로 보아도 무방함
   - 즉, 웹 개발용인 자바스크립트, HTML, CSS를 사용하게 될 것
       - Drizzle-react: 리액트 어플리케이션 개발할 때 꽤 많은 자바스크립트 모듈을 사용해야 하는데, 그것들을 미리 작성하고 제공함 -->Truffle box
   - 이더리움 Dapp = UL + Smart Contract
       - 이더리움 Dapp은 자바스크립트 뿐만이 아니라, Java, Python, .Net, Go 등 다양한 언어에서 개발이 가능하다. 라이브러리는 web3.js

### 1.2 ERC-721
   - Token
      - 특정 서비스에서 구매 등의 목적에 맞게 사용할 수 있는 교환 수단, 넓은 의미로는 다음과 같음, 화폐 ex) 이용권, 카지노, 칩, 각종 포인트, 암호화폐 "코인"
      - 가상 화폐도 넓은 의미에서 토큰이지만, 가상 화폐 세계에서 공용적으로 사용하는 것으로 화폐라고 보는 거이 일반적임
      - 이더리움은 공용 코인 ETH 외에 누구나 임의의 토큰을 발행할 수 있는 표준을 제공 --> Ex) ERC-20, ERC-721
      - Q) 이미 코인이 있는데 왜 토큰을 발행하는가?
         - A) 프로젝트를 수행하기 위한 거대한 투자를 유치해야 하는데, 증권형 토큰을 발행해줌 (토큰 구매 기록을 이더리움 블록체인 스마트컨트랙트에 기록하는 행위) 
   - Non-funcgibal Token (NFT)
      - ![image](https://user-images.githubusercontent.com/58179041/124741624-de054180-df56-11eb-815a-664552ceeb6f.png)
      - 서로 가치가 상이하지 않아서 교환할 수 없는 것, 대체 불가 (고유한 ID) Ex) 크립토키티의 고양이들
      - Non-fungible Token (NFT) = Deed (권리증)
         - 실물 자산 - 부동산, 예술품
         - 가상 자산 - 특별한 그림, 디지털 자산
         - "Negative value" assest - Loans, burdens and other respnsibilites 채무
         - ![image](https://user-images.githubusercontent.com/58179041/124742089-5a982000-df57-11eb-892d-6d1e2b7312c3.png)
         - ![image](https://user-images.githubusercontent.com/58179041/124742233-78fe1b80-df57-11eb-9133-f273d6dca605.png)
         - ![image](https://user-images.githubusercontent.com/58179041/124742276-81eeed00-df57-11eb-96fd-f7616be79755.png)
         - ![ezgif com-gif-maker (1)](https://user-images.githubusercontent.com/58179041/124754635-6854a200-df65-11eb-951b-bef361d5a008.gif)
---
## 2. 개발환경 구성

### 2.1 교육 자료 다운로드

### 2.1 트러플, 가나슈, 드리슐 설치



