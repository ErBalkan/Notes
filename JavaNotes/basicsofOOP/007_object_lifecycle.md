# 🧬 Java'da Object Lifecycle (Nesne Yaşam Döngüsü)

## 🚦 1. Tanım

Java'da bir nesnenin yaşam döngüsü, oluşturulmasından başlayıp çöp toplayıcı `(Garbage Collector)` tarafından bellekten silinmesine kadar geçen süreci ifade eder.

## 🧪 2. Aşamalar (Detaylı Lifecycle)

Java'da bir nesne şu 5 aşamadan geçer:

```css
[Declaring] → [Instantiating] → [Using] → [Eligible for GC] → [Finalization/Destruction]
```

### 📌 2.1. Declaring (Tanımlama)

Java'da bir nesnenin referansı tanımlanır.

```java
MyClass obj;  // sadece referans tanımlandı, heap'te nesne yok!
```

Sadece stack memory üzerinde bir referans alanı oluşturulur.

### ⚙️ 2.2. Instantiating (Oluşturma)

__new__ anahtar kelimesiyle `heap` üzerinde bir nesne yaratılır.

```java
obj = new MyClass();
```

`Bu noktada constructor çalışır. Nesne heap memory'de yer kaplar.`

### 🎯 2.3. Using (Kullanım)

Nesne üzerinden metodlar veya özellikler kullanılır.

```java
obj.sayHello();
obj.name = "Patron";
```

__Nesne, referansıyla birlikte aktif olarak yaşamaktadır.__

### 🧨 2.4. Eligible for GC (Çöp Toplamaya Uygunluk)

Nesneye artık hiçbir referans yoksa veya tüm referanslar scope dışına çıktıysa, Java bu nesneyi çöp olarak işaretler.

```java
obj = null; // artık heap'teki nesneye ulaşan yok.
```

### ☠️ 2.5. Finalization & Destruction

Java'da nesneler manuel __silinmez.__ `Garbage Collector (GC)` çalışınca __finalize()__ metodu tetiklenebilir (ama önerilmez – deprecated!).

```java
@Override
protected void finalize() throws Throwable {
    System.out.println("Nesne yok ediliyor!");
}
```

```
Java 9 sonrası finalize() deprecated oldu. Yerine AutoCloseable + try-with-resources kullanılır.
```

## 🧠 3. Bellek Yapısı (Memory Model)

| Alan      | Açıklama                                    |
| --------- | ------------------------------------------- |
| Stack     | Yerel değişkenler, metod çağrıları          |
| Heap      | `new` ile yaratılan tüm nesneler            |
| Metaspace | Class tanımları, static veriler             |
| GC Roots  | JVM'nin erişim noktaları (main, thread vb.) |


## 🗂️ 4. Örnekle Aşamaları Görelim

```java
public class Test {
    public static void main(String[] args) {
        MyClass obj1 = new MyClass(); // create (instantiation)
        obj1 = null;                  // eligible for GC

        MyClass obj2 = new MyClass();
        MyClass obj3 = obj2;          // iki referans aynı nesneye bağlı
        obj2 = null;                  // hâlâ obj3 var, GC çalışmaz
    }
}
```

## ♻️ 5. Garbage Collector (GC) Nasıl Çalışır?

- JVM tarafından yönetilir

- Belirli zaman aralıklarında çalışır (arka planda)

- Algoritmalar:

* Mark and Sweep
* Generational GC
* G1GC (Java 9+)

GC nesneleri aşağıdaki nesne graph'larına göre işaretler:

- Aktif referans yoksa
- Scope dışına çıkmışsa
- WeakReference kullanılmışsa

## 🧽 6. System.gc() Kullanımı

__Manuel GC çağrısı:__

```java
System.gc();
```

Zorunlu değil, JVM kararı verir. Sadece bir tavsiye niteliğindedir. Genellikle kullanılmaz.

