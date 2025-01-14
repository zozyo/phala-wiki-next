---
title: 'Use wPHA or delegation NFT for governance voting'
weight: 5012
draft: false
menu:
  general:
    parent: "general-delegation"
---


After the implementation of the StakePoolv2 feature, there has been a change in how delegations are stored in users' accounts. Previously, delegations were locked tokens, but now they are converted into wPHA and transferred to the StakePool in exchange for Delegation NFTs. As a consequence of this change, users are no longer able to use their delegations for direct voting on platforms such as subsquare.

In this page, we will guide you through the process of using Delegation NFT and wPHA in your account to participate in voting on Polkadot.js.

## Why can Delegation NFT and wPHA be used for voting?

In reality, The item used for voting is not Delegation NFTs or wPHAs, but locked PHAs. 
When users use WrappedBalances to exchange between PHA and wPHA tokens, WrappedBalances serves as an on-chain ledger that records ownership information for all wPHA tokens on the chain. All locked PHA is counted in WrappedBalances, and the corresponding voting right is assigned to the respective owner.

In other words, WrappedBalances will provide a combined value of your Delegation NFT and wPHA holdings, and allowing you to utilize this value to participate in voting for PHA.

## How to vote through Polkadot.js

### track my voting right

By utilizing on-chain queries, you can get the total value of your Delegation NFT and wPHA holdings. Within [the Phala App](https://app.phala.network/delegate/my-delegation), this information can be found easily.

![](https://i.imgur.com/HMHwrrv.png)
*The total value of your Delegation NFT and wPHA is indicated in the top left corner of the image as Delegation. In this photo, I can use 234793 tokens to participate in voting.*

### token-to-vote ratio

Your vote casted through WrappedBalances equals to 0.1x voting balance. It has no lockup period.

Voting 200,000 PHA here is equivalent to 20,000 votes.

### How to vote

* Use Polkadot.js, go to the [Extrinsics page](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fkhala-api.phala.network%2Fws#/extrinsics)
* Find `PhalaWrappedBalances`. Select `vote`. This is the entrance for voting.
![](https://i.imgur.com/Ssl3fdW.png)
* Please enter the number of votes you agree/disagree in the `aye` or `nay` column. Note that since we're using the u128 format here, you need to add 12 zeros at the end of the input value. So you'll need to input `5000000000000` to represent `5` votes.
* Enter the Referendum id in the `voteId: u32 (ReferendumIndex)` column, and you can find it on the [democracy page](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fkhala-api.phala.network%2Fws#/democracy)
* Click `Submit Transaction` and sign the signature. Then the voting will be finished.

### How can I cancel my previous vote history and initiate a new vote?

You just need to initiate a new voting transaction, and the previous voting transaction will be directly replaced by the new one.

### The voting is over. How can I unlock my voting rights?

* Firstly, with the [same page](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fkhala-api.phala.network%2Fws#/extrinsics), select `democracy.removeVote(index)`, enter the ended Referendum ID, remove your vote.
![](https://i.imgur.com/zKV1Emp.png)
* Secondly, go back to WrappedBalances and select `WrappedBalances.unlock(voteId, maxIterations)`. Enter the Referendum ID and the number of voting tokens you want to unlock, submit the transaction to unlock your them.
![](https://i.imgur.com/ttv0L5D.png)

Now your tokens have been unlocked.

* If you don't remember which Referendum you voted. Go to the [Chain state page](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fkhala-api.phala.network%2Fws#/chainstate), choose `phalaWrappedBalances.accountVoteMap(AccountId32, u32): Option<Null>`. Use the specific address to check its voted Referendum.
![](https://i.imgur.com/dWpQLB9.png)
* If you don't know how much tokens are used to vote in a Referendum. Go to the [Chain state page](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fkhala-api.phala.network%2Fws#/chainstate), choose `phalaWrappedBalances.voteAccountMap(u32, AccountId32): Option<(u128,u128)>`. Enter the Referendum id and use the specific address to check its locked tokens.
![](https://i.imgur.com/RzAy4lY.png)


**In summary, the voting process using WrappedBalance becomes to be challenging due to the need to transfer tokens during staking, which is not a seamless operation. However, we are actively working on improving this process to make it more user-friendly. Our goal is to create a separate voting page that enables users to vote and unlock with just one click, thus streamlining the process and making it more accessible for all.**



