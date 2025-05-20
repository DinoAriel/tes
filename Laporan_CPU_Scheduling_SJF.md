
# LAPORAN OPERATING SYSTEM

## TENTANG “CPU SCHEDULLING SJF”

---

### Anggota Kelompok:
- Havid Rosihandanu (3124500048)  
- Dino Ariel Ihsan Saputra (3124500053)  

### Dosen Pengajar:
- Dr. Ferry Astika Saputra, ST, M.Sc

---

## CPU SCHEDULLING SJF WITHOUT ARRIVAL TIME

### Analisa Code

```c
#include<stdio.h>

struct proc {
    int no, bt, ct, tat, wt;
};

struct proc read(int i) {
    struct proc p;
    printf("\nProcess No: %d\n", i);
    p.no = i;
    printf("Enter Burst Time: ");
    scanf("%d", &p.bt);
    return p;
}
```

Penjelasan:

- `no` : Nomor unik proses.  
- `bt` : Burst Time (waktu eksekusi proses).  
- `ct` : Completion Time (waktu selesainya proses).  
- `tat` : Turnaround Time (total waktu dari awal hingga selesai, `ct - arrival time`).  
- `wt` : Waiting Time (waktu menunggu proses di antrian, `tat - bt`).  

Fungsi `read` digunakan untuk membaca input burst time dari pengguna.  
Setiap proses diberi nomor sesuai urutan pemanggilan fungsi (`i`).

---

```c
printf("<--SJF Scheduling Algorithm Without Arrival Time (Non-Preemptive)-->
");
printf("Enter Number of Processes: ");
scanf("%d", &n);
```

Program meminta jumlah proses (`n`) dari pengguna.

---

```c
for(int i = 0; i < n; i++)
    p[i] = read(i + 1);
```

Loop untuk membaca data burst time setiap proses menggunakan fungsi `read()`.

---

```c
for(int i = 0; i < n - 1; i++)
    for(int j = 0; j < n - i - 1; j++)    
        if(p[j].bt > p[j + 1].bt) {
            tmp = p[j];
            p[j] = p[j + 1];
            p[j + 1] = tmp;
        }
```

Proses diurutkan berdasarkan burst time dari terkecil ke terbesar menggunakan algoritma Bubble Sort.  
**Tujuan:** Memprioritaskan proses dengan burst time terpendek (konsep SJF).

---

```c
for(int i = 0; i < n; i++) {
    ct += p[i].bt;
    p[i].ct = p[i].tat = ct;
    avgtat += p[i].tat;
    p[i].wt = p[i].tat - p[i].bt;
    avgwt += p[i].wt;
}
```

- **Completion Time (CT)**: Waktu selesainya proses dihitung secara akumulatif.  
- **Turnaround Time (TAT)**: Karena semua proses memiliki `arrival time = 0`, maka `TAT = CT`.  
- **Waiting Time (WT)**: `WT = TAT - BT`.

Nilai `TAT` dan `WT` diakumulasikan untuk menghitung rata-rata.

---

```c
printf("\nProcessNo\tBT\tCT\tTAT\tWT\tRT\n");
for(int i = 0; i < n; i++)
    printf("P%d\t\t%d\t%d\t%d\t%d\t%d\n", p[i].no, p[i].bt, p[i].ct, p[i].tat, p[i].wt, p[i].wt);
```

Menampilkan tabel hasil perhitungan untuk setiap proses.  
**Response Time (RT)** sama dengan **WT** karena SJF non-preemptive tidak ada interupsi.

---

```c
avgtat /= n;
avgwt /= n;
printf("\nAverage TurnAroundTime = %f\nAverage WaitingTime = %f", avgtat, avgwt);
```

Menghitung dan menampilkan rata-rata TAT dan WT.

---

## Gantt Chart

_(Gantt chart belum tersedia di dokumen asli, bisa ditambahkan berdasarkan urutan eksekusi)_

---

## Tabel

_(Tabel hasil eksekusi bisa ditambahkan jika hasil input tersedia)_

---

## Hasil

_(Hasil lengkap program tergantung dari input dan eksekusi program)_

---

## Kesimpulan

Kode ini adalah contoh dasar **SJF Non-Preemptive** yang efektif untuk kasus khusus di mana semua proses tersedia sejak awal.  
Meski memiliki keterbatasan, algoritma ini menjadi fondasi untuk memahami konsep optimasi penjadwalan proses dan bisa dikembangkan lebih lanjut untuk skenario yang lebih kompleks.
