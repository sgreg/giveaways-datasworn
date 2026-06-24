DATASWORN_ID_IS = giveaways_classic
DATASWORN_ID_SF = giveaways_starforged

VERSION ?= $(shell /bin/date +%Y%m%d-%H%M%S)
OUTDIR ?= dist
OUTFILE_IS = $(OUTDIR)/$(DATASWORN_ID_IS)-datasworn.$(VERSION).json
OUTFILE_SF = $(OUTDIR)/$(DATASWORN_ID_SF)-datasworn.$(VERSION).json

all: get

foo:
	@echo $(OUTFILE_IS) $(OUTFILE_SF)

sanity:
	@if [[ ${PWD}/ == */.dsbuild/ || ! -d .dsbuild ]] ; then\
		echo "Must be run from source repository root directory";\
		echo "";\
		exit 1;\
	fi
	@mkdir -p ${OUTDIR}

build: sanity
	docker rm -i dsbuilder
	docker run --name dsbuilder --volume .:/data:z datasworn-builder:0.1 /data/.dsbuild

get: build
	docker cp dsbuilder:/home/datasworn/datasworn/datasworn/$(DATASWORN_ID_IS)/$(DATASWORN_ID_IS).json $(OUTFILE_IS)
	docker cp dsbuilder:/home/datasworn/datasworn/datasworn/$(DATASWORN_ID_SF)/$(DATASWORN_ID_SF).json $(OUTFILE_SF)
	@echo ""
	@ls -l $(OUTFILE_IS) $(OUTFILE_SF)
