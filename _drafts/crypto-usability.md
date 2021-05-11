
Even crypto-exchanges use email signups and passwords, because PKI doesn't work for end-users. However, that is exactly what bitcoin-influencers want to get to.

Let's take an extreme example: if my house burns down today, I lose everything valuable in the house, and some cash. The money in my bank account is not affected.

If an average person's laptop breaks down, they don't lose access to their bank account - it is tied to your password. If you forget the password, you can go to the bank, prove your identity (they actually match your face with your photo on record!), and get back your access. You might lose your photos, but you can back-those easily without much concern.

However, if you own cryptocoins, the usability story is hell. That's not a statement about crypto, but usability of encryption tools in general is horrible. Someone defined cryptography as changing your problem to a Key Management Problem. And you don't ever want end-users to manage keys on their own, because they will screw up. The best modern crypto tools are purpose built and small, and still meant to be used only by technical users because Managing Keys is Hard.

Bitcoin purists will tell you that you should create a new bitcoin address for every transaction that you do. That means one private key per transaction. Managing that many keys is a pain, so some wallets will do that for you. But then, your keys are in software, which is not a good idea for irreversible transactions.

All right, lets keep your key in hardware. Hardware keys have security guarantees that make sure that an attacker who steals the key cannot get the private key out. Using the key to approve a transaction requires a passphrase. If you provide the wrong passphrase 3 times, the key destroys itself. But what happens if the key breaks? Don't worry - you must have a backup key. What if the backup key breaks? Don't worry - you need a paper backup with your wallet seed that you can use to re-create your private key. What if I forget the passphrase - silly, that's what the paper backup is for.

At this point you have:

1. 2 hardware security keys, each costing ~\$100. You're also trusting the key manufacturers - so this needs to be vetted.
2. A paper backup, and a backup of this paper backup. You put one copy in your bank vault, and another copy in another bank vault in another city (what if there's an earthquake?)

If you lose your key, you must visit your bank, buy a new one and configure that. And you want to do this completely offline (some new models let you do this without connecting to a computer by having a keypad on it, but its not a good idea) on an airgapped computer.

Surely that seems excessive? This is exactly the kind of security that CAs have to do. The ones that cost \$4M to run every year, and get audited to ensure that they are doing this.

If you have any meaningful amount of money in crypto, this is the least you _must do_. If you have more, you must hedge your bets, and setup multiple wallets, keys with split amounts and save them as per your risk profile. Then there is always the \$5 wrench attack - do you give up your passphrase when someone threatens to beat you up?

A lot of people will point out that you shouldn't be storing these large amounts with you, you should be storing them in crypto-exchanges. At which point, you've switched your trust model from "I trust math" to "I trust this crypto-exchange's security processes". But can you really trust these exchanges? What happens when they screw up?

Unlike CAs in the WebPKI ecosystem (that issue certificates), these exchanges are not audited. All your coins go into a common pool (similar to banks), which makes auditing them harder. Auditing them also requires a confusing mix of infosec and financial acumen, something that's not easily done. And they can still make mistakes.

CoinSecure, and Indian Coin Exchange lost 435 bitcoins (valued at 19cr INR then, now likely more) because their head of security screwed up while transferring keys. You'd assume that when someone moves around hundreds of bitcoins, there would be a bit more security, but no - he was allowed to do that on his personal laptop. The CEO claimed that he stole them, and filed a police complaint. The company has since shut down, but many involved is still promoting cryptocurrencies.

If a Coin-exchange across the globe runs with your money, what recourse do you have? Users in India haven't been able to recover that money while being within jurisdiction boundaries. Trusting an unregulated unaudited entity across international borders would be stupidity. Yet millions of people are doing it for greed as the bitcoin prices keep going up. Gold rushes can result in the most amazing cognitive dissonances.

The Web PKI model allows for mistakes - we have revocations in case a certificate is wrongly issued, we have transparency systems to ensure that CAs abide by the guidelines. If a CA turns into a bad-actor, they can be revoked worldwide in a matter of hours. If a CA loses its root keys, the world keeps moving as the CA gets a new root certificate. If a CA's keys get hacked, they get screwed, but the browsers can revoke that certificate in a few hours. Some parts of the Internet break for a few days, and then we keep moving along. We have audits to ensure that these keys stay in secure-offline-vaults.

I keep my passwords encrypted with GPG, and use a hardware key every time I login to a website - I have set it up so I that I need to touch it for every single login. I am accutely aware of the usability issues going on all-in on crypto has. (One of the many reasons PGP doesn't work). And none of these are issues I'd want my mom and dad to worry about.

When the bitcoin bubble bursts, a lot of people would have made a lot of money, but many more will lose their life savings. And many more will lose billions of dollars because crypto usability isn't there yet.

Maybe once we live in a more connected world, where cybernetic implants are common, and crypto computations can be done within your brain - crypto usability might get better. But till then, remember that all code has bugs - and you don't want random software bugs to cause you to lose all your money without any recourse.

// An example of this comes from how crypto exchanges blacklist known criminal bitcoin addresses.
