### Film Veritabanı Sorguları
Bu proje, bir film veritabanında farklı SQL sorgularının nasıl kullanılacağını göstermek için hazırlanmıştır. Aşağıda her sorgunun açıklaması ve amacı yer almaktadır.

### İçindekiler
Sorgu 1: Ortalama Süreden Uzun Filmler
Sorgu 2: En Yüksek Kiralama Ücreti
Sorgu 3: En Düşük Kiralama Ücreti ve Yenileme Maliyeti
Sorgu 4: En Çok Ödeme Yapan Müşteriler

### Sorgu 1: Ortalama Süreden Uzun Filmler
Amaç: Filmlerin süresini inceleyerek, süresi veritabanındaki film sürelerinin ortalamasından daha uzun olan filmlerin sayısını bulur.

```sql
SELECT COUNT(*) FROM film 
WHERE length > (SELECT AVG(length) FROM film);
```

### Sorgu 2: En Yüksek Kiralama Ücreti
Amaç: Veritabanındaki en yüksek kiralama ücretine sahip filmlerin sayısını bulur.

```sql
SELECT COUNT(*) FROM film 
WHERE rental_rate = (SELECT MAX(rental_rate) FROM film);
```

### Sorgu 3: En Düşük Kiralama Ücreti ve Yenileme Maliyeti
Amaç: Hem en düşük kiralama ücretine hem de en düşük yenileme maliyetine sahip filmlerin listesini elde eder. Liste, kiralama ücretine ve ardından yenileme maliyetine göre artan sırada sıralanır.

```sql
SELECT rental_rate, replacement_cost, title FROM film 
WHERE rental_rate = (SELECT MIN(rental_rate) FROM film) 
AND replacement_cost = (SELECT MIN(replacement_cost) FROM film)
ORDER BY rental_rate ASC, replacement_cost ASC;
```
### Sorgu 4: En Çok Ödeme Yapan Müşteriler
Amaç: Müşterilerin yaptığı ödeme sayısına göre sıralı bir liste oluşturur. Her müşterinin toplam ödeme sayısı hesaplanır ve çoktan aza doğru sıralanır.

```sql
SELECT customer.customer_id, customer.first_name, customer.last_name,
COUNT(payment.payment_id) AS total_payments FROM payment
JOIN customer ON customer.customer_id = payment.customer_id
GROUP BY customer.customer_id, customer.first_name, customer.last_name
ORDER BY total_payments DESC;
```
