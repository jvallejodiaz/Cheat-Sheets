# Podman

## Set max_map_count in VM

```@shell
$ podman machine ssh
$ sudo sysctl -w vm.max_map_count=262144
```
