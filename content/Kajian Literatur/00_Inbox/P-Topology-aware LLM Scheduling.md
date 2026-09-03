---
type: inbox
tags:
  - inbox
  - to-explore
tanggal:
---
# 📥 P-Topology-aware LLM Scheduling

**Link:**  https://arxiv.org/abs/2411.11560
**Sumber:** arXiv 2024

## 📌 Abstrak
Hosting diverse large language model workloads in a unified resource pool through co-location is cost-effective. For example, long-running chat services generally follow diurnal traffic patterns, which inspire co-location of batch jobs to fulfill resource valleys between successive peaks, and thus to saturate resource allocation in cluster-wide scope. These heterogeneous workloads often have different business priorities, and therefore preemption can be leveraged for resource elasticity. However, workloads often have distinct topology preferences as well. The resources released by lower-priority instances may fail to meet the requirements of high-priority online services which are usually latency-sensitive. The root cause behind such mis-match is a lack of topology awareness of resource scheduler, especially during preemption. To bridge this gap, we develop a fine-grained topology-aware method for preemptive scheduling of hybrid workloads. The method ensures that the resources freed by preempted tasks adhere to the topological affinity needs of high-priority preemptors in a guaranteed or best-effort manner. This dynamic alignment significantly increases the efficiency of preemption and improves overall scheduled performance for LLM workloads by 55%.

## 🔑 Keywords dari Paper
LLM serving , Co-location , Topology-aware scheduling, Preemption

## 💬 Kesan Awal
-  Cukup menarik, karena bagi scheduler  bisamemahami topologi GPU itu sangat baru di pikiran saya
- Masalahnya ada di kecocokan tata letak hardware, masalah yang sangat fisik, tapi diatasi dengan scheduler, menarik.

## 📝 Action
- [ ] Baca Bab 1
- [ ] Cari paper terkait dari references-nya