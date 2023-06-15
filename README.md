# Reproducing the results from the paper: *Heisenberg-Limited Ground-State Energy Estimation for Early Fault-Tolerant Quantum Computers*

The goal is to study the efficacy of their proposed algorithm by approximating the ground state of a 1D Hubbard Model of variable chain length with parameter $U = 10$, $U/t = 4$, and the open boundary condition.

## Idea:

The algorithm consists of preparing a good initial state (a state with a good-enough overlap with the true ground state of the system) and, by applying the following circuit, one can measure the ancilla in the computation basis and approximate a CDF which is then classically postprocessed to approximate the ground state:

![circuit](circuit.png)


## Notes on numerical experiments:

In the paper, two things are varied: the length of the 1D chain, and the ansatz overlap with the true initial state, $ p_0 = ||<\psi_0 | \rho>||^2 $.

the initial $\rho$ is taken to be the Hartree-Fock solution.

### Progress:

- Created OpenFermion Hamiltonian
- Translated the Hamiltonian into Qulacs observable object
- Created Trotterized Quantum Circuit for time evolution

### Ongoing

- Prepare HF state


### To-Do:

- Implement the controlled version of the time evolution Quantum Circuit


### Questions:



- Qulacs circuit methods
    - I am nort sure how to create the control version of the circuit. So far, I have created the Trotterized circuit to time evolve the qubits. However, the only method I found to do so in Qulacs so far is:

                circuit.add_observable_rotation_gate(qulacs_hamiltonian, angle, t_slice)

    However, we need a $N + 1$ qubit circuit where $N$ is trhe number of qubits for the Hamiltonian. Thus, my approach so far was to create a $N + 1$ qubit circuit 

                circuit = QuantumCircuit(n_qubits+1)

    and then add the trotterized gates. But when I do so, the gates will only act on $N$ qubits so how do I know which qubit is the ancilla? In othwer words, how do I spexcify Qulacs where to add this trotterized circuit?

    - On a similar note, is there some sort of built-in function to turn this circuit into a controlled-operator? If not, what would be the best approach to turn this into a cotrolled operation?

- Hartree-Fock initial state preparation
    - Thanks so much for the resources you provided. I understand how to prepare the HF state now, but I am just a little unsure about how many electron we have in our systrem (a 1D Hydrogen chain). I would have guessed that we have as many electrons as we have sites, thus for a 5 site chain we have a 10 qubit operator for which the HF state is $|1111100000>$. Is this correct?