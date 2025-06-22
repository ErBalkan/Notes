# 🧱 Basics of OOP (Object-Oriented Programming - Nesne Yönelimli Programlama)

Java, baştan sona OOP temelli bir dildir. Ne yazarsan yaz, doğru OOP prensiplerine dayanmazsa, kodun ölçeklenemez, sürdürülemez ve kurumsal seviyeye çıkamaz.

Bu yüzden bu konuyu sadece anlaman yetmez, içselleştirmen gerekir.

## 💡 OOP Nedir?
OOP, gerçek dünyadaki kavramları nesneler olarak modelleyerek yazılım geliştirme yaklaşımıdır. Her nesne, veri (alanlar) ve bu veriler üzerinde çalışan davranışları (metotlar) içerir.

## 🧩 Java’da OOP’nin 4 Ana Ayağı

| OOP Prensibi      | Tanım                                                    |
| ----------------- | -------------------------------------------------------- |
| **Encapsulation** | Veri ve davranışları bir kapsülde saklamak (class)       |
| **Abstraction**   | Gereksiz detayları gizleyip sadece önemli bilgiyi sunmak |
| **Inheritance**   | Bir sınıfın başka bir sınıftan özellik devralması        |
| **Polymorphism**  | Aynı isimli metodun farklı şekillerde çalışabilmesi      |


## 🔹 1. Class ve Object (Sınıf ve Nesne)

Sınıf bir şablondur __(template)__.

Nesne bu şablondan üretilmiş somut varlıktır.

```java
public class Araba {
    String marka;
    int hiz;

    void hizlan() {
        hiz += 10;
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Araba bmw = new Araba();       // Object oluşturma
        bmw.marka = "BMW";
        bmw.hizlan();                  // Davranış
        System.out.println(bmw.hiz);   // 10
    }
}
```

## 🔒 2. Encapsulation (Kapsülleme)

Alanları private yap __→__ dışarıdan doğrudan erişimi engelle.

getter ve setter metodlarıyla kontrollü erişim sağla.

```java
public class Kullanici {
    private String ad;

    public String getAd() {
        return ad;
    }

    public void setAd(String yeniAd) {
        this.ad = yeniAd;
    }
}
```

__📌 Veri bütünlüğü sağlar. Yani nesne içindeki veri her yerden rastgele değiştirilemez.__

## 🎭 3. Inheritance (Kalıtım)

`extends` anahtar kelimesiyle bir sınıf, başka bir sınıfı miras alır.

```java
public class Hayvan {
    void sesCikar() {
        System.out.println("Bir ses çıkardı.");
    }
}

public class Kedi extends Hayvan {
    void miyavla() {
        System.out.println("Miyav!");
    }
}
```

```java
Kedi k = new Kedi();
k.sesCikar(); // Üst sınıf davranışı
k.miyavla();  // Alt sınıf davranışı
```

`♻️ Kod tekrarını azaltır, mantıksal hiyerarşi kurar.`

## 🧬 4. Polymorphism (Çok Biçimlilik)

### 🔸 a) Overriding

Üst sınıftaki metodu alt sınıfta ezmek `(override etmek)`

```java
public class Hayvan {
    void sesCikar() {
        System.out.println("Ses");
    }
}

public class Kopek extends Hayvan {
    @Override
    void sesCikar() {
        System.out.println("Hav!");
    }
}
```

```java
Hayvan h = new Kopek();
h.sesCikar();  // Çıktı: Hav! → runtime polymorphism
```

### 🔸 b) Overloading

Aynı metot ismiyle farklı parametrelerle çalıştırma:

```java
public class Hesap {
    int topla(int a, int b) {
        return a + b;
    }

    int topla(int a, int b, int c) {
        return a + b + c;
    }
}
```

## 🧠 5. Abstraction (Soyutlama)

Kullanıcıya sadece ne yaptığını göster, nasıl yaptığını değil.

`abstract class` ya da `interface` ile sağlanır.

```java
abstract class Sekil {
    abstract double alanHesapla();
}

class Kare extends Sekil {
    double kenar;
    Kare(double kenar) { this.kenar = kenar; }

    @Override
    double alanHesapla() {
        return kenar * kenar;
    }
}
```

__Abstraction__, büyük sistemlerde modülerliği ve bağımsız geliştirilebilirliği sağlar.


## 🧪 Sık Hatalar

| Hata                        | Açıklama                                     |
| --------------------------- | -------------------------------------------- |
| `NullPointerException`      | Nesne üretilmeden kullanılmak istenmesi      |
| `Object reference required` | Statik olmayan üyeye statik kontekste erişim |
| `ClassCastException`        | Yanlış tür dönüşümü                          |
| `NoSuchMethodError`         | Yanlış veya eksik override                   |

## 🚀 OOP’in Getirdiği Kazanımlar

- ✅ Kodun bakımı kolaylaşır
- ✅ Genişletilebilirlik artar (Extensibility)
- ✅ Gerçek dünya modellemesi yapılır
- ✅ Yazılım test edilebilirliği yükselir
- ✅ Takım içi modüler geliştirme sağlanır

## 📌 Özet

| OOP Prensibi  | Anahtar Kelime             | Görev                             |
| ------------- | -------------------------- | --------------------------------- |
| Encapsulation | `private`, `getter/setter` | Veriyi koru, erişimi sınırla      |
| Inheritance   | `extends`                  | Kod tekrarını azalt, yapı kur     |
| Polymorphism  | `@Override`                | Farklı davranış, aynı referans    |
| Abstraction   | `abstract`, `interface`    | Detayları gizle, sadece işlev sun |


