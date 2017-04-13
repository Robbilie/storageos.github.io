# StorageOS Volume Plugin

The StorageOS volume plugin turns your Docker node into a hyper-converged storage platform. Each node that runs the StorageOS plugin can contribute available local or attached storage into a distributed pool, which is then available to all cluster members via a global namespace.

Volumes are available across the cluster so if a container gets moved to another node it still has access to its data. Data can be protected with synchronous replication. Compression, caching, and QoS are enabled by default, and all volumes are thin-provisioned.

No other hardware or software is required, except an optional KV store.

For Docker 1.10 - 1.12, an application container is available (storageos-node).

During beta, StorageOS is freely available for testing and experimentation. _DO NOT USE FOR PRODUCTION DATA_. A Developer edition will be free forever.

Full documentation is available at <https://docs.storageos.com>.

## Installation

_Optional:_ Enabling NBD prior to installation is recommended as it will increase performance for some workloads. To enable the module and increase the number of allowable devices run:

```bash
$ sudo modprobe nbd nbds_max=1024
```

Install StorageOS:

```bash
$ docker plugin install --alias storageos store/storageos/plugin
```

This requires you to have Consul installed and available on the Docker host. For single-node installs, you may use `KV_BACKEND=boltdb` instead.

For more details consult <https://docs.storageos.com/docs/install/docker.html>

## Use StorageOS

You can now run containers backed by StorageOS volumes:

```
$ sudo docker run -it --rm --volume-driver storageos -v test01:/data alpine sh -c "echo hello > /data/myfile"
```

## Next Steps

To get the most out of StorageOS, try:

1. Running the CLI to manage volumes, rules, and cluster configuration. See <https://docs.storageos.com/docs/reference/cli.html>
2. Joining more nodes to the cluster. A quick start guide is available at <https://docs.storageos.com/docs/install/clusterinstall.html>
3. Fail containers to other nodes, or enable replication and fail Docker nodes.