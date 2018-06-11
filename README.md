## Get started with the go repo!
```
a. Ensure that your `GOPATH` is set. (https://github.com/golang/go/wiki/SettingGOPATH)
b. Go get the repo (`go get github.ibm.com/nabla-containers/runnc`).
```

## Install Runnc

1. Make binaries and copy to bin dir
```
# Go to the repo
cd $GOPATH/src/github.ibm.com/nabla-containers/runnc

# Get the neceesary binaries for the runtime
make build

# Copy the binaries to /usr/local/bin
sudo hack/copy_bins.sh

# Install genisoimage on host
sudo apt install genisoimage
```

2. Modify to add runtime to `/etc/docker/daemon.json`, for example:
```
{
    "default-runtime": "runc",
    "runtimes": {
        "runsc": {
            "path": "/usr/local/bin/runsc",
            "runtimeArgs": [
                "--network=sandbox"
            ]
       },
        "runnc": {
                "path": "/usr/local/bin/runnc",
                "runtimeArgs": [
                ]
        }
    }
}
```

3. Restart docker 

```systemctl restart docker```

4. Run with runtime:

```sudo docker run --rm --runtime=runnc lumjjb/user-node:v0```
