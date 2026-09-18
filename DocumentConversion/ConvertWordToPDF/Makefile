UNAME := $(shell uname)

CXX ?= $(if $(filter Darwin,$(UNAME)),clang++,g++)

TARGET = convert_word_to_pdf
SRC = convert_word_to_pdf.cpp

SDK_ROOT ?= ../../..

CXXFLAGS = -std=c++17 -I$(SDK_ROOT)/include
# The sample calls only the Office-to-PDF SDK (office_to_pdf_sdk). That shared
# library loads the datalogics_interface interface and APDFL itself at run time;
# datalogics_interface_api is listed so the linker resolves that dependency
# chain from the SDK lib directory.
LDFLAGS = -L$(SDK_ROOT)/lib -loffice_to_pdf_sdk -ldatalogics_interface_api

SDK_LIB := $(abspath $(SDK_ROOT)/lib)

ifeq ($(UNAME),Darwin)
  LDFLAGS += -Wl,-rpath,$(SDK_LIB)
else
  LDFLAGS += -Wl,-rpath,$(SDK_LIB)
endif

all: $(TARGET)

$(TARGET): $(SRC)
	$(CXX) $(CXXFLAGS) -o $@ $< $(LDFLAGS)

clean:
	rm -f $(TARGET)

run: $(TARGET)
	./$(TARGET)

.PHONY: all clean run
