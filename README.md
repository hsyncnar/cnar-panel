# CNAR LLC · Maventa Home — Ortak Panel

Hüseyin Çınar ve Mustafa Ertuğrul'un ortak çalışma paneli.

**Canlı adres:** https://hsyncnar.github.io/cnar-panel/
**Giriş şifresi:** `3416`
**Sürüm:** v3.0 — "Komuta Merkezi"

---

## Bölümler

| Bölüm | Ne yapar |
|---|---|
| **Özet** | Kim çevrimiçi, bugünkü süre, açık görevler, kritik stok, yaklaşan etkinlikler, son mesajlar ve hareketler |
| **Sohbet** | İkiniz arasında canlı mesajlaşma; okunmamış rozeti ve tarayıcı bildirimi |
| **Görevler** | Kim neyi üstlendi — bekliyor / devam ediyor / bitti |
| **Takvim** | Alım günleri, ödemeler, kargo, kampanyalar; yaklaşanlar Özet'e düşer |
| **Mağazalar** | Amazon Seller, Trendyol Satıcı Paneli, Hepsiburada Merchant linkleri + ortak notlar |
| **Stok & Satış** | Ürün bazlı stok, günlük satış hızı, kaç günlük stok kaldığı, kritik seviye uyarıları |
| **Alım Planı** | Aylık düzenli stoklu alımın planlanması |
| **Alım Raporu** | Excel'den gelen 29 alımın maliyet/kâr grafikleri ve ürün kırılımı |
| **Kâr Hesaplayıcı** | Yeni ürün için kâr/marj simülasyonu, canlı kur, kayıtlı senaryolar |
| **Aktivite** | Giriş kayıtları, kişi başı toplam süre ve oturum sayıları |

Üst çubukta canlı USD/CAD kuru, İstanbul hava durumu, tarih-saat ve kimin çevrimiçi
olduğunu gösteren avatarlar bulunur.

## Yetkiler

`AYARLAR` bölümündeki `role` alanı belirler:

- `admin` → her şeyi düzenleyebilir (şu an: Hüseyin)
- `viewer` → görüntüler, mesaj yazabilir, düzenleyemez (şu an: Mustafa)

Mustafa'ya da düzenleme yetkisi vermek için `role` değerini `'admin'` yapmanız yeterli.

## Tema

07:00–19:00 arası otomatik aydınlık, dışında karanlık (İstanbul saati).
Sol alttaki güneş/ay simgesiyle elle de değiştirilebilir; seçim hatırlanır.

## Bildirimler

Sol alttaki zil simgesine bir kez basıp izin verirseniz, sekme arkadayken
yeni mesaj geldiğinde ve karşı taraf panele girdiğinde bildirim alırsınız.

## Ortak veritabanı

Firebase (Firestore) bağlantısı dosyaya gömülüdür — linke giren herkes otomatik
olarak aynı veritabanına bağlanır, kimsenin bir ayar yapmasına gerek yoktur.
Sol alttaki rozet **Ortak veritabanı bağlı** yazıyorsa her şey yolundadır.

> Firestore kuralları `allow read, write: if true` olduğu için adresi bilen biri
> teorik olarak veriye erişebilir. Panelde fatura, banka veya müşteri bilgisi tutmayın.

## Siteyi değiştirmek

Her şey tek bir `index.html` dosyasında. GitHub'da dosyaya tıklayıp kalem (✏️)
simgesiyle düzenleyip commit'lerseniz 1–2 dakikada canlıya yansır.
Dosya içi bölümler yorum satırlarıyla ayrılmıştır:

`1) AYARLAR` · `2) PROFİL FOTOĞRAFLARI` · `3) VERİ KATMANI` · `4) ÇEKİRDEK`
`5) SOHBET` · `6) KÂR HESAPLAYICI` · `7) TAKVİM` · `8) STOK & ALIM PLANI`
`9) ALIM VERİSİ` · `10) ALIM RAPORU`

Renkler `<style>` bloğunun en üstündeki `:root` değişkenlerinde.

### Şifreyi değiştirmek

Tarayıcı konsolunda çalıştırın, çıkan değeri `pinHash`'e yapıştırın:

```js
crypto.subtle.digest('SHA-256', new TextEncoder().encode('1234'))
  .then(b => console.log([...new Uint8Array(b)].map(x => x.toString(16).padStart(2,'0')).join('')))
```

## Güncelleme e-postası

`site-guncelleme-maili.yml` dosyasını repoda `.github/workflows/` klasörüne koyup
`MAIL_USERNAME` ve `MAIL_PASSWORD` secret'larını tanımlarsanız, her güncellemede
dört adrese otomatik bilgilendirme maili gider. Adımlar dosyanın en üstünde yazılı.

## Güvenlik hakkında not

Statik bir site olduğu için şifre kontrolü tarayıcıda yapılır. Adresi bilmeyen
kimse giremez, ancak teknik bilgisi olan biri sayfa kaynağını inceleyebilir.
Hassas finansal veri tutmayın; gerçek koruma gerekirse Firebase Authentication eklenebilir.
