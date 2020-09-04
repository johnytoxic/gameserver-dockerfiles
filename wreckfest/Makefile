IMAGE_NAME=jdoubleu/wreckfest
VARIATIONS=base no-restrictions

.PHONY: clean

all: $(addprefix image-, ${VARIATIONS})

image-%:
	docker build -t ${IMAGE_NAME}:$* $*

clean: $(addprefix rmi-, ${VARIATIONS})

rmi-%:
	docker rmi $*
