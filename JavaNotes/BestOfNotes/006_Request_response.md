# REQUEST - RESPONSE

## 🔁 Request-Response Modeli Nedir?

### Request (İstek):

- İstemciden sunucuya gelen veri.
- Örnek: Yeni bir kullanıcı kaydı oluşturmak için POST /api/users isteği.
- Veri genellikle JSON formatında request body içinde gelir.

### Response (Yanıt):

- Sunucudan istemciye dönen veri.
- Örnek: "Kullanıcı başarıyla oluşturuldu." gibi bir mesaj ya da kullanıcı objesi.
- Veri yine genellikle JSON formatında döner.

## 🧱 Katmanlı Mimaride Nerede Yer Alır?

| Katman                     | Açıklama                                                                |
| -------------------------- | ----------------------------------------------------------------------- |
| **Controller**             | HTTP isteklerini alır, Service'e yönlendirir, HTTP yanıtlarını üretir.  |
| **Service**                | İş mantığını içerir.                                                    |
| **Repository**             | Veritabanı işlemlerini gerçekleştirir.                                  |
| **DTO (Request/Response)** | Veri taşıma nesneleridir. API giriş/çıkış veri modellerini temsil eder. |


## 🧩 Request ve Response Nesneleri

Spring Boot’ta, `Request Body` ve `Response Body` verilerini temsil etmek için genellikle özel sınıflar `(DTO)` tanımlanır.

### 📥 Örnek: Request DTO (İstek verisi)

```java
public class CreateUserRequest {
    private String name;
    private String email;
    private String password;

    // Getter & Setter'lar
}
```

### 📤 Örnek: Response DTO (Yanıt verisi)

```java
public class UserResponse {
    private Long id;
    private String name;
    private String email;

    // Getter & Setter'lar
}
```

## 🔧 Controller Katmanında Kullanım

```java
@RestController
@RequestMapping("/api/users")
public class UserController {

    @PostMapping
    public ResponseEntity<UserResponse> createUser(@RequestBody CreateUserRequest request) {
        // request ile gelen veriyi işle
        UserResponse createdUser = userService.createUser(request);

        // 201 Created ile yanıtla
        return new ResponseEntity<>(createdUser, HttpStatus.CREATED);
    }
}
```

## 🧠 Spring Boot Request-Response Akışı (Özet)

```text
1. İstemci -> POST /api/users -> JSON body ile istek gönderir.
2. Controller -> @RequestBody ile JSON veriyi alır -> Service'e yollar.
3. Service -> İş mantığını çalıştırır -> Entity'yi oluşturur.
4. Repository -> Veritabanına kayıt yapar.
5. Service -> UserResponse DTO'su oluşturur.
6. Controller -> ResponseEntity ile DTO'yu JSON formatında döner.
7. Sunucu -> HTTP 201 + JSON yanıtı -> İstemciye gönderir.
```

## 📌 Notlar

- `@RequestBody` → JSON body’den Java objesi üretir.

- `@ResponseBody` veya otomatik olarak `@RestController` → Java objesini JSON’a dönüştürür.

- `ResponseEntity` → Status code, headers ve body kontrolü sağlar.

