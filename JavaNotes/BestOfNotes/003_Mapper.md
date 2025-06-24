# 🔧 Mapper Nedir? Ne İşe Yarar?

__Mapper__, farklı veri nesneleri arasında (genelde DTO ve Entity) otomatik ya da yarı otomatik dönüşüm sağlayan yapıdır.

## Neden Mapper Kullanılır?

* Entity’leri dış dünyaya açmamak için (security & encapsulation)
* Validation kontrolünü DTO üzerinde yapmak için
* Kod tekrarını azaltmak için (get/set satırlarından kurtulmak)
* Controller katmanında sadece DTO ile çalışmak için
* SOLID prensiplerine uymak için (özellikle SRP)

### 🧰 Mapper Kullanım Yöntemleri

#### 1. 🧱 Manuel Mapper (Basit Projelerde)

```java
public class UserMapper {
    public static UserDto toDto(User user) {
        UserDto dto = new UserDto();
        dto.setId(user.getId());
        dto.setUsername(user.getUsername());
        return dto;
    }

    public static User toEntity(UserDto dto) {
        User user = new User();
        user.setId(dto.getId());
        user.setUsername(dto.getUsername());
        return user;
    }
}
```

```
✔ Avantaj: Basit, kontrol sende
❌ Dezavantaj: Kod tekrarı, büyüdükçe yönetilmez olur
```

## 2. 🧠 MapStruct (Kurumsal Projeler İçin Tavsiye Edilen)

__MapStruct__, __compile-time__'da dönüşüm kodu üreten, en performanslı ve stabil mapper kütüphanesidir.

### 📦 Maven Bağımlılığı:

```xml
<dependency>
    <groupId>org.mapstruct</groupId>
    <artifactId>mapstruct</artifactId>
    <version>1.5.5.Final</version>
</dependency>
<dependency>
    <groupId>org.mapstruct</groupId>
    <artifactId>mapstruct-processor</artifactId>
    <version>1.5.5.Final</version>
    <scope>provided</scope>
</dependency>
```

### ⚙️ Kullanımı:

```java
@Mapper(componentModel = "spring")
public interface UserMapper {
    UserDto toDto(User user);
    User toEntity(UserDto dto);
}
```

`@Mapper(componentModel = "spring")` sayesinde bu interface Spring tarafından bir `bean` olarak otomatik tanımlanır. `@Autowired` ile enjekte edebilirsin.

## 🎯 Ne Zaman Mapper Kullanmalısın?

| Senaryo                                                   | Mapper Kullan        | Sebep                          |
| --------------------------------------------------------- | -------------------- | ------------------------------ |
| DTO-Entity dönüşümü varsa                                 | ✅ Evet               | Separation of concerns         |
| CRUD dışında özel dönüşüm ihtiyacı varsa                  | ✅ Evet               | Temiz kod                      |
| DTO kullanılmıyorsa (sadece Entity ile işlem yapılıyorsa) | 🚫 Hayır             | Ama bu zaten **bad practice**  |
| Hızlı demo/prototip projesi                               | ⚠️ Gerek olmayabilir | Kod kalitesi öncelikli değilse |


## 🔚 Özetle

- `Mapper`, kurumsal mimaride `DTO ↔ Entity` dönüşümü için olmazsa olmaz bir yapı.

- Manuel yazılabilir ama uzun vadede yönetilmesi zor olur.

- `MapStruct`, __performans + sadelik__ açısından en iyi çözüm.

- Spring Boot'ta `@Mapper(componentModel = "spring")` ile kullanımı çok kolay.
