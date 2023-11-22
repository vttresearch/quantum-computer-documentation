---
hide:
  - toc
---


# FAQ

**Q: Does the name "Helmi" have a meaning?**

Helmi is the Finnish word for pearl.

**Q: Does Helmi provide pulse-level access?**

Currently, we only provide circuit-level access.

**Q: Is there any optimization applied during gate-to-pulse compilation?**

No circuit optimization is performed after the circuit has been submitted in serialized form with the [IQM client](https://iqm-finland.github.io/iqm-client/). The gate-to-pulse compiler replaces each gate by the corresponding pulse and submits the pulses to the backend for execution.

**Q: Is heralding enabled on Helmi?**

[Heralding](https://iqm-finland.github.io/iqm-client/api/iqm.iqm_client.iqm_client.HeraldingMode.html#iqm.iqm_client.iqm_client.HeraldingMode) is an optional feature that allows for post-selection of shots, to filter out runs where one or more qubits were not in the ground state at the beginning of the circuit execution. The feature is currently unavailable on Helmi.

**Q: What is the time-to-execution after a job has been scheduled on Helmi?**

An overhead of 10 seconds can be expected. The largest overhead is introduced by compiling the pulses to instructions for the control electronics and the upload to the instruments.

**Q: Does the number of shots affect the calibration of Helmi?**

No, a large number of shots will not cause thermal excitations of the qubits.

**Q: Can Pennylane be used on Helmi?**

Yes, Pennylane can be used on Helmi through a [fork of the Pennylane-Qiskit package](https://github.com/NordIQuEst/pennylane-qiskit/tree/support-num-qubits). This is demonstrated in the [Introduction to Helmi with Qiskit example](examples/intro-to-helmi-qiskit.ipynb#pennylane-qiskit).
