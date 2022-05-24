# monero-gpg
Sign a message/file with GPG and include the current Monero block stats at the bottom.

A cool by-product of Proof of Work is that you can use block hashes as a sort of `time-minimum`. If you include a block's hash in a message, that message at the bare minimum was created when that block was first relayed to the network. In order to fake a message for the future, you'd have to know every block hash leading up to that block, all of which include its own RandomX hash, and all the transactions.

## usage
```bash
./monero-gpg <your_file> [monero-rpc ip]
```
* If the file is a text file, the raw text will be signed
* If the file is something else, the `sha256` hash of the file will be signed
* The default ip is `localhost:18081` (your own monero node)
* Place `monero-gpg` in `/usr/local/bin` or `/usr/bin` to execute `monero-gpg` anywhere

The Monero block info attached:
```
=== monero info ===
[ height ] <height>   # height of most recent block
[  time  ] <time>     # timestamp of block (always UTC)
[  hash  ] <hash>     # overall hash of block (not PoW hash)
```

## example
Text file:
```c
-----BEGIN PGP SIGNED MESSAGE-----
Hash: SHA256

#include <stdio.h>

int main(){
	printf("this is some C code written by me, hinto\n");
	return 0;
}

=== monero info ===
[ height ] 2630604
[  time  ] Tue May 24 05:37:06 PM UTC 2022
[  hash  ] 37dd5b1a6a50b29a3e018280a6cc7ece40b9228d6cc2d917aa092711760921c2
-----BEGIN PGP SIGNATURE-----

iQIzBAEBCAAdFiEEIZWO6UWYAoL8uEnI10g/bKJ9Gx0FAmKNGDwACgkQ10g/bKJ9
Gx0A7RAAoW3/8SfiZO+FoSPJBQ7S5zDQAm/GKLw252lgY/MiDAHmKIPF5dMUK/VA
/UkHFWLpQvl5QFNVGyCpqx/tpvUKefX2FoBkyal4q9mwPIK+4usWo7xU0QBryl/J
+YiHnfEMHN8pSXyD6QXG35XFJqWCGqqotyPBXQwp9RdL90seIpVDYNnDhqEqtOyZ
WDgbHY7+usYFZuSL2V8NjtF/b6mVP64wqzb0xq4OPeEohOKRSTgYJDOU6qDwfeAQ
pm/oGdb4NF7bubrz7Rab5x93tFk+4JdDhekfeuiZt2QY/g+42nraALdKjKIqhTY5
sVG14T3XTVEdBO/AvUHl8tXoym5G8rRUANzuYE03a/GpUVV2GmxymerTi6xXs/zK
o39XyKUCmnK1BY7Uj7VXaOGpebAIpetMoDo7w7pDvsTLkyweLGR72mtqPaZnUYYt
Bury0pLZDdNUKYe3VwMpoDiN5lhEXAMDkqy174rtbfbVTkP4O0sXM/1NIN+tDBRl
g2h93gzoa8BKBhkgHe8qajNOvsZmQIDqLVFlC2+H4owEmgrsLWadUrh5/hY0+c36
ayTB8XPUzAjzn/SWbJqJufWy4PpYV2hPTy4HPnCsifEzko6ZnHC6Us162DuEP61G
/ekxjSUwaIL81oCgQy/YAG0fNL5rwE9XacTAlP1Xb6vTGALVGlM=
=RYaN
-----END PGP SIGNATURE-----
```
Non-text file:
```
-----BEGIN PGP SIGNED MESSAGE-----
Hash: SHA256

2c0a609d667cb1978f318a4b4fadc57f3dae44aaddac01fe00e5236b2d003eb3  example.binary

=== monero info ===
[ height ] 2630604
[  time  ] Tue May 24 05:37:06 PM UTC 2022
[  hash  ] 37dd5b1a6a50b29a3e018280a6cc7ece40b9228d6cc2d917aa092711760921c2
-----BEGIN PGP SIGNATURE-----

iQIzBAEBCAAdFiEEIZWO6UWYAoL8uEnI10g/bKJ9Gx0FAmKNGD8ACgkQ10g/bKJ9
Gx3s/A//fQM6VJUYz47XwfR8n9PEsoF/HjIZyM+XP3TFM6Zvrti8fc7eeUE10OI3
Ltv9WHP0aSQ0tN8EoaXvqAHO18739GZxRjFiqIgfLxozAWfgs9kZUmrAeGfxocVr
Twbm4u7ObbNce6P9R5q3b2OmbhwzVt8iD1hyfzCNzMViOf7gue4FCZb4SuceJ6xA
fSfkWVR1cdj7Mz1MwAVn9lPpS66VzurYMzZqqMVemEZuqkTR2VZo8meNGHFWiONv
dfQRVrx/DY65oFbKf4LcCphx8CYICcyXfKJubsuwAFxFQccxBk9G4A+fs3rrz323
v/qh8VhYFmTTlIAIsf7PnLzKlk6UR7fT7Td/V64LEP0xYrMZAUfCHLtflMVh8iHv
TDo7scfoceBQhhMlRrO70DbzGLwOZcvBRIL5V8/jJ0dPZqBCHPeyMJ8XxJQhI+fM
gk2OJ5onslq5+beoBM1Jg95VYesNLiftYkopck4HNv8jseAr3B6E3bmGgMjDpOMY
w8pYE5PiAQmn6rCIgQ5sKx+rNOoiMx9z6eNtIBn7zeBSoR4lO9B/kBN9zU7im5Ag
5qUPgI47Z0dfKb8f8UurACeNlOQchILtRErOs1BmfVlSOUOUK1O1FTZt/ENN+ZEL
KaFyrbZIRDwfhDRyhige6OeXyYq3cT10zAEr9rK3ip5f3AAAwMI=
=E9DQ
-----END PGP SIGNATURE-----
```
