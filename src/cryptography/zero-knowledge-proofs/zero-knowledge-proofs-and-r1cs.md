# Zero-knowledge Proof Protocols and Rank-1 Constraint Systems

## Introduction 

Fast and efficient transaction validation is one of the main reasons for Layer 2 Scaling, especially for blockchains using confidential transactions. Rank-1 Constraint Systems (R1CS) are used to achieve faster zero-knowledge proofs, particularly in zk-SNARKs and Bulletproofs. 

An R1CS is “basically a language for arithmetic circuits with bilinear gates” [1.] It defines a set of bilinear equations that serve as constraints suitable for zero-knowledge proofs [2.] 

zk-SNARKs and Bulletproofs are special proof protocols in the family of Non-Interactive Zero-Knowledge proofs (NIZKs). Bulletproofs have been introduced and sufficiently discussed in the TLU [3.] It is the concept of zero-knowledge Succinct Non-interactive Argument of Knowledge (zk-SNARK) that is considered in the first part of this report, with a specific focus on the use of R1CS in building these zk-SNARKs. The second part of the report will focus on how R1CS are used in Bulletproofs.     

    
  ## Zero-Knowledge Proofs 

Unlike Bitcoin which keeps transacting parties anonymous yet leaving transaction amounts in the open, cryptocurrencies such as Monero and Zcash make sure that both the transacting parties and their transactions are confidential. The challenge, however, in such cryptocurrencies with confidential transactions (CTs) is how one party can verify that the other has actually made the right transaction. This is where zero-knowledge (ZK) proofs come in. 

A ZK proof protocol consists primarily of two parties, the Prover and the Verifier, where the Verifier poses a computational challenge to the Prover, who in turn provides proof that they have correctly solved the challenge without disclosing the actual solution or how they solved it. 

So the Prover produces proof that they have correctly carried out a specific computation, and the Verifier validates the proof. The protocol qualifies as 'zero-knowledge' proof protocol if the Prover simply proves to the Verifier that the computation is done correctly, without disclosing their solution or how the computations were carried out.  
   
  
  ### Example of a ZK Proof 
  
  Let's say the Verifier challenges the Prover to solve a 4x4 Sudoku board 
  
  			  _  _  3  _       
  			  3  _  _  2       
  			  4  _  _  _     
  			  _  2  4  _    
  
  The Verifier is not allowed to watch, so she leaves the room.
  The Prover solves the puzzle, and his solution is 
  
   			 2  1  3  4
   			 3  4  1  2
   			 4  3  2  1
   			 1  2  4  3
  
  But the Prover hides the solution by shuffling the numbers according to the shuffle  
  
 			 1 --> 3		which ends up as		4  3  2  1 
  			 2 --> 4						2  1  3  4 
  			 3 --> 2						1  2  4  3
  			 4 --> 1						3  4  1  2 
  
   The Prover then covers each cell of the board and the shuffle, before allowing the Verifier to come look 
   
   			 X  X  X  X		the shuffle		X --> X	
   			 X  X  X  X					X --> X 
   			 X  X  X  X					X --> X 
   			 X  X  X  X					X --> X 

   Here are the rules for verification. The Verifier is only allowed one of the following options; ask the Prover to either

       a) reveal a certain row, or  
       b) reveal a certain column, or  
       c) reveal a 2x2 square, or  
       d) reveal initially filled cells & the shuffle. 

   Say, the Verifier chooses the last option, and finds 
  
   			 X  X  2  X		and the shuffle		1 --> 3	
   			 2  X  X  4					2 --> 4 
   			 1  X  X  X					3 --> 2 
   			 X  4  1  X					4 --> 1    
  
   She now uses the shuffle (in reverse) on the revealed cells to find   
  
   			 X  X  3  X  
   			 3  X  X  2 	
   			 4  X  X  X 
   			 X  2  4  X  
  
   The Verifier sees that it matches the original challenge, but she is not yet convinced that the Prover's solution is correct.   
  
   The Verifier can request another round of verification, according to the following rules; 
  
   	1. The Prover shuffles the numbers in his solution differently  
	2. The Prover covers the shuffled solution and the shuffle   
	3. The Verifier chooses one of the four 'reveal' options given above   
	4. The Prover reveals according to Verifier's request    
	5. The Verifier checks.   
  
   The Verifier can request another round of verification until she is convinced that the Prover's solution is correct. 
   
   Yet in all these rounds, the Prover's solution is never fully revealed. That's how a zero-knowledge proof protocol works.
    
   "It is known that every language in NP has a zero knowledge proof system, thus opening up several cryptographic applications. While true in theory, designing proof systems that are efficient to be used in practice remains challenging" [5.] The above example of a ZK proof protocol is clearly interactive, that is, both the Prover and the Verifier have to be present for the verification to be completed. An interactive ZK proof is not practical in many ways, especially when the Prover and the Verifier are in different geographical locations. Hence the need for non-interactive ZK proofs.  
  
  
  ## Non-Interactive Zero Knowledge Proofs (or NIZKs)
  
  The two main challenges with Non-Interactive ZK proof protocols is speed and security. Thus an ideal NIZK protocol must carry out the verification process securely and with only one round of verification, not as many rounds as seen in the above example. 
  
  The Verifier is obviously not going to send the challenge to the Prover without first applying some 'hiding' or encryption to the challenge. And, the Prover must have known some 'unique' secret, called the witness, that only he can use to prove his identity. This is basically a public-key scenario, and requires a few cryptographic features to be added to a NIZK protocol. 
  
  Cryptographers have devised various protocols to allow secure non-interactive ZK proofs. Depending on specific applications of NIZKs, the following features are often involved; a public-key setup, authentication schemes, homomorphic encryptions, multi-party signatures, and bilinear mappings. (It is hard not to formalise things at this stage.) 
  
   
 
 
 *** Insert here the definition of a NIZK as a triple ( **Setup, P, V** )  ***   
   
  NIZK proofs are generally not possible without a trusted setup assumption and the one proposed initially in [10.] is the existence of a Common Reference String (CRS) received as input both by the prover and the verifier. Such a CRS model has been so far the standard setup for NIZK. 
  
  
 
