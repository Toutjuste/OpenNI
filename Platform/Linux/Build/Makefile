#############################################################################
# OpenNI makefile.
# 
# default configuration is Release. for a debug version use:
# 	make CFG=Debug
#
# default compiler is g++. for another one use:
#   make CXX=<comp>
#
# By default, CLR projects will only be build if mono is installed.
# To force CLR projects use:
#   make FORCE_BUILD_CLR=1
#
#############################################################################

include Common/CommonDefs.mak

# list all modules
ALL_MODULES = \
	Modules/nimCodecs \
	Modules/nimMockNodes \
	Modules/nimRecorder

# list all utils
ALL_UTILS = \
	Utils/niReg \
	Utils/niLicense
	
# list all core projects
ALL_CORE_PROJS = \
	OpenNI \
	$(ALL_MODULES) \
	$(ALL_UTILS)

# list all samples
CORE_SAMPLES = \
	Samples/NiSimpleRead \
	Samples/NiBackRecorder \
	Samples/NiConvertXToONI \
	Samples/NiRecordSynthetic \
	Samples/NiSampleModule \
	Samples/NiSimpleCreate \
	Samples/NiCRead \
	Samples/NiAudioSample \
	Samples/NiSimpleSkeleton \
	Samples/NiSkeletonBenchmark
	
ifeq "$(GLUT_SUPPORTED)" "1"
	CORE_SAMPLES += \
		Samples/NiViewer \
		Samples/NiSimpleViewer \
		Samples/NiUserTracker \
		Samples/NiUserSelection \
		Samples/NiHandTracker
else
	ifeq "$(GLES_SUPPORTED)" "1"
		CORE_SAMPLES += \
			Samples/NiUserTracker \
			Samples/NiUserSelection
	endif
endif

ALL_SAMPLES = \
	$(CORE_SAMPLES)

# list all projects that are build
ALL_BUILD_PROJS = \
	$(ALL_CORE_PROJS) \
	$(ALL_SAMPLES)

ALL_PROJS = \
	$(ALL_BUILD_PROJS)

ALL_PROJS_CLEAN = $(foreach proj,$(ALL_PROJS),$(proj)-clean)

# define a function which creates a target for each proj
define CREATE_PROJ_TARGET
$1: 
	$$(MAKE) -C $1

$1-clean: 
	$$(MAKE) -C $1 clean
endef

################ TARGETS ##################

.PHONY: all $(ALL_PROJS) $(ALL_PROJS_CLEAN) install uninstall clean 

# make all makefiles
all: $(ALL_PROJS)

core: $(ALL_CORE_PROJS)

samples: $(ALL_SAMPLES)

# create projects targets
$(foreach proj,$(ALL_PROJS),$(eval $(call CREATE_PROJ_TARGET,$(proj))))

# additional dependencies
Modules/nimCodecs:		OpenNI
Modules/nimMockNodes:		OpenNI
Modules/nimRecorder:		OpenNI

Utils/niReg:			OpenNI
Utils/niLicense:		OpenNI

Samples/NiSimpleRead:		OpenNI
Samples/NiBackRecorder:		OpenNI
Samples/NiConvertXToONI:	OpenNI
Samples/NiRecordSynthetic:	OpenNI
Samples/NiSampleModule:		OpenNI
Samples/NiSimpleCreate:		OpenNI
Samples/NiCRead:		OpenNI
Samples/NiAudioSample:		OpenNI
Samples/NiSimpleSkeleton:	OpenNI
Samples/NiSkeletonBenchmark: OpenNI
Samples/NiUserTracker:		OpenNI
Samples/NiUserSelection:	OpenNI
Samples/NiHandTracker:		OpenNI
Samples/NiViewer:		OpenNI
Samples/NiSimpleViewer:		OpenNI

# clean is cleaning all projects
clean: $(ALL_PROJS_CLEAN)

# redist target
redist: all
	cd ../CreateRedist; ./RedistMaker; cd -

# install target
install: redist
	cd ../Redist; ./install.sh; cd -

# uninstall target
uninstall:
	cd ../Redist; ./install.sh -u; cd -


