# FHEM Patches

## Purpose of this project

From time to time, I skimm through the [FHEM documentation](https://fhem.de/commandref_DE.html) and encounter typos, misspellings, misformats etc. pp. and have the urge to fix them. This is the place where I gather my patches.

## Usage 

Very simple, though. For every file I did a patch, I created a folder with subsequent patches in it. So the file

```
docs/commandref_frame_DE.html
```

becomes 
```
docs/commandref_frame_DE.html/<patch>
```

## Create a patch

I added `create-fhem-patches` to this repository. `create-fhem-patches` creates patches based on the [FHEM Git Mirror](https://github.com/mhop/fhem-mirror).
Invoke `create-fhem-patches -h` to get a manual.

## Example script

I.e. this little script will patch every affected file with it's subseqient patches:

### Prerequisits
* Replace `_FHEM_DIR` with your FHEM installation directory
* Replace `_PATCHES_DIR` with the path to this files

### Source
```bash
#!/usr/bin/env bash

# replace this with the path to this files
_PATCHES_DIR="$(realpath $(dirname $0)/../source/patches)"

# replace this with your FHEM installation directory
_FHEM_DIR="/opt/fhem"

# path to your patch binary, adding some flags
_PATCH_BIN="patch -r /dev/null -N"

echo "Source dir: ${_PATCHES_DIR}"

for patch_file in $(find "${_PATCHES_DIR}" -iname '*.patch' -type f -printf "%P\n")
do
    source="${_PATCHES_DIR}/$patch_file"
    target="$(dirname ${_FHEM_DIR}/$patch_file)"

    echo "Applying patch '${source}' to file '${target}'"
    ${_PATCH_BIN} ${target} ${source};

done
```

## LICENSE
This is distributed under the [GNU LGPLv3](https://choosealicense.com/licenses/lgpl-3.0/).

## See also
* Private website: [Christoph Morrison](http://christoph-jeschke.de)
* [FHEM](https://fhem.de)