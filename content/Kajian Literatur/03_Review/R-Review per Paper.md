### Informasi Ekstraksi dari Setiap Paper (Struktur Artikel Ilmiah)

---
#### Paper 1: AlphaBoot (`D-AlphaBoot.pdf`)

1. **Judul Spesifik, Area, Metode Usulan, & Objectives:**
    - **Judul:** _AlphaBoot: accelerated container cold start using SmartNICs_.
    - **Area:** _Cloud Datacenter Computing, Serverless Computing (FaaS), Container Orchestration, Hardware Offloading_.
    - **Metode Usulan:** Penggunaan _System-on-Chip (SoC)_ SmartNIC (NVIDIA BlueField-2) sebagai lapisan _shared cache container image_ lokal, yang dipadukan dengan transfer via _NFS mounted drive_ dan modifikasi _engine_ Docker.
    - **Objectives:** Mempercepat waktu _cold start_ kontainer dan menghemat _bandwidth_ jaringan di dalam data center akibat proses download _image_ berulang.
2. **Abstrak (Ringkasan Isi):**
    - **Inti Masalah:** _Cold start latency_ yang tinggi saat menarik gambar kontainer berukuran besar (500–700 MB) dari _registry online_ oleh banyak VM pada host fisik yang sama.
    - **Proses Inti:** Memotong permintaan download _image_, menyimpan layer _base image_ di media penyimpanan SmartNIC, dan membagikannya ke VM melalui _network drive_ lokal tanpa _SSL/TCP handshake_ berulang.
    - **Hasil Kuantitatif & Kesimpulan:** Mengurangi latensi _cold start_ hingga 92.64% (Alpine) dan 52.75%–62.52% (Nginx, Ubuntu, Python); mempercepat _deploy serverless function_ dari 4.7 detik menjadi 0.08 detik (58.75x lebih cepat).
3. **Introduction:**
    - **Gambaran Besar & PoV:** _Virtual Machines_ (VM) dan kontainer adalah fondasi cloud. Penarikan kontainer berulang menyia-nyiakan CPU host dan jaringan. Penulis berpandangan bahwa _Domain-Specific Processors/SmartNICs_ harus dimanfaatkan untuk tugas non-jaringan seperti _image caching_.
    - **Fokus & Tujuan:** Menghilangkan redundansi penarikan _image_ antar-VM pada server bare-metal yang sama.
4. **Studi Literature / Related Research:**
    - Merujuk pada optimasi _cold start_ berbasis aplikasi seperti _FaaSLight_, strategi penjadwalan pencopotan kontainer _LCS_, _ComboFunc_, serta optimasi _SmartNIC_ untuk komputasi serverless (lambda-NIC).
5. **Methods:**
    - **Research Steps:** Modifikasi _runtime_ Docker, integrasi protokol transfer NFS, pembuatan fungsi serverless OpenFaaS kustom, dan pengujian latensi/bandwidth.
    - **Data Source:** 4 _base image_ populer DockerHub: Alpine (7.7 MB), Ubuntu (69 MB), Nginx (188 MB), Python (996 MB) dan fungsi OpenFaaS kustom.
    - **Proposed Methods:** Algoritma *interception* penarikan _image_ (Algorithm 1), penyimpanan tarball gzip di SmartNIC, dan integrasi kebijakan _eviction_ fleksibel.
6. **Result and Discussion:**
    - Penggunaan SCP menghasilkan overhead buruk (-433%), namun protokol NFS memangkas latency _cold start_ hingga 92.64%. Penghematan _bandwidth_ jaringan dihitung berdasarkan perkalian jumlah request  (N) dan ukuran image (B). Overhead SmartNIC RAM/disk sangat kecil (penggunaan disk <1 GB dari total 42 GB).
7. **Conclusion & Future Works:**
    - **Kesimpulan:** AlphaBoot terbukti secara signifikan memangkas waktu _cold start_ dan penghematan energi/biaya jaringan pusat data.
    - **Future Works:** Akselerasi transfer menggunakan RDMA (RoCE), kompresi image via _Slim Toolkit_ (hingga 30x), algoritma _eviction_ berbasis _Machine Learning_, dan porting ke SmartNIC berbasis FPGA/ASIC.