**Definition**: (Publicly Verifiable Non-Interactive Zero-Knowledge Proof System) [9.] 

A non-interactive zero-knowledge (NIZK) proof system between a prover P and a verifier V for a family of languages  { L_crs }_crs   is a triple of probabilistic polynomial-time algorithms
(Setup,P, V) such that 

• crs ← Setup(1^κ), outputs a common reference string crs, 
 
• π ← P(crs, x, w), on input the  crs, a word x, and a witness w, outputs a proof π,  

• b ← V(crs, x, π), on input the  crs, a word x, and a proof π, outputs b ∈ {0, 1},

 
  
  
  
   Now, how can these keys, *vk* and *pk*, be generated?  
    	 
	1. Via a one time *trusted setup* who uses some randomly chosen *number used once* (nonce) to generate the two keys, (Common Reference String) 
	 
	2. Via a *multi-party* scenario, ... (ceremonies ?), or 

	3. ... pairings ... Elliptic Curve   
	
    



  except that it is now done 
  
  Let's focus on authentication. 
  
  
  Now, 'hiding' or 'encryption' ... 
  
  
  NIZK protocols are said to be categorised according to Sigma protocols and QAP-based ZK proofs. Sigma protocols are efficient for algebraic statements, while zk-SNARKs, which are QAP-based, result in short proofs and and efficient verification.  
 
 
 Definition:  $\Sigma$-protocol 
 
   A Σ-protocol for a language L is a public-coin three-move honest-verifier zero-knowledge proof of knowledge, that has the following structure: 
1. P sends to V some commitments values r,
2. V sends to P a uniformly random challenge e,
3. P sends to V an answer  *f*(w, r, e)  where  *f*  is some public function, and w is the witness
held by P . 

 
  
**Example** of a Discrete Log  $\Sigma$ protocol  ([9.] ) 
	
	Common Input: the description of a prime-order group G of (exponentially large) order  $p$  
	 with a generator g, and a group element h. 

	Prover Witness: A value  $ x ∈ Zp $  such that  $ g^x = h $. 
	 
	Protocol:
		1. P: pick  $ r ←  Z_p $, send  $ ρ ← g^r $.
		2. V: pick  $ e ← Z_p $, send  $ e $.
		3. P: send  $ d ← e · x + r mod p $. 
	
	Verification: V accepts iff  $ g^d = h^{e}ρ $.
  
  
   Although beyond the scope of this report, heuristics have been developed to transform 'any public coin ZK proof into a NIZK proof of knowledge' [5.], known as *Fiat-Shamir transform*. 
   
  
The use of polynomials and homomorphic encryption ...  
  
  
  One of the fundamental ideas with ZK proof protocols is that the Prover does most of the computations and provides proof while the Verifier does little, simply checking the proof. 

 (When discussing informally we will use the word proof to mean both an unconditionally sound proof and a
computationally sound proof (i.e., an argument). Only in the more formal part of the paper we will make a distinction
between arguments and proofs.)



[1.] https://diyhpl.us/wiki/transcripts/cryptoeconomic-systems/2019/zksharks/   

[2.] https://www.sikoba.com/docs/SKOR_GD_R1CS_Format.pdf. 

[3.] https://tlu.tarilabs.com/preface/learning/bulletproofs.html 

[4.] Rietwiessner, Christian; *Introduction to SNARKs*, DevCon 3, https://www.youtube.com/watch?v=jr95o_k_SwI 

[5.] Ganesh, Chaya; *Zero-knowledge Proofs: Efficient Techniques for Combination Statements and their Applications*, NYU, Sept. 2017. 

[6.] 

[7.]   

[8.] Mayer, Hartwig; *zk-SNARKS Explained: Basic Principles*, CoinFabrik, 06 Dec., 2016.

[9.] __ , Pointcheval; *Zero Knowledge Proofs for Secure Computations*
 
[10.]  [BDMP91] 
 
