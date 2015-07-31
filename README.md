# ChefDK_Bootstrap
## Setup your laptop for Chef development in minutes

Run one simple command to easily setup your Windows or Mac machine
for Chef cookbook development in about **20 minutes**.

## Quickstart - Windows

### Prerequisites

* [PowerShell 3.0](https://www.microsoft.com/en-us/download/details.aspx?id=34595)

### If you're behind a proxy...

If you need to go through a proxy server, export these environment variables before you run the commands below.

```PowerShell
# change these values to your proxy address
$env:http_proxy='http://myproxy.example.com:1234'
```
```PowerShell
$env:https_proxy=$env:http_proxy
```
```PowerShell
# don't go through the proxy for these addresses.
$env:no_proxy='127.0.0.1,localhost,example.com'
```

Copy the PowerShell commands below and paste them into a **PowerShell Admin** console. This will execute the [bootstrap](https://raw.githubusercontent.com/Nordstrom/chefdk_bootstrap/master/bootstrap.ps1)
script on your workstation.

```PowerShell
 (Invoke-WebRequest -Uri https://raw.githubusercontent.com/Nordstrom/chefdk_bootstrap/master/bootstrap.ps1 -ProxyUseDefaultCredentials -Proxy $env:https_proxy).Content | Invoke-Expression
```


## Quickstart - Mac

### If you're behind a proxy...
If you need to go through a proxy server, export these environment variables before you run the commands below:

```bash
# change these values to your proxy address
export http_proxy=http://myproxy.example.com:1234
```
```bash
export https_proxy=$http_proxy
```
*To make these changes permanent, export these environment variables from your bash or zsh profile.*

Copy the command below and paste it into a terminal. This will execute the [bootstrap](https://raw.githubusercontent.com/Nordstrom/chefdk_bootstrap/master/bootstrap.sh) script on your workstation.

```bash
curl https://raw.githubusercontent.com/Nordstrom/chefdk_bootstrap/master/bootstrap.sh | bash
```

### ChefDK profile setup
Follow the instructions in the [ChefDK README](https://github.com/chef/chef-dk#using-chefdk-as-your-primary-development-environment) to complete the Chef workstation setup.

## What does it do?
This cookbook installs these tools:

### Editor
[Atom](https://atom.io), a free, general purpose, cross-platform, open source,
text editor. Out of the box, Atom supports all the languages you will need
for Chef development: Ruby, PowerShell, Bash, XML, JSON, etc.

### Source Control
[Git](http://git-scm.com/) - command line git client and tools.


### Local Virtualization
[Virtualbox](https://www.virtualbox.org/) - Oracle's free, open source virtualization tool for local cookbook testing.

[Vagrant](https://www.vagrantup.com/) - ChefDK's included [Test Kitchen]() tool uses Vagrant to spin up local VMs for cookbook testing.

----

## Recipes

### default
* Installs [Chocolatey](https://chocolatey.org/) for a Windows machine and [homebrew](http://brew.sh) for a Mac machine. Both of these are package managers, similar to `apt-get` on Ubuntu. Chocolatey is used to install packages like `posh-git` and `kdiff3`, while homebrew is used to install packages like `iterm2 `.

* Installs all the other tools marked `true` in the
`node['chefdk_bootstrap']['package']` hash.

* On Windows, includes the Powershell profile configuration recipe.

### atom
* Installs the Atom editor

### git
* Installs git.
* On Windows, installs git-credential-winstore, and posh-git.

### gitextensions
* On Windows, installs gitextensions, a GUI git client.

### kdiff3
* On Windows, installs the free, open-source diff/merge tool, kdiff3.

### powershell_profile
* Configures a global PowerShell profile to correct the $env:HOME environment
variable and run `chef shell-init powershell`.

### vagrant
* Installs Vagrant.

### virtualbox
* Installs Virtualbox.

### iterm2
* On Mac, installs iterm2.

## Attributes

The attributes defined by this recipe are organized under the
`node['chefdk_bootstrap']` namespace.

Attribute | Description | Type   | Default
----------|-------------|--------|--------
['atom']['source_url'] | Windows: Atom installer package source URL | URL String | https://atom.io/download/windows
['atom']['source_url'] | Mac: Atom installer package source URL | URL String | https://atom.io/download/mac
['package']['atom'] | Whether to install Atom or not | boolean | true
['package']['kdiff3'] | Whether to install kdiff3 or not | boolean | true
['package']['vagrant'] | Whether to install Vagrant or not | boolean | true
['package']['virtualbox'] | Whether to install Virtualbox or not | boolean | true
['package']['git'] | Whether to install git and related packages or not | boolean | true
['package']['gitextensions'] | Whether to install gitextensions or not | boolean | true
['package']['iterm2'] | Whether to install iterm2 or not | boolean | true

## Author

Nordstrom, Inc.

## License

Copyright 2015 Nordstrom, Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
