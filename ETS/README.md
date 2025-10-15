# Sistem Vending Coffee Machine

LINK DEMO YOUTUBE: https://youtu.be/aPp8w-0so4E

---

## Fitur Mesin Vending Coffee Machine

### A. Pemilihan Kopi
- Menampilkan daftar **jenis kopi** yang tersedia (misalnya: *Espresso*, *Cappuccino*, *Latte*, *Americano*).  
- Menampilkan **harga tiap jenis kopi**.  
- Pengguna dapat **memilih jenis kopi** yang diinginkan.  


### B. Pemilihan Ukuran Gelas
- Menawarkan pilihan ukuran gelas: **Small**, **Medium**, **Large**.  
- Harga disesuaikan dengan ukuran gelas  
  > contoh: `+Rp2.000` untuk Medium, `+Rp4.000` untuk Large.  


### C. Penambahan Bahan Tambahan atau _add on_ (*Optional*)
- Pengguna dapat menambahkan **gula**  
  > Opsi:
  > *no sugar*, *less sugar*, *normal sugar*, *add sugar `+Rp1.000`*.  
- Pengguna dapat menambahkan **susu**.  


### D. Pembayaran
- Menampilkan **total harga** berdasarkan pilihan.  
- Mesin menampilkan QR code (QRIS) dengan nominal yang pas sesuai harga.
- Pengguna melakukan scan dan membayar dengan nominal tersebut.
- Sistem memverifikasi status pembayaran:
  - Jika berhasil, lanjut ke proses pembuatan kopi.
  - Jika gagal, transaksi dibatalkan dan tidak diproses.


### E. Proses Pembuatan Kopi
- Mesin **mengurangi stok bahan** (kopi, gula, susu, air) sesuai pesanan.  
- Menampilkan proses pembuatan kopi:  
  > `"Sedang membuat kopi Anda..."`  
- Setelah selesai, menampilkan pesan:  
  > `"Kopi siap disajikan!"`  


### F. Log Transaksi
- Setiap transaksi disimpan ke dalam **log**:  
  - tanggal  
  - jenis kopi  
  - ukuran  
  - tambahan  
  - harga  
  - metode pembayaran  
  - sisa stok  
- **Admin** dapat menampilkan log transaksi.  


### G. Manajemen Stok Bahan
- Melihat **jumlah stok bahan** (kopi, gula, susu, air).  
- Stok **berkurang otomatis** setiap kali kopi dibuat.  
- Menampilkan peringatan  
  > `"Stok hampir habis"` jika bahan di bawah batas minimum.  
- **Admin** dapat melakukan **refill stok bahan**.  


### H. Laporan Transaksi (administrator)
- Menampilkan daftar **transaksi yang sudah dilakukan**:  
  - tanggal  
  - pesanan  
  - total harga  
- Menampilkan **total pendapatan harian**.  


### I. Status Mesin (administrator)
- Menampilkan **status mesin**:  
  > “Aktif”, “Sedang membuat kopi”, atau “Butuh Refill”.  
- **Admin** dapat **mematikan** atau **menghidupkan mesin**.  

---

## Rancangan Kelas dan Rancangan Objek

### Deskripsi singkat sistem

Sistem Vending Coffee Machine ini mensimulasikan mesin kopi otomatis yang menerima pembayaran non-tunai (QRIS).
Pengguna memilih kopi, ukuran, tambahan bahan, lalu mesin menampilkan QR bayar dengan nominal sesuai total harga.
Setelah pembayaran berhasil diverifikasi, mesin membuat kopi dan menyimpan data transaksi ke log.

### Rancangan Kelas (Atribut dan Method)

1. Class Coffee
    Atribut:
    ```java
    String name;       // nama kopi (Espresso, Latte, dsb)
    String size;       // Small, Medium, Large
    boolean addSugar;  // true jika tambah gula
    boolean addMilk;   // true jika tambah susu
    double basePrice;  // harga dasar kopi
    ```
    
    Method:
    ```java
    public Coffee(String name, String size, boolean addSugar, boolean addMilk, double basePrice);
    public double calculatePrice();   // hitung total harga berdasarkan ukuran dan tambahan
    public String getDescription();   // kembalikan deskripsi pesanan
    ```

2. Class IngredientStock
    Atribut:
    ```java
    int coffeePowder;   // gram
    int sugar;          // gram
    int milk;           // ml
    int water;          // ml
    ```
    
    Method:
    ```java
    public IngredientStock(int coffeePowder, int sugar, int milk, int water);
    public boolean checkAvailability(Coffee coffee); // cek apakah bahan cukup
    public void useIngredients(Coffee coffee);       // kurangi stok sesuai pesanan
    public void refill();                            // isi ulang stok
    public void showStock();                         // tampilkan stok
    ```