8. **References & Acknowledgement:**
    - Didukung oleh Cloud Lab Santa Clara University; kode sumber terbuka dipublikasikan di GitHub. Mengutip 25+ referensi utama (Docker, Kubernetes, AWS, Azure, Google Cloud Streaming).

---

#### Paper 2: CloudCoaster (`D-Cloudcoaster.pdf`)

1. **Judul Spesifik, Area, Metode Usulan, & Objectives:**
    - **Judul:** _CloudCoaster: Transient-aware Bursty Datacenter Workload Scheduling_.
    - **Area:** _Datacenter Resource Management, Hybrid Workload Scheduling, Dynamic Cloud Infrastructure_.
    - **Metode Usulan:** _Hybrid Scheduler_ yang memanfaatkan server _transient_ (misal: AWS Spot Instances) murah untuk secara dinamis mengubah partisi kluster (_dynamic short partition resizing_).
    - **Objectives:** Mengurangi latensi antrean (_queueing delay_) tugas-tugas pendek (_short tasks_) saat terjadi lonjakan beban (_burstiness_) tanpa membengkakkan anggaran biaya atau mengganggu _long tasks_.
2. **Abstrak (Ringkasan Isi):**
    - **Inti Masalah:** Fluktuasi _arrival rate heterogeneity/burstiness_ pada kluster statis memicu fenomena _head-of-line blocking_, membuat _short jobs_ tertahan di belakang _long jobs_.
    - **Proses Inti:** Mengukur status beban kluster via metrik _long load ratio_ dan mengatur penambahan/pengurangan server _transient_ melalui komponen _Transient Manager_.
    - **Hasil Kuantitatif & Kesimpulan:** Mengurangi _average queueing delay_ tugas pendek sebesar 4.8x dan memotong *cost short partition* sebanyak 29.5%.
3. **Introduction:**
    - **Gambaran Besar & PoV:** Kluster modern memproses pekerjaan heterogen. Server _transient_ menawarkan potongan hingga 90% dibanding _on-demand_, namun memiliki risiko _revocation_ sewaktu-waktu. _Short tasks_ sangat cocok memanfaatkan server _transient_ karena durasinya singkat sebelum dicabut.
    - **Fokus & Tujuan:** Merancang scheduler hybrid yang adaptif terhadap fluktuasi kedatangan tugas.
4. **Studi Literature / Related Research:**
    - Membandingkan dengan scheduler terpusat (_YARN_, _Quincy_), terdistribusi (_Sparrow_), dan hybrid (_Eagle_, _Hawk_, _Mercury_).y
5. **Methods:**
    - **Research Steps:** Perancangan arsitektur _Centralized/Decentralized Scheduler_, formulasi matematis ukuran partisi dinamis \(T = N((r-1)p+1)\), dan simulasi berbasis _event-driven_.
    - **Data Source:** _Trace_ beban kerja nyata Yahoo (_Yahoo trace_) dan analisis _trace_ Google.
    - **Proposed Methods:** Penggunaan metrik _long-load ratio_ \(l_r = N_{long}/N_{total}\); logika penambahan agresif dan pengurangan konservatif server _transient_; penjadwalan minimal 1 salinan tugas ke server _on-demand_ untuk keamanan _revocation_.
6. **Result and Discussion:**
    - _Queueing delay_ rata-rata membaik dari 232.3 detik (_baseline Eagle_) menjadi 48.25 detik (pada _cost ratio_ \(r=3\), efisiensi 4.8x). Usia pakai rata-rata server _transient_ dalam simulasi adalah 0.77–0.82 jam (jauh di bawah _Mean Time To Failure_ Amazon Spot yang >18 jam). Penghematan biaya partisi pendek mencapai 29.5% (menghemat 11.8 server _on-demand_).
    - **Referensi:** _Section 4.1–4.2, Hal. 4–5_.
7. **Conclusion & Future Works:**
    - **Kesimpulan:** CloudCoaster terbukti ampuh menangani beban _bursty_ secara fleksibel dan hemat biaya.
    - **Future Works:** Evaluasi skala besar pada _trace_ kluster Google dan implementasi sebagai _scheduling plugin_ pada Apache Spark.
