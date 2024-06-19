# Composable Extensions Requirements

This document captures the requirements for the Composable Extensions
task group work products, which include ISA and non-ISA specifications
and other supporting work.  See the charter for details.

The document is currently in draft status for discussion.
Requirements are classified in into one of three categories: (1)
requirements which are proposed for inclusion, (2) requirements which
require further discussion whether they warrant inclusion or not,
notated *[discuss]*, and (3) requirements which are proposed for
exclusion from the present task group work and potentially considered
for future work, notated ~~[exclude]~~.  It is expected that all
requirements of the second type, *[discuss]*, will be changed to one
of the other types before work commences.

## Requirements

* A Composable Extension (CX) is an ISA contract that specifies the
  behavior of a composable custom extension.  This behavior is defined
  in terms of a set of custom instructions and custom CSRs,
  collectively termed custom operations, with a precise fixed model of
  state and behavior, that satisfies the criteria for
  composability.

* A CX Unit (CXU) is a reusable hardware module that implements one or
  more CXs.

* CX software is software that issues custom operations of a CX.

* Multiple categories of composable custom extensions will be
  specified, including the following:

  * Software Composable Extensions are the set of custom extensions
    whose state is isolated from the rest of the system and whose
    functional behavior does not change in the presence/absence of
    other such software composable extensions.

  * Hardware Composable Extensions are the set of Software Composable
    Extensions which are additionally implemented by a CXU with the
    specified logic interface.

* The specifications support interoperability without preference to
  any particular implementation tool.

* There may be multiple independent implementations of a CX.

* There may be multiple CX software collections that use a CX.

* Support switching a range of opcodes and CSRs between multiple
  composable extensions that allows the resources of each extension to
  be available when enabled, independent of what other composable
  extensions might exist in the system.

* *[discuss] Allow splitting the opcode space into more manageable
  portions.*

* *[discuss] Support, or allow logical enhancement for, multiple opcode
  spaces.*

* Support compatibility with existing use of custom opcode
  space.

* Use custom opcode space and custom CSR addresses for composable
  extensions.

* Use standard opcode space and standard CSR addresses for behavior
  that controls composable extensions.

* Do not impose unnecessary constraints on CX opcode
  interpretation.

* A system may have multiple harts.

* A system may have at least 255 CXs.

* Support heterogeneous composable extensions; that is, multiple harts
  in a system which each have different composable
  extensions.

* *[discuss] Support hotplugging composable extensions; that is,
  support the dynamic discovery of CXs that may become available or
  unavailable at runtime.*

* Support exactly one state context per hart efficiently.

* *[discuss] Support more than one state context per hart.*

* *[discuss] There may be zero or more CX state contexts in a system.*

* *[discuss] The number of state contexts of a CX must be equal to the
  number of harts in the system. If granted access, a hart may select
  and access that hart's CX state context.*

* *[discuss] The number of state contexts of a CX may be less than,
  equal to, or greater than the number of harts in the system. If
  granted access, a hart may select and access any CX state
  context. Multiple harts may select and access the same CX state
  context.*

* At any moment a thread may have a number of selected custom
  extensions (one of which may be the CPU's legacy custom
  extension(s)) and the same number of selected state contexts, one
  for each of the selected custom extensions, where the number selected
  is:

  * One,

  * *[discuss] One or more.*

* Support state contexts in size from zero to at least 512
  kiB.

* ~~[exclude] Support changing the state context size dynamically at
  runtime.~~

* ~~[exclude] Support changing the number of state contexts
  dynamically at runtime.~~

* One software thread may use zero or more CXs over time.

* Multiple harts may concurrently issue custom instructions to
  disjoint state contexts of the same or different CXs.

* ISA features must be cleanly separated into the appropriate
  privilege mode (M/S/U).

* Support RV32 and RV64, without preference for either.

* Support a wide range of implementation styles and performance
  targets, without preference to any.

* Support emulating a composable extension with trap and
  emulate.

* Support uniquely identifying each composable extension without any
  requirement for centralized coordination.

* Discovery of system configuration and parameters must be done using
  existing RISC-V mechanisms (Unified Discovery, Device Tree,
  ACPI).

* Provide an API to allow CX software to discover a CX using a unique
  CX identifier.

* ~~[exclude] Provide an API to allow CX software to discover a CX
  using a unique CX identifier and additional parameters.~~

* Support a logic interface that allows custom operations to source
  one or two operands from and/or write a single result to the integer
  register file.

* ~~[exclude] Support custom operations that access more than two read
  operands.~~

* ~~[exclude] Support a logic interface that allows custom operations
  to source operands from and/or write results to pairs of registers
  in the integer register file.~~

* ~~[exclude] Supports custom operations that access register pairs.~~

* *[discuss] Support a logic interface that allows custom operations
  to source operands from and/or write results to the floating point
  register file.*

* ~~[exclude] Support a logic interface that allows custom operations
  to source operands from and/or write results to the vector register
  file.~~

* *[discuss] Supports a logic interface that allows zero or more
  read/write accesses to system shared memory as if these accesses are
  performed by the CPU, in response to the custom operation, and
  ordered that way. In particular, these accesses enjoy the same
  memory protection, consistency, and ordering as if performed by the
  CPU.*

