# UKL_1sampai7

import java.util.*;
import java.text.NumberFormat;

public class UKL_RPL_SemesterGanjil2025 {

    static Scanner sc = new Scanner(System.in);
    static Random rand = new Random();
    static NumberFormat nf = NumberFormat.getInstance();

    public static void main(String[] args) {
        nf.setGroupingUsed(true); // untuk format Rp1,200,000

        int pilihan;
        do {
            System.out.println("\n" + "=".repeat(50));
            System.out.println("   📘 SOAL UKL - REKAYASA PERANGKAT LUNAK");
            System.out.println("   Kelas X | Semester Ganjil 2025/2026");
            System.out.println("=".repeat(50));
            System.out.println("1. Cek Bilangan Prima");
            System.out.println("2. Hitung Pecahan Uang");
            System.out.println("3. Kuis Perkalian, Pembagian, Modulus");
            System.out.println("4. Cek Duplikat dalam Array");
            System.out.println("5. Permainan Lempar Dadu");
            System.out.println("6. Hitung Biaya Pinjam Buku");
            System.out.println("7. Analisis Laba/Rugi Cookies");
            System.out.println("0. Keluar");
            System.out.print("Pilih soal (0–7): ");
            pilihan = sc.hasNextInt() ? sc.nextInt() : -1;

            switch (pilihan) {
                case 1 -> soal1();
                case 2 -> soal2();
                case 3 -> soal3();
                case 4 -> soal4();
                case 5 -> soal5();
                case 6 -> soal6();
                case 7 -> soal7();
                case 0 -> System.out.println("✅ Terima kasih. Program selesai.");
                default -> System.out.println("⚠️ Pilihan tidak valid.");
            }

            if (pilihan != 0) {
                System.out.print("\nTekan ENTER untuk kembali ke menu...");
                sc.nextLine(); // consume newline after nextInt
                sc.nextLine(); // wait for Enter
            }

        } while (pilihan != 0);
    }

    // ===== SOAL 1: Cek Bilangan Prima =====
    static void soal1() {
        System.out.println("\n🔹 SOAL 1: Cek Bilangan Prima");
        System.out.print("Masukkan bilangan: ");
        int n = sc.nextInt();

        if (n < 2) {
            System.out.println(n + " bukan bilangan prima.");
        } else {
            boolean isPrime = true;
            for (int i = 2; i * i <= n; i++) { // i <= Math.sqrt(n) → i*i <= n (lebih cepat)
                if (n % i == 0) {
                    isPrime = false;
                    break;
                }
            }
            System.out.println(isPrime ? n + " adalah bilangan prima." : n + " bukan bilangan prima.");
        }
    }

    // ===== SOAL 2: Hitung Pecahan Uang =====
    static void soal2() {
        System.out.println("\n🔹 SOAL 2: Hitung Pecahan Uang");
        System.out.print("Jumlah uang (dalam rupiah): ");
        int uang = sc.nextInt();

        if (uang < 0) {
            System.out.println("❌ Jumlah uang tidak boleh negatif.");
            return;
        }

        int[] pecahan = {100000, 50000, 20000, 10000, 5000, 2000, 1000};
        System.out.println("Hasil pecahan:");

        for (int p : pecahan) {
            int lembar = uang / p;
            if (lembar > 0) {
                System.out.println(lembar + " Lembar " + p);
                uang %= p;
            }
        }
        if (uang > 0) {
            System.out.println("⚠️ Sisa uang tidak bisa dipecah: Rp" + uang);
        }
    }

