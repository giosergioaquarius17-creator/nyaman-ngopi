import os

# Definisi Warna (ANSI Escape Codes)
BG_NAVY = "\033[48;5;18m"  # Background Biru Dongker
TEXT_WHITE = "\033[38;5;15m" # Teks Putih
BOLD = "\033[1m"
RESET = "\033[0m"

# Menu kafe
menu = {
    "Kopi Hitam": 15000,
    "Kopi Latte": 20000,
    "Teh Hijau": 12000,
    "Cappuccino": 25000,
    "Croissant": 18000,
    "Donat": 10000,
    "Salad": 22000,
    "Sandwich": 30000
}

def bersihkan_layar():
    os.system('cls' if os.name == 'nt' else 'clear')

def tampilkan_menu():
    print(f"{BG_NAVY}{TEXT_WHITE}{BOLD}")
    print("=" * 30)
    print(f"{'MENU KAFE DIGITAL':^30}")
    print("=" * 30 + RESET)
    print(f"{BG_NAVY}{TEXT_WHITE}")
    for item, harga in menu.items():
        # Mengatur format agar harga sejajar di kanan
        print(f" {item:<15} : Rp{harga:>7,}")
    print("=" * 30 + RESET)

def main():
    pesanan_user = []
    
    while True:
        bersihkan_layar()
        tampilkan_menu()
        
        print(f"\n{BOLD}Ketik 'selesai' untuk melihat struk.{RESET}")
        pilihan = input("Masukkan nama item: ").strip()

        if pilihan.lower() == 'selesai':
            break
        
        # Pencarian item (case-insensitive)
        item_ditemukan = next((k for k in menu if k.lower() == pilihan.lower()), None)
        
        if item_ditemukan:
            pesanan_user.append(item_ditemukan)
            print(f"✅ {item_ditemukan} ditambahkan!")
        else:
            print(f"❌ Item '{pilihan}' tidak ada di menu.")
        
        input("\nTekan Enter untuk lanjut...")

    # Cetak Struk
    bersihkan_layar()
    if pesanan_user:
        total = sum(menu[item] for item in pesanan_user)
        
        print(f"{BG_NAVY}{TEXT_WHITE}{BOLD}")
        print("=" * 30)
        print(f"{'STRUK PESANAN':^30}")
        print("=" * 30 + RESET)
        print(f"{BG_NAVY}{TEXT_WHITE}")
        
        for item in pesanan_user:
            print(f" {item:<15} : Rp{menu[item]:>7,}")
            
        print("-" * 30)
        print(f" {BOLD}{'TOTAL':<15} : Rp{total:>7,}{RESET}{BG_NAVY}{TEXT_WHITE}")
        print("=" * 30)
        print(f"{'Terima Kasih!':^30}")
        print("=" * 30 + RESET)
    else:
        print("Tidak ada pesanan yang dibuat.")

if __name__ == "__main__":
    main()
