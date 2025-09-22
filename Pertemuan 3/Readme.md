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





