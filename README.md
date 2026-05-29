# Pearl Miner Rehberi !

Bu rehber [AlphaMiner](https://github.com/AlphaMine-Tech/alpha-miner) ile AlphaPool üzerinden Pearl (PRL) kazımı içindir. Bu yöntemi kullanma sebebimiz, resmi full node / vLLM miner tarafında H100/H200 gibi pahalı cihazlara ihtiyaç duyulabilmesi ve bunun herkes için ulaşılabilir olmamasıdır. Bu rehber, kullanmadığınız veya içinde önemli bilgiler bulundurmadığınız cihazlarla Pearl mining denemek isteyenler içindir.

Güvenlik açısından miner’a sadece public Pearl cüzdan adresi verilir. Private key, seed phrase veya cüzdan şifresi kesinlikle kullanılmaz. Mümkünse ana cihaz yerine WSL2 Ubuntu, boş/ikinci cihaz veya cloud sunucu kullanmanız daha sağlıklı olur. Amaç, cihazınızdaki GPU’yu AlphaPool’a bağlayarak PRL kazımı yapmak. 3060/3070 gibi kartlarla günlük 4-5 dolar bile gelir oluşursa, cihaz boşta duracağına değerlendirilebilir. Kazanç PRL fiyatına, pool performansına ve elektrik/cloud maliyetine göre değişir.

---

## Havuz Komisyon Ücreti:

- Pool kesintisi: `%5`
- Miner geliştirici kesintisi: `%1`
- Toplam kesinti: yaklaşık `%6`

Bu kesintiler kazımdan otomatik alınır.

`%5` pool kesintisi, AlphaPool’un sistemi çalıştırması ve ödülleri madencilere dağıtması için alınır. `%1` dev fee ise `alpha-miner` geliştiricilerine gider. Yani miner’ın geliştirilmesi, güncellenmesi ve yeni ekran kartlarına destek eklenmesi için alınır.

- Ödeme sistemi: PPLNS
- Minimum ödeme: `0.5 PRL`
- Ödeme aralığı: yaklaşık her `4 saat`

PPLNS basitçe şu demek: Pool’a ne kadar katkı sağlarsan, ödülden o oranda pay alırsın.

---

## Gerekenler:

- NVIDIA ekran kartı lazım. RTX 30/40/50 serisi olur.
- Windows kullanıyorsan [WSL](https://github.com/UfukNode/WSL-Kurulum) Ubuntu kurman gerekiyor.
- Linux veya cloud Ubuntu kullanıyorsan direkt kurabilirsin.
- Ekran kartı driver’ın kurulu olmalı.

Kontrol:

```bash
nvidia-smi
```

GPU örnekleri:

<img width="1257" height="455" alt="image" src="https://github.com/user-attachments/assets/2abe9418-6ef8-4c53-930f-b07851eb8f36" />

---

## 1. Pearl cüzdan adresi al:

- Wallet: https://compute.pearlresearch.ai bağlantıya git ve kayıt ol.
- "My Wallet" kısmına geç ve "orl1p" ile başlayan adresini kaydet.

Adres örneği:
```text
prl1p...
```

---

## 2. Gerekli Paketleri Kur:

```bash
sudo apt update && sudo apt install -y curl screen ca-certificates
```

---

## 3. alpha-miner indir:

```bash
curl -sSL https://raw.githubusercontent.com/AlphaMine-Tech/alpha-miner/main/install.sh | bash
cd ~/alpha-miner
```

---

## 4. Pool bölgesi seç

En düşük gecikme için sana yakın endpoint seç.

```text
Europe:          eu1.alphapool.tech:5566 veya eu2.alphapool.tech:5566
North America:   us1.alphapool.tech:5566 veya us2.alphapool.tech:5566
Asia:            sg1.alphapool.tech:5566
Russia/Eurasia:  ru1.alphapool.tech:5566
```

Türkiye için genelde önce `eu1.alphapool.tech:5566` denenir.

---

## 5. Miner'ı screen içinde başlat

- `PRL_ADDRESS` yerine kendi Pearl adresini yaz.

```bash
screen -S alpha-pearl
```
```bash
cd ~/alpha-miner
```

```bash
./alpha-miner \
  --pool stratum+tcp://eu1.alphapool.tech:5566 \
  --address PRL_ADDRESS \
  --worker $(hostname)
```

📌 Eğer kendi cihazınıza kurmayıp avrupa dışı lokasyonlar kullanırsanız komuttak "eu1.alphapool.tech:5566" kısmını 4. adımdaki pool bölgesine göre değiştirebilirsiniz.

---

## 6. Screen Komutları:

Screen'den çıkmak:

```text
Ctrl+A, sonra D
```

Geri dönmek:

```bash
screen -r alpha-pearl
```

Durdurmak:

```text
Ctrl+C
```

---

## 7. Kazancı takip et

- https://pearl.alphapool.tech/#dashboard bağlantıya git.
- Aşağıya in ve "Look up your miner" kısmına yukarıda oluşturduğun wallet adresini gir.

✅ Bu şekilde aktif minerlarını ve ne kadar $PRL kazandığın gibi birçok bilgiyi görebilirsin.

---

# ⚠️Güvenlik notları !

- Bu resmi Pearl repo miner'ı değil, third-party AlphaPool miner'ıdır.
- Sadece public wallet adresi verilir; seed phrase/private key verilmez.
- Mümkünse root yerine ayrı bir Linux kullanıcısı ile çalıştır.
- Binary'yi sadece AlphaMine GitHub release veya AlphaPool sayfasından indir.
- Her güncellemede `sha256sum alpha-miner` ile hash'i kontrol et.
- Cihazında şüpheli durum görürsen miner'ı durdur, binary'yi sil, Windows/WSL ve startup/scheduled task kontrollerini yap.

---

## Linkler

- AlphaPool Pearl: https://pearl.alphapool.tech
- AlphaPool ana sayfa: https://www.alphapool.tech
- AlphaMiner GitHub: https://github.com/AlphaMine-Tech/alpha-miner
- Pearl Explorer: https://explorer.pearlresearch.ai
- Pearl Dashboard: https://compute.pearlresearch.ai/dashboard
