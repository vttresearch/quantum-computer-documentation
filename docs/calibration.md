Helmi is continuously calibrated to ensure functionality. The calibration process involves a series of experiments, aimed at fine-tuning the parameters, necessary for controlling and measuring the qubits. In addition to calibration, we run benchmarks to obtain the figures of merit reflecting the current state of the quantum computer.

### Calibration sequences

To minimize the impact of calibration on user operations, we calibrate Helmi at night, by running a specific sequence of experiments in order.

**Calibration**:

- Every day at 2 am
- Adjusts qubit drive frequency, amplitude fine-tuning and readout threshold
- Measures $T_1$, $T_2$, $T_2^*$, readout accuracy, single- and two-qubit gate fidelities

A calibration sequence produces what is called a `calibration_set`. This is a set of device parameters, which the quantum computer is currently using to execute quantum circuits. It is identified via a `calibration_set_id`, a unique identifier for the specific `calibration_set`. Usually, when submitting quantum circuits, the most up-to-date calibration set is used, however, it is possible to use a specific `calibration_set_id`. This can be useful for testing the degradation of the performance of our quantum computers.

### Quality metrics set

The benchmarks results are summarized in the *quality metric set* representing the figures of merit and reflecting the latest state of the quantum computer. The calibration metrics can be fetched from Helmi's API by sending HTTP `GET` requests to `/calibration/metrics/latest`. An example script is provided [here](https://github.com/FiQCI/helmi-examples/blob/main/scripts/get_calibration_data.py). Each quality metrics set is identified via a unique ID, with a new ID created after each calibration. Note, that not all metrics are updated after each calibration run. We recommend to save the current calibration set ID together with the job ID to facilitate debugging and analysis. Also note that it can happen that there is a delay of up to 10 minutes between calibrating the device and benchmarking the quality metrics set, causing there to be some delay in presenting the quality metrics data.

The metrics contained in the quality metrics set are summarized below:

| Metric                       | Description                                                                                                                                                                                                              |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| $T_1$ time (s)               | The $T_1$ time is called the longitudinal relaxation rate and describes how quickly the excited state of the qubit returns to its ground state.                                                                          |
| $T_2$ time (s)               | The $T_2$ time is called the transverse relaxation rate and describes loss of coherence of a superposition state.                                                                                                        |
| $T_2$-echo time (s)          | The $T_2$-echo time describes the loss of coherence of the superposition state of the qubit. It is more precise than the $T_2$ Time as it is less susceptible to low-frequency noise.                                    |
| Single-shot readout fidelity | Measures the average accuracy of distinguishing qubit states. The experiment prepares for 50% of the shots the qubit in the ground state $&#124; 0\rangle$ and for the other 50% in the excited state $&#124; 1\rangle$. |
| Single-shot readout 10 error | The error in labelling the qubit state as $&#124; 0\rangle$ when it was prepared in state $&#124; 1\rangle$                                                                                                              |
| Single-shot readout 01 error | The error in labelling the qubit state as $&#124; 1\rangle$ when it was prepared in state $&#124; 0\rangle$                                                                                                              |
| 1QB average gate fidelity    | Average 1QB gate fidelity estimated with randomized benchmarking.                                                                                                                                                        |
| 2QB average gate fidelity    | The average 2QB gate fidelity estimated with randomized benchmarking.                                                                                                                                                    |
| CZ gate fidelity             | The average CZ gate fidelity estimated with interleaved randomized benchmarking. It is usually higher than the average 2QB gate fidelity as a random 2QB Clifford transpiles on average to 8 1QB gates and 1.5 CZ gates. |

These metrics provide critical insights into the operational efficiency, error rates, and coherence properties of Helmi.
Understanding these figures of merit allows a user to make informed decisions on transpilation strategies and qubit selection, optimizing for circuit depth or fidelity.

#### Example response

Here is an example response from Helmi's API for the calibration and quality metrics set

```json
{
  "calibration_set_id": "5dae35ad-67d0-41eb-a73d-79e3828e2357",
  "calibration_set_number_of_observations": 166,
  "calibration_set_created_timestamp": "2024-11-26 03:03:10.359446+00:00",
  "calibration_set_end_timestamp": "2024-11-26 03:03:10.542733+00:00",
  "calibration_set_is_invalid": false,
  "quality_metric_set_id": "e9d1c497-3485-4d9b-b176-2c0b100a5ccd",
  "quality_metric_set_created_timestamp": "2024-11-26 03:03:10.496040+00:00",
  "quality_metric_set_end_timestamp": "2024-11-26 03:03:10.569614+00:00",
  "quality_metric_set_is_invalid": false,
  "metrics": {
    "metrics.ssro.measure.constant.QB1.fidelity": {
      "value": "0.9525",
      "unit": "",
      "uncertainty": "None",
      "timestamp": "2024-11-26 05:03:10.403869+00:00"
    },
    "metrics.ssro.measure.constant.QB1.error_1_to_0": {
      "value": "0.0525",
      "unit": "",
      "uncertainty": "None",
      "timestamp": "2024-11-26 05:03:10.403869+00:00"
    }
  }
}
```
