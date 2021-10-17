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
   - (2) 폐기되는 인덱스 ID 자리에, 새로운 토큰으로 업데이트를 해준다.
   - (3) 끝에 있던 토큰 ID 111번이 INDEX 1번에 들어가게 되고
   - (4) 토큰 ID 110번이 폐기되었음으로 배열의 길이를 하나 줄여준다.
   - solidity 에서는 고정길이 배열이 있고, 가변길이 배열이 있다. 선언된 가변길이 배열과 같은 경우에는 인덱싱이 가능하면, 수정이 가능하다.
   - ![image](https://user-images.githubusercontent.com/58179041/137618460-383a43ed-dd59-421b-8f21-fe19125e92b4.png)
   - 여러가지 방식으로 토큰ID를 생성할 수 있는데, 보통 일련번호를 많이 사용한다.여기에서도 일련변호를 토큰 ID로 사용한다. 
   - alltokens라는 배열에 발행할때마다 push하게 되는데, return되는 배열 길이를 이용한다. 즉, 토큰 ID는 0부터 시작하고, 현재 길이에서 1을빼면 그것을 방금 추가한 토큰의 아이디로 사용이 가능해진다.
   - tokenOwners라는 토큰 장부가 만들어지고, 그것에 저런식으로 되어있으면, 폐기 토큰도 저장이되나 소유주는 0이다.
   - ![image](https://user-images.githubusercontent.com/58179041/137618603-3958e8ac-e22b-47ff-8f59-0847ad9c31a7.png)
   - 사용하는 라이브러리 중에 address는 ERC721에서 소유권을 넘겨받는 계정이 contract인지 아닌지를 검토해봐야 한다.


### 3.4 컨트랙트 구현(1) - 기본 인터페이스 (Deeptoken.sol)
    pragma solidity 0.5.16;

    import "./ERC721.sol";
    import "./ERC165.sol";
    import "./SafeMath.sol";
    import "./Address.sol";

    contract DeedToken is ERC721, ERC165 {

    using SafeMath for uint256;
    using Address for address;

    address payable public owner;
    //mapping 타입의 selector가 true or false를 리턴할 수 있도록 변수 하나를 선언해
    mapping(bytes4 => bool) supportedInterfaces;
    //토큰의 소유자 정보를 담고 있는 mapping 타입으로 선언
    mapping(uint256 => address) tokenOwners;
    //특정 소유자가 가진 토큰의 수를 담을 수 있는 mapping 타입으로 선언
    mapping(address => uint256) balances;
    //어떤 토큰 ID를 어떤 address가 소유권 이전 승인의 권리를 가지고 있는가?
    mapping(uint256 => address) allowance;
    //어떤 소유자 계정이 다수에게 자신이 가진 토큰을 관리할 수 있도록 정보를 저장해야 하기 때문에 중계인 계정 address가 이제 boolean 타입으로..
    mapping(address => mapping(address => bool)) operators;
    //struct 타입의 asset의 구조체가 담고 있는 것은, 우리가 구현할 이미지의 얼굴, 눈, 입모
    struct asset {
        uint8 x; //face
        uint8 y; //eyes
        uint8 z; //mouth
    }
    //asset 모 구조체를 담을 수 있는 구조체 배열을 선언해준다.
    asset[] public allTokens;

    //for enumeration
    //유효한 토큰 아이디만 가지는 배열
    uint256[] public allValidTokenIds; //same as allTokens but does't have invalid tokens
    //토큰 아이디를 가지고 인덱스을 구할 수 있는.. 앞에 있는 것은 토큰 ID, 뒤에 있는 것은 INDEX
    mapping(uint256 => uint256) private allValidTokenIndex;


    modifier onlyOwner {
        require(msg.sender == owner, "Only owner can call this function.");
        _;
    }
    //public 생성자를 만들어, supportedInterfaces에 ERC 721의 selector값을 넣어줘야 true를 리턴할 수 있도
    constructor() public {
        owner = msg.sender;
        //ERC721.sol안에 들어 있음 아래의 0x01ffc9a7, 0x80ac58cd 이것들 생성자에서 초기화를 해주고 나서, supportsInterface구현하면 된다.!
        supportedInterfaces[0x01ffc9a7] = true; //ERC165
        supportedInterfaces[0x80ac58cd] = true; //ERC721
    }

    function supportsInterface(bytes4 interfaceID) external view returns (bool){
        //interface ID에 맞는 것이 있다면, true를 리턴하고 아니면 false를 리턴하게 될 것!
        return supportedInterfaces[interfaceID];
    }
    //ERC 721.sol에 제공되어있는 함수를 가져온 것,
    function balanceOf(address _owner) external view returns (uint256) {
        //토큰 소유 계정을 키로해서 그 값을 리턴해주면 된다 (== 소유 계정의 총 토큰 )
        require(_owner != address(0));
        return balances[_owner];
    }

    function ownerOf(uint256 _tokenId) public view returns (address) {
        //address owner는 우리가 tokenid 를 넣게 되면, tokenowers의 함수는 토큰 소유 계정을 리턴하여 준다. 여기서 조건 하나를 체크해야 한다!
        address addr_owner = tokenOwners[_tokenId];
        //조건: 소유자 계정이 address 가 (0) (== 즉 소유자가 없다면, 예외를 발생시켜라)
        require(
            addr_owner != address(0),
            "Token is invalid"
        );
        //괜찮다면, addr_owner를 리턴해주면 된다.
        return addr_owner;
    }
### 3.5 컨트랙트 구현(2) - 기본 인터페이스 (Deeptoken.sol)
    STEP2: 토큰 소유권 이전
    function transferFrom(address _from, address _to, uint256 _tokenId) public payable {
        //ownderOf에 tokenid를 넣어서, 토큰의 소유 계정을 가져오고 여기서 조건을 체크한다.
        address addr_owner = ownerOf(_tokenId);
        //파라미터로 받는 from 계정이 token의 오너와 일치해야 한다. 일치 하지 않은 경우, 예외 처
        require(
            addr_owner == _from,
            "_from is NOT the owner of the token"
        );

        require(
            //to 계정은 address(0)이 되면 안된다, 이렇게 되면 소유권 이전이 아니라, 토큰이 사라지는
            _to != address(0),
            "Transfer _to address 0x0"
        );
        //토큰 소유권 권리가 있는 allowance에 있는 계정들이면 가능하다. 그래서 해당 토큰 계정이 allowance에 있는 지 확인한다.
        address addr_allowed = allowance[_tokenId];
        //중개인 계정의 소유권 이전할 수 있는 권리가 true인지 승인을 할 수 있는 지 여
        bool isOp = operators[addr_owner][msg.sender];
        //msg 호출 계정이 소유계정이나, allowance에 있는 계정인지, 혹은 중개인 계정인지, 이 세 개 중 하나가 걸리면 통과!
        require(
            addr_owner == msg.sender || addr_allowed == msg.sender || isOp,
            "msg.sender does not have transferable token"
        );

        
        //transfer : change the owner of the token
        //토큰의 주인을 to 계정으로 바꿔준다. 
        tokenOwners[_tokenId] = _to;
        //from 계정의 balance는 한 개가 줄게 된다.
        balances[_from] = balances[_from].sub(1);
        //to계정의 balance는 한개가 늘어나게 됌.
        balances[_to] = balances[_to].add(1);

        //reset approved address
        //소유 계정이 바뀌었기 때문에, 이전 allowance에 있던 소유권 이전이 가능했던 그 계정을 reset 해주어야 한다. 
        if (allowance[_tokenId] != address(0)) {
            //delete 라는 키워드를 써서 지워주면, 저 안에 값이 0이 된다.
            delete allowance[_tokenId];
        }
        //ERC721.sol에 존재하는 함수 transfer가 되었다 라는 event를 발생시키면 된다.
        emit Transfer(_from, _to, _tokenId);

    }
    //transferfrom..
    function safeTransferFrom(address _from, address _to, uint256 _tokenId, bytes memory data) public payable {
        //바로 호줄해서, 
        transferFrom(_from, _to, _tokenId);

        //check if _to is CA
        //to 계정이 컨트랙트 계정이냐 아니냐에 따라 하나를 더 체크해주어야 한다.
        if (_to.isContract()) {
            //to 계정으로 ERC721TokenReceiver.onERC721Received이 함수를 호출한다. selector가 나와야 한다.
            bytes4 result = ERC721TokenReceiver(_to).onERC721Received(msg.sender, _from, _tokenId, data);
            //
            require(
                result == bytes4(keccak256("onERC721Received(address,address,uint256,bytes)")),
                "receipt of token is NOT completed"
            );
        }

    }
    //파라미터가 하나 없는 safeTransferFrom이다. 
    function safeTransferFrom(address _from, address _to, uint256 _tokenId) public payable {
        //마지막 data만 빈 값을 제공한다.
        safeTransferFrom(_from, _to, _tokenId, "");
    }

    //
    function approve(address _approved, uint256 _tokenId) external payable {

        address addr_owner = ownerOf(_tokenId);
        bool isOp = operators[addr_owner][msg.sender];

        require(
            addr_owner == msg.sender || isOp,
            "Not approved by owner"
        );

        allowance[_tokenId] = _approved;

        emit Approval(addr_owner, _approved, _tokenId);
    }

    function setApprovalForAll(address _operator, bool _approved) external {
        operators[msg.sender][_operator] = _approved;
        emit ApprovalForAll(msg.sender, _operator, _approved);
    }


    function getApproved(uint256 _tokenId) external view returns (address) {
        return allowance[_tokenId];
    }

    function isApprovedForAll(address _owner, address _operator) external view returns (bool) {
        return operators[_owner][_operator];
    }
### 3.6 컨트랙트 구현(3) - 기본 인터페이스 (Deeptoken.sol)
    //STEP3: 토큰 생성, 삭제 후 인덱싱 다시 하는 함
    //non-ERC721 standard
    //
    //
    function () external payable {}
    //토큰 생성 함수, 이미지 토큰 
    function mint(uint8 _x, uint8 _y, uint8 _z) external payable {
        //함수 내부에서만 쓰는 newAsset변수를 선언하고, asset을 통해서 구조체 하나 생성
        asset memory newAsset = asset(_x, _y, _z);
        //푸쉬를 했을때에 return은 배열의 길이가 나온다, 인덱스를 토큰 아이디로 사용하기로 함 0번부터
        uint tokenId = allTokens.push(newAsset) - 1;
        //token id starts from 0, index of assets array
        tokenOwners[tokenId] = msg.sender;
        //장부. 밸런스도 한개가 늘어났다.
        balances[msg.sender] = balances[msg.sender].add(1);

        //for enumeration
        //현재 만들어진 토큰 아이디를 넣고, 인덱스를 저장해준다.
        allValidTokenIndex[tokenId] = allValidTokenIds.length;
        //index starts from 0
        allValidTokenIds.push(tokenId);
        //처음에 생성자는 없기 때문에 address (0)이 들어간다.
        emit Transfer(address(0), msg.sender, tokenId);
    }
    //토큰 삭제, 토큰 아이디를 parameter로 받는다.
    function burn(uint _tokenId) external {
        //addr_owner 해당 토큰의 소유 계정을 구한다음에.
        address addr_owner = ownerOf(_tokenId);
        //msg.sender가 소유자 계정이랑 같은지 확인을 한다.
        require(
            addr_owner == msg.sender,
            "msg.sender is NOT the owner of the token"
        );

        //reset approved address
        //토큰의 소유권 이전을 할 수 있도록 계정들을 모아놓은 allowance.
        if (allowance[_tokenId] != address(0)) {
            //없다면, 토큰 자체를 지워준다.
            delete allowance[_tokenId];
            // tokenId => 0
        }

        //transfer : change the owner of the token, but address(0)
        //삭제하는 토큰에 address (0)을 넣어준다.
        tokenOwners[_tokenId] = address(0);
        balances[msg.sender] = balances[msg.sender].sub(1);

        //for enumeration
        removeInvalidToken(_tokenId);
        //burn 할때 transfer계정이 꼭 있어야 한다.
        emit Transfer(addr_owner, address(0), _tokenId);
    }
### 3.7 컨트랙트 구현(4) - 기본 인터페이스 (Deeptoken.sol)
   

    function removeInvalidToken(uint256 tokenIdToRemove) private {

        uint256 lastIndex = allValidTokenIds.length.sub(1);
        uint256 removeIndex = allValidTokenIndex[tokenIdToRemove];
        //마지막 토큰 아이디는 배열의 last 인덱스 값을 넣어줌으로써 구할 수 있다.
        uint256 lastTokenId = allValidTokenIds[lastIndex];

        //swap
        //이 두 개의 자리를 바꿔준다. 
        allValidTokenIds[removeIndex] = lastTokenId;
        allValidTokenIndex[lastTokenId] = removeIndex;

        //delete
        //Arrays have a length member to hold their number of elements.
        //Dynamic arrays can be resized in storage (not in memory) by changing the .length member.
        //유효한 토큰의 길이를 줄여준다.
        allValidTokenIds.length = allValidTokenIds.length.sub(1);
        //allValidTokenIndex is private so can't access invalid token by index programmatically
        //페기되는 토큰의 인덱스는 0으로 만들어준다, 의미는 X
        allValidTokenIndex[tokenIdToRemove] = 0;
    }

    //ERC721Enumerable
    //현재까지 발행된 유효한 토큰의 전체 개수
    function totalSupply() public view returns (uint) {
        return allValidTokenIds.length;
    }

    //ERC721Enumerable
    //인덱스로 토큰 아이디를 가져오는 것.
    function tokenByIndex(uint256 index) public view returns (uint256) {
        //인덱스는 토탈 서플라이보다 작아야 한다.
        require(index < totalSupply());
        return allValidTokenIds[index];
    }

    //ERC721Metadata
    //이모지토큰이라는 이름을 리턴해준다.
    function name() external pure returns (string memory) {
        return "EMOJI TOKEN";
    }

    //ERC721Metadata
    //ENJ라는 토큰 심볼을 리턴한다.
    function symbol() external pure returns (string memory) {
        return "EMJ";
    }
    function kill() external onlyOwner {
        selfdestruct(owner);
    }
    
### 3.8 트러플 컴파일, 배포, 단위 테스트


---
## 4. 드리즐(drizzle)
