# VALIDATION

## 🔷 1. Validation Nedir?

Validation, kullanıcıdan (veya dış sistemden) gelen verilerin:

- Uygun formatta,

- Gerekli alanların dolu,

- İş kurallarına uygun

olup olmadığını kontrol etme işlemidir.

Spring Boot’ta bu işlemler genelde:

- `javax.validation` (JSR 380 – Bean Validation 2.0)

- `jakarta.validation` (Spring 6 ve sonrası)

- `Hibernate Validator` (Default Spring Boot implementation)

tarafından sağlanır.

## 🔷 2. Spring Boot'ta Validation Mimarisine Genel Bakış

Spring Boot’ta validation genellikle şu yapının bir parçası olur:

```less
@Controller / @RestController
     ↓
@Valid veya @Validated
     ↓
DTO (Data Transfer Object)
     ↓
Anotasyonlar (@NotNull, @Size, @Email vs.)
     ↓
Hibernate Validator (engine)
```

## 🔷 3. Gerekli Bağımlılıklar

### Maven:

```xml
<!-- Spring Boot starter validation -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

```
Spring Boot 2.3+ sürümlerinde bu starter bağımlılığı jakarta.validation (önceki adıyla javax.validation) içerir.
```

## 🔷 4. DTO Üzerinde Validation Anotasyonları

DTO katmanında (request-body karşılayan sınıf) anotasyonları kullanarak validation yapılır:

### Örnek DTO:

```java
import jakarta.validation.constraints.*;

public class UserRequest {

    @NotNull(message = "İsim boş olamaz")
    @Size(min = 2, max = 50, message = "İsim 2 ile 50 karakter arasında olmalı")
    private String name;

    @Email(message = "Geçersiz e-posta formatı")
    private String email;

    @NotNull(message = "Yaş zorunludur")
    @Min(value = 18, message = "Yaş en az 18 olmalı")
    @Max(value = 65, message = "Yaş en fazla 65 olmalı")
    private Integer age;

    // getter-setter
}
```

## 🔷 5. Controller Üzerinde @Valid Kullanımı

```java
@RestController
@RequestMapping("/api/users")
public class UserController {

    @PostMapping
    public ResponseEntity<String> createUser(@RequestBody @Valid UserRequest userRequest) {
        // Eğer valid değilse otomatik olarak 400 hatası fırlatılır
        return ResponseEntity.ok("Kullanıcı başarıyla oluşturuldu");
    }
}
```

__🔹 Burada `@Valid`, `Java Bean Validation` mekanizmasını tetikler. Eğer `UserRequest` sınıfı geçersizse, framework `MethodArgumentNotValidException` fırlatır.__

## 🔷 6. Hataları Yakalama – @ControllerAdvice

__Custom hata mesajlarını kontrol etmek için global bir `exception handler` yazılır:__

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<Map<String, String>> handleValidationException(MethodArgumentNotValidException ex) {
        Map<String, String> errors = new HashMap<>();
        ex.getBindingResult().getFieldErrors().forEach(error -> {
            errors.put(error.getField(), error.getDefaultMessage());
        });
        return new ResponseEntity<>(errors, HttpStatus.BAD_REQUEST);
    }
}
```

## 🔷 7. Anotasyon Türleri – Tüm Validation Kuralları

| Anotasyon                                                      | Açıklama                                 |
| -------------------------------------------------------------- | ---------------------------------------- |
| `@NotNull`                                                     | Null olamaz (ama boş string olabilir)    |
| `@NotBlank`                                                    | Null veya boş string olamaz              |
| `@NotEmpty`                                                    | Boş koleksiyon/array/string olamaz       |
| `@Size(min, max)`                                              | Karakter uzunluğu veya koleksiyon boyutu |
| `@Min(value)`                                                  | Sayısal minimum değer                    |
| `@Max(value)`                                                  | Sayısal maksimum değer                   |
| `@Email`                                                       | E-posta format kontrolü                  |
| `@Pattern(regex)`                                              | Regex ile özel format doğrulama          |
| `@AssertTrue` / `@AssertFalse`                                 | Boolean kontroller                       |
| `@Past` / `@Future`                                            | Tarih kontrolleri (geçmiş/gelecek)       |
| `@Digits(integer, fraction)`                                   | Sayının integer ve ondalık kısmı sınırı  |
| `@Positive`, `@Negative`, `@PositiveOrZero`, `@NegativeOrZero` | Sayısal işaret doğrulamaları             |


## 🔷 8. @Validated vs @Valid Farkı

| Özellik           | @Valid                   | @Validated                                            |
| ----------------- | ------------------------ | ----------------------------------------------------- |
| Kaynak            | `javax.validation.Valid` | `org.springframework.validation.annotation.Validated` |
| Nerede kullanılır | Parametre, DTO sınıfları | Controller class veya method seviyesinde              |
| Gruplama desteği  | Yok                      | Var (advanced senaryolar)                             |


## 🔷 9. Gelişmiş Konu: Validation Groups

__Örneğin: `CreateUser` için farklı, `UpdateUser` için farklı kurallar istiyorsan:__


```java
public interface Create {}
public interface Update {}

public class UserDto {
    @NotNull(groups = Update.class)
    private Long id;

    @NotBlank(groups = {Create.class, Update.class})
    private String name;
}
```

```java
@PostMapping
public ResponseEntity<?> createUser(@Validated(Create.class) @RequestBody UserDto dto) { ... }

@PutMapping
public ResponseEntity<?> updateUser(@Validated(Update.class) @RequestBody UserDto dto) { ... }
```

## 🔷 10. Özelleştirilmiş Validation – Custom Annotation

### 1. Anotasyon Tanımı:

```java
@Documented
@Constraint(validatedBy = CustomNameValidator.class)
@Target({ElementType.FIELD})
@Retention(RetentionPolicy.RUNTIME)
public @interface ValidName {
    String message() default "İsim geçersiz";
    Class<?>[] groups() default {};
    Class<? extends Payload>[] payload() default {};
}
```

### 2. Validator Sınıfı:

```java
public class CustomNameValidator implements ConstraintValidator<ValidName, String> {

    @Override
    public boolean isValid(String value, ConstraintValidatorContext context) {
        return value != null && value.matches("^[A-Z][a-z]{2,}$"); // İlk harf büyük, min 3 harf
    }
}
```

## 🔷 11. Spring Boot Properties ile Validation Konfigürasyonu

`application.properties` veya `application.yml` dosyasına aşağıdaki konfigürasyon eklenebilir:

```properties
# Hata mesajlarında field name’leri göster
spring.mvc.log-request-details=true

# Varsayılan validation mesaj kaynağını tanımlamak
spring.messages.basename=messages
```

## 🔷 12. Validation Mesajlarını Özelleştirme (i18n / messages.properties)

### resources/messages.properties:

```properties
user.name.notnull=İsim zorunludur
user.email.invalid=Geçersiz e-posta
```

__DTO’da:__

```java
@NotNull(message = "{user.name.notnull}")
@Email(message = "{user.email.invalid}")
```

## 🔷 13. En İyi Pratikler

- ✅ Her zaman DTO üzerinde validation yap, Entity sınıfını validation için kullanma.
- ✅ Hataları `@ControllerAdvice` ile merkezi şekilde yönet.
- ✅ Gerektiğinde custom annotation yaz, business logic validation için.
- ✅ Validation Groups ile farklı senaryoları ayrıştır.
- ✅ Kullanıcı dostu mesajlar sun, i18n desteği ekle.

