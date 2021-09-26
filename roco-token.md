# Roco Token

RocoStorageBase is an APPSTORAGE model. It is coded by deriving from the Diamond Storage method. \(Diamond Standard EIP 2535 by Nick Mudge\) Allows the use of Structs and State Variables in the RocoStorageBase library. 

This allows the use of Eternal Storage and Diamon Standard Upgradeable Contract infrastructures. EIP 170 Large contracts can be designed regardless of the 24.5KB Contract Limit Size limit. 

These Libraries are always transferable by inheritance. Access from other Agreements is very simple. Examples of AppStorage models include GHSTStaking and AaveGotchi.



```text
library RocoStorageBase {
    using SafeMath for uint256;
    
    bytes32 constant public ROCO_STORAGE = keccak256("com.roco.storage.roco");

    //- Master Vesting
    struct VestingData {
        uint index;
        address walletaddress;
        uint256 totalamount;
        uint256 starttime;
        uint totalperiod;
    }

    //- Detail Vesting
    struct VestingDataDetail {
        uint index;
        uint256 periodtime;
        uint256 periodamount;
        uint period;
        bool confirm;
        address walletaddress;
    }

    struct AppStorage {
        //- Vesting Data
        mapping (address => VestingData) VestingStruct;
        address[] VestingIndex;
        //- Vesting Data Detail
        mapping (address => VestingDataDetail[]) VestingDetailStruct;
    }

    function rocostorage() internal pure returns(AppStorage storage app) {
        bytes32 rocoposition = ROCO_STORAGE;
        assembly {
            app.slot := rocoposition
        }
    }
```

