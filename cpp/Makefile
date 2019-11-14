EXAMPLE_ENC:=encode
EXAMPLE_DEC:=decode

# comment for verbose ouptut
Q=@

COMMON_FLAGS=-O2 -g -Wall -fmessage-length=0 -I. -I../c

ARFLAGS=crs
LDFLAGS=
CFLAGS=${COMMON_FLAGS}
CPPFLAGS=${COMMON_FLAGS} -std=c++11

vpath %.cpp examples/encode examples/decode

ENC_SRCS:=encode.cpp fit_developer_field_description.cpp fit_developer_field_definition.cpp \
	fit_developer_field.cpp fit_field_base.cpp fit_date_time.cpp fit.cpp fit_buffer_encode.cpp \
	fit_crc.cpp fit_encode.cpp fit_field_definition.cpp fit_field.cpp fit_mesg_definition.cpp \
	fit_mesg.cpp fit_profile.cpp fit_protocol_validator.cpp fit_unicode.cpp
ENC_OBJS:=$(filter %.o,${ENC_SRCS:.c=.o} ${ENC_SRCS:.cpp=.o})

DEC_SRCS:=decode.cpp fit_buffered_record_mesg_broadcaster.cpp fit_field_base.cpp fit_protocol_validator.cpp \
	fit_unicode.cpp fit_factory.cpp fit_developer_field_description.cpp fit_field.cpp \
	fit_field_definition.cpp fit_date_time.cpp fit_accumulated_field.cpp fit_encode.cpp \
	fit_buffered_mesg_broadcaster.cpp fit_decode.cpp fit_developer_field_definition.cpp \
	fit_developer_field.cpp fit_crc.cpp fit_profile.cpp fit.cpp fit_mesg_definition.cpp \
	fit_mesg_with_event_broadcaster.cpp fit_mesg_broadcaster.cpp fit_mesg.cpp \
	fit_accumulator.cpp fit_buffer_encode.cpp
DEC_OBJS:=$(filter %.o,${DEC_SRCS:.c=.o} ${DEC_SRCS:.cpp=.o})

all: ${EXAMPLE_ENC} ${EXAMPLE_DEC}

${EXAMPLE_ENC}: ${ENC_OBJS}
	@echo LD $@
	${Q}${CXX} ${CFLAGS} ${CPPFLAGS} -o $@ ${ENC_OBJS} ${LDFLAGS}

${EXAMPLE_DEC}: ${DEC_OBJS}
	@echo LD $@
	${Q}${CXX} ${CFLAGS} ${CPPFLAGS} -o $@ ${DEC_OBJS} ${LDFLAGS}

%.o: %.c
	@echo CC $@ $<
	${Q}${CC} ${CFLAGS} -c -o $@ $<

%.o: %.cpp
	@echo CXX $@ $<
	${Q}${CXX} $(filter-out ${COMMON_FLAGS},${CFLAGS}) ${CPPFLAGS} -c -o $@ $<

.phony: clean
clean:
	rm -f ${ENC_OBJS} ${DEC_OBJS} ${EXAMPLE_ENC} ${EXAMPLE_DEC}
