# **Automotive Grade Linux – Chiplet Abstraction Layer**  
*A conceptual reference implementation for enabling chiplet‑based compute architectures in Software‑Defined Vehicles (SDVs).*

---

## **📌 Overview**  
Automotive OEMs are transitioning from monolithic SoCs to **chiplet‑based compute architectures** to meet the performance, modularity, and scalability demands of SDVs. Initiatives like **CHASSIS** and **imec’s Automotive Chiplet Program** highlight the industry’s shift toward multi‑vendor chiplet ecosystems and standardized interfaces for in‑vehicle compute platforms.  
  [automotive-chiplets.eu](https://www.automotive-chiplets.eu/)  [imec-int.com](https://www.imec-int.com/en/expertise/cmos-advanced-and-beyond/compute/automotive-chiplet-program)

**Automotive Grade Linux (AGL)**, an open-source platform for connected vehicles, is simultaneously evolving toward **hardware‑agnostic SDV architectures**, as seen in the AGL SoDeV reference platform.  
  [Automotive Grade Linux](https://www.automotivelinux.org/)

This project proposes a **Chiplet Abstraction Layer (CAL)** for AGL to unify chiplet discovery, capability exposure, lifecycle management, and interoperability across heterogeneous compute modules.

---

## **🎯 Goals**  
The AGL Chiplet Abstraction Layer aims to:

- **Abstract heterogeneous chiplets** (CPU, GPU, NPU, ISP, safety islands, accelerators) behind a unified API.  
- **Enable multi‑vendor chiplet interoperability**, aligned with industry efforts toward open chiplet ecosystems.  
    [automotive-chiplets.eu](https://www.automotive-chiplets.eu/)
- **Support scalable SDV compute platforms**, consistent with AGL’s SoDeV initiative.  
    [Automotive Grade Linux](https://www.automotivelinux.org/)
- **Provide early hardware/software co‑validation**, similar to CHASSIS virtual/hybrid reference platforms.  
    [automotive-chiplets.eu](https://www.automotive-chiplets.eu/)
- **Expose chiplet capabilities to Linux user space** via sysfs, udev, or gRPC‑based services.
- **Support safety‑critical and real‑time workloads** through deterministic scheduling and isolation.

---

## **📐 Architecture**

### **1. Chiplet Discovery Layer**  
Responsible for enumerating chiplets via:

- Firmware descriptors (ACPI‑like tables, device tree extensions)  
- Vendor‑neutral metadata formats (aligned with CHASSIS and imec reference architectures)  
    [automotive-chiplets.eu](https://www.automotive-chiplets.eu/)  [imec-int.com](https://www.imec-int.com/en/expertise/cmos-advanced-and-beyond/compute/automotive-chiplet-program)

### **2. Capability Abstraction Layer**  
Normalizes chiplet capabilities such as:

- Compute (TOPS, cores, ISA)  
- Memory bandwidth  
- Interconnect topology  
- Safety level (ASIL rating)  
- Power/thermal envelopes  

### **3. Interconnect Virtualization**  
Abstracts physical interconnects:

- UCIe‑like die‑to‑die links  
- Proprietary automotive interconnects  
- High‑bandwidth memory channels  

### **4. Runtime Management**  
Handles:

- Chiplet power states  
- Fault isolation  
- Thermal throttling  
- OTA firmware updates (aligned with AGL’s OTA stack)

### **5. User‑Space Interfaces**  
Exposed via:

- `/sys/chiplets/*`  
- `/dev/chiplet-*`  
- gRPC/DBus services for higher‑level orchestration  
- Integration with AGL middleware and containers

---

## **🧪 Reference Implementations & Upstream Alignment**

### **AGL SoDeV**  
AGL’s SDV reference platform decouples software from hardware and is a natural integration point for chiplet abstraction.  
  [Automotive Grade Linux](https://www.automotivelinux.org/)

### **CHASSIS Automotive Chiplets**  
Provides multi‑vendor chiplet integration frameworks, base dies, and early co‑validation platforms.  
  [automotive-chiplets.eu](https://www.automotive-chiplets.eu/)

### **imec Automotive Chiplet Program**  
Defines reference chiplet architectures and interconnect quality‑and‑reliability models.  
  [imec-int.com](https://www.imec-int.com/en/expertise/cmos-advanced-and-beyond/compute/automotive-chiplet-program)

---

## **📦 Repository Structure (Proposed)**

```
agl-chiplet-abstraction/
│
├── docs/
│   ├── architecture.md
│   ├── chiplet-metadata-spec.md
│   └── integration-with-agl-sodev.md
│
├── kernel/
│   ├── drivers/chiplet/
│   ├── chiplet-discovery.c
│   ├── chiplet-capabilities.c
│   └── Kconfig
│
├── user-space/
│   ├── libchiplet/
│   ├── chipletctl/
│   └── grpc-services/
│
├── tests/
│   ├── unit/
│   └── integration/
│
└── examples/
    ├── chiplet-info
    └── performance-probe
```

---

## **🚀 Roadmap**

1. Define chiplet metadata schema (aligned with CHASSIS + imec).  
2. Implement kernel‑level discovery driver.  
3. Add capability abstraction and sysfs interface.  
4. Integrate with AGL SoDeV runtime.  
5. Provide reference chiplet simulators for early development.  
6. Validate on hybrid/virtual platforms.  
7. Upstream proposal to AGL expert groups.

---

## **📄 License**  
Apache‑2.0 (aligned with AGL and CHASSIS licensing models).  
 

