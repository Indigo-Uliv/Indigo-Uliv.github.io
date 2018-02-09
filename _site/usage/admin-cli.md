# Admin Command Line Interface


## Presentation

When installed, the Indigo lib provides a minimal set of commands
that can be used to configure the system. They have to be executed
on an installed Indigo node.


## Commands

### Initialise Cassandra

This command has to be executed once to set up the keyspace and the tables in
Cassandra.

```
$ iadmin create
```

### Create a user

```
$ iadmin mkuser <username>
```

### List existing users

* List all users

```
$ iadmin lu
```

* Display information on a specific user

```
$ iadmin lu <username>
```

### Modify a user

```
$ iadmin moduser <username> (email | administrator | active | password) [<value>]
```

For instance to change the email of the user user10

```
$ iadmin moduser user10 email user10@indigo.com
```

### Remove a user

```
$ iadmin rmuser <username>
```

### Create a group

```
$ iadmin mkgroup <groupname>
```

### List existing groups

* List all groups

```
$ iadmin lg
```

* Display information on a specific group

```
$ iadmin lg <groupname>
```

### Add user(s) to a group

```
$ iadmin atg <groupname> <userlist> ...
```

### Remove user(s) from a group

```
$ iadmin rfg <groupname> <userlist> ...
```

### Remove a group

```
$ iadmin rmgroup <groupname>
```
