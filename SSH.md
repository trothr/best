# SSH - Secure Shell

SSH is "Secure Shell" and is both a protocol and a utility.
As a utility, there are several implementations, both commercial and "free".

SSH protocol uses the same combined symmetric and asymmetric cryptography
as is found in PGP and PKI to establish secure command sessions between
computing systems. Most often, SSH is used for connecting from a laptop
or workstation to a server. It was invented in the mid 1990s as a secure
alternative to the Unix "R commands" for remote access. It also replaces
TELNET so it is well suited to session work.

SSH is the most secure way to connect between systems either for
interactiev access ("shell" access) or to drive specific commands.

## SSH Protocol

As a protocol, SSH uses similar combinations of symmetric and asymmetric
cryptography as found in SSL/TLS (PKI as found in support of HTTPS),
but SSH is a completely different protocol from TLS or SSL.

When connecting with an SSH-enabled tool (e.g., PuTTY or SecureCRT),
be sure you are in fact using SSH protocol and are using version 2
of the protocol. You may be able to sign-on with a password,
but signing-on with a public/private key pair is recommended.
The original SSH1 protocol was replaced by SSH2 several years ago,
but occasionally you will see references to SSH1. Avoid SSH1.
Disable SSH1 if at all possible, on both clients and servers.

## SSH Capabilities

Your SSH client provides secure communication between your laptop
or workstation and servers which speak the SSH protocol. The most
common capability is running a command shell on target systems.
SSH can also forward X11 traffic. It can forward arbitrary TCP ports
either direction. SSH can also safely forward your sign-on credentials.

Specific capabilities can be disabled, either on the server end or on
the client end, with possible loss of productivity. The ability to adjust
these things via configuration demonstrates the power of SSH as secure
utility and protocol.

## SSH Clients

There are many SSH client programs available.
In this document we'll discuss only three: PuTTY, SecureCRT, and OpenSSH.

PuTTY is a multi-protocol client and terminal emulator.
It can connect using wired communication lines (e.g., COM1:),
TELNET protocol, and of course SSH protocol. When using SSH,
if you use SSH keys, PuTTY has its own key management function.
To use an SSH public key from PuTTY with most servers, you'll need to
export it to OpenSSH format. PuTTY only runs on MS Windows.

SecureCRT from VanDyke Software is similar to PuTTY. It supports SSH
and other protocols like TELNET and includes terminal emulation.
It can interface with enterprise single-signon (SSO) solutions.
SecureCRT runs on MS Windows.

OpenSSH, as a package, includes both a client and a server.
It is the most popular SSH client and server for Linux and Unix systems.
Unlike PuTTY, the SSH client in the OpenSSH package does not provide
terminal emulation. It runs within a command shell by way of whatever
terminal emulator you choose. The `ssh` command provides a powerful
means of connecting and also of scripting.

All three of these SSH clients can forward a TCP port from the remote
(server) to the local (client) end, or vice versa. Both can forward
X11 traffic. Both can forward SSH agent service.

Of the three, the OpenSSH client program `ssh` is the most powerful
for automation and scripting. The `ssh` command underpins the `scp`
and `sftp` commands as well as secure mode `rsync` and other tools.

## Athentication and Agents

There are several ways one can authenticate an SSH connection, including

* password, which uses standard system security on the target end
* SSH key, using a public key delivered to target servers manually
* PKI certificate (essentially public key, but different trust model)
* others (including Kerberos-based services)

Authentication via
Traditional password is often needed for first-time connections.

Authentication via
SSH key is the most secure because credentials can be forwarded/proxied
and it offers multi-factor by default.

Other authentication methods may integrate with corporate services
such as single-signon and (like traditional password) are often helpful
for initial connections.

Of these, only the public key methods can be forwarded by an SSH agent.
SSH agent forwarding is both highly practical and highly secure
and offers improved productivity. To use SSH agent credential forwarding,
you will need to launch an SSH agent on your laptop or workstation
and then run SSH clients in a way that they can communicate with it.

This document does not discuss agent forwarding with PKI certificates.

This document does not discuss agent integration with PuTTY or SecureCRT.

With the agent in place, your SSH credentials can be forwarded securely
and automatically to other systems that you might connect to by way of
the first hop. In other words, say you connect to system A using SSH
with the `-A` option and an agent running. From the shell on system A,
you could then connect to system B using the same SSH public key.
System B might not even be reachable from your client.

In absense of agent credential forwarding,
all authentication methods work fine for the first hop.

##

The following sections discuss primarily OpenSSH or similar
command-line SSH client operation.

## Using Key-based Sign-on

When configured to allow it, SSH supports key-based sign-on so that you can
connect without use of a password. Instead of a password, your client-side
private key supplies the credentials to authenticate you. This is considered
by many to be more secure than using passwords of any length or form.
Your client-side private key is protected by a passphrase.

## Client Side: Creating a Key Pair

On systems with OpenSSH (including Unix, Linux, and CYGWIN),
creating an SSH key pair is as easy as ... 

    ssh-keygen -t rsa -b 4096 

