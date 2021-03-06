[![Build Status](https://travis-ci.org/futres/fovt.svg?branch=master)](https://travis-ci.org/futres/fovt)
[![DOI](https://zenodo.org/badge/13996/futres/fovt.svg)](https://zenodo.org/badge/latestdoi/13996/futres/fovt)

# FuTRES Ontology of Vertebrate Traits (FOVT)

This ontology is to map measurable vertebrate traits. We leverage the BioCollections Ontology ([BCO](http://purl.obofoundry.org/ontology/bco.owl)) to link observations of individual specimens to their trait values. Traits are defined in the Ontology of Biological Attributes ([OBA](http://purl.obofoundry.org/ontology/oba.owl)).

More information on the ontology can be found at http://obofoundry.org/ontology/fovt (once ontology is registered).

More information on FuTRES is available at https://futres.org/.

## Workflow

1. Check if needed parts of term are in UBERON or OBA. 
2. Add needed part of term to UBERON (7500000-7999999).
3. Import and add terms to OBA.
4. Import terms to FOVT, and import to <a href="https://geome-db.org/workbench/template"> GEOME</a> see @JDeck88.

## Term Requests

New term requests can be made by creating an issue. 

Please provide:
1. anatomical feature
2. anatomical points and/or anatomical axis
3. measurement (e.g., width, length, etc.)
4. reference for measurement

## Versions

### Stable release versions

The latest version of the ontology can always be found at:

http://purl.obolibrary.org/obo/fovt.owl

(note this will not show up until the request has been approved by obofoundry.org)

### Editors' version

Editors of this ontology should use the edit version, [src/ontology/fovt-edit.owl](src/ontology/fovt-edit.owl)

## Contact

Please use this GitHub repository's [Issue tracker](https://github.com/futres/fovt/issues) to request new terms/classes or report errors or specific concerns related to the ontology.

## Acknowledgements

FuTRES is funded by the National Science Foundation grant #

This ontology repository was created using the [ontology starter kit](https://github.com/INCATools/ontology-starter-kit)
