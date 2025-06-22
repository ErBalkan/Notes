# 🧱 Java’da Classes ve Objects

## 📌 1. Sınıf (Class) Nedir?

Bir sınıf, nesnelerin şablonudur. İçinde özellikler `(fields/attributes)` ve davranışlar `(methods)` bulunur.

- 🔧 Yani class = veri (değişken) + davranış (metot)

- 📦 "Bir varlığın nasıl göründüğü ve ne yaptığı

## 🧩 Yapısı:

```java
public class Araba {
    // Özellikler (fields)
    String marka;
    int hiz;

    // Davranışlar (metotlar)
    void hizlan() {
        hiz += 10;
    }
}
```

## 📌 2. Nesne (Object) Nedir?

Bir sınıftan türetilmiş canlı bir örnektir. Bellekte gerçek yer kaplar.

- Her nesne kendi verilerini tutar.

- 🔁 Aynı class’tan 100 farklı nesne oluşturabilirsin. Hepsi bağımsızdır.

## 🧪 Object Oluşturma

```java
public class Main {
    public static void main(String[] args) {
        Araba bmw = new Araba();    // Object oluşturuldu
        bmw.marka = "BMW";
        bmw.hizlan();

        System.out.println(bmw.marka);  // BMW
        System.out.println(bmw.hiz);    // 10
    }
}
```

- 📌 new anahtar kelimesi bellekte yeni bir nesne oluşturur.
- 📌 bmw referansıdır → nesneye erişim sağlar.


## 🛠 Sınıf Elemanları Nelerdir?

| Eleman             | Açıklama                                | Örnek              |
| ------------------ | --------------------------------------- | ------------------ |
| `fields`           | Nesnenin özellikleri                    | `String marka`     |
| `methods`          | Nesnenin davranışları                   | `void hizlan()`    |
| `constructors`     | Nesne oluştururken çalışan özel metot   | `public Araba()`   |
| `access modifiers` | Erişim belirleyiciler (public, private) | `private int hiz;` |


## 🏗 3. Constructor (Yapıcı Metot)

Sınıftan nesne türetildiğinde ilk çalışan bloktur.

Nesneye ilk değer atamak için kullanılır.

### 🔸 Varsayılan Constructor

```java
public class Araba {
    Araba() {
        System.out.println("Araba üretildi!");
    }
}
```

### 🔸 Parametreli Constructor

```java
public class Araba {
    String marka;
    int hiz;

    Araba(String marka, int hiz) {
        this.marka = marka;
        this.hiz = hiz;
    }
}
```

```java
Araba audi = new Araba("Audi", 120);
```

`🔑 this.marka = marka → sağdaki parametre, soldaki sınıf değişkenidir.`

## 🔄 4. Object-Oriented Memory Yapısı

```java
Araba a1 = new Araba("Opel", 50);
Araba a2 = new Araba("Ford", 100);
```

`Bu iki nesne, aynı class’tan türemiş ama bellekte farklı adreslerde yaşar. Değişiklikler birbirini etkilemez:`

```java
a1.hiz += 10;
System.out.println(a2.hiz); // 100 (değişmez)
```

## 👀 5. Class vs Object Özet

| Özellik      | Class                       | Object                       |
| ------------ | --------------------------- | ---------------------------- |
| Tanım        | Şablon, plan                | Bu şablondan üretilen varlık |
| Bellekte yer | Almaz                       | Alır (heap’te tutulur)       |
| Sayı         | 1 tane class, sonsuz object | Çok sayıda oluşturulabilir   |
| İçerik       | Alan + Davranış (kod)       | Veri + Davranışın sonucu     |


## ✅ Best Practices (Kurumsal Yaklaşımlar)

- Field’ları genellikle private yap → encapsulation uygula.

- Constructor içinde zorunlu alanları doldur.

- get ve set metotlarıyla erişim sağla.

- Tüm toString(), equals(), hashCode() metotlarını override etmeyi öğren (ileriki seviye).

## 🎯 Sınıflar İleri Düzeyde Ne İşe Yarar?

- Mimaride katmanları modülerleştirir.
- Domain modelleri (Kullanıcı, Ürün, Sipariş...) hep birer sınıftır.
- SOLID, Clean Code gibi prensiplerin tamamı sınıf odaklıdır.

