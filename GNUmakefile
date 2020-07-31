GOCMD=go
TEST?=$$(go list ./... |grep -v 'vendor')
INSTALL_DIR=~/.terraform.d/plugins
BINARY=terraform-provider-equinix

default: clean build test

all: default
	
test:
	echo $(TEST) | \
		xargs -t ${GOCMD} test -v $(TESTARGS)

testacc:
	TF_ACC=1 TF_SCHEMA_PANIC_ON_ERROR=1 ${GOCMD} test $(TEST) -v $(TESTARGS)

build:
	${GOCMD} build -o ${BINARY}

install: test build
	@if [ -d ${INSTALL_DIR} ]; then \
		echo "==> [INFO] installing in ${INSTALL_DIR} directory"; \
		cp ${BINARY} ${INSTALL_DIR}; \
	else \
		echo "==> [ERROR] installation plugin directory ${INSTALL_DIR} does not exist"; \
	fi

clean:
	${GOCMD} clean
	rm -f ${BINARY}

.PHONY: test testacc build install clean
