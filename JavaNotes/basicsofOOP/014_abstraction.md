# 🧠 ABSTRACTION (Soyutlama) — Java’da Karmaşıklığı Yönetmenin Yolu

## 📌 1. Abstraction Nedir?

Abstraction, nesneye ait detayları gizleyip, sadece ilgili özellikleri ve davranışları dışarıya açmaktır.

### 🔁 Özet tanım:
- "What it does" ✔️
- "How it does" ❌

## 💡 2. Gerçek Hayattan Analojiler

| Nesne        | Ne Gördük         | Ne Saklandı                         |
| ------------ | ----------------- | ----------------------------------- |
| Araba        | Direksiyon, pedal | Motorun iç yapısı, fren mekanizması |
| ATM Makinesi | Butonlar, ekran   | Ağ bağlantısı, hesap veritabanı     |
| Bilgisayar   | Tuşlar, ekran     | Anakart, işlemci işleyişi           |


## 🏗️ 3. Java'da Abstraction Nasıl Uygulanır?

Java'da abstraction, iki ana yapı üzerinden sağlanır:

## 🔑 4. abstract class — Soyut Sınıf

```java
abstract class Sekil {
    int x, y;

    abstract void ciz(); // soyut metod

    void hareketEt() {
        System.out.println("Şekil hareket ediyor");
    }
}
```

```java
class Daire extends Sekil {
    @Override
    void ciz() {
        System.out.println("Daire çiziliyor");
    }
}
```

### 🔍 Özellikler:

- `new` anahtar kelimesiyle örneklenemez
- En az bir tane soyut metod içermelidir
- Hem abstract hem somut metodlara sahip olabilir
- Alt sınıflar soyut metodları `override etmek zorundadır`

## 💼 5. interface — Arayüz

```java
interface Ucak {
    void havalan();
    void inisYap();
}
```

```java
class YolcuUcagi implements Ucak {
    public void havalan() {
        System.out.println("Yolcu uçağı havalanıyor");
    }
    public void inisYap() {
        System.out.println("Yolcu uçağı iniyor");
    }
}
```

### 🔍 Özellikler:

| Özellik                    | Açıklama                                            |
| -------------------------- | --------------------------------------------------- |
| %100 abstraction sağlar    | Tüm metotlar public ve abstract’tır (Java 8 öncesi) |
| Sadece method imzası       | Gövde yoktur (Java 8 öncesi)                        |
| Çoklu inheritance sağlar   | Bir sınıf birden fazla interface implement edebilir |
| `implements` ile uygulanır | Kalıtım gibi değil, sözleşme gibidir                |


## 🆚 6. abstract class vs interface

| Kriter         | `abstract class`           | `interface`                       |
| -------------- | -------------------------- | --------------------------------- |
| Kalıtım        | Sadece bir sınıf           | Birden çok interface olabilir     |
| Metot türü     | Hem soyut hem somut        | Default veya static (Java 8+)     |
| Constructor    | Var                        | Yok                               |
| Field          | State barındırabilir       | Sadece `public static final`      |
| Kullanım amacı | Ortak davranış + soyutlama | Sadece soyutlama (API sözleşmesi) |


## 🎯 7. Abstraction Kullanım Amacı
1. 🔐 Detayları gizlemek
2. 📦 Kod organizasyonunu artırmak
3. 🧩 Karmaşık sistemleri sadeleştirmek
4. ♻️ Genişletilebilir ve sürdürülebilir sistemler kurmak
5. ✅ Sözleşme (contract) ile API ya da servis yapısını garanti etmek

## 🧪 8. Örnek: API Katmanı

```java
interface KullaniciServisi {
    void kullaniciKaydet(KullaniciDto dto);
    KullaniciDto kullaniciBul(int id);
}
```

```java
class KullaniciServisiImpl implements KullaniciServisi {
    @Override
    public void kullaniciKaydet(KullaniciDto dto) {
        // veritabanına kaydet
    }

    @Override
    public KullaniciDto kullaniciBul(int id) {
        return new KullaniciDto(); // DB'den getirme
    }
}
```

```
👉 Client tarafı sadece KullaniciServisi'ni görür. İçeride MongoDB mi var, PostgreSQL mi? Bilmez.
```

## 🧠 9. Best Practices (Kurumsal Seviye)

| Kural                                   | Açıklama                                              |
| --------------------------------------- | ----------------------------------------------------- |
| Sadece ortak davranışlar soyutlanmalı   | Her sınıf interface olmasın                           |
| Interface isimleri net olmalı           | `ICustomerService` yerine `CustomerService` yeterli   |
| API sözleşmelerinde interface tercih et | Uygulama detayından bağımsız olmalı                   |
| Soyut sınıf mı interface mi?            | Ortak state varsa `abstract class`, yoksa `interface` |
| Her interface bir amaca hizmet etmeli   | `Interface Segregation Principle (ISP)`               |


## ✅ 10. Özet

| Kavram           | Açıklama                                      |
| ---------------- | --------------------------------------------- |
| Abstraction      | Karmaşıklığı gizler, sadece gerekeni açar     |
| `abstract class` | Hem davranış hem soyutluk sağlar              |
| `interface`      | Tam soyutlama, sadece davranış sözleşmesi     |
| Kullanım         | Mimariyi genişletmek, bağımlılığı azaltmak    |
| Avantaj          | Modülerlik, okunabilirlik, test edilebilirlik |


