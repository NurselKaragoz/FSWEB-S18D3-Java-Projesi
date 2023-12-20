# SQL Sorgu Alıştırmaları

Bu hafta SQL sorguları üzerine çalışıyorsunuz. Bugünkü alıştırmada sizin için hazırladığımız veritabanında aşağıda istediğimiz sonuçları elde etmenize yarayan SQL sorgularını oluşturacaksınız.

## Proje Kurulumu

Projeyi forklayın ve clonlayın. Tamamladığınızda da pushlayın.

### Kütüphane Bilgi Sistemi

Bu veritabanı, bir okulun kütüphanesinden öğrencilerin aldıkları kitapların bilgisini barındırmaktadır.

#### Tablolar

`ogrenci` tablosu öğrencilerin listesini tutar.
`islem` tablosu öğrencilerin kütüphaneden aldıkları kitapların bilgilerini tutar
`kitap` tablosu kütüphanedeki kitapların bilgisini tutar
`yazar` tablosu kitapların yazarları bilgisini tutar
`tur` tablosu kitapların türlerini tutar.

Tablo ilişiklerini görmek için [ktphn.png] dosyasına göz atın.

Yazdığınız sorguları buradan test edebilirsiniz: [https://ergineer.com/assets/materials/fkg36so5-kutuphanebilgisistemi-sql/]

##### Görevler

Aşağıda istenilen sonuçlara ulaşabilmek için gerekli SQL sorgularını yazın.

MIN-MAX, COUNT-AVG-SUM, GROUP BY, JOINS (INNER, OUTER, LEFT, RIGHT
#ilk 3 soruyu join kullanmadan yazın.

1. Öğrencinin adını, soyadını ve kitap aldığı tarihleri listeleyin.
   CEVAP: SELECT o.ograd, o.ogrsoyad, i.atarih FROM ogrenci as o , islem as i WHERE o.ogrno=i.ogrno
2. Fıkra ve hikaye türündeki kitapların adını ve türünü listeleyin.

CEVAP:SELECT k.kitapadi, t.turadi FROM kitap k, tur t WHERE k.turno = t.turno AND (t.turadi = "fikra" OR t.turadi = "hikaye");

3. 10B veya 10C sınıfındaki öğrencilerin numarasını, adını, soyadını ve okuduğu kitapları listeleyin.
   CEVAP: SELECT o.ograd, o.ogrsoyad ,k.kitapadi FROM ogrenci AS o, kitap as k , islem as i WHERE o.ogrno=i.ogrno AND o.sinif IN("10B","10C")
   #join ile yazın
4. Öğrencinin adını, soyadını ve kitap aldığı tarihleri listeleyin.
   CEVAP: SELECT o.ograd,o.ogrsoyad,i.atarih FROM ogrenci o JOIN islem i ON o.ogrno = i.ogrno;

5. Fıkra ve hikaye türündeki kitapların adını ve türünü listeleyin.
   CEVAP:SELECT k.kitapadi, t.turadi FROM kitap k JOIN tur t ON k.turno = t.turno WHERE t.turadi = "hikaye" OR t.turadi="fikra";

6. 10B veya 10C sınıfındaki öğrencilerin numarasını, adını, soyadını ve okuduğu kitapları, öğrenci adına göre listeleyin.

   CEVAP:SELECT o.ogrno, o.ograd, o.ogrsoyad, k.kitapadi FROM ogrenci o JOIN islem i ON o.ogrno = i.ogrno JOIN kitap k ON i.kitapno = k.kitapno WHERE o.sinif IN ('10B', '10C') ORDER BY o.ograd,o.ogrsoyad 7) Kitap alan öğrencinin adı, soyadı, kitap aldığı tarih listelensin. Kitap almayan öğrencilerinde listede görünsün.

   8. Kitap almayan öğrencileri listeleyin.

CEVAP:SELECT o.ogrno, o.ograd, o.ogrsoyad FROM ogrenci o LEFT JOIN islem i ON o.ogrno = i.ogrno WHERE i.ogrno IS NULL;

9.  Alınan kitapların kitap numarasını, adını ve kaç defa alındığını kitap numaralarına göre artan sırada listeleyiniz.

    10. Alınan kitapların kitap numarasını, adını kaç defa alındığını (alınmayan kitapların yanında 0 olsun) listeleyin.

CEVAP:SELECT k.kitapno, k.kitapadi, COUNT(i.kitapno) AS alim_sayisi FROM kitap k LEFT JOIN islem i ON k.kitapno= i.kitapno GROUP BY k.kitapno, k.kitapno;

    11) Öğrencilerin adı soyadı ve aldıkları kitabın adı listelensin.


    12) Her öğrencinin adı, soyadı, kitabın adı, yazarın adı soyad ve kitabın türünü ve kitabın alındığı tarihi listeleyiniz. Kitap almayan öğrenciler de listede görünsün.


    13) 10A veya 10B sınıfındaki öğrencilerin adı soyadı ve okuduğu kitap sayısını getirin.


    14) Tüm kitapların ortalama sayfa sayısını bulunuz.
    #AVG
    CEVAP:SELECT AVG(sayfasayisi) FROM kitap
    15) Sayfa sayısı ortalama sayfanın üzerindeki kitapları listeleyin.


    16) Öğrenci tablosundaki öğrenci sayısını gösterin


    17) Öğrenci tablosundaki toplam öğrenci sayısını toplam sayı takma(alias kullanımı) adı ile listeleyin.


    18) Öğrenci tablosunda kaç farklı isimde öğrenci olduğunu listeleyiniz.


    19) En fazla sayfa sayısı olan kitabın sayfa sayısını listeleyiniz.


    20) En fazla sayfası olan kitabın adını ve sayfa sayısını listeleyiniz.


    21) En az sayfa sayısı olan kitabın sayfa sayısını listeleyiniz.


    22) En az sayfası olan kitabın adını ve sayfa sayısını listeleyiniz.


    23) Dram türündeki en fazla sayfası olan kitabın sayfa sayısını bulunuz.


    24) numarası 15 olan öğrencinin okuduğu toplam sayfa sayısını bulunuz.


    25) İsme göre öğrenci sayılarının adedini bulunuz.(Örn: ali 5 tane, ahmet 8 tane )

CEVAP:SELECT o.ograd, COUNT(\*) AS ogrenci_sayisi FROM ogrenci o JOIN islem i ON o.ogrno= i.ogrno GROUP BY o.ograd;

    26) Her sınıftaki öğrenci sayısını bulunuz.

CEVAP:SELECT sinif, COUNT(\*) AS ogrenci_sayisi FROM ogrenci GROUP BY sinif;

    27) Her sınıftaki erkek ve kız öğrenci sayısını bulunuz.


    28) Her öğrencinin adını, soyadını ve okuduğu toplam sayfa sayısını büyükten küçüğe doğru listeleyiniz.


    29) Her öğrencinin okuduğu kitap sayısını getiriniz.
