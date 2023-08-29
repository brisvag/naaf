# cryohub

`cryohub` is a library for reading and writing Cryo-ET data based on the [`cryotypes`](https://github.com/teamtomo/cryotypes/) specification.

# Installation

```bash
pip install cryohub
```

# Usage

`cryohub` provides granular I/O functions such as `read_star` and `read_mrc`, which will all return objects following the `cryotypes` specification.

```py
from cryohub.reading import read_star
poseset = read_star('/path/to/file.star')
```

A higher level function called `read` adds some magic to the IO procedure, guessing file formats and returning a list of `cryotypes`.

```py
from cryohub import read
data = read('/path/to/file.star', '/path/to/directotry/', lazy=False, name_regex=r'tomo_\d+')
```

See the help for each function for more info.

Similarly to the `read_*` functions, `cryohub` provides a series of `write_*` functions.

```py
from cryohub.writing import write_tbl
write_tbl([poseset1, poseset2], 'particles.tbl')
```


## From the command line

If you just need to quickly inspect your data but want something more powerful than just reading text files or headers, this command will land you in an ipython shell with the loaded data collected in a list called `data`:

```bash
cryohub path/to/files/* /other/path/to/file.star
```

```py
print(data[0])
```

# Features

Currently `cryohub` is capable of reading images in the following formats:
- `.mrc` (and the `.mrcs` or `.st` variants)
- Dynamo `.em`
- EMAN2 `.hdf`

and particle data in the following formats:
- Relion `.star`
- Dynamo `.tbl`
- Cryolo `.cbox` and `.box`

Writer functions currently exist for:
- `.mrc`
- EMAN2 `.hdf`
- Dynamo `.em`
- Relion `.star`
- Dynamo `.tbl`

## Image data

When possible (and unless disabled), cryohub loads images lazily using [`dask`](https://docs.dask.org/en/stable/array.html). The resulting objects can be treated as normal numpy array, except one needs to call `array.compute()` to apply any pending operations and return the result.

# Contributing

Contributions are more than welcome! If there is a file format that you wish were supported in reading or writing, simply open an issue about it pointing to the specification. Alternatively, feel free to open a PR with your proposed implementation; you can look at the existing functions for inspiration.
