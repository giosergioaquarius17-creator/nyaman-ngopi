import os

# --- KONSTANTA & KONFIGURASI ---
COLORS = {
    "NAVY_BG": "\033[48;5;18m",
    "WHITE_TEXT": "\033[38;5;15m",
    "BOLD": "\033[1m",
    "GREEN": "\033[92m",
    "RED": "\033[91m",
    "RESET": "\033[0m"
}

MENU = {
    "Kopi Hitam": 15000,
    "Kopi Latte": 20000,
    "Teh Hijau": 12000,
    "Cappuccino": 25000,
    "Croissant": 18000,
    "Donat": 10000,
    "Salad": 22000,
    "Sandwich": 30000
}

# --- FUNGSI PENDUKUNG ---
def bersihkan_layar():
    os.system('cls' if os.name == 'nt' else 'clear')

def format_rupiah(angka):
    return f"Rp{angka:>7,}".replace(",", ".")

def cetak_header(judul):
    print(f"{COLORS['NAVY_BG']}{COLORS['WHITE_TEXT']}{COLORS['BOLD']}")
    print("=" * 35)
    print(f"{judul:^35}")
    print("=" * 35 + COLORS['RESET'])

# --- LOGIKA UTAMA ---
def tampilkan_menu():
    cetak_header("MENU KAFE DIGITAL")
    print(f"{COLORS['NAVY_BG']}{COLORS['WHITE_TEXT']}")
    for item, harga in MENU.items():
        print(f"  {item:<20} : {format_rupiah(harga)}")
    print("=" * 35 + COLORS['RESET'])

def cetak_struk(pesanan):
    bersihkan_layar()
    if not pesanan:
        print(f"{COLORS['RED']}Tidak ada pesanan yang dibuat.{COLORS['RESET']}")
        return

    total = sum(MENU[item] for item in pesanan)
    cetak_header("STRUK PESANAN")
    print(f"{COLORS['NAVY_BG']}{COLORS['WHITE_TEXT']}")
    
    # Menghitung jumlah per item unik agar struk lebih rapi
    for item in set(pesanan):
        qty = pesanan.count(item)
        subtotal = MENU[item] * qty
        print(f"  {item:<15} x{qty:<2} : {format_rupiah(subtotal)}")
    
    print("-" * 35)
    print(f"  {COLORS['BOLD']}{'TOTAL':<18} : {format_rupiah(total)}{COLORS['RESET']}{COLORS['NAVY_BG']}{COLORS['WHITE_TEXT']}")
    print("=" * 35)
    print(f"{'Terima Kasih Atas Kunjungan Anda':^35}")
    print("=" * 35 + COLORS['RESET'])

def main():
    keranjang = []
    
    while True:
        bersihkan_layar()
        tampilkan_menu()
        
        print(f"\n{COLORS['BOLD']}Ketik 'selesai' untuk checkout.{COLORS['RESET']}")
        pilihan = input("🛒 Pilih menu: ").strip()

        if pilihan.lower() == 'selesai':
            break
        
        # Pencarian item (Case-Insensitive)
        item_ditemukan = next((k for k in MENU if k.lower() == pilihan.lower()), None)
        
        if item_ditemukan:
            keranjang.append(item_ditemukan)
            print(f"{COLORS['GREEN']}✅ {item_ditemukan} berhasil ditambahkan!{COLORS['RESET']}")
        else:
            print(f"{COLORS['RED']}❌ Menu '{pilihan}' tidak tersedia.{COLORS['RESET']}")
        
        input("\nTekan Enter untuk melanjutkan...")

    cetak_struk(keranjang)

if __name__ == "__main__":
    try:
        main()
    except KeyboardInterrupt:
        print("\nProgram ditutup.")
