# Additional comments

## Clients to interact with backing store


### Client: deploy and configure

deploy a client pod and configure it by installing s3fs and mounting it against a noobaa bucket

deploy

```
kubectl apply -f ../deploy/ubuntu-fuse.yaml
```

login to pod

`kubectl exec -it ubuntu-fuse -- bash`

install s3fs

```
apt-get update
apt-get install s3fs
```

create secret file; copy secrets created by noobaa in [this step](../README.md#configure-aws-s3-cli)

```
echo "access key:secret key" > ${HOME}/s3cred
chmod 600 ${HOME}/s3cred
```

mount

```
s3fs bucket-from-noobaa  /mnt -o passwd_file=${HOME}/s3cred,use_path_request_style,url=http://s3:80
```

**Note:** `bucket-from-noobaa` is a bucket that was previously created on noobaa (e.g. in [this step](../README.md#run-aws-s3-commands))

### Client interactions with noobaa objects