Helmi is continously calibrated to ensure functionality. The calibration process involves a series of experiments, aimed at fine-tuning the parameters, necessary for controlling and measuring the qubits. In addition to calibration, we run benchmarks to obtain the figures of merit reflecting the current state of the quantum computer.

!!! note

    Calibration and benchmarking experiments are interleaved with regular user jobs in Helmi's job queue, as detailed in the [Running on Helmi](running.md) section. The calibration might therefore slightly increase the waiting time in the queue of regular user jobs.

### Calibration sequences

To minimize the impact of calibration on user operations, we execute shorter calibration sequences during the day and a longer calibration run throughout the night.

**Short calibration**:

- Every 2 hours from 11 am to 11 pm
- Adjusts qubit drive frequency, drive amplitude and readout threshold
- Measures $T_1$, $T_2$, $T_2^*$ and readout accuracy

**Extended calibration**:

- Every day at 4 am
- Adjusts qubit drive frequency, amplitude fine-tuning and readout threshold
- Measures $T_1$, $T_2$, $T_2^*$, readout accuracy, single- and two-qubit gate fidelities

### Figures of Merit

The benchmarks results are summarized in the *calibration set* representing the figures of merit and reflecting the latest state of the quantum computer. The calibration set can be fetched from Helmi's API. An example script is provided [here](https://github.com/FiQCI/helmi-examples/blob/main/scripts/get_calibration_data.py). Each calibration set is identified via a unique ID.
A new calibration set ID is created after each calibration. Note, that not all metrics are updated after each calibration run. We recommend to save the current calibration set ID together with the job ID to facilitate debugging and analysis.

The metrics contained in the calibration set are summarized below:

| Metric                       | Description                                                                                                                                                                                                              |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| $T_1$ time (s)               | The $T_1$ time is called the longitudinal relaxation rate and describes how quickly the excited state of the qubit returns to its ground state.                                                                          |
| $T_2$ time (s)               | The $T_2$ time is called the transverse relaxation rate and describes loss of coherence of a superposition state.                                                                                                        |
| $T_2$-echo time (s)          | The $T_2$-echo time describes the loss of coherence of the superposition state of the qubit. It is more precise than the T2 Time as it is less susceptible to low-frequency noise.                                       |
| Single-shot readout fidelity | Measures the average accuracy of distinguishing qubit states. The experiment prepares for 50% of the shots the qubit in the ground state $&#124; 0\rangle$ and for the other 50% in the excited state $&#124; 1\rangle$. |
| Single-shot readout 10 error | The error in labelling the qubit state as $&#124; 0\rangle$ when it was prepared in state $&#124; 1\rangle$                                                                                                              |
| Single-shot readout 01 error | The error in labelling the qubit state as $&#124; 1\rangle$ when it was prepared in state $&#124; 0\rangle$                                                                                                              |
| 1QB average gate fidelity    | Average 1QB gate fidelity estimated with randomized benchmarking.                                                                                                                                                        |
| 2QB average gate fidelity    | The average 2QB gate fidelity estimated with randomized benchmarking.                                                                                                                                                    |
| CZ gate fidelity             | The average CZ gate fidelity estimated with interleaved randomized benchmarking. It is usually higher than the average 2QB gate fidelity as a random 2QB Clifford transpiles on average to 8 1QB gates and 1.5 CZ gates. |

These metrics provide critical insights into the operational efficiency, error rates, and coherence properties of Helmi.
Understanding these figures of merit allows a user to make informed decisions on transpilation strategies and qubit selection, optimizing for circuit depth or fidelity.
