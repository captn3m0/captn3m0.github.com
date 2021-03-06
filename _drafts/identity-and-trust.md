## title: On Identity, Trust, and Cryptocurrencies

---

A short tl;dr for self:

1. Qauntifying "trust" - offline/online
2. The Identity/Trust relationship
3. How software eating the world changes this relationship economically
4. Thoughts on cryptocurrencies from the identity/trust/usability lens. (Moved to separate post now)

---

The dictionary defines "trust" as "firm belief in the reliability, truth, or ability of someone or something." In real-world that boils down to holding belief statements about the world, usually bayesian (ie to say you trust that the statement holds true some/most of the time). A more common usage is to say "you trust X", where you implicitly hold a belief statement that you trust X is acting in good faith.

As an example, let us take this statement: "I trust that I will not get scammed if I deposit money in the new SBI (State Bank of India, the largest bank in India) branch that opened last week". If you really think about it, its a statement about your trust relationship with a faceless entity - the bank in this case. Thinking from first princinples, there's a lot implied however:

1. To what degree do you trust the bank? Do you trust the security guard to save you in case there is a armed robbery? Do you trust the bank to grow your investments? Do you trust the bank to keep your deposits safe?
2. The bank branch belongs to the bank.

The second sounds like a stupid thing to list down, but that is exactly what happened in the town of "X", where a person managed to open a SBI branch without being an employee of SBI. It only came to notice when an actual SBI employee visited the town and realized he hadn't heard of a new branch being opened in their hometown.

