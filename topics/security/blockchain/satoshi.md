# Satoshi Nakamoto beginnings

<br>![miscellaneous image](https://raw.githubusercontent.com/AnselmoGPP/Learn_Computer_Science/master/resources/miscellany.jpg)


## Table of Contents

+ [**References**](#references)
+ [**Introduction**](#introduction)
+ [**First emails**](#first-emails)
+ [**Cryptography mailing list**](#cryptography-mailing-list)
+ [**P2P foundation**](#p2p-foundation)
+ [**SourceForge**](#sourceforge)
+ [**BitcoinTalk**](#bitcointalk.org)
+ [**Others**](#others)


## References

- [**Adam Back/Satoshi Nakamoto emails**](https://bitcoinmagazine.com/technical/bitcoin-adam-backs-complete-emails-satoshi-nakamoto)
- [**Wei Dai/Satoshi Nakamoto emails**](https://gwern.net/doc/bitcoin/2008-nakamoto#emails)
- [**metzdowd archive**](https://www.metzdowd.com/pipermail/cryptography/2008-October/date.html)
- [**P2P foundation**](http://p2pfoundation.ning.com/profile/SatoshiNakamoto)
- [**SourceForge**](https://sourceforge.net/projects/bitcoin/)
- [**bitcointalk.org**](https://bitcointalk.org/index.php?action=profile;u=3)
- [**Who is Satoshi Nakamoto?**](https://whoissatoshi.wordpress.com/2016/01/27/the-usual-suspects/)


## Introduction

**Satoshi Nakamoto** is the creator of **Bitcoin**. His first known communications happened via email with Adam Back and Wei Dai. Then, he appeared at the **Cryptography mailing list** (at metzdowd.com), where he published the Bitcoin whitepaper, participated in discussions about it, and announced the release of Bitcoin 0.1 software. He also announced Bitcoin 0.1 later at **P2P foundation** and discussed it a little. All these communications (emails and posts) have been compiled into this document.

He continued working on the Bitcoin software, together with some collaborators that decided to join him. He moved the source code to **sourceforge.net**, where he participated in an email list and [forum](http://bitcoin.sourceforge.net/boards/index.php). Then, he moved to **BitcoinTalk.org** forum. The publications Satoshi made in these two places are not included here since they are mostly technical discussions about issues that arised during Bitcoin software development. Finally, he decided to disappear forever and left Bitcoin development to his collaborators and community.

He appeared in different platforms:

- [**metzdowd cryptography mailing list**](https://www.metzdowd.com/pipermail/cryptography/2008-October/date.html): Whitepaper publishing, software release announcement, and discussions.
- [**P2P foundation**](http://p2pfoundation.ning.com/profile/SatoshiNakamoto): Software release announcement.
- [**SourceForge**](https://sourceforge.net/projects/bitcoin/): Code repository, mailing list, and forum.
- [**bitcointalk.org forum**](https://bitcointalk.org/index.php?action=profile;u=3): Forum.

He used different emails:

- satoshi@anonymousspeech.com: Used for communicating with Adam Back and Wei Dai.
- satoshi@vistomail.com: Used in the Cryptography mailing list.
- satoshin@gmx.com: First mentioned in the paper (31/10/2008).

Chronology:

- Second quarter of 2007: Nakamoto starts coding Bitcoin (according to himself). 
- 18/08/2008: The domain name [bitcoin.org](https://bitcoin.org) is registered and a web site is created at that address.
- 20/08/2008: satoshi@anonymousspeech.com email to **Adam Back**.
- 05/10/2008: "Nakamoto2" username registered at Sourceforge.
- 31/10/2008: Nakamoto publishes Bitcoin whitepaper at **metzdowd.com cryptography mailing list**. He participates from 31/10/2008 to 25/01/2009.
- 10/12/2008: "S_Nakamoto" username registered at Sourceforge. The Sourceforge email list goes from 10/12/2008 to 13/12/2010.
- 03/01/2009: Nakamoto mines the Genesis block.
- 09/01/2009: Nakamoto releases Bitcoin 0.1 software on SourceForge.
- 11/02/2009 - 18/02/2009: **P2P foundation** publications.
- 19-11-2009: Nakamoto is registered at [bitcointalk.org](https://bitcointalk.org/index.php?action=profile;u=3) forum as user number 3.
- Until mid-2010: Nakamoto collaborated with other developers on Bitcoin's software. He made all modifications to source code himself.
- Satoshi gives control of source code repository and network alert key to **Gavin Andresen**, and transfers related domains to prominent members from Bitcoin community. 
- 12/12/2010: Final public message (at [bitcointalk.org](https://bitcointalk.org/index.php?action=profile;u=3)).
- Nakamoto continued to correspond privately with Bitcoin’s early developers.
- 23/04/2011: Final private message (via gmx mail to Mike Hearn).
- 13/09/2011: Gavin moves source code to [GitHub](https://github.com/bitcoin/bitcoin/).

At the **Cryptography mailing list** he started 2 discussions and only participated on them:

- *Bitcoin P2P e-cash paper*
- *Bitcoin v0.1 released*

Here, he was invited to publish the whitepaper at the **P2P hackers mailing list**.

At the **P2P foundation forum** he started one discussion and only participated on it:

- *Bitcoin open source implementation of P2P currency*

At SourceForge he stored Bitcoin source code, and participated on a mailing list and forum. At **bitcointalk.org** he participated in discussions. In both sites his messages were related to technical issues involving Bitcoin development.

Here, I compiled the emails and posts made by Satoshi and other related participants around the beginning of Bitcoin. This includes:

- First emails (correspondence with Adam Back and Wei Dai)
- Cryptography mailing list emails
- P2P foundation posts
- Some other relevant writings

This doesn't include all the SourceForge and BitcoinTalk publications, which are mostly technical discussion about Bitcoin software development.


## First emails


### Satoshi reaches out to Adam Back

From: "satoshi@anonymousspeech.com" <satoshi@anonymousspeech.com>  
Sent: Wed 20/08/2008 6:30:39 PM (UTC+01:00)  
To: adam@cypherspace.org  
Subject: Citation of your Hashcash paper  

I'm getting ready to release a paper that references your Hashcash paper and I wanted to make sure I have the citation right. Here's what I have:

[5] A. Back, "Hashcash - a denial of service counter-measure"  
http://www.hashcash.org/papers/hashcash.pdf, 2002.

I think you would find it interesting, since it finds a new use for hash-based proof-of-work as a way to make e-cash work. You can download a pre-released draft at [http://www.upload.ae/file/6157/ecash-pdf.html](http://www.upload.ae/file/6157/ecash-pdf.html). Feel free to forward it to anyone else you think would be interested. I'm also nearly finished with a C++ implementation to release as open source.

Title: Electronic Cash Without a Trusted Third Party

Abstract: A purely peer-to-peer version of electronic cash would allow online payments to be sent directly from one party to another without the burdens of going through a financial institution. Digital signatures offer part of the solution, but the main benefits are lost if a trusted party is still required to prevent double-spending. We propose a solution to the double-spending problem using a peer-to-peer network. The network timestamps transactions by hashing them into an ongoing chain of hash-based proof-of-work, forming a record that cannot be changed without redoing the proof-of-work. The longest chain not only serves as proof of the sequence of events witnessed, but proof that it came from the largest pool of CPU power. As long as honest nodes control the most CPU power on the network, they can generate the longest chain and outpace any attackers. The network itself requires minimal structure. Messages are broadcasted on a best effort basis, and nodes can leave and rejoin the network at will, accepting the longest proof-of-work chain as proof of what happened while they were gone.

satoshi@anonymousspeech.com


### Adam points to Wei Dai's work

From: "Adam Back" <adam@cypherspace.org>  
Sent: Thur 21/08/2008 1:55:59 PM (UTC+01:00)  
To: satoshi@anonymousspeech.com  
Subject: Re: Citation of your Hashcash paper  

Yes citation looks fine, I'll take a look at your paper. You maybe aware of the "B-money" proposal, I guess google can find it for you, by Wei Dai which sounds to be somewhat related to your paper. (The b-money idea is just described concisely on his web page, he didn't write up a paper).

Adam


### Satoshi notes his unique contributions to Bitcoin

From: "satoshi@anonymousspeech.com" <satoshi@anonymousspeech.com>  
Sent: Thur 21/08/2008 6:59:49 PM (UTC+01:00)  
To: adam@cypherspace.org  
Subject: Re: Citation of your Hashcash paper  

Thanks, I wasn't aware of the b-money page, but my ideas start from exactly that point. I'll e-mail him to confirm the year of publication so I can credit him.

The main thing my system adds is to also use proof-of-work to support a distributed timestamp server. While users are generating proof-of-work to make new coins for themselves, the same proof-of-work is also supporting the network timestamping. This is instead of Usenet.

Satoshi


### Adam still hasn't read the white paper

From: "Adam Back" <adam@cypherspace.org>  
Sent: Thur 21/08/2008 7:17:17 PM (UTC+01:00)  
To: satoshi@anonymousspeech.com  
Subject: Re: Citation of your Hashcash paper  

Sorry still not read your paper yet, but another related paper is by Rivest et al called micromint, which uses k-way collisions to create an over-time computational advantage for the bank in creating coins. What you said about one group of players having an advantage (by compute cycles) reminded me of micromint. In micromint the bank gets an increasing advantage over time as there is some cumulative build up of advantage in terms of the partial results accumulated helping create further the partial-collisions more cheaply.

Adam


### Satoshi reaches out to Wei Dai

From: satoshi@anonymousspeech.com>  
Sent: Friday, August 22, 2008 4:38 PM  
To: "Wei Dai" <weidai@ibiblio.org>  
Cc: "Satoshi Nakamoto" <satoshi@anonymousspeech.com>  
Subject: Citation of your b-money page  

I was very interested to read your b-money page. I'm getting ready to release a paper that expands on your ideas into a complete working system. Adam Back (hashcash.org) noticed the similarities and pointed me to your site.

I need to find out the year of publication of your b-money page for the citation in my paper. It'll look like:

[1] W. Dai, "b-money," http://www.weidai.com/bmoney.txt, (2006?).

You can download a pre-release draft at

[http://www.upload.ae/file/6157/ecash-pdf.html](http://www.upload.ae/file/6157/ecash-pdf.html)  Feel free to forward it to anyone else you think would be interested.

Title: Electronic Cash Without a Trusted Third Party

Abstract: A purely peer-to-peer version of electronic cash would allow online payments to be sent directly from one party to another without the burdens of going through a financial institution.  Digital signatures offer part of the solution, but the main benefits are lost if a trusted party is still required to prevent double-spending.  We propose a solution to the double-spending problem using a peer-to-peer network.  The network timestamps transactions by hashing them into an ongoing chain of hash-based proof-of-work, forming a record that cannot be changed without redoing the proof-of-work.  The longest chain not only serves as proof of the sequence of events witnessed, but proof that it came from the largest pool of CPU power.  As long as honest nodes control the most CPU power on the network, they can generate the longest chain and outpace any attackers.  The network itself requires minimal structure.  Messages are broadcasted on a best effort basis, and nodes can leave and rejoin the network at will, accepting the longest proof-of-work chain as proof of what happened while they were gone.

Satoshi


### Wei points to his work

Hi Satoshi. b-money was announced on the cypherpunks mailing list in 1998. Here's the archived post:  
[https://cypherpunks.venona.com/date/1998/11/msg00941.html](https://cypherpunks.venona.com/date/1998/11/msg00941.html)

There are some discussions of it at  
[https://cypherpunks.venona.com/date/1998/12/msg00194.html](https://cypherpunks.venona.com/date/1998/12/msg00194.html).

Thanks for letting me know about your paper. I'll take a look at it and let you know if I have any comments or questions.


### Satoshi informs Wei of Bitcoin's release

From: Satoshi Nakamoto  
Sent: Saturday, January 10, 2009 11:17 AM  
To: weidai@weidai.com  
Subject: Re: Citation of your b-money page  

I wanted to let you know, I just released the full implementation of the paper I sent you a few months ago, Bitcoin v0.1.  Details, download and screenshots are at [www.bitcoin.org](www.bitcoin.org)

I think it achieves nearly all the goals you set out to solve in your b-money paper.

The system is entirely decentralized, without any server or trusted parties.  The network infrastructure can support a full range of escrow transactions and contracts, but for now the focus is on the basics of money and transactions.

There was a discussion of the design on the Cryptography mailing list. Hal Finney gave a good high-level overview:

> One thing I might mention is that in many ways bitcoin is two independent ideas: a way of solving the kinds of problems James lists here, of creating a globally consistent but decentralized database; and then using it for a system similar to Wei Dai's b-money (which is referenced in the paper) but transaction/coin based rather than account based. Solving the global, massively decentralized database problem is arguably the harder part, as James emphasizes. The use of proof-of-work as a tool for this purpose is a novel idea well worth further review IMO.

Satoshi


### Satoshi informs Adam of Bitcoin's release

From: "Satoshi Nakamoto" <satoshi@vistomail.com>  
Sent: Sat 10/1/2009 6:46:45 PM (UTC)  
To: adam@cypherspace.org  
Subject: Re: Citation of your Hashcash paper  

Thanks for the pointers you gave me to Wei Dai's b-money paper and others.

I just released the open source implementation of my paper, Bitcoin v0.1. Details, download and screenshots are at [www.bitcoin.org](www.bitcoin.org)

The main idea of the system is the generation of a chain of hash based proof-of-work to create self evident proof of the majority consensus. Users get new coins by contributing proof-of-work to the chain.

There was a discussion of the design on the Cryptography mailing list. Hal Finney gave a good high-level overview:

> One thing I might mention is that in many ways bitcoin is two independent ideas: a way of solving the kinds of problems James lists here, of creating a globally consistent but decentralized database; and then using it for a system similar to Wei Dai's b-money (which is referenced in the paper) but transaction/coin based rather than account based. Solving the global, massively decentralized database problem is arguably the harder part, as James emphasizes. The use of proof-of-work as a tool for this purpose is a novel idea well worth further review IMO.

Satoshi


## Cryptography mailing list


### Satoshi Nakamoto satoshi@vistomail.com (Fri Oct 31 14:10:00 EDT 2008)

> Note: Satoshi Nakamoto starts discussion "Bitcoin P2P e-cash paper"

I've been working on a new electronic cash system that's fully peer-to-peer, with no trusted third party.

The paper is available at: 

[http://www.bitcoin.org/bitcoin.pdf](http://www.bitcoin.org/bitcoin.pdf)

The main properties:

- Double-spending is prevented with a peer-to-peer network.
- No mint or other trusted parties.
- Participants can be anonymous.
- New coins are made from Hashcash style proof-of-work.
- The proof-of-work for new coin generation also powers the network to prevent double-spending.

Bitcoin: A Peer-to-Peer Electronic Cash System

Abstract.  A purely peer-to-peer version of electronic cash would allow online payments to be sent directly from one party to another without the burdens of going through a financial institution. Digital signatures provide part of the solution, but the main benefits are lost if a trusted party is still required to prevent double-spending.  We propose a solution to the double-spending problem using a peer-to-peer network.  The network timestamps transactions by hashing them into an ongoing chain of hash-based proof-of-work, forming a record that cannot be changed without redoing the proof-of-work.  The longest chain not only serves as proof of the sequence of events witnessed, but proof that it came from the largest pool of CPU power.  As long as honest nodes control the most CPU power on the network, they can generate the longest chain and outpace any attackers.  The network itself requires minimal structure.  Messages are broadcasted on a best effort basis, and nodes can leave and rejoin the network at will, accepting the longest proof-of-work chain as proof of what happened while they were gone.

Full paper at: 

[http://www.bitcoin.org/bitcoin.pdf](http://www.bitcoin.org/bitcoin.pdf)

Satoshi Nakamoto


### James A. Donald jamesd@echeque.com (Sun Nov 2 18:46:23 EST 2008)

Satoshi Nakamoto:
> I've been working on a new electronic cash system that's fully peer-to-peer, with no trusted third party.
> 
> The paper is available at: [http://www.bitcoin.org/bitcoin.pdf](http://www.bitcoin.org/bitcoin.pdf)

We very, very much need such a system, but the way I understand your proposal, it does not seem to scale to the required size.

For transferable proof of work tokens to have value, they must have monetary value.  To have monetary value, they must be transferred within a very large network - for example a file trading network akin to bittorrent.

To detect and reject a double spending event in a timely manner, one must have most past transactions of the coins in the transaction, which,  naively implemented, requires each peer to have most past transactions, or most past transactions that occurred recently. If hundreds of millions of people are doing transactions, that is a lot of bandwidth - each must know all, or a substantial part thereof.


### Satoshi Nakamoto satoshi@vistomail.com (Sun Nov 2 20:37:43 EST 2008)

James A. Donald:
>We very, very much need such a system, but the way I understand your proposal, it does not seem to scale to the required size.
>
>For transferable proof of work tokens to have value, they must have monetary value.  To have monetary value, they must be transferred within a very large network - for example a file trading network akin to bittorrent.
>
>To detect and reject a double spending event in a timely manner, one must have most past transactions of the coins in the transaction, which, naively implemented, requires each peer to have most past transactions, or most past transactions that occurred recently. If hundreds of millions of people are doing transactions, that is a lot of bandwidth - each must know all, or a substantial part thereof.

Long before the network gets anywhere near as large as that, it would be safe for users to use Simplified Payment Verification (section 8) to check for double spending, which only requires having the chain of block headers, or about 12KB per day.  Only people trying to create new coins would need to run network nodes.  At first, most users would run network nodes, but as the network grows beyond a certain point, it would be left more and more to specialists with server farms of specialized hardware.  A server farm would only need to have one node on the network and the rest of the LAN connects with that one node.

The bandwidth might not be as prohibitive as you think.  A typical transaction would be about 400 bytes (ECC is nicely compact).  Each transaction has to be broadcast twice, so lets say 1KB per transaction.  Visa processed 37 billion transactions in FY2008, or an average of 100 million transactions per day.  That many transactions would take 100GB of bandwidth, or the size of 12 DVD or 2 HD quality movies, or about $18 worth of bandwidth at current prices.

If the network were to get that big, it would take several years, and by then, sending 2 HD movies over the Internet would probably not seem like a big deal. 

Satoshi Nakamoto


### John Levine  johnl@iecc.com (Mon Nov 3 08:32:39 EST 2008)

Satoshi Nakamoto:
> As long as honest nodes control the most CPU power on the network, they can generate the longest chain and outpace any attackers.

But they don't. Bad guys routinely control zombie farms of 100,000 machines or more. People I know who run a blacklist of spam sending zombies tell me they often see a million new zombies a day.

This is the same reason that hashcash can't work on today's Internet -- the good guys have vastly less computational firepower than the bad guys.

I also have my doubts about other issues, but this one is the killer.

R's,
John


### Satoshi Nakamoto satoshi@vistomail.com (Mon Nov 3 11:23:49 EST 2008)

John Levine:
>But they don't.  Bad guys routinely control zombie farms of 100,000 machines or more.  People I know who run a blacklist of spam sending zombies tell me they often see a million new zombies a day.
>
>This is the same reason that hashcash can't work on today's Internet -- the good guys have vastly less computational firepower than the bad guys.

Thanks for bringing up that point.

I didn't really make that statement as strong as I could have.  The requirement is that the good guys collectively have more CPU power than any single attacker. 

There would be many smaller zombie farms that are not big enough to overpower the network, and they could still make money by generating bitcoins.  The smaller farms are then the "honest nodes".  (I need a better term than "honest")  The more smaller farms resort to generating bitcoins, the higher the bar gets to overpower the network, making larger farms also too small to overpower it so that they may as well generate bitcoins too.  According to the "long tail" theory, the small, medium and merely large farms put together should add up to a lot more than the biggest zombie farm.

Even if a bad guy does overpower the network, it's not like he's instantly rich.  All he can accomplish is to take back money he himself spent, like bouncing a check.  To exploit it, he would have to buy something from a merchant, wait till it ships, then overpower the network and try to take his money back.  I don't think he could make as much money trying to pull a carding scheme like that as he could by generating bitcoins.  With a zombie farm that big, he could generate more bitcoins than everyone else combined.

The Bitcoin network might actually reduce spam by diverting zombie farms to generating bitcoins instead.

Satoshi Nakamoto


### James A. Donald jamesd@echeque.com (Mon Nov 3 15:20:13 EST 2008)

Satoshi Nakamoto:
> Long before the network gets anywhere near as large as that, it would be Safe for users to use Simplified Payment Verification (section 8) to check for double spending, which only requires having the chain of block headers,

If I understand Simplified Payment Verification correctly:

New coin issuers need to store all coins and all recent coin transfers.

There are many new coin issuers, as many as want to be issuers, but far more coin users.

Ordinary entities merely transfer coins.  To see if a coin transfer is OK, they report it to one or more new coin issuers and see if the new coin issuer accepts it. New coin issuers check transfers of old coins so that their new coins have valid form, and they report the outcome of this check so that people will report their transfers to the new coin issuer.

If someone double spends a coin, and one expenditure is reported to one new coin issuer, and the other simultaneously reported to another new coin issuer, then both issuers to swifly agree on a unique sequence order of payments.  This, however, is a non trivial problem of a massively distributed massive database, a notoriously tricky problem, for which there are at present no peer to peer solutions.  Obviously it is a solvable problem, people solve it all the time, but not an easy problem. People fail to solve it rather more frequently.

But let us suppose that the coin issue network is dominated by a small number of issuers as seems likely.

If a small number of entities are issuing new coins, this is more resistant to state attack that with a single issuer, but the government regularly attacks financial networks, with the financial collapse ensuing from the most recent attack still under way as I write this.

Government sponsored enterprises enter the business, in due course bad behaviour is made mandatory, and the evil financial network is bigger than the honest financial network, with the result that even though everyone knows what is happening, people continue to use the paper issued by the evil financial network, because of network effects - the big, main issuers, are the issuers you use if you want to do business.

Then knowledgeable people complain that the evil financial network is heading for disaster, that the government sponsored enterprises are about to cause a "collapse of the total financial system", as Wallison and Alan Greenspan complained in 2005, the government debates shrinking the evil government sponsored enterprises, as with "S. 190 [109th]: Federal Housing Enterprise Regulatory Reform Act of 2005" but they find easy money too seductive, and S. 190 goes down in flames before a horde of political activists chanting that easy money is sound, and opposing it is racist, nazi, ignorant, and generally hateful, the recent S. 190 debate on limiting portfolios (bond issue supporting dud mortgages) by government sponsored enterprises being a perfect reprise of the debates on limiting the issue of new assignats in the 1790s.

The big and easy government attacks on money target a single central money issuer, as with the first of the modern political attacks, the French Assignat of 1792, but in the late nineteenth century political attacks on financial networks began, as for example the Federal reserve act of 1913, the goal always being to wind up the network into a single too big to fail entity, and they have been getting progressively bigger, more serious, and more disastrous, as with the most recent one.  Each attack is hugely successful, and after the cataclysm that the attack causes the attackers are hailed as saviors of the poor, the oppressed, and the nation generally, and the blame for the the bad consequences is dumped elsewhere, usually on Jews, greedy bankers, speculators, etc, because such attacks are difficult for ordinary people understand.  I have trouble understanding your proposal - ordinary users will be easily bamboozled by a government sponsored security update.  Further, when the crisis hits, to disagree with the line, to doubt that the regulators are right, and the problem is the evil speculators, becomes political suicide, as it did in America in 2007, sometimes physical suicide, as in Weimar Germany.

Still, it is better, and more resistant to attack by government sponsored enterprises, than anything I have seen so far.

Satoshi Nakamoto:
> Visa processed 37 billion transactions in FY2008, or > an average of 100 million transactions per day. That many transactions would take 100GB of bandwidth, or the size of 12 DVD or 2 HD quality movies, or about $18 worth of bandwidth at current prices.
>
> If the network were to get that big, it would take several years, and by then, sending 2 HD movies over the Internet would probably not seem like a big deal. If there were a hundred or a thousand money issuers by the time the government attacks, the kind of government attacks on financial networks that we have recently seen might well be more difficult.

But I think we need to concern ourselves with minimizing the data and bandwidth required by money issuers - for small coins, the protocol seems wasteful.  It would be nice to have the full protocol for big coins, and some shortcut for small coins wherein people trust account based money for small amounts till they get wrapped up into big coins.

The smaller the data storage and bandwidth required for money issuers, the more resistant the system is the kind of government attacks on financial networks that we have recently seen.


### Ray Dillinger bear@sonic.net (Thu Nov 6 00:14:37 EST 2008)

James A. Donald:
> If I understand Simplified Payment Verification correctly:
> 
> New coin issuers need to store all coins and all recent coin transfers.
> 
> There are many new coin issuers, as many as want to be issuers, but far more coin users.
> 
> Ordinary entities merely transfer coins.  To see if a coin transfer is OK, they report it to one or more new coin issuers and see if the new coin issuer accepts it. New coin issuers check transfers of old coins so that their new coins have valid form, and they report the outcome of this check so that people will report their transfers to the new coin issuer.

I think the real issue with this system is the market for bitcoins.  

Computing proofs-of-work have no intrinsic value.  We can have a limited supply curve (although the "currency" is inflationary at about 35% as that's how much faster computers get annually) but there is no demand curve that intersects it at a positive price point.

I know the same (lack of intrinsic value) can be said of fiat currencies, but an artificial demand for fiat currencies is created by (among other things) taxation and legal-tender laws.  Also, even a fiat currency can be an inflation hedge against another fiat currency's higher rate of inflation.   But in the case of bitcoins the inflation rate of 35% is almost guaranteed by the technology, there are no supporting mechanisms for taxation, and no legal-tender laws.  People will not hold assets in this highly-inflationary currency if they can help it.  

Bear


### Satoshi Nakamoto satoshi@vistomail.com (Thu Nov 6 15:15:40 EST 2008)

>[Lengthy exposition of vulnerability of a systm to use-of-force monopolies ellided.]
>
>You will not find a solution to political problems in cryptography.

Yes, but we can win a major battle in the arms race and gain a new territory of freedom for several years.

Governments are good at cutting off the heads of a centrally controlled networks like Napster, but pure P2P networks like Gnutella and Tor seem to be holding their own.  

Satoshi


### Perry E. Metzger perry@piermont.com (Fri Nov 7 12:32:23 EST 2008)

List Moderator's Edict of the Day:

A bunch of people seem anxious to branch the discussion of cryptographic cash protocols off into a discussion of the politics of money. I'm a rabid libertarian myself, but this isn't the rabid libertarian mailing list. Please stick to discussing either the protocols themselves or their direct practicality, and not the perils of fiat money, taxation, your aunt Mildred's gold coin collection, etc.

Perry


### zooko zooko@zooko.com (Fri Nov 7 16:10:31 EST 2008)

Hey folks: you are welcome to discuss money politics over at the p2p-hackers mailing list:

[http://lists.zooko.com/mailman/listinfo/p2p-hackers](http://lists.zooko.com/mailman/listinfo/p2p-hackers)

I'm extremely interested in the subject myself, having taken part in two notable failed attempts to deploy Chaumian digital cash and currently being involved in a project that might lead to a third attempt.

Regards,

Zooko


### Hal Finney hal@finney.org (Fri Nov 7 18:40:12 EST 2008)

Bitcoin seems to be a very promising idea. I like the idea of basing security on the assumption that the CPU power of honest participants outweighs that of the attacker. It is a very modern notion that exploits the power of the long tail. When Wikipedia started I never thought it would work, but it has proven to be a great success for some of the same reasons.

I also do think that there is potential value in a form of unforgeable token whose production rate is predictable and can't be influenced by corrupt parties. This would be more analogous to gold than to fiat currencies. Nick Szabo wrote many years ago about what he called "bit gold"[1] and this could be an implementation of that concept. There have also been proposals for building light-weight anonymous payment schemes on top of heavy-weight non-anonymous systems, so Bitcoin could be leveraged to allow for anonymity even beyond the mechanisms discussed in the paper.

Unfortunately I am having trouble fully understanding the system. The paper describes key concepts and some data structures, but does not clearly specify the various rules and verifications that the participants in the system would have to follow.

In particular I don't understand exactly what verifications P2P nodes perform when they receive new blocks from other nodes, and how they handle transactions that have been broadcast to them. For example, it is mentioned that if a broadcast transaction does not reach all nodes, it is OK, as it will get into the block chain before long. How does this happen - what if the node that creates the "next" block (the first node to find the hashcash collision) did not hear about the transaction, and then a few more blocks get added also by nodes that did not hear about that transaction? Do all the nodes that did hear it keep that transaction around, hoping to incorporate it into a block once they get lucky enough to be the one which finds the next collision?

Or for example, what if a node is keeping two or more chains around as it waits to see which grows fastest, and a block comes in for chain A which would include a double-spend of a coin that is in chain B? Is that checked for or not? (This might happen if someone double-spent and two different sets of nodes heard about the two different transactions with the same coin.)

This kind of data management, and the rules for handling all the packets that are flowing around is largely missing from the paper.
 
I also don't understand exactly how double-spending, or cancelling transactions, is accomplished by a superior attacker who is able to muster more computing power than all the honest participants. I see that he can create new blocks and add them to create the longest chain, but how can he erase or add old transactions in the chain? As the attacker sends out his new blocks, aren't there consistency checks which honest nodes can perform, to make sure that nothing got erased? More explanation of this attack would be helpful, in order to judge the gains to an attacker from this, versus simply using his computing power to mint new coins honestly.

As far as the spending transactions, what checks does the recipient of a coin have to perform? Does she need to go back through the coin's entire history of transfers, and make sure that every transaction on the list is indeed linked into the "timestamp" block chain? Or can she just do the latest one? Do the timestamp nodes check transactions, making sure that the previous transaction on a coin is in the chain, thereby enforcing the rule that all transactions in the chain represent valid coins?

Sorry about all the questions, but as I said this does seem to be a very promising and original idea, and I am looking forward to seeing how the concept is further developed. It would be helpful to see a more process oriented description of the idea, with concrete details of the data structures for the various objects (coins, blocks, transactions), the data which is included in messages, and algorithmic descriptions of the procedures for handling the various events which would occur in this system. You mentioned that you are working on an implementation, but I think a more formal, text description of the system would be a helpful next step.

Hal Finney

[1] [http://unenumerated.blogspot.com/2005/12/bit-gold.html](http://unenumerated.blogspot.com/2005/12/bit-gold.html)


### Satoshi Nakamoto satoshi@vistomail.com (Sat Nov 8 13:54:38 EST 2008)

Ray Dillinger:
> the "currency" is inflationary at about 35% as that's how much faster computers get annually... the inflation rate of 35% is almost guaranteed by the technology

Increasing hardware speed is handled: "To compensate for increasing hardware speed and varying interest in running nodes over time, the proof-of-work difficulty is determined by a moving average targeting an average number of blocks per hour. If they're generated too fast, the difficulty increases."

As computers get faster and the total computing power applied to creating bitcoins increases, the difficulty increases proportionally to keep the total new production constant.  Thus, it is known in advance how many new bitcoins will be created every year in the future.

The fact that new coins are produced means the money supply increases by a planned amount, but this does not necessarily result in inflation.  If the supply of money increases at the same rate that the number of people using it increases, prices remain stable.  If it does not increase as fast as demand, there will be deflation and early holders of money will see its value increase.

Coins have to get initially distributed somehow, and a constant rate seems like the best formula.

Satoshi Nakamoto


### Satoshi Nakamoto satoshi@vistomail.com (Sat Nov 8 20:58:48 EST 2008)

Hal Finney:
> it is mentioned that if a broadcast transaction does not reach all nodes, it is OK, as it will get into the block chain before long. How does this happen - what if the node that creates the "next" block (the first node to find the hashcash collision) did not hear about the transaction, and then a few more blocks get added also by nodes that did not hear about that transaction? Do all the nodes that did hear it keep that transaction around, hoping to incorporate it into a block once they get lucky enough to be the one which finds the next collision?

Right, nodes keep transactions in their working set until they get into a block.  If a transaction reaches 90% of nodes, then each time a new block is found, it has a 90% chance of being in it.

Hal Finney:
> Or for example, what if a node is keeping two or more chains around as it waits to see which grows fastest, and a block comes in for chain A which would include a double-spend of a coin that is in chain B? Is that checked for or not? (This might happen if someone double-spent and two different sets of nodes heard about the two different transactions with the same coin.)

That does not need to be checked for.  The transaction in whichever branch ends up getting ahead becomes the valid one, the other is invalid.  If someone tries to double spend like that, one and only one spend will always become valid, the others invalid.

Receivers of transactions will normally need to hold transactions for perhaps an hour or more to allow time for this kind of possibility to be resolved.  They can still re-spend the coins immediately, but they should wait before taking an action such as shipping goods.  

Hal Finney:
> I also don't understand exactly how double-spending, or cancelling> transactions, is accomplished by a superior attacker who is able to muster more computing power than all the honest participants. I see that he can create new blocks and add them to create the longest chain, but how can he erase or add old transactions in the chain? As the attacker sends out his new blocks, aren't there consistency checks which honest nodes can perform, to make sure that nothing got erased? More explanation of this attack would be helpful, in order to judge the gains to an attacker from this, versus simply using his computing power to mint new coins honestly.

The attacker isn't adding blocks to the end.  He has to go back and redo the block his transaction is in and all the blocks after it, as well as any new blocks the network keeps adding to the end while he's doing that.  He's rewriting history.  Once his branch is longer, it becomes the new valid one.

This touches on a key point.  Even though everyone present may see the shenanigans going on, there's no way to take advantage of that fact. 

It is strictly necessary that the longest chain is always considered the valid one.  Nodes that were present may remember that one branch was there first and got replaced by another, but there would be no way for them to convince those who were not present of this.  We can't have subfactions of nodes that cling to one branch that they think was first, others that saw another branch first, and others that joined later and never saw what happened.  The CPU power proof-of-work vote must have the final say.  The only way for everyone to stay on the same page is to believe that the longest chain is always the valid one, no matter what.

Hal Finney:
> As far as the spending transactions, what checks does the recipient of a coin have to perform? Does she need to go back through the coin's entire history of transfers, and make sure that every transaction on the list is indeed linked into the "timestamp" block chain? Or can she just do the latest one? 

The recipient just needs to verify it back to a depth that is sufficiently far back in the block chain, which will often only require a depth of 2 transactions.  All transactions before that can be discarded.

Hal Finney:
> Do the timestamp nodes check transactions, making sure that the previous transaction on a coin is in the chain, thereby enforcing the rule that all transactions in the chain represent valid coins?

Right, exactly.  When a node receives a block, it checks the signatures of every transaction in it against previous transactions in blocks.  Blocks can only contain transactions that depend on valid transactions in previous blocks or the same block.  Transaction C could depend on transaction B in the same block and B depends on transaction A in an earlier block.

Hal Finney:
> Sorry about all the questions, but as I said this does seem to be a very promising and original idea, and I am looking forward to seeing how the concept is further developed. It would be helpful to see a more process oriented description of the idea, with concrete details of the data structures for the various objects (coins, blocks, transactions), the data which is included in messages, and algorithmic descriptions of the procedures for handling the various events which would occur in this system. You mentioned that you are working on an implementation, but I think a more formal, text description of the system would be a helpful next step.

I appreciate your questions.  I actually did this kind of backwards.  I had to write all the code before I could convince myself that I could solve every problem, then I wrote the paper.  I think I will be able to release the code sooner than I could write a detailed spec.  You're already right about most of your assumptions where you filled in the blanks.

Satoshi Nakamoto


### Satoshi Nakamoto satoshi@vistomail.com (Sat Nov 8 22:09:49 EST 2008)

James A. Donald:
> The core concept is that lots of entities keep complete and consistent information as to who owns which bitcoins.
>
> But maintaining consistency is tricky. It is not clear to me what happens when someone reports one transaction to one maintainer, and someone else transports another transaction to another maintainer. The transaction cannot be known to be valid until it has been incorporated into a globally shared view of all past transactions, and no one can know that a globally shared view of all past transactions is globally shared until after some time has passed, and after many new transactions have arrived.
>
> Did you explain how to do this, and it just passed over my head, or were you confident it could be done, and a bit vague as to the details?

The proof-of-work chain is the solution to the synchronisation problem, and to knowing what the globally shared view is without having to trust anyone.

A transaction will quickly propagate throughout the network, so if two versions of the same transaction were reported at close to the same time, the one with the head start would have a big advantage in reaching many more nodes first.  Nodes will only accept the first one they see, refusing the second one to arrive, so the earlier transaction would have many more nodes working on incorporating it into the next proof-of-work.  In effect, each node votes for its viewpoint of which transaction it saw first by including it in its proof-of-work effort.

If the transactions did come at exactly the same time and there was an even split, it's a toss up based on which gets into a proof-of-work first, and that decides which is valid.

When a node finds a proof-of-work, the new block is propagated throughout the network and everyone adds it to the chain and starts working on the next block after it.  Any nodes that had the other transaction will stop trying to include it in a block, since it's now invalid according to the accepted chain.

The proof-of-work chain is itself self-evident proof that it came from the globally shared view.  Only the majority of the network together has enough CPU power to generate such a difficult chain of proof-of-work.  Any user, upon receiving the proof-of-work chain, can see what the majority of the network has approved.  Once a transaction is hashed into a link that's a few links back in the chain, it is firmly etched into the global history.

Satoshi Nakamoto


### James A. Donald jamesd@echeque.com (Sat Nov 8 23:55:23 EST 2008)

Satoshi Nakamoto:
 > The bandwidth might not be as prohibitive as you think.  A typical transaction would be about 400 bytes (ECC is nicely compact).  Each transaction has to be broadcast twice, so lets say 1KB per transaction. Visa processed 37 billion transactions in FY2008, or an average of 100 million transactions per day.  That many transactions would take 100GB of bandwidth, or the size of 12 DVD or 2 HD quality movies, or about $18 worth of bandwidth at current prices.

The trouble is, you are comparing with the Bankcard network.

But a new currency cannot compete directly with an old, because network effects favor the old.

You have to go where Bankcard does not go.

At present, file sharing works by barter for bits. This, however requires the double coincidence of wants. People only upload files they are downloading, and once the download is complete, stop seeding. So only active files, files that quite a lot of people want at the same time, are available.

File sharing requires extremely cheap transactions, several transactions per second per client, day in and day out, with monthly transaction costs being very small per client, so to support file sharing on bitcoins, we will need a layer of account money on top of the bitcoins, supporting transactions of a hundred thousandth the size of the smallest coin, and to support anonymity, chaumian money on top of the account money.

Let us call a bitcoin bank a bink.  The bitcoins stand in the same relation to account money as gold stood in the days of the gold standard.  The binks, not trusting each other to be liquid when liquidity is most needed, settle out any net discrepancies with each other by moving bit coins around once every hundred thousand seconds or so, so bitcoins do not change owners that often,   Most transactions cancel out at the account level.  The binks demand bitcoins of each other only because they don't want to hold account money for too long. So a relatively small amount of bitcoins infrequently transacted can support a somewhat larger amount of account money frequently transacted.


### James A. Donald jamesd@echeque.com (Sun Nov 9 03:56:53 EST 2008)

Satoshi Nakamoto:
 > The proof-of-work chain is the solution to the synchronisation problem, and to knowing what the globally shared view is without having to trust anyone.
 >
 > A transaction will quickly propagate throughout the network, so if two versions of the same transaction were reported at close to the same time, the one with the head start would have a big advantage in reaching many more nodes first.  Nodes will only accept the first one they see, refusing the second one to arrive, so the earlier transaction would have many more nodes working on incorporating it into the next proof-of-work.  In effect, each node votes for its viewpoint of which transaction it saw first by including it in its proof-of-work effort.

OK, suppose one node incorporates a bunch of transactions in its proof of work, all of them honest legitimate single spends and another node incorporates a slightly different bunch of transactions in its proof of work, all of them equally honest legitimate single spends, and both proofs are generated at about the same time.

What happens then?


### James A. Donald jamesd@echeque.com (Sun Nov 9 05:05:05 EST 2008)

Satoshi Nakamoto:
 > Increasing hardware speed is handled: "To compensate for increasing hardware speed and varying interest in running nodes over time, the proof-of-work difficulty is determined by a moving average targeting an average number of blocks per hour. If they're generated too fast, the difficulty increases."

This does not work - your proposal involves complications I do not think you have thought through.

Furthermore, it cannot be made to work, as in the proposed system the work of tracking who owns what coins is paid for by seigniorage, which requires inflation.

This is not an intolerable flaw - predictable inflation is less objectionable than inflation that gets jiggered around from time to time to transfer wealth from one voting block to another.


### Satoshi Nakamoto satoshi@vistomail.com (Sun Nov 9 11:31:26 EST 2008)

James A. Donald:
>OK, suppose one node incorporates a bunch of transactions in its proof of work, all of them honest legitimate single spends and another node incorporates a different bunch of transactions in its proof of work, all of them equally honest legitimate single spends, and both proofs are generated at about the same time.
>
>What happens then?

They both broadcast their blocks.  All nodes receive them and keep both, but only work on the one they received first.  We'll suppose exactly half received one first, half the other.  

In a short time, all the transactions will finish propagating so that everyone has the full set.  The nodes working on each side will be trying to add the transactions that are missing from their side.  When the next proof-of-work is found, whichever previous block that node was working on, that branch becomes longer and the tie is broken.  Whichever side it is, the new block will contain the other half of the transactions, so in either case, the branch will contain all transactions.  Even in the unlikely event that a split happened twice in a row, both sides of the second split would contain the full set of transactions anyway.

It's not a problem if transactions have to wait one or a few extra cycles to get into a block. 

Satoshi Nakamoto


### James A. Donald jamesd@echeque.com (Sun Nov 9 14:57:54 EST 2008)

Satoshi Nakamoto:
> They both broadcast their blocks.  All nodes receive them and keep both, but only work on the one they received first.  We'll suppose exactly half received one first, half the other.
>
> In a short time, all the transactions will finish propagating so that everyone has the full set.  The nodes working on each side will be trying to add the transactions that are missing from their side.  When the next proof-of-work is found, whichever previous block that node was working on, that branch becomes longer and the tie is broken.  Whichever side it is, the new block will contain the other half of the transactions, so in either case, the branch will contain all transactions.  Even in the unlikely event that a split happened twice in a row, both sides of the second split would contain the full set of transactions anyway.
>
> It's not a problem if transactions have to wait one or a few extra cycles to get into a block.

So what happened to the coin that lost the race?

On the one hand, we want people who make coins to be motivated to keep and record all transactions, and obtain an up to date record of all transactions in a timely manner.  On the other hand, it is a bit harsh if the guy who came second is likely to lose his coin.

Further, your description of events implies restrictions on timing and coin generation - that the entire network generates coins slowly compared to the time required for news of a new coin to flood the network, otherwise the chains diverge more and more, and no one ever knows which chain is the winner.

You need to make these restrictions explicit, for network flood time may well be quite slow.

Which implies that the new coin rate is slower.

We want spenders to have certainty that their transaction is valid at the time it takes a spend to flood the network, not at the time it takes for branch races to be resolved.

At any given time, for example at 1 040 689 138 seconds we can look back at the past and say:

- At 1 040 688 737 seconds, node 5 was *it*, and he incorporated all the coins he had discovered into the chain, and all the new transactions he knew about on top of the previous link.

- At 1 040 688 792 seconds, node 2 was *it*, and he incorporated all the coins he had discovered into the chain, and all the new transactions he knew about into the chain on top of node 5's link.

- At 1 040 688 745 seconds, node 7 was *it*, and he incorporated all the coins he had discovered into the chain, and all the new transactions he knew about into the chain on top of node 2's link.

But no one can know who is *it* right now

So how does one know when to reveal one's coins?  One solution is that one does not.  One incorporates a hash of the coin secret whenever one thinks one might be *it*, and after that hash is securely in the chain, after one knows that one was *it* at the time, one can then safely spend the coin that one has found, revealing the secret.

This solution takes care of the coin revelation problem, but does not solve the spend recording problem.  If one node is ignoring all spends that it does not care about, it suffers no adverse consequences.  We need a protocol in which your prospects of becoming *it* also depend on being seen by other nodes as having a reasonably up to date and complete list of spends - which this protocol is not, and your protocol is not either.


### Satoshi Nakamoto satoshi@vistomail.com (Sun Nov 9 21:14:30 EST 2008)

James A. Donald:
> Furthermore, it cannot be made to work, as in the proposed system the work of tracking who owns what coins is paid for by seigniorage, which requires inflation.

If you're having trouble with the inflation issue, it's easy to tweak it for transaction fees instead.  It's as simple as this: let the output value from any transaction be 1 cent less than the input value.  Either the client software automatically writes transactions for 1 cent more than the intended payment value, or it could come out of the payee's side.  The incentive value when a node finds a proof-of-work for a block could be the total of the fees in the block.

Satoshi Nakamoto


### Satoshi Nakamoto satoshi@vistomail.com (Mon Nov 10 17:18:20 EST 2008)

James A. Donald:
> So what happened to the coin that lost the race?
>
> ... it is a bit harsh if the guy who came second is likely to lose his coin.

When there are multiple double-spent versions of the same transaction, one and only one will become valid.

The receiver of a payment must wait an hour or so before believing that it's valid.  The network will resolve any possible double-spend races by then.

The guy who received the double-spend that became invalid never thought he had it in the first place.  His software would have shown the transaction go from "unconfirmed" to "invalid".  If necessary, the UI can be made to hide transactions until they're sufficiently deep in the block chain.

James A. Donald:
> Further, your description of events implies restrictions on timing and coin generation - that the entire network generates coins slowly compared to the time required for news of a new coin to flood the network

Sorry if I didn't make that clear.  The target time between blocks will probably be 10 minutes.

Every block includes its creation time.  If the time is off by more than 36 hours, other nodes won't work on it.  If the timespan over the last 6*24*30 blocks is less than 15 days, blocks are being generated too fast and the proof-of-work difficulty doubles.  Everyone does the same calculation with the same chain data, so they all get the same result at the same link in the chain.

James A. Donald:
> We want spenders to have certainty that their transaction is valid at the time it takes a spend to flood the network, not at the time it takes for branch races to be resolved.

Instantant non-repudiability is not a feature, but it's still much faster than existing systems.  Paper cheques can bounce up to a week or two later.  Credit card transactions can be contested up to 60 to 180 days later.  Bitcoin transactions can be sufficiently irreversible in an hour or two.

James A. Donald:
> If one node is ignoring all spends that it does not  care about, it suffers no adverse consequences.

With the transaction fee based incentive system I recently posted, nodes would have an incentive to include all the paying transactions they receive.

Satoshi Nakamoto


### James A. Donald jamesd@echeque.com (Thu Nov 13 01:16:31 EST 2008)

Satoshi Nakamoto:
> When there are multiple double-spent versions of the same transaction, one and only one will become valid.

That is not the question I am asking.

It is not trust that worries me, it is how it is possible to have a  a globally shared view even if everyone is well behaved.

The process for arriving at a globally shared view of who owns what bitgold coins is insufficiently specified. Once specified, then we can start considering whether everyone has incentives to behave correctly.

It is not sufficient that everyone knows X.  We also need everyone to know that everyone knows X, and that everyone knows that everyone knows that everyone knows X - which, as in the Byzantine Generals problem, is the classic hard problem of distributed data processing.

This problem becomes harder when X is quite possibly a very large amount of data - agreement on who was the owner of every bitgold coin at such and such a time.

And then on top of that we need everyone to have a motive to behave in such a fashion that agreement arises.  I cannot see that they have motive when I do not know the behavior to be motivated.

You keep repeating your analysis of the system under attack.  We cannot say how the system will behave under attack until we know how the system is supposed to behave when not under attack.

If there are a lot of transactions, it is hard to efficiently discover the discrepancies between one node's view and another node's view, and because new transactions are always arriving, no two nodes will ever have the same view, even if all nodes are honest, and all reported transactions are correct and true single spends.

We should be able to accomplish a system where two nodes are likely to come to agreement as to who owned what bitgold coins at some very recent past time, but it is not simple to do so.

If one node constructs a hash that represents its knowledge of who owned what bitgold coins at a particular time, and another node wants to check that hash, it is not simple to do it in such a way that agreement is likely, and disagreement between honest well behaved nodes is efficiently detected and efficiently resolved.

And if we had a specification of how agreement is generated, it is not obvious why the second node has incentive to check that hash.

The system has to work in such a way that nodes can easily and cheaply change their opinion about recent transactions, so as to reach consensus, but in order to provide finality and irreversibility, once consensus has been reached, and then new stuff has be piled on top of old consensus, in particular new bitgold has been piled on top of old consensus, it then becomes extremely difficult to go back and change what was decided.

Saying that is how it works, does not give us a method to make it work that way.

Satoshi Nakamoto:
> The receiver of a payment must wait an hour or so before believing that it's valid.  The network will resolve any possible double-spend races by then.

You keep discussing attacks.  I find it hard to think about response to attack when it is not clear to me what normal behavior is in the case of good conduct by each and every party.

Distributed databases are *hard* even when all the databases perfectly follow the will of a single owner. Messages get lost, links drop, syncrhonization delays become abnormal, and entire machines go up in flames, and the network as a whole has to take all this in its stride.

Figuring out how to do this is hard, even in the complete absence of attacks.  Then when we have figured out how to handle all this, then come attacks.


### Hal Finney hal@finney.org (Thu Nov 13 11:24:18 EST 2008)

James A. Donald:
> Satoshi Nakamoto:
> > When there are multiple double-spent versions of the same transaction, one and only one will become valid.
>
> That is not the question I am asking.
>
> It is not trust that worries me, it is how it is possible to have a  a globally shared view even if everyone is well behaved.
>
> The process for arriving at a globally shared view of who owns what bitgold coins is insufficiently specified.

I agree that the description is not completely clear on how these matters are handled. Satoshi has suggested that releasing source code may be the best way to clarify the design. As I have tried to work through details on my own, it does appear that the rules become rather complicated and indeed one needs at least a pseudo-code algorithm to specify the behavior. So perhaps writing real code is not a bad way to go. I found that there is a sourceforge project set up for bitgold, although it does not have any code yet.

In answer to James' specific question, about what happens when different nodes see different sets of transactions, due to imperfect broadcast, here is how I understand it. Each node must be prepared to maintain potentially several "candidate" block chains, each of which may eventually turn out to become the longest one, the one which wins. Once a given block chain becomes sufficiently longer than a competitor, the shorter one can be deleted. This length differential is a parameter which depends on the node's threat model for how much compute power an attacker can marshall, in terms of the fraction of the "honst" P2P network's work capacity, and is estimated in the paper. The idea is that once a chain gets far enough behind the longest one, there is essentially no chance that it can ever catch up.

In order to resolve the issue James raised, I think it is necessary that nodes keep a separate pending-transaction list associated with each candidate chain. This list would include all transactions the node has received (via broadcast by the transactees) but which have not yet been incorporated into that block chain. At any given time, the node is working to extend the longest block chain, and the block it is working to find a hash collision for will include all of the pending transactions associated with that chain.

I think that this way, when a candidate chain is deleted because it got too much shorter than the longest one, transactions in it are not lost, but have continued to be present in the pending-transaction list associated with the longest chain, in those nodes which heard the original transaction broadcast. (I have also considered whether nodes should add transactions to their pending-transaction list that they learn about through blocks from other nodes, even if those blocks do not end up making their way into the longest block chain; but I'm not sure if that is necessary or helpful.)

Once these rules are clarified, more formal modeling will be helpful in understanding the behavior of the network given imperfect reliability. For example, if on average a fraction f of P2P nodes receive a given transaction broadcast, then I think one would expect 1/f block-creation times to elapse before the transaction appears in what is destined to become the longest chain. One might also ask, given that the P2P network broadcast is itself imperfectly reliable, how many candidate chains must a given node keep track of at one time, on average? Or as James raised earlier, if the network broadcast is reliable but depends on a potentially slow flooding algorithm, how does that impact performance?

James A. Donald:
> And then on top of that we need everyone to have a motive to behave in such a fashion that agreement arises.  I cannot see that they have motive when I do not know the behavior to be motivated.

I am somewhat less worried about motivation. I'd be satisfied if the system can meet the following criteria:

1. No single node operator, or small collection of node operators which controls only a small fraction of overall network resources, can effectively cheat, if other players are honest.

2. The long tail of node operators is sufficiently large that no small collection of nodes can control more than a small fraction of overall resources. (Here, the "tail" refers to a ranking based on amount of resources controlled by each operator.)

3. The bitcoin system turns out to be socially useful and valuable, so that node operators feel that they are making a beneficial contribution to the world by their efforts (similar to the various "@Home" compute projects where people volunteer their compute resources for good causes).

In this case it seems to me that simple altruism can suffice to keep the network running properly.

James A. Donald:
> Distributed databases are *hard* even when all the databases perfectly follow the will of a single owner. Messages get lost, links drop, syncrhonization delays become abnormal, and entire machines go up in flames, and the network as a whole has to take all this in its stride.

A very good point, and a more complete specification is necessary in order to understand how the network will respond to imperfections like this. I am looking forward to seeing more detail emerge.

One thing I might mention is that in many ways bitcoin is two independent ideas: a way of solving the kinds of problems James lists here, of creating a globally consistent but decentralized database; and then using it for a system similar to Wei Dai's b-money (which is referenced in the paper) but transaction/coin based rather than account based. Solving the global, massively decentralized database problem is arguably the harder part, as James emphasizes. The use of proof-of-work as a tool for this purpose is a novel idea well worth further review IMO.

Hal Finney


### Satoshi Nakamoto satoshi@vistomail.com (Thu Nov 13 17:56:55 EST 2008)

James A. Donald:
> It is not sufficient that everyone knows X. We also need everyone to know that everyone knows X, and that everyone knows that everyone knows that everyone knows X - which, as in the Byzantine Generals problem, is the classic hard problem of distributed data processing.

The proof-of-work chain is a solution to the Byzantine Generals' Problem.  I'll try to rephrase it in that context.

A number of Byzantine Generals each have a computer and want to attack the King's wi-fi by brute forcing the password, which they've learned is a certain number of characters in length.  Once they stimulate the network to generate a packet, they must crack the password within a limited time to break in and erase the logs, otherwise they will be discovered and get in trouble.  They only have enough CPU power to crack it fast enough if a majority of them attack at the same time.

They don't particularly care when the attack will be, just that they all agree.  It has been decided that anyone who feels like it will announce a time, and whatever time is heard first will be the official attack time.  The problem is that the network is not instantaneous, and if two generals announce different attack times at close to the same time, some may hear one first and others hear the other first.

They use a proof-of-work chain to solve the problem.  Once each general receives whatever attack time he hears first, he sets his computer to solve an extremely difficult proof-of-work problem that includes the attack time in its hash.  The proof-of-work is so difficult, it's expected to take 10 minutes of them all working at once before one of them finds a solution.  Once one of the generals finds a proof-of-work, he broadcasts it to the network, and everyone changes their current proof-of-work computation to include that proof-of-work in the hash they're working on.  If anyone was working on a different attack time, they switch to this one, because its proof-of-work chain is now longer.

After two hours, one attack time should be hashed by a chain of 12 proofs-of-work.  Every general, just by verifying the difficulty of the proof-of-work chain, can estimate how much parallel CPU power per hour was expended on it and see that it must have required the majority of the computers to produce that much proof-of-work in the allotted time.  They had to all have seen it because the proof-of-work is proof that they worked on it.  If the CPU power exhibited by the proof-of-work chain is sufficient to crack the password, they can safely attack at the agreed time.

The proof-of-work chain is how all the synchronisation, distributed database and global view problems you've asked about are solved.


### Satoshi Nakamoto satoshi@vistomail.com (Fri Nov 14 13:55:35 EST 2008)

Hal Finney:
> I think it is necessary that nodes keep a separate pending-transaction list associated with each candidate chain. ... One might also ask ... how many candidate chains must a given node keep track of at one time, on average?

Fortunately, it's only necessary to keep a pending-transaction pool for the current best branch.  When a new block arrives for the best branch, ConnectBlock removes the block's transactions from the pending-tx pool.  If a different branch becomes longer, it calls DisconnectBlock on the main branch down to the fork, returning the block transactions to the pending-tx pool, and calls ConnectBlock on the new branch, sopping back up any transactions that were in both branches.  It's expected that reorgs like this would be rare and shallow.

With this optimisation, candidate branches are not really any burden.  They just sit on the disk and don't require attention unless they ever become the main chain.

Hal Finney:
> Or as James raised earlier, if the network broadcast is reliable but depends on a potentially slow flooding algorithm, how does that impact performance?

Broadcasts will probably be almost completely reliable.  TCP transmissions are rarely ever dropped these days, and the broadcast protocol has a retry mechanism to get the data from other nodes after a while.  If broadcasts turn out to be slower in practice than expected, the target time between blocks may have to be increased to avoid wasting resources.  We want blocks to usually propagate in much less time than it takes to generate them, otherwise nodes would spend too much time working on obsolete blocks.

I'm planning to run an automated test with computers randomly sending payments to each other and randomly dropping packets.

Hal Finney:
> 3. The bitcoin system turns out to be socially useful and valuable, so that node operators feel that they are making a beneficial contribution to the world by their efforts (similar to the various "@Home" compute projects where people volunteer their compute resources for good causes).
> 
> In this case it seems to me that simple altruism can suffice to keep the network running properly.

It's very attractive to the libertarian viewpoint if we can explain it properly.  I'm better with code than with words though.

Satoshi Nakamoto


### Ray Dillinger bear@sonic.net (Fri Nov 14 21:20:23 EST 2008)

Okay.... I'm going to summarize this protocol as I understand it. 

I'm filling in some operational details that aren't in the paper by supplementing what you wrote with what my own "design sense" tells me are critical missing bits or "obvious" methodologies for use.

First, people spend computer power creating a pool of coins to use as money.  Each coin is a proof-of-work meeting whatever criteria were in effect for money at the time it was created.  The time of creation (and therefore the criteria) is checkable later because people can see the emergence of this particular coin in the transaction chain and track it through all its "consensus view" spends.  (more later on coin creation tied to adding a link). 

When a coin is spent, the buyer and seller digitally sign a (blinded) transaction record, and broadcast it to a bunch of nodes whose purpose is keeping track of consensus regarding coin ownership.  If someone double spends, then the transaction record can be unblinded revealing the identity of the cheater.  This is done via a fairly standard cut-and-choose algorithm where the buyer responds to several challenges with secret shares, and the seller then asks him to "unblind" and checks all but one, verifying that they do contain secret shares any two of which are sufficient to identify the buyer.  In this case the seller accepts the unblinded spend record as "probably" containing a valid secret share. 

The nodes keeping track of consensus regarding coin ownership are in a loop where they are all trying to "add a link" to the longest chain they've so far recieved.  They have a pool of reported transactions which they've not yet seen in a "consensus" signed chain.  I'm going to call this pool "A".  They attempt to add a link to the chain by moving everything from pool A into a pool "L" and using a CPU-intensive digital signature algorithm to sign the chain including the new block L.  This results in a chain extended by a block containing all the transaction records they had in pool L, plus the node's digital signature.  While they do this, new transaction records continue to arrive and go into pool A again for the next cycle of work. 

They may also receive chains as long as the one they're trying to extend while they work, in which the last few "links" are links that are *not* in common with the chain on which they're working. These they ignore.  (?  Do they ignore them?  Under what circumstances would these become necessary to ever look at again, bearing in mind that any longer chain based on them will include them?) 

But if they receive a _longer_ chain while working, they immediately check all the transactions in the new links to make sure it contains no double spends and that the "work factors" of all new links are appropriate.  If it contains a double spend, then they create a "transaction" which is a proof of double spending, add it to their pool A, broadcast it, and continue work.  If one of the "new" links has an inappropriate work factor (ie, someone didn't put enough CPU into it for it to be "licit" according to the rules) a new "transaction" which is a proof of the protocol violation by the link-creating node is created, broadcast, and added to pool A, and the chain is rejected.  In the case of no double spends and appropriate work factors for all links not yet seen, they accept the new chain as consensus. 

If the new chain is accepted, then they give up on adding their current link, dump all the transactions from pool L back into pool A (along with transactions they've recieved or created since starting work), eliminate from pool A those transaction records which are already part of a link in the new chain, and start work again trying to extend the new chain. 

If they complete work on a chain extended with their new link, they broadcast it and immediately start work on another new link with all the transactions that have accumulated in pool A since they began work.  

Do I understand it correctly?

Biggest Technical Problem: 

Is there a mechanism to make sure that the "chain" does not consist solely of links added by just the 3 or 4 fastest nodes?  'Cause a broadcast transaction record could easily miss those 3 or 4 nodes and if it does, and those nodes continue to dominate the chain, the transaction might never get added.  

To remedy this, you need to either ensure provable propagation of transactions, or vary the work factor for a node depending on how many links have been added since that node's most recent link.

Unfortunately, both measures can be defeated by sock puppets.  This is probably the worst problem with your protocol as it stands right now; you need some central point to control the identities (keys) of the nodes and prevent people from making new sock puppets. 

Provable propagation would mean that When Bob accepts a new chain from Alice, he needs to make sure that Alice has (or gets) all transactions in his "A" and "L" pools.  He sends them, and Alice sends back a signed hash to prove she got them. Once Alice has received this block of transactions, if any subsequent chains including a link added by Alice do not include those transactions at or before that link, then Bob should be able to publish the block he sent Alice, along with her signature, in a transaction as proof that Alice violated protocol.  Sock puppets defeat this because Alice just signs subsequent chains using a new key, pretending to be a different node. 

If we go with varying the work factor depending on how many new links there are,  then we're right back to domination by the 3 or 4 fastest nodes, except now they're joined by 600 or so sock puppets which they use to avoid the work factor penalty. 

If we solve the sock-puppet issue, or accept that there's a central point controlling the generation of new keys, then generation of coins should be tied to the act of successfully adding a block to the "consensus" chain.  This is simple to do; creation of a coin is a transaction, it gets added along with all the other transactions in the block.  But you can only create one coin per link, and of course if your version of the chain isn't the one that gets accepted, then in the "accepted" view you don't have the coin and can't spend it.  This gives the people maintaining the consensus database a reason to spend CPU cycles, especially since the variance in work factor by number of links added since their own last link (outlined above) guarantees that everyone, not just the 3 or 4 fastest nodes, occasionally gets the opportunity to create a coin.

Also, the work requirement for adding a link to the chain should vary (again exponentially) with the number of links added to that chain in the previous week, causing the rate of coin generation (and therefore inflation) to be strictly controlled.  

You need coin aggregation for this to scale.  There needs to be a "provable" transaction where someone retires ten single coins and creates a new coin with denomination ten, etc.  This is not too hard, using the same infrastructure you've already got; it simply becomes part of the chain, and when the chain is accepted consensus, then everybody can see that it happened. 

Bear


### Satoshi Nakamoto satoshi@vistomail.com (Fri Nov 14 23:43:00 EST 2008)

I'll try and hurry up and release the sourcecode as soon as possible to serve as a reference to help clear up all these implementation questions.

Ray Dillinger:
> When a coin is spent, the buyer and seller digitally sign a (blinded) transaction record.

Only the buyer signs, and there's no blinding. 

Ray Dillinger:
> If someone double spends, then the transaction record can be unblinded revealing the identity of the cheater. 

Identities are not used, and there's no reliance on recourse.  It's all prevention.

Ray Dillinger:
> This is done via a fairly standard cut-and-choose algorithm where the buyer responds to several challenges with secret shares

No challenges or secret shares.  A basic transaction is just what you see in the figure in section 2.  A signature (of the buyer) satisfying the public key of the previous transaction, and a new public key (of the seller) that must be satisfied to spend it the next time.

Ray Dillinger:
> They may also receive chains as long as the one they're trying to extend while they work, in which the last few "links" are links that are *not* in common with the chain on which they're working. These they ignore. 

Right, if it's equal in length, ties are broken by keeping the earliest one received.

Ray Dillinger:
> If it contains a double spend, then they create a "transaction" which is a proof of double spending, add it to their pool A, broadcast it, and continue work.

There's no need for reporting of "proof of double spending" like that.  If the same chain contains both spends, then the block is invalid and rejected.  

Same if a block didn't have enough proof-of-work.  That block is invalid and rejected.  There's no need to circulate a report about it.  Every node could see that and reject it before relaying it.

If there are two competing chains, each containing a different version of the same transaction, with one trying to give money to one person and the other trying to give the same money to someone else, resolving which of the spends is valid is what the whole proof-of-work chain is about.

We're not "on the lookout" for double spends to sound the alarm and catch the cheater.  We merely adjudicate which one of the spends is valid.  Receivers of transactions must wait a few blocks to make sure that resolution has had time to complete.  Would be cheaters can try and simultaneously double-spend all they want, and all they accomplish is that within a few blocks, one of the spends becomes valid and the others become invalid.  Any later double-spends are immediately rejected once there's already a spend in the main chain.  

Even if an earlier spend wasn't in the chain yet, if it was already in all the nodes' pools, then the second spend would be turned away by all those nodes that already have the first spend.

Ray Dillinger:
> If the new chain is accepted, then they give up on adding their current link, dump all the transactions from pool L back into pool A (along with transactions they've received or created since starting work), eliminate from pool A those transaction records which are already part of a link in the new chain, and start work again trying to extend the new chain.

Right.  They also refresh whenever a new transaction comes in, so L pretty much contains everything in A all the time.

Ray Dillinger:
> CPU-intensive digital signature algorithm to sign the chain including the new block L. 

It's a Hashcash style SHA-256 proof-of-work (partial pre-image of zero), not a signature.  

Ray Dillinger:
> Is there a mechanism to make sure that the "chain" does not consist solely of links added by just the 3 or 4 fastest nodes? 'Cause a broadcast transaction record could easily miss those 3 or 4 nodes and if it does, and those nodes continue to dominate the chain, the transaction might never get added.

If you're thinking of it as a CPU-intensive digital signing, then you may be thinking of a race to finish a long operation first and the fastest always winning.

The proof-of-work is a Hashcash style SHA-256 collision finding.  It's a memoryless process where you do millions of hashes a second, with a small chance of finding one each time.  The 3 or 4 fastest nodes' dominance would only be proportional to their share of the total CPU power.  Anyone's chance of finding a solution at any time is proportional to their CPU power.

There will be transaction fees, so nodes will have an incentive to receive and include all the transactions they can.  Nodes will eventually be compensated by transaction fees alone when the total coins created hits the pre-determined ceiling.

Ray Dillinger:
> Also, the work requirement for adding a link to the chain should vary (again exponentially) with the number of links added to that chain in the previous week, causing the rate of coin generation (and therefore inflation) to be strictly controlled.

Right.

Ray Dillinger:
> You need coin aggregation for this to scale. There needs to be a "provable" transaction where someone retires ten single coins and creates a new coin with denomination ten, etc. 

Every transaction is one of these.  Section 9, Combining and Splitting Value.  


Satoshi Nakamoto


### Ray Dillinger bear@sonic.net (Sat Nov 15 02:04:21 EST 2008)

Satoshi Nakamoto:
> I'll try and hurry up and release the sourcecode as soon as possible to serve as a reference to help clear up all these implementation questions.
>
> Ray Dillinger:
> > When a coin is spent, the buyer and seller digitally sign a (blinded)
> > transaction record.
> 
> Only the buyer signs, and there's no blinding. 
> 
> Ray Dillinger:
> > If someone double spends, then the transaction record 
> > can be unblinded revealing the identity of the cheater. 
> 
> Identities are not used, and there's no reliance on recourse.  It's all prevention.

Okay, that's surprising.  If you're not using buyer/seller identities, then you are not checking that a spend is being made by someone who actually is the owner of (on record as having received) the coin being spent.  

There are three categories of identity that are useful to think about.  Category one: public.  Real-world identities are a matter of record and attached to every transaction.  Category two: Pseudonymous.  There are persistent "identities" within the system and people can see if something was done by the same nym that did something else, but there's not necessarily any way of linking the nyms with real-world identities.  Category three: unlinkably anonymous.  There is no concept of identity, persistent or otherwise.  No one can say or prove whether the agents involved in any transaction are the same agents as involved in any other transaction. 

Are you claiming category 3 as you seem to be, or category 2? Lots of people don't distinguish between anonymous and pseudonymous protocols, so it's worth asking exactly what you mean here.  

Anyway:  I'll proceed on the assumption that you meant very nearly (as nearly as I can imagine, anyway) what you said, unlinkably anonymous.  That means that instead of an "identity", a spender has to demonstrate knowledge of a secret known only to the real owner of the coin.  One way to do this would be to have the person recieving the coin generate an asymmetric key pair, and then have half of it published with the transaction.  In order to spend the coin later, s/he must demonstrate posession of the other half of the asymmetric key pair, probably by using it to sign the key provided by the new seller.  So we cannot prove anything about "identity", but we can prove that the spender of the coin is someone who knows a secret that the person who recieved the coin knows.

And what you say next seems to confirm this: 

Satoshi Nakamoto:
> No challenges or secret shares.  A basic transaction is just what you see in the figure in section 2.  A signature (of the buyer) satisfying the public key of the previous transaction, and a new public key (of the seller) that must be satisfied to spend it the next time.

Note, even though this doesn't involve identity per se, it still makes the agent doing the spend linkable to the agent who earlier recieved the coin, so these transactions are linkable. In order to counteract this, the owner of the coin needs to make a transaction, indistinguishable to others from any normal transaction, in which he creates a new key pair and transfers the coin to its posessor (ie, has one sock puppet "spend" it to another). No change in real-world identity of the owner, but the transaction "linkable" to the agent who spent the coin is unlinked.  For category-three unlinkability, this has to be done a random number of times - maybe one to six times?  

BTW, could you please learn to use carriage returns??  Your lines are scrolling stupidly off to the right and I have to scroll to see what the heck you're saying, then edit to add carriage returns before I respond. 

Satoshi Nakamoto:
> Ray Dillinger:
> > If it contains a double spend, then they create a "transaction" which is a proof of double spending, add it to their pool A, broadcast it, and continue work.
>
> There's no need for reporting of "proof of double spending" like that.  If the same chain contains both spends, then the block is invalid and rejected.  
>
> Same if a block didn't have enough proof-of-work.  That block is invalid and rejected.  There's no need to circulate a report about it.  Every node could see that and reject it before relaying it.

Mmmm.  I don't know if I'm comfortable with that.  You're saying there's no effort to identify and exclude nodes that don't cooperate?  I suspect this will lead to trouble and possible DOS attacks. 

Satoshi Nakamoto:
> If there are two competing chains, each containing a different version of the same transaction, with one trying to give money to one person and the other trying to give the same money to someone else, resolving which of the spends is valid is what the whole proof-of-work chain is about.

Okay, when you say "same" transaction, and you're talking about transactions that are obviously different, you mean a double spend, right?  Two transactions signed with the same key?

Satoshi Nakamoto:
> We're not "on the lookout" for double spends to sound the alarm and catch the cheater.  We merely adjudicate which one of the spends is valid.  Receivers of transactions must wait a few blocks to make sure that resolution has had time to complete. 

Until.... until what?  How does anybody know when a transaction has become irrevocable?   Is "a few" blocks three?  Thirty?  A hundred?  Does it depend on the number of nodes?  Is it logarithmic or linear in number of nodes?  

Satoshi Nakamoto:
> Would be cheaters can try and simultaneously double-spend all they want, and all they accomplish is that within a few blocks, one of the spends becomes valid and the others become valid.

But in the absence of identity, there's no downside to them if spends become invalid, if they've already received the goods they double-spent for (access to website, download, whatever).  The merchants are left holding the bag with "invalid" coins, unless they wait that magical "few blocks" (and how can they know how many?) before treating the spender as having paid.  

The consumers won't do this if they spend their coin and it takes an hour to clear before they can do what they spent their coin on. The merchants won't do it if there's no way to charge back a customer when they find the that their coin is invalid because the customer has doublespent.

Satoshi Nakamoto:
> Even if an earlier spend wasn't in the chain yet, if it was already in all the nodes' pools, then the second spend would be turned away by all those nodes that already have the first spend.

So there's a possibility of an early catch when the broadcasts of the initial simultaneous spends interfere with each other.  I assume here that the broadcasts are done by the sellers, since the buyer has a possible disincentive to broadly disseminate spends. 

Satoshi Nakamoto:
> Ray Dillinger:
> > If the new chain is accepted, then they give up on adding their current link ... and start work again trying to extend the new chain.
> 
> Right.  They also refresh whenever a new transaction comes in, so L pretty much contains everything in A all the time.

Okay, that's a big difference between a proof of work that takes a huge set number of CPU cycles and a proof of work that takes a tiny number of CPU cycles but has a tiny chance of success.  You can change the data set while working, and it doesn't mean you need to start over. This is good in this case, as it means nobody has to hold recently received transactions out of the link they're working on.

Satoshi Nakamoto:
> Ray Dillinger:
> > Is there a mechanism to make sure that the "chain" does not consist solely of links added by just the 3 or 4 fastest nodes? 
>
> If you're thinking of it as a CPU-intensive digital signing, then you may be thinking of a race to finish a long operation first and the fastest always winning.

Right.  That was the misconception I was working with.  Again, the difference between a proof taking a huge set number of CPU cycles and a proof that takes a tiny number of CPU cycles but has a tiny chance of success.

Satoshi Nakamoto:
> Anyone's chance of finding a solution at any time is proportional to their CPU power.

It's like a random variation in the work factor; in this way it works in your favor. 

Satoshi Nakamoto:
> There will be transaction fees, so nodes will have an incentive to receive and include all the transactions they can.  Nodes will eventually be compensated by transaction fees alone when the total coins created hits the pre-determined ceiling.

I don't understand how "transaction fees" would work, and how the money would find its way from the agents doing transactions to those running the network.  But the economic effect is the same (albeit somewhat randomized) if adding a link to the chain allows the node to create a coin, so I would stick with that.

Also, be aware that the compute power of different nodes can be expected to vary by two orders of magnitude at any given moment in history. 

Bear


### Satoshi Nakamoto satoshi@vistomail.com (Sat Nov 15 13:02:00 EST 2008)

Ray Dillinger:
> One way to do this would be to have the person recieving the coin generate an asymmetric key pair, and then have half of it published with the transaction. In order to spend the coin later, s/he must demonstrate posession of the other half of the asymmetric key pair, probably by using it to sign the key provided by the new seller.

Right, it's ECC digital signatures.  A new key pair is used for every transaction.

It's not pseudonymous in the sense of nyms identifying people, but it is at least a little pseudonymous in that the next action on a coin can be identified as being from the owner of that coin.

Ray Dillinger:
> Mmmm. I don't know if I'm comfortable with that. You're saying there's no effort to identify and exclude nodes that don't cooperate? I suspect this will lead to trouble and possible DOS attacks.

There is no reliance on identifying anyone.  As you've said, it's futile and can be trivially defeated with sock puppets. 

The credential that establishes someone as real is the ability to supply CPU power. 

Ray Dillinger:
> Until.... until what? How does anybody know when a transaction has become irrevocable? Is "a few" blocks three? Thirty? A hundred? Does it depend on the number of nodes? Is it logarithmic or linear in number of nodes?

Section 11 calculates the worst case under attack.  Typically, 5 or 10 blocks is enough for that.  If you're selling something that doesn't merit a network-scale attack to steal it, in practice you could cut it closer.

Ray Dillinger:
> But in the absence of identity, there's no downside to them if spends become invalid, if they've already received the goods they double-spent for (access to website, download, whatever). The merchants are left holding the bag with "invalid" coins, unless they wait that magical "few blocks" (and how can they know how many?) before treating the spender as having paid.
>
> The consumers won't do this if they spend their coin and it takes an hour to clear before they can do what they spent their coin on. The merchants won't do it if there's no way to charge back a customer when they find the that their coin is invalid because the customer has doublespent.

This is a version 2 problem that I believe can be solved fairly satisfactorily for most applications.

The race is to spread your transaction on the network first.  Think 6 degrees of freedom -- it spreads exponentially.  It would only take something like 2 minutes for a transaction to spread widely enough that a competitor starting late would have little chance of grabbing very many nodes before the first one is overtaking the whole network.  During those 2 minutes, the merchant's nodes can be watching for a double-spent transaction.  The double-spender would not be able to blast his alternate transaction out to the world without the merchant getting it, so he has to wait before starting.

If the real transaction reaches 90% and the double-spent tx reaches 10%, the double-spender only gets a 10% chance of not paying, and 90% chance his money gets spent.  For almost any type of goods, that's not going to be worth it for the scammer.

Information based goods like access to website or downloads are non-fencible.  Nobody is going to be able to make a living off stealing access to websites or downloads.  They can go to the file sharing networks to steal that.  Most instant-access products aren't going to have a huge incentive to steal. 

If a merchant actually has a problem with theft, they can make the customer wait 2 minutes, or wait for something in e-mail, which many already do.  If they really want to optimize, and it's a large download, they could cancel the download in the middle if the transaction comes back double-spent.  If it's website access, typically it wouldn't be a big deal to let the customer have access for 5 minutes and then cut off access if it's rejected.  Many such sites have a free trial anyway.

Satoshi Nakamoto


### James A. Donald jamesd@echeque.com (Sat Nov 15 19:00:04 EST 2008)

Satoshi Nakamoto:
 > Fortunately, it's only necessary to keep a pending-transaction pool for the current best branch.

This requires that we know, that is to say an honest well behaved peer whose communications and data storage is working well knows, what the current best branch is - but of course, the problem is that we are trying to discover, trying to converge upon, a best branch, which is not easy at the best of times, and becomes harder when another peer is lying about its connectivity and capabilities, and yet another peer has just had a major disk drive failure obfuscated by a software crash, and the international fibers connecting yet a third peer have been attacked by terrorists.

Satoshi Nakamoto:
>  When a new block arrives for the best branch,  ConnectBlock removes the block's transactions from the pending-tx pool.  If a different branch becomes longer

Which presupposes the branches exist, that they are fully specified and complete.  If they exist as complete works, rather than works in progress, then the problem is already solved, for the problem is making progress.

Satoshi Nakamoto:
> Broadcasts will probably be almost completely reliable.

There is a trade off between timeliness and reliability. One can make a broadcast arbitrarily reliable if time is of no consequence.  However, when one is talking of distributed data, time is always of consequence, because it is all about synchronization (that peers need to have corresponding views at corresponding times) so when one does distributed data processing, broadcasts are always highly unreliable Attempts to ensure that each message arrives at least once result in increased timing variation. Thus one has to make a protocol that is either UDP or somewhat UDP like, in that messages are small, failure of messages to arrive is common, messages can arrive in different order to the order in which they were sent, and the same message may arrive multiple times.  Either we have UDP, or we need to accommodate the same problems as UDP has on top of TCP connections.

Rather than assuming that each message arrives at least once, we have to make a mechanism such that the information arrives even though conveyed by messages that frequently fail to arrive.

Satoshi Nakamoto:
> TCP transmissions are rarely ever dropped these days

People always load connections near maximum.  When a connection is near maximum, TCP connections suffer frequent unreasonably long delays, and connections simply fail a lot - your favorite web cartoon somehow shows it is loading forever, and you try again, or it comes up with a little x in place of a picture, and you try again

Further very long connections - for example ftp downloads of huge files,  seldom complete. If you try to ftp a movie, you are unlikely to get anywhere unless both client and server have a resume mechanism so that they can talk about partially downloaded files.

UDP connections, for example Skype video calls, also suffer frequent picture freezes, loss of quality, and so forth, and have to have mechanisms to keep going regardless.

Satoshi Nakamoto:
> It's very attractive to the libertarian viewpoint if we can explain it properly.  I'm better with code than with words though.

No, it is very attractive to the libertarian if we can design a mechanism that will scale to the point of providing the benefits of rapidly irreversible payment, immune to political interference, over the internet, to very large numbers of people. You have an outline and proposal for such a design, which is a big step forward, but the devil is in the little details.

I really should provide a fleshed out version of your proposal, rather than nagging you to fill out the blind spots.


### Satoshi Nakamoto satoshi@vistomail.com (Mon Nov 17 12:24:43 EST 2008)

James A. Donald:
> Satoshi Nakamoto:
> > Fortunately, it's only necessary to keep a pending-transaction pool for the current best branch.
> 
> This requires that we know, that is to say an honest well behaved peer whose communications and data storage is working well knows, what the current best branch is -

I mean a node only needs the pending-tx pool for the best branch it has.  The branch that it currently thinks is the best branch. That's the branch it'll be trying to make a block out of, which is all it needs the pool for.

James A. Donald:
> Satoshi Nakamoto:
> > Broadcasts will probably be almost completely reliable.
> 
> Rather than assuming that each message arrives at least once, we have to make a mechanism such that the information arrives even though conveyed by messages that frequently fail to arrive.

I think I've got the peer networking broadcast mechanism covered.  

Each node sends its neighbours an inventory list of hashes of the new blocks and transactions it has.  The neighbours request the items they don't have yet.  If the item never comes through after a timeout, they request it from another neighbour that had it.  Since all or most of the neighbours should eventually have each item, even if the coms get fumbled up with one, they can get it from any of the others, trying one at a time.

The inventory-request-data scheme introduces a little latency, but it ultimately helps speed more by keeping extra data blocks off the transmit queues and conserving bandwidth.

James A. Donald:
> You have an outline and proposal for such a design, which is a big step forward, but the devil is in the little details.

I believe I've worked through all those little details over the last year and a half while coding it, and there were a lot of them. The functional details are not covered in the paper, but the sourcecode is coming soon.  I sent you the main files. (available by request at the moment, full release soon)

Satoshi Nakamoto


### Perry E. Metzger perry@piermont.com (Mon Nov 17 16:43:33 EST 2008)

I'd like to call an end to the bitcoin e-cash discussion for now -- a lot of discussion is happening that would be better accomplished by people writing papers at the moment rather than rehashing things back and forth. Maybe later on when Satoshi (or someone else) writes something detailed up and posts it we could have another round of this.

Perry
-- 
Perry E. Metzger
[perry at piermont.com](perry at piermont.com)


### Nicolas Williams Nicolas.Williams@sun.com (Mon Nov 17 16:54:28 EST 2008)

Ray Dillinger:
> Satoshi Nakamoto:
> > Ray Dillinger:
> > > If someone double spends, then the transaction record 
> > > can be unblinded revealing the identity of the cheater. 
> > 
> > Identities are not used, and there's no reliance on recourse.  It's all prevention.
> 
> Okay, that's surprising.  If you're not using buyer/seller identities, then you are not checking that a spend is being made by someone who actually is the owner of (on record as having received) the coin being spent.  

How do identities help?  It's supposed to be anonymous cash, right?  And say you identify a double spender after the fact, then what?  Perhaps you're looking at a disposable ID.  Or perhaps you can't chase them down.

Double spend detection needs to be real-time or near real-time.

Nico


### James A. Donald jamesd@echeque.com (Mon Nov 17 18:57:39 EST 2008)

Ray Dillinger:
> Okay.... I'm going to summarize this protocol as I understand it.
>
> I'm filling in some operational details that aren't in the paper by supplementing what you wrote with what my own "design sense" tells me are critical missing bits or "obvious" methodologies for use.

There are a number of significantly different ways this could be implemented.  I have been working on my own version based on Patricia hash trees, (not yet ready to post, will post in a week or so) with the consensus generation being a generalization of file sharing using Merkle hash trees. Patricia hash trees where the high order part of the Patricia key represents the high order part of the time can be used to share data that evolves in time.  The algorithm, if implemented by honest correctly functioning peers, regularly generates consensus hashes of the recent past - thereby addressing the problem I have been complaining about - that we have a mechanism to protect against consensus distortion by dishonest or malfunctioning peers, which is useless absent a definition of consensus generation by honest and correctly functioning peers.

Ray Dillinger:
> First, people spend computer power creating a pool of coins to use as money.  Each coin is a proof-of-work meeting whatever criteria were in effect for money at the time it was created.  The time of creation (and therefore the criteria) is checkable later because people can see the emergence of this particular coin in the transaction chain and track it through all its "consensus view" spends.  (more later on coin creation tied to adding a link).
>
> When a coin is spent, the buyer and seller digitally sign a (blinded) transaction record, and broadcast it to a bunch of nodes whose purpose is keeping track of consensus regarding coin ownership.

I don't think your blinding works.

If there is a public record of who owns what coin, we have to generate a  public diff on changes in that record, so the record will show that a coin belonged to X, and soon thereafter belonged to Y.  I don't think blinding can be made to work.  We can blind the transaction details easily enough, by only making hashes of the details public, (X paid Y for 49vR7xmwYcKXt9zwPJ943h9bHKC2pG68m) but that X paid Y is going to be fairly obvious.

If when Joe spends a coin to me, then I have to have the ability to ask "Does Joe rightfully own this coin", then it is difficult to see how this can be implemented in a distributed protocol without giving people the ability to trawl through data detecting that Joe paid me.

To maintain a consensus on who owns what coins, who owns what coins has to be public.

We can build a privacy layer on top of this - account money and chaumian money based on bitgold coins, much as the pre 1915 US banking system layered account money and bank notes on top of gold coins, and indeed we have to build a layer on top to bring the transaction cost down to the level that supports agents performing micro transactions, as needed for bandwidth control, file sharing, and charging non white listed people to send us communications.

So the entities on the public record are entities functioning like pre 1915 banks - let us call them binks, for post 1934 banks no longer function like that.

Ray Dillinger:
> But if they receive a _longer_ chain while working, they immediately check all the transactions in the new links to make sure it contains no double spends and that the "work factors" of all new links are appropriate.

I am troubled that this involves frequent retransmissions of data that is already mostly known. Consensus and widely distributed beliefs about bitgold ownership already involves significant cost.  Further, each transmission of data is subject to data loss, which can result in thrashing, with the risk that the generation of consensus may slow below the rate of new transactions.  We already have problems getting the cost down to levels that support micro transactions by software agents, which is the big unserved market - bandwidth control, file sharing, and charging non white listed people to send us communications.

To work as useful project, has to be as efficient as it can be - hence my plan to use a Patricia hash tree because it identifies and locate small discrepancies between peers that are mostly in agreement already, without them needing to transmit their complete data.

We also want to avoid very long hash chains that have to be frequently checked in order to validate things.  Any time a hash chain can potentially become enormously long over time, we need to ensure that no one ever has to rewalk the full length.  Chains that need to be re-walked can only be permitted to grow as the log of the total number of transactions - if they grow as the log of the transactions in any one time period plus the total number of time periods, we have a problem.

Ray Dillinger:
 > Biggest Technical Problem:
 >
 > Is there a mechanism to make sure that the "chain" does not consist solely of links added by just the 3 or 4 fastest nodes?  'Cause a broadcast transaction record could easily miss those 3 or 4 nodes and if it does, and those nodes continue to dominate the chain, the transaction might never get added.
 >
 > To remedy this, you need to either ensure provable propagation of transactions, or vary the work factor for a node depending on how many links have been added since that node's most recent link.
 >
 > Unfortunately, both measures can be defeated by sock puppets. This is probably the worst problem with your protocol as it stands right now; you need some central point to control the identities (keys) of the nodes and prevent people from making new sock puppets.

We need a protocol wherein to be a money tracking peer (an entity that validates spends) you have to be accepted by at least two existing peers who agree to synchronize data with you - presumably through human intervention by the owners of existing peers, and these two human approved synchronization paths indirectly connect you to the other peers in the network through at least one graph cycle.

If peer X is only connected to the rest of the network by one existing peer, peer Y, perhaps because X's directly connecting peer has dropped out, then X is demoted to a client, not a peer - any transactions X submits are relabeled by Y as submitted to Y, not X, and the time of submission (which forms part of the Patricia key) is the time X submitted them to Y, not the time they were submitted to X.

The algorithm must be able swiftly detect malfunctioning peers, and automatically exclude them from the consensus temporarily - which means that transactions submitted through malfunctioning peers do not get included in the consensus, therefore have to be resubmitted, and peers may find themselves temporarily demoted to clients, because one of the peers through which they were formerly connected to the network has been dropped by the consensus.

If a peer gets a lot of automatic temporary exclusions, there may be human intervention by the owners of those peers to which it exchanges data directly to permanently drop them.

Since peers get accepted by human invite, they have reputation to lose, therefore we can make the null hypothesis (the primary Bayesian prior) honest intent, valid data, but  unreliable data transmission - trust with infrequent random verification.  Designing the system on this basis considerably reduces processing costs.

Recall that SET died on its ass in large part because every transaction involved innumerable public key operations.  Similarly, we have huge security flaws in https because it has so many redundant public key operations that web site designers try to minimize the use of https to cover only those areas that truly need it - and they always get the decision as to what truly
needs it subtly wrong.

Efficiency is critical, particularly as the part of the market not yet served is the market for very low cost transactions.

Ray Dillinger:
 > If we solve the sock-puppet issue, or accept that there's a central point controlling the generation of  new keys,

A central point will invite attack, will be attacked.

The problem with computer networked money is that the past can so easily be revised, so nodes come under pressure to adjust the past - "I did not pay that" swiftly becomes "I should not have paid that", which requires arbitration, which is costly, and introduces uncertainty, which is costly, and invites government regulation, which is apt to be utterly ruinous and wholly devastating.

For many purposes, reversal and arbitration is highly desirable, but there is no way anyone can compete with the arbitration provided by Visa and Mastercard, for they have network effects on their side, and they do a really good job of arbitration, at which they have vast experience, accumulated skills, wisdom, and good repute. So any new networked transaction system has to target the demand for final and irreversible transactions.

The idea of a distributed network consensus is that one has a lot of peers in a lot of jurisdictions, and once a transaction has entered into the consensus, undoing it is damn near impossible - one would have to pressure most of the peers in most of the jurisdictions to agree, and many of them don't even talk your language, and those that do, will probably pretend that they do not. So people will not even try.

To avoid pressure, the network has to avoid any central point at which pressure can be applied.  Recall Nero's wish that Rome had a single throat that he could cut. If we provide them with such a throat, it will be cut.


### James A. Donald jamesd@echeque.com (Mon Nov 17 20:26:31 EST 2008)

Nicolas Williams:
> How do identities help?  It's supposed to be anonymous cash, right?

Actually no.  It is however supposed to be pseudonymous, so dinging someone's reputation still does not help much.

> And say you identify a double spender after the fact, then what?  Perhaps you're looking at a disposable ID. Or perhaps you can't chase them down.
>
> Double spend detection needs to be real-time or near real-time.

Near real time means we have to use UDP or equivalent, rather than TCP or equivalent, and we have to establish an approximate consensus, not necessarily the final consensus, not necessarily exact agreement, but close to it, in a reasonably small number of round trips.

(Note: This ends the discussion "Bitcoin P2P e-cash paper")


### Satoshi Nakamoto satoshi@vistomail.com (Thu Jan 8 14:27:40 EST 2009)

(Note: Satoshi Nakamoto starts discussion "Bitcoin v0.1 released")

Announcing the first release of Bitcoin, a new electronic cash system that uses a peer-to-peer network to prevent double-spending. It's completely decentralized with no server or central authority.

See [bitcoin.org](https://bitcoin.org) for screenshots.

Download link:

[http://downloads.sourceforge.net/bitcoin/bitcoin-0.1.0.rar](http://downloads.sourceforge.net/bitcoin/bitcoin-0.1.0.rar)

Windows only for now.  Open source C++ code is included.

- Unpack the files into a directory
- Run BITCOIN.EXE
- It automatically connects to other nodes

If you can keep a node running that accepts incoming connections, you'll really be helping the network a lot.  Port 8333 on your firewall needs to be open to receive incoming connections.

The software is still alpha and experimental.  There's no guarantee the system's state won't have to be restarted at some point if it becomes necessary, although I've done everything I can to build in extensibility and versioning.

You can get coins by getting someone to send you some, or turn on Options->Generate Coins to run a node and generate blocks.  I made the proof-of-work difficulty ridiculously easy to start with, so for a little while in the beginning a typical PC will be able to generate coins in just a few hours.  It'll get a lot harder when competition makes the automatic adjustment drive up the difficulty. Generated coins must wait 120 blocks to mature before they can be spent.

There are two ways to send money.  If the recipient is online, you can enter their IP address and it will connect, get a new public key and send the transaction with comments.  If the recipient is not online, it is possible to send to their Bitcoin address, which is a hash of their public key that they give you.  They'll receive the transaction the next time they connect and get the block it's in.  This method has the disadvantage that no comment information is sent, and a bit of privacy may be lost if the address is used multiple times, but it is a useful alternative if both users can't be online at the same time or the recipient can't receive incoming connections.

Total circulation will be 21,000,000 coins.  It'll be distributed to network nodes when they make blocks, with the amount cut in half every 4 years.

- first 4 years: 10,500,000 coins
- next 4 years: 5,250,000 coins
- next 4 years: 2,625,000 coins
- next 4 years: 1,312,500 coins
- etc...

When that runs out, the system can support transaction fees if needed.  It's based on open market competition, and there will probably always be nodes willing to process transactions for free.

Satoshi Nakamoto


### Hal Finney hal@finney.org (Sat Jan 10 21:22:01 EST 2009)

Satoshi Nakamoto:
> Announcing the first release of Bitcoin, a new electronic cash system that uses a peer-to-peer network to prevent double-spending. It's completely decentralized with no server or central authority.
>
> See [bitcoin.org](https://bitcoin.org) for screenshots.
>
> Download link:
>
> [http://downloads.sourceforge.net/bitcoin/bitcoin-0.1.0.rar](http://downloads.sourceforge.net/bitcoin/bitcoin-0.1.0.rar)

Congratulations to Satoshi on this first alpha release.  I am looking forward to trying it out.

Satoshi Nakamoto:
> Total circulation will be 21,000,000 coins.  It'll be distributed to network nodes when they make blocks, with the amount cut in half every 4 years.
>
> - first 4 years: 10,500,000 coins
> - next 4 years: 5,250,000 coins
> - next 4 years: 2,625,000 coins
> - next 4 years: 1,312,500 coins
> - etc...

It's interesting that the system can be configured to only allow a certain maximum number of coins ever to be generated. I guess the idea is that the amount of work needed to generate a new coin will become more difficult as time goes on.

One immediate problem with any new currency is how to value it. Even ignoring the practical problem that virtually no one will accept it at first, there is still a difficulty in coming up with a reasonable argument in favour of a particular non-zero value for the coins.

As an amusing thought experiment, imagine that Bitcoin is successful and becomes the dominant payment system in use throughout the world.  Then the total value of the currency should be equal to the total value of all the wealth in the world. Current estimates of total worldwide household wealth that I have found range from $100 trillion to $300 trillion. With 20 million coins, that gives each coin a value of about $10 million.

So the possibility of generating coins today with a few cents of compute time may be quite a good bet, with a payoff of something like 100 million to 1! Even if the odds of Bitcoin succeeding to this degree are slim, are they really 100 million to one against? Something to think about...

Hal


### Satoshi Nakamoto satoshi@vistomail.com (Fri Jan 16 11:03:14 EST 2009)

Dustin D. Trammell:
> Satoshi Nakamoto:
> > You know, I think there were a lot more people interested in the 90's, but after more than a decade of failed Trusted Third Party based systems (Digicash, etc), they see it as a lost cause. I hope they can make the distinction that this is the first time I know of that we're trying a non-trust-based system.
>
> Yea, that was the primary feature that caught my eye. The real trick will be to get people to actually value the BitCoins so that they become currency.
 
I would be surprised if 10 years from now we're not using electronic currency in some way, now that we know a way to do it that won't inevitably get dumbed down when the trusted third party gets cold feet.

It could get started in a narrow niche like reward points, donation tokens, currency for a game or micropayments for adult sites.  Initially it can be used in proof-of-work applications for services that could almost be free but not quite.

It can already be used for pay-to-send e-mail.  The send dialog is resizeable and you can enter as long of a message as you like. It's sent directly when it connects.  The recipient double clicks on the transaction to see the full message.  If someone famous is getting more e-mail than they can read, but would still like to have a way for fans to contact them, they could set up Bitcoin and give out the IP address on their website.  "Send X bitcoins to my priority hotline at this IP and I'll read the message personally." 

Subscription sites that need some extra proof-of-work for their free trial so it doesn't cannibalize subscriptions could charge bitcoins for the trial.

It might make sense just to get some in case it catches on.  If enough people think the same way, that becomes a self fulfilling prophecy.  Once it gets bootstrapped, there are so many applications if you could effortlessly pay a few cents to a website as easily as dropping coins in a vending machine.

Satoshi Nakamoto

[http://www.bitcoin.org](http://www.bitcoin.org)


### Jonathan Thornburg jthorn@astro.indiana.edu (Sat Jan 17 11:49:45 EST 2009)

Satoshi Nakamoto:
> [various possible uses of Bitcoin et al]
> Once it gets bootstrapped, there are so many applications if you could effortlessly pay a few cents to a website as easily as dropping coins in a vending machine.  

In the modern world, no major government wants to allow untrackable international financial transactions above some fairly modest size thresholds.  (The usual catch-phrases are things like "laundering drug money", "tax evasion", and/or "financing terrorist groups".) To this end, electronic financial transactions are currently monitored by various governments & their agencies, and any but the smallest of transactions now come with various ID requirements for the humans on each end.

But if each machine in a million-node botnet sends 10 cents to a randomly chosen machine in another botnet on the other side of the world, you've just moved $100K, in a way that seems very hard to trace.  To me, this means that no major government is likely to allow Bitcoin in its present form to operate on a large scale.

I also worry about other "domestic" ways nasty people could exploit a widespread Bitcoin deployment:

- Spammer botnets could burn through pay-per-send email filters trivially (as usual, the costs would fall on people other than the botnet herders & spammers).

- If each machine in a botnet sends 1 cent to a herder, that can add up to a significant amount of money.  In other words, Bitcoin would make botnet herding and the assorted malware industry even more profitable than it already is.

Is there something obvious I've missed?  Is there a clever aspect of the design which prevents botnets from exploiting the system?  Is there a way for every major government to monitor all Bitcoin transactions to watch for botnet-to-botnet sending?


### Hal Finney hal@finney.org (Sat Jan 24 11:48:03 EST 2009)

Jonathan Thornburg:
> In the modern world, no major government wants to allow untrackable international financial transactions above some fairly modest size thresholds.  (The usual catch-phrases are things like "laundering drug money", "tax evasion", and/or "financing terrorist groups".) To this end, electronic financial transactions are currently monitored by various governments & their agencies, and any but the smallest of transactions now come with various ID requirements for the humans on each end.
>
> But if each machine in a million-node botnet sends 10 cents to a randomly chosen machine in another botnet on the other side of the world, you've just moved $100K, in a way that seems very hard to trace.  To me, this means that no major government is likely to allow Bitcoin in its present form to operate on a large scale.

Certainly a valid point, and one which has been widely discussed in the debates over the years about electronic cash. Bitcoin has a couple of things going for it: one is that it is distributed, with no single point of failure, no "mint", no company with officers that can be subpoenaed and arrested and shut down. It is more like a P2P network, and as we have seen, despite degrees of at least governmental distaste, those are still around.

Bitcoin could also conceivably operate in a less anonymous mode, with transfers being linked to individuals, rather than single-use keys. It would still be useful to have a large scale, decentralized electronic payment system.

It also might be possible to refactor and restructure Bitcoin to separate out the key new idea, a decentralized, global, irreversible transaction database. Such a functionality might be useful for other purposes. Once it exists, using it to record monetary transfers would be a sort of side effect and might be harder to shut down.

Jonathan Thornburg:

> I also worry about other "domestic" ways nasty people could exploit a widespread Bitcoin deployment:
> 
> - Spammer botnets could burn through pay-per-send email filters trivially (as usual, the costs would fall on people other than the botnet herders & spammers).
>
> - If each machine in a botnet sends 1 cent to a herder, that can add up to a significant amount of money.  In other words, Bitcoin would make botnet herding and the assorted malware industry even more profitable than it already is.

It's important to understand that the proof-of-work (POW) aspect of Bitcoin is primarily oriented around ensuring the soundness of the historical transaction database. Each Bitcoin data block records a set of transactions, and includes a hash collision. Subsequent data blocks have their own transactions, their own collisions, and also chain to all earlier hashes.  The result is that once a block is "buried" under enough new blocks, it is essentially certain (given the threat model, namely that attackers cannot muster more than X% of the compute power of legitimate node operators) that old transactions can't be reversed.

Creating new coins is indeed currently also being done by POW, but I think that is seen as a temporary expedient, and in fact the current software phases that out over several years. Hence worries about botnets being able to manufacture large quantities of POW tokens are only a temporary concern, in the context of Bitcoin.

There have been a number of discussions in the past about POW tokens as anti spam measures, given the botnet threat. References are available from "Proof-of-work system" on Wikipedia. Analyses have yielded mixed results, depending on the assumptions and system design.

If POW tokens do become useful, and especially if they become money, machines will no longer sit idle. Users will expect their computers to be earning them money (assuming the reward is greater than the cost to operate). A computer whose earnings are being stolen by a botnet will be more noticeable to its owner than is the case today, hence we might expect that in that world, users will work harder to maintain their computers and clean them of botnet infestations.

Countermeasures by botnet operators would include moderating their take, perhaps only stealing 10% of the productive capacity of invaded computers, so that their owners would be unlikely to notice. This kind of thinking quickly degenerates into unreliable speculation, but it points out the difficulties of analysing the full ramifications of a world where POW tokens are valuable.

Hal Finney


### Bill Frantz frantz@pwpconsult.com (Sat Jan 24 18:22:21 EST 2009)

Hal Finney:
> Countermeasures by botnet operators would include moderating their take, perhaps only stealing 10% of the productive capacity of invaded computers, so that their owners would be unlikely to notice. This kind of thinking quickly degenerates into unreliable speculation, but it points out the difficulties of analyzing the full ramifications of a world where POW tokens are valuable.

Some people tell me that the 0wned machines are among the most secure on the network because botnet operators work hard to keep others from compromising "their" machines. I could see the operators moving toward being legitimate security firms, protecting computers against compromise in exchange for some of the proof of work (POW) money.

Cheers - Bill


### dan at geer.org dan@geer.org (Sat Jan 24 23:07:17 EST 2009)

Bill Frantz:
> Some people tell me that the 0wned machines are among the most secure on the network because botnet operators work hard to keep others from compromising "their" machines. I could see the operators moving toward being legitimate security firms, protecting computers against compromise in exchange for some of the proof of work (POW) money.

I'm one of those people.  Quoting from my speech of 1/20:

> Virus attacks have, of course, become rarer over time, which is to say that where infectious agents once ruled, today it is parasites.  Parasites have no reason to kill their hosts -- on the contrary they want their hosts to survive well enough to feed the parasite.  A parasite will generally not care to be all that visible, either.  The difference between parasitism and symbiosis can be a close call in some settings, and of the folks who famously bragged of being able to take the Internet down in twenty minutes, one has said that a computer may be better managed once it is in a botnet than before since the bot-master will be serious about closing the machine up tight against further penetration and similarly serious about patch management.  Therefore, since one can then say that both the machine's nominal owner and the bot master are mutually helped, what we see is evolution from parasite to symbiont in action. According to Margulis and Sagan, "Life did not take over the globe by combat, but by networking."  On this basis and others, bot-nets are a life form.

Rest of text upon request.  Incidentally, I *highly* recommend Daniel Suarez's _Daemon_; trust me as to its relevance.  Try this for a non-fiction taste:

[http://fora.tv/2008/08/08/Daniel_Suarez_Daemon_Bot-Mediated_Reality](http://fora.tv/2008/08/08/Daniel_Suarez_Daemon_Bot-Mediated_Reality)

--dan


### Satoshi Nakamoto satoshi@vistomail.com (Sun Jan 25 10:47:10 EST 2009)

Hal Finney:
> Jonathan Thornburg:
> > - Spammer botnets could burn through pay-per-send email filters trivially
> If POW tokens do become useful, and especially if they become money, machines will no longer sit idle. Users will expect their computers to be earning them money (assuming the reward is greater than the cost to operate). A computer whose earnings are being stolen by a botnet will be more noticeable to its owner than is the case today, hence we might expect that in that world, users will work harder to maintain their computers and clean them of botnet infestations.

Another factor that would mitigate spam if POW tokens have value: there would be a profit motive for people to set up massive quantities of fake e-mail accounts to harvest POW tokens from spam.  They'd essentially be reverse-spamming the spammers with automated mailboxes that collect their POW and don't read the message.  The ratio of fake mailboxes to real people could become too high for spam to be cost effective. 

The process has the potential to establish the POW token's value in the first place, since spammers that don't have a botnet could buy tokens from harvesters.  While the buying back would temporarily let more spam through, it would only hasten the self-defeating cycle leading to too many harvesters exploiting the spammers.

Interestingly, one of the e-gold systems already has a form of spam called "dusting".  Spammers send a tiny amount of gold dust in order to put a spam message in the transaction's comment field.  If the system let users configure the minimum payment they're willing to receive, or at least the minimum that can have a message with it, users could set how much they're willing to get paid to receive spam.

Satoshi Nakamoto


### John Gilmore gnu@toad.com (Sun Jan 25 17:40:45 EST 2009)

> Note: John Gilmore starts discussion "Proof of Work -> atmospheric carbon" about the energy consumption of PoW, which won't be included in this compilation)

Hal Finney:
> If POW tokens do become useful, and especially if they become money, machines will no longer sit idle. Users will expect their computers to be earning them money (assuming the reward is greater than the cost to operate).

Computers are already designed to consume much less electricity when idle than when running full tilt.  This trend will continue and extend; some modern chips throttle down to zero MHz and virtually zero watts at idle, waking automatically at the next interrupt.

The last thing we need is to deploy a system designed to burn all available cycles, consuming electricity and generating carbon dioxide, all over the Internet, in order to produce small amounts of bitbux to get emails or spams through.

Can't we just convert actual money in a bank account into bitbux -- cheaply and without a carbon tax?  Please?

John


### Hal Finney hal@finney.org (Tue Jan 27 14:35:43 EST 2009)

John Gilmore:
> The last thing we need is to deploy a system designed to burn all available cycles, consuming electricity and generating carbon dioxide, all over the Internet, in order to produce small amounts of bitbux to get emails or spams through.

It's interesting to consider the ultimate technological resolution to this issue. Will a global-scale proof-of-work based system inherently consume substantial amounts of energy? Or are there ways of doing computing which would allow such a system to use only moderate energy consumption?

This question relates to the thermodynamics of computation. It has long been known that logically reversible transformations can be done with arbitrarily low energy dissipation. Hence attention is focused on irreversible transformations, particularly those that require bit erasure. Erasing a bit dissipates approximately energy of approximately kT where k is Boltzmann's constant and T is temperature.

The question is whether a POW system inherently involves a great deal of irreversible logical transitions, causing bit erasure and dissipating energy? Or could a POW token be created using solely reversible logic?

One note is that any algorithm can in principle be made reversible except for the size of the output: compute it using reversible logic, possibly creating many excess bits which will allow the reversal, until we get the answer; then make a copy of the output; then reverse the calculation, consuming all the excess bits until we get back to the original value. The only irreversible step was saving the output. However this is impractical for large calculations like we are talking about, because the number of excess bits would dwarf the size of the calculation.

The hash collisions used in systems like Bitcoin or Hashcash (technically not collisions, rather searches for pre-images of hash values with many leading zero bits) seem inherently irreversible. The algorithm typically sets up a pre-image that includes a counter value, computes the hash, increments the counter and repeats until a hash is found with the desired properties. The hash function itself typically uses many intrinsically irreversible transitions, since logical irreversibility is a defining requirement of a hash function. Even if we use the trick in the preceding paragraph to eliminate the cost of the intermediate steps in computing the hash, we would still need to erase the output result each iteration, dissipating energy. Typical POW systems in use today require millions to billions of iterations, and this would be likely to increase in the future, so the dissipation could be substantial.

Replacing the hash with a logically invertible function might help to reduce the number of intermediate bits, and eliminate the need to use the run-backwards trick. One would require that both the pre-image and the post-image contain a number of bits in fixed positions. However this would still seem to require the same kind of search algorithm, causing dissipation as each intermediate result is erased.

Perhaps a variation on this idea would work, if the logically invertible function was itself very slow, perhaps paramaterized to have a huge number of rounds. Then only a relatively small number of iterations would be needed before a lucky result is found, for a given level of POW effort. This would reduce dissipation. However it would slow down verification, and since verification of the POW will be done far more often than creation, we can't afford to tip things too far in that direction.

Another idea I had was to use a deterministic POW rather than a random one like hash collision. Cryptographic work on "timed commitments" and related topics has shown that repeated squarings modulo an unknown RSA modulus allow for a relatively concise and quickly verifiable proofs that some very large number of squarings had taken place, with no shortcuts possible for the creation of the resulting certification. Broadly speaking, modular squaring is logically reversible, in that one could theoretically compute the square root. But in practice, as with the hash computation, computing a modular square using logically reversible operations will produce a large number of excess bits. Even if the excess from a single squaring could be consumed using the trick mentioned above, one would still be forced to erase the temporarily result of each individual squaring operation, as the POW would require a very large number of squarings.  So the overall dissipation would appear to be similar to the hash computation.

(Also, it's not clear that a deterministic POW works well for an application like Bitcoin; it might let the owner of the fastest computer win every POW race, giving him too much power.)

So the question from John's challenge remains open: is there a POW system which could be built solely on logically reversible computation? The computation has to be intrinsically time consuming, but with a short and quickly verifiable certificate of validity.

Hal Finney


## P2P foundation


### Satoshi Nakamoto (February 11, 2009, 22:27)

**Bitcoin open source implementation of P2P currency**

I've developed a new open source P2P e-cash system called Bitcoin. It's completely decentralized, with no central server or trusted parties, because everything is based on crypto proof instead of trust. Give it a try, or take a look at the screenshots and design paper:

Download Bitcoin v0.1 at [http://www.bitcoin.org](http://www.bitcoin.org)

The root problem with conventional currency is all the trust that's required to make it work. The central bank must be trusted not to debase the currency, but the history of fiat currencies is full of breaches of that trust. Banks must be trusted to hold our money and transfer it electronically, but they lend it out in waves of credit bubbles with barely a fraction in reserve. We have to trust them with our privacy, trust them not to let identity thieves drain our accounts. Their massive overhead costs make micropayments impossible.

A generation ago, multi-user time-sharing computer systems had a similar problem. Before strong encryption, users had to rely on password protection to secure their files, placing trust in the system administrator to keep their information private. Privacy could always be overridden by the admin based on his judgment call weighing the principle of privacy against other concerns, or at the behest of his superiors. Then strong encryption became available to the masses, and trust was no longer required. Data could be secured in a way that was physically impossible for others to access, no matter for what reason, no matter how good the excuse, no matter what.

It's time we had the same thing for money. With e-currency based on cryptographic proof, without the need to trust a third party middleman, money can be secure and transactions effortless.

One of the fundamental building blocks for such a system is digital signatures. A digital coin contains the public key of its owner. To transfer it, the owner signs the coin together with the public key of the next owner. Anyone can check the signatures to verify the chain of ownership. It works well to secure ownership, but leaves one big problem unsolved: double-spending. Any owner could try to re-spend an already spent coin by signing it again to another owner. The usual solution is for a trusted company with a central database to check for double-spending, but that just gets back to the trust model. In its central position, the company can override the users, and the fees needed to support the company make micropayments impractical.

Bitcoin's solution is to use a peer-to-peer network to check for double-spending. In a nutshell, the network works like a distributed timestamp server, stamping the first transaction to spend a coin. It takes advantage of the nature of information being easy to spread but hard to stifle. For details on how it works, see the design paper at http://www.bitcoin.org/bitcoin.pdf

The result is a distributed system with no single point of failure. Users hold the crypto keys to their own money and transact directly with each other, with the help of the P2P network to check for double-spending.

Satoshi Nakamoto

[http://www.bitcoin.org](http://www.bitcoin.org)


### Sepp Hasslberger (February 12, 2009, 14:44)

Great stuff.

This is the first real innovation in money since the Bank of England started to issue its promissory notes for gold in the vaults, which then became known as banknotes.

I believe an open source currency has great potential. A bit like Google becoming the default search engine for many of us.


### Sepp Hasslberger (February 14, 2009, 15:30)

[Dante](http://p2pfoundation.ning.com/profile/DanteGabryellMonson), in an email, has mentioned a UK project called Open Coin. It seems to go in a similar direction.

Could there be synergies with bitcoin?

[http://opencoin.org/](http://opencoin.org/)


### Satoshi Nakamoto (February 15, 2009, 16:42)

Could be. They're talking about the old Chaumian central mint stuff, but maybe only because that was the only thing available. Maybe they would be interested in going in a new direction.

A lot of people automatically dismiss e-currency as a lost cause because of all the companies that failed since the 1990's. I hope it's obvious it was only the centrally controlled nature of those systems that doomed them. I think this is the first time we're trying a decentralized, non-trust-based system.


### Joerg Baach (February 17, 2009, 10:42)

Hi Satoshi,

we are actually really talking about the old Chaumian central stuff. That was because a) it was there b) it was patent free (we have to think a bit about the US). I had a read of your paper on the weekend - thanks a lot for doing that work. Interesting read.

What I did not understand about your system - how would you use it for a currency of any sort? Everybody can create a coin as they like, as far as I understood, so therefore there is no trusted supply of tokens / coins.
Or the other way around: if you don't trust the double spending database, because its a central instance, you surely couldn't trust a central issuer to issue and redeem. How would a currency work otherwise? Would you use it for a mutual credit system in which the transactions are shown online?

Cheers,

Joerg


### Sepp Hasslberger (February 18, 2009, 14:41)

I have two questions, Satoshi.

the first one ties in with Joerg's doubts about the trusted supply of tokens/coins.

As far as I understand, there will be a limit of the total amount of tokens that can be created, and a changing gradient of difficulty in making the tokens, where the elaboration gets more and more difficult with time. Is that correct?

It is important that there be a limit in the amount of tokens/coins. But it is also important that this limit be adjustable to take account of how many people adopt the system. If the number of users changes with time, it will also be necessary to change the total amount of coins.

Is there a formula to decide on what should be the total amount of tokens, and if so, what is the formula?

If there is no formula, who gets to make that decision and based on what criteria will it be made?

I will keep my second question for later. One thing at a time...


### Satoshi Nakamoto (February 18, 2009, 20:50)

It is a global distributed database, with additions to the database by consent of the majority, based on a set of rules they follow:

- Whenever someone finds proof-of-work to generate a block, they get some new coins
- The proof-of-work difficulty is adjusted every two weeks to target an average of 6 blocks per hour (for the whole network)
- The coins given per block is cut in half every 4 years

You could say coins are issued by the majority. They are issued in a limited, predetermined amount.

As an example, if there are 1000 nodes, and 6 get coins each hour, it would likely take a week before you get anything.

To Sepp's question, indeed there is nobody to act as central bank or federal reserve to adjust the money supply as the population of users grows. That would have required a trusted party to determine the value, because I don't know a way for software to know the real world value of things. If there was some clever way, or if we wanted to trust someone to actively manage the money supply to peg it to something, the rules could have been programmed for that.

In this sense, it's more typical of a precious metal. Instead of the supply changing to keep the value the same, the supply is predetermined and the value changes. As the number of users grows, the value per coin increases. It has the potential for a positive feedback loop; as users increase, the value goes up, which could attract more users to take advantage of the increasing value.


## SourceForge


For more information about this, visit [**sourceforge.net**](https://sourceforge.net/projects/bitcoin/) and [bitcoin.sourceforge forum](http://bitcoin.sourceforge.net/boards/index.php).


## BitcoinTalk


For more information about this, visit [**bitcointalk.org**](https://bitcointalk.org/index.php?action=profile;u=3).


## Others


### Reaction to PC World article about Bitcoin

> Note: The 10/12/2010, PC World published an [article](https://www.pcworld.com/article/499375/could_wikileaks_scandal_lead_to_new_virtual_currency.html) about Wikileaks accepting Bitcoins.

At [bitcointalk.org](https://bitcointalk.org/index.php?topic=2216.msg29280#msg29280), December 11, 2010, 11:39:16 PM

It would have been nice to get this attention in any other context.  WikiLeaks has kicked the hornet's nest, and the swarm is headed towards us.


### Last public message

At [bitcointalk.org](https://bitcointalk.org/index.php?action=profile;u=3;sa=showPosts), December 12, 2010, 06:22:33 PM

There's more work to do on DoS, but I'm doing a quick build of what I have so far in case it's needed, before venturing into more complex ideas.  The build for this is version 0.3.19.

- Added some DoS controls  
As Gavin and I have said clearly before, the software is not at all resistant to DoS attack.  This is one improvement, but there are still more ways to attack than I can count.  

I'm leaving the -limitfreerelay part as a switch for now and it's there if you need it.

- Removed "safe mode" alerts  
"safe mode" alerts was a temporary measure after the 0.3.9 overflow bug.  We can say all we want that users can just run with "-disablesafemode", but it's better just not to have it for the sake of appearances.  It was never intended as a long term feature.  Safe mode can still be triggered by seeing a longer (greater total PoW) invalid block chain.

Builds:  
[http://sourceforge.net/projects/bitcoin/files/Bitcoin/bitcoin-0.3.19/](http://sourceforge.net/projects/bitcoin/files/Bitcoin/bitcoin-0.3.19/)


### Last private message

From: Satoshi Nakamote <satoshin@gmx.com>  
Date: Sat, Apr 23, 2011 at 3:40 PM  
To: Mike Hearn <mike@plan99.net>  
Subject: Re: Holding coins in an unspendable state for a rolling time window  

Mike Hearn:
> I had a few other things on my mind (as always). One is, are you planning on rejoining the community at some point (eg for code reviews), or is your plan to permanently step back from the limelight?

I've moved on to other things.  It's in good hands with Gavin and everyone.
 
I do hope your BitcoinJ continues to be developed into an alternative client.  It gives Java devs something to work on, and it's easier with a simpler foundation that doesn't have to do everything.  It'll get critical mass when impatient new users can get started using it while the other one is still downloading the block chain.
