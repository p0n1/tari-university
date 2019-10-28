# Zero-knowledge Proof Protocols and Rank-1 Constraint Systems

## Introduction 

Fast and efficient transaction validation is one of the main reasons for Layer 2 Scaling, especially for blockchains using confidential transactions. Rank-1 Constraint Systems (R1CS) are used to achieve faster zero-knowledge proofs, particularly in zk-SNARKs and Bulletproofs. 

An R1CS is “basically a language for arithmetic circuits with bilinear gates” [1.] It defines a set of bilinear equations that serve as constraints suitable for zero-knowledge proofs [2.] 

zk-SNARKs and Bulletproofs are special proof protocols in the family of Non-Interactive Zero-Knowledge proofs (NIZKs). Bulletproofs have been introduced and sufficiently discussed in the TLU [3.] It is the concept of zero-knowledge Succinct Non-interactive Argument of Knowledge (zk-SNARK) that is considered in the first part of this report, with a specific focus on the use of R1CS in building these zk-SNARKs. The second part part of the report will focus on how R1CS are used in Bulletproofs.     

    
  
  ## Non-Interactive Zero-Knowledge Proofs 

Unlike Bitcoin which keeps transacting parties anonymous yet disclosing the transactions amounts, cryptocurrencies such as Monero and Zcash make sure that both the parties and their transactions are confidential. The challenge therefore, in cryptocurrencies with confidential transactions (CTs), is how one party can verify that the other has actually made the right transaction. This is where zero-knowledge proofs come in. 

A zero-knowledge proof protocol consists primarily of two parties, the Prover and the Verifier, where the Verifier poses a computational challenge to the Prover, who in turn provides proof that they have correctly solved the challenge without disclosing the actual solution or how they solved it. 
 
So the Prover produces proof that they have correctly carried out a specific computation, and the Verifier validates the proof. The protocol qualifies as 'zero-knowledge' proof protocol if the Prover simply proves to the Verifier that the computation is done without disclosing their solution or how the computations were carried out.  
   
  
  ### Example of a NIZK ... (use the 4x4 Sudoku Example cf. Christian Reitwiessner's video at DevCon)
  
  

  ## Zero-Knowledge SNARKs 
  
  
  ###  5-step process of creating a zk-SNARK for a computation (Computation —> Arithmetic Circuit —> R1CS —> QAP —> Linear PCP —> zk-SNARK). 

 
  

  ## What is a Rank-1 Constraint Systems 
  called the Prover
  
  ## Rank-1 Constraint Systems and zk-SNARKs  
  
  
  ​  
  ## Rank-1 Constraint Systems and Bulletproofs  
  
  
  
  
  ## Various Ways to Implement R1CS 
- Cf. [2.] above regarding the “binary file format” versa vis “JSON lines format” (sizes of the constraints) 
- Implementation cases: Zcash, Zcoin,… Stellar (cf. Cathie Yun’s article “Programmable Constraint Systems for Bulletproofs”





[1.] https://diyhpl.us/wiki/transcripts/cryptoeconomic-systems/2019/zksharks/   

[2.] https://www.sikoba.com/docs/SKOR_GD_R1CS_Format.pdf. 

[3.] https://tlu.tarilabs.com/preface/learning/bulletproofs.html 




