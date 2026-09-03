---
type: inbox
tags:
  - inbox
  - to-explore
tanggal:
---

# 📥 P-CloudCoaster

**Link:** https://arxiv.org/abs/1907.02162
**Sumber:** arXiv 2019

## 📌 Abstrak
day’s clusters often have to divide resources among a
diverse set of jobs. These jobs are heterogeneous both
in execution time and in their rate of arrival. Execution
time heterogeneity has lead to the development of hybrid
schedulers that can schedule both short and long jobs to
ensure good task placement. However, arrival rate het-
erogeneity, or burstiness, remains a problem in existing
schedulers. These hybrid schedulers manage resources
on statically provisioned cluster, which can quickly be
overwhelmed by bursts in the number of arriving jobs.
In this paper we propose CloudCoaster, a hybrid
scheduler that dynamically resizes the cluster by lever-
aging cheap transient servers. CloudCoaster schedules
jobs in an intelligent way that increases job performance
while reducing overall resource cost. We evaluate the ef-
fectiveness of CloudCoaster through simulations on real-
world traces and compare it against a state-of-art hybrid
scheduler. CloudCoaster improves the average queueing
delay time of short jobs by 4.8X while maintaining long
job performance. In addition, CloudCoaster reduces the
short partition budget by over 29.5%

## 🔑 Keywords dari Paper
1. Hybrid Scheduler
    
2. Dynamic Cluster Resizing
    
3. Transient Servers
    
4. Bursty Workloads
    
5. Resource Cost Optimization


## 💬 Kesan Awal
- Menarik karena sangat konkret, bahwa job sangat heterogen dan punya karakteristik masing-masing
- Menarik sekali karena solusinya bahkan sangat sederhana, yaitu menambahkan transient server untuk leveraging ukuran server.
- Performa naik, tapi biaya turun (best way)

## 📝 Action
- [x] Baca Bab 1
- [ ] Cari paper terkait dari references-nya