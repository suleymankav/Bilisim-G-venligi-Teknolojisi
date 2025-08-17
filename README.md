import random
from textwrap import dedent

# ----- Soru bankası -----
SORULAR = [
    {
        "soru": "Malazgirt Meydan Muharebesi hangi yılda olmuştur?",
        "secenekler": ["1048", "1071", "1176", "1453"],
        "dogru": "1071",
        "aciklama": "26 Ağustos 1071'de Alparslan, Bizans'a karşı zafer kazandı."
    },
    {
        "soru": "İstanbul’un Fethi hangi yılda gerçekleşmiştir?",
        "secenekler": ["1453", "1071", "1402", "1517"],
        "dogru": "1453",
        "aciklama": "29 Mayıs 1453'te II. Mehmed şehri fethederek çağ açıp çağ kapattı."
    },
    {
        "soru": "Türkiye Cumhuriyeti hangi tarihte ilan edildi?",
        "secenekler": ["23 Nisan 1920", "29 Ekim 1923", "19 Mayıs 1919", "24 Temmuz 1923"],
        "dogru": "29 Ekim 1923",
        "aciklama": "Büyük Millet Meclisi’nin kararıyla cumhuriyet ilan edildi."
    },
    {
        "soru": "Türkiye Büyük Millet Meclisi’nin açılış tarihi nedir?",
        "secenekler": ["23 Nisan 1920", "29 Ekim 1923", "24 Temmuz 1923", "10 Ağustos 1920"],
        "dogru": "23 Nisan 1920",
        "aciklama": "TBMM işgale karşı milli iradeyi temsil etmek üzere açıldı."
    },
    {
        "soru": "Mustafa Kemal Atatürk’ün Samsun’a çıkışı hangi tarihtedir?",
        "secenekler": ["19 Mayıs 1919", "29 Ekim 1923", "30 Ağustos 1922", "18 Mart 1915"],
        "dogru": "19 Mayıs 1919",
        "aciklama": "Milli Mücadele’nin başlangıcı kabul edilir."
    },
    {
        "soru": "Lozan Barış Antlaşması hangi tarihte imzalanmıştır?",
        "secenekler": ["24 Temmuz 1923", "10 Ağustos 1920", "30 Ekim 1918", "28 Haziran 1919"],
        "dogru": "24 Temmuz 1923",
        "aciklama": "Türkiye’nin uluslararası alanda tanınmasını sağlayan barış antlaşmasıdır."
    },
    {
        "soru": "Sevr Antlaşması’nın tarihi nedir?",
        "secenekler": ["10 Ağustos 1920", "24 Temmuz 1923", "30 Ekim 1918", "28 Haziran 1919"],
        "dogru": "10 Ağustos 1920",
        "aciklama": "Osmanlı’ya ağır hükümler getiren ve uygulanamayan antlaşmadır."
    },
    {
        "soru": "Magna Carta hangi yılda imzalanmıştır?",
        "secenekler": ["1066", "1215", "1492", "1649"],
        "dogru": "1215",
        "aciklama": "İngiltere’de kralın yetkilerini sınırlayan sözleşme."
    },
    {
        "soru": "Fransız İhtilali hangi yılda başlamıştır?",
        "secenekler": ["1776", "1789", "1815", "1848"],
        "dogru": "1789",
        "aciklama": "Bastille’in basılmasıyla devrim ateşi başladı."
    },
    {
        "soru": "İkinci Dünya Savaşı hangi yıl başladı?",
        "secenekler": ["1937", "1938", "1939", "1941"],
        "dogru": "1939",
        "aciklama": "1 Eylül 1939’da Almanya’nın Polonya’yı işgaliyle."
    },
    {
        "soru": "Apollo 11’in Ay’a inişi hangi yıldadır?",
        "secenekler": ["1961", "1969", "1972", "1957"],
        "dogru": "1969",
        "aciklama": "20 Temmuz 1969: Neil Armstrong ve Buzz Aldrin Ay yüzeyine indi."
    },
    {
        "soru": "Berlin Duvarı’nın yıkılışı hangi yıldadır?",
        "secenekler": ["1987", "1989", "1991", "1993"],
        "dogru": "1989",
        "aciklama": "9 Kasım 1989’da sınır kapıları açıldı, duvarın yıkımı başladı."
    },
    {
        "soru": "Osmanlı Devleti’nin kuruluşu geleneksel olarak hangi yıla tarihlenir?",
        "secenekler": ["1071", "1299", "1302", "1453"],
        "dogru": "1299",
        "aciklama": "Geleneksel kabul 1299’dur; 1302 Koyunhisar Savaşı da önemli eştir."
    },
    {
        "soru": "Tanzimat Fermanı hangi yıl ilan edildi?",
        "secenekler": ["1826", "1839", "1856", "1876"],
        "dogru": "1839",
        "aciklama": "3 Kasım 1839’da Gülhane Hatt-ı Hümayunu ilan edildi."
    },
    {
        "soru": "Çanakkale Deniz Zaferi’nin tarihi hangisidir?",
        "secenekler": ["18 Mart 1915", "25 Nisan 1915", "30 Ağustos 1922", "9 Eylül 1922"],
        "dogru": "18 Mart 1915",
        "aciklama": "İtilaf donanmasının boğazı geçmesi engellendi."
    }
]

