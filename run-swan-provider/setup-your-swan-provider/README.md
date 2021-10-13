# Setup Your Swan Provider

nstall Swan ProviderSwan provider contains two major componentA download utility(aria2) for downloading .car files from remote server

* A .car file manager for managing importer process

Install aria2sudo apt install aria2Install Swan Provider BinaryThe Swan Provider is a binary that is created from therepository.It contains both the logic for running an Swan Provider and also provides a CLI for handling registry, staking and other operations.wget https://github.com/filswan/go-swan-provider/releases/download/release-0.1.0-beta-rc1/install.shchmod +x ./install.shsudo ./install.shThe Swan Provider is currently only supported on x86\_64 Linux systems.Building From SourceAlthough highly suggested, building from source is currently beyond the scope of this documentation.Seedocumentation for more details.The code in themight be incompatible with the code used by other nodes in the production.Make sure to use the version specified in the release.
