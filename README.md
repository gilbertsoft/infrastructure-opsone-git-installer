# GIT Installer Script (GIS)

The GIT Installer Script makes a simple cloning and setup of a git repository to
the user home or any sub directory on an [OpsOne Managed Server PaaS](https://opsone.ch/hosting/managed-server)
possible.

## Installation

The installation can easiely be done via the global server configuration by
adding this `Custom JSON`:

```json
{
  "globalrepo::repo": {
    "git-installer": {
      "source": "https://github.com/gilbertsoft/infrastructure-opsone-git-installer.git",
      "revision": "main",
      "exec_after": "sudo ./setup"
    }
  }
}
```

## Usage

### Configuration

Browse to the [OpsOne Cockpit](https://cockpit.opsone.ch) and add the following
configuration:

* `Custom JSON`:

  ```json
  {
    "envvar": {
      "GIS_REPOSITORY": "https://github.com/gilbertsoft/infrastructure-opsone-erpnext.git",
      "GIS_BRANCH": "main",
      "GIS_DESTINATION": "",
      "GIS_SETUP": "setup",
      "GIS_SETUP_OPTIONS": ""
    }
  }
  ```

Alternatively you can add the environment variables via `~/cnf/environment`. Do
not forget to relogin to the server afterwards.

The third option is to provide various `.env` files which will be loaded
automatically. Several `.env` files are available to set environment variables
in just the right situation:

* `.env`: defines the default values of the env vars.
* `.env.local`: overrides the default values for all contexts but only on the
  machine which contains the file. This file should not be committed to the
  repository.
* `.env.<context>` (e.g. `.env.STAGE`): overrides env vars only for one
  contexts but for all machines (these files are committed).
* `.env.<context>.local` (e.g. `.env.STAGE.local`): defines machine-specific
  env var overrides only for one contexts. It’s similar to `.env.local`, but
  the overrides only apply to one contexts.

Valid contexts are:

* `PROD`
* `STAGE`
* `DEV`

#### GIS_REPOSITORY (mandatory)

Defines the repository to be cloned e.g. `https://github.com/gilbertsoft/infrastructure-opsone-erpnext.git`.

#### GIS_BRANCH

Defines the branch of the repository to be cloned. Defaults to `main`.

#### GIS_DESTINATION

Defines the destination directory to be used. If not set the repository gets
cloned to the user home.

#### GIS_SETUP

Defines the setup script to be called after the cloning if found. Defaults to
`setup`.

#### GIS_SETUP_OPTIONS

Defines the options passed to the setup script. Defaults to none.

### Run the Installer

After the configuration you can run `gis` via SSH to get the configured
repository cloned and setted up.

For more information about the possible options run `gis --help`.

## Contact & Communication

### Contributing

Feel free to fork this project and create a pull request when you're happy
with your changes.

### Bug reporting

Please open an [issue at github](https://github.com/gilbertsoft/infrastructure-opsone-git-installer/issues)
and describe your problem.

## License

This project is released under the terms of the [GNU GENERAL PUBLIC LICENSE](LICENSE).
