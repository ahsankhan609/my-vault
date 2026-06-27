---
title: SSH & remote Access
created: 2026-06-27
YT: https://www.youtube.com/watch?v=7Zt2Mp2IeBI
---
[Stop Memorizing SSH Commands. Use SSH Agent Instead](Linux%20-%20Power%20Shell/Stop%20Memorizing%20SSH%20Commands.%20Use%20SSH%20Agent%20Instead.md)


This ==protocol== is the ==common means== of ==connecting to== and ==interacting with the command line== of a ==remote Linux machine==.

### What is SSH & how Does it Work?

Secure Shell or SSH simply is a protocol between devices in an encrypted form. Using ==cryptography==, any input we send in a human-readable format is encrypted for travelling over a network, where it is then unencrypted once it reaches the remote machine, such as in the diagram below.

![](Attachments/Pasted%20image%2020260627130615.png "ssh-workflow")

### Using SSH to Login to Your Linux Machine

The syntax to use SSH is very simple. We only need to provide two things:

1. The ==IP address== of the ==remote(target) machine==
2. Correct credentials to a valid account to login with on the remote machine

```bash
ssh attacker_username@target_ipaddress
```

