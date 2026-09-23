---
type: paper
status: explored
tags:
  - paper
konferensi: Frontiers HPC
tahun: "2025"
keywords: SmartNICs, cloud computing, containers, data center networks, virtual machines
---
# 📄AlphaBoot: accelerated container cold start using SmartNICs

**Link:** https://www.frontiersin.org/journals/high-performance-computing/articles/10.3389/fhpcp.2025.1499519/full
**Sumber:**  Frontiers HPC 2025

## 📌 Abstrak
Server punya banyak VM yang berjalan, di dalam setiap VM terdapat container. Dalam setiap container, ketika pertama kali mereka dijalankan, mereka akan mendownload image dari registry online. Hal ini masalah karena waktu download tlama dan di cloud container sering mati dan hidup lagi. Akibatnya CPU terbuang hanya untuk menunggu download image. Masalahnya, VM bersifat terisolasi, sehingga jika VM berbeda dalam satu server membutuhkan image yang sama persis, keduanya melakukan hal yang redundan dan akhirnya lalu lintas membengkak, latensi berlipat ganda, dan bandwith terbuang. Solusinya adalah SmartNIC yang menyimpan cache dari iamge yang telah didownload salah satu VM di server.

## 🔑 Keywords Utama
- SmartNICs
- Cloud Computring
- Containers
- Data Center Networks
- Virtual Machine

## 🎯 Problem yang Dipecahkan
VM terisolasi yang membuat mereka tidak bisa berbagi image yang sama, meskipun berada di server yang sama

## 💡 Solusi yang Ditawarkan
Mereka menggunakan SmartNIC yang menyimpan cache dari image yang telah didownload salah satu VM.

## 🔗 Paper Terkait (dari references mereka)
- 
- 

## 💭 Kesan & Potensi
- 