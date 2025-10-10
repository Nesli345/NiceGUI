# NiceGUI
NiceGUI, tarayıcıda çalışan grafiksel kullanıcı arayüzleri yazmak için açık kaynaklı bir Python kütüphanesidir.

Python kodu yazarak web uygulaması, dashboard, kontrol paneli veya veri görselleştirme arayüzü oluşturabilirsin.
Yani HTML, CSS, JavaScript yazmana gerek kalmadan, sadece Python ile görsel arayüz geliştirirsin.

NiceGUI'nin en büyük çekiciliği, tüm arayüzün Python koduyla tanımlanması ve arka plandaki tüm web teknolojilerinin sizin için yönetilmesidir. Bir web geliştiricisi olmanıza gerek kalmadan etkileşimli panolar, küçük araçlar, IoT çözümleri veya makine öğrenimi arayüzleri oluşturabilirsiniz.


### NiceGUI, arka planda üç ana teknolojiyi birleştirir:

#### 1- FastAPI: 
Uygulamanın arka yüzünü (backend) oluşturur ve web sunucusu işlevlerini yerine getirir. Bu, NiceGUI'nin yüksek performanslı ve modern bir yapıya sahip olmasını sağlar.

#### 2- Vue / Quasar: 
Ön yüz (frontend) için Vue.js çatısını ve bunun üzerine kurulu bir UI bileşen kütüphanesi olan Quasar'ı kullanır. Bu sayede uygulamalarınız modern, esnek ve "Material Design" görünümlü olur.

#### 3- WebSockets: 
Tarayıcı (istemci) ve sunucu (Python kodu) arasındaki gerçek zamanlı iletişimi sağlar. Bir butona tıkladığınızda veya bir veri güncellendiğinde, arayüz otomatik olarak ve anında tepki verir.

## Kurulum
Öncelikle, çalışmak istediğiniz projenin sanal ortamını (venv) terminalde etkinleştirin. (PyCharm'ın kendi terminali bunu genellikle otomatik yapar).

Ortam etkinleştirildikten sonra, aşağıdaki standart pip komutunu çalıştırın:


```bash
pip install nicegui
```

#### Docker Kullancaksanız;
-Projenizin ana dizininde bir Dockerfile oluşturun ve içine şunları yazın:

```Dockerfile
# Resmi Python imajını temel alır
FROM python:3.11-slim

# Gerekli bağımlılıkları kurar
RUN pip install nicegui

# Çalışma dizinini ayarlar
WORKDIR /app

# Kodunuzu Docker imajına kopyalar
COPY app.py .

# Uygulamanın çalışacağı portu açar (Varsayılan NiceGUI portu 8080'dir)
EXPOSE 8080

# Uygulamayı çalıştırır
CMD ["python", "app.py"]

```
-Terminalde, Dockerfile'ın bulunduğu dizinde aşağıdaki komutu çalıştırın:
```bash
docker build -t benim-nicegui-uygulamam .
```
-Uygulamayı 8080 portunda çalıştırın:

```bash
docker run -d -p 8080:8080 benim-nicegui-uygulamam
```

-Artık uygulamanıza web tarayıcınızdan http://localhost:8080 adresi üzerinden erişebilirsiniz.

#### ⚡Basit bir örnek
```python
from nicegui import ui

ui.label('Merhaba NiceGUI!')
ui.run()
```
Bu kodu çalıştırınca terminalde şöyle bir çıktı alırsın:
```nginx
NiceGUI running on http://localhost:8080
```
Tarayıcıda bu adrese gidince “Merhaba NiceGUI!” yazan bir sayfa görürsün.

#### 🧩 Temel Kullanım Mantığı
NiceGUI tamamen "declarative" (bildirimsel) bir yapıdadır. Yani HTML elementlerini Python komutlarıyla “tanımlarsın”.
```python
from nicegui import ui

ui.label('Hoş geldiniz!')
ui.button('Tıklayın', on_click=lambda: ui.notify('Butona tıkladınız!'))

ui.run()
```
#### Başlıca Widgetler
| Eleman | Kullanım |
| :--- | :--- |
| `ui.label('Metin')` | Yazı etiketi |
| `ui.button('Kaydet', on_click=...)` | Buton |
| `ui.input('Adınızı girin')` | Metin girişi |
| `ui.slider(min=0, max=100)` | Slider |
| `ui.checkbox('Onaylıyorum')` | Onay kutusu |
| `ui.select(['A', 'B', 'C'])` | Seçim kutusu |
| `ui.card()` | Kart tasarımı |
| `ui.table()` | Tablo görüntüleme |
| `ui.plot()` | Grafik çizimi (Plotly veya Matplotlib ile) |

#### Birden fazla sayfa (route) oluşturmak
```python
from nicegui import ui

@ui.page('/')
def ana_sayfa():
    ui.label('Burası ana sayfa')
    ui.link('Grafik sayfasına git', '/grafik')

@ui.page('/grafik')
def grafik_sayfasi():
    ui.label('Veri Grafiği')
    ui.button('Geri dön', on_click=lambda: ui.open('/'))

ui.run()
```










