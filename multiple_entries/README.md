# Multiple Entries

This contract has three different entries. 


1. It has an entry point that takes an integer and stores it. The entry point can only be called by the contract itself. If other contracts call it, it will fail.

2. It has a second entry point that calls the entrypoint in 1 with a value provided by the caller.

3. It has a third entry point that takes a timestamp. If the timestamp is less than the current time, it will fail, if it is greater it will increase a stored counter by one.


## Test Contract
 https://carthagenet.tezos.id/accounts/KT1CVVVP2FtdGDhkjMPgo2WixcbzRBSJmsBF?op=contractStorage&tab=contract


## Usage
### Notes

Because entry 1 can only be called by the contract itself, you will never be able to call it directly even with its manager. You can however call it indirectly by calling entry 2, as entry two will call the contract from the contract itself. 

### Originate
```
./tezos-client originate contract multientry transferring 0 from <manager> running multiple_contracts.mtz --burn-cap 2.314 --init "(Pair 0 0)"
```

### Call Entry 1

This will fail because you are not calling it from itself. 

```
./tezos-client -A carthagenet.tezos.cryptium.ch transfer 0 from manager to KT1CVVVP2FtdGDhkjMPgo2WixcbzRBSJmsBF --entrypoint store_int --arg 5
```

### Call Entry 2
```
./tezos-client -A carthagenet.tezos.cryptium.ch transfer 0 from manager to KT1CVVVP2FtdGDhkjMPgo2WixcbzRBSJmsBF --entrypoint call_store_int --arg
```

### Call Entry 3

```
./tezos-client -A carthagenet.tezos.cryptium.ch transfer 0 from manager to KT1CVVVP2FtdGDhkjMPgo2WixcbzRBSJmsBF --entrypoint update_counter --arg 1893456000
```