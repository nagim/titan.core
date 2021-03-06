##############################################################################
# Copyright (c) 2000-2018 Ericsson Telecom AB
# All rights reserved. This program and the accompanying materials
# are made available under the terms of the Eclipse Public License v2.0
# which accompanies this distribution, and is available at
# https://www.eclipse.org/org/documents/epl-2.0/EPL-2.0.html
#
# Contributors:
#   Szabo, Bence Janos
#
##############################################################################
TOPDIR := ../../../..
include $(TOPDIR)/Makefile.regression

ifdef LCOV
COVERAGE_FLAG := -C
endif

# ${MAKEPROG} has the same content as the built-in ${MAKE},
# except the special handling of ${MAKE} does not apply.
# If we used ${MAKE} in the rules below, 'make -n' would succeed once,
# then fail on every subsequent invocation until a 'make clean' is done. 

# Hierarchy
#            a
#            |
#            b<---<
#         c:1|    |
#            c    |b:1
#    c:1=>d:1|    |
#            d>--->
#Result will be: a:Default, b:Default, c:1, d:1
MAKEPROG := ${MAKE}

all: CheckTpd 

BuildTpd:
	$(TTCN3_DIR)/bin/ttcn3_makefilegen -F $(MFGEN_FLAGS) $(COVERAGE_FLAG) \
	-t a.tpd -r -c -W -g

CheckTpd: BuildTpd
	if [ ! -f "./a_binDefault/Makefile" ] || [ `grep -c "EXECUTABLE = binDefault" ./a_binDefault/Makefile` -ne 1 ]; \
	then echo "Makefilegen required config test 52 failed: Overall verdict: fail" && exit 1; fi
	if [ ! -f "./b_binDefault/Makefile" ] || [ `grep -c "EXECUTABLE = binDefault" ./b_binDefault/Makefile` -ne 1 ]; \
	then echo "Makefilegen required config test 52 failed: Overall verdict: fail" && exit 1; fi
	if [ ! -f "./c_bin1/Makefile" ] || [ `grep -c "EXECUTABLE = bin1" ./c_bin1/Makefile` -ne 1 ]; \
	then echo "Makefilegen required config test 52 failed: Overall verdict: fail" && exit 1; fi
	if [ ! -f "./d_bin1/Makefile" ] || [ `grep -c "EXECUTABLE = bin1" ./d_bin1/Makefile` -ne 1 ]; \
	then echo "Makefilegen required config test 52 failed: Overall verdict: fail" && exit 1; fi

clean:
	-rm -rf a_binDefault b_binDefault c_bin1 d_bin1

distclean: clean
	-rm -f *.out

.PHONY: all clean distclean BuildTpd CheckTpd

