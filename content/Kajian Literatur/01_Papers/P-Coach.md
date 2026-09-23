---
type: paper
status: explored
tags:
  - paper
konferensi: ASPLOS
tahun: "2025"
keywords: cloud utilization, temporal pattern, resource oversubscription, VM scheduling, memory management
---

# 📄 Coach: Exploiting Temporal Patterns for All-Resource Oversubscription in Cloud Platforms

**Link:**  https://dl.acm.org/doi/epdf/10.1145/3669940.3707226
**Sumber:** ASPLOS 25

## 📌 Abstrak
Cloud masih sering underutilized. Dari data Azure, CPU paling banyak idle, dan banyak VM punya pola pemakaian yang saling melengkapi. Coach memanfaatkan pola waktu itu untuk oversubscription semua resource. Tiap VM dibagi jadi bagian guaranteed dan oversubscribed, lalu dipantau agar tidak terjadi kontensi. Hasilnya platform bisa menampung sekitar 26% VM lebih banyak tanpa penurunan performa berarti.

## 🔑 Keywords Utama
- cloud utilization
- temporal pattern
- resource oversubscription
- VM scheduling
- memory management

## 🎯 Problem yang Dipecahkan
Resource cloud tidak terpakai optimal; solusi harus mengelola semua resource, bukan hanya CPU.

## 💡 Solusi yang Ditawarkan
Coach memprediksi pola waktu dan menjadwalkan VM untuk oversubscription resource. VM baru bernama CoachVM memisahkan alokasi guaranteed dan oversubscribed, sambil memonitor kontensi.

## 🔗 Paper Terkait (dari references mereka)
- Overload (ASPLOS'18)
- Yodel (NSDI'21)
- Borg (EuroSys'15)

## 💭 Kesan & Potensi
- 