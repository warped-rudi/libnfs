noinst_LTLIBRARIES = libnlm.la

nlm_SOURCES_GENERATED =
nlm_HEADERS_GENERATED =
nlm_GENERATED = $(nlm_SOURCES_GENERATED) $(nlm_HEADERS_GENERATED)

CLEANFILES = $(nlm_GENERATED) nlm-stamp

libnlm_la_CPPFLAGS = -I$(abs_top_srcdir)/include \
		     -I$(abs_top_srcdir)/include/nfsc
libnlm_la_SOURCES = \
	$(nlm_SOURCES_GENERATED) \
	nlm.c libnfs-raw-nlm.c

$(nlm_GENERATED) : nlm-stamp
nlm-stamp : nlm.x
	rm -f $(nlm_GENERATED)
	touch nlm-stamp

compile_rpc:	
	rpcgen -h @RPCGENFLAGS@ nlm.x | sed -e "s/#include <rpc\/rpc.h>//" | sed -e "s/xdr/zdr/g" -e "s/XDR/ZDR/g" > libnfs-raw-nlm.h
	rpcgen -c @RPCGENFLAGS@ nlm.x | sed -e "s/#include \".*nlm.h\"/#include \"libnfs-xdr.h\"\n#include \"libnfs-raw-nlm.h\"/" -e "s/xdr/zdr/g" -e "s/XDR/ZDR/g" -e "s/register int32_t \*buf;/register int32_t *buf;\n	buf = NULL;/" > libnfs-raw-nlm.c
