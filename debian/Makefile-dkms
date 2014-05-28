SHELL=/bin/bash
export KVER=$(KERNELRELEASE)
export KDIR=/lib/modules/$(KERNELRELEASE)/build

all:
	cd scst && $(MAKE) $@
	cd iscsi-scst && $(MAKE) include/iscsi_scst_itf_ver.h && $(MAKE) mods
	cd scst_local && $(MAKE) $@
	cd qla2x00t && BUILD_2X_MODULE=y CONFIG_SCSI_QLA_FC=y CONFIG_SCSI_QLA2XXX_TARGET=y $(MAKE) $@ 
	cd qla2x00t/qla2x00-target && BUILD_2X_MODULE=y CONFIG_SCSI_QLA_FC=y CONFIG_SCSI_QLA2XXX_TARGET=y $(MAKE) $@

fcst:
	cd fcst && cp ../scst/src/Module*.symvers . && $(MAKE) -C $(KDIR) SUBDIRS=$(shell pwd)/fcst BUILD_INI=m SCST_INC_DIR=$(shell pwd)/scst/include

.PHONY: all
