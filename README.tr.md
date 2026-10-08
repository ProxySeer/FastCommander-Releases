# FastCommander

Windows için hızlı **kopyalama, taşıma, aynalama (eşitleme), silme ve karşılaştırma** aracı. Gezgin sağ tık menüsü entegrasyonu da vardır.

**English:** [README.md](README.md)

## İndirme

**[Son sürümü indir](../../releases/latest)** (Windows 10/11, 64 bit, yaklaşık 80 MB)

1. Yukarıdaki bağlantıdan `FastCommander-...-win-x64.zip` dosyasını indirin.
2. Zip'i istediğiniz bir klasöre çıkarın.
3. `FastCommander.UI.exe` dosyasını çalıştırın. .NET kurmanıza gerek yok, uygulamanın içinde hazır gelir.

> Uygulama henüz kod imzalı değil. Windows SmartScreen ilk açılışta uyarı gösterebilir: **Daha fazla bilgi → Yine de çalıştır**.

## Özellikler

- **Kopyala, Taşı, Aynalama (Sync), Sil ve Kuru Deneme Karşılaştırması (Diff)** tek pencerede; iş kuyruğu, geçmiş, favori klasörler ve hız / kalan süre gösteren canlı ilerleme
- **İşlem sekmeleri:** Aktarım görünümünün üstündeki **+** düğmesi yeni bir Kopyala, Taşı, Eşitle, Karşılaştır veya Sil sekmesi açar. Her sekmenin kendi yolları, ayarları, ilerlemesi ve İptal düğmesi vardır ve tüm sekmeler aynı anda çalışır; yani bir işlem için diğerini beklemezsiniz. Sekme başlıkları "mod · kaynak → hedef" şeklindedir. Aynı sürücüdeki iki büyük kopyalama yavaşlarsa **Ayarlar → Genel → Aynı sürücüyü kullanan işlemler sırayla çalışsın** seçeneğini açın.
- **Hızlı kopyalama:** Büyük bir klasörde Windows kopyalamadan yaklaşık 18 kat hızlı, `robocopy /MT:16` ile aynı seviyede. Sayılar için [Hız](#hız) bölümüne bakın.
- **Büyük dosyalar** Windows önbelleğini doldurmayan bir Direct I/O hattıyla kopyalanır; iptal düğmesi her zaman çalışır. ReFS / Dev Drive birimlerinde dosyalar anında klonlanabilir.
- **Aynı sürücü içinde taşıma** yalnızca yeniden adlandırmadır, yani anlıktır.
- Büyük dosyalarda **zaman damgaları** ve NTFS alternatif veri akışları ("internetten indirildi" işareti gibi) korunur.
- **Üzerine yazma kuralları:** her zaman, sadece daha yeniyse, boyut veya tarih farklıysa ya da hiç.
- **Güvenlik:** Taşımada kaynak, hedef doğrulandıktan sonra silinir. Kilitli dosyalar atlanır ve klasörün geri kalanı kopyalanmaya devam eder. Silme ve eşitleme, salt okunur ve gizli dosyaları da işler.
- **Gezgin entegrasyonu:** Windows 11 modern sağ tık menüsü ve klasik menü; kopyalama, taşıma, yapıştırma, silme ve favori klasörlere yapıştırma. **Ayarlar → Genel** bölümünden açılır.
- **Komut satırı:** `FastCommander.UI.exe --cli --copy|-c <kaynak> <hedef>`, `--cli --move|-m`, `--cli --sync|-s`, `--cli --delete|-d <hedef>`.
- Türkçe ve İngilizce arayüz.

## Hız

Windows 11 çalışan tek bir bilgisayarda, kaynak ve hedef aynı SSD'deyken ve arka planda başka uygulamalar açıkken ölçüldü. Her araç aynı veriyi boş bir hedef klasöre kopyaladı ve araçların sırası turlar arasında değiştirildi. Her denemede kopyalanan dosya sayısı ve bayt miktarının aynı olduğu doğrulandı.

**14,3 GB klasör, 78.613 dosya**

| Araç | Süre | Hız |
|---|---|---|
| Windows kopyalama (Gezgin'in kopyalama motoru) | 859 sn (14 dk 19 sn), tek deneme | 17 MB/sn, 91 dosya/sn |
| `robocopy /MT:16` | 54,2 sn ve 50,5 sn, ortalama 52,4 sn | 280 MB/sn, 1.500 dosya/sn |
| **FastCommander** | 47,7 sn ve 44,8 sn, ortalama 46,3 sn | **317 MB/sn, 1.700 dosya/sn** |

FastCommander, Windows kopyalamadan yaklaşık 18 kat hızlıydı. `robocopy`'den yaklaşık %12 hızlıydı ve iki turu da önde bitirdi; ancak bu fark küçük olduğu için ikisini kabaca aynı seviyede sayın.

**8 GB tek dosya** (her araçla iki deneme)

| Araç | 1. deneme | 2. deneme | Ortalama |
|---|---|---|---|
| Windows kopyalama | 8,0 sn | 19,7 sn | 13,9 sn |
| `robocopy` | 8,3 sn | 17,2 sn | 12,8 sn |
| **FastCommander** | 4,2 sn | 6,7 sn | **5,5 sn** |

FastCommander iki turda da en hızlısıydı ve diğer ikisinden ortalama yaklaşık 2,5 kat hızlıydı. Tek dosya süreleri denemeden denemeye çok değişir (aynı dosya daha yoğun bir günde 20 saniyeden uzun sürmüştü), bu yüzden bunları kabaca bir fikir olarak alın.

**Notlar:** Tek bilgisayar, tek disk, tek klasör. "Windows kopyalama", Gezgin'in ilerleme penceresi olmadan çalıştırılan Windows kabuk kopyalama motorudur ve bunun için klasörde yalnızca bir deneme alabildim (aynı klasörün daha önce elle ölçülen Gezgin kopyası yaklaşık 400 sn sürmüştü; yani 6 ile 14 dakika arası bekleyin). HDD'ler, ağ paylaşımları ve çok farklı dosya boyutu karışımları denenmedi. Diskiniz, işlemciniz ve antivirüsünüz sonuçları değiştirir.

## Gereksinimler

- Windows 10 veya 11, 64 bit.
- Windows 11 modern sağ tık menüsü için **Geliştirici Modu** açık olmalıdır (Ayarlar → Sistem → Geliştiriciler). Kapalıysa uygulama sizi uyarır.

## Sağ tık menüsü

- **Modern menü** ve **klasik menü** aynı anda kurulamaz, çünkü her komut iki kez görünürdü. Modern menü kuruluyken klasik menü kaydı reddedilir.
- Her iki menüde de favori klasörleriniz "Favori: klasör adı" olarak listelenir.
- Eski bir sürümden güncelliyorsanız, eski pencereyi kapatın, yeni sürümü açın ve **Modern Menüyü Kaydet** düğmesine bir kez basarak menüyü yenileyin.

## Bilinen sınırlamalar

- 256 MB'tan küçük dosyalar tek parça kopyalanır; bu dosyalar dosya içinde ilerleme gösteremez ve tam ortasında iptal edilemez.
- Büyük bir kopyalamayı iptal ederseniz yarım yazılmış hedef dosya kalabilir.
- Farklı sürücüler arası taşıma ve ağ paylaşımları yeterince test edilmedi.

## Kaynak kodu

Kaynak kodu açık değildir. Bu depo yalnızca indirmeleri ve sürüm notlarını barındırır.
