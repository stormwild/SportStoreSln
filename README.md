# Angular .NET Core MVC

## Pre-requisites

- Git
- .NET 5 - latest version of .NET Core
- Docker
- Nodejs using NVM for Windows
- Visual Studio Code and/or Visual Studio 

### Git

[Git](https://git-scm.com/)

Using git bash, check for `.bash_profile` at the root of your user directory

```sh
$ ls -al ~ | grep .bash
-rw-r--r-- 1 User 197121     9112 Jan  4 02:28 .bash_history
-rw-r--r-- 1 User 197121      116 Aug 27 16:40 .bash_profile
```

Set the git settings to show git states in your git bash prompt:

```sh
$ cat ~/.bash_profile
GIT_PS1_SHOWDIRTYSTATE=1
GIT_PS1_SHOWUNTRACKEDFILES=1
GIT_PS1_SHOWSTASHSTATE=1
GIT_PS1_SHOWUPSTREAM="auto verbose"
```

In git bash, set some short cut alias:

```sh
git config alias.co checkout && \
git config alias.br branch  && \
git config alias.ci commit  && \
git config alias.st status  
```

Sample output using `git status`

```sh
User@DESKTOP MINGW64 /d/Source/Repos/gists/angular-dotnet-core (master * u=)
$ git st
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   angular-dotnet-core.md

no changes added to commit (use "git add" and/or "git commit -a")

User@DESKTOP MINGW64 /d/Source/Repos/gists/angular-dotnet-core (master * u=)
$
```

See [Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) for more info.

Load ssh key

```sh
$ eval $(ssh-agent -s)
Agent pid 2198
```

Add key to agent

```sh
$ ssh-add ~/.ssh/id_rsa
Enter passphrase for /c/Users/User/.ssh/id_rsa:
Identity added: /c/Users/User/.ssh/id_rsa (user@gmail.com)
```

Useful git commands

```sh
$ git help
usage: git [--version] [--help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]

These are common Git commands used in various situations:

start a working area (see also: git help tutorial)
   clone             Clone a repository into a new directory
   init              Create an empty Git repository or reinitialize an existing one

work on the current change (see also: git help everyday)
   add               Add file contents to the index
   mv                Move or rename a file, a directory, or a symlink
   restore           Restore working tree files
   rm                Remove files from the working tree and from the index
   sparse-checkout   Initialize and modify the sparse-checkout

examine the history and state (see also: git help revisions)
   bisect            Use binary search to find the commit that introduced a bug
   diff              Show changes between commits, commit and working tree, etc
   grep              Print lines matching a pattern
   log               Show commit logs
   show              Show various types of objects
   status            Show the working tree status

grow, mark and tweak your common history
   branch            List, create, or delete branches
   commit            Record changes to the repository
   merge             Join two or more development histories together
   rebase            Reapply commits on top of another base tip
   reset             Reset current HEAD to the specified state
   switch            Switch branches
   tag               Create, list, delete or verify a tag object signed with GPG

collaborate (see also: git help workflows)
   fetch             Download objects and refs from another repository
   pull              Fetch from and integrate with another repository or a local branch
   push              Update remote refs along with associated objects

'git help -a' and 'git help -g' list available subcommands and some
concept guides. See 'git help <command>' or 'git help <concept>'
to read about a specific subcommand or concept.
See 'git help git' for an overview of the system.
```

Other useful commands

```sh
$ git branch -av
* master                fe7d222
  remotes/origin/HEAD   -> origin/master
  remotes/origin/master fe7d222

$ git remote -v
origin  git@gist.github.com:85dc12af6f0e28af0e4d5ba05ea255f4.git (fetch)
origin  git@gist.github.com:85dc12af6f0e28af0e4d5ba05ea255f4.git (push)


$ git log --oneline -10
fe7d222 (HEAD -> master, origin/master, origin/HEAD)

```

### .NET 5 (latest .NET Core)

[Download .NET](https://dotnet.microsoft.com/download)

```sh
 dotnet --info
.NET SDK (reflecting any global.json):
 Version:   5.0.101
 Commit:    d05174dc5a

Runtime Environment:
 OS Name:     Windows
 OS Version:  10.0.18363
 OS Platform: Windows
 RID:         win10-x64
 Base Path:   C:\Program Files\dotnet\sdk\5.0.101\

Host (useful for support):
  Version: 5.0.1
  Commit:  b02e13abab

.NET SDKs installed:
  2.2.207 [C:\Program Files\dotnet\sdk]
  5.0.101 [C:\Program Files\dotnet\sdk]

.NET runtimes installed:
  Microsoft.AspNetCore.All 2.1.23 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.All]
  Microsoft.AspNetCore.All 2.2.8 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.All]
  Microsoft.AspNetCore.App 2.1.23 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
  Microsoft.AspNetCore.App 2.2.8 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
  Microsoft.AspNetCore.App 3.1.7 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
  Microsoft.AspNetCore.App 3.1.10 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
  Microsoft.AspNetCore.App 5.0.1 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
  Microsoft.NETCore.App 2.1.23 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
  Microsoft.NETCore.App 2.2.8 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
  Microsoft.NETCore.App 3.1.7 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
  Microsoft.NETCore.App 3.1.10 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
  Microsoft.NETCore.App 5.0.1 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
  Microsoft.WindowsDesktop.App 3.1.7 [C:\Program Files\dotnet\shared\Microsoft.WindowsDesktop.App]
  Microsoft.WindowsDesktop.App 3.1.10 [C:\Program Files\dotnet\shared\Microsoft.WindowsDesktop.App]
  Microsoft.WindowsDesktop.App 5.0.1 [C:\Program Files\dotnet\shared\Microsoft.WindowsDesktop.App]

To install additional .NET runtimes or SDKs:
  https://aka.ms/dotnet-download
```

List dotnet templates, see [dotnet new](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-new)

```sh
$ dotnet new -l
Templates                                         Short Name               Language          Tags
--------------------------------------------      -------------------      ------------      ----------------------
Console Application                               console                  [C#], F#, VB      Common/Console
Class library                                     classlib                 [C#], F#, VB      Common/Library
WPF Application                                   wpf                      [C#], VB          Common/WPF
WPF Class library                                 wpflib                   [C#], VB          Common/WPF
WPF Custom Control Library                        wpfcustomcontrollib      [C#], VB          Common/WPF
WPF User Control Library                          wpfusercontrollib        [C#], VB          Common/WPF
Windows Forms App                                 winforms                 [C#], VB          Common/WinForms
Windows Forms Control Library                     winformscontrollib       [C#], VB          Common/WinForms
Windows Forms Class Library                       winformslib              [C#], VB          Common/WinForms
Worker Service                                    worker                   [C#], F#          Common/Worker/Web
Unit Test Project                                 mstest                   [C#], F#, VB      Test/MSTest
NUnit 3 Test Project                              nunit                    [C#], F#, VB      Test/NUnit
NUnit 3 Test Item                                 nunit-test               [C#], F#, VB      Test/NUnit
xUnit Test Project                                xunit                    [C#], F#, VB      Test/xUnit
Razor Component                                   razorcomponent           [C#]              Web/ASP.NET
Razor Page                                        page                     [C#]              Web/ASP.NET
MVC ViewImports                                   viewimports              [C#]              Web/ASP.NET
MVC ViewStart                                     viewstart                [C#]              Web/ASP.NET
Blazor Server App                                 blazorserver             [C#]              Web/Blazor
Blazor WebAssembly App                            blazorwasm               [C#]              Web/Blazor/WebAssembly
ASP.NET Core Empty                                web                      [C#], F#          Web/Empty
ASP.NET Core Web App (Model-View-Controller)      mvc                      [C#], F#          Web/MVC
ASP.NET Core Web App                              webapp                   [C#]              Web/MVC/Razor Pages
ASP.NET Core with Angular                         angular                  [C#]              Web/MVC/SPA
ASP.NET Core with React.js                        react                    [C#]              Web/MVC/SPA
ASP.NET Core with React.js and Redux              reactredux               [C#]              Web/MVC/SPA
Razor Class Library                               razorclasslib            [C#]              Web/Razor/Library
ASP.NET Core Web API                              webapi                   [C#], F#          Web/WebAPI
ASP.NET Core gRPC Service                         grpc                     [C#]              Web/gRPC
dotnet gitignore file                             gitignore                                  Config
global.json file                                  globaljson                                 Config
NuGet Config                                      nugetconfig                                Config
Dotnet local tool manifest file                   tool-manifest                              Config
Web Config                                        webconfig                                  Config
Solution File                                     sln                                        Solution
Protocol Buffer File                              proto                                      Web/gRPC
```

To create a dotnet angular spa project with individual authentication using localdb

```sh
$ dotnet new angular -n SportStore -au Individual -uld -f net5.0 -o SportStore
The template "ASP.NET Core with Angular" was created successfully.

Processing post-creation actions...
Running 'dotnet restore' on SportStore\SportStore.csproj...
  Determining projects to restore...
  Restored D:\Source\Repos\DotNet\SportStore\SportStore.csproj (in 37.75 sec).
Restore succeeded.

```

The `-uld` indicates usage of localdb. The database files will be created at `C:\Users\"username"\`. See [Part 5, work with a database in an ASP.NET Core MVC app](https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/working-with-sql?view=aspnetcore-5.0&tabs=visual-studio).

```sh
aspnet-SportStore-53bc9b9d-9d6a-45d4-8429-2a2761773502.mdf
aspnet-SportStore-53bc9b9d-9d6a-45d4-8429-2a2761773502_log.ldf
```

### Docker

[Docker Desktop](https://www.docker.com/products/docker-desktop)

Some docker commands

```
$ docker image list
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE

$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

```

Check docker is working

```sh
$ docker run --rm hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
21be49aa856f: Pulling fs layer
8d3bdee7e2fc: Pulling fs layer
0a3419bde20a: Pulling fs layer
0a3419bde20a: Verifying Checksum
0a3419bde20a: Download complete
8d3bdee7e2fc: Download complete
21be49aa856f: Download complete
21be49aa856f: Pull complete
8d3bdee7e2fc: Pull complete
0a3419bde20a: Pull complete
Digest: sha256:1a523af650137b8accdaed439c17d684df61ee4d74feac151b5b337bd29e7eec
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (windows-amd64, nanoserver-1809)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run a Windows Server container with:
 PS C:\> docker run -it mcr.microsoft.com/windows/servercore powershell

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

```

A new image has been added

```sh
$ docker image list
REPOSITORY    TAG       IMAGE ID       CREATED       SIZE
hello-world   latest    85b72bead12e   4 weeks ago   252MB

```

If we ran `docker run hello-world`, without the `--rm` flag we would see the recently run container:

```sh
$ docker ps -a
CONTAINER ID   IMAGE         COMMAND                   CREATED          STATUS                      PORTS     NAMES
aab90196dd14   hello-world   "cmd /C 'type C:\\helÔÇª"   24 seconds ago   Exited (0) 22 seconds ago             optimistic_hopper

```

### NVM

[Set up your Node.js development environment directly on Windows](https://docs.microsoft.com/en-us/windows/nodejs/setup-on-windows)

```
$ nvm help

Running version 1.1.7.

Usage:

  nvm arch                     : Show if node is running in 32 or 64 bit mode.
  nvm install <version> [arch] : The version can be a node.js version or "latest" for the latest stable version.
                                 Optionally specify whether to install the 32 or 64 bit version (defaults to system arch).
                                 Set [arch] to "all" to install 32 AND 64 bit versions.
                                 Add --insecure to the end of this command to bypass SSL validation of the remote download server.
  nvm list [available]         : List the node.js installations. Type "available" at the end to see what can be installed. Aliased as ls.
  nvm on                       : Enable node.js version management.
  nvm off                      : Disable node.js version management.
  nvm proxy [url]              : Set a proxy to use for downloads. Leave [url] blank to see the current proxy.
                                 Set [url] to "none" to remove the proxy.
  nvm node_mirror [url]        : Set the node mirror. Defaults to https://nodejs.org/dist/. Leave [url] blank to use default url.
  nvm npm_mirror [url]         : Set the npm mirror. Defaults to https://github.com/npm/cli/archive/. Leave [url] blank to default url.
  nvm uninstall <version>      : The version must be a specific version.
  nvm use [version] [arch]     : Switch to use the specified version. Optionally specify 32/64bit architecture.
                                 nvm use <arch> will continue using the selected version, but switch to 32/64 bit mode.
  nvm root [path]              : Set the directory where nvm should store different versions of node.js.
                                 If <path> is not set, the current root will be displayed.
  nvm version                  : Displays the current running version of nvm for Windows. Aliased as v.

```

```sh
$ nvm list available

|   CURRENT    |     LTS      |  OLD STABLE  | OLD UNSTABLE |
|--------------|--------------|--------------|--------------|
|    15.5.1    |   14.15.4    |   0.12.18    |   0.11.16    |
|    15.5.0    |   14.15.3    |   0.12.17    |   0.11.15    |
|    15.4.0    |   14.15.2    |   0.12.16    |   0.11.14    |
|    15.3.0    |   14.15.1    |   0.12.15    |   0.11.13    |
|    15.2.1    |   14.15.0    |   0.12.14    |   0.11.12    |
|    15.2.0    |   12.20.1    |   0.12.13    |   0.11.11    |
|    15.1.0    |   12.20.0    |   0.12.12    |   0.11.10    |
|    15.0.1    |   12.19.1    |   0.12.11    |    0.11.9    |
|    15.0.0    |   12.19.0    |   0.12.10    |    0.11.8    |
|   14.14.0    |   12.18.4    |    0.12.9    |    0.11.7    |
|   14.13.1    |   12.18.3    |    0.12.8    |    0.11.6    |
|   14.13.0    |   12.18.2    |    0.12.7    |    0.11.5    |
|   14.12.0    |   12.18.1    |    0.12.6    |    0.11.4    |
|   14.11.0    |   12.18.0    |    0.12.5    |    0.11.3    |
|   14.10.1    |   12.17.0    |    0.12.4    |    0.11.2    |
|   14.10.0    |   12.16.3    |    0.12.3    |    0.11.1    |
|    14.9.0    |   12.16.2    |    0.12.2    |    0.11.0    |
|    14.8.0    |   12.16.1    |    0.12.1    |    0.9.12    |
|    14.7.0    |   12.16.0    |    0.12.0    |    0.9.11    |
|    14.6.0    |   12.15.0    |   0.10.48    |    0.9.10    |

This is a partial list. For a complete list, visit https://nodejs.org/download/release
```

```sh
$ nvm install 15.5.1
Downloading node.js version 15.5.1 (64-bit)...
Complete
Creating D:\nvm\temp

Downloading npm version 7.3.0... Complete
Installing npm v7.3.0...

Installation complete. If you want to use this version, type

nvm use 15.5.1
```

```
$ nvm list

    15.5.1
  * 14.13.0 (Currently using 64-bit executable)
    13.8.0
```

```
$ node -v
v14.13.0
```

Change the current node version to use the newly installed version 15.5.1

```sh
$ nvm use 15.5.1
Now using node v15.5.1 (64-bit)
```

Check node version

```sh
$ node -v
v15.5.1
```

## Install Angular Globally

```
$ npm i -g @angular/cli
npm WARN deprecated har-validator@5.1.5: this library is no longer supported
npm WARN deprecated debug@4.2.0: Debug versions >=3.2.0 <3.2.7 || >=4 <4.3.1 have a low-severity ReDos regression when used in a Node.js environment. It is recommended you upgrade to 3.2.7 or 4.3.1. (https://github.com/visionmedia/debug/issues/797)
npm WARN deprecated request@2.88.2: request has been deprecated, see https://github.com/request/request/issues/3142

added 253 packages, and audited 254 packages in 22s

16 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities

```

Check angular is installed

```
$ ng --version

     _                      _                 ____ _     ___
    / \   _ __   __ _ _   _| | __ _ _ __     / ___| |   |_ _|
   / Ôû│ \ | '_ \ / _` | | | | |/ _` | '__|   | |   | |    | |
  / ___ \| | | | (_| | |_| | | (_| | |      | |___| |___ | |
 /_/   \_\_| |_|\__, |\__,_|_|\__,_|_|       \____|_____|___|
                |___/


Angular CLI: 11.0.6
Node: 15.5.1
OS: win32 x64

Angular:
...
Ivy Workspace:

Package                      Version
------------------------------------------------------
@angular-devkit/architect    0.1100.6 (cli-only)
@angular-devkit/core         11.0.6 (cli-only)
@angular-devkit/schematics   11.0.6 (cli-only)
@schematics/angular          11.0.6 (cli-only)
@schematics/update           0.1100.6 (cli-only)


```

Syncing TypeScript with C#

[6+ ways to marry C# with TypeScript](https://alex-klaus.com/marry-csharp-typescript/)

- [NSwag](http://nswag.org/)



