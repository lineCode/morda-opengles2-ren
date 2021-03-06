include prorab.mk

include $(d)../raspberrypi.mk

this_name := morda-opengles2-ren

this_soname := $(shell cat $(d)soname.txt)

this_srcs += $(call prorab-src-dir,.)

this_cxxflags += -Wall # enable all warnings
this_cxxflags += -Wno-comment # no warnings on nested comments
this_cxxflags += -funsigned-char # the 'char' type is unsigned
this_cxxflags += -Wnon-virtual-dtor # warn if base class has non-virtual destructor
this_cxxflags += -fno-operator-names # do not treat 'and', 'bitand','bitor','compl','not','or','xor' as keywords
this_cxxflags += -Werror # treat warnings as errors
this_cxxflags += -Wfatal-errors # stop on first error encountered
this_cxxflags += -fstrict-aliasing # in order to comply with the c++ standard more strictly
this_cxxflags += -g # include debugging symbols
this_cxxflags += -std=c++14

ifeq ($(debug),true)
    this_cxxflags += -DDEBUG
else
    this_cxxflags += -O3
endif

ifeq ($(raspberrypi),true)
    this_cxxflags += -I/opt/vc/include
    this_ldflags += -L/opt/vc/lib
endif

ifeq ($(os), linux)
    this_cxxflags += -fPIC # generate position independent code
else ifeq ($(os), windows)
else ifeq ($(os), macosx)
    this_cxxflags += -stdlib=libc++ # this is needed to be able to use c++11 std lib
    this_ldlibs += -lc++
endif

ifeq ($(raspberrypi),true)
    this_ldlibs += -lbrcmGLESv2
else
    this_ldlibs += `pkg-config --libs glesv2`
endif

this_ldlibs += -lmorda

$(eval $(prorab-build-lib))
