LUAPOWER := $(HOME)/Apps/luapower/
OSARCH   := linux64

TMPLIB := tmplib
TMPINC := tmpinc
CMAKE_BUILD := build

LYAML_DIR := lyaml

LIBYAML_DIR := libyaml
LIBYAML_LIB := $(TMPLIB)/libyaml.a
LIBYAML_INC := $(TMPLIB)/yaml.h

.PHONY: distribution
distribution: libyaml build copy

.PHONY: copy
copy:
	mkdir -p luapower-lyaml/bin/$(OSARCH)/clib/
	/bin/cp $(CMAKE_BUILD)/yaml.so luapower-lyaml/bin/$(OSARCH)/clib/
	/bin/cp -r $(LYAML_DIR)/lib/lyaml luapower-lyaml/


.PHONY: build
build:
	@-/bin/rm -r ./$(CMAKE_BUILD)
	@mkdir $(CMAKE_BUILD)
	cd $(CMAKE_BUILD) && cmake -D LUA_INCLUDE_DIR=$(LUAPOWER)csrc/lua-headers/ -D LUA_LIBRARIES=$(LUAPOWER)bin/$(OSARCH)/libluajit.a .. && make

.PHONY: libyaml
libyaml:
	@-mkdir $(TMPLIB) $(TMPINC)
	cd $(LIBYAML_DIR) && ./bootstrap && ./configure --enable-shared=no --with-pic && make clean && make
	/bin/cp $(LIBYAML_DIR)/src/.libs/libyaml.a $(TMPLIB)
	/bin/cp $(LIBYAML_DIR)/include/yaml.h      $(TMPINC)

.PHONY: clean
clean:
	-/bin/rm -r ./$(TMPLIB) ./$(TMPINC) ./$(CMAKE_BUILD)
