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

## Auditing 

- Different appraoches, some allow auditors to decrypt and the spot and invalidate a vote, others allow voters themselves to verify on the spot and still be protected from coercion. 
- Even with a small number of people committed to verification and auditing, the tally will be accurate. Voter identity is hidden, machine does not know who is voting, thus it does not know when it will be checked so it has to behave honestly during each vote creation.

## Discussion about Threshold Schemes

### Setup with Maths 

- Take some field modulo p, and take all the non-zero elements so that each element can have a multiplicative inverse. 
- We know such a field to be cyclic so we know that it possesses a generator. 
- We choose some value s, s.t. 0<s<p. S is the secret key. 
- Public key is z=g^s. 
	- Makes sense, we are masking the private key be raising g to that power. 

### Encryption and Decryption

- Take message M, 0<=M<p and 0<r<p and obtain (x,y)=(Mz^r, g^r). 
- Decrypt by x/y^s to remove the z^r factor. 
- Cannot be done without the knowledge of the secret key s. 

### Re-encryption 

**This seems like a very important concept in crypto to be fair.** 
- we take r' in 0<r'<p and we compute (x',y') = (xz^r', yg^r'). 
- go back to (x,y) by doing x'/y'^s. 
- Revealing r' to the intruder only lets him verify that (x,y) and (x',y') have the same decryption. Without knowledge of secret key s, no other information is accessible. 
- One can also strategically release r'-r'' to illustrate that (x',y') and (x'',y'') have the same decryption without tying it back to (x,y). **This seems to be very important in the shuffling step and the illustrative proofs.**

### Shamir 

- This guy is a genius. 
- Distributing shares made easier. 
- Each shareholder creates their own secret polynomial and contributes g^cj for each coefficient cj. Then each shareholder gives one point from their poly to every other shareholder (these can be verified by computing g^(P(i)) - easily doable since all the g^cj have been already published.) 
- All these polys are used to create one global poly and then all the shareholders can sum up their points from each poly that they received and this constitutes their share of the overall global poly. Explanation is a bit shady here, but will be better when I summarize the paper fully.  
