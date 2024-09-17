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
spec-isa-unpriv unprivileged opcode and state multiplexing [3w, 4w, 6w]
spec-isa-state privileged state management [3w, 4w, 6w]
spec-disc Discovery
spec-disc-ud Unified Discovery [1w, 2w, 4w]
spec-disc-dt Devicetree [1w, 2w, 4w]
spec-disc-acpi ACPI [2w, 3w, 6w]
spec-sbi SBI extension []

  It is unclear if an SBI extension is necessary.  It will be specified as needed.

spec-linux Linux syscall
spec-abi User space ABI
spec-abi-cx Composable custom extension aware calling convention [4w, 6w, 8w]
spec-abi-legacy Legacy interoperability calling convention [4w, 6w, 8w]
spec-uapi User space API [1w, 4w, 6w]
spec-li Logic interface [8w, 12w, 16w]
rv ISA Specification support
rv-sail SAIL model
rv-sail-priv privileged opcode and state multiplexing dep=spec-isa-priv []
rv-sail-unpriv unprivileged opcode and state multiplexing dep=spec-isa-unpriv []
rv-sail-state privileged state management dep=spec-isa-state []
rv-act ACT
rv-act-priv privileged opcode and state multiplexing dep=spec-isa-priv [2w, 3w, 4w]
rv-act-unpriv unprivileged opcode and state multiplexing dep=spec-isa-unpriv [8d, 2w, 3w]
rv-act-state privileged state management dep=spec-isa-state [8d, 2w, 3w]
sw Software ecosystem support
sw-opensbi OpenSBI support dep=spec-sbi []
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
poc-int-qemu QEMU model integration testing dep=sw,poc-qemu,poc-sampleapp [3w, 4w, 8w]
poc-int-hw Hardware implementation integration testing dep=sw,poc-hw,poc-sampleapp [3w, 4w, 8w]
