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
