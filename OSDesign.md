# OS BOOK PART I
*NEED TO RE-READ THE KERNEL ABSTRACTION PART*

## RANDOM USEFUL NOTES
- many core ideas in modern os have become widely applied throughout computer science.
- Software engineers use many of the same technologies and design patterns as those used in operating systems to build other complex systems. 
- in modern world, nearly everything a user does is distributed, nearly every computer is multi-core, security threads abound

## OUTLINE
- **[abstract/general]overall goal** is to build a system that is
  - reliable
  - secure
  - portable, flexible
  - efficient
  - resilient
  
- **evaluating the system: DESIGN TRADOFFS**
  - reliability
  - availability
    - the percentage of time that the system is usable
    - two factors
      - MTTF: mean time to failure
      - MTTR: mean time to repair
  - security
    - cannot be compromised by malicious attacker
    - privacy
  - portability
    - easy to move to a new hardware platform?
  - performance
    - overhead
    - efficiency
    - throughput: rate with which system completes tasks
    - response time
    - fairness
    - performance predictability
    
- [more specific]design consideration (mainly arising out of the need for multi-tasking)
  - resource management/allocation
    - abstraction of physical hardware
    - ensure responsiveness
  - communication
    - common service
    - data sharing
  - isolation: security/failure (fault) isolation
  
- key questions to consider
  - how to enable multiple applications to communicate with each other?
  - how does the operating system enable applications to do multiple things at once?
  - how to facilidate sharing? how to synchronize shared data access ? 
  
## RECURING THEMES

- **ISOLATION**:
  - os:
    - failure isolation: os isolate applications from each other so that a bug in one application does not corrupt other applications running on the same machine
    - this requires restricting the behavior of applications to less than the full power of the underlying hardware
    - flip side is communication

- **ABSTRACTION/ILLUSIONIST/VIRTUALIZATION**: 
  - os:
    - provide abstration to simply application design
    - illusion of infinite resources: os provdes the **illusion** that each program has infinite memory and the computor's processors entirely to itself.
      - most physical resources can be virtualized
    - illusion of no failure: os masks failures such as wireless networks drop or corrupt packets to provide reliable services.
    - can even virtualize the entire computer - virtual machine
  - distributed system
    - many web services are geographically distributed. users do not notice the difference. if one server crashes or its network connection has problems, application can connect to a different site.

- **RESOURCE MANAGEMENT**
  - os:
    - few processors, finite amount of physical memory, network bandwidth, disk space
    - need to balance needs, separates conflicts, and facilitates sharing
    - one user should not be allowed to monopolize system resources or to access or corrupt another user's files without permission
  - cloud computing:
    - how are resources allocated between competing applications running in the cloud (shared computing and storage infrastructure in large-scale data centers)?
  - browsers:
    - how to ensure responsiveness with each tab running a script

- **FACILITATE SHARING**
  - os:
    - arise with the need to coordinate many simultaneous activities
    - can do so by providing common service; generic interface
  - cloud computing:
    - cloud services often distribute their work across different machines. What abstractions should cloud software provide to help services coordinate and share data between their various activities?
  
    
## notes  
- issue arising when you allows running of **third-party script**
  - become more powerful and widely used if you allow user to customize them, but doing so raise security issue  
  - "process": execution of application program with restricted rights -> all dangerous operations disabled.
    - privileged instructions
    - memory protection
    - timer interrupts
  
- privileged instruction: design pattern of kernel mode
  - kernel is necessarily trusted to do anything with the hardware; everything else is run in a restricted environment with less than complete access to the full power of the hardware.
  
  - speed/safety trade-off
    - key question is how to ensure safety while at the same time running application code at high speed.
    - how to protect?if
      - if we ignore performance/efficience we of course could have the kernel simulate the instructions and see if it is permitted. only execute it if it is, otherwise cause exception to handler.
      - a faster way is to implement this check directly on hardware (the checking bit is turned off in kernel mode)
      - another consideration is how to prevent user from directly chaging their privilege level


- how to protect unsafe memory access?
  - base/bound registers (using virtual addresses) - processor check if the memory is within boundary before each instruction, causing exception if violated.
    - efficiency issue arises: since applications touches only their own memory, data sharing become less efficient
    
# OS BOOK PART II

## NOTES
- the design of shared objects can have large impact on multiprocessor performance - lock protecting a frequently accessed shared object can become a bottleneck.

