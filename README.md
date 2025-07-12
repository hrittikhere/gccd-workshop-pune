
```
export HF_TOKEN=hf_jmrCNEeKZYFRlppkvUCaAqgzYnYkRAmiC
```
```
kubectl create secret generic l4-demo \
    --from-literal=HUGGING_FACE_TOKEN=${HF_TOKEN} \
    --dry-run=client -o yaml | kubectl apply -f -
```
