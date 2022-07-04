# Browser related privacy issues or cheeky techniques

### Favicon
Set cookies and unique identifiers by setting a series of favicon redirects etc. 0101000, you got it.

### FLoC by Google

Yet another illusion whereas it is claimed that this new way of tracking (rather than cookies) is more private. And of course its bs. Options shouldn't be old tracking (cookies) vs new tracking (FLoC). It should be tracking or no tracking. The way it is presented could be sensed as deceptive on it's own.

### Idle Detection API by Chrome

*Refer to browsers folder.*


# Messaging apps

### Easy to query
- It is just so easy to query certain keywords, terms, meanings in a big data. 

### Honeypot

- Most of these apps that claim to be "private" are just gov honeypots. 

# DNS and TLS

### Goverment owned Certificate Authorities

Some governments are publishing their own certificate authorities. CA (certificate authority) is used in TLS (SSL) and has to be a trusted party. Because if not, it can rather easily access/listen/override data passing through. MItM attacks are common in this case. Some governments known for doing this infamy (Disclamer: this is not government secret, you can easily look em up online.

**Keep in mind: CA can intercept, decrypt, re-encrypt, alter communication bi-directionally. So it can change what you receive (you think you login to facebook but it ain't the Facebook, just a bogus custom version. It's some mirror copy. Or change what you send.**

But worry not it cannot be activated on it's own. For example Russia has announced that citizens should install a government issued CA in order to access internet. They can limit access or deny it all together but can't install it to your computer. 

Firefox and Chrome doesn't allow user's to install any govt issued CA even if they wanted. So far only Microsoft Windows and Edge browser (also some third-party browsers) allow it.

> "you're safe to install the CA cert when you need to use it to connect to any government internet services that require it. When you're done with that interaction, don't uninstall it though... Move it to the "Untrusted Certificate Authorities" category in Windows, or similar in other operating systems, to get a free pop-up alert anytime that CA cert is referenced. Then you'll know the moment that you visit any web site that has already been overtaken by the state."

# Smart Phone

### Forced data extraction
*Sam, are we the baddies ?*
These tools are often used by authorities, but can also be used by general public.
- Grayshift
- Cellebrite
- UFED (Universal forensic extraction device)
- Exploits that use Zero-Day
They allow the user to forcefully extract certain data from the smart phone. Images, messages etc.
Can actually get the data in most cases. IPhone might do a better job at keeping the data encrypted and safe.
- If a device has gone under this process, it is eager that the device has a special data package planted inside. Which allows for geo tracking and more.
- In an emergency, you can maximize the security of your IPhone by pressing the side button 5 times.
- Know your rights, this is a personal device and you cannot be forced into unlocking it. *Uhhh, i think i forgot my pass. Sheeesh !*
- Never use biometric methods for they can kinda force this way to unlock the device.
- Shutdown the damn phone.

#### BFU (Before first unlock)
- As long as the device is not unlocked after cold boot, it is in the most secure state.

#### AFU (After first unlock)
- Far more vulnerable compared to BFU
