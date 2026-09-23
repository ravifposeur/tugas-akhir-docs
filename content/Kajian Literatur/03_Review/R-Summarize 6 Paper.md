
## 1. Overview & Area Identification

Keenam paper berada dalam bidang **cloud and datacenter resource management**, khususnya pada masalah efisiensi pemanfaatan resource, scheduling, resource allocation, dan optimasi infrastruktur. Walaupun fokus masing-masing paper berbeda, semuanya berangkat dari masalah yang sama, yaitu **resource datacenter tidak selalu dapat dimanfaatkan secara optimal karena workload bersifat dinamis, heterogen, dan memiliki kebutuhan resource yang berbeda**.

Secara umum, keenam paper dapat dikelompokkan berdasarkan aspek yang dioptimalkan:

- **Container & infrastructure optimization**
    - _AlphaBoot_ → mengurangi _container cold-start_ dan penggunaan bandwidth melalui SmartNIC.
- **Workload scheduling**
    - _CloudCoaster_ → menangani workload bursty dan _queueing delay_.
    - _Starburst_ → mengoptimalkan trade-off antara utilisasi private cluster dan biaya public cloud.
- **Resource utilization**
    - _Coach_ → meningkatkan utilisasi CPU, memory, network, dan storage melalui oversubscription.
    - _Quicksand_ → memanfaatkan kembali CPU dan memory yang _stranded_ melalui granular computing.
- **Hardware/topology-aware scheduling**
    - _Topology-aware Scheduling_ → mempertahankan kesesuaian topology CPU, NUMA, socket, dan GPU setelah preemption.

Dengan demikian, hubungan keenam penelitian dapat dilihat sebagai **optimasi datacenter dari beberapa *layer* yang berbeda**, mulai dari container image delivery, *scheduling workload*, pemanfaatan resource fisik, hingga *topology-aware allocation*.

---

## 2. Core Problems & Objectives

### A. Permasalahan Utama

Dari keenam paper, terdapat beberapa bentuk permasalahan utama:

1. **Resource tidak termanfaatkan secara optimal**
    - Resource dapat menjadi _stranded_ karena kebutuhan workload tidak sesuai dengan resource yang tersedia.
    - Dibahas terutama oleh **Coach** dan **Quicksand**.
2. **Workload memiliki karakteristik dinamis dan bursty**
    - Lonjakan workload dapat menyebabkan antrean panjang dan _head-of-line blocking_.
    - Menjadi fokus **CloudCoaster** dan **Starburst**.
3. **Resource tersedia tetapi tidak sesuai secara topology**
    - Pada workload GPU, resource yang tersedia (secara jumlah) belum tentu dapat digunakan apabila konfigurasi NUMA, socket, atau NVLink tidak sesuai.
    - Menjadi fokus **Topology-aware Scheduling**.
4. **Overhead pada infrastructure layer**
    - *Downloading* container image berulang menyebabkan _cold-start latency_ dan penggunaan bandwidth.
    - Menjadi fokus **AlphaBoot**.

### B. Tujuan Penelitian

Masing-masing paper kemudian memiliki tujuan yang lebih spesifik:

|Paper|Objective|
|---|---|
|**AlphaBoot**|Mengurangi _container cold-start latency_ dan penggunaan bandwidth.|
|**CloudCoaster**|Mengurangi _queueing delay_ workload pendek tanpa meningkatkan biaya secara berlebihan.|
|**Coach**|Meningkatkan utilisasi seluruh resource melalui oversubscription tanpa mengorbankan SLA.|
|**Quicksand**|Memanfaatkan kembali CPU dan memory yang _stranded_ secara lebih granular.|
|**Starburst**|Meningkatkan utilisasi private cluster dan mengurangi biaya public cloud dengan peningkatan JCT yang kecil.|
|**Topology-aware Scheduling**|Memastikan resource hasil preemption tetap memenuhi kebutuhan topology workload prioritas tinggi.|

Jadi, meskipun tujuan spesifiknya berbeda, **tujuan dari semua paper itu adalah meningkatkan efisiensi resource datacenter dengan tetap mempertahankan performa workload**.

---

## 3. Methods & Approaches

Pendekatan yang digunakan keenam paper cukup beragam.

### A. Berdasarkan mekanisme optimasinya

- **Hardware-based optimization**
    - **AlphaBoot**
    - Menggunakan NVIDIA BlueField-2 SmartNIC sebagai cache lokal container image.
    - Mengintegrasikan SmartNIC dengan NFS dan Docker runtime.
- **Dynamic scheduling**
    - **CloudCoaster**
    - Menggunakan hybrid scheduler dan transient server.
    - Ukuran partition dapat disesuaikan berdasarkan kondisi workload.
- **Prediction-based resource management**
    - **Coach**
    - Menggunakan time-window scheduling.
    - Memanfaatkan EWMA dan LSTM untuk memprediksi penggunaan resource.
- **Granular resource management**
    - **Quicksand**
    - Menggunakan _Resource Proclets_ untuk memisahkan kebutuhan compute dan memory.
    - AutoSharder melakukan penyesuaian ukuran resource secara dinamis.