This command will prompt you for the name of the files to hold your key pair
(press enter for the default), create your `$HOME/.ssh` directory (if needed),
and prompt you for a passphrase. The passphrase operates like a password
but is entirely local, never gets sent to the server, and is associated
with the private key just created. Protect your private key ($HOME/.ssh/id_rsa),
but distribute the public key widely ($HOME/.ssh/id_rsa.pub).

On servers you wish to connect with securely, append the
public key to the $HOME/.ssh/authorized_keys file. (see below)

SSH steps up the security of interactive command access. An attacker
could not masqueraed as you unless they got #1 access to the client system
(e.g., your PC or workstation), #2 your private key file, and #3 your passphrase. 

## Server Side: `$HOME/.ssh/authorized_keys`

SSH server implementations vary, but our Linux servers run OpenSSH.
For that, you can enable key-based sign-on by simply appending your SSH
public key (from the client side) to your "authorized_keys" file
(on the server side, the target system). Copy your SSH public key to the
remote system where you need to sign-on (e.g. as /tmp/mysshkey.pub),
sign-on to that system (using a password or SSO), and then append your public
key to your `authorized_keys` file with the commands ...

    mkdir -m 700 -p $HOME/.ssh
    cat /tmp/mysshkey.pub >> $HOME/.ssh/authorized_keys

(Run the above sequence on *server* systems, not on the client.)

The first command will create your `.ssh` sub-directory if it is not
already there, but will harmlessly do nothing if it already exists.
Remember to clean-up after yourself and remove your /tmp/mysshkey.pub file.

On some systems, there is an `ssh-copy-id` command (see next)
to perform the above concatenation in a single fell swoop.

## `ssh-copy-id`

You can often
use the `ssh-copy-id` command to copy public SSH keys to selected
remote machines (servers).

`ssh-copy-id` is a script that uses `ssh` to log into a remote machine
(presumably using a login password) and then add public keys
by appending them to the remote user's `~/.ssh/authorized_keys` file.
The file and directory are created if necessary.

`ssh-copy-id` is convenient, but not strictly needed.
You can manually concatenate keys to `~.ssh/authorized_keys` (see above).

### `ssh-agent`

You can launch an SSH agent manually,
but most Linux and Mac systems do so automatically when you sign-on.

The SSH agent will securely hold you passphrase and act on your behalf
facilitating automation and repetition and boosting productivity.
Agent service can be proxied, which does more than simply avoiding
passphrase re-entry. By way of agent proxy, you can access remote
systems by way of intermediate systems without needing additional
SSH private keys. In other words, you can keep your private keys
on the client end, dramatically reducing risk.

Commands run under the SSH agent inherit the settings,
the environment variables, of the agent. Any `ssh` command
invoked by these "child" processes also inherits the agent info.
An `ssh` command with that information can securely connect
to the agent and does not require manual intervention.

To launch your SSH agent as a parental umbrella process ...

    ssh-agent $SHELL

All commands run from that shell benefit from inheritance.

### `ssh-add`

Use `ssh-add` to add selected SSH keys to the set of keys handled by
your SSH agent. By default, `ssh-add` adds all standard identities
that it finds to its virtual keyring.

    ssh-add

On Linux systems, this is not normally needed.

On Mac systems, this should be run once per sign-on session
(at the laptop or desktop).

On Windows systems, you'll need to bring up a POSIX shell environment,
using CYGWIN or MINGW or "Git Bash" or similar, or use WSL1 or WSL2.

## Server Key Alerts

SSH not only authenticates you to the target server. It also authenticates
the target server to you. This is important because it minimizes the risk
that someone will trick you into signing-on to a different system
than you believe you're connecting to. 

Without other pre-configuration, when first connecting to an SSH server,
your client will present that server's key fingerprint and ask for you
to confirm that you truly want to connect. Most often, at that point,
one trusts that the connection is legitimate. (The window of opportunity
for an attacker is very small in the case of a new server, e.g., a
freshly installed SecureData appliance.) Your action of accepting the
server's key in this case is called "manual assertion" and is essentially
the same as when accepting a self-signed web server certificate,
telling your browser that site is okay. 

An example first-time connection using the OpenSSH client might show something like ... 

    The authenticity of host '172.16.11.212 (172.16.11.212)' can't be established.
    ECDSA key fingerprint is SHA256:pl+MABw5nu8ly/sd8E7Tw7RW8q311eJDjoI5QV7+N1Q.
    Are you sure you want to continue connecting (yes/no)? 

Once that server's key is trusted, your SSH stores the public key
and uses it every time you reconnect. If at any time the server's key
does not match, you will get an error. Your SSH client (whether PuTTY
or command-line 'ssh') will warn you loudly that the key does not match.
Someone wishing to introduce a masquerading false server would need the
SSH server key of the true target server, very difficult for the attacker to obtain. 

An example of connecting to a server with a new host key using OpenSSH similar to ... 

    @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    @    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
    @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
    Someone could be eavesdropping on you right now (man-in-the-middle attack)!
    It is also possible that a host key has just been changed.
     ...
    Add correct host key in /home/myid/.ssh/known_hosts to get rid of this message.
    Offending ECDSA key in /home/myid/.ssh/known_hosts:28


