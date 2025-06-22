# 🧊 ENCAPSULATION — Nesneye Yönelik Programlamada Koruma Kalkanı

## 📌 1. Tanım – Encapsulation Nedir?

Encapsulation, bir sınıfın içindeki verilerin (fields) dış dünya tarafından doğrudan erişilmesini engelleyip, bu verilere sadece kontrollü yollarla erişilmesini sağlayan ilkedir.

### 🔁 Basitçe:

Veriyi gizle, sadece izin verdiğin şekilde dışarı aç.

## 🧠 2. Temel Amacı Nedir?

| Amaç                          | Açıklama                                                  |
| ----------------------------- | --------------------------------------------------------- |
| 🔐 **Veri gizleme**           | Doğrudan erişimi engeller, sadece sınıf içinden erişilir. |
| 📦 **Dış dünyadan soyutlama** | Kullanıcı sadece ne olduğunu bilir, nasıl olduğunu değil. |
| 🔧 **Değişkenlerin kontrolü** | Set ederken validasyon, loglama, vs. eklenebilir.         |
| 🧪 **Test edilebilirlik**     | Her şey merkezi kontrol altında olur.                     |
| ♻️ **Bakım kolaylığı**        | Değişiklik tek noktadan yapılır, yayılmaz.                |


## 🏗️ 3. Java'da Nasıl Uygulanır?

### ✅ Adımlar:

1. Alanları private yap
2. Getter ve Setter metodlarını yaz
3. İsteğe göre setter içinde kontrol ekle


### 📌 Örnek:

```java
public class Calisan {
    private String isim;
    private double maas;

    public String getIsim() {
        return isim;
    }

    public void setIsim(String isim) {
        this.isim = isim;
    }

    public double getMaas() {
        return maas;
    }

    public void setMaas(double maas) {
        if (maas > 0) {
            this.maas = maas;
        } else {
            throw new IllegalArgumentException("Maaş 0'dan büyük olmalı!");
        }
    }
}
```

#### 🔍 Ne Yaptık?

1. isim ve maas dışarıdan direkt erişilemez hale geldi.
2. get ile veri okunabilir, set ile sadece kurallar çerçevesinde yazılabilir oldu.

```
Encapsulation’da alanlar çoğunlukla private olur. Erişim public getter/setter ile sağlanır.
```

## ⚙️ Getter / Setter’ın Özelleştirilmesi

```java
public void setEmail(String email) {
    if (email.contains("@")) {
        this.email = email;
    } else {
        throw new IllegalArgumentException("Geçersiz e-posta!");
    }
}
```

__Yani setter, sadece değer atamaz, aynı zamanda kontrol merkezi olur.__

## 🧩 Modern Java: Lombok ile Getter/Setter

Kurumsal projelerde genelde `Lombok` kütüphanesi ile boilerplate kodlar kaldırılır.

```java
import lombok.Getter;
import lombok.Setter;

@Getter
@Setter
public class Urun {
    private String ad;
    private double fiyat;
}
```

