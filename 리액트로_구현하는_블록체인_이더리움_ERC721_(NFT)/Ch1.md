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

## 2. 개발환경 구성 (21/07/08)

### 2.1 교육 자료 다운로드
   
### 2.1 트러플, 가나슈, 드리슐 설치 (21/07/21)
   - 개발환경 구성
      - 소스 파일 작성 도구 - 편집기
         - Yakindu
         - Atom + Solidity package
         - IntelliJ IDEA/Webstorm + Solidity plugin
         - Remix : web-based Solidity IDE  
      - solidity 컴파일러, 단위테스트, 베포 도구
      - 이더리움 노드 (로컬 개발용)
      - 웹 개발 서버 - 프론트엔드 개발

---
## 3. ERC721 표준

### 3.1 NFT, Deed의 개념과 토큰 표준

   - A standard interface for non-fungible tokens, also known as deeds(소유권 증명서)
   - ![image](https://user-images.githubusercontent.com/58179041/130433796-6cfa7268-d493-43c0-a279-d08a07c516b0.png)
   - interface 인터페이스
      - 구현부(body)가 전혀 없이 함수를 선언한 컨트랙트 (하나라도 구현한 것이 있으면 추상 컨트랙트)
      - 함수는 external로 선언되어야 하고(외부에서만 호출가능),생성자와 상태변수를 가질 수 없음 (직접 내에서 호출은 안된다.
      - 다중 인터페이스는 가능
   - ERC-721 표준에 정의된 인터페이스
      - ![image](https://user-images.githubusercontent.com/58179041/130434202-6b66c9f9-7c71-43da-a8c5-2ea5281aa968.png)
      - ERC-721 메인 인터페이스
      - ![image](https://user-images.githubusercontent.com/58179041/130434271-fa5c240c-17a0-47f4-b86f-48fdb58fb1c2.png)
   - 기타 사항
      - ![image](https://user-images.githubusercontent.com/58179041/130434476-35f57995-1e8a-429d-894d-bd24ad84e14e.png)
      - 토큰 ID는 정해진 표준 규격이 없지만, 유니크 해야 하긴 한다.

### 3.2 ERC721 인터페이스

   - ![image](https://user-images.githubusercontent.com/58179041/130436048-d450e1eb-bd24-4513-acc9-8e9f4a1cae0d.png)
   - ERC165는 ERC721이 구현되었다는 것을 True 값으로 바꿔주며 알려줄 부분
   - "this.~"이 부분은 selection 부분을 모두 xor 연산을 진행하여서 그 값을 그 함수에 전달했을 때에 'true'가 나오면 그 값이 전달이 되었다라는 의미 (아래 이미지 포함)
   - ![image](https://user-images.githubusercontent.com/58179041/130436365-baa4262c-2e9e-4a0d-8d81-aac0d00fc410.png)
   
   - ![image](https://user-images.githubusercontent.com/58179041/130436497-ac5857eb-fcd8-4b70-913b-005b1cf6175a.png)
   - 특정 상황에 따라 각각 이벤트가 발생하도록 하게 함
   - ![image](https://user-images.githubusercontent.com/58179041/130436713-7a3d1821-9054-40ba-8f55-16ea079617c1.png)
   - bytes data는 부가적인 데이터를 줄 수 있는 함수, tokenid는 어떤 토큰을 넘겨줄 것인지, 소유권이 한번 넘어가게되면 블록체인에는 계정정보가 존재하지 않아서 굉장히 찾기가 어려워진다. 그래서 code size>0 클 경우 한번 더 체크해본다. 한번 트랜색션이 성공하면 거의 끝난다! 조심!
   - ![image](https://user-images.githubusercontent.com/58179041/130437666-bf80390a-74ee-4f6d-a7e5-cfee64001031.png)
   - ![image](https://user-images.githubusercontent.com/58179041/130437899-67b572e7-fd3a-49f5-91de-a8b0c9e2eb53.png)
   - 확장 인터페이스 부분
   - 유효한 토큰 수: 소유 계정이 존재하고 있는 토큰의 총합
   - TokenOfOwnerByIndeex 부분은 토큰 ID를 조회하는 부분
   - ![image](https://user-images.githubusercontent.com/48021223/136767338-5a9c74be-44f1-43f1-9c1c-49a5b788c350.png)
   - Meta 정보를 토근 ID쪽으로 리턴해주는 정보
   - tokenURI : 토큰의 return 하는 정보 (url, ipfs 파일의 해쉬값 등을 문자열 형태로)
   - 

### 3.3 컨트랙트 - 주요로직

   - ![image](https://user-images.githubusercontent.com/48021223/136767895-eb34118f-65b6-4509-ab81-7acfe2cf6c94.png)
   - 우리가 작성할 컨트랙트 이름은 Deedtoken이며, 이것을 작성하기 위해서 ERC 721, 165 인터페이스를 구축를 하고, SafeMath와 Address 라이브러리를 사용할 것이고, 이것들은 Solidity 프로그래밍에서 자주 활용되는 OpenZeppelin repo에서 가져오도록 한다.
   - ![image](https://user-images.githubusercontent.com/48021223/136768200-56f840db-96df-4a0b-bb4c-87011261d2e2.png)
   - Solidity 의 major 버전이 바뀌면서, 다수의 breaking changes 있다. 1) 두 가지는 address에 payable이 붙을 수 있다. 2) reference type의 변수를 전달할 때에는 명시적으로 memory라고 적어주어야 한다. 이에 맞춰서 컨트랙트를 수정!
   - ![image](https://user-images.githubusercontent.com/48021223/136768480-9fa2d42e-9e75-4cd1-ae2e-1700764fb4af.png)
   - 각 이미지를 벡터 조합 -> unsigned int 타입으로 x, y, z에 저장하고 그것들을 토큰 ID와 연결
   - asset[]는 이미지를 나타내는 구조체의 배열을 의미
   - ![image](https://user-images.githubusercontent.com/58179041/136769061-86f89e8e-f97e-4a64-8afb-4d2143084d94.png)
   - 토큰 목록을 화면에 표시하려면 Enumeration이 필요하다. 
   - unit256 [] 배열: 인덱스로 토큰 ID를 가져오려면, 이런 구조의 allValidTokenIds (폐기, 삭제가 아닌 유효한 토큰들)가 만들어져 있어야 한다. 
   - mapping(unit256 => uint256) : 부가적으로, 반대로 토큰ID로 인덱스를 가져올 수 도 있다. 
   - ![image](https://user-images.githubusercontent.com/58179041/136807354-f01baca0-315f-449b-8a29-1b8afd9d6c85.png)
   - 인덱스는 total supply 보다 작아야 한다 = 토큰이 하나 폐기되면 인덱스를 다시 매겨야 한다.
   - (1) 만약 토큰 ID 110이 사라진다고 한다면, 토큰 ID에 해당하는 폐기 되는 토큰과 마지막 토큰 ID를 구한다. 
   - (2) 폐기되는 인덱스 ID 자리에, 새로운 토큰으로 업데이를 해준다.


### 3.4 컨트랙트 구현(1) - 기본 인터페이스
### 3.5 컨트랙트 구현(2) - 기본 인터페이스
### 3.6 컨트랙트 구현(3) - 기본 인터페이스
### 3.7 컨트랙트 구현(4) - 기본 인터페이스
### 3.8 트러플 컴파일, 배포, 단위 테스트


---
## 4. 드리즐(drizzle)
