# 🧠 Variables and Scopes (Değişkenler ve Kapsamlar)

Bu konu, yazdığın değişkenin nerede tanımlandığına ve nerede erişilebilir olduğuna odaklanır. Java'da değişkenleri sadece tanımlamak yetmez; onları doğru kapsamda, doğru sürede ve doğru yerde yönetmek zorundasın. Aksi takdirde performans, okunabilirlik ve güvenlik problemleri kaçınılmaz olur.

## 🔰 1. Java’da Değişken (Variable) Nedir?

__Değişken__, bellekte bir veri tutmak için kullanılan isimlendirilmiş bir alandır.

```java
int age = 30;
String name = "Patron";
```

__Her değişken:__

- Bir isim alır (identifier)
- Bir veri tipi taşır
- Bellekte bir alan kaplar

## 🔎 2. Değişken Türleri (Variable Types)

Java'da değişkenler kapsamlarına ve tanımlandıkları yere göre üçe ayrılır:

| Tür                  | Nerede Tanımlanır           | Ne Zaman Yaşar?         |
| -------------------- | --------------------------- | ----------------------- |
| **Local**            | Metot/blok içinde           | Sadece blok içinde      |
| **Instance (Field)** | Class içinde, metot dışında | Nesneyle birlikte yaşar |
| **Static (Class)**   | Class içinde, `static` ile  | Tüm sınıf boyunca yaşar |


### ✅ a) Local Variables (Yerel Değişkenler)

- Metot veya blok içinde tanımlanır.
- Sadece o blok içinde geçerlidir.
- JVM otomatik olarak null ya da 0 vermez __→__ kullanılmadan önce initialize edilmelidir.

```java
public void sayHi() {
    String message = "Merhaba";
    System.out.println(message); // Geçerli
}
// message burada erişilemez!
```

### ✅ b) Instance Variables (Örnek Değişkenler)

- __Class__ içinde, ama herhangi bir metodun dışında tanımlanır.
- Her nesneye özel kendi kopyası olur.
- JVM tarafından otomatik initialize edilir (null, 0, false, vs.).

```java
public class Person {
    String name; // instance variable

    public void sayName() {
        System.out.println("Adım: " + name);
    }
}
```

### ✅ c) Static Variables (Sınıf Değişkenleri)

- static anahtar kelimesiyle tanımlanır.
- Tüm nesneler arasında ortak kullanılır.
- Bellekte sadece bir kopyası olur (class level).

```java
public class Counter {
    static int count = 0; // static variable

    public Counter() {
        count++;
    }
}
```

__📌 Örnek:__

```java
Counter c1 = new Counter(); // count = 1
Counter c2 = new Counter(); // count = 2
```

## 🧱 3. Scope (Kapsam) Nedir?

Scope, bir değişkenin erişilebilir olduğu alan anlamına gelir. Java’da 4 temel scope vardır:

| Scope            | Tanımı                             | Nerede Erişilir  |
| ---------------- | ---------------------------------- | ---------------- |
| **Block Scope**  | `{}` içinde tanımlanan değişkenler | Sadece o blokta  |
| **Method Scope** | Bir metodun içindeki değişkenler   | Sadece o metodda |
| **Class Scope**  | Sınıf düzeyindeki değişkenler      | Tüm sınıf içinde |
| **Global Scope** | Java'da yoktur (bilinçli olarak!)  | ❌                |


### 🧪 Örnek – Tüm Scope'lar:

```java
public class ScopeExample {

    static int staticCount = 0;        // static (class-level)
    int instanceCount = 0;            // instance (object-level)

    public void doSomething() {
        int localValue = 5;           // method scope
        if (true) {
            int blockValue = 10;      // block scope
            System.out.println(blockValue);
        }
        // System.out.println(blockValue); // HATA: blockValue burada görünmez
        System.out.println(localValue);
    }
}
```

## 🧠 Bellek Yönetimi Bağlantısı

| Tür      | Nerede Tutulur?  | Ömrü Ne Kadar?           |
| -------- | ---------------- | ------------------------ |
| Local    | Stack            | Metot çalıştığı sürece   |
| Instance | Heap             | Nesne yaşadığı sürece    |
| Static   | Metaspace / Heap | Program çalıştığı sürece |


## 🚨 Best Practices (Kurumsal Seviyede Dikkat Edilecekler)

- Yerel değişkenleri sadece ihtiyaç duyulan blokta tanımla (minimum scope).

- Instance değişkenleri private yap + getter/setter kullan (encapsulation).

- Static değişkenleri final ile sabitle (global constant gibi).

__Örnek:__

```java
public static final String APP_NAME = "BlogApp";
```

```
“Değişkenin kapsamı, onun yaşam süresidir. Gereğinden uzun yaşarsa hafıza israfı, kısa yaşarsa erişim hatası çıkar. Doğru scope yönetimi, temiz kodun ve güvenli belleğin temelidir.”
```

