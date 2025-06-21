# 🧮 Operators (Operatörler)

Java’da operatörler, değişkenler ve değerler üzerinde işlem yapmak için kullanılır. Bu konu, sadece temel hesaplamalar için değil — aynı zamanda karşılaştırmalar, mantıksal akış kontrolü, bit işlemleri ve hatta __memory optimizasyonu__ gibi ileri düzey konular için de kritik öneme sahiptir.

## 🚀 Operatör Tipleri

| Kategori                      | Açıklama                             |                           |         |
| ----------------------------- | ------------------------------------ | ------------------------- | ------- |
| **Aritmetik**                 | Toplama, çıkarma, çarpma, bölme, mod |                           |         |
| **İlişkisel (Karşılaştırma)** | `==`, `!=`, `>`, `<`, `>=`, `<=`     |                           |         |
| **Mantıksal (Logical)**       | `&&`, \`                             |                           | `, `!\` |
| **Atama**                     | `=`, `+=`, `-=`, `*=`, `/=`, `%=`    |                           |         |
| **Artırma/Azaltma**           | `++`, `--`                           |                           |         |
| **Bitwise**                   | `&`, \`                              | `, `^`, `\~`, `<<`, `>>\` |         |
| **Ternary**                   | `? :`                                |                           |         |
| **Instanceof**                | Nesne türü kontrolü                  |                           |         |


## ➕ 1. Aritmetik Operatörler

```java
int a = 10;
int b = 3;

System.out.println(a + b); // 13
System.out.println(a - b); // 7
System.out.println(a * b); // 30
System.out.println(a / b); // 3
System.out.println(a % b); // 1
```

`⚠️ Tam sayılarda 10 / 3 = 3 olur, çünkü int'dir → küsurat atılır.`

## 🔍 2. Karşılaştırma (Relational) Operatörleri

```java
int x = 5;
int y = 10;

System.out.println(x == y); // false
System.out.println(x != y); // true
System.out.println(x < y);  // true
System.out.println(x >= y); // false
```

## 🧠 3. Mantıksal Operatörler (Boolean Logic)

```java
boolean a = true;
boolean b = false;

System.out.println(a && b); // false
System.out.println(a || b); // true
System.out.println(!a);     // false
```

| Operatör | Anlamı | Açıklama                         |
| -------- | ------ | ---------------------------------|
| `&&`     | ve     | İki koşul da doğruysa `true`     |
|          | veya   | İki koşuldan biri doğruysa `true`|
| `!`      | değil  | Mantıksal tersini alır           |


## 🧾 4. Atama Operatörleri

```java
int x = 10;
x += 5;  // x = x + 5
x *= 2;  // x = x * 2
x -= 3;  // x = x - 3
x /= 4;  // x = x / 4
```

## 🔄 5. Artırma ve Azaltma Operatörleri

```java
int i = 5;

System.out.println(i++); // 5 (önce yaz, sonra artır)
System.out.println(++i); // 7 (önce artır, sonra yaz)
```

| Operatör | Açıklama                 |
| -------- | ------------------------ |
| `++i`    | Önce artır, sonra kullan |
| `i++`    | Önce kullan, sonra artır |
| `--i`    | Önce azalt, sonra kullan |
| `i--`    | Önce kullan, sonra azalt |


## ❓ 7. Ternary Operatör

Kısa `if/else` yapısıdır. Çok tercih edilir çünkü okunabilirliği artırır.

```java
int age = 20;
String status = (age >= 18) ? "Yetişkin" : "Çocuk";
System.out.println(status); // Yetişkin
```

## 🔎 8. instanceof Operatörü

Bir nesnenin belirli bir sınıftan türetilip türetilmediğini kontrol eder.

```java
String str = "hello";
System.out.println(str instanceof String); // true
```

## 💼 Kurumsal Best Practices
- Ternary operatör, karmaşık if yapılarında temiz kod sağlar.

- Mantıksal operatörlerde null kontrollerine dikkat et (&&, ||).

- == yerine equals() kullanmayı unutma (özellikle String için).

## ⚠️ Sık Hatalar

```java
int x = 5;
if (x = 10) { } // ❌ Hata: "=" atama operatörü, "==" bekleniyor

boolean b = false;
if (b = true) { } // ❌ Hata yok ama mantık hatası
```