Having trust in India's largest bank is reasonable. We're told by the RBI that our deposits are insured, banks are regularly audited, and that the RBI will step in, if there are any concerns (As they've done in the past). It is what we call a "security guarantee" in the infosec industry. The banking system has enough checks and balances that you can vouch for the safety of your deposits (atleast upto the deposit insurance limit). Trust, in infosec terms is the belief in security guarantees, such as these.

But depositing money in the SBI bank branch in (city) wouldn't have come with those guarantees, so clearly we've missed something - its a question of Identity and how trust relates to it.

---

When you go visit a Bank ATM - you're giving away your card details to the ATM machine. You're implicitly trusting the ATM machine to:

1. Be run by a trustworthy bank.
2. Not be tampered with, such as having a skimmer installed that steals your card details and PIN.
3. Have adequate security to prevent a currency snatching.
4. Give you your money.

How do you decide to trust an ATM though? An ATM costs roughly 15-20Lac INR new, so it would be cost-prohibhitive to setup a new one to steal some cards. You're trusting the security guard next to the ATM. You're basing this on the (likely) past visits to the ATM where nothing bad happened, and the proximity to the bank branch itself. Maybe you've looked it up on the bank website's ATM locator feature to confirm that this is a real ATM of your bank.

Let's focus on the last one, and realize what that means - we have a way to "bootstrap trust", so to speak. Trust relationships (especially those in the real-world) grow/infect (need a better word here) all the time, an idea that gave birth to the "Web of Trust" (Add note about WoT and what it is).

But clearly, this trust still has boundaries.

---

Let's focus on a specific kind of trust relationship - "The Identity Trust", where you vouch for someone's identity and leave the rest. ~~Why Identity, and why not others? Identity Trust lets you "bootstrap" and borrow trust much easier than anything else. For eg, if you can prove that you are really a Delivery Executive from Dominos, I trust the pizza to be safe to eat automatically.~~

Say, you visit a Car Dealership. You can vouch for its identity, by various means:

1. Checking the manufacturer's website for a list of dealerships.
2. Calling the official helpline to validate the same.
3. Checking with your friend who bought a car from there.
4. Googling for "car dealership" and seeing this address turn up.
5. Going to the website that the dealership brochure gave you.

Each of these gives a different trust rating of sorts. In the real-world - trust acts similar to Social Capital: It slowly builds up over time. Everyday interactions can increase this trust:

1. If I call the dealership, and they sound professional on the phone.
2. The dealership website looks professionally made.
3. The dealership store is a large building with lots of cars on display.
4. Maybe a friend referred this place to me.

All of these small things add up, and I can decide to buy a car because the dealership has "gained my trust". I trust them that they are acting in "good faith", which is basically shorthand for saying they are not out there to scam me. Sure they'll try to rip me off on spurious charges, but I'll get a car.

Having an "Identity" relationship lets you bootstrap this trust much more easily. Large companies have spent years building that trust. If I trust that the bank branch is an SBI Branch, it automaticaly confers the same trust relationships I have with SBI the bank (TODO: reword). That trust than passes on to the employees, who I can feel comfortable sharing my financials with, or handing them large amounts of cash.

So far, important takeaways:

1. Trust is earned slowly, but can be bootstrapped by your identity. This requires a way to trust the identity itself.
2. Trust has boundaries on both ends. The amount of trust you need to earn is proportional to what I trust you for.

The second has interesting parallels in cryptography, because the math forces you to quantify these boundaries. Say you build a new encryption scheme - other cryptographers can vet it, vouch for it, but their boundaries come in the form of "economical costs to break the scheme". We call a scheme unbreakable when the economical costs are astronomically high (literally astronomical - you'll need entirety of suns' energy output for billions of years to break some of these schemes). The two common measures are economical and energy-based. (insert energy and economic costs of bitcoin).

In some ways, energy is true currency of the world (something Eragon readers should relate to) - the cost of getting something done relates to how much effort goes into it, and that effort is best approximated by the energy that goes into it. It is also the one thing we cannot produce from thin-air (unlike money). This is also something that the crypto-world likes to iterate because it ties down the world currency to energy costs and usage. (Also why so many blockchain projects are around energy distribution).

Let's get back to Trust and Identity. A lot of trust relationships seem to be bootstrapped these days from the "official website" of some entity. If you see the branch address at onlinesbi.com, you have bootstrapped that trust from the website. This is where the worlds usually collde - trusting domain names and websites. There's a lot of interesting observations that we've learned over the last 3 decades of internet's existence:

1. Scammers will go to any lengths to impersonate a website. This is something browsers had to actively fight.
2. The "Padlock=Secure" guarantee only worked as long as it was costly to acquire TLS certificates. Having that cost brought to zero has resulted in every phishing website now having a green padlock.

Sometimes, there's vendors making that trust implicit. For eg, searching for SBI on the app store gets you hundreds of apps, including one that uses the SBI logo and name without being affiliated with the bank. The user trusts Apple to have vetted these apps, and ensured that a fake SBI app would not be allowed in. This is clearly misplaced, but is good enough for most uses.

Let's move to the next part: lets talk about software.

"Software eats the world" remains true because the costs of doing anything in software are so massively low. If it can be done in software, it will be done remains a fairly true maxim.

However, the costs keep falling further and further. Building a million dollar software business is a reality today for 1-person startups, because software scales like nothing else can. However, this also makes trusting identities much harder, because the cost of setting up a thousand fake websites is minisucule these days.

As an example, look at this case from the XXX High Court, where the court has ordered registrars to prevent registrations of any domain names that include the world "Amul". The court pushed this order, because enough scammers create websites that impersonate Amul and run job-for-money scams using that to bootstrap trust.

It works, because nobody knows what Amul's real website is. It is not something I see mentioned anywhere offline. Amul has daily ads in most Indian newspapers, and the easiest way for them to fix this is to use the official website everywhere across their ads and products, but they took the wrong route imo.

The scammers link the victims to the fake website which has the scammer details - they bootstrap that trust by pretending to be Amul and making off with money.

Say you want to prevent these kind of frauds - how do you even solve for this? Educating the users is one part, but how do you bootstrap this trust in an increasingly digital world where you might never see a physical store for a company you deal with daily.

The cost of software will keep going down, so building new websites would only become easier with time. You could make it harder to register domains, but its a global system, and the scammers just register the domain from a different registrar (the real reason why the Amul judgement is toothless).

The older markers for trust in online properties (padlock, well designed website) are no longer economical hurdles - you can build a professional looking website for pennies in 2020. Entire companies are running from just an Instagram account, which doesn't even require a website.

One solution to the problem was "EV certificates", which was the idea to issue TLS certificates to businesses that would showcase the business name prominently and make it easier to bootstrap that trust. However, the internet is global and the economical hurdles of registering a business are different across all countries, and as such - there is no minimum baseline security guarantee that they end up offering. You could register a business called Stripe in Ireland and get an EV certificate for it, letting you leech off the trust people have in Stripe. There's also the issue that the business names rarely match up with the known names of businesses. If OLA were to use an EV certificate, it say "ANI Technologies Pvt. Ltd". If EV certs are not the answer, what is?

The crypto-nerds will tell you that the answer is math. Having faith in strong cryptographic identities is a nice idea - if you could trust McDonald once cryptographically, and McD could use that trust relationship to bootstrap using that trust. Say you enter a McD restaurant in a new town, and you could scan a QR code to validate that this is from the same McD corporation that you usually eat at.

But the moment you go all-in on crypto, there are a ton of other problems that start to surface:

Remember trust boundaries? You don't trust the McD key to invest your money, you trust it to deliver you safe and hygenic food. How do you differentiate between them? OpenPGP has this 1-5 rating system for trust, which is frankly absurd. At the other end you have people trying to code this into smart contracts. Surely, if we can encode the trust relationship itself into software, it works out right?

But how do you encode my trust in McD about it delivering me safe food? Oh, you need to validate their supply chain throughout and the delivery process must also involve cryptographic signatures (see how blockchain startup ideas have a starting point?). This results in a stupid explosion of ideas around:

1. Lets put everything in the blockchain, because that lets us provide useful cryptographic guarantees.
2. Lets put smart contracts everywhere, because we can't encode what those guarantees mean otherwise.

Because you want to encode that trust relationship, and the fact that trust is almsot always very nuanced - mixing these 2 things requires you to go all-in. The hard math approach says: we want to provide security guarantees. The soft requirement is that these guarantees are always nuanced and not binary. Mixing them together is ungodly and results in startups that claim to:

1. (insert stupid blockchain startups list)

The counter-point here is that not every crypto startup is trying to change the world. They're starting from the simpler problems, the ones where the relationships are less nuanced, the trust is binary, and math is easy. That's the world of Finance.

Hence, cryptocurrencies.

Before we get into cryptocurrencies, let's take a detour into usability first.

The world's largest (and most successful) deployment of cryptography (to this date) remains the Web PKI. It is a massively large effort that has resulted in two important accomplishments:

1. Providing cryptographic guarantees to Internet security. Your data is encrypted and can only be read by the two parties (your browser and the server), despite it travelling across 3-different continents and 2-oceans on cables owned by thousands of different companies.
2. Providing trust guarantees on the Internet. Seeing a green padlock next to "google.com" provides users the guarantee that this is the real website behind Google.com.

Those are the two things that the end-user sees. But behind the scenes, running the Web PKI infrastructure requires:

1. Regular audits of the CAs who are issuing these certificates and vouching for the owners of these domains.
2. A lot of complimentary infrastructure that tracks these CAs publicly (Certificate Transparency).
3. Certificate revocation. If Google gets hacked, and someone else steals their keys, they can stop the hackers from using that to impersonate Google.
4. Infrastructure that the browsers maintain to keep track of revoked certificates, or CAs that don't seem trustworthy. The Government of India CA for eg, issued a few certs for google.com without approval, and was limited to issuing certs for `gov.in/nic.in` domains as a consequence. Browsers take these strict actions to make sure that the trust in Web PKI is backed up their actions. Issuing a trusted certificate for google.com and getting it from being revoked would require a nation-state level effort today.
5. Innovation in browser UX. As attacks have become more sophisticated, browsers have had to take harder measures to prevent various impersonation attacks.
6. A system to track these CAs, their certificates and delivering it securely to your device.

It is a lot of people keeping each other accountable in a system that has held up over time. There's also some parts that don't get used much these days, and some parts that aren't allowed to be used:

1. Browsers deprecated MD5 certificates for eg.
2. EV certificates no longer show a green bar or the business name on modern browsers today. We learned that the security guarantees that tried to provide were not really backed strongly enough and caused more usability issues than the benefits.
3. Client certificates are an authentication mechanism that relies on PKI to authenticate the user to the website, but nobody really uses it.

A large part of the success of PKI comes from its usability in modern browsers for end-users. If logging in to Google required generating and using a private key, GMail wouldn't have worked. Every business went with usernames and passwords because that was a much more usable solution.
