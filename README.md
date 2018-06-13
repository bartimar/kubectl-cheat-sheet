# kubectl-cheat-sheet
my kubectl cheat sheet

### bash completions ftw
https://kubernetes.io/docs/tasks/tools/install-kubectl/#enabling-shell-autocompletion

### aliases
```
alias k='kubectl'
alias kds='kubectl describe service'
alias kdd='kubectl describe deployment'
alias ksc='function _ksc(){ kubectl config set-context `kubectl config current-context` --namespace=$1; };_ksc'
alias kp-a='kubectl get pods --all-namespaces'
alias wk='watch kubectl get pods'
alias wka='watch kubectl get pods --all-namespaces'
alias kf='function _kf(){ kubectl logs -f $1;};_kf'
```

### rather than deleting a deployment, zeroscale it
```
alias zeroscale='function _zs(){ kubectl scale deploy $1 --replicas 0;}; _zs'
```
### list all pods that have more than one gcePersistentDisk volume in spec
```
kubectl get pods --all-namespaces  -o \
jsonpath="{range .items[*]}{'\n'}{.metadata.name}{': '}{range .spec.volumes[*]}{.gcePersistentDisk.pdName}{end}{'\n'}{end}" \
| tail -n +2 \
| awk 'NF>=2'
```
