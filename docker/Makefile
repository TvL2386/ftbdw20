.RECIPEPREFIX = >

IMG := tvl2386/ftbdw20:2.5.0

extract:
> mkdir extract && \
    unzip *.zip -d extract || (rm -rf extract && false)

PHONY: build
build: extract
> docker build . -t $(IMG)

.PHONY: push
push:
> docker push $(IMG)

.PHONY: deploy
deploy:
> kubectl --context=proxmox --namespace=mc3 delete deployment mcserver && \
    kubectl --context=proxmox --namespace=mc3 apply -f ../mcserver-dep.yml

PHONY: bash
bash:
> docker run --rm -it $(IMG) /bin/bash

PHONY: all
all: build push

PHONY: clean
clean:
> rm -rf extract
