---
title: BaseSpace
parent: Data management
---

# Principles

- Machine readable
    - Avoid special characters ()?\!@\*%{[<> and spaces
    - Hyphens - and underscores _ can be used to separate related and unrelated chunks, respectively
        - Underscore separates units of metadata, hyphen separates related words
    - Case-sensitive: use lowercase when possible
- Human readable
    - Descriptive identifiers (slugs) 
- Promotes useful default ordering
    - Dates in ISO 8601 format (YYYYMMDD)
    - Left padded numbers for cardinal ordering (01, 02)
    - Semantic versioning (vX.Y.Z)

# Rules for file naming


## Additional guidelines

- Use the researcher’s name/initials
- Use the version number of file (v001, v002) or language used in the document (ENG)
- Do not make file names too long (this can complicate file transfers)
- Avoid personal data in file names

# Resources

[MIT file and folder naming guidelines](https://libraries.mit.edu/data-management/store/organize/)
[The Turing way for data organization](https://book.the-turing-way.org/reproducible-research/rdm/rdm-storage#rr-rdm-storage-organisation)