8. **References & Acknowledgement:**
    - Kode simulasi dipublikasikan secara terbuka di GitHub. Mengutip 34 referensi (USENIX ATC, EuroSys, SOSP, SoCC).
---

#### Paper 3: Coach (`D-Coach.pdf`)

1. **Judul Spesifik, Area, Metode Usulan, & Objectives:**
    - **Judul:** _Coach: Exploiting Temporal Patterns for All-Resource Oversubscription in Cloud Platforms_.
    - **Area:** _Cloud Infrastructure, Virtual Machine Management, Resource Oversubscription, Predictive Scheduling_.
    - **Metode Usulan:** Sistem _oversubscription_ untuk **semua jenis sumber daya** (_CPU, Memory, Network, Storage_) dengan mengeksploitasi pola penggunaan temporal melalui jenis VM baru (_CoachVM_) dan _time-window scheduling_.
    - **Objectives:** Meningkatkan utilisasi pusat data yang rendah (_underutilized/stranded resources_) secara transparan dan aman tanpa mengorbankan _Service Level Agreements (SLA)_ beban kerja.
2. **Abstrak (Ringkasan Isi):**
    - **Inti Masalah:** Rendahnya utilisasi sumber daya di _public cloud_ (Azure) akibat pemesanan statis dan fenomena _resource stranding_. _Memory oversubscription_ sangat berisiko karena sifatnya yang _non-fungible_ dan sensitif terhadap kontensi.
    - **Proses Inti:** Membagi alokasi VM menjadi bagian _Guaranteed (Physical Allocation)_ dan _Oversubscribed (Virtual Allocation)_, memprediksi utilisasi per _time window_, serta menggunakan prediktor kontensi dua tingkat (EWMA + LSTM).
    - **Hasil Kuantitatif & Kesimpulan:** Memungkinkan kluster menampung hingga ~26% lebih banyak VM, menghemat jumlah server hingga 44%, dengan degradasi kinerja beban kerja <10%.
3. **Introduction:**
    - **Gambaran Besar & PoV:** Penyedia awan (Azure, AWS, GCP) menghadapi utilisasi memori dan CPU yang sangat rendah. _Oversubscription_ tradisional berfokus pada satu sumber daya (misal CPU saja), yang justru memperparah _stranding_ pada sumber daya lain seperti memori.
    - **Fokus & Tujuan:** Solusi _all-resource oversubscription_ holistik berbasis pola temporal.
    - **Referensi:** _Section 1 & 2.1, Hal. 1–3_.
4. **Studi Literature / Related Research:**
    - Menganalisis _Borg_ (Google), _Autopilot_, _Twine_ (Meta), _Resource Central_ (Azure), serta pendekatan _far memory/CXL_ (Pond). Coach adalah sistem virtualisasi VM pertama yang menargetkan seluruh sumber daya sekaligus.
    - **Referensi:** _Section 5, Hal. 9–10_.
5. **Methods:**
    - **Research Steps:** Karakterisasi _trace_ Azure 1 juta VM selama 2 minggu, perancangan _CoachVM_, simulasi skala besar, dan eksperimen nyata pada server produksi.
    - **Data Source:** _Trace_ produksi Microsoft Azure (10 kluster, 7 region); 9 aplikasi benchmark nyata: _Cache (Redis), Database, Big Data, Web, KV-Store, Graph, Microservice, LLM-FT, Video Conf_.
    - **Proposed Methods:** _CoachVM partitioning_ (PA vs VA); _Time-window bin-packing_ (6 window x 4 jam per hari dengan prediksi P95); Prediktor kontensi _EWMA_ (20 detik) + _LSTM_ (5 menit); Mitigasi reaktif dan proaktif (_trimming cold memory_, _extend pool_, _VM migration_).
    - **Referensi:** _Section 2, 3.1–3.4, & 4.1, Hal. 2–6_.
6. **Result and Discussion:**
    - Menambah kapasitas jual VM sebesar +26% dibanding _baseline_ statis. Menekan _slowdown_ beban kerja real-time sensitif (Cache, KV-Store) dari 4.3x saat terjadi kontensi menjadi hanya 1.3x dengan mitigasi proaktif. _Overhead platform_ sangat efisien (model training offline <121 detik, memori model 186 MB).
    - **Referensi:** _Section 4.2–4.5, Hal. 6–9_.
