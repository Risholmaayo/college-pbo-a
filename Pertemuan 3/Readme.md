Nama: Achmad Hasan Al Fikri

NRP: 5025231052

Kelas: PBO A

<br>

Kali ini saya membuat sistem ticket machine menggunakan Java (BlueJ). Biasanya BlueJ dipakai untuk latihan OOP (Object Oriented Programming). Jadi, kita bisa membuat kelas sederhana yang merepresentasikan mesin tiket, lalu pengguna bisa "membeli" tiket dengan memasukkan uang.

Berikut contoh implementasi sederhana sistem TicketMachine:

```java
/**
 * TicketMachine.java
 * Sebuah mesin tiket sederhana
 */
public class TicketMachine {
    // Harga tiket
    private int price;
    // Jumlah uang yang sudah dimasukkan user
    private int balance;
    // Total uang yang dikumpulkan mesin
    private int total;

    // Constructor untuk menentukan harga tiket
    public TicketMachine(int ticketCost) {
        price = ticketCost;
        balance = 0;
        total = 0;
    }

    // Method untuk melihat harga tiket
    public int getPrice() {
        return price;
    }

    // Method untuk melihat saldo saat ini
    public int getBalance() {
        return balance;
    }

    // Method untuk memasukkan uang
    public void insertMoney(int amount) {
        if (amount > 0) {
            balance = balance + amount;
        } else {
            System.out.println("Masukkan uang harus lebih dari 0!");
        }
    }

    // Method untuk mencetak tiket
    public void printTicket() {
        if (balance >= price) {
            System.out.println("##################");
            System.out.println("#  Tiket Bus    #");
            System.out.println("#  Harga: Rp " + price + " #");
            System.out.println("##################");
            System.out.println();

            // Tambahkan ke total mesin
            total = total + price;
            // Kurangi saldo user
            balance = balance - price;
        } else {
            System.out.println("Saldo tidak cukup. Masukkan Rp " + (price - balance) + " lagi.");
        }
    }

    // Method untuk mengembalikan uang user
    public int refundBalance() {
        int amountToRefund = balance;
        balance = 0;
        return amountToRefund;
    }

    // Method untuk melihat total uang yang sudah dikumpulkan mesin
    public int getTotal() {
        return total;
    }
}
```

<br>

Kode ini adalah simulasi mesin tiket sederhana:
- Mesin punya harga tiket tetap (misalnya Rp 5.000).
- Pengguna bisa memasukkan uang ke mesin.
- Kalau uang cukup → mesin akan mencetak tiket.
- Kalau uang kurang → mesin akan minta tambahan uang.
- Mesin juga bisa mengembalikan saldo jika pengguna membatalkan.

<br>

Cara menjalankannya di BlueJ:
1. Buat Project baru → beri nama misalnya TicketMachineProject.
2. Buat kelas baru dengan nama TicketMachine.
3. Copy-paste kode di atas.
4. Compile.
5. Klik kanan pada kelas TicketMachine, pilih new TicketMachine(5000) (misalnya harga tiket Rp 5000).
6. Objek akan muncul.
    - Klik kanan objek → insertMoney(2000) → saldo bertambah Rp 2000.
    - Klik lagi insertMoney(3000) → total saldo Rp 5000.
    - Klik printTicket() → tiket akan tercetak di terminal.


**Penjelasan Kelas & Variabel**
```java
public class TicketMachine {
    private int price;   // harga tiket (misalnya Rp 5000)
    private int balance; // jumlah uang yang sudah dimasukkan user
    private int total;   // total uang yang dikumpulkan mesin
```
- price → harga tiket tetap, ditentukan ketika objek mesin dibuat.
- balance → saldo uang yang sudah dimasukkan pengguna ke mesin.
- total → total pendapatan mesin (uang yang sudah benar-benar masuk setelah tiket dicetak).

**Constructor**
```java
public TicketMachine(int ticketCost) {
    price = ticketCost;
    balance = 0;
    total = 0;
}
```
- Saat buat objek baru, misalnya new TicketMachine(5000) → maka harga tiket = Rp 5000.
- Saldo awal (balance) dan total (total) = 0.

**Getter Methods**
```java
public int getPrice() {
    return price;
}

public int getBalance() {
    return balance;
}

public int getTotal() {
    return total;
}
```
- getPrice() → lihat harga tiket.
- getBalance() → cek berapa saldo yang sudah dimasukkan.
- getTotal() → lihat total pendapatan mesin.

**Insert Money**
```java
public void insertMoney(int amount) {
    if (amount > 0) {
        balance = balance + amount;
    } else {
        System.out.println("Masukkan uang harus lebih dari 0!");
    }
}
```
- Digunakan untuk memasukkan uang ke mesin.
- Jika amount lebih dari 0 → saldo (balance) bertambah.
- Kalau salah (misal angka negatif) → mesin menolak.

**Print Ticket**
```java
public void printTicket() {
    if (balance >= price) {
        System.out.println("##################");
        System.out.println("#  Tiket Bus    #");
        System.out.println("#  Harga: Rp " + price + " #");
        System.out.println("##################");
        System.out.println();

        total = total + price;   // uang masuk ke mesin
        balance = balance - price; // saldo user dikurangi
    } else {
        System.out.println("Saldo tidak cukup. Masukkan Rp " + (price - balance) + " lagi.");
    }
}
```
- Jika saldo cukup → cetak tiket (pakai `System.out.println`).
- Tambahkan harga tiket ke total.
- Kurangi saldo user (balance).
- Kalau saldo kurang → beri pesan “masukkan uang lagi”.

**Refund**
```java
public int refundBalance() {
    int amountToRefund = balance;
    balance = 0;
    return amountToRefund;
}
```
- Untuk mengembalikan sisa saldo yang belum terpakai.
- Misalnya harga tiket Rp 5000, user sudah masukkan Rp 7000.
- Setelah cetak tiket → saldo = 2000.
- Kalau dipanggil refundBalance() → user dapat Rp 2000 kembali.

**Contoh Alur Interaksi**
1. Membuat objek ticket machine


   
3. User memasukkan uang
4. Mencoba cetak tiket
5. User memasukkan uang lagi
6. Mencetak tiket
7. Coba dengan memasukkan jumlah uang yang lebih besar
8. Refund atau mengambil sisa saldo yang tersedia



