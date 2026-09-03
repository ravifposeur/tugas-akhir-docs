---
type: topik
status: draft
tags: [topik]
---

# 🎯 Fokus Eksplorasi - Draft 1

## 📌 Topik
Saya tertarik pada **efisiensi resource di data center/cloud** khususnya bagaimana scheduling bisa mengatasi masalah, seperti
1. Stranded Resource : CPU Habis, Memori terlantar atau sebaliknya
2. Workload Bursty: Lonjakan job tiba-tiba
3. Workload Heterogen: Karakter job yang berbeda-beda perlu penanganan yang berbeda-beda
4. Container Cold Start: Startup container/image yang menghambat respone time di serverless/event-driven
5. Topology Affinity: Kesadaran topologi (NUMA/CPU) untuk workload latency-sensitive, sehingga job yang pake latency-sensitive tidak bisa pakai GPU yang jelek, atau terpaksa dipasang di topologi yang tidak cocok.
## 🎯 Problem Statement
Resource di data center/cloud sering tidak termanfaatkan secara optimal karena:
- Scheduler tidak mendeteksi resource yang terdampar (stranded)
- Cold start membuat response time memburuk di workload serverless
- Workload bursty membuat cluster kewalahan
- Workload heterogen (prioritas tinggi vs rendah) tidak ditangani dengan baik
- Scheduler tidak memahami topologi dengan baik.

## 🔑 Keyword Utama
-  Resource Stranding
-  Granular Computing
-  Resource Proclet
-  Container Cold Start
-  Bursty Workload
-  Topology-aware Scheduling
-  Preemptive Scheduling
-  Hybrid Scheduler
-  Control Plane
-  SRE / SLO / Tail Latency

## 🔎 Boolean Search String


## 📚 Paper Pendukung
- [[Kajian Literatur/01_Papers/P-Quicksand|P-Quicksand]]
- [[Kajian Literatur/01_Papers/P-CloudCoaster|P-CloudCoaster]]
- [[P-Topology Aware LLM Scheduling]]
- [[Kajian Literatur/01_Papers/P-AlphaBoot|P-AlphaBoot]]

## 💡 Novelty / Kebaruan


## 📝 Catatan Dosen
- 