7. **Conclusion & Future Works:**
    - **Kesimpulan:** Coach membuktikan bahwa _all-resource oversubscription_ berbasis pola temporal dapat meningkatkan kapasitas kluster secara masif dengan proteksi performa yang handal.
    - **Future Works:** Peluncuran bertahap (_staged rollout_) untuk _third-party workloads_ melalui opsi _opt-in discounted VM_, serta integrasi dengan arsitektur memori CXL modern.
    - **Referensi:** _Section 3.5 & 6, Hal. 5, 10_.
8. **References & Acknowledgement:**
    - Dibiayai dan dikembangkan oleh Microsoft Research bekerjasama dengan UIUC, UW, dan UCLA. Mengutip 110 referensi bereputasi.
    - **Referensi:** _References, Hal. 10–18_.

---

#### Paper 4: Quicksand (`D-Quicksand.pdf`)

1. **Judul Spesifik, Area, Metode Usulan, & Objectives:**
    - **Judul:** _Quicksand: Harnessing Stranded Datacenter Resources with Granular Computing_.
    - **Area:** _Datacenter Resource Management, Memory Disaggregation, Granular Computing, Rack-scale Systems_.
    - **Metode Usulan:** _Framework runtime_ komputasi granular yang memisahkan konsumsi CPU dan Memori ke dalam _Resource Proclets_ (Compute Proclet, Memory Proclet, Hybrid Proclet) yang dapat membelah (_split_), menggabung (_merge_), dan bermigrasi secara mandiri dalam hitungan milidetik.
    - **Objectives:** Mendaur ulang _stranded resources_ (sumber daya menganggur terisolasi) di tingkat rak pusat data tanpa terhambat oleh _overhead kernel paging_ pada sistem disagregasi memori konvensional.
    - **Referensi:** _Title & Section 1, Hal. 1–2_.
2. **Abstrak (Ringkasan Isi):**
    - **Inti Masalah:** _Resource stranding_ akibat ketidakcocokan antara kebutuhan aplikasi dan ketersediaan fisik pada mesin, membuat CPU atau RAM terbuang.
    - **Proses Inti:** Membongkar aplikasi menggunakan abstraksi _Resource Proclets_, mengelola ukuran proclet via _AutoSharder_, dan memindahkan proclet secara dinamis ke mesin yang memiliki ketersediaan sumber daya.
    - **Hasil Kuantitatif & Kesimpulan:** Mencapai _throughput_ 2–8x lebih tinggi dibanding _Hermit_ (disagregasi memori) dan 2–3x dibanding _Nu_ (komputasi granular konvensional); menghemat 60% CPU pada _video encoding_; meningkatkan utilisasi 25%–60%.
    - **Referensi:** _Abstract & Section 7.1–7.3, Hal. 1, 7–9_.
3. **Introduction:**
    - **Gambaran Besar & PoV:** Aplikasi pusat data terikat oleh batas fisik mesin. Disagregasi komputasi berbasis perangkat lunak granular memungkinkan aplikasi mengonsumsi CPU dan RAM secara terpisah di seluruh rak jaringan berkecepatan tinggi (100–400 GbE).
    - **Fokus & Tujuan:** Menyediakan antarmuka pemrograman berkinerja tinggi yang fleksibel untuk memanfaatkan sumber daya terdampar.
    - **Referensi:** _Section 1 & 3, Hal. 1–3_.
4. **Studi Literature / Related Research:**
    - Menganalisis sistem disagregasi _far-memory_ (_Hermit_, _Infiniswap_), sistem komputasi granular (_Nu_), kerangka _auto-sharding_ (_Slicer_, _Shard Manager_), dan _resource harvesting_.
    - **Referensi:** _Section 9, Hal. 10–11_.
