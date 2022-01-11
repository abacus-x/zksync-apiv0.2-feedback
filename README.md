# zkSync API v0.2 feedback

This is meant to help provide feedback for the v0.2 API. I found few items that require fixes, as well as a couple items that would help users understand the API interface better. 

Reference schema.json and its commit history to see recommended changes. 

## Items
- **Transaction token/tokenId reference:** Transactions use two different keys to reference tokens - 'token' and 'tokenId'. Using tokenId as specified in API docs for Withdraw transactions throws an error. It would be helpful to normalize this to 'token' (see schema.json commit history).
- **Swap transaction:** Adding a second order to the orders array would help clarify that tx.orders requires \[Order A, Order B\]. Also, it would be helpful to note somewhere in the docs that the ethSignature requires an array of ethSignatures \[Swap, Order A, Order B\] - this format is different than all other transactions, and it is not noted in the docs. The API error response is general, so it's not easy to understand what's causing the issue.
- **ForcedExit:** I recommend adding 'feeToken' as an optional param. It appears that the fee is paid in the token being withdrawn, and there is no option to specify a feeToken. If a user tries to withdraw a token not enabled for paying fees, then there could be an issue (I was not able to test it since I do not have a token that meets this criteria). 
- **Token endpoint:** I recommend changing this endpoint to make the tokenLike param case insensitive. Currently the token endpoint is case-sensitive. For instance, https://rinkeby-api.zksync.io/api/v0.2/tokens/eth returns an error, while https://rinkeby-api.zksync.io/api/v0.2/tokens/ETH works.  
