# 🧩 Java Interface — Bağlantı Noktası, Sözleşme, Soyutlama Aracı

## 📌 1. Interface Nedir?

`interface`, bir sınıfın __uygulaması gereken davranışların imzasını__ tanımlar. Herhangi bir gövde (body) içermez (Java 8’den önce), sadece “ne yapılacağını” söyler, “nasıl yapılacağını” söylemez.

### 🎯 Tanım:

"Interface, bir sözleşmedir. Bu sözleşmeye uyan sınıf, tüm davranışları eksiksiz sağlar."

## 📚 Arayüzler Ne Zaman Kullanılır?

* Servis, DAO, Controller gibi bileşenlerde
* Spring gibi framework'lerde bean tanımlarında
* Bağımlılığı ters çevirmek (DIP) için
* Test/mock yazmak için

## 🧩 Interface ile Çoklu Kalıtım

Java’da çoklu sınıf kalıtımı yoktur, ama çoklu interface implementasyonu serbesttir.

```java
interface Ucan {
    void havalan();
}

interface Yuruyen {
    void yuru();
}

class Kus implements Ucan, Yuruyen {
    public void havalan() { ... }
    public void yuru() { ... }
}
```

## 🔄 Interface vs Abstract Class

| Özellik        | Interface                        | Abstract Class              |
| -------------- | -------------------------------- | --------------------------- |
| Çoklu kalıtım  | ✅                                | ❌                           |
| Constructor    | ❌                                | ✅                           |
| Metot türleri  | public abstract (default/statik) | abstract, concrete          |
| Değişkenler    | `public static final`            | Her türden olabilir         |
| Kullanım amacı | Sözleşme                         | Temel davranış + ortak yapı |
| State tutma    | Hayır                            | Evet                        |


## 🔧 Interface Kullanımında Best Practices

| Pratik                                        | Açıklama                              |
| --------------------------------------------- | ------------------------------------- |
| Arayüzleri ihtiyaç bazlı ayır                 | SRP ve ISP’ye uygun tasarla           |
| Arayüz isimleri net olsun                     | `CustomerService`, `Repository` gibi  |
| Arayüzü servisin dışına koy                   | `application` veya `domain` katmanına |
| Yalnızca davranış tanımla                     | State barındırma yok                  |
| Uygulama sınıfını değiştirmeden kodu geliştir | Kod tekrarını önle                    |


## 🔒 Sealed Interface (Java 15+)

```java
public sealed interface Sekil
    permits Daire, Kare {}
```

```
Bu yapı, hangi sınıfların bu interface'i implement edebileceğini sınırlamak için kullanılır.
```

## 🧰 Spring Framework’te Interface Kullanımı

```java
public interface ProductService {
    void save(Product product);
}
```

```java
@Service
public class ProductServiceImpl implements ProductService {
    public void save(Product product) {
        // DB işlemleri
    }
}
```

Spring arayüzü inject eder, implementasyonu değiştirsen bile sistem bozulmaz.

