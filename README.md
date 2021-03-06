# Qiskit AQT Provider

[![License](https://img.shields.io/github/license/Qiskit/qiskit-aqt-provider.svg?style=popout-square)](https://opensource.org/licenses/Apache-2.0)[![Build Status](https://img.shields.io/travis/com/Qiskit/qiskit-aqt-provider/master.svg?style=popout-square)](https://travis-ci.com/Qiskit/qiskit-aqt-provider)[![](https://img.shields.io/github/release/Qiskit/qiskit-aqt-provider.svg?style=popout-square)](https://github.com/Qiskit/qiskit-aqt-provider/releases)[![](https://img.shields.io/pypi/dm/qiskit-aqt-provider.svg?style=popout-square)](https://pypi.org/project/qiskit-aqt-provider/)

Qiskit is an open-source framework for working with noisy intermediate-scale
quantum computers (NISQ) at the level of pulses, circuits, and algorithms.

This project contains a provider that allows access **[AQT]** ion-trap quantum
devices.

## Installation

You can install the provider using pip tool:

```bash
pip install qiskit-aqt-provider
```

`pip` will handle installing all the python dependencies automatically and you
will always install the  latest (and well-tested) version.

**Note**: to get the full advantages of this provider you will need to have
a development version of qiskit-terra installed. The current releases don't
support transpilation for the basis gates of the AQT devices. While you'll be
able to use this provider with the qiskit-terra 0.9.x release series, it
will not automatically translate circuits for you. Therefore it will only
work if you manually use `Rx` and `Ry` gates.

## Setting up the AQT Provider

Once the package is installed, you can use it to access the provider from
qiskit.

### Use your AQT credentials

You can initialize an AQT provider using your token locally with:

```python
from qiskit.providers.aqt import AQT
aqt = AQT.enable_account('MY_TOKEN')
```

Where `MY_TOKEN` is your access token for the AQT device. Then you can access
the backends from that provider:

```python
backends = aqt.backends()
innsbruck_backend = aqt.get_backend('aqt_innsbruck')
```

You can then use that backend like you would use any other qiskit backend. For
example, getting running a bell state:

```python
from qiskit import *
qc = QuantumCircuit(2, 2)
qc.h(0)
qc.cx(0, 1)
qc.measure([0,1], [0,1])
result = execute(qc, innsbruck_backend).result()
print(result.get_counts(qc))
```


## Authors and Citation

The Qiskit AQT provider is the work of many people who contribute to the
project at different levels. If you use Qiskit, please cite as per the included
[BibTeX file].

## License

[Apache License 2.0].

[AQT]: https://www.aqt.eu/
[BibTeX file]: https://github.com/Qiskit/qiskit/blob/master/Qiskit.bib
[Apache License 2.0]: https://github.com/Qiskit/qiskit-aqt-provider/blob/master/LICENSE.txt
