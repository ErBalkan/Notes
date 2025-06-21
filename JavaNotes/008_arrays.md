# 📦 Arrays (Diziler)

Java’da `Array`, sabit uzunlukta ve aynı türdeki verileri tutmak için kullanılan veri yapısıdır. Hem memory optimizasyonu hem de temel veri organizasyonu için çok önemlidir. Profesyonel Java geliştirmede `List`, `Map` gibi koleksiyonlara geçmeden önce array yapısını çok iyi anlaman gerekir.

## 🧱 1. Dizi Nedir?

- Aynı türde verilerin sıralı bir şekilde tutulduğu yapılardır.

- Sabit boyutludur (runtime’da değiştirilemez).

- Her elemanın bir indeksi vardır (0 tabanlı)

```java
int[] sayilar = new int[5];  // 5 elemanlı int dizisi
```

## 📌 2. Dizi Oluşturma Yolları

### 🔹 a) Sabit Uzunlukla Tanımlama

```java
String[] isimler = new String[3];
isimler[0] = "Patron";
isimler[1] = "Yok";
isimler[2] = "Z-Gen";
```

### 🔹 b) Doğrudan Değer Atama (Literal)

```java
int[] notlar = {85, 90, 78, 100};
```

## 🔄 3. Diziye Erişim

```java
int[] notlar = {85, 90, 78, 100};
System.out.println(notlar[0]); // 85
notlar[1] = 95; // Değeri güncelle
System.out.println(notlar.length); // 4
```

`⚠️ Java'da dizi sınırları dışına çıkmak ArrayIndexOutOfBoundsException fırlatır.`

```java
System.out.println(notlar[10]); // ❌ Hata!
```

## 🧪 4. Döngüyle Dizi İşleme
### 🔸 Klasik for Döngüsü

```java
for (int i = 0; i < notlar.length; i++) {
    System.out.println(notlar[i]);
}
```

### 🔸 Gelişmiş for-each Döngüsü

```java
for (int not : notlar) {
    System.out.println(not);
}
```

## 🔍 5. Çok Boyutlu Diziler (Multi-dimensional Arrays)

```java
int[][] tablo = {
    {1, 2, 3},
    {4, 5, 6}
};

System.out.println(tablo[0][1]); // 2
```

`Bunlar aslında içinde array barındıran array’lerdir (array of arrays).`

## 🧠 6. Arrays Sınıfı (java.util.Arrays)

Java, dizi işlemleri için utility method'lar sunar.

```java
import java.util.Arrays;

int[] dizi = {3, 1, 4, 2};

Arrays.sort(dizi);               // Sıralama
System.out.println(Arrays.toString(dizi)); // [1, 2, 3, 4]

int index = Arrays.binarySearch(dizi, 3);  // 2 (sorted olmalı)
System.out.println(index);

int[] kopya = Arrays.copyOf(dizi, dizi.length); // dizi kopyalama
```

## 📊 Dizi vs Collection

| Yapı        | Esneklik | Performans | Kullanım Alanı                  |
| ----------- | -------- | ---------- | ------------------------------- |
| `Array`     | Sabit    | Yüksek     | Sabit uzunluklu, primitive veri |
| `ArrayList` | Dinamik  | Orta       | Koleksiyon bazlı işlemler       |



