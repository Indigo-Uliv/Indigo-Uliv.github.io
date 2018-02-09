# Indigo Command Line Interface


## Presentation

The [Indigo Command Line Interface](https://github.com/Indigo-Uliv/indigo-cli)
is a client project written in Python that can be installed on any machine. It accesses an Indigo cluster through its RESTful APIs (CDMI and Admin interface).


## Installation

### Create And Activate A Virtual Environment

```
$ virtualenv ~/ve/indigo/cli-1.2
...
$ source ~/ve/indigo/cli-1.2/bin/activate
```

### Clone the indigo-cli project

```
$ git clone https://github.com/Indigo-Uliv/indigo-cli.git
$ cd indigo-cli
```

### Install Dependencies

```
$ pip install -r requirements.txt
```

### Install Indigo Client

```
$ pip install -e .
```

### Detailed OSX install  commands

```
$ sudo easy_install virtualenv      # virtualenv installs pip
$ python -m virtualenv ~/ve/indigoclient-1.2
$ source ~/ve/indigoclient-1.2/bin/activate
$ pip install -r requirements.txt
$ pip install -e .
```

## Usage

Don't forget to activate the virtual environment which has been created during
install. It will provide the _**indigo**_ command.

```
$ source ~/ve/indigo/cli-1.2/bin/activate
```

## Commands

### Connection

* Connect to an Indigo Cluster as an anonymous user

```
$ indigo init --url=http://indigo.example.com
```

* Connect to an Indigo Cluster as a registered user

```
$ indigo init --url=http://indigo.example.com --username=USER [--password=PASS]
```

* Disconnect from the cluster

```
$ indigo exit
```

* Show current authenticated user

```
$ indigo whoami
```

### Manage Collections and Data Objects

* Show current working container

```
$ indigo pwd
```

* List a container

```
$ indigo ls <path>
```

* List a container with ACL information

```
$ indigo ls -a <path>
```

* Move to a new container

```
$ indigo cd <path>
```

* Move to the parent container

```
$ indigo cd ..
```

* Create a new container

```
$ indigo mkdir <path>
```

* Put a local file

```
$ indigo put <src> [<dst>]
```

* Create a reference object

```
$ indigo put --ref <url> <dest>
```

* Provide the MIME type of the object (if not supplied
  ``indigo put`` will attempt to guess)

```
$ indigo put --mimetype="text/plain" <src>
```

* Fetch a data object from the archive to a local file

```
$ indigo get [--force] <src> [<dst>]
```

* Get the CDMI json dict for an object or a container

```
$ indigo cdmi <path>
```

* Remove an object or a container

```
$ indigo rm <src>
```

* Add or modify an ACL to an object or a container

```
$ indigo chmod <path> (read|write|null) <group>
```

### Manage Metadata


* Set (overwrite) a metadata value for a field

```
$ indigo meta set <path> "org.dublincore.creator" "S M Body"
$ indigo meta set . "org.dublincore.title" "My Collection"
```

* Add another value to an existing metadata field

```
$ indigo meta add <path> "org.dublincore.creator" "A N Other"
```

$ List metadata values for all fields

```
$ indigo meta ls <path>
```

* List metadata value(s) for a specific field

```
$ indigo meta ls <path> org.dublincore.creator
```

* Delete a metadata field

```
$ indigo meta rm <path> "org.dublincore.creator"
```

* Delete a specific metadata field with a value

```
$ indigo meta rm <path> "org.dublincore.creator" "A N Other"
```

### Manage Users and Groups

* Create a user

```
$ iadmin mkuser <username>
```

* List all users

```
$ iadmin lu
```

* Display information on a specific user

```
$ iadmin lu <username>
```

* Modify a user

```
$ iadmin moduser <username> (email | administrator | active | password) [<value>]
```

For instance to change the email of the user user10

```
$ iadmin moduser user10 email user10@indigo.com
```

* Remove a user

```
$ iadmin rmuser <username>
```

* Create a group

```
$ iadmin mkgroup <groupname>
```

* List all groups

```
$ iadmin lg
```

* Display information on a specific group

```
$ iadmin lg <groupname>
```

* Add user(s) to a group

```
$ iadmin atg <groupname> <userlist> ...
```

* Remove user(s) from a group

```
$ iadmin rfg <groupname> <userlist> ...
```

* Remove a group

```
$ iadmin rmgroup <groupname>
```
