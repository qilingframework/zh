### Features and Funtionalities

Qiling Framework is an advanced binary emulation framework, with the following features:
- Able to run on Windows/MacOS/Linux/FreeBSD without CPU architecture limitation
- Emulate Cross platform support: Windows, MacOS, Linux, BSD
- Emulate Cross architecture support: X86, X86_64, Arm, Arm64, Mips
- Supports Multiple file formats: PE, MachO, ELF, or direct binary input (shellcode)
- Emulates & sandbox machine code in an isolated environment
- Provides high level API to setup & configure the sandbox
- Provides granular instrumentation: allowing hooks at various levels (instruction/basic-block/memory-access/exception/syscall/IO/etc)
- Allows dynamic patch on-the-fly running code, including the loaded libraries
- A true framework written in Python, makes it easy to build customized security analysis tools for integration

Qiling Framework is the only solution combines disassember, binary instrumentation and binary emulation into single framework and provides cross-platform and multi arch support

- Qiling Framework is an advanced binary emulation framework which able to do the follow during execution
    - Redirect process execution flow on the fly
        - *Change execution flow when there is a check eg, cmp EAX,EBX always = true*
    - Hot-patching binary during execution
        - *Define a code address and patch it during execution, and keeping the original binary untouched* 
    - Code injection during execution
        - *Able to inject opcode or asm code into the binary during execution*
    - Partial binary execution, without running the entire file
        - *If the target section is only one part (example, function_targetedbug() ) of a huge binary*
        - *Each execution need to fulfill different user input before reaching function_targetedbug()*
        - *Qiling Framework is able to set and pre-fulfilled the state/ requirement, so that each new execute will go directly to function_targetbug()*
    - Patch a "unpacked" content of a packed binary file
        - *Able to patch a "packed" binary during execution, without unpacking*
