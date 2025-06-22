# ⚙️ Initializer Block (Başlatıcı Bloklar) – Java'nın Gizli Canlılığı

## 📌 1. Nedir Bu Initializer Block?

Java’da initializer block (başlatıcı blok), bir sınıf örneği oluşturulurken constructor’dan önce çalışan kod bloklarıdır.
Kodu tekrarsız ve merkezi bir yerde başlatmak için kullanılır.

```java
{
    // Bu blok bir initializer block’tur
    System.out.println("Initializer çalıştı!");
}
```

## 🔄 Nerede Çalışır?

- Constructor'dan önce çalışır
- Her nesne oluşturulmasında yeniden tetiklenir
- static değilse, instance initializer block denir

## 🧩 2. Türleri

| Tür                               | Açıklama                                    |
| --------------------------------- | ------------------------------------------- |
| 🟢 **Instance Initializer Block** | Nesne oluşturulurken çalışır                |
| 🔵 **Static Initializer Block**   | Sınıf belleğe yüklenirken *bir kez* çalışır |

## 🧪 3. Örneklerle Anlayalım

### ➤ Instance Initializer Block

```java
public class Kullanici {
    {
        System.out.println("Yeni kullanıcı oluşturuluyor...");
    }

    public Kullanici() {
        System.out.println("Constructor çalıştı.");
    }
}
```

```java
new Kullanici();
```

`Çıktı:`

```
Yeni kullanıcı oluşturuluyor...
Constructor çalıştı.
```

### ➤ Static Initializer Block

```java
public class Ayarlar {
    static {
        System.out.println("Ayarlar sınıfı yükleniyor...");
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Ayarlar a = new Ayarlar(); // sadece 1 kez çalışır
    }
}
```

Static initializer block, sınıf ilk defa JVM'e yüklendiğinde bir kez çalışır.

## ⚙️ 4. Nerede Kullanılır?

| Kullanım Senaryosu                     | Açıklama                                           |
| -------------------------------------- | -------------------------------------------------- |
| ✅ Kod tekrarını önlemek                | 3 constructor varsa aynı başlatma kodu burada olur |
| ✅ Loglama, başlangıç mesajı            | Hangi nesne ne zaman yaratılmış izlenebilir        |
| ✅ Map, List gibi sabitlerin yüklenmesi | static initializer içinde yapılır                  |
| ✅ Config dosyalarının okunması         | static initializer içinde çağrılır                 |


## 🛠️ 5. Constructor + Initializer Kombosu

```java
public class Siparis {
    int siparisNo;

    {
        System.out.println("Sipariş işlemleri başlatılıyor...");
    }

    public Siparis() {
        this.siparisNo = 100;
        System.out.println("Sipariş oluşturuldu: " + siparisNo);
    }

    public Siparis(int no) {
        this.siparisNo = no;
        System.out.println("Sipariş oluşturuldu: " + siparisNo);
    }
}
```

```java
new Siparis();
new Siparis(200);
```

`Çıktı:`

```less
Sipariş işlemleri başlatılıyor...
Sipariş oluşturuldu: 100
Sipariş işlemleri başlatılıyor...
Sipariş oluşturuldu: 200
```

Aynı kodu iki constructor’a yazmak yerine instance initializer block ile `DRY (Don’t Repeat Yourself)` uygulanır.


## 🧱 6. Static Initializer ile Sabit Veri Yükleme

```java
public class ParaBirimleri {
    public static final List<String> desteklenenBirimler;

    static {
        desteklenenBirimler = new ArrayList<>();
        desteklenenBirimler.add("USD");
        desteklenenBirimler.add("EUR");
        desteklenenBirimler.add("TRY");
    }
}
```

Bu kullanım, `Map`, `List`, `Set` gibi sabit yapıların sınıf yüklendiğinde hazırlanmasını sağlar.

## ⚠️ 7. Dikkat Edilmesi Gerekenler

| Uyarı                                  | Açıklama                              |
| -------------------------------------- | ------------------------------------- |
| `super()`'dan **önce** çalışır         | Inheritance varsa önemlidir           |
| Çok sayıda initializer karmaşa yaratır | Kodu okunmaz hale getirebilir         |
| `static` ve instance block’lar farklı  | Karıştırılmamalı                      |
| `static` bloklar sıraya göre çalışır   | Dosya içindeki tanım sırası önemlidir |


## 🔚 Özet

| Başlık                    | Detay                                             |
| ------------------------- | ------------------------------------------------- |
| Instance initializer      | Nesne oluşturulurken constructor’dan önce çalışır |
| Static initializer        | Sınıf yüklendiğinde sadece 1 kez çalışır          |
| DRY sağlar                | Kod tekrarını önler                               |
| Kapsam                    | Class içinde çalışır, metod içinde olmaz          |
| En iyi kullanım senaryosu | DTO başlatma, sabit veri yükleme, loglama         |


