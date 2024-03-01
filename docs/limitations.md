---
hide:
  - toc
---

# Limitations

There are a number of limitations on Helmi that need to be taken into account when writing quantum circuits.

**Queue length**

To ensure manageable wait times, the job queue can accommodate up to **100 sequential jobs**.
Jobs when the queue reached its limit will be denied, triggering the following error message from the IQM client:

```bash
ClientAuthenticationError: Authentication failed: {"detail":"Job rejected: Too many circuits in queue"}
```

**Batch size**

On our Helmi system, quantum circuits within a batch are processed sequentially. To prevent extensive queue occupation by large batches, we have set a maximum limit of **20 circuits per batch**.
Jobs submitting batches with more than 20 circuits will be rejected and the IQM client will return the following error

```bash
ClientAuthenticationError: Authentication failed: {"detail":"Too many circuits X in batch (max: 20)"}
```

Here, 'X' denotes the actual number of circuits attempted to be included in the batch.

**Number of shots**

The execution time for a quantum circuit scales with the number of shots. To avoid disproportionately long job durations, we impose a threshold of **100,000 shots per circuit**. Should your experiment require more shots, we recommend dividing it into multiple separate jobs. For cases where this shot limit proves inadequate, please do not hesitate to reach out to our [support](support.md).
