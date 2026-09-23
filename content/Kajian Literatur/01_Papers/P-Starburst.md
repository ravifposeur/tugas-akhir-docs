---
type: paper
status: explored
tags:
  - paper
konferensi: USENIX ATC
tahun: "2024"
keywords: hybrid cloud, cost-aware scheduling, cluster utilization, job completion time, waiting budget
---

# 📄 Starburst: a cost-aware scheduler for hybrid cloud

**Link:** https://www.usenix.org/conference/atc24/presentation/luo
**Sumber:** USENIX ATC 24
## 📌 Abstrak
Hybrid cloud dipakai untuk menangani lonjakan job batch. Masalahnya, scheduler yang ada sering boros biaya cloud atau malah memperlama JCT. Starburst mencoba memaksimalkan utilisasi cluster dengan mengatur waktu tunggu: job besar ditahan lebih lama di cluster, job kecil lebih cepat dikirim ke cloud. Ada waiting budget untuk mengatur trade-off biaya vs JCT. Hasilnya biaya cloud turun 54–91%, dengan kenaikan JCT maksimal 5,8%.

## 🔑 Keywords Utama
- hybrid cloud
- cost-aware scheduling
- cluster utilization
- job completion time
- waiting budget

## 🎯 Problem yang Dipecahkan
Scheduler hybrid cloud yang ada memberi trade-off biaya dan JCT yang tidak efisien karena utilisasi cluster rendah.

## 💡 Solusi yang Ditawarkan
Starburst mengatur waktu tunggu job secara dinamis dimana job besar diprioritaskan tetap di cluster, sedangkan job kecil diarahkan ke cloud. Administrator bisa mengatur posisi trade-off lewat waiting budget.

## 🔗 Paper Terkait (dari references mereka)
- 
- 

## 💭 Kesan & Potensi
- 