## v0.24.0 PENDING
^--- PENDING wasn't purged on sdk v0.23.0 release.

BREAKING CHANGES
* Update to tendermint v0.23.0. This involves removing crypto.Pubkey,
maintaining a validator address to pubkey map, and using time.Time instead of int64 for time. [SDK PR](https://github.com/cosmos/cosmos-sdk/pull/1927)

## PENDING

BREAKING CHANGES
* API
  - \#1880 and \#2000 [x/stake] changed the endpoints to be more REST-ful
* Update to tendermint v0.22.5. This involves changing all of the cryptography imports. [Ref](https://github.com/tendermint/tendermint/pull/1966)
* [baseapp] Msgs are no longer run on CheckTx, removed `ctx.IsCheckTx()`
* [x/gov] CLI flag changed from `proposalID` to `proposal-id`
* [x/stake] Fixed the period check for the inflation calculation
* [x/stake] Inflation doesn't use rationals in calculation (performance boost)
* [x/stake] CLI flags for identity changed from `--keybase-sig` to `--identity`, effects:
  * `gaiacli stake create-validator`
  * `gaiacli stake edit-validator`
* [baseapp] NewBaseApp constructor now takes sdk.TxDecoder as argument instead of wire.Codec
* [x/auth] Default TxDecoder can be found in `x/auth` rather than baseapp
* \#1606 The following CLI commands have been switched to use `--from`
  * `gaiacli stake create-validator --address-validator`
  * `gaiacli stake edit-validator --address-validator`
  * `gaiacli stake delegate --address-delegator`
  * `gaiacli stake unbond begin --address-delegator`
  * `gaiacli stake unbond complete --address-delegator`
  * `gaiacli stake redelegate begin --address-delegator`
  * `gaiacli stake redelegate complete --address-delegator`
  * `gaiacli stake unrevoke [validator-address]`
  * `gaiacli gov submit-proposal --proposer`
  * `gaiacli gov deposit --depositer`
  * `gaiacli gov vote --voter`
* [x/gov] Added tags sub-package, changed tags to use dash-case
* [x/gov] Governance parameters are now stored in globalparams store
* [core] \#1807 Switch from use of rational to decimal
* [lcd] \#1866 Updated lcd /slashing/signing_info endpoint to take cosmosvalpub instead of cosmosvaladdr
* [types] sdk.NewCoin now takes sdk.Int, sdk.NewInt64Coin takes int64
* [cli] #1551: Officially removed `--name` from CLI commands
* [cli] Genesis/key creation (`init`) now supports user-provided key passwords
* [cli] unsafe_reset_all, show_validator, and show_node_id have been renamed to unsafe-reset-all, show-validator, and show-node-id

FEATURES
* [lcd] Can now query governance proposals by ProposalStatus
* [x/mock/simulation] Randomized simulation framework
  * Modules specify invariants and operations, preferably in an x/[module]/simulation package
  * Modules can test random combinations of their own operations
  * Applications can integrate operations and invariants from modules together for an integrated simulation
* [baseapp] Initialize validator set on ResponseInitChain
* [cosmos-sdk-cli] Added support for cosmos-sdk-cli tool under cosmos-sdk/cmd
   * This allows SDK users to initialize a new project repository.
* [tests] Remotenet commands for AWS (awsnet)
* [networks] Added ansible scripts to upgrade seed nodes on a network
* [store] Add transient store
* [gov] Add slashing for validators who do not vote on a proposal
* [cli] added `gov query-proposals` command to CLI. Can filter by `depositer`, `voter`, and `status`
* [core] added BaseApp.Seal - ability to seal baseapp parameters once they've been set
* [scripts] added log output monitoring to DataDog using Ansible scripts
* [gov] added TallyResult type that gets added stored in Proposal after tallying is finished

IMPROVEMENTS
* [baseapp] Allow any alphanumeric character in route
* [cli] Improve error messages for all txs when the account doesn't exist
* [tools] Remove `rm -rf vendor/` from `make get_vendor_deps`
* [x/auth] Recover ErrorOutOfGas panic in order to set sdk.Result attributes correctly
* [x/stake] Add revoked to human-readable validator
* [spec] \#967 Inflation and distribution specs drastically improved
* [tests] Add tests to example apps in docs
* [x/gov] Votes on a proposal can now be queried
* [x/bank] Unit tests are now table-driven
* [tests] Fixes ansible scripts to work with AWS too
* [tests] \#1806 CLI tests are now behind the build flag 'cli_test', so go test works on a new repo
* [x/gov] Initial governance parameters can now be set in the genesis file
* [x/stake] \#1815 Sped up the processing of `EditValidator` txs.
* [server] \#1930 Transactions indexer indexes all tags by default.
* [x/stake] \#2000 Added tests for new staking endpoints
* [x/stake] [#2023](https://github.com/cosmos/cosmos-sdk/pull/2023) Terminate iteration loop in `UpdateBondedValidators` and `UpdateBondedValidatorsFull` when the first revoked validator is encountered and perform a sanity check.
* [tools] Make get_vendor_deps deletes `.vendor-new` directories, in case scratch files are present.

BUG FIXES
*  \#1988 Make us compile on OpenBSD (disable ledger) [#1988] (https://github.com/cosmos/cosmos-sdk/issues/1988)
*  \#1666 Add intra-tx counter to the genesis validators
*  \#1797 Fix off-by-one error in slashing for downtime
*  \#1787 Fixed bug where Tally fails due to revoked/unbonding validator
*  \#1766 Fixes bad example for keybase identity
*  \#1804 Fixes gen-tx genesis generation logic temporarily until upstream updates
*  \#1799 Fix `gaiad export`
*  \#1828 Force user to specify amount on create-validator command by removing default
*  \#1839 Fixed bug where intra-tx counter wasn't set correctly for genesis validators
* [staking] [#1858](https://github.com/cosmos/cosmos-sdk/pull/1858) Fixed bug where the cliff validator was not be updated correctly
* [tests] \#1675 Fix non-deterministic `test_cover`
* [client] \#1551: Refactored `CoreContext`
  * Renamed `CoreContext` to `QueryContext`
  * Removed all tx related fields and logic (building & signing) to separate
  structure `TxContext` in `x/auth/client/context`
  * Cleaned up documentation and API of what used to be `CoreContext`
  * Implemented `KeyType` enum for key info
*  \#1666 Add intra-tx counter to the genesis validators
* [tests] \#1551: Fixed invalid LCD test JSON payload in `doIBCTransfer`
*  \#1787 Fixed bug where Tally fails due to revoked/unbonding validator
*  \#1787 Fixed bug where Tally fails due to revoked/unbonding validator
* [basecoin] Fixes coin transaction failure and account query [discussion](https://forum.cosmos.network/t/unmarshalbinarybare-expected-to-read-prefix-bytes-75fbfab8-since-it-is-registered-concrete-but-got-0a141dfa/664/6)
* [cli] \#1997 Handle panics gracefully when `gaiacli stake {delegation,unbond}` fail to unmarshal delegation.
