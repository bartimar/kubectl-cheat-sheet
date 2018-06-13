# kubectl-cheat-sheet
my kubectl cheat sheet

### list all pods that have more than one gcePersistentDisk volume in spec
```
kubectl get pods --all-namespaces  -o \
jsonpath="{range .items[*]}{'\n'}{.metadata.name}{': '}{range .spec.volumes[*]}{.gcePersistentDisk.pdName}{end}{'\n'}{end}" \
| tail -n +2 \
| awk 'NF>=2'
```
