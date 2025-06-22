# 🧱 enums – Enumerated Types (Sıralı Sabitler)

## 🔍 1. Enum Nedir?

enum, __sabit (değişmeyen)__ değerler kümesini tanımlamak için kullanılan özel bir veri türüdür.

```java
public enum Gun {
    PAZARTESI, SALI, CARSAMBA, PERSEMBE, CUMA, CUMARTESI, PAZAR
}
```

Enum’lar, Java’da `class` düzeyinde bir yapıdır. Her enum aslında `java.lang.Enum` sınıfının bir alt sınıfıdır.

## 🧠 2. Neden Enum Kullanılır?

| Avantaj                     | Açıklama                               |
| --------------------------- | -------------------------------------- |
| ✅ Tip güvenliği (type-safe) | String ya da int yerine özel enum türü |
| ✅ Kod okunabilirliği        | `DURUM = AKTIF` gibi net ifadeler      |
| ✅ Otomatik `toString()`     | Enum ismi döner                        |
| ✅ Switch-case ile uyumlu    | Daha okunaklı kontrol akışı            |
| ✅ Sabitleri merkezi yönetme | Hardcode yerine anlamlı isimler        |


## ⚙️ 3. Enum Nasıl Tanımlanır?

`Basit Tanım:`

```java
public enum Renk {
    KIRMIZI, YESIL, MAVI
}
```

`Kullanımı:`

```java
Renk r = Renk.KIRMIZI;
System.out.println(r); // KIRMIZI
```

## 🧩 4. Enum Sınıf Gibi Kullanılır

Enum içine alan (field), constructor, method yazabilirsin.

```java
public enum Durum {
    AKTIF(1),
    PASIF(0);

    private final int kod;

    Durum(int kod) {
        this.kod = kod;
    }

    public int getKod() {
        return kod;
    }
}
```

`Kullanımı:`

```java
Durum d = Durum.AKTIF;
System.out.println(d.getKod()); // 1
```

## 🔄 5. Enum ile switch-case

```java
public void islemYap(Gun gun) {
    switch (gun) {
        case PAZARTESI -> System.out.println("Hafta başı.");
        case CUMA -> System.out.println("Haftanın son iş günü.");
        case PAZAR -> System.out.println("Tatilsin.");
        default -> System.out.println("Normal gün.");
    }
}
```

Enum ile `switch` kullanmak okunabilirliği ve kontrol yapısını artırır.

## 🧮 6. Enum Metodları

| Metot                 | Açıklama                               |
| --------------------- | -------------------------------------- |
| `.values()`           | Tüm enum sabitlerini dizi olarak döner |
| `.ordinal()`          | Sabitin sırasını (index) döner         |
| `.name()`             | Enum ismini string olarak döner        |
| `Enum.valueOf("...")` | String’i enum’a çevirir                |


## 🧠 7. Enum ile Polimorfizm

Enum’lar içerisinde soyut metod tanımlayıp her sabit için farklı implementasyon verebilirsin:

```java
public enum Operasyon {
    TOPLA {
        public int islem(int a, int b) { return a + b; }
    },
    CIKAR {
        public int islem(int a, int b) { return a - b; }
    };

    public abstract int islem(int a, int b);
}
```

```java
int sonuc = Operasyon.TOPLA.islem(10, 5); // 15
```

Bu yapı ile enum, `Strategy Pattern` gibi çalışır.


## 🔐 Örnek: HTTP Durum Kodu Enum’u

```java
public enum HttpStatus {
    OK(200, "Başarılı"),
    BAD_REQUEST(400, "Geçersiz istek"),
    NOT_FOUND(404, "Bulunamadı");

    private final int code;
    private final String mesaj;

    HttpStatus(int code, String mesaj) {
        this.code = code;
        this.mesaj = mesaj;
    }

    public int getCode() { return code; }
    public String getMesaj() { return mesaj; }
}
```

## 📦 Best Practice & Kullanım Alanları

| Kullanım Alanı              | Açıklama                            |
| --------------------------- | ----------------------------------- |
| ✅ Durum yönetimi            | `ACTIVE`, `PASSIVE`, `DELETED` gibi |
| ✅ Rol tanımlamaları         | `ADMIN`, `MODERATOR`, `USER`        |
| ✅ Konfigürasyon/ayarlamalar | `ENV.DEV`, `ENV.PROD`               |
| ✅ HTTP durum kodları        | `HttpStatus.NOT_FOUND`              |
| ✅ Opsiyon listeleri         | GUI'deki dropdown verileri          |


## 🎯 Özet

| Özellik        | Detay                                                  |
| -------------- | ------------------------------------------------------ |
| Tanım          | Sabitler kümesini temsil eden özel sınıf               |
| İçerik         | Alan, metod, constructor içerebilir                    |
| Avantaj        | Tip güvenliği, okunabilirlik, switch-case uyumu        |
| Kullanım Alanı | Durum kodları, roller, ayarlar, dropdown verileri      |
| Risk           | Fazla karmaşık hale getirme, enum'a aşırı yük bindirme |


