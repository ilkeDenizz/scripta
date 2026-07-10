# Cookie Clicker Sürümü 🍪

<img src="img/perfectCookie.png" width="128">

Orijinal oyun şu adreste bulunabilir: [http://orteil.dashnet.org/cookieclicker/](http://orteil.dashnet.org/cookieclicker/)

Bu sürüm (mirror), tamamen **eğitim amaçlıdır**. İster çevrimdışı ortamda kodları incelemek için kullanın, isterseniz de kendi web sitenize entegre edip oynayın! 🚀

---

## 🔄 Oyunu Nasıl Güncellerim?

Eğer orijinal oyuna yeni bir güncelleme gelirse, kendi repodaki dosyalarını şu Linux terminal komutlarıyla kolayca güncelleyebilirsin:

### 1. Yeni Görselleri Çekme (Images) 🖼️
Ana dizinde terminali açıp öncelikle User-Agent ayarını yap:
* `USER="Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.0.0 Safari/537.36"`

Ardından şu komutları sırasıyla çalıştır:
* `cd img/`
* `wget --user-agent="$USER" --convert-links -O index.html http://orteil.dashnet.org/cookieclicker/img/`
* `grep -v PARENTDIR index.html | grep '\[IMG' | grep -Po 'a href="\K.*?(?=")' | sed 's/\?.*//' > _imglist.txt`
* `wget --user-agent="$USER" -N -i _imglist.txt -B http://orteil.dashnet.org/cookieclicker/img/`

### 2. Yeni Sesleri Çekme (Sounds) 🎵
Ana dizine dön ve şu komutları gir:
* `cd snd/`
* `wget --user-agent="$USER" --convert-links -O index.html http://orteil.dashnet.org/cookieclicker/snd/`
* `grep -v PARENTDIR index.html | grep '\[SND' | grep -Po 'a href="\K.*?(?=")' | sed 's/\?.*//' > _sndlist.txt`
* `wget --user-agent="$USER" -N -i _sndlist.txt -B http://orteil.dashnet.org/cookieclicker/snd/`

### 3. Yeni Çevirileri Çekme (Translations) 🌍
Ana dizine dön ve dil dosyaları için şunları çalıştır:
* `cd loc/`
* `wget --user-agent="$USER" --convert-links -O index.html http://orteil.dashnet.org/cookieclicker/loc/`
* `grep -v PARENTDIR index.html | grep '\[TXT' | grep -Po 'a href="\K.*?(?=")' | sed 's/\?.*//' > _loclist.txt`
* `wget --user-agent="$USER" -i _loclist.txt http://orteil.dashnet.org/cookieclicker/loc/`

### 4. `js`, `html`, `css` ve Fontları Çekme ⚙️
Ana dizinden oyunun omurgasını oluşturan dosyaları güncellemek için:
* Güncel `index.html` dosyasını çek: `wget --user-agent="$USER" -O index.html http://orteil.dashnet.org/cookieclicker/` 
* Güncel `style.css` dosyasını çek: `wget --user-agent="$USER" -O style.css http://orteil.dashnet.org/cookieclicker/style.css`
* Güncel `js` dosyalarını çek: `wget --user-agent="$USER" -i _jslist.txt -B http://orteil.dashnet.org/cookieclicker/`
* Font URL'lerini `index.html`'den çıkar: `grep -Po 'url\(\K/cf-fonts/[^)]+' index.html > _fontlist.txt`
* Fontları indir: `wget --user-agent="$USER" -x -nH -N -i _fontlist.txt -B http://orteil.dashnet.org`

### 5. `js` ve `html` Dosyalarını Düzeltme 🛠️
* `index.html` içinde yeni bir `<script src` kodu var mı veya `main.js` içinde yeni bir yerel javascript dosyası eklenmiş mi kontrol et (örneğin `Game.last.minigameUrl`). Yeni scriptler varsa, `_jslist.txt` dosyanı buna göre güncelle.
* `main.js` içindeki çalışmayan veri URL'sini bul: `DataDir=window.location.origin+'/data/';` ve bunu şu şekilde değiştir: `DataDir='https://orteil.dashnet.org/data/';`
* Son olarak `index.html` içindeki font URL'lerini yerel (local) çalışacak şekilde şu komutla düzelt: `sed -i 's|url(/cf-fonts/|url(cf-fonts/|g' index.html`
