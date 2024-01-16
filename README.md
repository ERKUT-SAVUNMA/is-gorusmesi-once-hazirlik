<p align="center">
  <img src="https://www.erkutsavunma.com/assets/images/logo2.png">
</p>


# İş Görüşmesi Öncesi HAZIRLIK ÇALIŞMASI

İş görüşmesi öncesi değerlendirmeye alabilmemiz için sizden bir takım basit çalışmalar yapmanızı istiyoruz. İş görüşmesi sırasında çalışma adımları üzerinde yüzeysel olarak konuşacağız.

❗❗ Çalışma sırasında kullandığınız `komutları, scriptleri, konfigürasyon dosyalarını` ve `bir bakkalın sadece kodları kopyalayıp çalıştırabilmesini sağlayacak şekilde dökümantasyon (README.md)` dosyasını hazırlayıp, kendinize ait bir git reposuna yükleyip, ePosta ile repo bağlantınızı bizimle paylaşın.

Örnek: [ÖRNEK HAZIRLIK ÇALIŞMASI](./ORNEK-calisma/)

❗❗ Oluşturmuş olduğunuz sanal makineleri silmeyiniz. Mülakat sırasında çalıştırmanızı isteyeceğiz.

❗❗ İşlemlerinizi terminal/shell (kara ekran) üzerinde Linux komutları kullanarak yapmanızı istiyoruz. Bu sebeple dökümantasyonunuzda ekran görüntüsü yerine Linux komutları görmeyi tercih ederiz.

```yaml
to: sgezer@erkutsavunma.com
cc: mkarabacak@erkutsavunma.com
```

❗❗ Herhangi bir sorun için `sgezer@erkutsavunma.com` iletişime geçebilirsiniz. (Genellikle 20.00-00.00 arasında cevap verebilirim.)

## Adımlar

(?) - Olması zorunlu değil, olursa güzel olur.

2 makine diye belirtilmemişse işlemleri Ubuntu 22.04 üzerinde yapılacak diye düşünebilirsiniz.

### SANALLAŞTIRMA ve İŞLETİM SİSTEMİ 

1. `VirtualBox` sanallaştırma üzerine `Vagrant` kullanarak aşağıdaki makineleri oluşturun. (Yani vagrantfile oluşturup vagrant up dediğimizde sırayla makine oluşturacak.)
   
   ```bash
   1. makine
   Ubuntu 22.04
   Minimum 4 GB RAM
   Minimum 4 Core
   (?) 150 GB Disk tanımlanması 
   IP: 192.168.66.100

   2. makine
   RockyLinux
   Minimum 4 GB RAM
   Minimum 4 Core
   (?) 100 GB Disk tanımlanması 
   IP: 192.168.66.200
   ```

   1. 2 makinede de `LinuxAdmin` kullanıcısı oluşturun ve parolasını `SysAdmin99` olarak belirleyin.
   2. 2 makinede de `LinuxAdmin` kullanıcısına **şifresiz olarak root** yetkisi verin. (Yani sudo komutunu çalıştırırken şifre sormasın.)
   3. Aşağıdaki çıktıyı veren scripti(tarih-bas.sh) yazın ve çalıştırın.
   
   ```bash
   Script i çalıştırdığımda;
   
   #Output
   Adınız Soyadınız
   Tarih: 2024-01-12 (Script çalıştığı tarih)
   Saat: 22:15 (Script çalıştığı saat)
   ```
   4. **tarih-bas.sh** scrpitinin sahipliğini `root` olarak ata ve izinlerini `777` olarak değiştirin.
   5. UFW/Firewalld servisini komple durdurun. (Sunucu yeniden başladığında çalışmasın.)
   6. Sistem log dosyası içerisinde `ERROR,error,eRRor` geçen kelimleri filtrele ve `LinuxAdmin Home Dizini` içerisinde `error.logs` dosyasına yazdırın.
   7. Ubuntu 22.04 makinesinde IP netplan ile verilmiştir. Bu konfigürasyona `8.8.8.8` ve `8.8.4.4 DNS` kayıtlarını ekleyin.


### DOCKER ve KUBERNETES

1. Ubuntu 22.04 makinesine `APT repoları kullanılarak`, son sürüm `docker` ve `docker-compose`  kurun. 
   1. `docker` ve `docker-compose` versiyonlarını ekrana bastırın.
   2. `busybox:1.35.0` sürümünü docker ile çekin.
   3. Wordress + Veritabanı (MySQL/MariaDB) ayağa kaldıracak bir `docker-compose-wordpress.yaml` oluşturun.
   4. Wordpress servisinin loglarını ekrana bastırın.
   5. Çekilen imajların bilgilerini ekrana bastırın.
   6. Veritabanı konteynırının içerisine girip, wordpress table larını listeleyin.
   7. `docker-compose-wordpress.yaml`  ile ayağa kaldırdığınız servisleri durdurun ve Wordpress + DB imajlarını sistemden silen scripti yazınız.


(?) 2. RockyLinux makinesine [`k3s Kubernetes dağıtımını`](https://k3s.io/) kurunuz.
   1. Kubernetes node un özelliklerini gösterin.
   2. Wordpress+DB'yi kubernetes ortamına deploy(çalışır hale) edin.
   3. http://IP_ADRESINIZ:32222  üzerinden Wordpress e giriş yapabileyim.
   4. Wordpress loglarını ekrana bastırın.
   5. Kubernetes Dashboard ı aktif edip, pod durumlarını gösterin. (?) k9s/Lens ile de gösterebilirsiniz.


Esen kalın ...