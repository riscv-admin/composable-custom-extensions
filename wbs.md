= Composable Custom Extensions Developement Plan =

  This file captures the work items for the Composable Custom
  Extensions Task Group in a work breakdown structure (WBS) [1].

  [1] https://en.wikipedia.org/wiki/Work_breakdown_structure

  Tasks must follow the principles of a WBS:

  - Any, and varying, levels of hierarchy are allowed.  Only leaf
    elements in the hierarchy represent work to be done.  Thus, only
    leaf elements have time estimates, dependencies, owners, etc.,
    assigned to them.

  - Every task is only captured in a single place; nothing is duplicated.

  - Non-leaf elements can be considered as the sum of all leaf items
    with respect to time estimates, dependencies, etc.

  - Time estimates are three point estimates (optimistic, expected,
    and pessimistic).

  This file is intended to be machine readable with ad-hoc tooling.

  Time estimates are work time; scheduling will be done separately.
  For estimating purposes, one day (1d) is eight hours (8h), one week
  (1w) is five days, and one month (1m) is four weeks.

spec Specifications
spec-isa ISA Specification Package
spec-isa-priv privileged opcode and state multiplexing dep=none owner=unknown@example.com [5w, 6w, 8w] progress=0%

  Specify an ISA extension for more privileged code to grant access to
  a CX to less privileged code, and to enable privileged code to trap
  and emulate CX instructions/CSRs.

  If necessary the ISA extension also supports access control to multiple
  CX instances of the same CX.

spec-isa-unpriv unprivileged opcode and state multiplexing [3w, 4w, 6w]

  Specify an ISA extension to select the current CX to perform custom
  instructions/CSRs, and to indicate multiplexing status/errors.

  If necessary the ISA extension supports selection of one of possibly
  multiple CX instances of the same CX.

  If necessary the ISA extension also supports selection of a current
  CX (or CX instance) for each of multiple subranges of custom
  instructions/CSRs.

spec-isa-state privileged state management [3w, 4w, 6w]

  Specify an ISA extension to uniformly initialize, save, and restore
  any CX state context.

spec-criteria Composability criteria

  Specify criteria for a composable custom extension.

spec-criteria-ext Basic composability criteria [1w, 1w, 2w]

  Specify basic criteria for a custom extension to be deemed a
  composable custom extension, excluding any behavior for accessing
  memory.

spec-criteria-mem Composable memory access behavior [1w, 1w, 2w]

  Specify a portable memory model for composable custom extensions.

spec-disc Discovery
spec-disc-ud Unified Discovery [1w, 2w, 4w]

  Add schema for identifying composable custom extension on harts and
  any necessary parameters, such as state size.

  If necessary add schema for identifying multiple CX instances and
  heterogeneous per-hart accessibility of these CX instances.

spec-disc-dt Devicetree [1w, 2w, 4w]

  Add schema for attributes that identify composable custom extension
  on harts and any necessary parameters, such as state size.

  If necessary add schema for identifying multiple CX instances and
  heterogeneous per-hart accessibility of these CX instances.

spec-disc-acpi ACPI [2w, 3w, 6w]

  Add definition for ACPI table for identifying composable custom
  extension on harts and any necessary parameters, such as state size.

  If necessary add support for identifying multiple CX instances and
  heterogeneous per-hart accessibility of these CX instances.

spec-sbi SBI extension [0d, 0d, 0d]

  It is unclear if an SBI extension is necessary.  It will be specified as needed.

spec-linux Linux syscall [2w, 3w, 5w]

  Add interfaces to hwprobe, prctl, and sysfs to provide discovery of
  composable custom extensions and related parameters and control of
  extension enablement.

  If necessary add additional interfaces or syscalls to support a multiple
  CX instance model.

spec-abi User space ABI
spec-abi-cx Composable custom extension aware calling convention [4w, 6w, 8w]

  Define a calling convention for handling composable custom extension
  framework state on calls between object files that both support this
  convention.

  Define criteria for use by composable custom extension authors in
  defining extension specific calling conventions that support similar
  behavior.