- **Cost-aware scheduling**
    - **Starburst**
    - Menggunakan _Compute-Wait_, _Star-Wait_, _Out-of-Order execution_, dan _Waiting Budget_.
- **Topology-aware scheduling**
    - **Topology-aware Scheduling**
    - Menggunakan FlexTopo untuk merepresentasikan topology hardware.
    - IMP digunakan untuk memilih kombinasi victim task pada proses preemption.

### B. Data Source / Workload

Sumber data yang digunakan juga cukup beragam:

- **AlphaBoot**
    - 4 Docker base images:
        - Alpine
        - Ubuntu
        - Nginx
        - Python
    - Custom OpenFaaS functions.
- **CloudCoaster**
    - Yahoo workload trace
    - Google workload trace.
- **Coach**
    - Microsoft Azure production trace
    - ±1 juta VM
    - 10 cluster dan 7 region
    - 9 workload nyata.
- **Quicksand**
    - Alibaba datacenter trace
    - ML Training Pipeline
    - SocialNetwork
    - Data Sorting
    - Video Encoding.
- **Starburst**
    - Microsoft Philly
    - Microsoft Helios
    - Cluster fisik 32 GPU NVIDIA V100
    - ResNet, BERT, GPT-2, MobileNet.
- **Topology-aware Scheduling**
    - Cluster near-production Baichuan-Inc
    - 41 server × 8 RTX 4090
    - Simulasi 100-node menggunakan KWOK.
---

## 4. Results, Conclusions, & Future Works

### A. Hasil Kuantitatif Paper

|Paper|Hasil utama|
|---|---|
|**AlphaBoot**|Cold-start latency turun hingga **92,64%**; deployment 4,7 s → 0,08 s.|
|**CloudCoaster**|_Queueing delay_ rata-rata **4,8× lebih rendah**; biaya turun **29,5%**.|
|**Coach**|Kapasitas VM meningkat **26%**; dapat menghemat hingga **44% server**.|
|**Quicksand**|Throughput **2–8× lebih tinggi** dibanding Hermit dan **2–3×** dibanding Nu; utilisasi meningkat **25–60%**.|
|**Starburst**|Biaya cloud turun **54–91%** pada simulasi dan **78–80%** pada cluster fisik; JCT meningkat maksimal **5,8%**.|
|**Topology-aware Scheduling**|_Topology affinity hit rate_ meningkat dari **44,5% → 100%** dan _cross-socket allocation_ dieliminasi.|

### B. Kesimpulan

Dari hasil tersebut, terdapat beberapa pola yang terlihat:
- **Optimasi tidak hanya bisa dilakukan pada satu jenis resource.**
    - CPU dan memory → Coach, Quicksand
    - GPU → Starburst, Topology-aware Scheduling
    - Network/storage → AlphaBoot, Coach
    - Cloud capacity/cost → CloudCoaster, Starburst
- **Pendekatan dinamis menjadi pola penting.**
    - Dynamic partitioning
    - Predictive scheduling
    - Dynamic resource migration
    - Dynamic preemption
    - Dynamic cloud provisioning
- **Efisiensi resource semakin bergantung pada konteks workload.**
    - Workload bursty → CloudCoaster
    - Workload temporal → Coach
    - Workload hybrid/private-public → Starburst
    - Workload GPU dengan topology khusus → Topology-aware Scheduling

Artinya, literatur ini menunjukkan bahwa **efisiensi datacenter tidak cukup dicapai hanya dengan menambah resource**, tetapi juga melalui kemampuan sistem untuk memahami kondisi workload dan kemudian mengalokasikan resource secara adaptif.

### C. Future Works / Research Gap

Beberapa _future works_ yang muncul dari keenam paper antara lain:

1. **Hardware acceleration & disaggregation**
    
    - RDMA/RoCE
    - FPGA/ASIC SmartNIC
    - CXL / Gen-Z.
    
2. **Scalability**
    
    - Evaluasi pada cluster yang lebih besar.
    - Multi-cluster scheduling.
    - Inter-node network topology.
    
3. **Smarter resource management**
    
    - ML-based cache eviction.
    - Prediksi workload yang lebih baik.
    - Dynamic GPU partitioning seperti MPS/MIG.
    
4. **Broader workload compatibility**
    
    - Dukungan terhadap aplikasi legacy.
    - Workload pihak ketiga.
    - Workload yang checkpointable.
    

### D.  Research Opportunity

Kalau keenam paper ini ditarik menjadi **satu research gap**, yang dapat saya temukan adalah

**Bagaimana membangun resource management dan scheduling yang secara bersamaan mempertimbangkan karakteristik workload, kondisi resource, topology hardware, dan biaya infrastruktur dalam lingkungan datacenter yang dinamis?**

Karena masing-masing paper cenderung mengoptimalkan **satu atau beberapa dimensi tertentu**, masih terdapat ruang untuk mengintegrasikan dimensi-dimensi tadi menjadi satu riset yang utuh.