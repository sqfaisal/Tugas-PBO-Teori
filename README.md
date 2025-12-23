package tiketkereta;


abstract class Penumpang {
    protected String nama;
    protected String noTiket;
    
    
    public Penumpang(String nama, String noTiket) {
        this.nama = nama;
        this.noTiket = noTiket;
    }

    public abstract double hitungHargaTiket();

    public void tampilkanData() {
        System.out.println("Nama        \t: " + nama);
        System.out.println("No Tiket    \t: " + noTiket);
        System.out.println("Harga Tiket \t: Rp. " + hitungHargaTiket());
        System.out.println("Jenis       \t: Reguler");
    }
    
    public void tampilkanData(String jenis) {
        System.out.println("Nama        \t: " + nama);
        System.out.println("No Tiket    \t: " + noTiket);
        System.out.println("Harga Tiket \t: Rp. " + hitungHargaTiket());
        System.out.println("Jenis       \t: " + jenis);
    }
}


package tiketkereta;
import java.util.Scanner;

class InputPenumpang {
    protected Scanner input = new Scanner(System.in);
    }

package tiketkereta;
import tiketkereta.Penumpang;

class PenumpangVIP extends Penumpang {
    
    public PenumpangVIP(String nama, String noTiket) {
        super(nama, noTiket);
    }
    @Override
    public double hitungHargaTiket() {
        return 100000; 
        }
    }


    package tiketkereta;
class PenumpangReguler extends Penumpang {
    public PenumpangReguler(String nama, String noTiket) {
        super(nama, noTiket);
    }
    
    @Override
    public double hitungHargaTiket() {
       return 80000;
    }
}

package tiketkereta;

public class TiketKereta {
    public static void main(String[] args) {

        InputPenumpang ip = new InputPenumpang();
        
        System.out.print("Masukkan Jumlah Penumpang : ");
        int jml = ip.input.nextInt();

        Penumpang[] data = new Penumpang[jml]; 
        int jumlah = 0;
        int pil;

        do {
            System.out.println("\n==== TIKET KERETA ===");
            System.out.println("1. Tambah Penumpang");
            System.out.println("2. Tampilkan Data");
            System.out.println("3. Keluar");
            System.out.print("Masukkan pilihan : ");
            pil = ip.input.nextInt();
            ip.input.nextLine(); 

            switch (pil) {
                case 1:
                    System.out.println("\n=== TAMBAH PENUMPANG ===");

                    System.out.print("Masukkan Nama       : ");
                    String nama = ip.input.nextLine();

                    System.out.print("Masukkan No Tiket   : ");
                    String noTiket = ip.input.nextLine();

                 

                    System.out.println("Jenis Penumpang \n1. VIP \n2. Reguler");
                    System.out.print("Masukkan pilihan :");
                    int jenis = ip.input.nextInt();
                    ip.input.nextLine();

                    if (jenis == 1) {
                        data[jumlah] = new PenumpangVIP(nama, noTiket);
                    } else {
                        data[jumlah] = new PenumpangReguler(nama, noTiket);
                    }

                    jumlah++;
                    System.out.println("Penumpang berhasil ditambahkan!");
                    break;

                case 2:
                    System.out.println("\n=== DATA PENUMPANG ===");
                    if (jumlah == 0) {
                        System.out.println("Belum ada data.");
                    } else {
                        
                        for (int i = 0; i < jumlah; i++) {
                            System.out.println("\nPenumpang ke-" + (i + 1));
                            if(data[i] instanceof PenumpangVIP){
                                data[i].tampilkanData("VIP");
                            }else{
                                data[i].tampilkanData();
                            }
                            
                            
                        }
                    }
                    break;

                case 3:
                    System.out.println("Terima kasih!");
                    break;

                default:
                    System.out.println("Pilihan tidak valid!");
            }
        } while (pil != 3);
    }
}
