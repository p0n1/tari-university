# Zero-knowledge Proof Protocols and Rank-1 Constraint Systems

## Introduction 

Fast and efficient transaction validation is one of the main reasons for Layer 2 Scaling, especially for blockchains using confidential transactions. Rank-1 Constraint Systems (R1CS) are used to achieve faster zero-knowledge proofs, particularly in zk-SNARKs and Bulletproofs. 

An R1CS is “basically a language for arithmetic circuits with bilinear gates” [1.] It defines a set of bilinear equations that serve as constraints suitable for zero-knowledge proofs [2.] 

zk-SNARKs and Bulletproofs are special proof protocols in the family of Non-Interactive Zero-Knowledge proofs (NIZKs). Bulletproofs have been introduced and sufficiently discussed in the TLU [3.] It is the concept of zero-knowledge Succinct Non-interactive Argument of Knowledge (zk-SNARK) that is considered in the first part of this report, with a specific focus on the use of R1CS in building these zk-SNARKs. The second part of the report will focus on how R1CS are used in Bulletproofs.     

    
  
  ## Zero-Knowledge Proofs 

Unlike Bitcoin which keeps transacting parties anonymous yet leaving transaction amounts in the open, cryptocurrencies such as Monero and Zcash make sure that both the transacting parties and their transactions are confidential. The challenge, however, in such cryptocurrencies with confidential transactions (CTs) is how one party can verify that the other has actually made the right transaction. This is where zero-knowledge proofs come in. 

A zero-knowledge proof protocol consists primarily of two parties, the Prover and the Verifier, where the Verifier poses a computational challenge to the Prover, who in turn provides proof that they have correctly solved the challenge without disclosing the actual solution or how they solved it. 

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
  
 			 1 --> 3 
  			 2 --> 4 
  			 3 --> 2 
  			 4 --> 1 
  
   which ends up as  
   
   			 4  3  2  1 
   			 2  1  3  4   
   			 1  2  4  3
   			 3  4  1  2  
   
   The Prover them covers each cell of the board and the shuffle, before allowing the Verifier to come look 
   
   			 X  X  X  X		the shuffle			X --> X	
   			 X  X  X  X					X --> X 
   			 X  X  X  X					X --> X 
   			 X  X  X  X					X --> X 

   Here are the rules for verification. The Verifier is only allowed one of the following options; ask the Prover to either

       a) reveal a certain row, or  
       b) reveal a certain column, or  
       c) reveal a square, or  
       d) reveal initially filled cells & the shuffling. 

   Say, the Verifier chooses the last option, and finds 
  
   			 X  X  2  X		the shuffle			1 --> 3	
   			 2  X  X  4					2 --> 4 
   			 1  X  X  X					3 --> 2 
   			 X  4  1  X					4 --> 1    
  
   She now uses the shuffle on the revealed cells to find   
  
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

   This example of a zero-knowledge protocol is clearly interactive, that is both the Prover and the Verifier have to be present for the verification to be completed. 
   
  
  
  
  ## Non-Interactive Zero Knowledge Proofs 
  
  	The use of polynomials and homomorphic encryption ...  
  
  
  

  ## Zero-Knowledge SNARKs  
  
  ###  5-step process of creating a zk-SNARK for a computation 
  
  (Computation —> Arithmetic Circuit —> R1CS —> QAP —> Linear PCP —> zk-SNARK). PCP = probabilistically checkable proofs. 

 
  
  

  ## What is a Rank-1 Constraint Systems 
  
   
  
  ## Rank-1 Constraint Systems and zk-SNARKs  
  
  
  ​  
  ## Rank-1 Constraint Systems and Bulletproofs  
  
  
  
  
  ## Various Ways to Implement R1CS 
- Cf. [2.] above regarding the “binary file format” versa vis “JSON lines format” (sizes of the constraints) 
- Implementation cases: Zcash, Zcoin,… Stellar (cf. Cathie Yun’s article “Programmable Constraint Systems for Bulletproofs”
- "Libra: Succinct Zero-Knowledge Proof with Optimal Prover Computation" - Tiancheng Xie et al, eprint.iacr.org/2019/317.pdf  





[1.] https://diyhpl.us/wiki/transcripts/cryptoeconomic-systems/2019/zksharks/   

[2.] https://www.sikoba.com/docs/SKOR_GD_R1CS_Format.pdf. 

[3.] https://tlu.tarilabs.com/preface/learning/bulletproofs.html 

[4.] Rietwiessner, Christian; *Introduction to SNARKs*, DevCon 3, https://www.youtube.com/watch?v=jr95o_k_SwI 