def karistir_secnekler(secenekler):
    # Şıkları karıştırıp harflerle eşleştirir
    karisik = secenekler[:]
    random.shuffle(karisik)
    harfler = "ABCD"
    return {harf: karisik[i] for i, harf in enumerate(harfler)}

def soru_sor(kayit, numara):
    print(f"\nSoru {numara}: {kayit['soru']}")
    harf_map = karistir_secnekler(kayit["secenekler"])
    for harf, metin in harf_map.items():
        print(f"  {harf}) {metin}")

    # Geçerli giriş al
    while True:
        cevap = input("Cevabınız (A/B/C/D): ").strip().upper()
        if cevap in ("A", "B", "C", "D"):
            break
        print("Lütfen A, B, C veya D giriniz.")

    kullanici_cevap = harf_map[cevap]
    dogru_mu = (kullanici_cevap == kayit["dogru"])

    if dogru_mu:
        print("✅ Doğru!")
    else:
        # Doğru şıkkı bul
        dogru_harf = next(h for h, v in harf_map.items() if v == kayit["dogru"])
        print(f"❌ Yanlış. Doğru cevap: {dogru_harf}) {kayit['dogru']}")

    print(f"Bilgi: {kayit['aciklama']}")
    return 1 if dogru_mu else 0

def ozet(durum):
    toplam = durum["toplam"]
    dogru = durum["dogru"]
    yanlis = toplam - dogru
    yuzde = (dogru / toplam) * 100 if toplam else 0
    print("\n" + "="*48)
    print("YARIŞMA BİTTİ • Sonuçlar")
    print("-"*48)
    print(f"Toplam Soru : {toplam}")
    print(f"Doğru       : {dogru}")
    print(f"Yanlış      : {yanlis}")
    print(f"Başarı      : %{yuzde:.1f}")
    print("="*48)

def giris_metni():
    print(dedent("""
    ╔══════════════════════════════════════════════╗
    ║       TARİH BİLGİ YARIŞMASI (Python)         ║
    ╚══════════════════════════════════════════════╝
    Kurallar:
    • Sorular ve şıklar karıştırılır.
    • Cevaplar A/B/C/D olarak girilir.
    • Her sorudan sonra kısa bir açıklama verilir.
    """))

def main():
    random.seed()  # rastgelelik
    giris_metni()

    # Kaç soru istendiğini sor (maksimum mevcut soru sayısı)
    maks = len(SORULAR)
    try:
        adet_str = input(f"Kaç soru ile oynansın? (1-{maks}, Enter=10): ").strip()
        adet = int(adet_str) if adet_str else 10
    except ValueError:
        adet = 10
    adet = max(1, min(adet, maks))

    secilenler = random.sample(SORULAR, adet)
    skor = 0
    for i, kayit in enumerate(secilenler, start=1):
        skor += soru_sor(kayit, i)

    ozet({"toplam": adet, "dogru": skor})
    print("\nOyun bitti. Tekrar oynamak için programı yeniden çalıştırın.")

if __name__ == "__main__":
    main()
