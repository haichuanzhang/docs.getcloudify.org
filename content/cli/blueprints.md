---
layout: bt_wiki
title: blueprints
category: Docs
draft: false
abstract: Cloudify's Command-Line Interface
weight: 20
---

The `cfy blueprints` command is used to manage blueprints on a Cloudify manager.

You can use the command to upload, delete, download, validate and list blueprints and to retrieve information for a specific blueprint.


## Commands

### upload

Usage: `cfy blueprints upload [options] BLUEPRINT_ID`

Upload a blueprint to a manager. 

#### Required flags

*  `BLUEPRINT_PATH` -   The path to the application's blueprint file.
                        (default: blueprint.yaml)

#### Optional flags

* `-b, --blueprint-id=BLUEPRINT_ID` - 
                        A user provided blueprint ID

* `-n, --blueprint-filename TEXT` -  
                        The name of the archive's main blueprint
                        file. This is only relevant if uploading an
                        archive

* `--validate` -                                
                        Validate the blueprint before uploading it to the
                        manager
* `-v, --verbose` -     Show verbose output. You can supply this up
                        to three times (i.e. -vvv)
* `-h, --help` -       Show this message and exit.

&nbsp;
#### Example

```markdown
$ cfy blueprints upload simple-python-webserver-blueprint/blueprint.yaml
...

blueprint.yaml 
Uploading blueprint simple-python-webserver-blueprint/blueprint.yaml...
 blueprint.yaml |######################################################| 100.0%
Blueprint uploaded. The blueprint's id is simple-python-webserver-blueprint

...

$ cfy blueprints upload simple-python-webserver-blueprint/blueprint.yaml --validate
...

Validating blueprint: simple-python-webserver-blueprint/blueprint.yaml
Blueprint validated successfully
Uploading blueprint simple-python-webserver-blueprint/blueprint.yaml...
 blueprint.yaml |######################################################| 100.0%
Blueprint uploaded. The blueprint's id is simple-python-webserver-blueprint

...
```

### delete

Usage: `cfy blueprints delete BLUEPRINT_ID` 

Delete a blueprint. It's important to note that deleting a blueprint does not mean deleting the deployments created from that blueprint and resources of those deployments.

#### Optional flags

*  `-v, --verbose` -    Show verbose output. You can supply this up to three times
                        (i.e. -vvv)
*  `-h, --help` -       Show this message and exit.

&nbsp;
#### Example

```markdown
$ cfy blueprints delete simple-python-webserver-blueprint
...

Deleting blueprint simple-python-webserver-blueprint...
Blueprint deleted

...
```


### download

Usage: `cfy blueprints download [options] BLUEPRINT_ID`

Download a blueprint from the manager.

#### Required flags

*  `BLUEPRINT_ID` -     is the id of the blueprint to download.

#### Optional flags

*  `-o, --output-path TEXT` -
                        The local path to download to
*  `-v, --verbose` -    Show verbose output. You can supply this up to three
                        times (i.e. -vvv)
*  `-h, --help` -       Show this message and exit.

&nbsp;
#### Example

```markdown
$ cfy blueprints download simple-python-webserver-blueprint
...

Downloading blueprint simple-python-webserver-blueprint...
 simple-python-web... |################################################| 100.0%
Blueprint downloaded as simple-python-webserver-blueprint.tar.gz

...
```


### validate

Usage: `cfy blueprints validate BLUEPRINT_PATH` 

Validate a blueprint. This checks that the blueprint's syntax is valid and that all imports are accessible.

{{% gsNote title="Note" %}}
Import validation is done only on the client side. That means that if, for some reason, the imports are accessible by the client but not on the manager, this validation will still pass.
{{% /gsNote %}}

#### Required flags

*  `BLUEPRINT_PATH` -   The path to the application's blueprint file.
                        (default: blueprint.yaml)

#### Optional flags

*  `-v, --verbose` -    Show verbose output. You can supply this up to three
                        times (i.e. -vvv)
*  `-h, --help` -       Show this message and exit.

&nbsp;
#### Example

```markdown
$ cfy blueprints validate simple-python-webserver-blueprint/blueprint.yaml
...

Validating blueprint: simple-python-webserver-blueprint/blueprint.yaml
Blueprint validated successfully

...
```

### list

Usage: `cfy blueprints list`

List all existing blueprints.

&nbsp;
#### Example

```markdown
$ cfy blueprints list
...

Listing all blueprints...

Blueprints:
+-----------------------------------+-------------+----------------+--------------------------+--------------------------+
|                 id                | description | main_file_name |        created_at        |        updated_at        |
+-----------------------------------+-------------+----------------+--------------------------+--------------------------+
|               simple              |             | blueprint.yaml | 2016-08-02 11:02:51.562  | 2016-08-02T11:02:51.562Z |
| simple-python-webserver-blueprint |             | blueprint.yaml | 2016-08-02 11:10:15.527  | 2016-08-02T11:10:15.527Z |
+-----------------------------------+-------------+----------------+--------------------------+--------------------------+

...
```

### get

Usage: `cfy blueprints get BLUEPRINT_ID`

Retrieve information for a single blueprint.

#### Required flags

*  `BLUEPRINT_ID` -     A user provided blueprint ID

#### Optional flags

*  `-v, --verbose` -    Show verbose output. You can supply this up to three
                        times (i.e. -vvv)
*  `-h, --help` -       Show this message and exit.

&nbsp;
#### Example

```markdown
$ cfy blueprints get simple-python-webserver-blueprint
...

Retrieving blueprint simple-python-webserver-blueprint...

Blueprint:
+-----------------------------------+----------------+--------------------------+--------------------------+--------------+
|                 id                | main_file_name |        created_at        |        updated_at        | #deployments |
+-----------------------------------+----------------+--------------------------+--------------------------+--------------+
| simple-python-webserver-blueprint | blueprint.yaml | 2016-08-02 11:19:02.177  | 2016-08-02T11:19:02.177Z |      1       |
+-----------------------------------+----------------+--------------------------+--------------------------+--------------+

Description:


Existing deployments:
["simple-python-webserver-blueprint"]
...
```

### inputs

Usage: `cfy blueprints inputs -b BLUEPRINT_ID`

Lists all inputs for a blueprint. Note that not every blueprint has inputs.

#### Required flags

*  `BLUEPRINT_ID` -     A user provided blueprint ID

#### Optional flags

*  `-v, --verbose` -    Show verbose output. You can supply this up to three
                        times (i.e. -vvv)
*  `-h, --help` -       Show this message and exit.

&nbsp;
#### Example

```markdown
$ cfy blueprints inputs simple-python-webserver-blueprint
...

Retrieving inputs for blueprint simple-python-webserver-blueprint...

Inputs:
+----------------+------+-----------+---------------------------+
|      name      | type |  default  |        description        |
+----------------+------+-----------+---------------------------+
| webserver_port |  -   |    8000   | The HTTP web server port. |
|                |      |           |                           |
|    host_ip     |  -   | localhost |             -             |
+----------------+------+-----------+---------------------------+

...
```