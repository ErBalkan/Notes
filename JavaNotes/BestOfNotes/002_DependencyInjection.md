# 🔍 Giriş: Dependency Injection Nedir?

__Dependency Injection (Bağımlılıkların Enjekte Edilmesi)__, bir sınıfın ihtiyaç duyduğu diğer sınıfları (bağımlılıklarını) kendisi oluşturmadan, dışarıdan almasını sağlayan bir tasarım desenidir. Bu desenin amacı:

- Gevşek bağlı (loose coupling) kod yazmak.

- Test edilebilirliği artırmak.

- Sürdürülebilir ve genişletilebilir bir sistem inşa etmek.

## 🎯 Neden Dependency Injection?

Normalde bir sınıf bağımlılıklarını şöyle alır:

```java
public class OrderService {
    private final PaymentService paymentService = new PaymentService();
}
```

Yukarıdaki örnekte, `OrderService` doğrudan `PaymentService’i` oluşturuyor. Bu:

1. Sıkı bağlılık (tight coupling) yaratır.

2. Testi zorlaştırır.

3. Genişletilebilirliği azaltır.

## Doğrusu nedir?

```java
public class OrderService {
    private final PaymentService paymentService;

    public OrderService(PaymentService paymentService) {
        this.paymentService = paymentService;
    }
}
```

Artık __OrderService__ bağımlılığını dışarıdan alıyor. Bu, Dependency Injection’ın temelidir.

## ⚙️ Spring Framework'te DI Nasıl Çalışır?

__Spring__, bir `IoC Container (Inversion of Control Container)` kullanır. Bu __container:__

- Uygulamadaki nesneleri (bean’leri) oluşturur,

- Bağımlılıklarını belirler,

- Bağımlılıkları otomatik olarak enjekte eder.

## 🧱 Spring Boot’ta Bean Kavramı

__Spring context__ tarafından yönetilen nesnelere `bean` denir. Bean’ler 3 yolla tanımlanır:

### 1. @Component Anotasyonu ile

```java
@Component
public class PaymentService {
    public void processPayment() { /*...*/ }
}
```

### 2. @Service, @Repository, @Controller Özel Component’lerdir

```java
@Service
public class OrderService { }
```

### 3. @Configuration + @Bean

```java
@Configuration
public class AppConfig {

    @Bean
    public PaymentService paymentService() {
        return new PaymentService();
    }
}
```

## 💉 Spring’de Dependency Injection Yöntemleri

### 1. Constructor Injection ✅ En çok önerilen

```java
@Service
public class OrderService {

    private final PaymentService paymentService;

    @Autowired
    public OrderService(PaymentService paymentService) {
        this.paymentService = paymentService;
    }
}
```

```
Spring 4.3+ itibarıyla sınıf tek bir constructor’a sahipse, @Autowired yazmaya gerek yoktur.
```

### 2. Field Injection ❌ Antipattern, test edilemezlik nedeniyle önerilmez

```java
@Service
public class OrderService {

    @Autowired
    private PaymentService paymentService;
}
```

### 3. Setter Injection 🔄 Opsiyonel bağımlılıklar için ideal

```java
@Service
public class OrderService {

    private PaymentService paymentService;

    @Autowired
    public void setPaymentService(PaymentService paymentService) {
        this.paymentService = paymentService;
    }
}
```

## 🔄 Scope Kavramı: Bean’in Yaşam Süresi

Spring bean’leri farklı scope’larda olabilir:

1. `singleton:` (default) her istek için aynı instance.

2. `prototype:` her kullanımda yeni instance.

3. `request, session:` web uygulamaları için özel scope’lar.

```java
@Component
@Scope("prototype")
public class PaymentService {
}
```

## 🧠 Arka Planda Ne Oluyor? (Spring’in İç Mekanizması)

1. Spring context çalıştığında tüm bean’leri tarar (component scan).
2. Bean’leri ApplicationContext içine alır.
3. Hangi bean’in neye ihtiyacı olduğunu analiz eder.
4. İhtiyaçları otomatik olarak enjekte eder.
5. Singleton bean’leri önceden oluşturur (eager init).

## 🧪 Test Edilebilirlik Avantajı

`Constructor injection`, Spring testlerinde __mock bean__’lerin kolayca verilmesini sağlar:

```java
@Test
public void testOrderService() {
    PaymentService mockPayment = Mockito.mock(PaymentService.class);
    OrderService orderService = new OrderService(mockPayment);
}
```

## 🧭 Best Practices (Kurumsal Yaklaşım)

| Pratik                                  | Açıklama                                                     |
| --------------------------------------- | ------------------------------------------------------------ |
| Constructor Injection                   | Daima tercih edilmelidir.                                    |
| Interface Tabanlı Gelişim               | Servisleri interface üzerinden yönetin.                      |
| `@Primary` / `@Qualifier` Kullanımı     | Çoklu bean durumlarında kullan.                              |
| `@Lazy`, `@Scope`, `@Profile` Kullanımı | Ortama göre yönetilebilir yapı sağlar.                       |
| Circular dependency'den kaçın           | Gerekiyorsa event’ler ya da başka design pattern’ler kullan. |


## 🔚 Özetle

__Dependency Injection__, Spring Boot’ta işin kalbidir. Projeyi modüler, test edilebilir ve sürdürülebilir hale getirir.

Spring Boot bu işi senin yerine yapar ama anlamadan yazarsan ileride duvara toslarsın. __DI__ konusunu içselleştirmeden Spring’te ileri seviye işler yapılamaz.

