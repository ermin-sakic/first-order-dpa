first-order-dpa
===============

An implementation of the first-order Differential Power Analysis (DPA) attack, suited for evaluations of AES-128 algorithm on microcontrollers leaking Hamming Weight power models. 

### Introduction:
The last round of the AES encryption procedure is targeted in this implementation. The traces were taken by using the picoscope and sampling power measurements of encryption executions.
Also the recorded cyphertexts (output of the encryption procedures) were written to a matrix used to build intermediate value hypotheses (256 key hypotheses for each byte of the encrypted text).
After the execution of the inverse Sub-Byte lookup step on the intermediate value, it is necessary to find a correlation between the encyption of data and the power consumption model. There is need to correlate the Hamming weight of the intermediate hypotheses, which are representations of the true intermediate values, with the power consumption vectors of the actual taken traces. 
Via Hamming-Weight model one can mathematically describe the power consumption according to computed bits (number of 1s in the intermediate byte value). The hypothesis leading to the vector of intermediate values resulting with the highest correlation with the real (taken) power traces corresponds to the true (actual) key byte
of the 16-byte wide key used in the AES-128 encryption implementation.

### Implementation:

After the Hamming matrix of the intermediate values has been calculated, correlation of these vectors with the traces needs to be computed. Using the following correlation equation:

<a href="http://imgur.com/7CGew9v"><img src="http://i.imgur.com/7CGew9v.png"/></a>

one can calculate the so-called correlation matrix, where r stands for every correlation entry of the matrix, t for used traces and h for the matrix of Hamming-Weight. Please note that the equation is given for 2 dimensional operations and our Hamming-Weight Matrix is actually 3 dimensional. But basically, as we correlate only one dimension of the Hamming(-Weight)-Matrix to the Trace matrix, we can still use this equation above; we just repeat this operation for every 3rd Dimension of the Hamming-Weight Matrix.






