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

  Means to control access to CXs by less priv code, sufficient for M,
  M/U, M/S/U, and HV systems.
  Means to trap, and to trap & emulate, a CX instruction/CSR.
  discuss: Means to control mapping of CX instances to harts.

spec-isa-unpriv unprivileged opcode and state multiplexing [3w, 4w, 6w]

  Means to select CX(s) to peform custom instructions/CSRs.
  Means to indicate multiplexing status/errors.
  discuss: Means to select CX instances(s) to perform opcodes and CSRs.

spec-isa-state privileged state management [3w, 4w, 6w]

  Means to uniformly initialize, save, and restore any CX save record.
  discuss: Means to support variable sized CX save records.

spec-disc Discovery
spec-disc-ud Unified Discovery [1w, 2w, 4w]
spec-disc-dt Devicetree [1w, 2w, 4w]
spec-disc-acpi ACPI [2w, 3w, 6w]
spec-sbi SBI extension [0d, 0d, 0d]

  It is unclear if an SBI extension is necessary.  It will be specified as needed.

spec-linux Linux syscall [2w, 3w, 5w]
spec-abi User space ABI
spec-abi-cx Composable custom extension aware calling convention [4w, 6w, 8w]
spec-abi-legacy Legacy interoperability calling convention [4w, 6w, 8w]
spec-uapi User space API [1w, 4w, 6w]

  Means to discover a CX by CX GUID.
  Means to request a CX by CX GUID.
  Means to select CX(s) to perform custom instructions/CSRs.
  Means to indicate actionable errors.
  discuss: Means to request another CX instance by CX GUID.
  discuss: Means to release a CX instance.

spec-li Logic interface [8w, 12w, 16w]
rv ISA Specification support
rv-test RISC-V Test Input []

  Test configuration input

rv-sail SAIL model
rv-sail-priv privileged opcode and state multiplexing dep=spec-isa-priv []
rv-sail-unpriv unprivileged opcode and state multiplexing dep=spec-isa-unpriv []
rv-sail-state privileged state management dep=spec-isa-state []
rv-act ACT
rv-act-priv privileged opcode and state multiplexing dep=spec-isa-priv [2w, 3w, 4w]
rv-act-unpriv unprivileged opcode and state multiplexing dep=spec-isa-unpriv [8d, 2w, 3w]
rv-act-state privileged state management dep=spec-isa-state [8d, 2w, 3w]
sw Software ecosystem support
sw-opensbi OpenSBI support dep=spec-sbi [0d, 0d, 0d]
sw-linux Linux support
sw-linux-dt Devicetree configuration dep=spec-disc-dt [1w, 8d, 2w]
sw-linux-acpi ACPI configuration dep=spec-disc-acpi [8d, 2w, 3w]
sw-linux-state Context save and restore dep=spec-isa-state [3w, 4w, 6w]
sw-linux-syscall Syscall dep=spec-linux [2w, 3w, 5w]
sw-abi User space ABI
sw-abi-binutils binutils support dep=spec-abi-cx,spec-abi-legacy [3w, 4w, 6w]
sw-abi-gcc gcc support dep=spec-abi-cx,spec-abi-legacy [2w, 3w, 5w]
sw-abi-glibc glibc support dep=spec-abi [1w, 2w, 4w]
sw-uapi User space API
sw-uapi-glibc glibc support dep=spec-linux,spec-uapi [1w, 2w, 4w]
poc Proof of concept
poc-qemu QEMU model
poc-qemu-isa ISA support
poc-qemu-isa-priv privileged opcode and state multiplexing dep=spec-isa-priv [2w, 4w, 6w]
poc-qemu-isa-unpriv unprivileged opcode and state multiplexing dep=spec-isa-unpriv [2w, 3w, 5w]
poc-qemu-isa-state privileged state management dep=spec-isa-state [2w, 3w, 5w]
poc-qemu-sampleext Sample extension [1w, 2w, 3w]
poc-hw Hardware implementation
poc-hw-isa ISA support
poc-hw-isa-priv privileged opcode and state multiplexing dep=spec-isa-priv [2w, 4w, 6w]
poc-hw-isa-unpriv unprivileged opcode and state multiplexing dep=spec-isa-unpriv [2w, 3w, 5w]
poc-hw-isa-state privileged state management dep=spec-isa-state [2w, 3w, 5w]
poc-hw-li Logic interface dep=spec-li [2w, 4w, 6w]
poc-hw-sampleext Sample extension dep=spec-li [4w, 6w, 8w]
poc-sampleapp Sample application dep=spec-uapi [2w, 3w, 4w]
poc-int Integration testing
poc-int-qemu QEMU model integration testing dep=sw,poc-qemu,poc-sampleapp [3w, 4w, 12w]
poc-int-hw Hardware implementation integration testing dep=sw,poc-hw,poc-sampleapp [3w, 4w, 12w]

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
