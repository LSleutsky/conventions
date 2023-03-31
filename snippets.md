# Command Line 

```sh
# open chrome in cors-less state
open -n -a /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --args --user-data-dir="/tmp/chrome_dev_test" --disable-web-security
```

```sh
# prepend text to file
cat <<< "prepend"
$(cat file) > file
```

```sh
# add text to file heredoc
cat >> file << EOF
add content
on multiple lines
if needed
EOF

# override file heredoc
cat > file << EOF
whatever new content
will be in file
overwriting existing
EOF
```

```sh
# kill homebrew process
rm -rf $(brew --prefix)/var/homebrew/locks
```

# Neovim 

```sh
# copy filename method 1
!echo %:p | pbcopy
```

```sh
# copy filename method 2
!echo -n % | pbcopy
```

```sh
# treesitter dependencies
TSInstall bash comment css diff dockerfile dot git_rebase gitattributes gitcommit gitignore graphql help hjson html http javascript jsdoc json json5 jsonc lua make markdown markdown_inline mermaid php pug python query regex ruby rust scss todotxt toml tsx typescript vim yaml
```

```sh
# mason language servers
MasonInstall bash-language-server chrome-debug-adapter css-lsp cssmodules-language-server diagnostics-languageserver docker-compose-language-service dockerfile-language-server dot-language-server eslint-lsp eslint_d firefox-debug-adapter html-lsp js-debug-adapter json-lsp jsonlint lua-language-server node-debug2-adapter prettier stylua tailwindcss-language-server typescript-language-server vim-language-server yaml-language-server yamllint
```

```sh
# case insensitive search
\<search\>\c

# case sensitive search
\<search\>\C
```

# AWS 

```sh
# list clusters
aws eks list-clusters
```

```sh
# updates kubernetes config for given profile
aws eks update-kubeconfig --region <region_name> --name <cluster> --profile <aws_profile>
```

## S3 

```sh
# list s3 buckets
aws s3 ls
```

```sh
# list s3 bucket contents
aws s3 ls s3://<bucket_name>
```

```sh
# copy from local dir to s3
aws s3 cp <local> s3://<bucket_name>

# copy from local dir to s3 with public read permissions
aws s3 cp <local> s3://<bucket_name> --acl public-read
```

# Kubernetes 

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

# Linux

```sh
# arch linux archinstall fix
find /usr/lib/python3.10/site-packages/archinstall/ -type f -exec sed -i "s/lsblk --json/lsblk -a -e <MAJ #> --json/g" {} \;
```
