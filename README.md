<a className="gh-badge" href="https://datahub.io/core/ISO-Container-Codes"><img src="https://badgen.net/badge/icon/View%20on%20datahub.io/orange?icon=https://datahub.io/datahub-cube-badge-icon.svg&label&scale=1.25" alt="badge" /></a>

# ISO 6346 Container Type Codes

Coded list of ISO 6346 shipping containers, used in international trade and electronic shipping messages: the size and type codes (for example `22G1`) and the groups they belong to.

Column definitions and types are in `datapackage.json`.

## Data

The data is compiled by hand. There is no script that updates it. It was put together between December 2015 and February 2020, and the last change to the data files was in February 2020, so new or changed codes since then are not included.

There are two files. Both use Windows line endings (CRLF).

`data/iso-container-codes.csv` has 716 rows, one per size and type code, with 5 columns:

| Column | Meaning |
|---|---|
| `code` | The 4-character ISO 6346 size and type code, for example `22G1`. The first character is the length, the second is the width and height (coded), and the last two describe the type. Not every code starts with two digits (see the limitations). `code` is not unique |
| `description` | The container type in words, for example `Dry Bulk` |
| `length` | External length in feet. `0` means none is given |
| `height` | External height in feet, for example `8.5` or `9.5`. `0` means none is given |
| `group` | The code of the group the container belongs to. These are the codes in `data/iso-container-groups.csv`, and they are the codes used in electronic shipping messages |

`data/iso-container-groups.csv` has 28 rows with 2 columns, `code` (unique) and `description`, for example `20 BULK CONTAINER`.

### Known limitations

These are in the data as committed and have not been changed:

* `code` is not unique: `42HR` appears in two rows, once with group `42HR` ("Insulated (Conair)") and once with group `42RT`.
* 45 codes start with a letter (for example `L5G0`, `M2G0`) and 3 have a letter second (`4CG0`, `4CG1`, `4CGP`).
* The group codes `42TN` (33 rows) and `L5RT` (29 rows) are used in `iso-container-codes.csv` but are not in `iso-container-groups.csv`. The groups file instead has `42TD` and `L5R1`, which no row uses as a group.
* Where a code starts with `4`, the length column is normally `40`. 13 rows say `45` (for example `45R0`, `45H2`) and `45G4` says `0`. Other rows have an odd length for their code (`3399` has length 23, `2650` has length 0, `12TR` has length 42).
* The description of group `22BU` ends with a tab character.
* The data is not complete or checked against the current standard. It was made before ISO 6346:2022 was published.
* Where each row comes from is not recorded (see Data sources).
* The codes are text, as `datapackage.json` says. Some are made only of digits (for example `3399`). With pandas, read them as text: `pd.read_csv("data/iso-container-codes.csv", dtype=str)`.

## Data sources

There is no script and no record of how the rows were made. This is what we could establish.

* [Container Container][cc], a shipping container sales company (now Parsons Containers). The group list in `iso-container-groups.csv` matches the table on this page for most groups, with a length number added at the front of each description. Most of the rows in `iso-container-codes.csv` are not on this page, and the page has no length or height. Licence: unclear (see [License](#license)).
* [Wikipedia, "ISO 6346"][wp] has a table of size and type codes with the same codes as the Container Container table. We could not establish whether any rows were taken from it. Licence: [CC BY-SA 4.0][ccbysa], if rows were taken (see [License](#license)).
* [shippingcontainers24.com][sc24] has the same list. The original page is gone; the link is to an Internet Archive copy. We could not establish whether it was used. Licence: unclear (we found no terms).
* [ISO 6346:2022][iso], the standard (paid; the ISO site refuses scripts, so this link could not be checked automatically). The [BIC (Bureau International des Containers) page on size and type codes][bic] explains the structure of the codes. The size and type code list is part of the standard. We could not establish whether rows here come from it. Licence: unclear (ISO says reproduction needs its written permission).

Changes made to the source data: not recorded. The Container Container table has no length or height columns, and the group descriptions here have a length number added at the front. We could not tell where the length and height values come from, or how the other rows were made.

Not endorsed by, or affiliated with, Container Container, Parsons Containers, Wikipedia, ISO or BIC.

[cc]: https://www.containercontainer.com/iso6346/
[wp]: https://en.wikipedia.org/wiki/ISO_6346
[ccbysa]: https://creativecommons.org/licenses/by-sa/4.0/
[sc24]: https://web.archive.org/web/20161028170916/http://www.shippingcontainers24.com/general/iso-6346-codes/
[iso]: https://www.iso.org/standard/83558.html
[bic]: https://www.bic-code.org/size-type-code/

## Preparation

The data is edited by hand in the two CSV files. There is no script and no GitHub workflow that changes them. Keep the CRLF line endings and the column order when editing, and update `datapackage.json` if columns change.

## License

The licence of this data is unclear. What we checked:

* Container Container: the page of the ISO 6346 table has no licence. Its footer said "All rights reserved" in 2015 and now says "Copyright © Parsons Containers". We found no permission to copy the table.
* Wikipedia: its text is under CC BY-SA 4.0, which would need credit and sharing under the same licence. That does not fit the PDDL. We could not establish whether its table was used.
* ISO: ISO says all its publications are protected by copyright and that "any use, including reproduction requires our written permission". We could not read the paid standard to compare it with these rows.
* shippingcontainers24.com: we found no terms.

We could not establish where most of the rows come from, so we cannot say whether they may be released under an open licence. Do not rely on this data being in the public domain. If you plan to use it commercially, check the terms of the sources above first.

The maintainers place only their own work (for example the selection and arrangement of the rows and the CSV format) under the [Public Domain Dedication and License (PDDL)](https://opendatacommons.org/licenses/pddl/1.0/). This does not cover the sources above. See also [ATTRIBUTION.txt](ATTRIBUTION.txt).
