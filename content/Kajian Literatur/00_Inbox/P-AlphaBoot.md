---
type: inbox
tags:
  - inbox
  - to-explore
tanggal:
---

# 📥 P-AlphaBoot

**Link:** https://www.frontiersin.org/journals/high-performance-computing/articles/10.3389/fhpcp.2025.1499519/full
**Sumber:**  Frontiers HPC 2025

## 📌 Abstrak
Scalability and flexibility of modern cloud application can be mainly attributed to virtual machines (VMs) and containers, where virtual machines are isolated operating systems that run on a hypervisor while containers are lightweight isolated processes that share the Host OS kernel. To achieve the scalability and flexibility required for modern cloud applications, each bare-metal server in the data center often houses multiple virtual machines, each of which runs multiple containers and multiple containerized applications that often share the same set of libraries and code, often referred to as images. However, while container frameworks are optimized for sharing images within a single VM, sharing images across multiple VMs, even if the VMs are within the same bare-metal server, is nearly non-existent due to the nature of VM isolation, leading to repetitive downloads, causing redundant added network traffic and latency. This work aims to resolve this problem by utilizing SmartNICs, which are specialized network hardware that provide hardware acceleration and offload capabilities for networking tasks, to optimize image retrieval and sharing between containers across multiple VMs on the same server. The method proposed in this work shows promise in cutting down container cold start time by up to 92%, reducing network traffic by 99.9%. Furthermore, the result is even more promising as the performance benefit is directly proportional to the number of VMs in a server that concurrently seek the same image, which guarantees increased efficiency as bare metal machine specifications improve.

## 🔑 Keywords dari Paper
container cold start, smartNIC, container image caching,  vm isolation, cloud resource optimization

## 💬 Kesan Awal
- 
- 

## 📝 Action
- [ ] Baca Bab 1
- [ ] Cari paper terkait dari references-nya