3. Class Payment (QRIS Version)
    Atribut:
    ```java
    double totalPrice;
    boolean paymentStatus;
    ```
    
    Method:
    ```java
    public Payment(double totalPrice);
    public void generateQR();     // tampilkan QR dengan nominal pembayaran
    public void confirmPayment(); // simulasi pembayaran berhasil
    public boolean isPaid();      // kembalikan status pembayaran
    ```

5. Class TransactionLog
    Atribut:
    ```java
    ArrayList<String> logs;
    ```
    
    Method:
    ```java
    public TransactionLog();
    public void addLog(String transaction); // tambahkan data transaksi
    public void showLogs();                 // tampilkan semua transaksi
    ```

6. Class Admin
    Atribut:
    ```java
    String name;
    ```
    
    Method:
    ```java
    public Admin(String name);
    public void checkStock(IngredientStock stock);
    public void refillStock(IngredientStock stock);
    public void viewTransactions(TransactionLog log);
    ```

7. Class VendingMachine
    Atribut:
    ```java
    IngredientStock stock;
    TransactionLog log;
    boolean isActive;
    ```
    
    Method:
    ```java
    public VendingMachine();
    public void startMachine();           // mengaktifkan mesin
    public void showMenu();               // menampilkan daftar kopi
    public Coffee selectCoffee();         // memilih kopi dan ukuran
    public void processOrder(Coffee coffee); // alur pembayaran dan pembuatan kopi
    public void makeCoffee(Coffee coffee);   // proses pembuatan kopi
    public void stopMachine();            // mematikan mesin
    ```


## Implementasi dan Output

### Gambaran Alur
- Alur simulasi ketika program dijalankan:
- Mesin dihidupkan → menampilkan menu kopi.
- Pengguna memilih kopi dan ukuran.
- Pengguna menentukan tambahan (gula/susu).
- Sistem menghitung total harga.
- Sistem menampilkan QRIS pembayaran dengan nominal sesuai harga.
- Pengguna “membayar” (disimulasikan otomatis berhasil).
- Mesin membuat kopi → mengurangi stok bahan.
- Mesin menampilkan pesan “Kopi siap disajikan”.
- Sistem menyimpan transaksi ke log.

### Struktur Kelas Final
Kita akan menggunakan 6 kelas utama:
- `Coffee` → mendefinisikan jenis kopi dan harga dasarnya.
- `Stock` → mengatur ketersediaan bahan (kopi, gula, susu, air).
- `Payment` → memproses pembayaran QRIS.
- `Transaction` → mencatat setiap transaksi.
- `VendingMachine` → logika utama mesin kopi.
- `Main` → menjalankan simulasi.


1. Coffee.java
    ```java
    public class Coffee {
        private String name;
        private String size;
        private boolean addSugar;
        private boolean addMilk;
        private double price;
    
        public Coffee(String name, String size, boolean addSugar, boolean addMilk) {
            this.name = name;
            this.size = size;
            this.addSugar = addSugar;
            this.addMilk = addMilk;
            calculatePrice();
        }
    
        private void calculatePrice() {
            double basePrice = 0;
            switch (name.toLowerCase()) {
                case "espresso": basePrice = 10000; break;
                case "americano": basePrice = 12000; break;
                case "latte": basePrice = 15000; break;
                case "cappuccino": basePrice = 16000; break;
                default: basePrice = 10000; break;
            }
    
            if (size.equalsIgnoreCase("medium")) basePrice += 2000;
            if (size.equalsIgnoreCase("large")) basePrice += 4000;
            if (addSugar) basePrice += 1000;
            if (addMilk) basePrice += 1500;
    
            this.price = basePrice;
        }
    
        public double getPrice() { return price; }
    
        public String getDescription() {
            return name + " (" + size + ")" +
                    (addSugar ? " + gula" : "") +
                    (addMilk ? " + susu" : "");
        }
    }
    ```

2. Stock.java
    ```java
    public class Stock {
        private int coffee;
        private int sugar;
        private int milk;
        private int water;
    
        public Stock(int coffee, int sugar, int milk, int water) {
            this.coffee = coffee;
            this.sugar = sugar;
            this.milk = milk;
            this.water = water;
        }
    
        public boolean isAvailable(boolean needSugar, boolean needMilk) {
            return coffee > 0 && water > 0 &&
                   (!needSugar || sugar > 0) &&
                   (!needMilk || milk > 0);
        }
    
        public void useIngredients(boolean needSugar, boolean needMilk) {
            coffee--;
            water--;
            if (needSugar) sugar--;
            if (needMilk) milk--;
        }
    
        public void showStock() {
            System.out.println("\n--- Stok Bahan ---");
            System.out.println("Kopi : " + coffee);
            System.out.println("Gula : " + sugar);
            System.out.println("Susu : " + milk);
            System.out.println("Air  : " + water);
        }
    }
    ```

