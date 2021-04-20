# ERC-20

## EIP20 と ERC20

Ethereum には EIP（Ethereum Improvement Proposal）と呼ばれるシステム改善提案の仕組みがあり、Bitcoin の BIP（Bitcoin Improvement Proposal）と同様、システム改善の草案が提出され議論が行われます。Ethereum ベースのトークンのインターフェースの標準「ERC20」を提案した EIP20 は Fabian Vogelsteller 氏と Vitalik Buterin 氏によって 2015 年 11 月に提出され、2017 年 9 月に採用が決定しました。EIP20 については GitHub の EIP のリポジトリで公開されています。

EIPs/eip-20-token-standard.md at master · ethereum/EIPs · GitHub

ERC20 というトークンの標準が公式に確立されたことで、トークンの転送やトークンの情報を取得するといった処理を共通のインターフェースで扱えるようになりました。

## なぜ ERC20 が生まれたのか

Ethereum はビットコインコミュニティーの若きプログラマー Vitalik Buterin 氏が考案し、ブロックチェーン上でスマートコントラクトと呼ばれるプログラムを実行できるプラットフォームとして 2015 年 7 月に β 版がローンチされました。Ethereum プラットフォーム上には多くのアプリケーションがリリースされ、2017 年 9 月に ERC20 が正式に採択される前から草案に基づくトークンが発行されてきました。背景には分散型取引所やウォレットの開発で統一されたインターフェースが求められたことや、利用者側のさまざまなトークンを一元管理したいといった事情がありました。

## ERC20 を使うメリット

少し技術的な内容になりますが、実際に ERC20 をコードとして見てみましょう。Ethereum コミュニティーによる The Ethereum Wiki に ERC20 を満たすように書かれたインターフェースコントラクトが掲載されています。EIP20 の GitHub のページにリストアップされている ERC20 トークンに必須のメソッドやイベントの名前、引数、戻り値などをコードに見ることができます。

```typescript:ERC20
// ----------------------------------------------------------------------------
// ERC Token Standard #20 Interface
// https://github.com/ethereum/EIPs/blob/master/EIPS/eip-20-token-standard.md
// ----------------------------------------------------------------------------
contract ERC20Interface {
    function totalSupply() public constant returns (uint);
    function balanceOf(address tokenOwner) public constant returns (uint balance);
    function allowance(address tokenOwner, address spender) public constant returns (uint remaining);
    function transfer(address to, uint tokens) public returns (bool success);
    function approve(address spender, uint tokens) public returns (bool success);
    function transferFrom(address from, address to, uint tokens) public returns (bool success);

    event Transfer(address indexed from, address indexed to, uint tokens);
    event Approval(address indexed tokenOwner, address indexed spender, uint tokens);
}
// ----------------------------------------------------------------------------
// ERC Token Standard #20 Interface
// https://github.com/ethereum/EIPs/blob/master/EIPS/eip-20-token-standard.md
// ----------------------------------------------------------------------------
contract ERC20Interface {
    function totalSupply() public constant returns (uint);
    function balanceOf(address tokenOwner) public constant returns (uint balance);
    function allowance(address tokenOwner, address spender) public constant returns (uint remaining);
    function transfer(address to, uint tokens) public returns (bool success);
    function approve(address spender, uint tokens) public returns (bool success);
    function transferFrom(address from, address to, uint tokens) public returns (bool success);

    event Transfer(address indexed from, address indexed to, uint tokens);
    event Approval(address indexed tokenOwner, address indexed spender, uint tokens);
}
```

ERC20 トークンを提供する側は、このようなインターフェースの中身を実装することになります。ERC20 トークンをプログラムで扱う側、たとえば分散型取引所やウォレットでは共通のインターフェースがあることでトークンごとに個別の処理を記述する必要がなく、どの ERC20 トークンに対しても転送であれば tranferFrom メソッドを使うといったように処理を共通化し、実装をシンプルにすることができます。トークンの保有者には ERC20 に対応したウォレットで ERC20 トークンを一括して管理できるというメリットもあります。また、ICO では ERC20 トークンを発行することで、参加者のトークン管理の利便性を高め、ICO においてより多くの資金を調達することが期待できます。

ERC20 トークンやそれを扱うスマートコントラクトを開発する場合、OpenZeppelin という Solidity で書かれた安全性を重視したスマートコントラクトのオープンフレームワークを使うとよいでしょう。実装の手間を省くというだけでなく、独自のコードに起因する事故を防ぐという点でも有用です。OpenZeppelin では、StandardToken というスマートコントラクトとして ERC20 の実装を提供していて、EIP20 のページでも名前が挙がっています。

OpenZeppelin は利用した組織が、これまでにトタールで 450 百万ドル以上を調達したというぐらい、広く使われいてます。
