
LBITS             := $(shell getconf LONG_BIT)
ifeq ($(LBITS),64)
PROGNAME          := ICCBusiness
LIBHASP_KEYDOG    := hasp_linux_x86_64_108728
RELEASE_PATH      := ../../output/Linux/Release_64/twomachine/ICCBUSINESS/exe
else
PROGNAME          := ICCBusiness
LIBHASP_KEYDOG    := hasp_linux_108728
RELEASE_PATH      := ../../output/Linux/Release_32/twomachine/ICCBUSINESS/exe
endif

CFLAGS          := -g -O -Wall -fPIC -Wformat
CPPFLAGS        := -g -O -Wall -fPIC -Wformat  -std=c++0x
LINKFLAGS       := -lpthread -lrt -lstdc++ -lVOS -lVDB_SQlite -l$(LIBHASP_KEYDOG) -lperipheral -lRide -lgpio -lasound -lwebrtc -lmysqlclient -ldl -Wl,-rpath ./
USER_MACROS     := LINUX DEBUG
C_MACROS		:= $(USER_MACROS) USE_WEBSOCKET USE_STACK_SIZE=102400
LIB_PATH        := $(RELEASE_PATH)
INC_PATH    	:= ../../h ../../h/json ../../h/civetweb ../../h/audio ../../h/db ../../h/mysql ../../h/peripheral ../../h/transport ../../h/webrtc ../../h/plate ../../h/police ../../h/gps ../../h/idcard ../../h/usb ../../h/scene ../../h/websocket ../../h/fpru
SRC_PATH        := ../../c ../../c/audio ../../c/db ../../c/peripheral ../../c/transport ../../c/plate ../../c/police ../../c/gps ../../c/idcard ../../c/usb ../../c/scene ../../c/websocket ../../c/fpru
ONEMACHINE_PATH := ../../output/Linux/Release_64/onemachine/exe 
TWOMACHINE_PATH := $(RELEASE_PATH)
EXE_NAME        := $(PROGNAME).exe
SRC_CPP         := $(foreach SRC_PATH,$(SRC_PATH), $(wildcard $(SRC_PATH)/*.cpp))
SRC_C						:= $(foreach SRC_PATH,$(SRC_PATH), $(wildcard $(SRC_PATH)/*.c))
OBJ_CPP         := $(patsubst %.cpp,%.o,$(SRC_CPP))
OBJ_C						:= $(patsubst %.c,%.o,$(SRC_C))
#OBJ_CPP        := $(notdir $(OBJ_CPP))
#OBJ_C          := $(notdir $(OBJ_C))
OBJS						:= $(OBJ_C)
OBJS            += $(OBJ_CPP)
CC							:= gcc
CXX             := g++

build:      $(EXE_NAME)
	cp $(EXE_NAME) $(TWOMACHINE_PATH)
	cp $(EXE_NAME) $(ONEMACHINE_PATH)
clean:
	rm -f $(OBJS)
	rm -f $(EXE_NAME)
	rm -f *~ */*~

# Compiling to object files.
%.o:%.cpp
	$(CXX) $(CPPFLAGS) $(addprefix -D,$(USER_MACROS)) $(addprefix -I,$(INC_PATH)) -c $< -o $@
%.o:%.c
	$(CC) $(CFLAGS) $(addprefix -D,$(C_MACROS)) $(addprefix -I,$(INC_PATH)) -c $< -o $@

# Linking to execute file.
$(EXE_NAME): $(OBJS)
	@echo "Link..."
	$(CXX) $(CPPFLAGS) $(LINKFLAGS) -o $@ $(OBJS) $(addprefix -L,$(LIB_PATH))
