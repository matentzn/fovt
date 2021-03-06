These notes are for the EDITORS of fovt

This project was created using the [ontology development kit](https://github.com/INCATools/ontology-development-kit). See the site for details.

For more details on ontology management, please see the [OBO tutorial](https://github.com/jamesaoverton/obo-tutorial) or the [Gene Ontology Editors Tutorial](https://go-protege-tutorial.readthedocs.io/en/latest/)

You may also want to read the [GO ontology editors guide](http://go-ontology.readthedocs.org/)

## Requirements

 1. Protege (for editing)
 2. A git client (we assume command line git)
 3. [docker](https://www.docker.com/get-docker) (for managing releases)

## Editors Version

Make sure you have an ID range in the [idranges file](fovt-idranges.owl)

If you do not have one, get one from the maintainer of this repo.

The editors version is [fovt-edit.owl](fovt-edit.owl)

** DO NOT EDIT fovt.obo OR fovt.owl in the top level directory **

[../../fovt.owl](../../fovt.owl) is the release version

To edit, open the file in Protege. First make sure you have the repository cloned, see [the GitHub project](https://github.com/futres/fovt) for details.

You should discuss the git workflow you should use with the maintainer
of this repo, who should document it here. If you are the maintainer,
you can contact the odk developers for assistance. You may want to
copy the flow an existing project, for example GO: [Gene Ontology
Editors Tutorial](https://go-protege-tutorial.readthedocs.io/en/latest/).

In general, it is bad practice to commit changes to master. It is
better to make changes on a branch, and make Pull Requests.

## ID Ranges

These are stored in the file

 * [fovt-idranges.owl](fovt-idranges.owl)

** ONLY USE IDs WITHIN YOUR RANGE!! **

If you have only just set up this repository, modify the idranges file
	and add yourself or other editors. Note Protege does not read the file
- it is up to you to ensure correct Protege configuration.


### Setting ID ranges in Protege

We aim to put this up on the technical docs for OBO on http://obofoundry.org/

For now, consult the [GO Tutorial on configuring Protege](http://go-protege-tutorial.readthedocs.io/en/latest/Entities.html#new-entities)

## Imports

All import modules ready for release are in the root [imports/](../../imports/) folder.

Each ontology that you want to import from must be specified in the makefile. This is done automatically when you set up the repo with ODK, but if you want to import from a new ontology, you need to add it to the makefile in several places.

Terms to be imported from each ontology are in text files in the src directory under /fovt/src/ontology/imports, e.g., /fovt/src/ontology/imports/iao_terms.txt.

Note: the $ontology_terms.txt files created by ODK may include 'starter' classes seeded from
the ontology starter kit. These were removed and replaced with the terms BCO needs to import.

Import files for edit version are stored under /bco/src/ontology/imports. To make the import files while editing, run `sh ./run.sh make all_imports` from within /fovt/src/ontology. This stores the new files in `/fovt/src/ontology/imports` with today's data in the release IRI.

To make import files for a release, run `sh run.sh make prepare_release`. This checks for newer versions of the import source ontologies and stores them locally, then creates new import files (unless you have specified otherwise in your makefile) which are stored at `/fovt/imports`.

## Release

1. Run reasoner and save changes to edit.owl in Protégé 
2. Navigate to src/ontology
3. On GitHub Desktop, create and switch to a new branch; label it the release version (be sure to bring all changes over to that new branch)
4. Run `sh run.sh make prepare_release`
5. Commit and push changes on GitHub Desktop
6. Create a pull request
7. On github.com/futres/fovt, switch to master branch and merge pull request
8. Create a new release with tag labled "vYYYY-MM-DD"

### Error messages

_Error 1_
* Open Protégé
* Navigate to Entities, switch to inferred
* Click on "owl:Thing" to get to "owl:Nothing"
* On the bar "Description: owl:Nothing" click the "?" square
* Run and stop after it finds 1 error
* Look at the disjoint axiom and explanation
* Save to edit.owl in Protégé

## Design patterns

You can automate (class) term generation from design patterns by placing DOSDP
yaml file and tsv files under src/patterns. Any pair of files in this
folder that share a name (apart from the extension) are assumed to be
a DOSDP design pattern and a corresponding tsv specifying terms to
add.

Design patterns can be used to maintain and generate complete terms
(names, definitions, synonyms etc) or to generate logical axioms
only, with other axioms being maintained in editors file.  This can be
specified on a per-term basis in the TSV file.

Design pattern docs are checked for validity via Travis, but can be
tested locally using

`./run.sh make patterns`

In addition to running standard tests, this command generates an owl
file (`src/patterns/pattern.owl`), which demonstrates the relationships
between design patterns.

(At the time of writing, the following import statements need to be
added to `src/patterns/pattern.owl` for all imports generated in
`src/imports/*_import.owl`.   This will be automated in a future release.')

To compile design patterns to terms run:

`./run.sh make ../patterns/definitions.owl`

This generates a file (`src/patterns/definitions.owl`).  You then need
to add an import statement to the editor's file to import the
definitions file.


## Release Manager notes

You should only attempt to make a release AFTER the edit version is
committed and pushed, AND the travis build passes.

These instructions assume you have
[docker](https://www.docker.com/get-docker). This folder has a script
[run.sh](run.sh) that wraps docker commands.

to release:

first type

    git branch

to make sure you are on master

    cd src/ontology
    sh ./build.sh

If this looks good type:

    sh ./prepare_release.sh

This generates derived files such as fovt.owl and fovt.obo and places
them in the top level (../..).

Note that the versionIRI value automatically will be added, and will
end with YYYY-MM-DD, as per OBO guidelines.

Commit and push these files.

    git commit -a

And type a brief description of the release in the editor window

Finally type:

    git push origin master

IMMEDIATELY AFTERWARDS (do *not* make further modifications) go here:

 * https://github.com/futres/fovt/releases
 * https://github.com/futres/fovt/releases/new

__IMPORTANT__: The value of the "Tag version" field MUST be

    vYYYY-MM-DD

The initial lowercase "v" is REQUIRED. The YYYY-MM-DD *must* match
what is in the `owl:versionIRI` of the derived fovt.owl (`data-version` in
fovt.obo). This will be today's date.

This cannot be changed after the fact, be sure to get this right!

Release title should be YYYY-MM-DD, optionally followed by a title (e.g. "january release")

You can also add release notes (this can also be done after the fact). These are in markdown format.
In future we will have better tools for auto-generating release notes.

Then click "publish release"

__IMPORTANT__: NO MORE THAN ONE RELEASE PER DAY.

The PURLs are already configured to pull from github. This means that
BOTH ontology purls and versioned ontology purls will resolve to the
correct ontologies. Try it!

 * http://purl.obolibrary.org/obo/fovt.owl <-- current ontology PURL
 * http://purl.obolibrary.org/obo/fovt/releases/YYYY-MM-DD.owl <-- change to the release you just made

For questions on this contact Chris Mungall or email obo-admin AT obofoundry.org

# Requesting an OBO Foundry PURL

This only needs to be done once, but you may need to edit the metadata or yaml files during the life of the ontology.

Instructions for requesting the namespace and PURL are at https://github.com/futres/fovt/tree/master/src/metadata.

# License

The repo does not come with a license. To add one, in the home directory, create a new file called LICENSE. Once you have named the file, GitHub will automatically offer you the option to choose a license. We have chosen CC0. Be sure to update ../metadata/fovt.md with the correct license information.

# Travis Continuous Integration System

Check the build status here: [![Build Status](https://travis-ci.org/futres/fovt.svg?branch=master)](https://travis-ci.org/futres/fovt)

Note: if you have only just created this project you will need to authorize travis for this repo.

 1. Go to [https://travis-ci.org/profile/futres](https://travis-ci.org/profile/futres)
 2. click the "Sync account" button
 3. Click the tick symbol next to fovt

Travis builds should now be activated
