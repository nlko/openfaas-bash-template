```
echo $OPENFAAS_ADMIN_PASSWORD | faas login -s

faas template pull https://github.com/nlko/openfaas-bash-template.git

faas new my-func --lang=bash 

mv my-func.yml stack.yml

faas new my-func2 --lang=bash -a stack.yml

faas build

faas deploy

echo hello | curl -X POST -d @- http://localhost:8080/function/my-func2

```