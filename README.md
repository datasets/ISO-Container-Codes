<a className="gh-badge" href="https://datahub.io/core/ISO-Container-Codes"><img src="https://badgen.net/badge/icon/View%20on%20datahub.io/orange?icon=https://datahub.io/datahub-cube-badge-icon.svg&label&scale=1.25" alt="badge" /></a>

Coded list of ISO 6346 shipping containers, used in international trade and electronic shipping messages.

## Data

The data is compiled by hand. There is no script that updates it. It was put together between 2016 and 2020 and the last change to the data files was in February 2020, so new or changed codes since then are not included.

There are two files:

* `data/iso-container-codes.csv` has 716 rows, one per size and type code, with 5 columns:
  * `code`: the 4-character ISO 6346 size and type code, for example `22G1`. The first character is the length, the second is the height, and the last two describe the type. Not every code starts with two digits: 45 start with a letter (for example `L5G0`, `M2G0`) and 3 have a letter second (`4CG0`, `4CG1`, `4CGP`). `code` is not unique: `42HR` appears in two rows.
  * `description`: the container type in words, for example `Dry Bulk`.
  * `length`: external length in feet. `0` means none is given.
  * `height`: external height in feet, for example `8.5` or `9.5`. `0` means none is given.
  * `group`: the code of the group the container belongs to. These are the codes in `data/iso-container-groups.csv`, and they are the codes used in electronic shipping messages.
* `data/iso-container-groups.csv` has 28 rows with 2 columns, `code` (unique) and `description`.

Both files use Windows line endings (CRLF).

### Known quirks

These are in the data as committed and have not been changed:

* The group codes `42TN` (33 rows) and `L5RT` (29 rows) are used in `iso-container-codes.csv` but are not in `iso-container-groups.csv`. The groups file instead has `42TD` and `L5R1`, which no row uses as a group.
* `42HR` is listed twice, once with group `42HR` ("Insulated (Conair)") and once with group `42RT`.
* Where a code starts with `4`, the length column is normally `40`. 13 rows say `45` (for example `45R0`, `45H2`) and `45G4` says `0`. Other rows have an odd length for their code (`3399` has length 23, `2650` has length 0, `12TR` has length 42).

Source of information is from Container Container website (http://www.containercontainer.com/ISO6346.aspx) but multiple other sources of information exist on the web:
* https://en.wikipedia.org/wiki/ISO_6346
* http://www.shippingcontainers24.com/general/iso-6346-codes/
* http://www.iso.org/iso/catalogue_detail?csnumber=20453 (Paid For)

## License

This Data Package is licensed by its maintainers under the [Public Domain Dedication and License (PDDL)](http://opendatacommons.org/licenses/pddl/1.0/).