spec-abi-legacy Legacy interoperability calling convention [4w, 6w, 8w]

  Define calling conventions for handling composable custom extension
  framework state on calls between object files that support
  composable custom extensions (as defined in spec-abi-cx) and those
  that do not.

  Define criteria for use by composable custom extension authors in
  defining extension specific calling conventions that support similar
  behavior.

spec-uapi User space API [1w, 4w, 6w]

  Specify an API that provides a uniform CX programming model
  including CX naming, discovery, versioning, CX selection, and error
  handling and correct composition of CX libraries.

  If necessary the API will support both the singleton CX model and the
  multiple CX instance model.

spec-li Logic interface [8w, 12w, 16w]

  Specify a logic signal level interface for composable custom
  extensions.

rv ISA Specification support
rv-test RISC-V Test Input []

  Test configuration input

rv-sail SAIL model
rv-sail-priv privileged opcode and state multiplexing dep=spec-isa-priv []

  Implement SAIL support for the privileged opcode and state
  multiplexing features of the ISA.

rv-sail-unpriv unprivileged opcode and state multiplexing dep=spec-isa-unpriv []

  Implement SAIL support for the unprivileged opcode and state
  multiplexing features of the ISA.

rv-sail-state privileged state management dep=spec-isa-state []

  Implement SAIL support for the privileged state management features
  of the ISA.

rv-act Architecture Compliance Tests (ACT)

  All compliance tests should test basic functionality and need not be
  complete verification tests that cover all corner cases.

rv-act-priv privileged opcode and state multiplexing dep=spec-isa-priv [2w, 3w, 4w]

  Implement compliance tests for the privileged opcode and state
  multiplexing features of the ISA.

rv-act-unpriv unprivileged opcode and state multiplexing dep=spec-isa-unpriv [8d, 2w, 3w]

  Implement compliance tests for the unprivileged opcode and state
  multiplexing features of the ISA.

rv-act-state privileged state management dep=spec-isa-state [8d, 2w, 3w]

  Implement compliance tests for the privileged state management features
  of the ISA.

sw Software ecosystem support
sw-opensbi OpenSBI support dep=spec-sbi [0d, 0d, 0d]

  Implement the specified SBI extension in OpenSBI.

sw-linux Linux support
sw-linux-dt Devicetree configuration dep=spec-disc-dt [1w, 8d, 2w]

  Add support to Linux for obtaining the composable custom extension
  configuration from the specified devicetree attributes.

sw-linux-acpi ACPI configuration dep=spec-disc-acpi [8d, 2w, 3w]

  Add support to Linux for obtaining the composable custom extension
  configuration from the specified ACPI table.

sw-linux-state Context save and restore dep=spec-isa-state [3w, 4w, 6w]

  Add support to Linux for managing composable custom extension
  framework state and extension state, including saving and restoring
  state on context switch, allocating memory for state efficiently,
  and reporting errors.

  If necessary add additional support for a multiple CX instance model.

sw-linux-uabi Linux User Space ABI dep=spec-linux [2w, 3w, 5w]

  Add support to Linux for specified the user space ABI, including
  hwprobe, prctl, and sysfs support.  Add documentation and self tests
  as appropriate.

  If necessary add additional support for a multiple CX instance model.

sw-abi User space ABI
sw-abi-binutils binutils support dep=spec-abi-cx,spec-abi-legacy [3w, 4w, 6w]

  Add support for managing the specified ABI variants to RISC-V ELF
  files, including support in ld, readelf, and objdump.

  Add support to assembler and disassembler for new opcodes, as
  needed.

sw-abi-gcc gcc support dep=spec-abi-cx,spec-abi-legacy [2w, 3w, 5w]

  Add support for saving and restoring composable custom extension
  framework state.  Add support for managing the appropriate ABI
  variants in RISC-V ELF files.

  Add instrinsics for new opcodes, as needed.

sw-abi-glibc glibc support dep=spec-abi [1w, 2w, 4w]

  Handle user visible framework hart state as necessary, including in
  setcontext/makecontext and setjmp/longjmp.

  If necessary add additional support for a multiple CX instance model.

sw-uapi User space API
sw-uapi-glibc glibc support dep=spec-linux,spec-uapi [1w, 2w, 4w]

  Add wrappers in glibc for the specified Linux hwprobe and/or prctl
  functions.

