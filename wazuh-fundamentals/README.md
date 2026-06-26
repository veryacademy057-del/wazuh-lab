# 🛡️ Wazuh Fundamentals — Platform Keamanan Open Source untuk Deteksi Ancaman

> **Seri Lab:** Blue Team SOC Lab  
> **YouTube:** [▶️ Tonton Tutorial di YouTube](https://youtu.be/Q4HBV3ZdGjA?si=lO4K8d0M_fp9hxjA)  
> **Kategori:** `SIEM, XDR, Threat Detection`

---

## 📋 Deskripsi

Materi ini membahas **Wazuh** secara menyeluruh — mulai dari pengertian, arsitektur tiga komponen utama, kemampuan deteksi ancaman, perbandingan dengan tools SIEM lain, hingga alasan mengapa Wazuh wajib dikuasai di bidang cybersecurity. Pemahaman ini adalah fondasi sebelum menginstall dan mengkonfigurasi Wazuh di lab.

---

## 🎬 Video Tutorial

[![Wazuh Fundamentals - Platform Keamanan Open Source](https://img.youtube.com/vi/Q4HBV3ZdGjA/maxresdefault.jpg)](https://youtu.be/Q4HBV3ZdGjA?si=lO4K8d0M_fp9hxjA)

> 📺 **[Tonton di YouTube → Wazuh Fundamentals: Platform Keamanan Open Source](https://youtu.be/Q4HBV3ZdGjA?si=lO4K8d0M_fp9hxjA)**

---

## 🔐 Apa itu Wazuh?

**Wazuh** adalah platform keamanan open source yang menyediakan kemampuan **deteksi ancaman, monitoring integritas, respons insiden, dan kepatuhan regulasi** secara terpusat. Wazuh mengumpulkan, menganalisis, dan mengkorelasikan data keamanan dari seluruh infrastruktur — baik server, endpoint, maupun cloud — dalam satu dashboard terpusat.

### Kategori Wazuh

| Kategori | Penjelasan |
|----------|------------|
| **SIEM** (Security Information and Event Management) | Mengumpulkan dan menganalisis log dari seluruh infrastruktur |
| **XDR** (Extended Detection and Response) | Aktif mendeteksi ancaman, memberikan alert, dan melakukan respons otomatis |

> 💡 Wazuh sering digunakan sebagai **alternatif open source** dari tools berbayar seperti Splunk, IBM QRadar, dan Microsoft Sentinel — dengan kemampuan yang sebanding namun **tanpa biaya lisensi**.

---

## 🏗️ Arsitektur Wazuh — Tiga Komponen Utama

```
┌─────────────────────────────────────────────────────────────┐
│                    Infrastruktur Lab                        │
│                                                             │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │  Wazuh Agent │  │  Wazuh Agent │  │  Wazuh Agent │      │
│  │  Windows 10  │  │  Win Server  │  │  Kali Linux  │      │
│  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘      │
│         │                 │                 │               │
│         └─────────────────┼─────────────────┘               │
│                           │  Port 1514 (terenkripsi)        │
│                           ▼                                 │
│              ┌────────────────────────┐                     │
│              │     Wazuh Server       │                     │
│              │  (Analisis & Alert)    │                     │
│              └────────────┬───────────┘                     │
│                           │                                 │
│                           ▼                                 │
│              ┌────────────────────────┐                     │
│              │   Wazuh Dashboard      │                     │
│              │  (HTTPS via Browser)   │                     │
│              └────────────────────────┘                     │
└─────────────────────────────────────────────────────────────┘
```

### Penjelasan Setiap Komponen

**1. Wazuh Agent**

Program ringan yang diinstall di setiap endpoint yang ingin dimonitor — Windows, Linux, atau macOS. Agent mengumpulkan:
- Log sistem
- Perubahan file
- Aktivitas proses
- Koneksi jaringan

Semua data dikirim ke Wazuh Server menggunakan **protokol terenkripsi di port 1514**.

---

**2. Wazuh Server**

Otak dari seluruh sistem Wazuh. Server bertugas:
- Menerima data dari semua agent
- Menganalisis menggunakan ruleset deteksi ancaman
- Mengkorelasikan event dari berbagai sumber
- Menghasilkan alert saat aktivitas mencurigakan terdeteksi
- Menyimpan konfigurasi terpusat yang bisa di-push ke semua agent sekaligus

---

**3. Wazuh Dashboard**

Antarmuka web berbasis **OpenSearch Dashboards** untuk memantau kondisi seluruh infrastruktur secara real-time. Menyajikan:
- Visualisasi alert
- Status agent
- Laporan kepatuhan
- Timeline kejadian keamanan

Diakses melalui browser menggunakan **HTTPS**.

---

### Alur Data

```
[Agent di endpoint]
        │
        │  Kirim log (Port 1514 terenkripsi)
        ▼
[Wazuh Server]
        │
        │  Analisis & generate alert
        ▼
[Wazuh Dashboard]
        │
        │  Visualisasi real-time
        ▼
[SOC Analyst]
```

---

## 💪 Kemampuan Utama Wazuh

| Kemampuan | Penjelasan |
|-----------|------------|
| **Log Data Analysis** | Mengumpulkan dan menganalisis log dari OS, aplikasi, dan perangkat jaringan untuk mendeteksi aktivitas mencurigakan |
| **File Integrity Monitoring (FIM)** | Memantau perubahan pada file dan direktori penting — siapa yang mengubah, kapan, dan apa yang berubah |
| **Vulnerability Detection** | Mendeteksi software usang atau memiliki CVE yang diketahui di setiap endpoint |
| **Threat Intelligence** | Mengkorelasikan event dengan database ancaman seperti VirusTotal dan MITRE ATT&CK |
| **Intrusion Detection** | Mendeteksi pola serangan seperti brute force, port scan, dan privilege escalation |
| **Active Response** | Melakukan tindakan otomatis saat ancaman terdeteksi — misalnya memblokir IP penyerang |
| **Compliance Monitoring** | Membantu memenuhi standar kepatuhan PCI DSS, GDPR, HIPAA, dan ISO 27001 |
| **Cloud Security** | Monitoring keamanan di AWS, Azure, dan Google Cloud |

---

## ⚖️ Wazuh vs Tools SIEM Lain

| Aspek | Wazuh | Splunk | Microsoft Sentinel | IBM QRadar |
|-------|-------|--------|-------------------|------------|
| **Lisensi** | Open source (gratis) | Berbayar (mahal) | Berbayar (per GB) | Berbayar (enterprise) |
| **Deployment** | On-premise / cloud | Cloud / on-premise | Cloud (Azure) | On-premise / cloud |
| **Kemudahan Setup** | Menengah | Mudah | Mudah | Kompleks |
| **Komunitas** | Besar, aktif | Sangat besar | Besar | Terbatas |
| **Cocok untuk** | Home lab, SME, belajar | Skala besar | Ekosistem Microsoft | Skala besar |

---

### Wazuh + Elastic Stack

Wazuh secara native terintegrasi dengan **Elastic Stack** (Elasticsearch, Kibana). Kombinasi ini sering disebut **ELK + Wazuh** dan merupakan salah satu stack SIEM open source yang paling banyak digunakan saat ini.

```
Wazuh Agent → Wazuh Server → Elasticsearch → Kibana Dashboard
```

---

### Wazuh dan MITRE ATT&CK

Setiap alert di Wazuh **dipetakan ke framework MITRE ATT&CK** — standar internasional yang mengelompokkan teknik serangan siber. Ini memudahkan analis untuk:
- Memahami konteks serangan
- Mengidentifikasi fase serangan (reconnaissance, execution, persistence, dll)
- Menentukan langkah respons yang tepat

---

## 🎯 Kenapa Wazuh Wajib Dipelajari?

Dengan membangun dan mengoperasikan Wazuh di home lab, kita membangun skill nyata yang dibutuhkan di industri:

| Skill | Yang Dipelajari |
|-------|----------------|
| **Deploy & Konfigurasi SIEM** | Cara kerja server, agent, dan dashboard sebagai satu kesatuan sistem monitoring |
| **Log Collection & Analisis** | Membaca, memahami, dan menginterpretasikan security event dari berbagai OS |
| **Threat Detection** | Bagaimana serangan terlihat dari sisi defender — pola brute force, port scan, privilege escalation |
| **Alert Triage** | Membedakan alert yang perlu ditindaklanjuti dengan false positive |
| **MITRE ATT&CK Mapping** | Mengklasifikasikan teknik serangan ke framework standar internasional |

---

## 📌 Kesimpulan

| Konsep | Poin Penting |
|--------|-------------|
| **Wazuh** | Platform SIEM + XDR open source — gratis, powerful, komunitas besar |
| **Wazuh Agent** | Diinstall di setiap endpoint yang ingin dimonitor |
| **Wazuh Server** | Otak sistem — analisis, korelasi, dan generate alert |
| **Wazuh Dashboard** | Antarmuka web real-time untuk monitoring seluruh infrastruktur |
| **MITRE ATT&CK** | Setiap alert Wazuh dipetakan ke framework standar internasional ini |
| **ELK + Wazuh** | Kombinasi SIEM open source paling populer saat ini |

---

## 📚 Referensi

- [Wazuh Official Documentation](https://documentation.wazuh.com/)
- [Wazuh GitHub Repository](https://github.com/wazuh/wazuh)
- [MITRE ATT&CK Framework](https://attack.mitre.org/)
- [Wazuh + Elastic Stack Integration](https://documentation.wazuh.com/current/deployment-options/elastic-stack/index.html)

---

*📺 Ikuti tutorialnya di [YouTube](https://youtu.be/Q4HBV3ZdGjA?si=lO4K8d0M_fp9hxjA) | ⭐ Star repo ini jika membantu!*
