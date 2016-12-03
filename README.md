# ansible-resolv.conf

Usually I have a local nameserver on my virtualization hosts to serve all virtual machines and the host itself with DNS service. I often use it to serve local addresses.

In the process of provisioning of new machines there are situations where the local nameserver is not available yet.

This role checks whether the local nameserver is available before it deploys a new `/etc/resolv.conf` file. So in the beginning all hosts will use the public nameservers but when the local nameserver is configured I apply this role again and everything is forced to use my own nameserver.

The default values are localhost and the OpenDNS servers:

```
local_nameserver: 127.0.0.1

public_nameservers:
  - server: 208.67.220.220
  - server: 208.67.222.222
```

You can overwrite this values with normal Ansible variables.

Note: When the playbook starts it flushes all handlers to make sure that reconfigured nameservers are reloaded.
