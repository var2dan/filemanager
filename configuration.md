---
layout: page
title: Configuration
permalink: /configuration/
---

File Manager can work either via a command line interface, with flags, or through a configuration file, which can be either in JSON, YAML or TOML.

## Flags

This meaning of each flag is transcendant to the correspondant options in the configuration files. Here are the configurations to the **File Manager itself**:

- ```-a, --address``` is the address to listen to. Defaults to "" (empty string, all of the addresses).
- ```-c, --config``` specifies a configuration file.
- ```-d, --database```is the path to the database file. Defaults to "./filemanager.db".
- ```-l, --log``` indicates the error logger; it can be 'stdout', 'stderr' or a file path. Defaults to "stdout".
- ```-p, --port``` is the port to listen to. Defaults 0 (random free port).
- ```--plugin``` specifies if you want to enable a plugin.
- ```-v, --version``` prints the version of the executable.

These options are used to set the default values for new users:

- ```--allow-commands``` is the default value for allow commands option. Defaults to true.
- ```--allow-edit``` is the default value for allow edit option. Defaults to true.
- ```--allow-new``` is the default value for allow new option. Defaults to true.
- ```--commands``` is a space separated string with the available commands for new users. Defaults to "git svn hg".
- ```--no-auth``` disables the authentication. Using this option, the default values will be used for the permissions.
- ```-s, --scope``` is the default scope for new users. Defaults to the working directory.

So, if you wanted to run File Manager on port 80, with the database on `/etc/fm.db` and the default scope to `/data`, you would run:

```
filemanager --port 80 --database /etc/fm.db --scope /data
```

## Configuration File

By default, File Manager will try to find a file named "filemanager.yaml", "filemanager.toml" or "filemanager.json" on the current working directory to use as its configuration file. If you want to use another file, you only need to specify the `-c` flag with its path.

Here is a specimen of a JSON configuration file:

```json
{
  "port": 80,
  "noAuth": false,
  "address": "127.0.0.1",
  "database": "/path/to/database.db",
  "log": "stdout",
  "plugin": "",
  "scope": "/path/to/my/files",
  "allowCommands": true,
  "allowEdit": true,
  "allowNew": true,
  "commands": [
    "git",
    "svn"
  ]
}
```

In YAML:

```yaml
port: 80
noAuth: false
address: 127.0.0.1
database: "/path/to/database.db"
log: stdout
plugin: ''
scope: "/path/to/my/files"
allowCommands: true
allowEdit: true
allowNew: true
commands:
- git
- svn
```

In TOML:

```toml
port = 80
address = 127.0.0.1
noAuth = false
database = "/path/to/database.db"
log = stdout
plugin = ''
scope = "/path/to/my/files"
allowCommands = true
allowEdit = true
allowNew = true
commands = ["git", "svn"]
```