Join the club discord:
[urlsl.me/ClubDiscord](https://urlsl.me/ClubDiscord)
## What is SSH?
Secure SHell, because many protocols at the time of inception were unsecure. Nowadays, the most popular SSH implementation by far is OpenSSH. Basically, its main function is to provide secure, remote terminal access.
## [SSH Uses](https://phoenixnap.com/kb/what-is-ssh)
> These scenarios include:
> - Connecting to a [remote host](https://phoenixnap.com/blog/secure-remote-access-best-practices).
> - Backing up, copying, and mirroring files using SFTP.
> - [Mapping a client's port to the server's port](https://phoenixnap.com/kb/ssh-port-forwarding) to secure TCP/IP and other network protocols.
> - Forwarding X Window System from the server to clients.
> - Tunneling sensitive data through a secure channel.
> - Using a Virtual Private Network.

We will focus on remote shell, tunneling and file transfer.
## OpenSSH News
[OpenSSH 9 released last week.](https://www.linuxadictos.com/en/openssh-9-0-arrives-with-sftp-instead-of-scp-improvements-and-more.html)
The scp utility now uses sftp instead of the less secure scp/rcp protocol.
Forward-thinking authentication and encryption methods enable "quantum-resistant" protections.
## Remote shell
### The Server
The config is typically in `/etc/ssh/sshd_config`. Edit with superuser.
Look up "SSH hardening". This should give you some good ideas for what to manipulate here. [Here's](https://node-security.com/posts/ssh-server-hardening/) a decent page about it. 
[This](https://www.ssh.com/academy/ssh/sshd_config) webpage has a nearly exhaustive list of options
### The Client
Here's a basic ssh connection command:
`ssh student@ssh.csclub.xyz`
It will ask you for a password and you can then login.
But there are better authentication methods!

#### ssh-keygen
There is this concept of using cryptographic keys for authentication instead of passwords. There are many benefits to this some of which are discussed [here](https://security.stackexchange.com/questions/69407/why-is-using-an-ssh-key-more-secure-than-using-passwords). I will put in my 2 cents and say that they also enable strict permissions and managing multiple authorized users via the `authorized_keys` file.

An example is if a sysadmin leaves an organization, and all the other sysadmins were using the same user on every machine for simplicity. Then you only have to remove the key instead of worrying about resetting passwords everywhere.
Another example is ssh tunnels, where you can specify a connection is not allowed shell access and only allowed certain ports.

To generate keys use the `ssh-keygen` command. It has many options, but for most uses the defaults and onscreen prompts are fine.
Then, copy your new key with the `ssh-copy-id` command (and disable password authentication server side). You can instead copy over your key (`keyname.pub`) on a newline manually into `~/.ssh/authorized_keys` if you know what you're doing.

There are many types of keys including some cool ones like those appended with `-sk` (for "Security Key") and some OpenPGP-based options.

#### Config
Client config is typically in `~/.ssh/config`. This makes it easier to connect with a shorthand instead of remembering all your options:
```
Host csclub
        HostName ssh.csclub.xyz
        User student
        Port 22
        IdentityFile ~/.ssh/id_rsa
```
Now you can use `ssh csclub`.

## File copy
Connect with sftp:
`sftp user@host`
The basic commands in sftp are:
- *lcd* change local directory
- *cd* change remote directory
- *get* download remote file
- *put* upload remote file
You can find more commands with `help`.
The best way to transfer entire directories is just to tar and zip, then grab that file instead of messing with directory structures and such.
## SSH tunneling
I didn't have time to prepare this so [here's a webpage](https://www.ssh.com/academy/ssh/tunneling). I'll demonstrate it at the meeting.