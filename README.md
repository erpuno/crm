CRM: Ukrainian Govermental Document Management
==============================================

* Prerequisites
* Build
* Deploy
* Operate

The МІА:Документообіг [CRM.ERP.UNO] in essense is
the system for managing documents and activities its implies.

APT Prerequisites
-----------------

The application supports development on Windows, WSL, Linux or Mac.

* Erlang 22.0
* Elixir 1.9
* CMake 3.15
* libcsv 3.0
* .NET Core 3.1

Erlang, Elixir and developer libraries for building from sources:

```sh
$ sudo apt install erlang elixir build-essential libcsv3 libcsv-dev cmake
```

As Word/Excel JavaScript control CRM uses OnlyOffice
which can be installed on Ubuntu as [snap](https://github.com/ONLYOFFICE/snap-documentserver):

```sh
$ sudo snap install onlyoffice-ds
```

CRM also is in need of DOCX to PDF converter and PNG
manipulation console program at the server side:

```sh
$ sudo apt install unoconv pdftk img2pdf poppler-utils
$ sudo apt-get --reinstall install ttf-mscorefonts-installer
```

Python3 and Node.js:

```sh
$ sudo apt install python3 python3-pip npm nodejs
```

In case of troubles with ITT Sign Agent (Linux client) perform these installments:

```sh
$ sudo apt install libusb libccid pcscd libpcsclite1 pcscd pcsc-tools
```

.NET Prerequisites
------------------

```sh
$ wget https://dot.net/v1/dotnet-install.sh
$ chmod +x dotnet-install.sh
$ ./dotnet-install.sh -c 3.1
```

Then put into your `~/.profile` the following

```
export DOTNET_ROOT=$HOME/.dotnet
export PATH=$PATH:$HOME/.dotnet
```

PIP3 Prerequisites
------------------

```sh
$ python3 -m pip install --upgrade pip
$ python3 -m pip install --upgrade pymupdf
```

Then put into your `~/.profile` the following

```
export PATH=$PATH:/home/azureuser/.local/bin
```

Then install and run `unoserver` in case `production_convert` is true:

```sh
$ sudo pip3 install unoserver
$ unoserver --interface $IP_ADDR --port $PORT --daemon
```

Node.js Prerequisites
---------------------

The minimal `node` should be 12.13.0.
If you have Ubuntu 20.04 you should install it through `nvm`:

```sh
$ curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash
$ source ~/.profile
$ nvm install node
```

Then install `sharp` converter:

```sh
$ cd sharp
$ npm install
$ npm install -g pkg
$ pkg ./
```

Build with proper database backup
---------------------------------

Restore from backup `Mnesia.demo@edoc` and `rocksdb` folders (file copy backup/restore):

```sh
$ ls -1 -S
/Mnesia.demo@edoc
/c_src
/config
/deps
/documents
/include
/lib
/priv
/rel
/rocksdb
/src
/test
CHANGELOG
mix.exs
README.md
```

Ensure you have the same `hostname` as in mnesia databse folder:

```
$ sudo hostname edoc
```

Retrieve external dependencies, compile and run locally with provided `Mnesia` database:

```sh
$ mix deps.get
$ mix compile
$ iex --name demo@edoc -S mix
```

Deploy
------

Deploy MIX release as UNIX background application:

```sh
$ mix release
$ _build/dev/rel/crm/bin/demo daemon
```

Then open <a href="http://localhost:50111/app/ldap.htm">http://localhost:50111/app/ldap.htm</a>.

Operate
-------

Attach to running instance of the deployed MIX release and perform migration procedure:

```sh
$ _build/dev/rel/crm/bin/demo remote
```

Commiters
---------

* Maksym Sokhatskyi
* Andrii Zadorozhnii
* Ivan Kulyk
* Denys Shkurko
* Andriy Tsehmeistruk
* Victoria Kosholap
* Bohdan Kotenko
* Artem Sitalo
* Borys Trokhymchuk
* Iryna Kostyuk
* Ruslan Moroz
* Oleksandr Naumov
* Anton Nesterenko
* Valery Kalenyk
* Vladyslav Kaltymenko
* Igor Gorodetsky
