# A Note

This is a journal in which I will document my learning process. I will refer back to this in order to respond to potential future queries about my initial quantum programming experience. All entries are dated and timestamped in 24-hour time.

### Wed, Jul 31, 1:19

On the 28th, I set out to find a quantum language suitable to my needs. The day before this I had begun to read about quantum principles, but I was still not comfortable with principles such as entanglement. At first I experimented with Quipper, but I ultimately settled on QCL.

On the 29th I attempted to make a program to entangle 3 qubits to generate an equal probability from <1| to <6|, leaving <0| and <7| with a zero probability. This essentially emulates a die roll. I had no problem setting up the first qubit (obviously, 1/2 chance it's a <1| so a simple Hadamard suffices). The second qubit was not too difficult for me either once I discovered the Rot() function. At first I struggled with the third qubit a great deal. After failing to figure out a clever way to entangle it to the first two, I simply hard-coded an 8x8 matrix. After a little more thought, I figured out how to decompose this into two calls of a hardcoded 4x4 matrix gate. As I was unable to simplify this further, I posted a question on stackoverflow: http://stackoverflow.com/questions/17937220/how-can-i-make-a-two-qubit-controlled-rotate-in-qcl.

Today (really yesterday) I woke up ready to accept the controlled phase shift gate as something I needed to use. I looked back at one of the quantum programming tutorials to see how they suggested rotating a single qubit, and simply translated this over to a controlled-V gate. I went on to prove that the routine I had implemented actually did what it was supposed to. I then simplified this even further: my code is now a simple Hadamard followed by two controlled-V gates followed by another Hadamard. I understand why this code works, but I am still unclear exactly what makes up the phase of a qubit. The entire complex component of a qubit continues to confuse me. However, I do understand that a phase adjustment ultimately does not affect the probabilistic outcome of a given quantum state. One other thing I still do not understand: in the tutorial, they suggest shifting the result of a rotation by (pi/2 + a) in order to yield cos(t)*<0| + e^(i*a)*sin(t)*<1|. I do not understand why the pi/2 needs to be there. I will continue to play with single-qubit rotation until I fully understand.

In the mean time, I spent the latter half of today manipulating not gates in order to create a quantum adder on an arbitrarily sized qureg. I used this to add the outcomes of two die rolls in order to generate a probability distribution for two dice (e.g. the way you roll in Monopoly).

### Wed, Jul 31, 19:58

This morning I decided to create something to mix two states (i.e. Mix(<010|, <110|) = 0.5 <010| + 0.5 <110|). At first I was hopelessly unable to figure out how to do this. After a while, however, I realized that I could implement it if I made an equality gate. This gate would act as a NOT gate only if two n-qubit strings were identical. I then continued to make new discoveries: CNot(a, b) will only leave `a` with a value of <1| if a != b. Thus, I could make my equality gate if I could make a controlled not gate whose control was an n-qubit long string. Ultimately, I used a nice recursive algorithm to implement an n-qubit controlled not gate. From there I went up the ladder all the way back to my mixer. I completed this last step in about half an hour and was quite pleased with myself.

### Thu, Aug 1, 17:21

Last night and today I began to ponder how quantum algorithms could be faster than classical algorithms. I discovered that, in order to understand Shor's algorithm, I would first need a full grasp on the Quantum Fourier Transform. The tutorial which I've been following (http://www.quantiki.org/wiki/Basic_concepts_in_quantum_computation#Bibliography) had only a brief explanation and thus I was unable to grasp even the functionality of the QFT. Eventually, I came to understand the QFT as the DFT where the coefficients of each state (e.g. the coefficients of <000|, <001|, <010|… for a 3 qubit register) act as the vector which is to be transformed. Furthermore, in order to understand the actual QFT circuit, I decided to only prove that the circuit worked for a pure input (i.e. one of the input coefficients is 1 and the rest are 0).

On paper I was able to calculate what the coefficient for each result state would need to be. However, I had trouble using this information to derive the coefficient for each qubit. After reading http://www.cs.washington.edu/education/courses/cse599d/06wi/lecturenotes9.pdf I still struggled to understand some of the logic required to arrive at the final circuit. At present, I can convince myself that the circuit works, but it certainly does not feel natural or elegant to me in the least. I want to refrain from learning about Shor's algorithm, at least until I fully understand the QFT.

### Fri, Aug 2, 19:26

Today I finally became comfortable with the QFT. Now it is beginning to make sense to me how it works in its entirety. I think the majority of my struggling was caused by the unusual fact that the QFT can actually be expressed as a set of unentangled qubits. Anyways, I set out today to understand Shor's algorithm. I think that I now have a pretty good understanding of how the algorithm works.

In preparation for implementing Shor's algorithm on my own, I decided to write my own arithmetic operations so that I could implement exponentiation mod N (needed for Shor's algorithm). While I did not nearly finish what I plan to, I was able to implement an addition function which does not return an additional carry bit (although at present it still uses a scratch qubit for this). In addition, I made a wrapper function which adds in place (although at present it does allocate a third qureg). This will make it possible to implement long multiplication.

While most of the circuits I am implementing are pretty closely knit with their classical equivalents, I am noticing myself becoming increasingly comfortable with unitary operations. I can quickly tell whether something is possible or not, and I can pretty quickly implement any gate which is thrown my way.