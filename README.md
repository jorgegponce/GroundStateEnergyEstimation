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
- Translated the Hamiltonian into Pennylane observable object
- Prepared HF state
- Trotterized the Circuit and implemented the $e^{i\sigma \theta}$ gates
- Created the discrete distribuition from which to sample $\{J_k\}$
- Defined the random varaibles for the Hadamard test based on the outcome of the circuit

### Ongoing

- Calculate the estimator $G(x)$

### To-Do:

- Recover the graphs from the paper
- Implement their CERTIFY method

### Questions:

I have been having a hard time nunmerically intergating the functions. The calculations for a single estimator calculation take a really long time, and from what I see in the paper, they use a sample size of 3000 for each approximate CDF evaluation. Is there a better way to integrate numerically the necessary functions? (the Mollifier functions and its fourier transform). These integrals also fail to converge.

