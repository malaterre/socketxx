SET(TESTSRCS
  # tdunread.C:(.text+0xc8): undefined reference to `isockunix::isockunix(sockbuf::type, int)'
  # tdunread  
  # tdunwrite.C:(.text+0xc8): undefined reference to `osockunix::osockunix(sockbuf::type, int)'
  #tdunwrite
	tdinread 
# tdinwrite
  # tsunread.C:(.text+0xc5): undefined reference to `sockunixbuf::sockunixbuf(sockbuf::type, int)'
  #	tsunread 
  # tsunwrite.C:(.text+0xc8): undefined reference to `iosockunix::iosockunix(sockbuf::type, int)'
  #tsunwrite
	tpopentest
	tnntp
  # error: cast from ‘sockinetbuf*’ to ‘unsigned int’ loses precision
  # thostnames
	twhois
	tbind-0 tbind-1
	test_sockerr
  # error: ‘inet_ntoa’ was not declared in this scope
  #simple_httpd.C
  )

IF(WIN32)
ELSE(WIN32)
SET(TESTSRCS
${TESTSRCS}
	tsecho tcecho
	tsockpair
	tcsmtp
        tcftp
	testall
	tsinread tsinwrite
	tfork tfork0
	tpipe
	tpopen tpopen-lpc tpopen-ftp
	tsendfiles
        tsig-0
	tsmtp
)

ENDIF(WIN32)

foreach( test ${TESTSRCS} )
ADD_EXECUTABLE(${test} ${test}.C)
target_link_libraries(${test} ${SOCKETXX_LIBRARY_NAME})
endforeach()


#.PHONY: check
#check: testall.out
#	diff -c testall.exp testall.out || make -f Makefile.in message
#
#message:
#	@echo
#	@echo If there are any differences, manually check whether
#	@echo testall.out and testall.exp have the same lines but
#	@echo only their order is different. If they have the same
#	@echo lines but for the order, you have installed properly.
#	@echo Otherwise, try to findout what might be the reason and
#	@echo if you could not please email me with your problem at
#	@echo gs4t@virginia.edu
#	@echo
#
#
#testall.out: $(TESTS)
#	./testall > testall.out
