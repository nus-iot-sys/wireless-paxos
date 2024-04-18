all:
	$(MAKE) cooja TARGET=sky log=0 printf=1 tx=31 mch=0 pch=0 sec=0 src=2 sync=0 failure=0 dynamic=1 initiator=3 interval=39 max_node_count=$(nodes) duration=15 description=“multipaxos” -j4

CONTIKI_PROJECT = multipaxos-app
CONTIKI_WITH_CHAOS = 1
ifeq ($(dynamic),1)
	CHAOS_NODE_DYNAMIC=1
else
	ifeq ($(dynamic),2)
		CHAOS_NODE_DYNAMIC=1
	else
		CHAOS_NODE_DYNAMIC=0
	endif
endif

CFLAGS += -DPROJECT_CONF_H=\"project-conf.h\"

CONTIKI = ../../..
include $(CONTIKI)/Makefile.include

CONTIKI_TARGET_SOURCEFILES += contiki-wsn430-platform.c
include $(CONTIKI)/platform/wsn430/Makefile.common


id: burn-nodeid.upload
