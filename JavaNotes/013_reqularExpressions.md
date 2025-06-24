# 🔍 Java Regular Expressions (Regex) – Kurumsal Seviye Detaylar

## 1️⃣ Regex Nedir?

Regular Expressions, metinlerde belirli kalıpları eşleştirmek için kullanılan bir şablon dilidir. Java'da özellikle:

- Input Validation (e-posta, telefon, şifre)
- Log Parsing
- Veri temizleme
- Template Matching
- Metin madenciliği

için yoğun şekilde kullanılır.

## 2️⃣ Java’da Regex Yapısı

Java’da `regex` ile çalışmak için iki temel sınıf kullanılır:

| Sınıf     | Açıklama                             |
| --------- | ------------------------------------ |
| `Pattern` | Regex şablonunu derler               |
| `Matcher` | Pattern'ı bir metin üzerinde uygular |


### ✅ Örnek Kullanım

```java
import java.util.regex.*;

public class RegexExample {
    public static void main(String[] args) {
        String metin = "Merhaba, mailim test@example.com";
        Pattern pattern = Pattern.compile("\\b\\w+@\\w+\\.\\w+\\b");
        Matcher matcher = pattern.matcher(metin);

        while (matcher.find()) {
            System.out.println("Eşleşen email: " + matcher.group());
        }
    }
}
```

## 3️⃣ Regex Sembolleri

__Karakter Sınıfları:__

| Sembol  | Anlamı                  | Örnek             |
| ------- | ----------------------- | ----------------- |
| `.`     | Herhangi bir karakter   | `a.c` → `abc`     |
| `\d`    | Sayı (0–9)              | `\d{2}` → `23`    |
| `\w`    | Harf, rakam, alt çizgi  | `\w+` → `abc_123` |
| `\s`    | Boşluk karakteri        | `\s+`             |
| `[...]` | Belirli karakter kümesi | `[abc]` → `a`     |


__Tekrarlayıcılar:__

| Sembol  | Anlamı                  | Örnek            |
| ------- | ----------------------- | ---------------- |
| `*`     | 0 veya daha fazla       | `a*`             |
| `+`     | 1 veya daha fazla       | `a+`             |
| `?`     | 0 veya 1 kere           | `a?`             |
| `{n}`   | n kez                   | `\d{4}` → `2024` |
| `{n,}`  | en az n kez             | `a{3,}`          |
| `{n,m}` | en az n, en fazla m kez | `a{2,4}`         |


__Sınırlar:__

| Sembol | Anlamı        |
| ------ | ------------- |
| `^`    | Satır başı    |
| `$`    | Satır sonu    |
| `\b`   | Kelime sınırı |


## 4️⃣ Pattern Flags (Modlar)

| Flag                       | Anlamı                                          |
| -------------------------- | ----------------------------------------------- |
| `Pattern.CASE_INSENSITIVE` | Büyük/küçük harf duyarsızlığı                   |
| `Pattern.MULTILINE`        | Satır satır eşleştirme                          |
| `Pattern.DOTALL`           | `.` her karakteri (yeni satır dahil) eşleştirir |


```java
Pattern p = Pattern.compile("java", Pattern.CASE_INSENSITIVE);
```

## 5️⃣ Regex ile Replace, Split, Matches

```java
String text = "123-456-7890";

// Doğrudan eşleşme kontrolü
System.out.println(text.matches("\\d{3}-\\d{3}-\\d{4}")); // true

// Bölme
String[] parts = text.split("-");
System.out.println(Arrays.toString(parts)); // [123, 456, 7890]

// Değiştirme
String hidden = text.replaceAll("\\d", "*");
System.out.println(hidden); // ***-***-****
```

## 6️⃣ Kurumsal Senaryolar

| Senaryo             | Regex Kalıbı                                                         |
| ------------------- | -------------------------------------------------------------------- |
| E-posta doğrulama   | `\\b\\w+@\\w+\\.\\w+\\b`                                             |
| TC Kimlik doğrulama | `^[1-9]{1}[0-9]{9}[02468]{1}$`                                       |
| IPv4 adresi         | `\\b(\\d{1,3}\\.){3}\\d{1,3}\\b`                                     |
| Telefon numarası    | `\\+?90[ -]?[1-9]{1}[0-9]{2}[ -]?[0-9]{3}[ -]?[0-9]{2}[ -]?[0-9]{2}` |


## 7️⃣ Regex Performance & Best Practices

- Pattern compile edildikten sonra cache'lenmeli.
- Aşırı karmaşık regex’lerden kaçınılmalı. Regex Engine CPU sömürür.
- Gelişmiş uygulamalarda regex testleri yapılmalı → regex101.com
- Log ve input verilerinde güvenlik için dikkatli olunmalı (ReDoS saldırıları).

## 8️⃣ Java 9+ Yenilikleri

Java 9 ile `Matcher::results()` methodu geldi __→ Stream API__ ile entegre regex aramaları yapılabilir:

```java
Pattern p = Pattern.compile("\\d+");
Matcher m = p.matcher("12 ab 34 cd 56");

List<String> matches = m.results()
    .map(MatchResult::group)
    .collect(Collectors.toList());

System.out.println(matches); // [12, 34, 56]
```

## 🚀 Özet: Regex = Güç + Tehlike

| Artı Yönler                           | Dikkat Gereken Noktalar                |
| ------------------------------------- | -------------------------------------- |
| Metin işleme ve doğrulamada süper     | Okunabilirliği düşük olabilir          |
| Hızlı veri filtreleme sağlar          | Performans tuzaklarına dikkat edilmeli |
| Pattern compile + matcher mantığı net | Regex hataları sessizce çalışabilir    |


