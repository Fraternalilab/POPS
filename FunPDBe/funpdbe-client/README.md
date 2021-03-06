FunPDBe Deposition Client
=====

The client can be used to connect to the FunPDBe deposition system API, and perform GET, POST, PUT and DELETE calls. Making calls to the deposition API require authentication.

Quick start
-----------

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

There are no prerequisites for installing the client. Please note that the client is written in Python3, and the dependencies have to be installed accordingly (for example by using pip3)!

### Installing

The are two main approaches to getting the client up and running.

#### Checking out this repository

```
$ git clone git@gitlabci.ebi.ac.uk:pdbe-kb/funpdbe/funpdbe-client.git
$ cd funpdbe-client
$ pip3 install -r requirements.txt
```

## Using as module import

The client can be used by importing the "Plugin" module within a Python script. This makes it easier to push JSON data that is generated by a pipeline, i.e. there is no need to save the data as JSON files.

The Plugin() class requires three variable:

* user name
* password
* data (in JSON/dictionary format)

The .post() method of the Plugin() class has one optional parameter:

* update (False by default, if True then it will overwrite the previous entry)

Example of using from a module:

```
from funpdbe_client.plugin import Plugin

plugin = Plugin("your_user_name", "your_password", your_data_in_json)
plugin.post(update=True) # This will overwrite an existing entry
```

## Using from command line

Examples of usage:

```
$ ./funpdbe_client.py
```

### Parameters

* -h, --help:       Help (this is what you see now)
* -u, --user:       FunPDBe user name
* -p, --pwd:        FunPDBe password
* -m, --mode:       Running mode (get, post, delete, put, validate)
* -i, --pdbid:      PDB id of an entry
* -r, --resource:   Name of a resource
* -f, --path:       Path to JSON file (.json ending), or files (folder name)
* -d, --debug:      Enable more detailed logging

### Examples

#### Validating JSON file against schema

This is one of the main uses of the client, i.e. to validate a JSON file against the FunPDBe schema. This functionality requires no authentication.

```
$ ./funpdbe_client.py --path=path/to/file.json --mode=validate
```

#### Listing entries from "resource_name"

This call will list all the entries currently deposited in "resource_name". Permission is required to view depositions. NB: The client is for deposition, not data retrieval.

```
$ ./funpdbe_client.py --user=username --pwd=password --mode=get --resource=resource_name
```

#### Listing entry for PDB id "pdb_id" from "resource_name"

This call will give a detailed view for a particular entry "pdb_id" from a specific resource "resource_name"

```
$ ./funpdbe_client.py --user=username --pwd=password --mode=get --pdb_id=pdb_id --resource=resource_name
```

#### Posting an entry to "resource_name"
```
$ ./funpdbe_client.py --user=username --pwd=password --mode=post --path=path/to/data.json --resource=resource_name
```

#### Deleting an entry ("pdb_id") from "resource_name"
```
$ ./funpdbe_client.py --user=username --pwd=password --mode=delete --pdb_id=pdb_id --resource=resource_name
```

#### Updating an entry ("pdb_id) from "resource_name"
```
$ ./funpdbe_client.py --user=username --pwd=password --mode=put --path=path/to/data.json --resource=resource_name --pdb_id=pdb_id
```

## Running the tests

Running tests for the client is performed simply by using
```
$ pytest
```

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the tags.

## Authors

* **Mihaly Varadi** - *Initial work* - [mvaradi](https://gitlab.ebi.ac.uk/mvaradi)

## License

This project is licensed under the EMBL-EBI License - see the [LICENSE](LICENSE) file for details

## Acknowledgments

We would like to thank the PDBe team for their support and feedback, as well as all the members of the FunPDBe consortium:

* PDBe team - [team website](https://www.ebi.ac.uk/services/teams/pdbe)
* Orengo team - [CATH](http://www.cathdb.info/)
* Vranken team - [DynaMine](http://dynamine.ibsquare.be/)
* Barton team - [NoD](http://www.compbio.dundee.ac.uk/www-nod/)
* Wass team - [3DLigandSite](http://www.sbg.bio.ic.ac.uk/3dligandsite/)
* Blundell team - [CREDO](http://marid.bioc.cam.ac.uk/credo)
* Fraternali team - [POPSCOMP](https://mathbio.crick.ac.uk/wiki/POPSCOMP)
