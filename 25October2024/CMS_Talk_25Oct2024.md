![f35LighningII](https://github.com/valeriupredoi/CMS_Talks/blob/479d13452afb0020d3e5253acffbc57d57400547/images/f35.jpg)

## F-35 Lightning II Computing

### Flying and Combat system

Beyond HOTAS (Hands On Throttle And on Stick: put all necessary buttons on throttle lever and pilot side stick):

- massive amount of sensors, each feeding data to central computers
![sensors](https://github.com/valeriupredoi/CMS_Talks/blob/ccc589499da3f4648a0c5e406cf9c8ec9df78e7d/images/sensorrsF35.jpeg)
- computer needs to take decisions for: flying (fly-by-wire, fuel consumption etc), navigation, combat
- decisions are fed to the pilot in "as **real time** as possible"
- no time to fiddle with buttons, levers, and other mechanical devices, like in the past
- instead of HOTAS: massive LCD screens with tons of data, including a full 360deg view **through** the airframe
![360view](https://github.com/valeriupredoi/CMS_Talks/blob/ccc589499da3f4648a0c5e406cf9c8ec9df78e7d/images/throughF35.jpg)

### Hardware and Software

- Integrated Core Processor ([F35 ICP](https://www.l3harris.com/all-capabilities/high-performance-integrated-core-processor-icp)) and [civilian Q-SYS](https://www.audiologic.co.uk/partners-area/products/q-sys-integrated-core-processor):
  - pretty low compute power: 2900 DMIPS approx 2.3GHz (factor of 1.25), 1MB L2 Cache, 512MB DRAM, 256MB Flash
  - the main job is to manage integrated CPUs or full blown compute nodes, with **real-time** optimization, and seamless integration with videodisplaying
  - OS is key: **RTOS or Real Time Operating System** (F-35 uses Green Hills Software Integrity DO-178B, absolutely not open source)
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
