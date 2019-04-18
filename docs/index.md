# ![Strongman](img/favicon-32x32.png) Strongman
Free Open Source Online Password Manager

---

## Overview

Strongman is a **free open-source online password manager** written in javascript with a touch of php. 

**Strongman has two basic modes of functionality:**

1. It uses a master password combined with the username and domain to create "computed" passwords (similar to [lesspass]). In this mode, only a "password profile" is stored on the server. The site password itself is not stored.
2. It can use the master password to encrypt (AES-256) "custom" passwords and "secure notes," which are then stored on a web server.

The emphasis is on **speed**, [**security**](#strongman-security), and **simplicity**. [Open Strongman Password Manager]

## Features

- Strongman is completely free and open source. 
- [Diceware](#diceware-passwords) master passphrases are strongly recommended, and in fact **must be used** unless overridden by a setting.
- It provides both lesspass-style computed passwords as well as AES-256-encrypted "custom" passwords.
- Strongman does all password computations as well as AES-256 encryption/decryption of custom passwords **in your browser**. Your master password is never transmitted to the server.
- Being an online service, Strongman is available from all your Internet-connected devices. There is no need to synchronize password databases among devices.
- Like all good security software, the source code is available for inspection! ([github repository])
- Strongman does not require signup or login. Since there is no session, it is *stateless*, adding greatly to its security.  You need only enter your master password, which never leaves your browser page (examine the source code if you want to confirm that).
- Strongman is extremely simple and fast to use.  It aims to put your password into the computer clipboard **with as few clicks as possible.** It doesn't fill any web forms for you, to avoid security risks.
- The app is mobile-adaptive for use on cell phones and the like. Later, with help from the Github community, I may add a native Android app.
- The truly paranoid who cannot audit the source code can **turn off online mode** after the Strongman app is loaded.  In offline mode, stored password profiles and encrypted passwords are unavailable, but computed passwords will work fine.

## Why I Created Strongman

There are many password managers.  Why did I invent a new one?

In the first place, I became convinced that for proper security for online accounts, **everyone should use a password manager**. But I couldn't fully trust a program that wasn't open source, which ruled out all the commercial ones I knew about.  Also, I wanted to be able to host it on my own server. That greatly reduced my options. I also wanted great speed and ease of use.

I found [lesspass], which is open source and can be self-hosted.  It nearly filled my needs, except migrating to it would mean I would have to change all my site passwords.  Furthermore, there's no way to change the master password without changing **all the website passwords it generates.**

So I set out to build my ideal password manager.  Essentially I adopted the extremely secure computed passwords of lesspass, but *added* the ability to use AES-256 encryption for "custom" passwords and "secure notes."  This way, one can optionally store *any* password one wants.  This also allowed me to add the ability to **change the master password.**

!!! Note
    When changing a master password in Strongman, all the computed passwords associated with the old master password are converted to AES-256 encrypted passwords using the new master password.

## Installation

Installation is not necessary for most users, since the Strongman project hosts the web app for free public access: [https://strongman.tech/app].

If you wish to run the web app on your own server, or to help with development, download the project from the [github repository].  Upload the "app" directory to any location accessible to your php7.1+-enabled web server. Make sure the "data-source" directory is writable by your web server user.  You should also be sure that the site can't be accessed by both the base domain and the www subdomain, so that cookies can work properly.  That's it.  There's no database. Account information is stored in files, one file per master password.

[https://strongman.tech/app]: https://strongman.tech/app
[github repository]: https://github.com/lstandish/strongman
[lesspass]: https://lesspass.com
[security analysis]: https://www.usenix.org/node/184484
[Open Strongman Password Manager]: https://strongman.tech/app/index.php
[Diceware information]: https://theintercept.com/2015/03/26/passphrases-can-memorize-attackers-cant-guess/

## Strongman Security

#### __Security Overview__

According to a [security analysis] presented at the 23rd Usenix Security Symposium in 2014, 80% of the web-based password managers tested were insecure. Strongman should be immune to the cited vulnerabilities due to its *statelessness* as well as the lack of vulnerable features such as bookmarklets, one-time passwords, and shared passwords. I invite others to perform a security audit for Strongman.

#### __Computed Passwords__

Strongman allows lesspass-style computed passwords, which does not involve storing the password at all.  The password is "recalculated" from the master password, domain name, username, and password options, such as length and character sets. For these computed passwords, only a "profile" is stored. Here is an example "profile" entry from my own Strongman account. (I have modified the email address.)

```
[vitacost.com]
myemail@example.com = 7,14,1,,0,1542057929
```

In this case, **vitacost.com** is the domain name, and **myemail@example.com** is the username. The other profile information is:

```no-highlight
7: bitfield-encoded character set. "7" means use upper/lowercase letters and numbers, but no special characters.  
14: password length  
1: password sequence number (This is incremented to create a new computed password.)  
empty: encrypted secure notes (none in this case)
0: Password category number
1542057929: timestamp to keep track of password age
```
 
In sum, computed passwords involve no password storage whatsoever.  However, they are very inflexible.  Computed passwords cannot be modified by the user other than specifying the character set and length.  So if you already have some secure passwords that you'd like to keep using with Strongman, computed passwords are not a solution. Plus, as explained in [Why I Created Strongman](#why-i-created-strongman), the master password cannot be changed without changing all the computed passwords.

To solve this problem, Strongman allows storing AES-encrypted passwords and notes, described in the next section.

#### __AES-Encrypted Passwords and Notes__

Whenever you need to store a *particular* password (rather than use a computed one) you click the "Save" button in Strongman. That causes the password to be encrypted (by the webpage, using javascript) and then sent to the server for storage.  This is military-grade encryption, and in my opinion is every bit as secure as the computed passwords. When using encrypted passwords, Strongman remains *stateless*. Futhermore, the AES-encryption takes place in the browser, before being transmitted to the server for storage.

In addition to encrypted passwords, Strongman offers encrypted *secure notes*.  This allows you to add any sort of information to either a computed or an encrypted password entry.

Here's an example of an encrypted password entry from my own Strongman account:

```bash
[wimaxcr.com]
invoice@ = 15,14,1,fc430283546cf012faf69539a13c5bd4,0,cb4c00b93772d665d6e8f8158f09779f,1539199590
```
Here, **wimaxcr.com** is the domain name, and **invoice@** is the username. The other profile information is:

```
15: character sets (ignored)  
14: password length (ignored)  
1: password sequence number (ignored)  
fc430283546cf012faf69539a13c5bd4: AES-256 encrypted note  
0: Password category number
cb4c00b93772d665d6e8f8158f09779f: AES-256 encrypted password  
1539199590: timestamp to keep track of password age
```

## The Master Password

####__The Password Dilema__

It is surprisingly difficult for a human to choose a strong password.  Humans are not made to think at random; we are creatures of patterns and habits.  On the other hand, random (machine chosen) passwords consisting of letters, numbers, and symbols are hard to memorize.  How would you like to memorize this example 14-character password: wyY#XiQ1h0E/2~?

On the other hand, simply mangling dictionary words to create a password might *look* secure, but it probably isn't.  Here's a [web comic with commentary](https://www.explainxkcd.com/wiki/index.php/936:_Password_Strength) that illustrates that point well. The conclusion drawn by the comic is *"Through 20 years of effort, we've successfully trained everyone to use passwords that are hard for humans to remember, but easy for computers to guess."*

####__Diceware Passwords__

This is where "Diceware" passwords come to the rescue.  It turns out that humans ARE capable of easily memorizing "passphrases" consisting of, say, 7 random *words*, taken from a "Diceware" dictionary of 7,776 words.  This results in a passphrase which is similar in entropy (difficulty to guess) to the 14 character password.  Here is an example 7-word Diceware passphrase: "catalyst sedative certify unused gap dodge alienate".

If you're not completely convinced that a random series of words (Diceware passphrase) is far better than a random or contrived series of characters, please read this [excellent article about Diceware](https://theintercept.com/2015/03/26/passphrases-can-memorize-attackers-cant-guess/).  When you are ready to obtain a Diceware passphrase, take a look at this [excellent online Diceware passphrase generator](https://www.rempe.us/diceware/#eff). In addition to generating passphrases using the browser's built-in random number generator, you can use real dice with it.

As a final note: if a brute force attacker were to obtain a password hash created from a 7-word Diceware passphrase, and if he could muster 1,000,000,000,000 guesses per second (only possible by a nation state player such as the NSA), the average time to guess a 7-word passphrase would be over 27 million years!

Test Line #4.

<!--stackedit_data:
eyJoaXN0b3J5IjpbOTMyMDQyLDIwNzgxNDEzODUsLTEwNjU5ND
czNjYsMjExMjUzMTkzMywtNjQ0MDkyMDM4XX0=
-->