    // ===== SOAL 3: Kuis Matematika =====
    static void soal3() {
        System.out.println("\n🔹 SOAL 3: Kuis Perkalian, Pembagian, Modulus");
        String lanjut;
        do {
            int a = rand.nextInt(10) + 1; // 1–10
            int b = rand.nextInt(10) + 1; // 1–10
            char op = "*%/".charAt(rand.nextInt(3));
            int hasil = 0;

            // Pastikan pembagian menghasilkan integer
            if (op == '/') {
                while (a % b != 0) {
                    a = rand.nextInt(100) + 1;
                    b = rand.nextInt(10) + 1;
                }
                hasil = a / b;
            } else if (op == '*') {
                hasil = a * b;
            } else { // '%'
                hasil = a % b;
            }

            System.out.print(a + " " + op + " " + b + " = ");
            int jawaban = sc.nextInt();

            if (jawaban == hasil) {
                System.out.println("✅ Benar!");
            } else {
                System.out.println("❌ Salah. Jawaban benar: " + hasil);
            }

            System.out.print("Lanjut? (y/n): ");
            lanjut = sc.next().trim().toLowerCase();
        } while (lanjut.equals("y"));
    }

    // ===== SOAL 4: Cek Duplikat dalam Array =====
    static void soal4() {
        System.out.println("\n🔹 SOAL 4: Cek Duplikat dalam Array");
        System.out.print("Masukkan jumlah elemen array: ");
        int n = sc.nextInt();
        int[] arr = new int[n];
        System.out.println("Masukkan elemen-elemen array:");
        for (int i = 0; i < n; i++) {
            arr[i] = sc.nextInt();
        }

        Set<Integer> seen = new HashSet<>();
        List<Integer> duplikat = new ArrayList<>();
        for (int num : arr) {
            if (!seen.add(num) && !duplikat.contains(num)) {
                duplikat.add(num);
            }
        }

        if (duplikat.isEmpty()) {
            System.out.println("Tidak ada elemen duplikat.");
        } else {
            System.out.print("Array memiliki elemen duplikat: ");
            for (int i = 0; i < duplikat.size(); i++) {
                if (i > 0) System.out.print(", ");
                System.out.print(duplikat.get(i));
            }
            System.out.println();
        }
    }

    // ===== SOAL 5: Permainan Lempar Dadu =====
    static void soal5() {
        System.out.println("\n🔹 SOAL 5: Permainan Lempar Dadu");
        List<Integer> komputer = new ArrayList<>();
        List<Integer> pemain = new ArrayList<>();
        int winK = 0, winP = 0, ronde = 1;

        System.out.println("Permainan dimulai! Target: 5 kemenangan.");
        sc.nextLine(); // consume newline

        while (winK < 5 && winP < 5) {
            System.out.println("\n--- Ronde " + ronde + " ---");

            int dk = rand.nextInt(6) + 1;
            komputer.add(dk);
            System.out.println("Komputer melempar... Dadu: " + dk);

            System.out.print("Tekan ENTER untuk melempar dadu Anda: ");
            sc.nextLine();
            int dp = rand.nextInt(6) + 1;
            pemain.add(dp);
            System.out.println("Dadu Anda: " + dp);

            if (dp > dk) {
                winP++;
                System.out.println("🎉 Pemain menang di ronde ini!");
            } else if (dk > dp) {
                winK++;
                System.out.println("🤖 Komputer menang di ronde ini!");
            } else {
                System.out.println("🤝 Seri!");
            }
            System.out.println("Skor: Pemain(" + winP + ") vs Komputer(" + winK + ")");
            ronde++;
        }

        System.out.println("\n" + "=".repeat(40));
        System.out.println("🎮 PERMAINAN SELESAI!");
        if (winP == 5) {
            System.out.println("🏆 Pemenangnya adalah: PEMAIN");
        } else {
            System.out.println("🏆 Pemenangnya adalah: KOMPUTER");
        }
        System.out.println("=".repeat(40));
        System.out.println("Riwayat lemparan komputer: " + komputer);
        System.out.println("Riwayat lemparan pemain  : " + pemain);
        System.out.println("Total kemenangan: Pemain(" + winP + "), Komputer(" + winK + ")");
    }

