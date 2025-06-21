# ⚙️ Conditionals (Koşul İfadeleri)

`Conditionals`; programın, belirli koşullara göre farklı yollar izlemesini sağlar. Kurumsal seviyede yazılım geliştirirken mantık dallanmasının omurgasını oluşturur. Java'da bu yapıların doğru, temiz ve okunabilir kullanımı temiz kodun temelidir.

## 🔧 Java'da Koşul Tipleri

| Yapı      | Kullanım Amacı                                |
| --------- | --------------------------------------------- |
| `if`      | Basit bir koşulu kontrol eder                 |
| `if-else` | Koşul doğru değilse alternatif aksiyon        |
| `else if` | Birden fazla koşulu zincirlemek               |
| `switch`  | Çoklu durumları daha okunabilir kontrol etmek |


## 🔹 1. if Yapısı

```java
int yas = 20;

if (yas >= 18) {
    System.out.println("Reşit.");
}
```

Blok parantez `{}` yazmak zorunlu değil ama best practice gereği her zaman kullan.

## 2. if-else Yapısı

```java
if (yas >= 18) {
    System.out.println("Ehliyet alabilir.");
} else {
    System.out.println("Ehliyet alamaz.");
}
```

## 3. if - else if - else Zinciri

```java
int not = 85;

if (not >= 90) {
    System.out.println("AA");
} else if (not >= 80) {
    System.out.println("BA");
} else if (not >= 70) {
    System.out.println("BB");
} else {
    System.out.println("Kaldı");
}
```

`🧠 else if zinciri okunabilirliği korur. Karmaşık switch-case’ler yerine tercih edilebilir.`

## 🌀 4. Ternary Operator (Kısa if)

```java
int sayi = 10;
String sonuc = (sayi % 2 == 0) ? "Çift" : "Tek";
System.out.println(sonuc); // Çift
```

Kod okunabilirliğini artırır ama iç içe ternary kullanımı __anti-pattern__ sayılır.

## 🔄 5. switch Yapısı

Çok fazla `else if` varsa yerine `switch` kullanılır. Daha düzenli ve daha hızlıdır (derleyici tarafından optimize edilir).

```java
int gun = 3;

switch (gun) {
    case 1:
        System.out.println("Pazartesi");
        break;
    case 2:
        System.out.println("Salı");
        break;
    case 3:
        System.out.println("Çarşamba");
        break;
    default:
        System.out.println("Geçersiz gün");
}
```

`✅ break kullanmazsan tüm case’ler akmaya başlar (fall-through problemi).`

## ☕ Java 14+ ile switch expression

Yeni nesil switch yapısı daha modern ve expression bazlıdır:

```java
String result = switch (gun) {
    case 1 -> "Pazartesi";
    case 2 -> "Salı";
    case 3 -> "Çarşamba";
    default -> "Geçersiz";
};
```

## 💼 Kurumsal Best Practice

- ✅ Her koşul bloğu için else veya default yaz.
- ✅ Karmaşık if-else yapılarında guard clause yaklaşımını kullan:

```java
if (user == null) return;

if (!user.isActive()) return;

processUser(user);
```

- ✅ switch içinde enum kullanımı daha güvenlidir:

```java
enum Role { ADMIN, USER, GUEST }

Role role = Role.ADMIN;

switch (role) {
    case ADMIN -> System.out.println("Admin panel");
    case USER  -> System.out.println("Kullanıcı paneli");
    case GUEST -> System.out.println("Giriş yapınız");
}
```

