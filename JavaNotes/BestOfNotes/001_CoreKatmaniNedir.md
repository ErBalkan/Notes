# 🔍 1. CORE KATMANI NEDİR?

__Core (çekirdek)__ katmanı, yazılımın altyapısal ve temel işlevlerini sağlayan soyut yapıları, ortak bileşenleri ve sistem genelinde kullanılan util sınıflarını içerir. Genellikle şu bileşenler yer alır:

| Bileşen                    | Açıklama                                                                   |
| -------------------------- | -------------------------------------------------------------------------- |
| 🔸 `BaseEntity`            | Tüm varlıkların (entity) kalıtım alacağı temel sınıf                       |
| 🔸 `BaseResponse`          | API'lerin döneceği ortak response yapısı                                   |
| 🔸 `Result`/`DataResult`   | İşlemlerin başarılı/başarısız olduğunu anlamak için kullanılan sarmal yapı |
| 🔸 `CustomException`       | Proje genelinde kullanılacak özelleştirilmiş hata yapıları                 |
| 🔸 `ExceptionHandler`      | Global hata yakalama mekanizması                                           |
| 🔸 `MapperConfig`          | MapStruct gibi mapping kütüphanelerinin temel ayarları                     |
| 🔸 `Constants`, `Messages` | Sabitler ve ortak mesajlar                                                 |
| 🔸 `Utilities`             | Tarih, string işlemleri vb. tool sınıflar                                  |


```
💡 Core katmanını bir framework gibi düşünebilirsin. Diğer modüller bu katmana bağımlı olabilir ama core, hiçbir katmana bağımlı olmamalıdır. Tek yönlü bağımlılık.
```

## 🎯 2. NE İŞE YARAR?

| FAYDA                               | AÇIKLAMA                                                   |
| ----------------------------------- | ---------------------------------------------------------- |
| ✅ **Kod Tekrarını Engeller**        | Ortak yapılar tek yerde tanımlanır                         |
| ✅ **Katmanlı Mimariyi Güçlendirir** | Her katmanın görevi ayrılır, bağımlılıklar netleşir        |
| ✅ **Bakımı Kolaylaştırır**          | Değişiklik yapılması gereken kodlar merkezi hale gelir     |
| ✅ **Test Edilebilirliği Artırır**   | Soyut yapıların kullanımıyla bağımlılıklar azalır          |
| ✅ **Kurumsal Standartları Sağlar**  | Core katmanı yazmak kurumsal dünyada bir best practice’tir |


## 🏗️ 3. CORE KATMANI NASIL YAZILIR?

### 3.1. 📁 Klasör Yapısı (Minimum)

```text
src
└── main
    └── java
        └── com.example.core
            ├── base
            │   ├── BaseEntity.java
            │   ├── BaseDto.java
            │   └── BaseResponse.java
            ├── exception
            │   ├── BusinessException.java
            │   ├── GlobalExceptionHandler.java
            │   └── ErrorResponse.java
            ├── result
            │   ├── Result.java
            │   ├── SuccessResult.java
            │   ├── ErrorResult.java
            │   ├── DataResult.java
            │   └── SuccessDataResult.java
            ├── constants
            │   └── Messages.java
            └── utils
                └── DateUtil.java
```

## 🧱 4. ÖRNEK BİLEŞENLERLE ANLATIM

### 4.1. BaseEntity.java

```java
@MappedSuperclass
public abstract class BaseEntity {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private LocalDateTime createdAt = LocalDateTime.now();
    private LocalDateTime updatedAt;
}
```

__🔹 Tüm @Entity sınıflar bu sınıftan türetilir. ID ve zaman bilgisi hep ortaktır.__

### 4.2. BaseResponse.java

```java
public class BaseResponse<T> {
    private boolean success;
    private String message;
    private T data;

    public BaseResponse(boolean success, String message, T data) {
        this.success = success;
        this.message = message;
        this.data = data;
    }

    // Getters, Setters
}
```

__🔹 API response'larının ortak kalıba oturmasını sağlar.__

### 4.3. Result.java ve Türevleri

```java
public class Result {
    private boolean success;
    private String message;

    public Result(boolean success, String message) {
        this.success = success;
        this.message = message;
    }
}

public class SuccessResult extends Result {
    public SuccessResult(String message) {
        super(true, message);
    }
}

public class ErrorResult extends Result {
    public ErrorResult(String message) {
        super(false, message);
    }
}
```

__🔹 Her servis metodunun başarılı mı başarısız mı olduğunu anlamak için kullanılır. Response gibi ama daha sade.__

### 4.4. BusinessException.java

```java
public class BusinessException extends RuntimeException {
    public BusinessException(String message) {
        super(message);
    }
}
```

__🔹 Örneğin: Aynı email ile kayıt olmaya çalışılırsa bu exception fırlatılır.__

### 4.5. GlobalExceptionHandler.java

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(BusinessException.class)
    public ResponseEntity<ErrorResponse> handleBusinessException(BusinessException ex) {
        ErrorResponse response = new ErrorResponse("BUSINESS_ERROR", ex.getMessage());
        return new ResponseEntity<>(response, HttpStatus.BAD_REQUEST);
    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorResponse> handleException(Exception ex) {
        ErrorResponse response = new ErrorResponse("SYSTEM_ERROR", "Unexpected error occurred.");
        return new ResponseEntity<>(response, HttpStatus.INTERNAL_SERVER_ERROR);
    }
}
```

__🔹 Tüm projedeki exception’ları yakalar ve merkezi şekilde yönetir.__

### 4.6. Messages.java

```java
public class Messages {
    public static final String USER_NOT_FOUND = "Kullanıcı bulunamadı.";
    public static final String EMAIL_ALREADY_EXISTS = "Bu e-posta adresi zaten kayıtlı.";
}
```

__🔹 Tüm mesajlar tek yerden yönetilir. Kod içinde hardcoded string yerine sabit kullanılır.__

### 4.7. DateUtil.java

```java
public class DateUtil {
    public static String formatDate(LocalDateTime date) {
        return date.format(DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm"));
    }
}
```

__🔹 Her yerde tarih formatlaması gerektiğinde tek bir yerden yapılır.__

## 🧠 5. BEST PRACTICE’LER

| Best Practice                         | Açıklama                                                                      |
| ------------------------------------- | ----------------------------------------------------------------------------- |
| 🔒 Core katmanı dışa bağımlı olmamalı | Hiçbir başka modüle bağımlı olmamalı. Kendisi bağımsız çalışmalı.             |
| ♻️ Reusable bileşenler olmalı         | Başka projelerde de kullanılabilir şekilde modüler yazılmalı.                 |
| 💬 Sabitler dışarı taşınmalı          | Magic string veya hardcoded mesajlar `Messages.java` gibi sınıflara alınmalı. |
| 📁 Temiz klasör yapısı                | Base, exception, result, utils gibi net ayrımlar yapılmalı.                   |
| 🧪 Core test edilebilir olmalı        | Özellikle exception, result yapıları unit test’lerle doğrulanmalı.            |


## 🔚 ÖZETLE

Spring Boot core katmanı, yazılımın temelini oluşturan, tekrar kullanılabilir, ortak bileşenlerin yer aldığı bir katmandır. Bu katman iyi yazıldığında:

- Kod okunabilirliği artar
- Bakım maliyeti düşer
- Profesyonel ve kurumsal uygulama geliştirilmiş olur

