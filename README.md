# ironclad
learning code// SPDX-License-Identifier: MIT
pragma solidity ^0.8.22;

contract icfirsttryAI  {
    string public symbol;
    string public name;
    uint8 public decimals;
    uint public _totalSupply;
    mapping(address => uint) balances;
    mapping(address => mapping(address => uint)) allowed;

    event Transfer(address indexed from, address indexed to, uint tokens);

   constructor() {
    // constructor logic
        symbol = "iftai";
        name = "icfristtry IA";
        decimals = 2;
        _totalSupply =100000;
        balances[msg.sender] = _totalSupply;
        emit Transfer(address(0), msg.sender, _totalSupply);
    }

    function totalSupply() public view returns (uint) {
        return _totalSupply - balances[address(0)];
    }

    function safeSub(uint a, uint b) public pure returns (uint c) {
        require(b <= a, "Subtraction underflow");
        c = a - b;
    }

    function transfer(address to, uint tokens) public returns (bool success) {
        balances[msg.sender] = safeSub(balances[msg.sender], tokens);
        balances[to] = safeAdd(balances[to], tokens);
        emit Transfer(msg.sender, to, tokens);
        return true;
    }
    
    function safeAdd(uint a, uint b) internal pure returns (uint c) {
        c = a + b;
        require(c >= a, "Addition overflow");
    }
}

