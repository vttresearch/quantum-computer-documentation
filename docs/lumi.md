# Accessing LUMI

Before accessing LUMI you need to be added to a project in [My CSC](https://my.csc.fi/) with your CSC account. Access to LUMI is currently only through the command line interface, with access provided over SSH. Users using LUMI should have some experience with the Linux command line and familiarity with HPC systems. To log on to LUMI, you will first need to add your ssh key on your [My CSC](https://my.csc.fi/) profile section.

The LUMI documentation offers a [guide](https://docs.lumi-supercomputer.eu/firststeps/SSH-keys/) for creating SSH keypairs from which you should follow the instructions labeled "With a Finnish allocation".

!!! note

    It might take a couple of hours until your public key is distributed to all LUMI nodes.

!!! warning

    The private key should never be shared with anyone. It should only be stored on your local computer. Otherwise, anyone can steal the SSH key and impersonate you.

Once your public SSH key is available on all login nodes, you can access LUMI using

``` bash
ssh -i <path-to-private-key> <username>@lumi.csc.fi
```

The LUMI [documentation](https://docs.lumi-supercomputer.eu/firststeps/loggingin/) provides further information on how to connect to LUMI. For an introduction to LUMI, its architecture, modules and software stack, take a look at the [LUMI training materials](https://lumi-supercomputer.github.io/LUMI-training-materials/1day-20230921/#downloads).

## Storage

LUMI uses a Linux based parallel filesystem, utilising [lustre](https://www.lustre.org/). Access to differents parts of the file system are based on the projects you are associated with. LUMI's storage areas and their intended use cases are described [here](https://docs.lumi-supercomputer.eu/storage/).

## Configuring the environment

To run quantum circuits on LUMI we need to load certain Python modules. Dependencies are managed via [`modules`](https://curc.readthedocs.io/en/latest/compute/modules.html), which can be loaded.

To load the required modules, after connecting to LUMI, run the following lines in your terminal

```bash
module use /appl/local/quantum/modulefiles
module load helmi_qiskit  # or helmi_cirq
```

This commands can also be added to your `.bashrc` to save repetition. In case you are curious, you can explore other available modules via `module avail`.

### Using a custom Python environment

Loading `helmi_qiskit` or `helmi_cirq` on LUMI comes with a preconfigured Python environment for submitting jobs to Helmi. This environment can be replicated by users, by following the [LUMI documentation on installing python packages](https://docs.lumi-supercomputer.eu/software/installing/python/#installing-python-packages). To access Helmi you will still need to load the `helmi_standard` module.

<center>

| Package                                             | Version       |
| --------------------------------------------------- | ------------- |
| [iqm-client ](https://pypi.org/project/iqm-client/) | >=12.5 < 13.0 |
| [qiskit-iqm](https://pypi.org/project/qiskit-iqm/)  | >=8.3 < 9.0   |
| [cirq-iqm](https://pypi.org/project/qiskit-iqm/)    | >=11.9 < 12.0 |

</center>

Newer versions of the above Python packages can be installed and may work with Helmi, however these are currently unsupported and may lead to errors.

As an alternative to the above, Python packages can be installed on top of `helmi_qiskit` or `helmi_cirq` into the Python user install directory by specifying `python -m pip install --user whatsapp`. This, however, may lead to increased dependency conflicts.

<!-- Once LUMI uses a conda based tykky env we can recommend to users to create a virtual env with the --system-site-packages flag -->

## Submitting jobs

Once you have access to LUMI and have configured your environment you can learn how to run jobs on Helmi with the [Running on Helmi](running.md).
