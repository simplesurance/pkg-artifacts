PRISMA_ENGINES_VERSION=3.9.0

.PHONY: all
all: build.arm64 cp.arm64

.PHONY: build.arm64
build.arm64:
	echo "alpine-prisma-build-$(shell date '+%Y%m%d.%H%M%S.%N')" > .iid
	docker buildx build \
		--build-arg PRISMA_ENGINES_VERSION=$(PRISMA_ENGINE_VERSION) \
		--platform linux/arm64 \
		--output type=docker \
		-t $(shell cat .iid) \
		.

.PHONY: cp.arm64
cp.arm64:
	cid=$$(docker create $(shell cat .iid))
	docker cp $$cid:/prisma/prisma-engines-${PRISMA_ENGINES_VERSION}.musl-arm64.tar.gz .
	docker rm -f $$cid
