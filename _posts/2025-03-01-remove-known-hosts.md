# How to Remove Known Hosts Entry on Windows and Linux

## Introduction

When working with SSH (Secure Shell), the `known_hosts` file is a key component that stores the SSH fingerprints of servers you've previously connected to. This file ensures that you're connecting to the same server you connected to earlier, and helps protect against man-in-the-middle attacks. However, as servers change configurations or if their keys are updated, you may encounter the error:

**"WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!"**

This error can happen when the server's fingerprint changes, potentially signaling a security risk or simply a legitimate configuration change. Regardless of the cause, the outdated entries in the `known_hosts` file need to be removed for SSH to work correctly again.

In this post, we will guide you through how to safely remove outdated `known_hosts` entries on both **Windows** and **Linux** to restore your ability to connect without issues.

---

## Why Is This a Problem?

The `known_hosts` file is used by SSH to verify that the server you're connecting to matches the previously recorded server fingerprint. If the server's fingerprint changes or if there's an accidental connection to a different server, SSH will flag it as a potential security risk.

Some common reasons for needing to remove an entry from the `known_hosts` file include:

1. **Server IP or Hostname Changed**: Reinstalling or migrating the server may change its public key.
2. **Host Key Update**: The server administrator may have updated the server's SSH key for security reasons.
3. **Infrastructure Changes**: Cloud servers or virtual machines may undergo frequent IP and key changes.
4. **Wrong Server Connection**: Sometimes you may accidentally connect to the wrong server, adding an incorrect entry in your `known_hosts` file.

Once an outdated or incorrect entry is detected, SSH will block the connection and prompt a security warning, like the one shown above. To resolve this issue, you need to remove the invalid entry from the `known_hosts` file.

---

## Solution: Removing Known Hosts Entry

Let’s go over how to safely remove the outdated known host entries on both **Windows** and **Linux** systems.

You can remove specific entries using the ssh-keygen command:

```
ssh-keygen -R [hostname_or_ip]
```
For example:
```
ssh-keygen -R 123.456.123.456
```
This command will automatically remove the corresponding entry from the known_hosts file.

**Example**:
If you're working with a server at IP address `123.456.123.456` and you encounter a warning that the host's fingerprint has changed, you would run the following command:
```
ssh-keygen -R 123.456.123.456
```
This would result in output like this:
```
# Host 123.456.123.456 found: line 4
~/.ssh/known_hosts updated.
Original contents retained as ~/.ssh/known_hosts.old
```
Now, you can attempt to reconnect, and SSH will ask you to verify the new fingerprint for that server.

---

## Conclusion
Outdated or incorrect entries in the known_hosts file can prevent successful SSH connections, often leading to the "REMOTE HOST IDENTIFICATION HAS CHANGED" warning. Removing these entries is straightforward, but it's important to ensure that any changes to the server's fingerprint are legitimate.
