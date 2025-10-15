# RTSP

RTSP, gerçek zamanlı akış protokolünün kısaltmasıdır, akışlı ortam sunucularını kontrol etmek için eğlence ve iletişim sistemlerinde kullanılmak üzere tasarlanmış bir ağ kontrol protokolüdür. 
Protokol, son noktalar arasında medya oturumları oluşturmak ve kontrol etmek için kullanılır. 
Yani, RTSP (Real-Time Streaming Protocol) internet üzerinden ses ve video gibi sürekli medya akışlarını (stream) kontrol etmek için tasarlanmış bir uygulama katmanı ağı protokolüdür.

RTSP'nin ana görevi, bir medya sunucusu (örneğin bir IP kamera veya bir video sunucusu) ile bir istemci (örneğin VLC Player, bir güvenlik yazılımı veya mobil uygulama) arasındaki akış oturumunu kurmak ve kontrol etmektir.

### RTSP, medya verisinin kendisini taşımaz; bu işi başka protokoller yapar:
| Protokol Adı | **Temel Görev** |  Basit Benzetme |
| :--- | :--- | :--- |
| **RTSP** | **Oturum Kontrolü ve Yönetimi** | Uzaktan Kumanda (PLAY, PAUSE, SETUP gibi komutları gönderir) |
| **RTP** | **Gerçek Zamanlı Veri İletimi** | Veri Taşıyıcı (Ses ve video paketlerini ağ üzerinde taşır) |
| **RTCP** | **Akış Kalitesi Geri Bildirimi** | Kalite Kontrolcü (Gecikme, veri kaybı ve senkronizasyon hakkında bilgi sağlar) |

Genellikle bir RTSP oturumu kurulduğunda, medya akışı RTP (Real-time Transport Protocol) üzerinden, genellikle UDP (User Datagram Protocol) kullanılarak taşınır. Bu, düşük gecikme (latency) için kritiktir.

RTSP, HTTP'ye (Web protokolü) benzer bir İstemci-Sunucu mimarisi kullanır, ancak HTTP durumsuz (stateless) iken, RTSP durumludur (stateful); yani oturumun durumunu (oynatılıyor, duraklatıldı gibi) takip eder.

### Temel RTSP Komutları (Metotları)

Bu komutlar, istemci ve sunucu arasında medya akışı oturumunu kontrol etmek için kullanılır.

| RTSP Komutu | **İşlevi / Amacı** | Detaylı Açıklama |
| :--- | :--- | :--- |
| **OPTIONS** | **Destek Kontrolü** | Sunucunun hangi RTSP komutlarını desteklediğini öğrenmek için kullanılır. |
| **DESCRIBE** | **Medya Bilgisi İsteği** | Akışın kodek, çözünürlük, port ve taşıma detaylarını içeren SDP (Session Description Protocol) dosyasını ister. |
| **SETUP** | **Oturumu Yapılandırma** | Akış için kullanılacak taşıma protokolünü (RTP/UDP veya RTP/TCP) ve istemci portlarını belirler. **PLAY** komutundan önce zorunludur. |
| **PLAY** | **Akışı Başlatma** | Sunucuya, **SETUP** ile belirlenen parametreler üzerinden medya akışını göndermeye başlamasını emreder. |
| **PAUSE** | **Akışı Duraklatma** | Medya akışını geçici olarak durdurur. |
| **TEARDOWN** | **Oturumu Sonlandırma** | Akışı durdurur ve sunucudaki oturum için ayrılan tüm kaynakları serbest bırakır. |
| **RECORD** | **Kaydı Başlatma** | Akışın yönünü istemciden sunucuya doğru ayarlayarak, bir kayıt oturumunu başlatır. |
