## network namespace

```bash
ip netns add ns1
ip netns add ns2

ip netns exec ns1 ip address show
ip netns exec ns1 ip route show
```

### veth

virtual ethernet device

```bash
ip link add ns1-veth0 type veth peer name ns2-veth0
ip link show | grep veth
```

link set

```bash
ip link set ns1-veth0 netns ns1
ip link set ns2-veth0 netns ns2
ip netns exec ns1 ip link show | grep veth
```

add ip address

```bash
ip netns exec ns1 ip address add 192.0.2.1/24 dev ns1-veth0
ip netns exec ns2 ip address add 192.0.2.2/24 dev ns2-veth0
ip netns exec ns1 ip route show
```

status up

```bash
ip netns exec ns1 ip link show ns1-veth0 | grep state
ip netns exec ns1 ip link set ns1-veth0 up
ip netns exec ns2 ip link set ns2-veth0 up
ip netns exec ns1 ip link show ns1-veth0 | grep state
```

ping

```bash
# ns1 -> ns2
ip netns exec ns1 ping -c 3 192.0.2.2
```
