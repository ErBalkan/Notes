# 🧠 Pass by Value vs Pass by Reference (Java’da Gerçek Ne?)

## ⚠️ 1. Klişe Cümleyle Başlayalım:

Java is always pass by value.
Java’da her şey pass by value’dur.

Ama bu cümle yeterli değil. Çünkü:

- ilkel (primitive) tiplerle,

- referans (nesne) tiplerinde davranış farklı görünür.

Bunu derinlemesine anlayalım.

## 🧪 2. İlkel Tiplerde (Primitives) – %100 Net “Pass by Value”

```java
public class Main {
    public static void main(String[] args) {
        int sayi = 10;
        degistir(sayi);
        System.out.println(sayi);  // 👉 10
    }

    public static void degistir(int x) {
        x = 999;
    }
}
```

__Ne Oldu?__

- sayi değişkeninin değeri kopyalandı (10)
- x değişti ama sayi değişmedi

✅ Java burada açıkça pass-by-value çalışıyor.

## 📦 3. Referans Tiplerinde (Objects) – “Referansın Kopyası” (Burada Kafa Karışıyor)

```java
class Kullanici {
    String isim;
}

public class Main {
    public static void main(String[] args) {
        Kullanici k = new Kullanici();
        k.isim = "Ahmet";

        degistir(k);
        System.out.println(k.isim);  // 👉 "Mehmet"
    }

    public static void degistir(Kullanici kisi) {
        kisi.isim = "Mehmet";
    }
}
```

__Ne Oldu?__

- k nesnesinin referansı kopyalandı
- Ama bu kopya da aynı nesneyi işaret ediyor
- isim alanı değiştirildi → bu yüzden dışarıdan da görüldü

❗ Ancak kisi referansının kendisini değiştirmeye çalışırsan…

```java
public static void degistir(Kullanici kisi) {
    kisi = new Kullanici(); // 🔁 referans değiştirdin
    kisi.isim = "Veli";
}
```

```java
System.out.println(k.isim); // 👉 Hâlâ "Ahmet"
```

Çünkü burada sadece __referansın__ kopyası değiştirildi. Orijinal referans etkilenmedi.

## 🎯 4. Peki Gerçek Ne?

Java’da:
- Primitive değerler → değeri kopyalanır
`int, double, boolean, vs.`

- Nesne (Object) → referansın kendisi kopyalanır,

yani parametre olarak gelen değişken orijinal nesneyle aynı objeyi işaret eder.

## 📌 String Neden Değişmiyor?

```java
public class Main {
    public static void main(String[] args) {
        String s = "Java";
        degistir(s);
        System.out.println(s); // 👉 Java
    }

    public static void degistir(String str) {
        str = "Python";
    }
}
```

Çünkü `String` immutable’dır. `str = "Python"` dediğinde yeni bir `String` nesnesi oluşturulur. Orijinal `s` etkilenmez.



