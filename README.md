# Semaphore
Crowdfunding with bitcoin

# What is this?
A crowdfunding app that uses bitcoin's smart contracting functionality to let contributors recover their funds if the fundraiser does not reach its goal

# How can I try it?
Just click here: https://semaphore.finance/

# Or view an existing fundraiser
Just click here: https://semaphore.finance/?fundraiser=sprj13n5y0vnu9ajuaund2nxzphy357m82gk7vumup4mys67ketxlsch8wumn8ghj7mn0wd68yat99e3k7mggacq09

# Video explainer
[![](https://i.ibb.co/v1Srq3g/semaphore-yt-thumbnail-with-yt-logo.jpg)](https://www.youtube.com/watch?v=VHGRQVuVtCY)

# How does it work?
Semaphore gives contributors two ways to give someone money: irreversible and reversible. If you choose irreversible, it sends the money straight to the recipient's bitcoin address and there are no "takebacks" after the money confirms. If you choose reversible, it sends the money to a bitcoin smart contract with two spending paths: one lets the contributor take their money back at any time, the other is a "multisig" path that can only spend the money if the contributor and the recipient both cosign a transaction.

After sending money to this smart contract, the contributor creates a bitcoin transaction that sends the money to the recipient but *only* if the fundraiser reaches the goal amount. The contributor signs this transaction and publishes their signature, and thus the recipient can only take the money if he gets *enough* signatures on valid contributions that he reaches his goal. If he tries to spend the money in any transaction that *doesn't* reach the goal, the signatures simply won't be valid, and bitcoin won't let him take the money.

# But I thought bitcoin didn't have smart contracts!
It does. In fact, it's had them since day 1. Satoshi put a crowdfunding feature called "anyone_can_pay" directly into the original bitcoin code and several pieces of software over the years used it, including the now-abandoned [Lighthouse project by Mike Hearn](https://github.com/vinumeris/lighthouse). Semaphore is basically just a recreation of that project but now using modern bitcoin tools like taproot.

# What are automatic refunds?
Well, they're only semi-automatic. When a contributor makes their pledge I also have them create a "recovery" signature that sends their money back to themselves. But this signature is "timelocked" -- another bitcoin smart contracting tool -- so that a transaction that uses this signature is only valid if it is broadcasted *after* the fundraiser is over. The contributor uploads this signature *along with* the signature that lets the *intended* recipient take the money if the goal is reached. If the fundraiser ends and the recipient hasn't taken the money, that signals that the goal was *not* reached, so a script will automatically recreate the "recovery transaction" and slap on the contributor's recovery signature to make the transaction valid, then "automatically" broadcast it. But I put "automatically" in quotes because it's not *fully* automatic. Someone has to visit the webpage 24 hours after the fundraiser ends in order to trigger the "automatic" recovery transaction that gives all the contributors their money back. Alternatively, any of the contributors can visit the page themselves and take their money back manually.

# Why did you make this?
Alternative fundraising platforms like geyser.fund don't let contributors take their money back. Contributors send their money directly to the recipient and that's that. I wanted modern "refund" features like platforms like gofundme have, so that's what I made. And all my software is free and open source so companies like geyser are free to use it if they like it.

# What if people contribute to my fundraiser but not enough for me to reach my goal?
If you have enough to make up the difference just contribute your own funds to the fundraiser so that you *do* have enough. That's perfectly acceptable in my opinion and I hope it is clear to contributors that the recipient can contribute too.
