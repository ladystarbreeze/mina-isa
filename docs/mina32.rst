MINA32 Base Integer Instruction Set, Version 1
==============================================

The following sections describe version 1 of the MINA32 base integer ISA.

Overview
---------

MINA32 has a total of 27 registers:

* 24 32-bit general-purpose registers.
* 2 system registers.
* user-visible 32-bit program counter.

General-purpose registers ``r0-r7`` are shared across all modes, ``r8-r15`` are mode-specific.

.. note:: ``r15`` is used as a *stack pointer* (SP) for instructions that use the stack. At all other times you can treat ``r15`` as a general-purpose register.

.. note:: It is possible to access ``User`` mode registers ``r8_usr-r15_usr`` from ``Supervisor`` mode through the use of special move instructions.

The two system registers are MCR - the *Machine Control Register* - and FRET - the *Fault Return Address* register.
While limited MCR access is possible in ``User`` mode, FRET is only visible to ``Supervisor`` mode threads.

The user-visible *program counter* (PC) holds the address of the currently executing instruction.

Fault Entry And Exit
--------------------

MINA faults are handled as follows:

1. Depending on the fault cause, FRET is loaded with ``PC`` or ``PC + 4``.
2. MCR is left-shifted by 32. ``ID`` is pulled ``high``, ``MODE`` is loaded with ``10`` (``Supervisor``).
3. ``CAUSE`` is loaded with an appropriate fault code.
4. In case of a user-generated fault, ``COMMENT`` is loaded with a user-defined 8-bit value.
5. ``PC`` is set to 0.

To return from a fault, a fault handler must use the ``SWITCH`` instruction.
``SWITCH`` restores MCR by right-shifting it by 32 and resets ``PC`` to the value stored in FRET.
