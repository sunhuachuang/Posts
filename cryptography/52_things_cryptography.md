# 52 Things People Should Know To Do Cryptography
What is this?
Cryptography is a highly interdiscplinary area; calling on expertise in Pure Mathematics, Computer Science and Electronic Engineering. At Bristol we cover the full range of these topics and as such our students come with a variety of backgrounds and need to understand a diverse range of topics. Students starting can often feel overwhelmed by the types of knowledge that they feel they need to know; not knowing what they need to remember and what they should not bother remembering.

To aid you, below we have collected a set of 52 short points of things we think that at the end of the first year of a PhD all students should have some familiarity with. There is one point for every week of the year. If you know these things then following seminars, study groups and conference talks will be much easier. It will also help in putting your own work into context. Some of these are somewhat advanced topics, some of these are what one would pick up in certain undergraduate courses. This is deliberate since some are about being a cryptographer, and some are to address the fact that students start with different backgrounds.

If at the end of the first year you know the answers to ninety percent of the things we list then you should find that you will get more out of the conferences and talks you attend in your second year. In addition it will be easier to talk to cryptographers (who may be future employers) from other institutions since you will be able to converse with them using a common language. Almost all of the following are discussed in our undergraduate cryptography courses.

By each section we give a reference to places where the definitions can be found, or where to start your reading. The list of references can be found at the bottom. Not all answers can be found in the references cited, but they should give you a place to start looking.

### Computer Engineering ([E])
1. What is the difference between the following?
    - general-purpose processor.
    - general-purpose processor with instruction-set extensions.
    - special-purpose processor (or co-processor).
    - An FPGA.
2. What is the difference between a multi-core processor and a vector processor?
3. Estimate the relative computational and storage capabilities of...
    - a smart-card
    - a micro-controller (i.e. a sensor node)
    - an embedded or mobile computer (e.g., a mobile phone or PDA)
    - a laptop- or desktop-class computer.

### Theoretical Computer Science ([F])
4. What is meant by the complexity class P?
5. What is meant by the complexity class NP?
6. How can we interpret NP as the set of theorems whose proofs can be checked in polynomial time?
7. How does randomness help in computation, and what is the class BPP?
8. How does interaction help in computation, and what is the class IP?
9. What are Shannon's definitions of entropy and information?

### Mathematical Background ([A,B])
10. What is the difference between the RSA and the Strong-RSA problem?
11. What are the DLP, CDH and DDH problems?
12. What is the elliptic curve group law?
13. Outline the use and advantages of projective point representation.
14. What is a cryptographic pairing?

### Basic (Practical or Deployed) Cryptographic Schemes and Protocols ([A])
15. Describe the key generation, encryption and decryption algorithms for RSA-OAEP and ECIES.
16. Describe the key generation, signature and verification algorithms for DSA, Schnorr and RSA-FDH.
17. Describe and compare the round structure of DES and AES.
18. Draw a diagram (or describe) the ECB, CBC and CTR modes of operation.
19. Describe the Shamir secret sharing scheme.
20. How are Merkle-Damgaard style hash functions constructed?

### Cryptographic Implementation Details ([A])
21. How does the CRT method improve performance of RSA?
22. How do you represent a number and multiply numbers in Montgomery arithmetic?
23. Write a C program to implement Montgomery arithmetic.
24. Describe the binary, m-ary and sliding window exponentiation algorithms.
25. Describe methods for modular reduction using "special" primes that define GF(p) and GF(2^n).
26. Describe the NAF scalar multiplication algorithm.

### Security Definitions and Proofs ([A,B,C])
27. What is the AEAD security definition for symmetric key encryption?
28. What is the IND-CCA security definition for public key encryption?
29. What is the UF-CMA security definition for digital signatures?
30. Roughly outline the BR security definition for key agreement?
31. Give one proof of something which involves game hopping
32. Outline the difference between a game based and a simulation based security definition.

### Mathematical Attacks ([A,B])
33. How does the Bellcore attack work against RSA with CRT?
34. Describe the Baby-Step/Giant-Step method for breaking DLPs
35. Give the rough idea of Pollard rho, Pollard "kangaroo" and parallel Pollard rho attacks on ECDLP.
36. What is meant by index calculus algorithms?
37. Roughly outline (in two paragraphs only) how the NFS works.

### Practical Attacks ([D])
38. What is the difference between a covert channel and a side-channel?
39. What is the difference between a side-channel attack and a fault attack?
40. What is usually considered the difference between DPA and SPA?
41. Are all side channels related to power analysis?
42. Look at your C code for Montgomery multiplication above; can you determine where it could leak side channel information?
43. Describe some basic (maybe ineffective) defences against side channel attacks proposed in the literature for AES.
44. Describe some basic (maybe ineffective) defences against side channel attacks proposed in the literature for ECC.
45. Describe some basic (maybe ineffective) defences against side channel attacks proposed in the literature for RSA.

### Advanced Protocols and Constructions ([A,B])
46. What does correctness, soundness and zero-knowledge mean in the context of a Sigma protocol?
47. What is the Fiat-Shamir transform?
48. What is the purpose and use of a TPM?
49. Describe the basic ideas behind IPSec and TLS.
50. What is the BLS pairing based signature scheme?
51. What is the security model for ID-based encryption, and describe one IBE scheme.
52. Pick an advanced application concept such as e-Voting, Auctions or Multi-Party Computation. What are the rough security requirements of such a system?

## Further Reading
[A] Nigel's book is deliberately informal and tries to give quick flavours of what is important in theory and practice.
[B] The Katz Lindell book is a better formal introduction to modern theoretical cryptography but it is less good in its treatment of what is important in the real world (e.g. the coverage of AES, ECC, implementation, etc is quite limited).
[C] Goldreich's two volume book is a very good introduction to the deep theory, but deliberately does not cover practical cryptography.
[D] Elisabeth's DPA book is the best introduction to all things about side-channels.
[E] Dan's book is a good starting place for computer architecture and learning VHDL.
[F] Goldreich's book on complexity theory is a good place to start. Its approach is much more down-to-earth and sensible than other approaches (i.e. P vs NP is presented in terms of is it easier to check or find proofs?)
