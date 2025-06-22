# 🧬 Attributes (Nitelikler) ve Methods (Yöntemler)

Bu ikili, sınıfları veri + davranış yönünden şekillendirir. Java’nın kurumsal mimarilerindeki tüm soyutlamalar, sınıf içindeki bu iki yapı üzerinden inşa edilir.

## 🔹 1. Attributes (Fields / Properties / Instance Variables)

### ✅ Tanım:

Sınıfın veya nesnenin özelliklerini temsil eden değişkenlerdir.

### 🎯 Temel Yapı:

```java
public class Araba {
    // Attribute'lar
    String marka;
    int hiz;
    boolean calisiyorMu;
}
```

__📦 Her nesne kendi attribute değerlerini ayrı tutar:__

```java
Araba bmw = new Araba();
bmw.marka = "BMW";
bmw.hiz = 120;

Araba audi = new Araba();
audi.marka = "Audi";
audi.hiz = 100;
```

## 🔐 Access Modifiers ile Kullanımı:

| Modifier    | Açıklama                              |
| ----------- | ------------------------------------- |
| `private`   | Sadece sınıf içinden erişilir         |
| `public`    | Her yerden erişilir                   |
| `protected` | Aynı paket + alt sınıflardan erişilir |
| (default)   | Sadece aynı paketten erişilir         |


```java
public class Araba {
    private String marka;

    public void setMarka(String marka) {
        this.marka = marka;
    }

    public String getMarka() {
        return this.marka;
    }
}
```

`📌 Kurumsal kodlamada her zaman private kullanılır → dışarıya kontrolsüz erişim engellenir.`

## 🛠 Static vs Instance Attributes:

- static → sınıfa aittir (tüm nesneler ortak kullanır)

- Normal attribute → nesneye özeldir

```java
public class Araba {
    static int tekerSayisi = 4; // Her arabada ortak
    String marka;               // Nesneye özel
}
```

## 🔸 2. Methods (Davranışlar / İşlevler)

### ✅ Tanım:

Sınıfın ne yaptığı, nasıl çalıştığını temsil eden fonksiyonlardır.

```java
public class Araba {
    int hiz;

    // Method
    void hizlan() {
        hiz += 10;
    }

    void dur() {
        hiz = 0;
    }
}
```

- 📌 void = geriye değer döndürmez
- 📌 Parametreli de olabilir:

```java
void frenYap(int azalt) {
    hiz -= azalt;
}
```

## 🔂 Return Tipleri:

```java
int getHiz() {
    return hiz;
}

String getBilgi() {
    return "Marka: " + marka + ", Hız: " + hiz;
}
```

## 🔁 Parametreli Metotlar

```java
void ayarla(String yeniMarka, int yeniHiz) {
    this.marka = yeniMarka;
    this.hiz = yeniHiz;
}
```

- `this` → sınıfın kendi attribute'una erişim sağlar

## ⚙️ Static Method Nedir?

Sınıfa ait genel metotlardır. Nesne oluşturmadan çalıştırılabilir.

```java
public class AracAraci {
    public static void tanitim() {
        System.out.println("Araç sistemi başlatıldı.");
    }
}
```

```java
AracAraci.tanitim();  // Nesne olmadan çağrıldı
```

## ⚠️ İyi Tasarlanmış Attribute ve Method İlişkisi

Bir sınıfın attribute ve metotları birlikte yüksek tutarlılık(cohesion) göstermeli:

### Kötü örnek (low cohesion):

```java
class Araba {
    String marka;
    int hiz;

    void yazdir() {}         // printing?
    void kullaniciEkle() {}  // unrelated
    void hesaplaFiyat() {}   // unrelated
}
```

### İyi örnek (high cohesion):

```java
class Araba {
    String marka;
    int hiz;

    void hizlan() {}
    void frenYap() {}
    void bilgiGoster() {}
}
```

## ✅ Kurumsal Best Practices

| Kural                                        | Neden Önemli?                       |
| -------------------------------------------- | ----------------------------------- |
| Field’ları `private`, metotları `public` yap | Encapsulation                       |
| Setter yerine constructor kullan             | Immutable veri güvenliği            |
| Method isimleri fiil olmalı (`hizlan()`)     | Temsil ettiği aksiyonu net gösterir |
| Static method sadece bağımsız işlemlerde     | Nesneyle ilgili olmayan mantık      |


## 🧠 Sık Yapılan Hatalar

| Hata                                          | Açıklama                          |
| --------------------------------------------- | --------------------------------- |
| Field’ları `public` yapmak                    | Encapsulation bozulur             |
| Static method içinde non-static field erişimi | Derleme hatası verir              |
| Metot isimlerini rastgele koymak              | Anlaşılmaz, okunaksız kod üretir  |
| Field ve parametre adlarını karıştırmak       | `this` kullanılmazsa veri karışır |


## 🔄 Summary: Attribute vs Method

| Özellik             | Attribute (Field)   | Method                       |
| ------------------- | ------------------- | ---------------------------- |
| Tanım               | Nesne durumu/verisi | Nesnenin işlevleri/davranışı |
| Örnek               | `String ad`         | `void yazdir()`              |
| Static olabilir mi? | Evet                | Evet                         |
| Erişim              | Getter/Setter ile   | Doğrudan çağrılır            |