5. **Methods:**
    - **Research Steps:** Pengembangan prototipe C++ (10k LoC) di atas _Nu_, pembuatan pustaka abstraksi _AutoSharder_ (_ShardedVector_, _ShardedMap_, _BatchComputing_), dan porting 4 aplikasi studi kasus.
    - **Data Source:** _Trace_ pusat data Alibaba; 4 aplikasi representatif: _ML Training Pipeline, SocialNetwork (DeathStarBench), Data Sorting (TritonSort), Video Encoding (ExCamera)_.
    - **Proposed Methods:** Tiga tipe _Resource Proclets_ (Compute ratio >0.1, Memory ratio <0.001, Hybrid 0.001–0.1); penyesuaian skala otomatis berbasis panjang antrean; serta mekanisme pembelahan/penggabungan proclet dalam skala 2 ms.
    - **Referensi:** _Section 4, 5, & 6, Hal. 3–7_.
6. **Result and Discussion:**
    - Pada skenario _unbalanced resources_, Quicksand mempertahankan _throughput_ mendekati kondisi _ideal_ (26k image/s pada ML pipeline). Menghilangkan lonjakan latensi ekstrim pada aplikasi _latency-critical_ dibanding _Hermit_ yang menderita _paging overhead_. Skala adaptif cepat (2 ms) terbukti krusial untuk menjaga saturasi GPU.
    - **Referensi:** _Section 7.1–7.4, Hal. 7–10_.
7. **Conclusion & Future Works:**
    - **Kesimpulan:** Quicksand berhasil mendaur ulang _stranded resources_ secara dinamis dan presisi melalui skema komputasi granular.
    - **Future Works:** Refactoring aplikasi _monolithic legacy_ agar mendukung komputasi terdistribusi granular, dan eksplorasi dukungan _interconnect_ CXL/GenZ.
    - **Referensi:** _Section 8.1–8.2 & 10, Hal. 10–11_.
8. **References & Acknowledgement:**
    - Proyek dipublikasikan _open-source_ di GitHub; didukung oleh Facebook Research, Google, DARPA FastNICs, NSF, dan VMware. Mengutip 61 referensi.
    - **Referensi:** _References & Acknowledgements, Hal. 11–12_.

---

#### Paper 5: Starburst (`D-Starburst.pdf`)

1. **Judul Spesifik, Area, Metode Usulan, & Objectives:**
    - **Judul:** _Starburst: A Cost-aware Scheduler for Hybrid Cloud_.
    - **Area:** _Hybrid Cloud Management, Cost-Aware Scheduling, Large-Scale AI & Data Analytics Workloads_.
    - **Metode Usulan:** _Higher-level Resource Manager_ yang menerapkan algoritma penundaan dinamis (_Compute-Wait_ dan _Star-Wait_), eksekusi _Out-of-Order (OO)_ agresif, serta kerangka _Waiting Budget (\(P%\))_.
    - **Objectives:** Memaksimalkan utilisasi kluster swasta (_on-premise_) guna meminimalkan biaya _public cloud_ hingga mendekati batas matematis optimal dengan peningkatan _Job Completion Time (JCT)_ yang sangat kecil.
    - **Referensi:** _Title & Section 1, Hal. 1–2_.
2. **Abstrak (Ringkasan Isi):**
    - **Inti Masalah:** Beban kerja AI/analitik data yang _bursty_ memaksa organisasi menggunakan _hybrid cloud_. Namun, scheduler _cloud-enabled_ eksisiting menghasilkan kompromi biaya-JCT yang tidak efisien akibat utilisasi kluster swasta yang rendah.
    - **Proses Inti:** Menahan _job_ besar lebih lama di antrean agar mendapatkan sumber daya lokal, dan melempar _job_ kecil lebih cepat ke cloud; menghindari _head-of-line blocking_ via _Out-of-Order scheduling_.
    - **Hasil Kuantitatif & Kesimpulan:** Mengurangi biaya cloud sebesar 54%–91% pada simulasi _trace_ produksi dan 78%–80% pada kluster fisik 32-GPU, hanya dengan peningkatan JCT rata-rata maksimal 5.8%.
    - **Referensi:** _Abstract & Section 6.2–6.3, Hal. 1, 6–7_.
