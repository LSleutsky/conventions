## `Command Line`

```sh
# open chrome in cors-less state
open -n -a /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --args --user-data-dir="/tmp/chrome_dev_test" --disable-web-security
```

## `Neovim`

```sh
# copy filename method 1
!echo %:p | pbcopy
```

```sh
# copy filename method 2
!echo -n % | pbcopy
```

## `AWS`

```sh
# list clusters
aws eks list-clusters
```

```sh
# updates kubernetes config for given profile
aws eks update-kubeconfig --region <region_name> --name <cluster> --profile <aws_profile>
```

### `S3`

```sh
# list s3 buckets
aws s3 ls
```

```sh
# list s3 bucket contents
aws s3 ls s3://<bucket_name>
```

## `Kubernetes`

```sh
# get available kubernetes pods in given namespace
kubectl get pods -n <namespace>
```

```sh
# get specific pod in yaml format
kubectl get pod  -n <namespace> <pod> -o yaml
```

```sh
# edit specific kubernetes pod
kubectl edit pod -n <namespace> <pod> -o yaml
```

```sh
# deploy saved changes from the edit command above
kubectl apply -f <filename>
```
