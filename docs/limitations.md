---
hide:
  - toc
---

# Limitations

There are a number of limitations on Helmi that need to be taken into account when writing quantum circuits.

**Batch size**

On our Helmi system, quantum circuits within a batch are processed sequentially. To prevent extensive queue occupation by large batches, we have set a maximum limit of **200 circuits per batch**.
Jobs submitting batches with more than 200 circuits will be rejected and the IQM client will return the following error

```bash
ClientConfigurationError: Client configuration error: {"error":"Request contains x circuits in batch which is larger than maximum number of circuits (200) allowed per batch for device Helmi."}
```

Here, 'X' denotes the actual number of circuits attempted to be included in the batch.

**Number of shots**

The execution time for a quantum circuit scales with the number of shots. To avoid disproportionately long job durations, we impose a threshold of **100,000 shots per circuit**. Should your experiment require more shots, we recommend dividing it into multiple separate jobs. For cases where this shot limit proves inadequate, please do not hesitate to reach out to our [support](support.md).
