# Overview

This project implements and evaluates a flag-based fault-tolerant (FT) error-correction scheme for the 3-qubit bit-flip repetition code. We deliberately inject bit-flip noise, extract stabilizer syndromes using minimal ancilla + flag qubits, and compare simulated vs. real quantum hardware execution. The goal is to demonstrate how flag qubits enable fault-tolerant syndrome extraction with dramatically fewer resources than conventional FTQC circuits. 



# Motivation

Conventional FTQC typically requires many ancillas, increasing circuit depth and exposure to noise on NISQ devices. Flag-based methods reduce ancilla count (here, just two extra qubits) while still catching dangerous error propagations during stabilizer measurements, making FT techniques more practical on today’s hardware. 



Method

Code & Noise Model: 
Protect a single-qubit state 
∣
𝜓
⟩
∣ψ⟩ via the 3-qubit encoding 
∣
𝜓
′
⟩
=
𝑎
∣
000
⟩
+
𝑏
∣
111
⟩
∣ψ
′
⟩=a∣000⟩+b∣111⟩ against bit-flip (X) errors modeled by a classical-analogue bit-flip channel.

Stabilizers: Measure commuting generators ZZI and IZZ to obtain error syndromes without collapsing the logical superposition.

Flagged Syndrome Extraction: Add flag qubits to the parity-check circuits. If a flag trips, re-extract targeted syndromes to identify and safely correct error patterns that could otherwise spread.

Pipelines:

Simulation with Qiskit Aer to validate circuits and correction logic.

Hardware runs on an IBM Quantum backend to observe real-device behavior (counts, histograms, and final-state similarity).

Notebook implements: circuit construction (data + ancilla + flag), flagged/unflagged syndrome extraction, histogram plotting, and Hellinger fidelity between the pre- and post-correction measurement distributions.

# Results

The flag-based scheme functions as expected in simulation.

On hardware, we observe notable fidelity degradation driven by decoherence and noise on current-generation devices; the paper reports an average final fidelity around 2.34% on the IBM backend, underscoring practical NISQ limitations and motivating further error-mitigation/compilation strategies.
