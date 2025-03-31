import java.util.Scanner;

public class SinemaKayitSistemi {
    private static String[] filmler = new String[10]; 
    private static String[] filmTurleri = new String[10]; 
    private static int[] filmSureleri = new int[10]; 
    private static int filmSayisi = 0; 
    
    private static String[] musteriler = new String[20]; 
    private static String[] musteriemail = new String[20]; 
    private static int musteriSayisi = 0; 
    
    private static int[][] biletler = new int[20][10];
    
    private static Scanner scanner = new Scanner(System.in); 
    
    public static void main(String[] args) {
        while (true) {
            System.out.println("\n--- Sinema Sistemi ---");
            System.out.println("1- Film Ekle");
            System.out.println("2- Filmleri Listele");
            System.out.println("3- Müşteri Ekle");
            System.out.println("4- Müşterileri Listele");
            System.out.println("5- Bilet Satışı");
            System.out.println("6- Satılan Biletler");
            System.out.println("0- Çıkış");
            System.out.print("Seçiminiz: ");
            int secim = scanner.nextInt();
            scanner.nextLine();

            if (secim == 0) {
                System.out.println("Çıkış yapılıyor...");
                break;
            }

            switch (secim) {
                case 1:
                    filmEkle();
                    break;
                case 2:
                    filmleriListele();
                    break;
                case 3:
                    musteriEkle();
                    break;
                case 4:
                    musterileriListele();
                    break;
                case 5:
                    biletSat();
                    break;
                case 6:
                    biletleriListele();
                    break;
                default:
                    System.out.println("Geçersiz giriş!");
            }
        }
    }

    private static void filmEkle() {
        if (filmSayisi >= 10) {
            System.out.println("Maksimum film eklenmiş!");
            return;
        }
        System.out.print("Film adı: ");
        filmler[filmSayisi] = scanner.nextLine();
        System.out.print("Film türü: ");
        filmTurleri[filmSayisi] = scanner.nextLine();
        System.out.print("Film süresi (dakika): ");
        filmSureleri[filmSayisi] = scanner.nextInt();
        scanner.nextLine();
        filmSayisi++;
        System.out.println("Film kaydedildi!");
    }

    private static void filmleriListele() {
        if (filmSayisi == 0) {
            System.out.println("Henüz film eklenmedi!");
            return;
        }
        for (int i = 0; i < filmSayisi; i++) {
            System.out.println((i + 1) + "- " + filmler[i] + " (" + filmTurleri[i] + ", " + filmSureleri[i] + " dk)");
        }
    }

    private static void musteriEkle() {
        if (musteriSayisi >= 20) {
            System.out.println("Maksimum müşteri eklenmiş!");
            return;
        }
        System.out.print("Müşteri adı: ");
        musteriler[musteriSayisi] = scanner.nextLine();
        System.out.print("Email: ");
        musteriemail[musteriSayisi] = scanner.nextLine();
        musteriSayisi++;
        System.out.println("Müşteri kaydedildi!");
    }

    private static void musterileriListele() {
        if (musteriSayisi == 0) {
            System.out.println("Henüz müşteri eklenmedi!");
            return;
        }
        for (int i = 0; i < musteriSayisi; i++) {
            System.out.println((i + 1) + "- " + musteriler[i] + " (" + musteriemail[i] + ")");
        }
    }

    private static void biletSat() {
        System.out.println("Müşteri seçin:");
        musterileriListele();
        System.out.print("Seçim: ");
        int musteriIndex = scanner.nextInt() - 1;
        
        System.out.println("Film seçin:");
        filmleriListele();
        System.out.print("Seçim: ");
        int filmIndex = scanner.nextInt() - 1;
        scanner.nextLine();

        if (musteriIndex < 0 || musteriIndex >= musteriSayisi || filmIndex < 0 || filmIndex >= filmSayisi) {
            System.out.println("Geçersiz seçim!");
            return;
        }

        biletler[musteriIndex][filmIndex] = 1;
        System.out.println("Bilet kaydedildi!");
    }

    private static void biletleriListele() {
        boolean biletVar = false;
        for (int i = 0; i < musteriSayisi; i++) {
            for (int j = 0; j < filmSayisi; j++) {
                if (biletler[i][j] == 1) {
                    System.out.println(musteriler[i] + " --> " + filmler[j]);
                    biletVar = true;
                }
            }
        }
        if (!biletVar) {
            System.out.println("Henüz satılmış bilet yok!");
        }
    }
}

