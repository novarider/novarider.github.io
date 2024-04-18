---
title: "Rediscovered my GPG Key"
date: 2024-04-15T20:36:33+01:00
draft: false
---

After some task at work I remembered that I once created a GPG Key during a information security class.
So I started to search for it and found it on my old windows machine with this command

```bash
gpg --list-keys
```

So I wondered if I can export this key and reuse it. Google as always had an answer for me!

Private GPG Keys are protected by a passphrase which is choosen when generating a keypair. By this mechanism
the private key file can be savely moved from one machine to another, because before a useage you need to know the
passphrase!

**This is for sure not best practice because the file is not protected against bruteforce attacks!**

But for moderate security I think it's just fine. To export the key to a ASCII encoded format I used

```bash
gpg --armor --export <email-id-of-key> > public.asc
```

After that I could just copy the key from my old machine to current one and import it to the keyring with

```bash
gpg --import public.asc
```

I then noticed that I used an outdated comment in my key's uid. So I was curious if I could change this...
And yes this is also possible via the --edit-key option.

```bash
gpg --edit-key <key-hash>

gpg> adduid
[Follow prompts]

gpg> uid
[List of all uids with their ids]
gpg> uid <id-of-outdated-uid>
gpg> deluid <id-of-outdated-uid>
```

After that I had my old, but now polished key in my keyring and can use it again.

So if you want to send me an encrypted email feel free to use my public key

```
-----BEGIN PGP PUBLIC KEY BLOCK-----

mQENBFcnn2UBCADLnpard2xCRqyULt6ajKM3EyjzxDXb1JkPRuWHo1j1i+AfFhzG
USxgClwm90ZVXDq3ixO1KHwF012PcGZU2y9/rr7RRaBQfN3fIi2Fc/2F5CNkJTWj
Qie9Sx4tRrX4GccNmOGx3kcX0kbb04+WQLQOV0NLz7hLljrMEFdJ6ljo6ovSAOkd
H5axWGwJq2JINbwnox8S4GixT0Sk3Y/DGsD6n6+CEVVHaV/F/6b3i5dZsDGfgIhA
t0AD9rP18qb5aeGLJrPpF+N52PYP2iTJCIBIqgIoLuBMs5nt2TrYE7WBhonvVIGd
t4cJlD3ru9ChoBWHs4jaoqnFCIVAOc5fFxW9ABEBAAG0N1BhdHJpY2sgUnVkaWdp
ZXIgKFByaXZhdGUgS2V5KSA8cGF0LnJ1ZGlnaWVyQGdtYWlsLmNvbT6JAU4EEwEK
ADgWIQSp+5kWtfepz82yYskjfvnN56f4YAUCZiFlIQIbAwULCQgHAgYVCgkICwIE
FgIDAQIeAQIXgAAKCRAjfvnN56f4YLr3B/9EwlZvciAg2EBsg0tfil0YINY4Ki3K
/Pv2Ny2Tpco7ceRZs3nDYoFHEZBUf01/YzrunNxELW8wLb9PjHaDIYjhWmVdZR3t
vbvqPANmxUZYVEXyCUpDWZHol8NVMLsVAwWljTGB9OJNL027ubCPN5VLL1xRjuws
h9kqbUR4u3HPE60/xCexnggJ25uxTsxydFGRyeaXudcmF8lq6EYuu9RD14MMXedz
Qndvr9bzYINGNf0ueI4nWrfrYw2SYyKUvu0GFmMT4pOBM96eX986FBLfFJNaB62M
vOATzjCXoVTDGDuBPohprEp0e/r1a22FJrL2zy45rvexNGw3G8pxgV8WuQENBFcn
n2UBCAC3p4zzH6P+KTUme98XV6B90v9kODX0loHbeyc6SttVbFT9hjtdzIsMYvSZ
f50ev+SR2foPLW53wDrtJScyqy2q3XFymncuRJXAGrjIRnaGhrchO8tPSUhRXxHX
ZFAymvpaxR5x2l6l7XNoLaG6rhqMqUN2wavJTPHTcm/GXrJ9TNmrZPrVAGGF3xSE
MJUnKCZMd1YNV/X3DN2PrNTsOr+qTcy9kKLP7/btc0g6TS42tr5TIfyOn63FuBuC
AP+yAYEqxaAx5U1FkuQNj+SQ6Lw+zR0+alLrbbO4RZ3aSiUFZxQkGNBFMwZqUhbm
DJyi+wgydEzn7gDppGgLkaUFe1V/ABEBAAGJAR8EGAEIAAkFAlcnn2UCGwwACgkQ
I375zeen+GDxqgf7BPMTFg7DQjlZpfIqXW2Y8I/dW/F46TVYQQOBWV+rwllbeUCA
2to1ngNCKyOqoXx/NC0MU3A7g0jEgKCBHtSuMYT9B8hm8RI6tfK0QIl5JYWjdDb8
GT24N1DW8neCh8iQXStqcRbsSMrsIQawll3jpnKR5AjCYwS042SqJ9FuLGXzf0mB
BxNUPHoDgTw2tQ4qPnzH9IOEyy1F0hbWVFhwO6PCjacMuzSmj6ZF6H7GXbc3BROf
njs1PBEuxgG4EtKCqGMy9LVOpbPgHM/Kiah8ElsyLlZpVkO70+K5mLvn2z7oQ6Kz
5Qs+1gaAY5y8NsaPPsELAZaKzJcCzkqbw73mZw==
=t944
-----END PGP PUBLIC KEY BLOCK-----
```