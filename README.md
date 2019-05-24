# Docker OpenFaaS 

This is based on this [guide](https://blog.alexellis.io/cli-functions-with-openfaas/), using Ubuntu instead od Alpien since the glibc dependency in [wasmer](https://wasmer.io)

## Buid Container

```shell
 faas build -f wasm.yml
```

## Enter in the container

```shell
docker run -it wasm sh
```

