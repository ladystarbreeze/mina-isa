Introduction
============

MINA is an *open* instruction set architecture (ISA) designed to be extendable and easy to decode.

Current and future goals include:

* An ISA suitable for hardware implementation.
* 32-bit and 64-bit address space variants.

MINA ISA Overview
-----------------

The MINA ISA is defined as a base integer ISA with optional floating-point, SIMD and user-defined extensions.
Current base integer ISAs are *MINA32* and *MINA64*, which has not been defined yet.

Planned extensions include *FloatingMINA* (floating-point) and *VectorMINA* (single instruction, multiple data).

Events, Faults And Interrupts
-----------------------------

Unusual conditions occurring at run time are referred to as *events*.

*Faults* are events that occur synchronously to the current MINA thread; they transfer control to a *fault handler*.

*Interrupts* are similar to faults. However, interrupts occur *asynchronously* to the current MINA thread.

Data Types
-----------

The MINA ISA currently defines the following data types:

* *Byte* (8-bit)
* *Halfword* (16-bit)
* *Word* (32-bit)
* *Longword* (64-bit)

Future versions of the MINA ISA will define more data types.

Machine Control Register
------------------------

The *Machine Control Register* (MCR) is a longword register displaying information about the current state of a MINA implementation.
It is accessible through special move and load-store instructions.
