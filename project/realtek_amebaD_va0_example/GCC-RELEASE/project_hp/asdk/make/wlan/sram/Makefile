include $(MAKE_INCLUDE_GEN)
IFLAGS               += -I$(BASEDIR)/component/common/network/libcoap/include

.PHONY: lib lib_mp lib_lp lib_lt clean

#*****************************************************************************#
#                               VARIABLES	                              #
#*****************************************************************************#
DIR = $(BASEDIR)/component/common/drivers/wlan/realtek/src
lib_mp:GLOBAL_CFLAGS += -DCONFIG_MP_INCLUDED
lib_lp:GLOBAL_CFLAGS += -DLOW_POWER_WIFI_CONNECT
lib_lt:GLOBAL_CFLAGS += -DLONG_PERIOD_TICKLESS
#*****************************************************************************#
#                               Object FILE LIST                              #
#*****************************************************************************#
OBJS += $(DIR)/core/rtw_xmit.o	\
	$(DIR)/core/rtw_recv.o \
	$(DIR)/osdep/freertos/lxbus_intf.o \
	$(DIR)/osdep/freertos/freertos_skbuff.o \
	$(DIR)/osdep/freertos/freertos_isr.o \
	$(DIR)/osdep/freertos/freertos_recv.o \
	$(DIR)/osdep/freertos/freertos_xmit.o \
	$(DIR)/osdep/freertos/rtk_wlan_if.o \

OBJS += $(DIR)/hal/phydm/phydm_cfotracking.o \
	$(DIR)/hal/phydm/phydm_antdiv.o \
	$(DIR)/hal/phydm/phydm_math_lib.o \
	$(DIR)/hal/phydm/phydm_phystatus.o \
	$(DIR)/hal/phydm/phydm_soml.o
	
OBJS += $(DIR)/hal/rtl8721d/src/lx_bus/rtl8721d_xmit.o
OBJS += $(DIR)/hal/rtl8721d/src/rtl8721d_rf_onoff.o


#include ../config/Makefile.config

#ifeq ($(CONFIG_HIGH_TP),y)
#OBJS += $(OBJS_CONFIG)
#endif
#*****************************************************************************#
#                               Dependency	                              #
#*****************************************************************************#
-include $(OBJS:.o=.d)

#*****************************************************************************#
#                        RULES TO GENERATE TARGETS                            #
#*****************************************************************************#

# Define the Rules to build the core targets
lib: CORE_TARGETS COPY_RAM_OBJS
lib_mp: CORE_TARGETS COPY_RAM_OBJS
lib_lp: CORE_TARGETS COPY_RAM_OBJS
lib_lt: CORE_TARGETS COPY_RAM_OBJS
#*****************************************************************************#
#              GENERATE OBJECT FILE 
#*****************************************************************************#
CORE_TARGETS:	$(OBJS)

%.o:%.c
	$(CC) $(GLOBAL_CFLAGS) $(MODULE_IFLAGS) $<  -o $@
	$(FROMELF) --prefix-sections .image2.net.ram $@
	
#*****************************************************************************#
#                        RULES TO CLEAN TARGETS                               #
#*****************************************************************************#
clean: CLEAN_OBJS 
	$(REMOVE) *.o
	$(REMOVE) *.i
	$(REMOVE) *.s
	$(REMOVE) *.d
