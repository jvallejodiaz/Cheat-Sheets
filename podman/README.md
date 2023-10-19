# Podman

## Set max_map_count in VM

```@shell
$ podman machine ssh
$ sudo sysctl -w vm.max_map_count=262144
```
### To do it permanently 

```@shell
cp /etc/sysctl.conf /tmp/
echo "vm.max_map_count=262144" >> /tmp/sysctl.conf
sudo cp /tmp/sysctl.conf /etc/
```