3. **Introduction:**
    - **Gambaran Besar & PoV:** Pertumbuhan model AI membutuhkan kluster GPU multi-tenant yang mahal. Saat _burst_ terjadi, membeli _hardware on-premise_ baru tidak ekonomis. Penulis menekankan bahwa kunci penghematan biaya adalah memaksimalkan utilisasi kluster privat hingga >95% sebelum menyewa kluster publik.
    - **Fokus & Tujuan:** Menyediakan kontrol fleksibel tunggal (_waiting budget_) bagi administrator untuk menavigasi kurva _trade-off_ Biaya vs JCT.
    - **Referensi:** _Section 1 & 2, Hal. 1–2_.
4. **Studi Literature / Related Research:**
    - Dibandingkan dengan _Slurm_, _Kubernetes Autoscaler_, strategi _Constant-Wait_, _Backfill Scheduling_, dan penyedia multi-cloud broker (_SkyPilot_).
    - **Referensi:** _Section 2 & 7, Hal. 2, 9_.
5. **Methods:**
    - **Research Steps:** Formulasi masalah _Cost-JCT trade-off_, perancangan algoritma _Compute-Wait_ (rumus \(w^*(j) = \alpha \cdot (\sum W_k r_{jk}) \cdot t_j\)) dan _Star-Wait_ (tanpa estimasi waktu runtime), pembangunan _simulator_ dan sistem riil terdistribusi (5k LoC Python), serta pengujian kluster fisik.
    - **Data Source:** _Trace_ produksi publik Microsoft Philly (~100k GPU jobs), Microsoft Helios (~250k jobs), dan pengujian fisik 32-GPU NVIDIA V100 dengan model AI (_ResNet, BERT, GPT-2, MobileNet_).
    - **Proposed Methods:** _Compute-Wait_ / _Star-Wait preemption threshold_ \(T_{max}\); _Aggressive Out-of-Order Execution_; _Waiting Budget Knob_ (\(P%\)); Integrasi _SkyPilot API_ untuk penyediaan multi-cloud.
    - **Referensi:** _Section 4 & 5, Hal. 3–5_.
6. **Result and Discussion:**
    - Menghemat biaya cloud $134K–$650K pada _trace_ Philly/Helios. Utilisasi kluster privat meningkat dari 81% (baseline) menjadi 92.6%–99.2%. Hasil Starburst terbukti mendekati titik optimal teori matematika _Mixed Integer Linear Programming (MILP)_ dengan deviasi hanya ~5%. Robust terhadap kelemahan _data gravity_ (transfer delay) dan lonjakan kedatangan sangat _bursty_.
    - **Referensi:** _Section 6.2–6.6, Hal. 6–9_.
7. **Conclusion & Future Works:**
    - **Kesimpulan:** Starburst terbukti menjadi manajer sumber daya hybrid yang sangat tangguh dalam menekan biaya pengoperasian komputasi awan.
    - **Future Works:** Dukungan untuk pekerjaan yang dapat di-_checkpoint_ secara otomatis serta alokasi sumber daya berbasis _spot instances_ antar penyedia awan yang lebih dinamis.
    - **Referensi:** _Section 4 & 8, Hal. 3, 9_.
8. **References & Acknowledgement:**
    - Dibiayai oleh UC Berkeley, Accenture, AMD, Google, Intel, Microsoft, IBM; kode terbuka di GitHub. Mengutip 75 referensi.
    - **Referensi:** _References & Artifact Appendix, Hal. 9–10_.

---

#### Paper 6: Topology-aware Scheduling (`D-Topology-aware Scheduling.pdf`)

1. **Judul Spesifik, Area, Metode Usulan, & Objectives:**
    - **Judul:** _Topology-aware Preemptive Scheduling for Co-located LLM Workloads_.
    - **Area:** _Cloud-Native GPU Datacenter Scheduling, Large Language Model (LLM) Serving, Preemptive Scheduling, Hardware Topology Affinity_.
    - **Metode Usulan:** Pengenalan _FlexTopo_ (representasi topologi terpadu real-time) dan algoritma preepsi terkoordinasi _FlexTopo-based IMP (Iterative Max-Priority)_ dengan dua tahap: _Guaranteed Filtering_ dan _Best-effort Sorting_.
    - **Objectives:** Menjamin bahwa sumber daya GPU/CPU yang dibebaskan oleh _victim task_ saat preempsi memenuhi kebutuhan afinitas topologi perangkat keras (_NUMA, Socket, NVLink_) dari _workload_ LLM prioritas tinggi.
    - **Referensi:** _Title & Section 1, Hal. 1–2_.
