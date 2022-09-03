# merico


## Introduction

Given a file path, calculate the cyclomatic complexity of the source file under this path.

Supported languages:

- [Python](https://github.com/tree-sitter/tree-sitter-python)
- [JavaScript](https://github.com/tree-sitter/tree-sitter-javascript)
- [Go](https://github.com/tree-sitter/tree-sitter-go)

## Installation

```shell
pip install git+https://github.com/anzhaozhong/merico.git
```

## Usage

You can use `mcc` both as a CLI program and as a module in your program.

### CLI

```shell
> mcc --help
Usage: mcc [OPTIONS]

  Calculate the cyclomatic complexity of the source code

Options:
  -V, --version              Show the version and exit.
  -d, --directory TEXT       The source code directory
  -f, --file TEXT            The source code file
  -m, --min INTEGER          The min threshold value
  -l, --language [py|go|js]  The source code language  [required]
  --help                     Show this message and exit.
```

### For a single file

You can calculate the cyclomatic complexity for a single source file.

```shell
> mcc -l py -f tests/test_languages.py
{
    "tests/test_languages.py": 9
}
```

### For multiple files under a directory.

You can also calculate the cyclomatic complexity for all files inside a directory, which leverages parallel computing.

```shell
> mcc -l py -d tests
{
    "tests/test_languages.py": 9,
    "tests/__init__.py": 0,
    "tests/test_provider.py": 4,
    "tests/test_cyclomaticc_complexity.py": 8,
    "tests/sources/py.py": 24
}
```

### Set threshold value

You can set a minimun threshold value by using the `-m` flag.

```shell
> mcc -l py -d tests -m 5
{
    "tests/test_languages.py": 9,
    "tests/test_cyclomaticc_complexity.py": 8,
    "tests/sources/py.py": 24
}
```

### Use in program

Also, you can load it as a module in your programs.

```python
from mcc import get_provider_class
from mcc.languages import Lang

cls = get_provider_class(Lang.py)
ret = cls(file="test.py").run()
print(ret)
```
