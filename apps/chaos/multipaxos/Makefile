CONTIKI_PROJECT = multipaxos-app
TARGET = sky

log=0
printf=1 
tx=31 
mch=0 
pch=0
sec=0
src=2
sync=0
interval=39

CW_CONFIG_HEADER = configs/config_$(config).h

FIRMWARE = firmware/multipaxos-app_$(config).$(TARGET)

all: $(FIRMWARE)

$(FIRMWARE): touch_config $(CONTIKI_PROJECT) firmware/
	mv $(CONTIKI_PROJECT).$(TARGET) $@

.PHONY: touch_config
touch_config:
	@if [ -z $(config) ]; then \
		echo "config is not set. Use 'make config=example' to set the configuration"; \
		exit 1; \
	fi
	@if [ -f $(CW_CONFIG_HEADER) ]; then \
		touch $(CW_CONFIG_HEADER); \
		touch project-conf.h; \
	else \
		echo "Configuration $(config) does not exist"; \
		exit 1; \
	fi

firmware/:
	mkdir -p $@

PROJECTDIRS += configs
PROJECT_HEADERS += $(CW_CONFIG_HEADER)

CONTIKI_WITH_CHAOS = 1
CHAOS_NODE_DYNAMIC=0

CFLAGS += -DPROJECT_CONF_H=\"project-conf.h\"
CFLAGS += -DCW_CONFIG_HEADER=\"$(CW_CONFIG_HEADER)\"

CFLAGS += -DCOOJA=1 -DWITH_TINYOS_AUTO_IDS=1 

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
