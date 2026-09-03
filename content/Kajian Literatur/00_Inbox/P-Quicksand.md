---
type: inbox
tags: [inbox, to-explore]
tanggal: 2026-09-02
---
# 📥 Quicksand - NSDI 2025

**Link:** https://www.usenix.org/conference/nsdi25/presentation/ruan
**Sumber:** USENIX NSDI 2025

## 📌 Abstrak
Datacenters today waste CPU and memory, as re-
sources demanded by applications often fail to match the
resources available on machines. This leads to stranded re-
sources because one resource that runs out prevents placing
additional applications that could consume the other resources.
Unusable stranded resources result in reduced utilization of
servers, and wasted money and energy.
Quicksand is a new framework and runtime system that
unstrands resources by providing developers with familiar,
high-level abstractions (e.g., data structures, batch comput-
ing). Internally Quicksand decomposes them into resource
proclets, granular units that each primarily consume resources
of one type. Inspired by recent granular programming models,
Quicksand decouples consumption of resources as much as
possible. It splits, merges, and migrates resource proclets in
milliseconds, so it can use resources on any machine, even if
available only briefly.
Evaluation of our prototype with four applications shows
that Quicksand uses stranded resources effectively; that Quick-
sand reacts to changing resource availability and demand
within milliseconds, increasing utilization; and that porting
applications to Quicksand requires moderate effort.

## 🔑 Keywords dari Paper
stranded resource, resource stranding, granular computing, resource proclets, scheduler

## 💬 Kesan Awal
- Menarik karena Paper ini mencoba untuk menggunakan resources yang "tak terpakai" secara efisien
- Metode pembagian procletsnya menarik karena dibagi jadi 2, yaitu memory dan computing, sehingga memory dan cpu tak terikat dan independen.
- Hasilnya cukup memuaskan, 2-8x lebih baik daripada Hermit dan 2-3x troughput Nu.

## 📝 Action
- [x] Baca Bab 1
- [ ] Cari paper terkait dari references-nya