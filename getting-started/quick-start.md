# Quick Start

## Install

Kye is available as a python library on [pypi](https://pypi.org/project/kye/)

```
pip install kye
```

## Run

Pass the location of the kye file, the data (`.csv`, `.json` or `.jsonl`) file, and the name of the Model to evaluate the data against. If the data does not pass the model's assertions then the errors and errant data will be displayed.

```
kye user.kye --data users.csv --model User
```

## Compile

The Kye language can optionally be compiled into a json or yaml file. Using the `-c` flag followed by a path to a `.json` or `.yaml` file. Run the compiled file like you would a normal `.kye` file

```
kye user.kye -c user.kye.yaml
kye user.kye.yaml --data users.csv --model User
```

