# 🧩 Method Chaining (Metot Zincirleme)

## 🔍 1. Nedir?

Method Chaining, bir nesne üzerinde birden fazla metodu noktalarla `(.)` arka arkaya çağırarak zincirleme bir şekilde çalıştırma tekniğidir.

```java
kullanici.setIsim("Ali")
         .setSoyisim("Yılmaz")
         .setYas(28);
```

Metotlar `this` referansını döndürdüğü sürece zincir uzar.

## 🧠 2. Neden Kullanılır?

| Fayda                          | Açıklama                                           |
| ------------------------------ | -------------------------------------------------- |
| ✅ Akıcı API (Fluent Interface) | Daha doğal ve okunabilir kod                       |
| ✅ Tek satırda çok iş           | Az satır, daha fazla ifade gücü                    |
| ✅ Builder Pattern ile uyumlu   | Nesne üretimini sadeleştirir                       |
| ✅ Immutable sınıflarla uyumlu  | Yeni nesne döndürme stratejileriyle kullanılabilir |


## 🔧 3. Nasıl Uygulanır?

### 3.1. Standart Setter vs Chaining

`Klasik yaklaşım:`

```java
Kullanici k = new Kullanici();
k.setIsim("Ali");
k.setYas(30);
k.setEmail("ali@x.com");
```

`Method Chaining ile:`

```java
Kullanici k = new Kullanici()
                .setIsim("Ali")
                .setYas(30)
                .setEmail("ali@x.com");
```

### 3.2. Şart: Setter’lar this döndürmeli

```java
public class Kullanici {
    private String isim;
    private int yas;
    
    public Kullanici setIsim(String isim) {
        this.isim = isim;
        return this;
    }

    public Kullanici setYas(int yas) {
        this.yas = yas;
        return this;
    }
}
```

`return this;` metot sonunda yazılmalı ki aynı nesneyle zincir devam edebilsin.

## 🧱 4. Gerçekçi Örnek: Builder Pattern ile Chaining

```java
public class Post {
    private String baslik;
    private String icerik;
    
    public Post setBaslik(String baslik) {
        this.baslik = baslik;
        return this;
    }

    public Post setIcerik(String icerik) {
        this.icerik = icerik;
        return this;
    }
}
```

`Kullanım:`

```java
Post post = new Post()
                .setBaslik("Yeni Blog")
                .setIcerik("Bu bir içeriktir.");
```

## 🧬 5. Fluent Interface ile Method Chaining

Fluent Interface, method chaining'in bir üst kavramıdır. Deyimsel ve "doğal okunuşlu" API tasarımıdır.

```java
new QueryBuilder()
    .select("isim", "soyisim")
    .from("kullanicilar")
    .where("yas > 18")
    .orderBy("isim")
    .build();
```

## ⚠️ 6. Dikkat Edilmesi Gerekenler

| Risk                      | Açıklama                                               |
| ------------------------- | ------------------------------------------------------ |
| ❌ Null referans           | Zincir bozulur: `NullPointerException`                 |
| ❌ Immutable yapılarda zor | Değişmez nesnelerde `return new` yaklaşımı gerekir     |
| ❌ Debug zorluğu           | Zincirin ortasında hata varsa izole etmek zorlaşır     |
| ❌ Karmaşık zincirler      | Kod okunabilirliğini bozabilir, max 4-5 metot önerilir |


## ✅ 7. Best Practice Önerileri

| Öneri                            | Açıklama                                   |
| -------------------------------- | ------------------------------------------ |
| Setter yerine chaining kullan    | Özellikle POJO nesnelerinde                |
| `return this` kullanmayı unutma  | Zincirin devamı için şart                  |
| Metotlar anlamlı isimler almalı  | `withX()`, `addY()` gibi                   |
| FluentBuilder pattern uygula     | Constructor yerine builder ile başla       |
| IDE’de zincir satırlarını hizala | Okunabilirlik için alt alta yazım önerilir |


## 🚀 8. Modern Kullanım: Lombok ile @Accessors(chain = true)

`Lombok` kütüphanesi ile method chaining otomatik sağlanabilir:

```java
@Getter
@Setter
@Accessors(chain = true)
public class Kullanici {
    private String isim;
    private int yas;
}
```

```java
Kullanici k = new Kullanici()
                    .setIsim("Ayşe")
                    .setYas(25);
```

## 📌 10. Örnek: Custom QueryBuilder

```java
public class QueryBuilder {
    private String query = "";

    public QueryBuilder select(String... fields) {
        query += "SELECT " + String.join(", ", fields) + " ";
        return this;
    }

    public QueryBuilder from(String table) {
        query += "FROM " + table + " ";
        return this;
    }

    public QueryBuilder where(String condition) {
        query += "WHERE " + condition + " ";
        return this;
    }

    public String build() {
        return query.trim() + ";";
    }
}
```

`Kullanımı:`

```java
String sql = new QueryBuilder()
                .select("id", "ad")
                .from("kullanicilar")
                .where("yas > 18")
                .build();

System.out.println(sql);
// OUTPUT: SELECT id, ad FROM kullanicilar WHERE yas > 18;
```

