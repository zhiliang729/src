#	$OpenBSD: Makefile,v 1.8 2020/05/25 15:53:14 deraadt Exp $

NOMAN=
#MAN=		boot.8

.if ${MACHINE} == "octeon"
all: bsd rdboot

bsd:
	cd ${.CURDIR}/../../compile/BOOT && \
	    ${MAKE} config && ${MAKE} clean && ${MAKE}
	cp -p ${.CURDIR}/../../compile/BOOT/obj/bsd bsd

rdboot:
	cp -p ${.CURDIR}/../rdboot/obj/rdboot rdboot
	strip rdboot

mr.fs: rdboot
	rm -rf $@.d
	install -d -o root -g wheel $@.d/dev
	install -d -o root -g wheel $@.d/mnt
	install -d -o root -g wheel $@.d/sbin
	install -o ${BINOWN} -g ${BINGRP} -m 555 rdboot $@.d/sbin/init
	cd $@.d/dev && sh ${DESTDIR}/dev/MAKEDEV boot
	makefs -o disklabel=rdboot,minfree=0,density=1024 $@ $@.d

boot: bsd mr.fs
	cp bsd boot
	rdsetroot boot mr.fs

realinstall: boot
	${INSTALL} -o ${BINOWN} -g ${BINGRP} -m 444 boot ${DESTDIR}/usr/mdec

clean:
	rm -f boot bsd mr.fs rdboot
	rm -rf mr.fs.d
.endif

.include <bsd.prog.mk>
