# 🔁 Loops (Döngüler)

Döngüler, tekrarlayan işlemleri otomatikleştirir. Yani kod tekrarını ortadan kaldırır ve verimliliği uçurur. Java’da 4 temel döngü yapısı vardır:

## 🔸 1. for Döngüsü

__Yapı:__

```java
for (başlangıç; koşul; artış/azalış) {
    // tekrar eden kod bloğu
}
```

__Örnek:__

```java
for (int i = 0; i < 5; i++) {
    System.out.println("i: " + i);
}
```

`🔍 for döngüsü, sabit sayıda dönecek durumlar için idealdir.`

## 🔹 2. while Döngüsü

__Yapı:__

```java
while (koşul) {
    // koşul doğru olduğu sürece çalışır
}
```

__Örnek:__

```java
int i = 0;
while (i < 5) {
    System.out.println("i: " + i);
    i++;
}
```

`🔁 Koşul önceden kontrol edilir. Sonsuz döngüye dikkat!`

## 🔸 3. do-while Döngüsü

__Yapı:__

```java
do {
    // en az bir kez çalışır
} while (koşul);
```

__Örnek:__

```java
int i = 0;
do {
    System.out.println("i: " + i);
    i++;
} while (i < 5);
```

`🧠 Koşul sonradan kontrol edilir, yani içerideki blok en az bir kere çalışır.`

## 🔹 4. for-each Döngüsü (Enhanced For Loop)

Sadece diziler ve koleksiyonlar üzerinde döner.

__Örnek:__

```java
int[] sayilar = {1, 2, 3, 4};

for (int sayi : sayilar) {
    System.out.println(sayi);
}
```

`🚀 Daha okunabilir, hata oranı daha düşük. Ama indeks gerekirse klasik for kullan.`

## 🚫 Kontrol Anahtarları: break ve continue

### 🔻 break → Döngüyü kırar ve dışına çıkar:

```java
for (int i = 0; i < 10; i++) {
    if (i == 5) break;
    System.out.println(i);
}
// 0, 1, 2, 3, 4
```

### 🔻 continue → O anki iterasyonu atlar ve devam eder:

```java
for (int i = 0; i < 5; i++) {
    if (i == 2) continue;
    System.out.println(i);
}
// 0, 1, 3, 4
```

## 💼 Gerçek Dünya Örneği

```java
String[] kullanicilar = {"Ahmet", "Mehmet", "Patron", "Yok"};

for (String ad : kullanicilar) {
    if (ad.equals("Patron")) {
        System.out.println("Admin bulundu!");
        break;
    }
}
```

## 🧨 Sonsuz Döngü Hataları

```java
while (true) {
    // koşul yok = sonsuz döngü
}
```

`🧠 Sonsuz döngü bazı durumlarda bilinçli kullanılır (sunucu işlemleri, oyun döngüleri vs), ancak koşulsuz döngülerin kontrolsüz olması uygulamayı kilitler.`

## ⚙️ Döngü Seçim Tablosu

| Yapı       | Kullanım Durumu                        |
| ---------- | -------------------------------------- |
| `for`      | Sayma/indeks bazlı tekrar              |
| `while`    | Önceden bilinmeyen sayıda tekrar       |
| `do-while` | En az bir kere çalışması gereken blok  |
| `for-each` | Dizi/koleksiyon üzerinde kolay gezinti |


