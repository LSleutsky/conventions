## Command Line

```sh
# copy filename method 1
!echo %:p | pbcopy
```

```sh
# copy filename method 2
!echo -n % | pbcopy
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
# get specific pod in yaml format
kubectl get pod <pod> -o yaml

# get specific pod in json format
kubectl get pod <pod> -o json
```

```sh
# edit specific kubernetes pod
kubectl edit pod <pod>
```

```sh
# deploy saved changes from the edit command above
kubectl apply -f <filename>
```
