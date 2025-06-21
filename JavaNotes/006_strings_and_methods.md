# 🧵 Strings and Methods in Java

Java’da String veri tipi, metinlerle çalışmak için kullanılır. Ama dikkat: String basit bir veri tipi değildir — nesne (object)'dir. İçerisinde çok sayıda güçlü method barındırır ve __immutable (değiştirilemez)__ doğasıyla Java’nın en kritik yapıtaşlarından biridir.

## 📌 1. String Nedir?

```java
String message = "Merhaba, Patron!";
```

- Java’da String aslında bir class’tır: `java.lang.String`

- JVM içinde __immutable (değiştirilemez)__ olarak tasarlanmıştır.

- Her değişiklik __→__ yeni bir String nesnesi oluşturur.


## 🧱 2. String Oluşturma Yöntemleri
### 🔹 a) String Literal

```java
String name = "Patron";
```

- String pool içinde saklanır (hafıza optimizasyonu için).
- JVM önce havuza bakar, aynı değer varsa onu kullanır.

### 🔹 b) new Anahtar Kelimesi ile

```java
String name = new String("Patron");
```

- Heap’te yeni bir nesne oluşturur.
- String pool’u bypass eder.

`💡 Best practice`: Mümkünse literal kullan __→__ memory daha verimli olur.

## 🧠 3. Immutable Ne Demek?

```java
String str = "Java";
str.concat(" Bootcamp");
System.out.println(str); // Java  → değişmedi!
```

`str` nesnesi değişmez. `concat()` çağrısı yeni bir String döner ama orijinali etkilemez.

```java
str = str.concat(" Bootcamp");
System.out.println(str); // Java Bootcamp
```

## 🛠️ 4. En Çok Kullanılan String Metotları

### 🔹 length()

```java
String s = "Java";
System.out.println(s.length()); // 4
```

### 🔹 charAt(int index)

```java
System.out.println(s.charAt(2)); // 'v'
```

### 🔹 substring(int beginIndex)

```java
String result = s.substring(1); // "ava"
```

### 🔹 substring(int begin, int end)

```java
String sub = s.substring(1, 3); // "av"
```

### 🔹 toUpperCase() / toLowerCase()

```java
System.out.println(s.toUpperCase()); // JAVA
```

### 🔹 equals() / equalsIgnoreCase()

`equals()` tam eşleşme kontrolü yapar, `equalsIgnoreCase()` büyük küçük harf duyarlılığını yok sayar.

### 🔹 contains()

```java
System.out.println(s.contains("av")); // true
```

### 🔹 replace()

```java
System.out.println(s.replace("a", "o")); // "Jovo"
```

### 🔹 trim() → baştaki ve sondaki boşlukları kaldırır

```java
String input = "  hello ";
System.out.println(input.trim()); // "hello"
```

### 🔹 split() → parçalama

```java
String data = "ad,soyad,email";
String[] pieces = data.split(",");
```

### 🔹 startsWith() / endsWith()

```java
"Java".startsWith("Ja"); // true
```

## 📦 5. String Pool ve Bellek Yönetimi

- `String` literal'lar interned (pool içinde tutulur)
- `new String("x")` her çağrıldığında yeni nesne üretir
- Bu yüzden `==` yerine `equals()` kullanılır

```java
String a = "abc";
String b = "abc";
System.out.println(a == b); // true → aynı pool

String x = new String("abc");
System.out.println(a == x); // false → farklı nesne

System.out.println(a.equals(x)); // true → içerik aynı
```

## ⚠️ Sık Yapılan Hatalar

```java
String a = "Java";
String b = "Java";
System.out.println(a == b); // true

String c = new String("Java");
System.out.println(a == c); // false → referanslar farklı

System.out.println(a.equals(c)); // true → içerik aynı
```

## 💡 Kurumsal Best Practices

- String karşılaştırmalarında `==` kullanma. Her zaman `equals()` veya `equalsIgnoreCase()` kullan.
- Büyük metin işlemleri için `StringBuilder` kullan.
- String pool’dan faydalanmak için `new` kullanmaktan kaçın.
- 
- 