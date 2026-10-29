
import matplotlib.pyplot as plt
from matplotlib_venn import venn2

# Dataset 1: minat mahasiswa
dataset1 = {
    "nama": "Dataset 1 - Minat Mahasiswa",
    "universe": {
        "Andi", "Budi", "Citra", "Dina", "Eko",
        "Fani", "Gilang", "Hani"
    },
    "A": {"Andi", "Budi", "Citra", "Dina"},
    "B": {"Citra", "Dina", "Eko", "Fani"}
}

# Dataset 2: kategori produk
dataset2 = {
    "nama": "Dataset 2 - Kategori Produk",
    "universe": {
        "Beras", "Gula", "Minyak", "Telur", "Tepung",
        "Kopi", "Teh", "Susu", "Garam"
    },
    "A": {"Beras", "Gula", "Minyak", "Tepung"},
    "B": {"Minyak", "Telur", "Tepung", "Kopi"}
}


def tampilkan_himpunan(U, A, B):
    print("\nHimpunan semesta (U):", sorted(U))
    print("Himpunan A:", sorted(A))
    print("Himpunan B:", sorted(B))


def operasi_himpunan(U, A, B):
    print("\n--- OPERASI HIMPUNAN ---")
    print("1. Union (A ∪ B)")
    print("2. Intersection (A ∩ B)")
    print("3. Difference (A - B)")
    print("4. Difference (B - A)")
    print("5. Complement A (Aᶜ)")
    print("6. Complement B (Bᶜ)")

    pilihan = input("Pilih operasi (1-6): ")

    if pilihan == "1":
        hasil = A | B
        nama = "A ∪ B (Union)"
    elif pilihan == "2":
        hasil = A & B
        nama = "A ∩ B (Intersection)"
    elif pilihan == "3":
        hasil = A - B
        nama = "A - B (Difference)"
    elif pilihan == "4":
        hasil = B - A
        nama = "B - A (Difference)"
    elif pilihan == "5":
        hasil = U - A
        nama = "A Complement"
    elif pilihan == "6":
        hasil = U - B
        nama = "B Complement"
    else:
        print("Pilihan tidak valid.")
        return

    print("\nHasil", nama, ":", sorted(hasil))
    print("Jumlah anggota:", len(hasil))


def tampilkan_venn(A, B, nama_dataset):
    plt.figure(figsize=(7, 6))
    venn2(
        [A, B],
        set_labels=("Himpunan A", "Himpunan B")
    )
    plt.title("Diagram Venn - " + nama_dataset)
    plt.tight_layout()
    plt.show()


def hitung_pie(A, B):
    jumlah_A = len(A)
    jumlah_B = len(B)
    irisan = len(A & B)
    gabungan = len(A | B)

    print("\n--- PRINSIP INKLUSI-EKSKLUSI ---")
    print("|A| =", jumlah_A)
    print("|B| =", jumlah_B)
    print("|A ∩ B| =", irisan)
    print("Rumus: |A ∪ B| = |A| + |B| - |A ∩ B|")
    print(
        f"Perhitungan: {jumlah_A} + {jumlah_B} - {irisan}"
        f" = {gabungan}"
    )
    print("Jumlah anggota unik:", gabungan)


def main():
    while True:
        print("\n==============================")
        print(" SISTEM KLASIFIKASI HIMPUNAN")
        print("==============================")
        print("1. Dataset 1 - Minat Mahasiswa")
        print("2. Dataset 2 - Kategori Produk")
        print("0. Keluar")

        pilihan = input("Pilih dataset: ")

        if pilihan == "0":
            print("Program selesai.")
            break
        elif pilihan == "1":
            data = dataset1
        elif pilihan == "2":
            data = dataset2
        else:
            print("Pilihan dataset tidak valid.")
            continue

        U = data["universe"]
        A = data["A"]
        B = data["B"]

        print("\n", data["nama"])
        tampilkan_himpunan(U, A, B)

        while True:
            print("\n--- MENU UTAMA ---")
            print("1. Operasi himpunan")
            print("2. Diagram Venn")
            print("3. Perhitungan PIE")
            print("4. Tampilkan semua fitur")
            print("0. Kembali ke pilihan dataset")

            menu = input("Pilih menu: ")

            if menu == "0":
                break
            elif menu == "1":
                operasi_himpunan(U, A, B)
            elif menu == "2":
                tampilkan_venn(A, B, data["nama"])
            elif menu == "3":
                hitung_pie(A, B)
            elif menu == "4":
                operasi_himpunan(U, A, B)
                tampilkan_venn(A, B, data["nama"])
                hitung_pie(A, B)
            else:
                print("Pilihan menu tidak valid.")


if __name__ == "__main__":
    main()
