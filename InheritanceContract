// SPDX-License-Identifier: MIT
pragma solidity ^0.5.7;

contract Will {
    address owner;
    uint fortune;
    bool deceased;

    constructor() payable public {
        owner = msg.sender;  //represents address being called
        fortune = msg.value; //represents how much ether is being sent
        deceased = false; 
    }
    //create modifier so the only person who can call the contract is the owner
    modifier onlyOwner {
        require(msg.sender == owner);
        _;
    }
    //create modifier so funds are only allocated if relative deceased
    modifier mustBeDeceased {
    require(deceased == true);
    _;
    }

    address payable[] familyWallets;

    mapping(address => uint) inheritance;  

    function setInheritance(address payable wallet, uint amount) public onlyOwner {
        familyWallets.push(wallet);
        inheritance[wallet] = amount;
    }

//pay each family member based on wallet address

function payout() private mustBeDeceased {
    for(uint i = 0; i < familyWallets.length; i++) {
        familyWallets[i].transfer(inheritance[familyWallets[i]]);
    }
}

function hasDeceased() public onlyOwner {
    deceased = true;
    payout();
}

}
