# 📌 Java Annotations – Derinlemesine Teknik İnceleme

## 1️⃣ Annotations Nedir?

- Java’da metadata (veri hakkında veri) sağlayan özel yapı.
- Kodun üzerine eklenir, derleyiciye, araçlara veya runtime’a ekstra bilgi verir.
- Kodun davranışını veya işleyişini değiştirmez, ancak framework ve kütüphane altyapılarında kritik rol oynar.
- Kurumsal projede otomasyon, konfigürasyon ve kodun kendini ifade etmesi için vazgeçilmezdir.

## 2️⃣ Annotations’ın Temel İşlevleri

- Derleyiciye bilgi verme: Örneğin, `@Override` ile derleyiciye “bu metot üst sınıfın metodunu ezmektedir” diyorsun.

- Kod analiz ve doğrulama: Örneğin, `@Deprecated` ile “bu metodun kullanımı önerilmez” sinyali.

- Runtime işlem için veri sağlama: Özellikle frameworklerde (Spring, Hibernate) kullanılır.

- Kodun okunabilirliğini ve bakımını artırma.

## 3️⃣ Yaygın Kullanılan Java Annotations

| Annotation             | Kullanım Amacı                                       |
| ---------------------- | ---------------------------------------------------- |
| `@Override`            | Üst sınıftan metodun geçersiz kılındığını belirtir   |
| `@Deprecated`          | Kodun kullanımının sonlandırıldığını bildirir        |
| `@SuppressWarnings`    | Derleyici uyarılarını bastırmak için                 |
| `@FunctionalInterface` | Tek metotlu arayüz olduğunu belirtir                 |
| `@SafeVarargs`         | Varargs tipi kullanımı ile ilgili uyarıları engeller |


## 4️⃣ Annotation Sınıfı Nasıl Yazılır?

Kendi annotation’ını tanımlamak için:

```java
import java.lang.annotation.*;

@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface Audit {
    String value() default "UserAction";
}
```

- `@Retention:` Annotations’ın ne zaman kullanılacağını belirtir (SOURCE, CLASS, RUNTIME).

- `@Target:` Annotation’ın nerede kullanılacağını sınırlar (method, field, type vs).

- `Metot benzeri yapı:` Annotation içindeki değerler parametre gibi tanımlanır.

## Framework ve Kütüphanelerde Annotations Kullanımı

- __Spring:__ `@Controller`, `@Service`, `@Autowired`, `@RequestMapping` gibi IoC ve MVC için kritik.

- __JPA/Hibernate:__ `@Entity`, `@Table`, `@Column`, `@Id` gibi ORM yönetiminde.

- __JUnit:__ `@Test`, `@Before`, `@After` test yaşam döngüsü kontrolü için.

- __Lombok:__ `@Data`, `@Builder` gibi boilerplate’i azaltmak için.


## Reflection ile Annotations Okuma

Runtime’da annotation bilgisine erişmek için reflection kullanılır:

```java
Method method = MyClass.class.getMethod("myMethod");
if (method.isAnnotationPresent(Audit.class)) {
    Audit audit = method.getAnnotation(Audit.class);
    System.out.println("Audit value: " + audit.value());
}
```

## Kurumsal İyi Pratikler

- Annotations’ı gereksiz yere abartma, sadece anlamlı yerlerde kullan.
- Kodun okunabilirliğini ve bakımını olumsuz etkileyecek karmaşıklıktan kaçın.
- Annotation parametrelerine anlamlı default değerler ver.
- Kodda annotation kullanımını belgeleyip standartlaştır (örneğin şirket içi kod kuralları).
- Framework ve kütüphane entegrasyonlarında annotation tabanlı konfigürasyonu tercih et.



