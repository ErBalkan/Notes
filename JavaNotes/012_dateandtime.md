# ⏰ Java Date and Time – Kurumsal Ölçekte Modern Zaman Yönetimi

## 1️⃣ Tarih ve Zaman Yönetimi Neden Kritik?

- Zaman, veri bütünlüğü, logging, scheduling, auditing gibi birçok kurumsal süreçte temel bileşen.

- Yanlış zaman yönetimi, hatalı raporlama, veri tutarsızlığı, güvenlik açıkları yaratır.

- Farklı zaman dilimleri ve kültürlere uyum zorunluluğu vardır.

## java.time Paketi

| Sınıf               | Açıklama                                       |
| ------------------- | ---------------------------------------------- |
| `LocalDate`         | Tarih (Yıl, Ay, Gün) - saat yok                |
| `LocalTime`         | Zaman (Saat, Dakika, Saniye) - tarih yok       |
| `LocalDateTime`     | Tarih ve zaman birleşimi (saat dilimi yok)     |
| `ZonedDateTime`     | Tarih, zaman ve saat dilimi (timezone)         |
| `Instant`           | UTC tabanlı anlık zaman (epoch time)           |
| `Duration`          | İki zaman arasındaki süre (saniye, nanosaniye) |
| `Period`            | İki tarih arasındaki süre (yıl, ay, gün)       |
| `DateTimeFormatter` | Tarih ve zaman formatlama/parse işlemleri      |

## Temel Kullanım Örnekleri

### LocalDate – Tarih

```java
LocalDate today = LocalDate.now();
LocalDate specificDate = LocalDate.of(2025, Month.JUNE, 23);
```

### LocalTime – Zaman

```java
LocalTime now = LocalTime.now();
LocalTime specificTime = LocalTime.of(14, 30, 0);
```

### LocalDateTime – Tarih ve Zaman

```java
LocalDateTime now = LocalDateTime.now();
LocalDateTime specific = LocalDateTime.of(2025, 6, 23, 14, 30);
```

### ZonedDateTime – Zaman Dilimi ile

```java
ZonedDateTime zdt = ZonedDateTime.now(ZoneId.of("Europe/Istanbul"));
```

## Özet Tablo

| Sınıf           | Kullanım Amacı               | Özellik                        |
| --------------- | ---------------------------- | ------------------------------ |
| `LocalDate`     | Yıl, ay, gün - tarih         | Saat bilgisi yok               |
| `LocalTime`     | Saat, dakika, saniye - zaman | Tarih bilgisi yok              |
| `LocalDateTime` | Tarih + zaman birleşimi      | Saat dilimi yok                |
| `ZonedDateTime` | Tarih + zaman + saat dilimi  | Global uygulamalar için kritik |
| `Instant`       | Epoch tabanlı anlık zaman    | UTC standart                   |


