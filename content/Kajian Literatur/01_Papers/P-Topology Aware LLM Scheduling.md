---
type: paper
status: explored
tags:
  - paper
konferensi: arXiv
tahun: "2024"
keywords: LLM serving , co-location , topology-aware scheduling, preemption
---
# 📄Topology-aware Preemptive Scheduling for Co-located LLM Workloads

**Link:** https://arxiv.org/abs/2411.11560
**Sumber:** arXiv 2024

## 📌 Abstrak
Menjalankan berbagai workload LLM dalam satu cluster GPU bisa menghemat biaya. Preemption dipakai untuk elastisitas resource, tetapi resource yang dilepas sering tidak cocok dengan kebutuhan topologi layanan prioritas tinggi. Akibatnya preemption jadi tidak efisien. Solusinya, scheduling preemptive yang sadar topologi: resource yang dibebaskan disesuaikan dengan affinity topologi preemptor. Performa penjadwalan LLM meningkat 55%.

## 🔑 Keywords Utama
- LLM workloads
- co-location
- preemptive scheduling
- topology awareness
- resource affinity
## 🎯 Problem yang Dipecahkan
Resource yang di-preempt tidak selalu sesuai kebutuhan topologi layanan prioritas tinggi yang latency-sensitive.

## 💡 Solusi yang Ditawarkan
Metode topology-aware preemptive scheduling yang memastikan resource hasil preemption memenuhi kebutuhan topological affinity preemptor, baik secara guaranteed maupun best-effort.

## 🔗 Paper Terkait (dari references mereka)
- vLLM (SOSP'23)
- Orca (OSDI'22)

## 💭 Kesan & Potensi
- 