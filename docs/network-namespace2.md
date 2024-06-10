# network namespace

## add network namespace

```bash
ip netns add ns1
ip netns add router
ip netns add ns2

ip netns list
```

## add veth

```bash
ip link add ns1-veth0 type veth peer name gw-veth0
ip link add ns2-veth0 type veth peer name gw-veth1
ip link show | grep veth
```

## link set

```bash

```
