title: 'MTGox Panics, Bitcoin Plunges to 102, This is a fearmongering headline'
url: 159.html
id: 159
categories:
  - Cryptocurrency
date: 2014-02-10 20:45:42
tags:
---
[https://www.mtgox.com/press_release_20140210.html](https://www.mtgox.com/press_release_20140210.html) [https://en.bitcoin.it/wiki/Transaction_Malleability](https://en.bitcoin.it/wiki/Transaction_Malleability)

> This page was last modified on 21 January 2013, at 02:49.

From the #bitcoin channel on Freenode, at UTC +8 time:

> [19:15:21] <@gmaxwell> Plarkplark: the issue is https://en.bitcoin.it/wiki/Transaction_Malleability (known since at least 2011)

Funny how they didn't panic earlier, when Bitcoin was on cloud 9. [![](/wp-content/uploads/2014/02/btce-102-e1392034388900-150x150.jpg)](/wp-content/uploads/2014/02/btce-102-e1392034388900-1024x721.jpg) Meanwhile in China, where the end of Chinese New Year is theorized to be contributing to the chaos: [![](/wp-content/uploads/2014/02/okcoin_ticker-e1392038698106-150x150.jpg)](/wp-content/uploads/2014/02/okcoin_ticker-e1392038698106.jpg) The rollercoaster isn't nearly as severe.   And meanwhile in the #unobtanium altcoin channel...

> [19:06:55] <redactedname1> well these unos are worth jack shit now
[19:07:17] <redactedname1> fucking mt gox
[19:07:18] <redactedname2> btc will be back to 900 before you know it
[19:07:26] <redactedname1> releasing the news like that
[19:07:49] <redactedname3> did i miss something on uno?
[19:07:51] <redactedname1> they probably had agents in place to get that 102 buy
[19:08:08] <redactedname4> ahahahahahahah
[19:08:09] <redactedname4> fuck
[19:08:16] <redactedname4> 546 USD
[19:08:16] <redactedname2> how much btc was the 102 sell?
[19:08:20] <redactedname4> wtf is going on
[19:08:30] <redactedname1> end of chinese new year
[19:08:34] <redactedname1> they want out
[19:08:47] <redactedname5> yeah. crypto is pretty fucked right about now. :(
[19:08:57] <redactedname6> 4k i think jawa
[19:09:13] <redactedname2> 4k btc or 4k usd of btc?
[19:09:18] <redactedname4> is this all bc of gox?
[19:09:23] <redactedname6> 4k usd i think
[19:09:34] <redactedname4> nm, just read up

EDIT: Since MTGox is in damage control mode; here's what it had to say:

> Dear MtGox Customers and Bitcoiners,
As you are aware, the MtGox team has been working hard to address an issue with the way that bitcoin withdrawals are processed. By "bitcoin withdrawal" we are referring to transactions from a MtGox bitcoin wallet to an external bitcoin address. Bitcoin transactions to any MtGox bitcoin address, and currency withdrawals (Yen, Euro, etc) are not affected by this issue.

>The problem we have identified is not limited to MtGox, and affects all transactions where Bitcoins are being sent to a third party. We believe that the changes required for addressing this issue will be positive over the long term for the whole community. As a result we took the necessary action of suspending bitcoin withdrawals until this technical issue has been resolved.

>Addressing Transaction Malleability
MtGox has detected unusual activity on its Bitcoin wallets and performed investigations during the past weeks. This confirmed the presence of transactions which need to be examined more closely.

>Non-technical Explanation:
A bug in the bitcoin software makes it possible for someone to use the Bitcoin network to alter transaction details to make it seem like a sending of bitcoins to a bitcoin wallet did not occur when in fact it did occur. Since the transaction appears as if it has not proceeded correctly, the bitcoins may be resent. MtGox is working with the Bitcoin core development team and others to mitigate this issue.

>Technical Explanation:
Bitcoin transactions are subject to a design issue that has been largely ignored, while known to at least a part of the Bitcoin core developers and mentioned on the BitcoinTalk forums. This defect, known as "transaction malleability" makes it possible for a third party to alter the hash of any freshly issued transaction without invalidating the signature, hence resulting in a similar transaction under a different hash. Of course only one of the two transactions can be validated. However, if the party who altered the transaction is fast enough, for example with a direct connection to different mining pools, or has even a small amount of mining power, it can easily cause the transaction hash alteration to be committed to the blockchain.

>The bitcoin api "sendtoaddress" broadly used to send bitcoins to a given bitcoin address will return a transaction hash as a way to track the transaction's insertion in the blockchain.

>Most wallet and exchange services will keep a record of this said hash in order to be able to respond to users should they inquire about their transaction. It is likely that these services will assume the transaction was not sent if it doesn't appear in the blockchain with the original hash and have currently no means to recognize the alternative transactions as theirs in an efficient way.

>This means that an individual could request bitcoins from an exchange or wallet service, alter the resulting transaction's hash before inclusion in the blockchain, then contact the issuing service while claiming the transaction did not proceed. If the alteration fails, the user can simply send the bitcoins back and try again until successful.

>We believe this can be addressed by using a different hash for transaction tracking purposes. While the network will continue to use the current hash for the purpose of inclusion in each block's Merkle Tree, the new hash's purpose will be to track a given transaction and can be computed and indexed by hashing the exact signed string via SHA256 (in the same way transactions are currently hashed).
This new transaction hash will allow signing parties to keep track of any transaction they have signed and can easily be computed, even for past transactions.

>We have discussed this solution with the Bitcoin core developers and will allow Bitcoin withdrawals again once it has been approved and standardized.

> In the meantime, exchanges and wallet services - and any service sending coins directly to third parties - should be extremely careful with anyone claiming their transaction did not go through.
Note that this will also affect any other crypto-currency using the same transaction scheme as Bitcoin.

> Conclusion
To put things in perspective, it's important to remember that Bitcoin is a very new technology and still very much in its early stages. What MtGox and the Bitcoin community have experienced in the past year has been an incredible and exciting challenge, and there is still much to do to further improve.
MtGox will resume bitcoin withdrawals to outside wallets once the issue outlined above has been properly addressed in a manner that will best serve our customers.
More information on the status of this issue will be released as soon as possible.
We thank you for taking the time to read this, and especially for your patience.
Best Regards,
MtGox Team