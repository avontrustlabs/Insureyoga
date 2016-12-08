
A blockchain ased system to unify identification data from all countries into a borderless global  passport. This is the top hack idea proposed and we would like to have a crack at it with our own approach. Our identity system will also have sub-modules that will allow this decentralized ledger to operate insurance, land, relationships, financial matters seamlessly.

Web and mobile app (to be built)

Proposed dependencies

PHP 5 core lib /
Lavarel framework /
Google php lib /
Amazon AWS php lib /
Php word and excel file readers /

Compiled Modules Will not be published here

Usage:

1.Sends national identity number to generate blockchain public key https://form.io/view/#/rgqhelvairpeltf/mgi?header=1

2.Send public key to smart contract deployed on Ehtereum blockchain at: 
to generate global identity

3 Use the newly generated smart contract identity key for borderless applications !

http://www.uncitral.org/uncitral/en/uncitral_texts/arbitration/2010Arbitration_rules.html

https://en.wikipedia.org/wiki/International_arbitration


/*
Draft Smart Contract 

*/

import "github.com/Arachnid/solidity-stringutils/strings.sol";

contract Verificator {

    string public creator;
    mapping (address => bytes32) public stringToSign;
    mapping (address => string) public signedString;
    mapping (address => string) public keyFingerprint;
    mapping (address => string) public urlToVerifyKey;
    string urlBase;

    function Verificator(){
        creator = "www.identityo.ga";
        urlBase = "https://formview.io/#/rgqhelvairpeltf/mgi";
    }

    function getStringToSignWithKey(string _fingerprint) returns (bytes32) {

        keyFingerprint[msg.sender] = _fingerprint;
        urlToVerifyKey[msg.sender] = strings.concat(
                                        strings.toSlice(urlBase),
                                        strings.toSlice(_fingerprint)
                                    );

        var strToSign = sha3(
                msg.sender,
                block.blockhash(block.number),
                block.timestamp,
                block.blockhash(block.number - 250)
            );

        stringToSign[msg.sender] = strToSign;
        signedString[msg.sender] = "waiting to singed string";

        return stringToSign[msg.sender];
    }

    function uploadSignedString(string _signedString){

        signedString[msg.sender] = _signedString;
    }

}
