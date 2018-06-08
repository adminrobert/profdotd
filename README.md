# ProfDotD

Organized profile sharing

## Premise

Profiles can get a bit messy at times specifically when trying to share certain pieces of profiles with a team. This project aims to make things a little easier to keep track of different aspects of your profile.

## Getting started

Clone this repo and source profdotd. Some where in your `~/.bashrc`:

```bash
ProfDotD_Priority=(personal devteam)

. ~/profdotd/profdotd
```

## How it works

ProfDotD will create 2 directories by default in your home directory a `~/bin.d` and a `~/.profile.d`. These 2 directories will then contain any number of directories to organize profiles and scripts. This structure is meant to be a single level deep, and any directories nested further than shown below will be ignored.

your setting from `ProfDotD_Priority` determines which files get loaded and which don't. Priority items are considered first in the order specified, then all other items in alphanumeric order. Any filename loaded by an earlier profile will not get loaded in later profiles.

```bash
$ tree -aF bin.d .profile.d
bin.d
├── personal/
│   ├── myscript*
│   └── overridden*
├── devteam/
│   ├── dev*
│   └── overridden* # Not found by command: which overridden
└── test/
    ├── overridden* # Not found by command: which overridden
    └── testscript*
.profile.d
├── personal/
│   ├── personalonly
│   └── shared
├── devteam/
│   ├── devonly
│   └── shared # Does not get run
└── test/
    ├── testonly
    └── shared # Does not get run
```

## Configuration

There are only a couple of configuration items:

* `ProfDotD_Priority=(personal)`
    * This is a bash array containing the priority in which to load profiles
* `ProfDotD_BaseDir="${HOME}"`
    * The base directory that ProfDotD works from, for simplicity this is defaulted to your home
    
## Extra points

Included in this repo is a small sample ansible repository. This repo could be forked and you could immediately have your profile stored in source management with a reliable method for updating entries. To use the ansible repo do the following:

* first install ansible: https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html
    * TL;DR: your package manager should have 'ansible' if not `sudo pip install ansible`


```bash
cd ansible
ansible-playbook profdotd.yml
```

The above makes use of `ProfDotD_BaseDir` to put the files in the right place by default so your terminal should already have ProfDofD sourced

This ansible setup could also be altered and the name of the profile changed from personal to the name of your team which can then be easily shared with every one.

see [ansible.cfg](ansible/ansible.cfg) for the options used

## Testing/Debugging

In the testing folder you will find a super simple layout as would be in your home directory. You can run the [test](test) script to simulate the profile loading. The script will make it so that run will print out debugging messages. It could be helpful to add echo statements if necessary to figure out what might be happening.

The variable for enabling debug is:

```bash
ProfDotD_Debug='true'
```

# License

[License](LICENSE)