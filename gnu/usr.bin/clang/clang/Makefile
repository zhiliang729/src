# $OpenBSD: Makefile,v 1.16 2020/08/03 14:45:22 patrick Exp $

.include <bsd.own.mk>

PROG=	clang
BINDIR=	/usr/bin
LIBEXECDIR=/usr/libexec
SRCS=	driver.cpp \
	cc1_main.cpp \
	cc1as_main.cpp \
	cc1gen_reproducer_main.cpp

LINKS=	${BINDIR}/clang ${BINDIR}/clang++ \
	${BINDIR}/clang ${BINDIR}/clang-cpp

.if ${COMPILER_VERSION:L} == "clang"
LINKS+=	${BINDIR}/clang ${BINDIR}/cc \
	${BINDIR}/clang ${BINDIR}/c++ \
	${BINDIR}/clang ${LIBEXECDIR}/cpp

maninstall:
	cd ${DESTDIR}${MANDIR}1 && { \
	rm -f cc.1 && ln clang.1 cc.1; \
	rm -f c++.1 && ln clang.1 c++.1; \
	rm -f cpp.1 && ln clang.1 cpp.1; }
.endif

CPPFLAGS+=	-I${.CURDIR}/../../../llvm/clang/include

.PATH:	${.CURDIR}/../../../llvm/clang/tools/driver

LLVM_LIBDEPS=	LLVM \
		clangFrontendTool \
		clangFrontend \
		clangDriver \
		clangDriverArch \
		clangSerialization \
		clangCodeGen \
		clangParse \
		clangSema \
		clangRewriteFrontend \
		clangRewrite \
		clangAnalysis \
		clangEdit \
		clangAST \
		clangLex \
		clangBasic \
		clangBasicTargets

.include <bsd.prog.mk>
