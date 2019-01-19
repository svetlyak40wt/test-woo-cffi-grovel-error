A test to check cffi-grovel is loaded automatically when you do
``qlot install`` and your project have dependency from Woo.

Seems, that this commit has broken everything: `52bf0ede5c2798cb170e0c298e834ee67d79c3d8`_
because before it everything has worked fine. Probably, because where
was ``(ql:quickload :cffi-grovel)`` in the ``woo.asd`` file and it was
removed in the abovementioned commit.

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
  9: (QUICKLISP-CLIENT::CALL-WITH-MACROEXPAND-PROGRESS #<CLOSURE (LAMBDA NIL :IN QUICKLISP-CLIENT::APPLY-LOAD-STRATEGY) {100388575B}>)
  10: (QUICKLISP-CLIENT::AUTOLOAD-SYSTEM-AND-DEPENDENCIES "cffi-grovel" :PROMPT NIL)
  11: ((:METHOD QL-IMPL-UTIL::%CALL-WITH-QUIET-COMPILATION (T T)) #<unused argument> #<CLOSURE (FLET QUICKLISP-CLIENT::QL :IN QUICKLISP-CLIENT:QUICKLOAD) {100354A12B}>) [fast-method]
  12: ((:METHOD QL-IMPL-UTIL::%CALL-WITH-QUIET-COMPILATION :AROUND (QL-IMPL:SBCL T)) #<QL-IMPL:SBCL {1005FAB703}> #<CLOSURE (FLET QUICKLISP-CLIENT::QL :IN QUICKLISP-CLIENT:QUICKLOAD) {100354A12B}>) [fast-method]
  13: ((:METHOD QUICKLISP-CLIENT:QUICKLOAD (T)) "cffi-grovel" :PROMPT NIL :SILENT T :VERBOSE NIL) [fast-method]
  14: (QL-DIST::CALL-WITH-CONSISTENT-DISTS #<CLOSURE (LAMBDA NIL :IN QUICKLISP-CLIENT:QUICKLOAD) {100353ACBB}>)
  15: ((FLET "H0" :IN QLOT/INSTALL::APPLY-QLFILE-TO-QLHOME) Component "cffi-grovel" not found, required by NIL)
  16: (SB-KERNEL::%SIGNAL Component "cffi-grovel" not found, required by NIL)
  17: (ERROR MISSING-DEPENDENCY :REQUIRED-BY NIL :REQUIRES "cffi-grovel")
  18: (ASDF/FIND-COMPONENT:RESOLVE-DEPENDENCY-NAME NIL "cffi-grovel" NIL)
  19: ((LAMBDA NIL :IN ASDF/PARSE-DEFSYSTEM:REGISTER-SYSTEM-DEFINITION))
  20: (SB-INT:SIMPLE-EVAL-IN-LEXENV (DEFSYSTEM "woo" :VERSION "0.11.5" :AUTHOR "Eitaro Fukamachi" :LICENSE "MIT" :DEFSYSTEM-DEPENDS-ON ("cffi-grovel") :DEPENDS-ON ("lev" "clack-socket" "swap-bytes" "cffi" "static-vectors" "bordeaux-threads" "fast-http" "quri" "fast-io" "smart-buffer" "trivial-utf-8" "vom" ...) ...) #<NULL-LEXENV>)
  21: (SB-EXT:EVAL-TLF (DEFSYSTEM "woo" :VERSION "0.11.5" :AUTHOR "Eitaro Fukamachi" :LICENSE "MIT" :DEFSYSTEM-DEPENDS-ON ("cffi-grovel") :DEPENDS-ON ("lev" "clack-socket" "swap-bytes" "cffi" "static-vectors" "bordeaux-threads" "fast-http" "quri" "fast-io" "smart-buffer" "trivial-utf-8" "vom" ...) ...) 0 NIL)
  22: ((LABELS SB-FASL::EVAL-FORM :IN SB-INT:LOAD-AS-SOURCE) (DEFSYSTEM "woo" :VERSION "0.11.5" :AUTHOR "Eitaro Fukamachi" :LICENSE "MIT" :DEFSYSTEM-DEPENDS-ON ("cffi-grovel") :DEPENDS-ON ("lev" "clack-socket" "swap-bytes" "cffi" "static-vectors" "bordeaux-threads" "fast-http" "quri" "fast-io" "smart-buffer" "trivial-utf-8" "vom" ...) ...) 0)
  23: ((LAMBDA (SB-KERNEL:FORM &KEY :CURRENT-INDEX &ALLOW-OTHER-KEYS) :IN SB-INT:LOAD-AS-SOURCE) (DEFSYSTEM "woo" :VERSION "0.11.5" :AUTHOR "Eitaro Fukamachi" :LICENSE "MIT" :DEFSYSTEM-DEPENDS-ON ("cffi-grovel") :DEPENDS-ON ("lev" "clack-socket" "swap-bytes" "cffi" "static-vectors" "bordeaux-threads" "fast-http" "quri" "fast-io" "smart-buffer" "trivial-utf-8" "vom" ...) ...) :CURRENT-INDEX 0)
  24: (SB-C::%DO-FORMS-FROM-INFO #<CLOSURE (LAMBDA (SB-KERNEL:FORM &KEY :CURRENT-INDEX &ALLOW-OTHER-KEYS) :IN SB-INT:LOAD-AS-SOURCE) {1003511A4B}> #<SB-C::SOURCE-INFO {1003511A03}> SB-C::INPUT-ERROR-IN-LOAD)
  25: (SB-INT:LOAD-AS-SOURCE #<SB-INT:FORM-TRACKING-STREAM for "file /Users/art/projects/lisp/test-woo/quicklisp/dists/woo/software/woo-52bf0ede5c2798cb170e0c298e834ee67d79c3d8/woo.asd" {100350EBC3}> :VERBOSE NIL :PRINT NIL :CONTEXT "loading")
  26: ((FLET SB-FASL::THUNK :IN LOAD))
  27: (SB-FASL::CALL-WITH-LOAD-BINDINGS #<CLOSURE (FLET SB-FASL::THUNK :IN LOAD) {21FD28B}> #<SB-INT:FORM-TRACKING-STREAM for "file /Users/art/projects/lisp/test-woo/quicklisp/dists/woo/software/woo-52bf0ede5c2798cb170e0c298e834ee67d79c3d8/woo.asd" {100350EBC3}>)
  28: ((FLET SB-FASL::LOAD-STREAM :IN LOAD) #<SB-INT:FORM-TRACKING-STREAM for "file /Users/art/projects/lisp/test-woo/quicklisp/dists/woo/software/woo-52bf0ede5c2798cb170e0c298e834ee67d79c3d8/woo.asd" {100350EBC3}> NIL)
  29: (LOAD #P"/Users/art/projects/lisp/test-woo/quicklisp/dists/woo/software/woo-52bf0ede5c2798cb170e0c298e834ee67d79c3d8/woo.asd" :VERBOSE NIL :PRINT NIL :IF-DOES-NOT-EXIST T :EXTERNAL-FORMAT :UTF-8)
  30: (CALL-WITH-MUFFLED-CONDITIONS #<CLOSURE (LAMBDA NIL :IN LOAD*) {100350B06B}> ("Overwriting already existing readtable ~S." #(#:FINALIZERS-OFF-WARNING :ASDF-FINALIZERS)))
  31: ((FLET "THUNK" :IN PERFORM))
  32: (SB-IMPL::%WITH-STANDARD-IO-SYNTAX #<CLOSURE (FLET "THUNK" :IN PERFORM) {21FD5DB}>)
  33: ((:METHOD PERFORM (DEFINE-OP SYSTEM)) #<DEFINE-OP > #<ASDF/SYSTEM:UNDEFINED-SYSTEM "woo">) [fast-method]
  34: ((SB-PCL::EMF PERFORM) #<unused argument> #<unused argument> #<DEFINE-OP > #<ASDF/SYSTEM:UNDEFINED-SYSTEM "woo">)
  35: ((LAMBDA NIL :IN ASDF/ACTION:CALL-WHILE-VISITING-ACTION))
  36: ((:METHOD PERFORM-WITH-RESTARTS :AROUND (T T)) #<DEFINE-OP > #<ASDF/SYSTEM:UNDEFINED-SYSTEM "woo">) [fast-method]
  37: ((:METHOD PERFORM-PLAN (T)) #<SEQUENTIAL-PLAN {10034EFD53}>) [fast-method]
  38: ((FLET SB-C::WITH-IT :IN SB-C::%WITH-COMPILATION-UNIT))
  39: ((:METHOD PERFORM-PLAN :AROUND (T)) #<SEQUENTIAL-PLAN {10034EFD53}>) [fast-method]
  40: ((:METHOD OPERATE (OPERATION COMPONENT)) #<DEFINE-OP > #<ASDF/SYSTEM:UNDEFINED-SYSTEM "woo"> :PLAN-CLASS NIL :PLAN-OPTIONS NIL) [fast-method]
  41: ((SB-PCL::EMF OPERATE) #<unused argument> #<unused argument> #<DEFINE-OP > #<ASDF/SYSTEM:UNDEFINED-SYSTEM "woo">)
  42: ((LAMBDA NIL :IN OPERATE))
  43: ((:METHOD OPERATE :AROUND (T T)) #<DEFINE-OP > #<ASDF/SYSTEM:UNDEFINED-SYSTEM "woo">) [fast-method]
  44: ((LAMBDA NIL :IN FIND-SYSTEM))
  45: (ASDF/SESSION:CONSULT-ASDF-CACHE (FIND-SYSTEM "woo") #<CLOSURE (LAMBDA NIL :IN FIND-SYSTEM) {10034BCA0B}>)
  46: ((:METHOD FIND-COMPONENT (STRING T)) "woo" (NIL) :REGISTERED NIL) [fast-method]
  47: ((:METHOD OPERATE (OPERATION T)) #<DEFINE-OP > ("woo")) [fast-method]
  48: ((SB-PCL::EMF OPERATE) #<unused argument> #<unused argument> #<DEFINE-OP > ("woo"))
  49: ((LAMBDA NIL :IN OPERATE))
  50: ((:METHOD OPERATE :AROUND (T T)) #<DEFINE-OP > ("woo")) [fast-method]
  51: (ASDF/SESSION:CALL-WITH-ASDF-SESSION #<CLOSURE (LAMBDA NIL :IN OPERATE) {10034BBB0B}> :OVERRIDE T :KEY NIL :OVERRIDE-CACHE T :OVERRIDE-FORCING NIL)
  52: ((LAMBDA NIL :IN OPERATE))
  53: ((:METHOD OPERATE :AROUND (T T)) #<DEFINE-OP > #<ASDF/SYSTEM:UNDEFINED-SYSTEM "woo">) [fast-method]
  54: ((LAMBDA NIL :IN LOAD-ASD))
  55: ((LAMBDA NIL :IN FIND-SYSTEM))
  56: (ASDF/SESSION:CONSULT-ASDF-CACHE (FIND-SYSTEM "woo") #<CLOSURE (LAMBDA NIL :IN FIND-SYSTEM) {1001B5E23B}>)
  57: (ASDF/SESSION:CALL-WITH-ASDF-SESSION #<CLOSURE (LAMBDA NIL :IN FIND-SYSTEM) {1001B5E23B}> :OVERRIDE NIL :KEY (FIND-SYSTEM "woo") :OVERRIDE-CACHE NIL :OVERRIDE-FORCING NIL)
  58: ((LABELS QLOT/INSTALL::SYSTEM-DEPENDENCIES :IN QLOT/INSTALL::APPLY-QLFILE-TO-QLHOME) "woo")
  59: ((LAMBDA NIL :IN QLOT/INSTALL::APPLY-QLFILE-TO-QLHOME))
  60: (QLOT/UTIL:CALL-IN-LOCAL-QUICKLISP #<CLOSURE (LAMBDA NIL :IN QLOT/INSTALL::APPLY-QLFILE-TO-QLHOME) {1001A27CBB}> #P"/Users/art/projects/lisp/test-woo/quicklisp/" :SYSTEMS (#P"/Users/art/projects/lisp/test-woo/test.asd") :CENTRAL-REGISTRY (#P"/Users/art/.roswell/local-projects/fukamachi/qlot/"))
  61: (QLOT/INSTALL::APPLY-QLFILE-TO-QLHOME #P"/Users/art/projects/lisp/test-woo/qlfile" #P"/Users/art/projects/lisp/test-woo/quicklisp/" :IGNORE-LOCK NIL :PROJECTS NIL)
  62: (QLOT/INSTALL:INSTALL-QLFILE #P"/Users/art/projects/lisp/test-woo/qlfile" :QUICKLISP-HOME #P"/Users/art/projects/lisp/test-woo/quicklisp/")
  63: (ROS/SCRIPT/QLOT::MAIN "install")
  64: (SB-INT:SIMPLE-EVAL-IN-LEXENV (APPLY (QUOTE ROS/SCRIPT/QLOT::MAIN) ROSWELL:*ARGV*) #<NULL-LEXENV>)
  65: (SB-INT:SIMPLE-EVAL-IN-LEXENV (ROSWELL:QUIT (APPLY (QUOTE ROS/SCRIPT/QLOT::MAIN) ROSWELL:*ARGV*)) #<NULL-LEXENV>)
  66: (SB-EXT:EVAL-TLF (ROSWELL:QUIT (APPLY (QUOTE ROS/SCRIPT/QLOT::MAIN) ROSWELL:*ARGV*)) NIL NIL)
  67: ((LABELS SB-FASL::EVAL-FORM :IN SB-INT:LOAD-AS-SOURCE) (ROSWELL:QUIT (APPLY (QUOTE ROS/SCRIPT/QLOT::MAIN) ROSWELL:*ARGV*)) NIL)
  68: (SB-INT:LOAD-AS-SOURCE #<CONCATENATED-STREAM :STREAMS NIL {1002E0E853}> :VERBOSE NIL :PRINT NIL :CONTEXT "loading")
  69: ((FLET SB-FASL::THUNK :IN LOAD))
  70: (SB-FASL::CALL-WITH-LOAD-BINDINGS #<CLOSURE (FLET SB-FASL::THUNK :IN LOAD) {21FF53B}> #<CONCATENATED-STREAM :STREAMS NIL {1002E0E853}>)
  71: ((FLET SB-FASL::LOAD-STREAM :IN LOAD) #<CONCATENATED-STREAM :STREAMS NIL {1002E0E853}> NIL)
  72: (LOAD #<CONCATENATED-STREAM :STREAMS NIL {1002E0E853}> :VERBOSE NIL :PRINT NIL :IF-DOES-NOT-EXIST T :EXTERNAL-FORMAT :DEFAULT)
  73: ((FLET ROSWELL::BODY :IN ROSWELL:SCRIPT) #<SB-SYS:FD-STREAM for "file /Users/art/.roswell/bin/qlot" {1002E0A043}>)
  74: (ROSWELL:SCRIPT "/Users/art/.roswell/bin/qlot" "install")
  75: (ROSWELL:RUN ((:EVAL "(ros:asdf)") (:EVAL "(ros:quicklisp)") (:SCRIPT "/Users/art/.roswell/bin/qlot" "install") (:QUIT NIL)))
  76: (SB-INT:SIMPLE-EVAL-IN-LEXENV (ROSWELL:RUN (QUOTE ((:EVAL "(ros:asdf)") (:EVAL "(ros:quicklisp)") (:SCRIPT "/Users/art/.roswell/bin/qlot" "install") (:QUIT NIL)))) #<NULL-LEXENV>)
  77: (EVAL (ROSWELL:RUN (QUOTE ((:EVAL "(ros:asdf)") (:EVAL "(ros:quicklisp)") (:SCRIPT "/Users/art/.roswell/bin/qlot" "install") (:QUIT NIL)))))
  78: (SB-IMPL::PROCESS-EVAL/LOAD-OPTIONS ((:EVAL . "(progn #-ros.init(cl:load \"/Users/art/usr/roswell/etc/roswell/init.lisp\"))") (:EVAL . "(ros:run '((:eval\"(ros:asdf)\")(:eval\"(ros:quicklisp)\")(:script \"/Users/art/.roswell/bin/qlot\"\"install\")(:quit ())))")))
  79: (SB-IMPL::TOPLEVEL-INIT)
  80: ((FLET SB-UNIX::BODY :IN SB-EXT:SAVE-LISP-AND-DIE))
  81: ((FLET "WITHOUT-INTERRUPTS-BODY-34" :IN SB-EXT:SAVE-LISP-AND-DIE))
  82: ((LABELS SB-IMPL::RESTART-LISP :IN SB-EXT:SAVE-LISP-AND-DIE))
  
  unhandled condition in --disable-debugger mode, quitting
  ;
  ; compilation unit aborted
  ;   caught 1 fatal ERROR condition
  ...

.. _52bf0ede5c2798cb170e0c298e834ee67d79c3d8: https://github.com/fukamachi/woo/commit/52bf0ede5c2798cb170e0c298e834ee67d79c3d8
