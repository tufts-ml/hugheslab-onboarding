
# One-time setup (macbook)

### Create a nickname'd entry in your .ssh/config file

```
Host tuftshpc
    User {YOUR_USERNAME_HERE}
    HostName login.cluster.tufts.edu
    ControlMaster auto
    ControlPath ~/.ssh/%r@%h:%p
    UseKeychain yes
```

This will let you cleanly refer to the remote filesystem as `tuftshpc`

# Every time

### Login to the cluster

Follow standard procedures to log into the cluster 

1) Open VPN and start a secure session

2) Log into the tufts HPC via an SSH tunnel in a window of your terminal

```
$ ssh tuftshpc
```

### Use scp to move files to/from the cluster

Open a fresh terminal. Keep the old window open (so the tunnel is open).

The `scp` works just like Unix's `cp` command, but over SSH tunnels

Setup the local path (on your laptop filesystem) and the remote path

```
REMOTE_PATH=/cluster/tufts/hugheslab/datasets/
LOCAL_PATH='/Users/mhughes/Desktop/
```

Send data to the cluster
```
scp $LOCAL_PATH/myfile.txt tuftshpc:$REMOTE_PATH
```

Copy data from the cluster

```
scp tuftshpc:$REMOTE_PATH/myfile.txt $LOCAL_PATH
```
