# 🚀 Java Programının Yaşam Döngüsü (Lifecycle of a Java Program)

Bir Java programının yaşam döngüsü şu adımlardan oluşur:

```
Yazım (Writing)
    ↓
Derleme (Compilation)
    ↓
Bytecode Oluşturma
    ↓
Yorumlama & Çalıştırma (Execution)
    ↓
JVM Tarafından Yürütme (Run by JVM)
```

Şimdi her adımı detaylıca ele alalım:

## ✅ 1. Writing Code (Kodun Yazılması)

Geliştirici bir `.java` dosyası yazar.

Bu dosya içerisinde `class`, `method`, `değişken` gibi yapılar bulunur.

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Merhaba Dünya");
    }
}
```

💡 __Not:__ Dosya adı `(HelloWorld.java)` ile public class adı birebir aynı olmalıdır.

## ✅ 2. Compilation (Derleme)

* Java kodu doğrudan çalıştırılamaz. Önce derlenir.
* Derleyici: javac (Java Compiler)
* .java dosyası derlenince .class uzantılı bir dosya (bytecode) oluşur.

### 🧠 Neden bytecode?
Çünkü Java “platform bağımsız” çalışır. JVM her sistemde farklıdır ama bytecode evrenseldir.

__🔧 Komut:__

`javac HelloWorld.java`

__📁 Sonuç:__ HelloWorld.class (bytecode)

## ✅ 3. Bytecode Oluşturma

* Derleyici, Java kaynak kodunu __bytecode__ denilen bir ara koda çevirir.
* Bu bytecode, __JVM’nin anlayacağı dildir.__
* İnsan okuyamaz, makineler içindir.

### 🧱 Bytecode örneği (görsel değil ama fikir vermesi açısından):

`cafebabe 0000 0034 001d 0a00 ...`

Bu bytecode platformdan bağımsızdır. Yani Windows, Linux, Mac’te aynı `.class` dosyası çalışır.

## ✅ 4. Execution by JVM (JVM ile Çalıştırma)

* __JVM (Java Virtual Machine)__, bytecode’u alır ve çalıştırır.
* JVM, bytecode’u __Just-In-Time (JIT)__ derleyici ile anında makine diline çevirir.
* Böylece işlemci tarafından çalıştırılabilir hale gelir.

__🔧 Komut:__

`java HelloWorld`

__📌 Not:__ `.class` uzantısını yazmazsın.

## ✅ 5. Programın Koşması (Runtime)

- `main()` metodu __JVM__ tarafından çağrılır.
- Kod satır satır çalıştırılır.
- `Bellek (Heap, Stack)`, `GC (Garbage Collector)`, `Thread` gibi __JVM__ bileşenleri devreye girer.
- `System.out.println(...)` çıktıyı ekrana verir.

## 🔁 Kısaca Java Yaşam Döngüsü:

| Aşama            | Açıklama                                              |
| ---------------- | ----------------------------------------------------- |
| 1. Yazma         | `.java` dosyası oluşturulur                           |
| 2. Derleme       | `javac` ile `.class` (bytecode) üretilir              |
| 3. Çalıştırma    | `java` komutuyla JVM çalıştırır                       |
| 4. JVM Yorumlar  | Bytecode → Makine kodu (JIT)                          |
| 5. Program Koşar | Bellek yönetimi, I/O, GC gibi sistemler devreye girer |


## 🧠 Gerçek Hayatta Bu Ne İşine Yarar?

- Build automation yaparken (Maven, Gradle), derleme sürecini sen kontrol edersin.

- CI/CD pipeline’larında (GitHub Actions, Jenkins) bu döngüyü otomatize edersin.

- JVM tuning, garbage collection ve performans analizleri yaparken bu bilgiyi kullanırsın.


```
“Bir Java geliştiricisi için yazdığı kodun JVM’de nasıl işlendiğini anlamak, motorun nasıl çalıştığını bilen bir sürücü gibi olmaktır. Hızlı, güvenli ve sorunsuz geliştirme yapabilmek için bu lifecycle’ı ezbere bilmelisin.”
```