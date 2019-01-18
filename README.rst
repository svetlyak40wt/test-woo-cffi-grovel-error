A test to check cffi-grovel is loaded automatically when you do
``qlot install`` and your project have dependency from Woo.

Seems, that this commit has broken everything:

https://github.com/fukamachi/woo/commit/52bf0ede5c2798cb170e0c298e834ee67d79c3d8

because before it everything has worked fine.

To run a check
==============

Run::

  qlot install

It should fail with this error::

  While evaluating the form starting at line 1, column 0
  of #P"/Users/art/projects/lisp/test-woo/quicklisp/dists/woo/software/woo-52bf0ede5c2798cb170e0c298e834ee67d79c3d8/woo.asd":
  Unhandled MISSING-COMPONENT in thread #<SB-THREAD:THREAD "main thread" RUNNING {10005205B3}>: Component "cffi-grovel" not found
  
  Backtrace for: #<SB-THREAD:THREAD "main thread" RUNNING {10005205B3}>
  0: (SB-DEBUG::DEBUGGER-DISABLED-HOOK Component "cffi-grovel" not found #<unused argument> :QUIT T)
  1: (SB-DEBUG::RUN-HOOK SB-EXT:*INVOKE-DEBUGGER-HOOK* Component "cffi-grovel" not found)
  2: (INVOKE-DEBUGGER Component "cffi-grovel" not found)
  3: (ERROR MISSING-COMPONENT :REQUIRES "cffi-grovel")
  4: ((:METHOD OPERATE (SYMBOL T)) LOAD-OP "cffi-grovel" :VERBOSE NIL) [fast-method]
  5: ((SB-PCL::EMF OPERATE) #<unused argument> #<unused argument> LOAD-OP "cffi-grovel" :VERBOSE NIL)
  6: ((LAMBDA NIL :IN OPERATE))
  7: ((:METHOD OPERATE :AROUND (T T)) LOAD-OP "cffi-grovel" :VERBOSE NIL) [fast-method]
  8: (LOAD-SYSTEM "cffi-grovel" :VERBOSE NIL)
  9: (QUICKLISP-CLIENT::CALL-WITH-MACROEXPAND-PROGRESS #<CLOSURE (LAMBDA NIL :IN QUICKLISP-CLIENT::APPLY-LOAD-STRATEGY) {10035D585B}>)
  10: (QUICKLISP-CLIENT::AUTOLOAD-SYSTEM-AND-DEPENDENCIES "cffi-grovel" :PROMPT NIL)
  11: ((:METHOD QL-IMPL-UTIL::%CALL-WITH-QUIET-COMPILATION (T T)) #<unused argument> #<CLOSURE (FLET QUICKLISP-CLIENT::QL :IN QUICKLISP-CLIENT:QUICKLOAD) {10032BA12B}>) [fast-method]
  12: ((:METHOD QL-IMPL-UTIL::%CALL-WITH-QUIET-COMPILATION :AROUND (QL-IMPL:SBCL T)) #<QL-IMPL:SBCL {1005FAB703}> #<CLOSURE (FLET QUICKLISP-CLIENT::QL :IN QUICKLISP-CLIENT:QUICKLOAD) {10032BA12B}>) [fast-method]
  13: ((:METHOD QUICKLISP-CLIENT:QUICKLOAD (T)) "cffi-grovel" :PROMPT NIL :SILENT T :VERBOSE NIL) [fast-method]
  14: (QL-DIST::CALL-WITH-CONSISTENT-DISTS #<CLOSURE (LAMBDA NIL :IN QUICKLISP-CLIENT:QUICKLOAD) {10032AACBB}>)
  15: ((FLET "H0" :IN QLOT/INSTALL::APPLY-QLFILE-TO-QLHOME) Component "cffi-grovel" not found, required by NIL)
  16: (SB-KERNEL::%SIGNAL Component "cffi-grovel" not found, required by NIL)
  17: (ERROR MISSING-DEPENDENCY :REQUIRED-BY NIL :REQUIRES "cffi-grovel")
  18: (ASDF/FIND-COMPONENT:RESOLVE-DEPENDENCY-NAME NIL "cffi-grovel" NIL)
  19: ((LAMBDA NIL :IN ASDF/PARSE-DEFSYSTEM:REGISTER-SYSTEM-DEFINITION))
  ...