    // ===== SOAL 6: Biaya Pinjam Buku =====
    static void soal6() {
        System.out.println("\n🔹 SOAL 6: Hitung Biaya Pinjam Buku");
        System.out.print("Nama peminjam: ");
        sc.nextLine(); // consume leftover
        String nama = sc.nextLine();
        System.out.print("Judul buku: ");
        String judul = sc.nextLine();
        System.out.print("Kategori buku (A/B/C): ");
        char kat = sc.nextLine().toUpperCase().charAt(0);
        System.out.print("Lama peminjaman (hari): ");
        int hari = sc.nextInt();

        int tarif = switch (kat) {
            case 'A' -> 2000;
            case 'B' -> 1500;
            case 'C' -> 1000;
            default -> {
                System.out.println("⚠️ Kategori tidak valid → gunakan C (Rp1.000/hari)");
                yield 1000;
            }
        };

        long biayaAwal = (long) tarif * hari;
        long denda = 0;
        if (hari > 7) denda = (hari - 7) * 500L;
        long total = biayaAwal + denda;

        System.out.println("\n=== STRUK PEMINJAMAN ===");
        System.out.println("Nama peminjam      : " + nama);
        System.out.println("Judul buku         : " + judul);
        System.out.println("Kategori buku      : " + kat);
        System.out.println("Lama peminjaman    : " + hari + " hari");
        System.out.println("Biaya peminjaman   : Rp" + nf.format(biayaAwal));
        System.out.println("Denda keterlambatan: Rp" + nf.format(denda));
        System.out.println("Total biaya akhir  : Rp" + nf.format(total));
    }

    // ===== SOAL 7: Analisis Laba/Rugi Cookies =====
    static void soal7() {
        System.out.println("\n🔹 SOAL 7: Analisis Laba/Rugi Cookies");
        System.out.print("Masukkan jumlah jenis cookies: ");
        int n = sc.nextInt();
        sc.nextLine(); // consume

        class Cookie {
            String nama;
            long biaya, pendapatan, labaRugi;

            Cookie(String nama, long biaya, long pendapatan) {
                this.nama = nama;
                this.biaya = biaya;
                this.pendapatan = pendapatan;
                this.labaRugi = pendapatan - biaya;
            }

            String getStatus() {
                return labaRugi > 0 ? "Laba" : labaRugi < 0 ? "Rugi" : "Impas";
            }
        }

        List<Cookie> list = new ArrayList<>();
        long totalLabaRugi = 0;
        Cookie maxLaba = null;

        for (int i = 1; i <= n; i++) {
            System.out.println("\nCookies ke-" + i + ":");
            System.out.print("Nama cookies: ");
            String nama = sc.nextLine();
            System.out.print("Harga produksi per bungkus: ");
            long hp = sc.nextLong();
            System.out.print("Harga jual per bungkus: ");
            long hj = sc.nextLong();
            System.out.print("Jumlah terjual: ");
            long jt = sc.nextLong();
            sc.nextLine();

            long biaya = hp * jt;
            long pendapatan = hj * jt;
            Cookie c = new Cookie(nama, biaya, pendapatan);
            list.add(c);
            totalLabaRugi += c.labaRugi;

            if (maxLaba == null || c.labaRugi > maxLaba.labaRugi) {
                maxLaba = c;
            }
        }

        // Tabel Output
        String line = "-".repeat(85);
        System.out.println("\n" + line);
        System.out.printf("%-20s | %-15s | %-18s | %-12s | %-8s%n",
                "Nama Cookies", "Total Biaya", "Total Pendapatan", "Laba/Rugi", "Status");
        System.out.println(line);

        for (Cookie c : list) {
            System.out.printf("%-20s | Rp%-13s | Rp%-16s | Rp%-10s | %-8s%n",
                    c.nama,
                    nf.format(c.biaya),
                    nf.format(c.pendapatan),
                    (c.labaRugi >= 0 ? "" : "-") + nf.format(Math.abs(c.labaRugi)),
                    c.getStatus());
        }

        System.out.println(line);
        System.out.println("Total Laba/Rugi Keseluruhan: Rp" + (totalLabaRugi >= 0 ? "" : "-") + nf.format(Math.abs(totalLabaRugi)));

        if (maxLaba != null && maxLaba.labaRugi > 0) {
            System.out.println("Cookies dengan Laba Tertinggi: " + maxLaba.nama + " (Rp" + nf.format(maxLaba.labaRugi) + ")");
        } else {
            System.out.println("Tidak ada cookies yang untung.");
        }
    }
}
