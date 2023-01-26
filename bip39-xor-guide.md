## BIP-39 seed XOR pen&paper backup guide

so i decided to make a guide about how to secure bip39 seeds with just pen and paper, no additional devices or software required.

we gonna be using xor cipher, and the following cheat sheet: \
sigle page: https://raw.githubusercontent.com/moonsettler/guides/main/bip39-cheatsheet.pdf \
landscape 3 pages: https://raw.githubusercontent.com/moonsettler/guides/main/bip39_cheatsheet_landscape.pdf \
you may also want to print out this helper page which is mostly a printer friendly HEX XOR table \
XOR table: https://raw.githubusercontent.com/moonsettler/guides/main/xor-table.pdf

it's a pdf file you can print it out, very easy to parse because it's naturally indexed for both alphabetic order and hexadecimal digits.

![FGvO1U_VgBY8c_L](https://user-images.githubusercontent.com/90689674/146413523-780d8d73-dc80-4dd2-a15a-9418f0e4b9e6.jpg)

## step 1:
let's say our seed words are

`crunch village pepper tired cabin bike uphold demand canvas gown cost million`

as in

`1A7, 7A0, 517, 715, 0FE, 0B1, 776, 1D1, 10D, 329, 185, 465`

## step  2:
let's decide the split, like i said earlier n of n and also 2 of n are fairly trivial to make.

we are going to do a 2 of 3 split. that means we will have 3 groups of words where S = A ⊕ B ⊕ C:

`A, B`\
`B, C`\
`A, C`

any 2 of these makes recovery of S possible.

## step 3:
since S = A ⊕ B ⊕ C it's also true, that C = S ⊕ A ⊕ B, and if all words are within the bip39 11 bit word list every bip39 word xor any other word will also be a valid word.

this is what we will use to make our life very easy.

to get A and B we gonna simply generate 2 more seeds (that will never have any balance or used only as decoys)

A: `execute delay bleak deer gym damp loop delay matrix typical ghost auto`

B: `knee agree balcony gap now butter figure column sheriff output portion middle`

## step 4:
to get C, we simply xor up our words for the same positions

A: `279, 1CF, 0BC, 1CA, 340, 1B9, 41F, 1CF, 449, 75F, 30C, 07C`\
B: `3DC, 028, 08E, 2FA, 4B9, 0FA, 2B0, 16E, 62C, 4EB, 542, 462`\
S ⊕ A ⊕ B = C: `002, 647, 525, 425, 707, 1F2, 1D9, 77E, 368, 09D, 7CB, 07B`

## step 5:
now let's look up the words for C!

`able, similar, pigeon, lucky, thought, dinner, depth, used, home, beauty, west, author`

now we have our 3 components for S which are A, B, C

we only need to take a look at step 2 for the groups now!

## step 6:
let's create our recovery sheets! each of them 24 words, but none of them are our valid seed actually.

however we can recover our secret S from any 2 of them! (if i did not mess something up)
![FGvf44wVkAUBd7G](https://user-images.githubusercontent.com/90689674/146414046-1c069644-8266-4da6-b1a9-eadaa8c92803.png)

## advanced - other threshold xor splits (proposed, under review)

### 2 of n (where n:4..6)

`S = A ⊕ B ⊕ C = D ⊕ E ⊕ F`

1. `(A, B, D ⊕ C)`
2. `(B, C, E ⊕ A)`
3. `(C, A, F ⊕ B)`
4. `(D, E, A ⊕ F)`
5. `(E, F, B ⊕ D)`
6. `(F, D, C ⊕ E)`

example 2 of 5:
`(A, B, D ⊕ C), (B, C, E ⊕ A), (C, A, F ⊕ B), (D, E, A ⊕ F), (E, F, B ⊕ D)`

### 3 of 5 by @ZeWiseLib

`S = A ⊕ B ⊕ C ⊕ D ⊕ E ⊕ F`
1. `(A, B, D ⊕ F)`
2. `(B, C, E ⊕ F)`
3. `(C, D, A ⊕ F)`
4. `(D, E, B ⊕ F)`
5. `(E, A, C ⊕ F)`

alternatively:

`S = A ⊕ B ⊕ C ⊕ D ⊕ E = F ⊕ G ⊕ H ⊕ I ⊕ J`
1. `(A, B, F, G)`
2. `(B, C, H, I)`
3. `(C, D, J, F)`
4. `(D, E, G, H)`
5. `(E, A, I, J)`

## notes - on seeds passwords and backups
you can put them on steel, but technically if they are stored at different locations the chances of losing access to 2 of them at the same time are very small.

also i strongly strongly recommend to use a passphrase as well for your wallet creation!

the passphrase should be memorable, should not be written down ever, it should be breakable but only with weeks or months of brute force effort.

this means if the seed entropy survives you, your family can still recover your coins it just gonna take a while...

this accomplishes 2 things:

1 in the event of threshold (in our case 2) number of locations compromised you still have time to use your wallet (or from memory) to move the assets to a new wallet.

2 your coins are very unlikely to be lost forever if you die.

the seeds are mnemonic for a reason btw. try to remember your 12 words!

## xor table - a little help for step4:
to xor 2 hexa numbers you perform the xor by digit
`10D ⊕ 449 ⊕ 62C = 368` because

`1 ⊕ 4 = 5` and then `5 ⊕ 6 = 3`\
`0 ⊕ 4 = 4` and then `4 ⊕ 2 = 6`\
`D ⊕ 9 = 4` and then `4 ⊕ C = 8`


![image](https://user-images.githubusercontent.com/90689674/214966127-10953c64-6001-4154-8a29-8b4084d1b40e.png)