poc Proof of concept
poc-qemu QEMU model
poc-qemu-isa ISA support
poc-qemu-isa-priv privileged opcode and state multiplexing dep=spec-isa-priv [2w, 4w, 6w]

  Implement a model of the privileged opcode and state multiplexing features of
  the ISA.

poc-qemu-isa-unpriv unprivileged opcode and state multiplexing dep=spec-isa-unpriv [2w, 3w, 5w]

  Implement a model of the unprivileged opcode and state multiplexing
  features of the ISA.

poc-qemu-isa-state privileged state management dep=spec-isa-state [2w, 3w, 5w]

  Implement a model of the privileged state management features of the
  ISA.

poc-qemu-sampleext Sample extension [1w, 2w, 3w]

  Implement a model of a sample composable custom extension that
  provides all necessary interface with framework and a simple noop
  function.

poc-hw Hardware implementation
poc-hw-isa ISA support
poc-hw-isa-priv privileged opcode and state multiplexing dep=spec-isa-priv [2w, 4w, 6w]

  Implement the privileged opcode and state multiplexing features of
  the ISA in hardware.

poc-hw-isa-unpriv unprivileged opcode and state multiplexing dep=spec-isa-unpriv [2w, 3w, 5w]

  Implement the unprivileged opcode and state multiplexing
  features of the ISA in hardware.

poc-hw-isa-state privileged state management dep=spec-isa-state [2w, 3w, 5w]

  Implement the privileged state management features of the ISA in
  hardware.

poc-hw-li Logic interface dep=spec-li [2w, 4w, 6w]

  Implement the logic level interface to a processor in hardware.

poc-hw-sampleext Sample extension dep=spec-li [4w, 6w, 8w]

  Implement a sample composable custom extension that provides all
  necessary interface with framework and a simple noop function.

poc-sampleapp Sample application dep=spec-uapi [2w, 3w, 4w]

  Implement the software for a sample application that exercises the
  basic framework functions and a noop extension function.

poc-int Integration testing
poc-int-qemu QEMU model integration testing dep=sw,poc-qemu,poc-sampleapp [3w, 4w, 12w]

  Combine completed system software, QEMU model, and application
  software; test and debug.

poc-int-hw Hardware implementation integration testing dep=sw,poc-hw,poc-sampleapp [3w, 4w, 12w]

  Combine completed system software, hardware implementation, and
  application software; test and debug.

freeze Ratification Plan Freeze Milestone

  The sub tasks here represent the tasks on the ratification plan
  checklist for the freeze milestone.  These are dependency tasks with
  no real work and reflect dependencies on other tasks.

freeze-isa ISA Freeze Checklist
freeze-isa-opcode Opcode Support dep=sw-abi-gcc [0d, 0d, 0d]

  Enough opcode encoding to support GCC.

freeze-isa-sim Simulator Support dep=poc-qemu [0d, 0d, 0d]

  Enough simulator support so that basic RISC-V tests can be run.

freeze-isa-psabi psABI dep=spec-abi [0d, 0d, 0d]

  ABI extensions.

freeze-isa-gcc gcc dep=sw-abi [0d, 0d, 0d]

  Support on GCC (optimizations not required).

freeze-isa-llvm llvm [0d, 0d, 0d]

  Support on LLVM (optimizations not required).  [not planned]

freeze-isa-rvtestinput RISC-V Test Input dep=rv-test [0d, 0d, 0d]

  Test configuration input (YAML schema & values, Test Coverage YAML rules).

freeze-isa-rvtest RISC-V Tests dep=rv-act [0d, 0d, 0d]

  Basic tests that do not cover corner cases.

freeze-isa-rvsail RISC-V SAIL dep=rv-sail [0d, 0d, 0d]

  SAIL support.

freeze-nonisa Non-ISA Freeze Checklist
freeze-nonisa-opensbi OpenSBI dep=sw-opensbi [0d, 0d, 0d]

  Discovery and configuration.  [as needed]

freeze-nonisa-linux Linux dep=sw-linux [0d, 0d, 0d]

  Discovery and configuration, context management, access control.

freeze-nonisa-glibc glibc dep=sw-uapi [0d, 0d, 0d]

  Discovery and configuration, user context management.