2. **Abstrak (Ringkasan Isi):**
    - **Inti Masalah:** Ko-lokasi _workload_ LLM heterogen (layanan chat online sensitif latensi vs _batch jobs_) memicu preempsi saat _auto-scaling_. Preempsi standar melepaskan GPU secara terfragmentasi (_cross-socket/cross-NUMA_), menyebabkan alokasi gagal atau degradasi performa.
    - **Proses Inti:** Mengumpulkan topologi fisik server via _FlexTopo Agent_, memetakan status alokasi, dan memilih kombinasi _victim_ yang memberikan penyatuan topologi terbaik untuk _preemptor_.
    - **Hasil Kuantitatif & Kesimpulan:** Meningkatkan _topology affinity hit rate_ dari 44.5% menjadi 100%; mengeliminasi alokasi lintas-socket; dan meningkatkan performa penjadwalan terjangkau beban kerja LLM sebesar 55%.
    - **Referensi:** _Abstract & Section 5, Hal. 1, 11–13_.
3. **Introduction:**
    - **Gambaran Besar & PoV:** Beban kerja LLM online memiliki pola lalu lintas harian (_diurnal pattern_). Ko-lokasi dengan _batch job_ memaksimalkan utilisasi GPU yang sangat mahal. Penulis menekankan bahwa penjadwalan terprediksi tanpa kepedulian topologi pada tingkat preempsi adalah penyebab utama ketidakefisienan kluster.
    - **Fokus & Tujuan:** Menyediakan kerangka terpadu penyesuaian topologi dinamis tanpa memicu _restart/failure_.
    - **Referensi:** _Section 1 & 2.3, Hal. 1–3_.
4. **Studi Literature / Related Research:**
    - Membandingkan dengan _Kubernetes TopologyManager_, _MOTAS_, _Gödel (ByteDance Katalyst)_, dan penjadwalan berbasis grafik komunikasi GPU.
    - **Referensi:** _Section 6, Hal. 14–15_.
5. **Methods:**
    - **Research Steps:** Pemodelan graf topologi perangkat keras _FlexTopo_, pembuatan _FlexTopo Agent_ daemon, perancangan algoritma seleksi korban _IMP_, serta validasi kluster fisik dan simulasi KWOK.
    - **Data Source:** Kluster _near-production_ Baichuan-Inc berisi 41 GPU server (tiap server 8x NVIDIA RTX 4090 GPU, 2-socket, 8-NUMA); serta simulasi 100-node GPU cluster berbasis KWOK (_Kubernetes Without Kubelet_).
    - **Proposed Methods:** _FlexTopo unified graph representation_ (edge: _host, contain, localized, nearby_); Fungsi skor perkelompokan \(S(C) = \alpha \cdot \frac{1}{\sum \text{priority}} + (1-\alpha) \cdot T(C_{flextopo})\); Optimasi pencarian _Iterative Max-Priority (IMP)_.
    - **Referensi:** _Section 3.2–3.4, Hal. 5–8_.
6. **Result and Discussion:**
    - Mengeliminasi alokasi _cross-socket_ secara total. Pada 5.000 skenario preempsi, _FlexTopo_ mencapai _hit rate_ topologi 100% dibanding 44.5% pada metode _Gödel_ standar. Algoritma optimasi IMP memotong overhead durasi pencarian kandidat sebesar 32.8%–33.9%.
    - **Referensi:** _Section 5, Hal. 11–13_.
7. **Conclusion & Future Works:**
    - **Kesimpulan:** FlexTopo terbukti menyelesaikan masalah _misalignment_ topologi saat preempsi pada kluster ko-lokasi LLM.
    - **Future Works:** Pengembangan untuk skala multi-cluster, integrasi topologi jaringan inter-node, serta dukungan pemisahan intra-GPU dinamis (MPS/MIG).
    - **Referensi:** _Section 6 & 7, Hal. 14–15_.
8. **References & Acknowledgement:**
    - Diproduksi oleh tim infrastruktur Baichuan-Inc. Mengutip 35 referensi ilmiah terkemuka.
    - **Referensi:** _References, Hal. 14–15_.
