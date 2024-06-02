---
layout: "post"
title: "rENTAS CTF"
categories: [rENTAS_CTF]
tags: "RE TI olevba rhysida"
image: /assets/CTF/rENTAS_CTF/logo.jpg
---

## RE/Resign Letter

**Challenge Description:**

![light mode only](/assets/CTF/rENTAS_CTF/RE/chal.png){: .light .w-75 .shadow .rounded-10 w='1212' h='668' }
![dark mode only](/assets/CTF/rENTAS_CTF/RE/chal.png){: .dark .w-75 .shadow .rounded-10 w='1212' h='668' }

**Solution**

In this challenge, we were provided with a Word document. We used `olevba`, a tool commonly used for examining Microsoft Office documents for malicious content. It helps in extracting and analyzing macros embedded in the file.

![light mode only](/assets/CTF/rENTAS_CTF/RE/olevba.jpg){: .light .w-75 .shadow .rounded-10 w='1212' h='668' }
![dark mode only](/assets/CTF/rENTAS_CTF/RE/olevba.jpg){: .dark .w-75 .shadow .rounded-10 w='1212' h='668' }

We discovered an embedded GitHub link and it led us to a repository containing a file named `lenovo.exe`. We downloaded this executable file and used `strings` command to analyze the file.

![light mode only](/assets/CTF/rENTAS_CTF/RE/strings.jpeg){: .light .w-75 .shadow .rounded-10 w='1212' h='668' }
![dark mode only](/assets/CTF/rENTAS_CTF/RE/strings.jpeg){: .dark .w-75 .shadow .rounded-10 w='1212' h='668' }

Among the extracted strings, we discovered a base64 encoded string. After decoding, it revealed the flag.

![light mode only](/assets/CTF/rENTAS_CTF/RE/cyberchef.jpeg){: .light .w-75 .shadow .rounded-10 w='1212' h='668' }
![dark mode only](/assets/CTF/rENTAS_CTF/RE/cyberchef.jpeg){: .dark .w-75 .shadow .rounded-10 w='1212' h='668' }

**Flag**

`RWSC{p@ss123}`


## TI/Скорпион

**Challenge Description:**

![light mode only](/assets/CTF/rENTAS_CTF/TI/chal.png){: .light .w-75 .shadow .rounded-10 w='1212' h='668' }
![dark mode only](/assets/CTF/rENTAS_CTF/TI/chal.png){: .dark .w-75 .shadow .rounded-10 w='1212' h='668' }

We were provided with a text file containing filenames of malicious executables along with their hashes.
```text
Table 2: Malicious Executables Affiliated with xxxxxxx Infections

conhost.exe
6633fa85bb234a75927b23417313e51a4c155e12f71da3959e168851a600b010
A ransomware binary.

psexec.exe
078163d5c16f64caa5a14784323fd51451b8c831c73396b967b4e35e6879937b
A file used to execute a process on a remote or local host.

S_0.bat
1c4978cd5d750a2985da9b58db137fc74d28422f1e087fd77642faa7efe7b597
A batch script likely used to place 1.ps1 on victim systems for ransomware staging purposes [T1059.003].

1.ps1
4e34b9442f825a16d7f6557193426ae7a18899ed46d3b896f6e4357367276183
Identifies an extension block list of files to encrypt and not encrypt.

S_1.bat
97766464d0f2f91b82b557ac656ab82e15cae7896b1d8c98632ca53c15cf06c4
A batch script that copies conhost.exe (the encryption binary) on an imported list of host names within the C:\Windows\Temp directory of each system.

S_2.bat
918784e25bd24192ce4e999538be96898558660659e3c624a5f27857784cd7e1
Executes conhost.exe on compromised victim systems, which encrypts and appends the extension of .groupname(sensored) across the environment.
```

**Solution**

We performed an online search using one of the hashes and confirmed that the hash belonged to `Rhysida Ransomware`. Next, we searched through various platforms to gather more information about Rhysida Ransomware. During our search, we found a crucial clue on a Telegram channel. The clue indicated that the challenge creators preferred using `mirrors` over direct domains.

![light mode only](/assets/CTF/rENTAS_CTF/TI/telegram.jpeg){: .light .w-75 .shadow .rounded-10 w='1212' h='668' }
![dark mode only](/assets/CTF/rENTAS_CTF/TI/telegram.jpeg){: .dark .w-75 .shadow .rounded-10 w='1212' h='668' }

From the clue, we needed to understand what type of mirror was being referenced. The term `mirror` in the context of hacktivists and ransomware typically refers to websites hosted on the dark web, which often use the `.onion` domain suffix. The mention of `mirror not .domain` suggested that we should look for a [non-standard top-level domain](https://medium.com/@bitDomains/what-is-a-non-standard-domain-7ec7d61c38f3), which reinforced the idea that it could be a `.onion` address.

We proceeded to search for mirrors related to Rhysida Ransomware. Our top search result led us to a Twitter post mentioning Rhysida Ransomware.

![light mode only](/assets/CTF/rENTAS_CTF/TI/twitterpost.png){: .light .w-75 .shadow .rounded-10 w='1212' h='668' }
![dark mode only](/assets/CTF/rENTAS_CTF/TI/twitterpost.png){: .dark .w-75 .shadow .rounded-10 w='1212' h='668' }

The Twitter post contained an `.onion` domain. According to the clue, the content before the `.onion` domain in the post constituted the flag

**Flag**

`RWSC{rhysidafc6lm7qa2mkiukbezh7zuth3i4wof4mh2audkymscjm6yegad}`



