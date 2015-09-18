# Vagrant-based Ghost Blog Deployment

## The Purpose

For testing the latest version of Ghost in an isolated environment on a local system. Good for pre-production work like theme designing.

## System Requirements

* Vagrant
* VirtualBox

## Usage

Since this is a git repo, it's best to pull it down via git:

```git clone https://github.com/jelyman2/vagrant-ghost && vagrant up```

I've tested this deployment on OS X. I expect Linux and Windows to be the same. As of the release of this repo, `sqlite3` does not compile properly via `NPM` unless specific versions of `GCC` and `G++`` are specified via environment variables. As such, I've included this command in the `Vagrantfile`:

```CC=gcc-4.9 CXX=g++-4.9 npm install sqlite3```

## Accessing Ghost

After Vagrant finishes provisioning, browse to http://10.10.10.11.

## The Technical Stuff

- Ports (internal/external): `80:80`
- RAM: `512MB`

## License

The MIT license is in effect here. Do with this repo whatever you wish. Fork the hell out of it and make it awesome!
