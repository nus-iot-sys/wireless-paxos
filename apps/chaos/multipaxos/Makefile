CONTIKI_PROJECT = multipaxos-app
TARGET ?= sky

log=0
printf=1 
tx=31 
mch=0 
pch=0
sec=0
src=2
sync=0
failure=0
initiator=3
interval=39

$(if $(nodes),,$(error Please specify the number of nodes with make nodes=))

FIRMWARE = firmware/multipaxos-app_n$(nodes).$(TARGET)

all: make_firmware

.PHONY: make_firmware
make_firmware: $(CONTIKI_PROJECT)
	mv $(CONTIKI_PROJECT).$(TARGET) $(FIRMWARE)

CONTIKI_WITH_CHAOS = 1
CHAOS_NODE_DYNAMIC=1

CFLAGS += -DPROJECT_CONF_H=\"project-conf.h\"

CFLAGS+=-DCOOJA=1 -DWITH_TINYOS_AUTO_IDS=1 

CONTIKI = ../../..
include $(CONTIKI)/Makefile.include

# CONTIKI_TARGET_SOURCEFILES += contiki-wsn430-platform.c
# include $(CONTIKI)/platform/wsn430/Makefile.common

id: burn-nodeid.upload

# .PHONY bytes
# bytes: $(CONTIKI_PROJECT)
# 	msp430-size $(CONTIKI_PROJECT).${TARGET}
# #	$(OBJDUMP) -h $(CONTIKI_PROJECT).sky | perl -ne '$$b{$$1}=hex $$2 if /^\s*\d+\s*\.(text|data|bss|chaos)\s+(\S+)/; END { printf("%16d bytes in ROM\n%16d bytes in RAM\n",$$b{text}+$$b{data},$$b{data}+$$b{bss}); }'
# 	@echo '    ' `date`
