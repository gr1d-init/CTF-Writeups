# Github
Here compiles all the challenge related to bruteforing github commit SHA1 hashes

## Goals
1. Some commits are deleted, but it is still hidden on github with original SHA1 key unless the whole repo is deleted and rebuilt.
2. We need to scrape the hidden commit by doing bruteforcing from hex 0000 until ffff to retrieve all the available commit hashes

## Challenges

| Challenges | Category |
| -------- | -------- |
| Garry: Beyond Music's End 3 | OSINT |
| Github is weirdddd 1.0 | Brainfuck |
| Github is weirdddd 2.0 | Brainfuck |

## Solution
@gr1d    wrote a bruteforce tool, [GitSHA](https://github.com/gr1d-init/gitsha), for these challenges.

### Steps
1. Install the tool.
```bash=
git clone https://github.com/gr1d-init/gitsha.git
```

2. Automate bruteforcing with the tool.
```bash=
python gitsha.py -r "<author's name>/<repo's name>"
```

## Final result
1. Garry: Beyond Music's End 3
```
3419
4568 #
66f8
8da4 #
a5b6 #
```
2. Github is weirdddd 1.0 and 2.0
```
0067
0b3d
2a63
458e (GitHub 2.0)
481f
4bec
5b27
5ef6
621e
693a
724c
8f66
a24a
b2ff
c47a
cf29
cfba (GitHub 1.0)
ed44
ed90
f6aa
```
### Flags
| Challenges | Category |
| -------- | -------- |
| Garry: Beyond Music's End 3 | EQCTF{w1z4rd_0f_l3g3nds_1n_d1sgu1s3} |
| Github is weirdddd 1.0 | EQCTF{hmmmmmmmm_G1t_L3ak_d@_Fl3g} |
| Github is weirdddd 2.0 | EQCTF{Brut3333333333_D@_C0mm1t_99} |