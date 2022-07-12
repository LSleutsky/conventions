## Command Line

```sh
# copy filename from nvim command prompt
!echo %:p | pbcopy
```

```sh
# open chrome in cors-less state
open -n -a /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --args --user-data-dir="/tmp/chrome_dev_test" --disable-web-security
```

## Kubernetes

```sh
# get available kubernetes pods in given namespace
kubectl get pods -n <namespace>
```

```sh
# edit specific kubernetes pod
kubectl edit pod <pod name>
```

```sh
# deploy saved changes from the edit command above
kubectl apply -f <filename>
```
