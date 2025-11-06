# Notes from Benaloh's Simple Verifiable Elections 

## Abstract 

- Most approaches are too sophisticated. 
- Not approachable enough. 

## Phases 

### Phase 1 

- Ballots are cast.
- Encrypted, made public. 

### Phase 2

- Tally is verified. 

## Threshold Encryption 

- Each trustee possesses a portion of a public key. 
- Aggregate public key is produced that encrypts ballots. 
- Ballots can only be decrypted with a threshold number of private key trustee shares. 

## Ballot Tallying 

- We can't allow trustees to decrypt and reveal voter identity. 
- We re-encrypt and shuffle original ballot set. 
- We don't show equivalence through revealing a mapping (bad for privacy). 

### Interactive Proofs 

- Basic concept is that a claim is challenged. 
- Challenger and proover both have same public key. 
- Challenger encrypts with private key and asks proover to produce expected result through decryption. 
- In effect, the key is verified without being revealed. 

### Scheme 

- Take original ballot set B, re-encrypt and shuffle, this produces B'. 
- Do the same for other sets B1, B2,...,Bn. 
- Come up with challenge bits c1,c2,...,cn. 
- For i s.t. ci=0 show that Bi matches B through doing the inverse re-encryption and shuffling operation. - For i s.t. ci=1 show that Bi->B->B'.

**My understanding is not good yet.**

## Attacks Regarding Challenge Bits 

- Simply guess the challenge bits and then make an artificial set of ballots that pass the tests outlined in the challenge bits. Very hard, succeeds only 1/2^n cases. 

### Producing Challenge Bits 

- Take ballot set as input into one-way hash. 
- Output becomes the challenge bits. 
- After seeing the challenge bits, attacker cannot modify the ballot sets to fool the challenger since alteration of the ballot sets will result in another set of challenge bits. 
- Attacker can take n challenge bits (2^n many of them) and for each possible sequence of challenge bits, construct a set of ballots. For large n (n = 100), this would require 2^100 ballot sets, re-encryptions, and shuffles. Not feasible. 

## Shuffling 

- Votes are cast and identifying info is removed. 
- Any party can choose to shuffle this ballet set as long as the newly shuffled set can be linked back to the original. 
- In the case of an invalid shuffle, simply go back to the previous state. 

**Very important to differentiate between ballot creation and casting the ballot into the tally as a legitamate vote.**

## Voter POV 

- Go to polling station, interact with device, and make vote. 
- Receive a card with a magnetic stripe and a crypto thumbprint. Stripe includes the vote, thumbprint can be used by voter later to verify that his vote has been cast. 
- After receiving card, go to the polling station, insure eligibility, and then swipe the card. 
- Now the vote is cast, and the thumbprints are published for independent verification by each voter.  