* *[discuss] Supports a logic interface that provides access to the
  current privilege mode of the hart executing a custom operation.*

* Supports a logic interface which allows access to custom CSRs ("CX
  CSRs") with access control for privilege mode and read-only or
  read-write checked by the hart.

* Support systems with varying privilege modes:

  * Support machine mode only systems.

  * Support machine and user mode only systems.

  * Support supervisor mode operating systems.

  * Support the hypervisor extension.

* M, S, or U level software can use composable extensions.

* ~~[exclude] A system must support use of composable extensions from
  any privilege level.~~

* Provide a mechanism for the hart to select the current CX and state
  context for custom operations that follow, including the ability to
  specify legacy custom extension behavior.

* Provide a mechanism to collect accumulated errors that may arise
  from use of the mechanism the hart uses to select the current
  CX.

* Supervisor CX software may be aware of CX implementation properties
  such as context save size or support for flash init, but should not
  rely on it for proper functional behavior.

* A hart's CX selection(s) identify the CX to perform custom
  operations.

* ~~[exclude] A hart's CX selection(s) identify the CX implementation
  to perform custom operations.~~

* Each hart has a set of CX selector(s) used across all privilege
  levels.

* ~~[exclude] Each hart has a set of CX selector(s) per privilege
  level.~~

* More-privileged software can securely grant/deny access by
  less-privileged software to a CX and its state context.

* Support reading and writing all architecturally visible composable
  extension state in a general way that is not specific to individual
  extensions.

* Privileged software can manage, initialize, save, and restore a
  state context of any arbitrary CX, without utilizing CX specific
  software.

* Every CX incorporates CX state context CSRs that enable any OS
  to manage its current state context. ("All CXs are stateful, but
  some CXs have zero-sized state.")

* ~~[exclude] Every stateful CX incorporates CX state context CSRs
  that enable any OS to manage its current state context. ("And some
  CXs are stateless.")~~

* CX state context initialization supports iterative initialization of
  XLEN sized words.

* CX state context initialization may support flash (single action)
  self-initialization.

* CX ISA extensions comport with current and foreseeable standard
  extensions, including Smstateen, Xstatus.XS CX.

* In supervisor mode operating systems, support allowing the operating
  system to mediate access to composable extension resources.

* ~~[exclude] Support performance monitors on composable extension
  specific behavior.~~

* ~~[exclude] Support debugging and tracing composable extension
  behavior.~~

* ~~[exclude] Support configuration information that provides
  performance and topology information to allow, for example, a
  supervisor mode operating system to optimize scheduling based on
  system specific characteristics.~~

* Supports an API with uniform CX access control.

* Supports an API with uniform CX error handling.

* Support efficient calling conventions for managing user visible CX
  state and control.

* Support function calls between software aware of CX state and
  control and software that is not (between CX ABI and non-CX
  ABI).

* Provide an ABI which supports disciplined correct nesting of various
  CX software libraries that discover, select, and issue custom
  operations of various CXs

* Provide an ABI which supports interoperability of CX library
  software with legacy code and compilers that target legacy custom
  instructions.

* A system may have at least 255 CXUs.

* A CXU may implement one or more CXs.

* A system may have more than one CXU that implements a CX.

* Support a logic interface that permits interconnection between a
  composable extension implementation and a RISC-V hart
  implementation.

* Support a logic interface that is flexible for FPGA and ASIC
  implementations, without preference for either.

* The logic interface shall support simple processors and complex
  processors.

* Support a CX system implemented without the specified logic
  interface

* The logic interface shall support CXU implementations with varying
  timing behavior between the request and the response, including;

  * Combinational,

  * Pipelined fixed latency, and

  * Pipelined variable latency flow-controlled channels.

* *[discuss] The logic interface shall support flow controlled
  channels to be uniformly transported over AXI4 streams.*

* The logic interface shall support build-time configurable fixed
  latencies.

* The logic interface shall support build-time configurable maximum
  latency.

* The logic interface shall support a reset.

* The logic interface shall support a power save mechanism.

* The logic interface shall support optional request and response
  transaction IDs.

* *[discuss] The logic interface shall support optional out-of-order
  responses.*

* *[discuss] The logic interface shall support speculative issue and
  cancellation of custom instructions.*

* Supports CXUs that, in response to CXU requests, issue new (possibly
  stateful) CXU requests.

* For systems that are composed of multiple CXUs, potentially
  interconnected to each other as well as RISC-V harts, the behavior
  visible from the RISC-V hart(s) must meet the requirements
  specified.

* The logic interface supports automatic composition of one or more
  harts to one or more CXUs.

* The logic interface shall be defined in terms of logic signals,
  ports, configuration parameters.

* The logic interface shall provide an abstraction that does not
  require either the hart implementation or the CXU implementation to
  be modified to accommodate the other.

* CX interfaces incorporate forward compatibility mechanisms so that
  old CX libraries and old CXUs may be used in a system with revised
  CX interfaces.

* The CX system supports versioning of CXs, including negotiation of
  mutually supported CXs between old and new CX libraries and old and
  new CXUs.
