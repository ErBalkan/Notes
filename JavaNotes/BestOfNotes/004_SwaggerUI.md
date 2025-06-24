# SWAGGER UI

## 🔧 1. Bağımlılıkları Ekle (pom.xml)

Spring Boot 3+ ve Springdoc OpenAPI 2.x için:

```xml
<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
    <version>2.5.0</version>
</dependency>
```

✅ Spring Boot 2.x kullanıyorsan springdoc-openapi-ui ile 1.6.14 gibi bir versiyon kullanmalısın.

## 🚀 2. Spring Boot Uygulamanı Başlat

Herhangi özel bir konfigürasyon yapmadan, default olarak şu adreslere erişebilirsin:

### Swagger UI:

```bash
http://localhost:8080/swagger-ui.html
```

__veya__

```bash
http://localhost:8080/swagger-ui/index.html
```

## ⚙️ 3. (Opsiyonel) Swagger Konfigürasyonu Yaz

Eğer __başlık__, __açıklama__, __versiyon__ gibi bilgileri özelleştirmek istersen aşağıdaki gibi bir `config` sınıfı oluştur:

```java
import io.swagger.v3.oas.models.info.Info;
import io.swagger.v3.oas.models.OpenAPI;
import org.springdoc.core.models.GroupedOpenApi;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class SwaggerConfig {

    @Bean
    public OpenAPI apiInfo() {
        return new OpenAPI()
                .info(new Info()
                        .title("Blog API")
                        .description("Spring Boot ile geliştirilen örnek blog projesinin API dökümantasyonu")
                        .version("1.0.0"));
    }

    @Bean
    public GroupedOpenApi publicApi() {
        return GroupedOpenApi.builder()
                .group("v1-definition")
                .pathsToMatch("/api/**")
                .build();
    }
}
```

