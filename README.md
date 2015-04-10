A lightweight VM with SQL Server 2014 Express

# Prerequisites

- [Vagrant][]
- [VirtualBox][]

# Install and start up

The first time that you do this it will download a large Vagrant box
file (about 2.7 GB) from the Internet, so you may want to wait until you
have a good connection.

```bash
vagrant up
```

To verify that the VM started, you can use the `tsql` utility bundled
with FreeTDS. E.g.:

```
$ tsql -H localhost -p 1433 -U vagrant -P vagrant
locale is "en_US.UTF-8"
locale charset is "UTF-8"
using default charset "UTF-8"
1> SELECT @@VERSION
2> GO

Microsoft SQL Server 2014 - 12.0.2000.8 (X64)
Feb 20 2014 20:04:26
Copyright (c) Microsoft Corporation
Express Edition (64-bit) on Windows NT 6.3 <X64> (Build 9600: )

(1 row affected)
```

# Details

You now have a VirtualBox VM with:

- [Microsoft Hyper-V Server 2012 R2][Hyper-V Server] – free, stripped-down
  version of Windows; has very little GUI or admin/desktop tools, but it's good
  enough to run SQL Server Express and it can be managed remotely via PowerShell.
- [Chocolatey][] (a package manager for easily installing software in Windows)
- [PuTTY][] (client for ssh/telnet/etc.)
- git (version 1.9.5.msysgit.1) - installed via [Chocolatey][]. This
  comes with a bunch of other UNIX utilities like: awk, bash, bzip,
  diff, du, find, gpg, grep, less, openssl, scp, ssh, tar, etc.
- [SQL Server Express][] 2014 (free version of SQL Server) - installed
  via a [Chocolatey][] package called [MsSqlServer2014Express][]. I've
  configured it as follows:

  - Listens on TCP port 1433
  - Uses mixed mode authentication; so it allows SQL Server Authentication; not just Windows Authentication
  - Has a login called `vagrant` with password `vagrant`
  - Management tools (e.g.: SSMS) are **not** included, as these are not
    supported on the free Hyper-V Server product. However, [SQLCMD][] is available.

# Screenshot

![Screenshot](screenshot.png)

# Tips

- You can get a bash shell by executing `"git bash"` (with quotes) at
  the command prompt. From this shell, you can access a bunch of UNIX
  utilities, including some that you can't use from the Windows command
  prompt like vim and gitk. You can see all of the available stuff in
  `/usr/bin`.
- perl (v5.8.8) is available, if that's the way you roll.
- If you want more UNIX goodies, you can install [Cygwin][] with `choco
  install -y cyg-get` in a command prompt or PowerShell. This will
  create a basic Cygwin install in `C:\tools\cygwin`.
- If you accidentally close the command prompt window and need to open
  another, press Ctrl + Alt + Del and pick "Task Manager". Then in the
  `File` menu, choose "Run new task" and type `cmd` and hit Enter.
- Port 1433 on the host is forwarded to port 1433 on the guest, so from
  the host, you can connect to SQL Server Express by connecting to
  `localhost:1433`.
- You can RDP to the host by doing `vagrant rdp`.

[Vagrant]: https://www.vagrantup.com/
[VirtualBox]: https://www.virtualbox.org/
[Hyper-V Server]: https://technet.microsoft.com/en-us/library/hh833684.aspx
[SQL Server Express]: http://www.microsoft.com/en-us/server-cloud/products/sql-server-editions/sql-server-express.aspx
[Chocolatey]: https://chocolatey.org/
[PuTTY]: http://www.chiark.greenend.org.uk/~sgtatham/putty/
[MsSqlServer2014Express]: https://chocolatey.org/packages/MsSqlServer2014Express
[devmonkeys/database]: http://code.corp.surveymonkey.com/devmonkeys/database
[SQLCMD]: https://msdn.microsoft.com/en-us/library/ms162773.aspx
[Cygwin]: https://www.cygwin.com/
