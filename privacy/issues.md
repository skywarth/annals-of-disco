# Browser related privacy issues or cheeky techniques

### Favicon
Set cookies and unique identifiers by setting a series of favicon redirects etc. 0101000, you got it.

### FLoC by Google

Yet another illusion whereas it is claimed that this new way of tracking (rather than cookies) is more private. And of course its bs. Options shouldn't be old tracking (cookies) vs new tracking (FLoC). It should be tracking or no tracking. The way it is presented could be sensed as deceptive on it's own.

### Idle Detection API by Chrome

*Refer to browsers folder.*

# DNS and TLS

### Goverment owned Certificate Authorities

Some governments are publishing their own certificate authorities. CA (certificate authority) is used in TLS (SSL) and has to be a trusted party. Because if not, it can rather easily access/listen/override data passing through. MItM attacks are common in this case. Some governments known for doing this infamy (Disclamer: this is not government secret, you can easily look em up online. This document doesn't reveal any sensitive information. Source: https://wiki.mozilla.org/CA:GovernmentCAs and some other)

- Kazakhstan
- Turkey (many which incooperate private companies. )
- Russia (started recently due to the doctrine of close-network)
- France
- Spain
- Netherlands
- Taiwan
- China (CNNIC. many)
- Hong Kong
- Japan
- And some more.

Of course governments don't establish CA just for the sake of accessibility. It's mainly two purposes: to keep encryption standarts and data in-house, and to snoofing/sniffing purposes. So latter allows for spying on the users of the CA, which is citizens.

**Keep in mind: CA can intercept, decrypt, re-encrypt, alter communication bi-directionally. So it can change what you receive (you think you login to facebook but it ain't the Facebook. It's some mirror copy. Or change what you send.**

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

#### AFU (Before first unlock)
- Far more vulnerable compared to BFU