3. Payment.java
    ```java
    public class Payment {
        private double totalPrice;
        private boolean isPaid;
    
        public Payment(double totalPrice) {
            this.totalPrice = totalPrice;
            this.isPaid = false;
        }
    
        public void generateQR() {
            System.out.println("\n[QRIS] Silakan scan QR untuk membayar sebesar Rp" + totalPrice);
        }
    
        public void confirmPayment() {
            // Dalam simulasi: pembayaran selalu sukses
            System.out.println("Pembayaran berhasil diterima ✅");
            isPaid = true;
        }
    
        public boolean isPaid() {
            return isPaid;
        }
    }
    ```

4. Transaction.java
    ```java
    import java.util.ArrayList;
    
    public class Transaction {
        private ArrayList<String> logs = new ArrayList<>();
    
        public void addTransaction(String coffeeName, double price) {
            logs.add(coffeeName + " - Rp" + price);
        }
    
        public void showTransactions() {
            System.out.println("\n Riwayat Transaksi:");
            if (logs.isEmpty()) {
                System.out.println("Belum ada transaksi.");
            } else {
                for (String log : logs) {
                    System.out.println("- " + log);
                }
            }
        }
    }

    ```

5. VendingMachine.java
    ```java
    import java.util.Scanner;
    
    public class VendingMachine {
        private Stock stock;
        private Transaction transaction;
    
        public VendingMachine() {
            stock = new Stock(10, 10, 10, 10);
            transaction = new Transaction();
        }
    
        public void start() {
            Scanner sc = new Scanner(System.in);
            System.out.println("=== Vending Coffee Machine ===");
    
            boolean running = true;
            while (running) {
                System.out.println("\n1. Beli Kopi");
                System.out.println("2. Lihat Stok");
                System.out.println("3. Lihat Transaksi");
                System.out.println("4. Keluar");
                System.out.print("Pilih menu: ");
                int menu = sc.nextInt();
                sc.nextLine();
    
                switch (menu) {
                    case 1 -> makeCoffee(sc);
                    case 2 -> stock.showStock();
                    case 3 -> transaction.showTransactions();
                    case 4 -> running = false;
                    default -> System.out.println("Pilihan tidak valid!");
                }
            }
    
            System.out.println("Terima kasih telah menggunakan mesin kopi ☕");
            sc.close();
        }
    
        private void makeCoffee(Scanner sc) {
            System.out.println("\nPilih jenis kopi:");
            System.out.println("1. Espresso\n2. Americano\n3. Latte\n4. Cappuccino");
            int choice = sc.nextInt(); sc.nextLine();
    
            String name = switch (choice) {
                case 1 -> "Espresso";
                case 2 -> "Americano";
                case 3 -> "Latte";
                case 4 -> "Cappuccino";
                default -> "Espresso";
            };
    
            System.out.print("Pilih ukuran (small/medium/large): ");
            String size = sc.nextLine();
    
            System.out.print("Tambah gula? (y/n): ");
            boolean addSugar = sc.nextLine().equalsIgnoreCase("y");
    
            System.out.print("Tambah susu? (y/n): ");
            boolean addMilk = sc.nextLine().equalsIgnoreCase("y");
    
            if (!stock.isAvailable(addSugar, addMilk)) {
                System.out.println("❌ Stok tidak cukup! Silakan hubungi admin.");
                return;
            }
    
            Coffee coffee = new Coffee(name, size, addSugar, addMilk);
            System.out.println("\nTotal harga: Rp" + coffee.getPrice());
    
            Payment payment = new Payment(coffee.getPrice());
            payment.generateQR();
    
            // Simulasi pembayaran
            System.out.print("Tekan ENTER setelah pembayaran berhasil...");
            sc.nextLine();
            payment.confirmPayment();
    
            if (payment.isPaid()) {
                stock.useIngredients(addSugar, addMilk);
                System.out.println("☕ Sedang membuat kopi Anda...");
                System.out.println("Kopi " + coffee.getDescription() + " siap dinikmati!");
                transaction.addTransaction(coffee.getDescription(), coffee.getPrice());
            }
        }
    }

    ```

6. Main.java
   ```java
    public class Main {
        public static void main(String[] args) {
            VendingMachine machine = new VendingMachine();
            machine.start();
        }
    }
   ```

   <img width="500" alt="image" src="https://github.com/user-attachments/assets/963a4bcf-3419-4a67-b0ed-f4496ec8f36f" />
    <img width="500" alt="image" src="https://github.com/user-attachments/assets/8c368241-06a8-44f5-9bc3-e98579d5f843" />
















