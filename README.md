
# Measurement-Free Quantum Error Correction (MFQEC) Simulation

> **⚠️ Status: Initial Draft / Proof of Concept**
> *This repository contains an initial implementation of a measurement-free error correction protocol simulation. The code is currently in a prototype stage and is subject to significant changes, optimization, and validation in future updates. Feedback and collaborative insights are welcome.*

## Overview

This project simulates **Measurement-Free Quantum Error Correction (MFQEC)** protocols using the `Stim` library. Unlike standard measurement-based QEC, which relies on measuring syndromes and processing them with a classical decoder, MFQEC relies on autonomous coherent feedback (typically via Toffoli gates) to correct errors in real-time without collapsing the quantum state.

This simulation approximates the coherent feedback process using a **semi-classical trace method** within Stim. It mimics the logic of a Toffoli gate by inspecting the stabilizer tableau and applying corrective feedback dynamically, allowing for the simulation of logical error suppression in near-term devices.

## Key Features

* **Repetition Code Implementation:** Supports variable distances () to test scaling behavior.
* **Measurement-Free Logic:** Implements a `toffoli_mimicer` function that simulates the action of autonomous correction gates.
* **Systematic Noise Injection:** A modular noise model (`add_noise_to_stim_circuit`) that allows independent tuning of:
* Idle Noise ( at TICKs)
* Gate Noise (Depolarizing/Biased noise after Cliffords)
* Readout & Reset Errors (SPAM)


* **Threshold Analysis:** Scripts to generate Logical Error Rate () vs. Physical Error Rate () plots to observe exponential suppression of errors.

## Code Structure

The simulation is built around a "Chunked Circuit" architecture:

1. **`encoder_mf_st`**: Prepares the logical state and ancillas.
2. **`synd_extractor_mf_st`**: Generates the noisy syndrome extraction circuit (the "Recipe").
3. **`toffoli_mimicer_mf_st`**: Analyzes the syndrome and appends the corresponding correction gates to the circuit.
4. **`add_noise_to_stim_circuit`**: Injects realistic noise models into the clean circuit chunks before simulation.

## Simulation Results

Preliminary runs with `rounds=1` demonstrate the expected **exponential suppression** of logical error rates as the code distance increases from  to .


This serves as a sanity check. 

## Future Roadmap

* **Logic Refinement:** Improving the fidelity of the Toffoli mimicry to better account for coherent error propagation across multiple rounds.
* **Code Expansion:** extending the simulation to Surface Codes and Bacon-Shor codes.
* **Noise Analysis:** Identifying the specific noise regimes (biased vs. depolarizing) where MFQEC provides a distinct advantage over standard measurement-based schemes.

## Requirements

* Python 3.x
* `stim`
* `numpy`
* `matplotlib`
* `tqdm`

## License

This project is open for research and educational purposes.

---

### Author

**Dharmaraj Ramachandran**
*Research Associate, QSRG, SETS Chennai*
