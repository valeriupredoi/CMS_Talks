## F-35 Lightning II Computing

### Hardware and Software

- Integrated Core Processor ([ICP](https://www.l3harris.com/all-capabilities/high-performance-integrated-core-processor-icp)):
  - pretty low compute power: 2900 DMIPS approx 2.3GHz (factor of 1.25), 1MB L2 Cache, 512MB DRAM, 256MB Flash
  - OS is key: **RTOS (Real Time Operating System, Green Hills Software Integrity DO-178B)**
- the ICP is designed to handle priority-ranked parallelism; from Lockheed-Martin:
  """
  Integrated Core Processor (ICP) is one of the world’s smallest deployed liquid cooled, airborne super computer.
  The ICP provides the primary embedded computing elements capable of managing all aircraft subsystems and sensors.
  The ICP has the processing power to handle all sensor processing and mission planning.
  It is enabled with a high-speed photonic data network for low latency subsystem communications.
  """
- the OS is completely different than normal/civilian OS's:
  """
  A real-time operating system (RTOS) is designed for real-time computing applications that process data and events
  with **strict time constraints**. RTOSs are event-driven and preemptive, meaning they can monitor the priority of
  competing tasks and make changes to them.
  """
- an [RTOS](https://en.wikipedia.org/wiki/Real-time_operating_system) minimizes:
  - iterrupt latency (time it takes from an Interrupt Request to the actual interrupt process start)
  - thread switching latency (moving one task from one thread to another)
  - **preemptive scheduling** (interrupting running task, when more imporant task needs resources)
- memory allocation in an RTOS:
  - critical! There can not be any memory leaks!
  - mostly all statical memory allocation (at compile time)
  - time-critical processes: there could be memory fragmentation, and a process can not run even if memory is available, but is fragmented
  - no SWAPping: disks have unpredictable I/O response times
