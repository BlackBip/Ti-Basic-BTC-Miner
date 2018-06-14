# Ti-Basic Bitcoin Miner
A bitcoin miner for Texas Instruments calculators (Ti-83 Premium CE/TI-84 Plus CE) fully written in Ti-Basic. It should work on other TI calculators, but I can't check that since I don't have any other. It was written on a Ti-83 Premium CE (french model of the TI-84 Plus CE), OS version 5.2.0. It can't actually generate any bitcoins since it's well too slow to mine of the actual blockchain - it uses old blocks that you can find on https://blockchain.info/.

## Hashrate
TBD

## How to use
Download Ti-Connect to transfer the files to your calculator.
Enter your block version/prev_block/merkle_root/time/bits/nonce in Str5/Str6/Str7/Str8/Str9/Str0 in BTCINIT.
Start BTCMINE and wait for arround 4 hours. Your block hash will be displayed and it will tell you if your nonce is or isn't correct.

## How does it works
Since I can't put any comments in Ti-Basic, here is a summary :

- **BTMINE** : Takes BTCINIT's block informations and generate the block hash.
It uses :
- **BTCINIT** : Sets some constants, like the block's informations and BCHANGE key.
- **BTCCONST** : Sets SHA-256 constants in L6.
- **BTCSTEP1** : Puts the block's informations in decimal in L1 and preprocess them.
- **BTCSTEP2** : Generates the W(j) list of L1 (W(1)-W(16) are L1(1+16.E)-L1(1+16.E)) in L2.
- **BTCSTEP3** : SHA-256 compression function of L2. Output in L6(1)-L6(8) (where the constants were for the second round).
- **BTCSTEP4** : Moves the hash of the block from L6(1)-L6(8) to L1(1)-L1(8) and preprocess them.
- **BTCSTEP5** : Generates the final hash, diplay it and tell if the nonce was or wansn't correct.
And those use : 
- **BCHANGE** : Changes the base of Str0 (initial base : A | new base : B) - supports bases 2,10,16 (and 36 as input)
- **CHOOSE** : SHA-256 Choose function (inputs : S,T,U | output : V)
- **MAJORITY** : SHA-256 Majority function (inputs : S,T,U | output : V)
- **SIGMA0** : SHA-256 SIGMA_0 function (input : S | output : V)
- **SIGMA1** : SHA-256 SIGMA_1 function (input : S | output : V)
- **GAMMA0** : SHA-256 GAMMA_0 function (input : S | output : V)
- **GAMMA1** : SHA-256 GAMMA_1 function (input : S | output : V)
- **ROTATE** : Bitwise right rotate through carry function (input : S,T | output : Str0 in binary)

If that doesn't make any sense to you :
- **SHA-256 white paper** : http://www.iwar.org.uk/comsec/resources/cipher/sha256-384-512.pdf
- **A good youtube video on that subject** : https://www.youtube.com/watch?v=UZBZPOEVyJA

## In the future
I don't plan to make a lot of changes to this project, it was done in 2 days to prove how slow those calculators are. It is actually pretty amazing that they can actually do all of this stuff in some sense - and you can do it with 10 strings. I could optimise it a little more, make a loop that will try increase the nonce until the block is solved, but it is well too slow anyway. I know that it would be faster if it was written in C and then compiled in ASM, but that wasn't the point : I did everything directly on the calculator, without tranfering anything from my computer to my calculator, and I can't code in C on my calculator. I ended up learning a lot a things so it wasn't lost time it the end.

## How you can help
If you are better than me in english and see any mistakes, fell free to contact me, that's not my native language.
IF you have a better calculator (like a TI-Nspire) or an older one (like a Ti-82 Plus) that can run this code, please send me the time that BTCMINE took to run so I can write here.
If you want to improve it, feel free to create a new branch or to ask for commit right.
