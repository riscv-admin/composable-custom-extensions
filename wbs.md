= Composable Extensions Developement Plan =

1. Specifications
1.1. ISA Specification Package
1.1.1. privileged opcode and state multiplexing [1w, 2w, 4w]
1.1.2. unprivileged opcode and state multiplexing [1w, 2w, 4w]
1.1.3. privileged state management [1w, 2w, 4w]
1.2. Discovery
1.2.1. Unified Discovery [2d, 1w, 2w]
1.2.2. Devicetree [3d, 1w, 2w]
1.2.3. ACPI [3d, 1w, 3w]
1.3. Linux syscall
1.4. User space ABI
1.4.1. Composable custom extension aware calling convention
1.4.2. Legacy interoperability calling convention
1.5. User space API
1.6. Logic interface

  A lengthy description of the item could be put here, and ignored
  when a CSV file is generated from this as the source.

2. ISA Specification support
2.1. SAIL model
2.2. ACT
3. Proof of concept
3.1. QEMU model
3.1.1. ISA support
3.1.1.1. privileged opcode and state multiplexing
3.1.1.2. unprivileged opcode and state multiplexing
3.1.1.3. privileged state management
3.1.2. Sample extension
3.2. Hardware implementation
3.2.1. ISA support
3.2.1.1. privileged opcode and state multiplexing
3.2.1.2. unprivileged opcode and state multiplexing
3.2.1.3. privileged state management
3.2.2. Logic interface
3.2.3. Sample extension
3.3. Linux support
3.3.1. Devicetree configuration
3.3.2. ACPI configuration
3.3.3. Context save and restore
3.3.4. Syscall
3.4. User space ABI
3.4.1. binutils support
3.4.2. gcc support
3.4.3. glibc suppor
3.5. User space API
3.6. Sample application
