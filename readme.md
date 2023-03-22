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
#ilk 3 soruyu join kullanmadan yazın. 1) Öğrencinin adını, soyadını ve kitap aldığı tarihleri listeleyin.

    select ogrenci.ograd,ogrenci.ogrsoyad,islem.atarih from ogrenci,islem

where ogrenci.ogrno=islem.ogrno

    2) Fıkra ve hikaye türündeki kitapların adını ve türünü listeleyin.

select kitap.kitapadi,tur.turadi from kitap,tur
where kitap.turno=tur.turno and tur.turadi in("Fıkra","Hikaye")

    3) 10B veya 10C sınıfındaki öğrencilerin numarasını, adını, soyadını ve okuduğu kitapları listeleyin.

    #join ile yazın





    4) Öğrencinin adını, soyadını ve kitap aldığı tarihleri listeleyin.

    select ogrenci.ograd as "Öğrenci Adı",ogrenci.ogrsoyad as "Öğrenci Soyadı",islem.atarih as "Kitap Aldığı Tarih" from ogrenci

inner join islem on ogrenci.ogrno=islem.ogrno

    5) Fıkra ve hikaye türündeki kitapların adını ve türünü listeleyin.

select kitapadi,turadi from kitap as k
inner join tur as t on t.turno=k.turno
where turadi="Fıkra" or turadi="Hikaye"

    6) 10B veya 10C sınıfındaki öğrencilerin numarasını, adını, soyadını ve okuduğu kitapları, öğrenci adına göre listeleyin.


    7) Kitap alan öğrencinin adı, soyadı, kitap aldığı tarih listelensin. Kitap almayan öğrencilerin de listede görünsün.

     select ogrenci.ograd,ogrenci.ogrsoyad,islem.atarih from ogrenci left join islem on ogrenci.ogrno=islem.ogrno




    8) Kitap almayan öğrencileri listeleyin.

    select ogrenci.ograd,ogrenci.ogrsoyad,islem.atarih from ogrenci left join islem on ogrenci.ogrno=islem.ogrno where islem.atarih is null


    9) Alınan kitapların kitap numarasını, adını ve kaç defa alındığını kitap numaralarına göre artan sırada listeleyiniz.

select kitap.kitapno,kitap.kitapadi,count(islem.islemno) as "İşlem sayısı" from kitap left join islem on
kitap.kitapno=islem.kitapno
group by kitapno

    10) Alınan kitapların kitap numarasını, adını kaç defa alındığını (alınmayan kitapların yanında 0 olsun) listeleyin.

     select kitap.kitapno,kitap.kitapadi,count(islem.islemno) as "İşlem sayısı"  from kitap left join islem on

kitap.kitapno=islem.kitapno
group by kitapno

    11) Öğrencilerin adı soyadı ve aldıkları kitabın adı listelensin.

     select o.ograd,o.ogrsoyad,k.kitapadi from ogrenci as o

left join islem as i on o.ogrno=i.ogrno
left join kitap as k on k.kitapno=i.kitapno

    12) Her öğrencinin adı, soyadı, kitabın adı, yazarın adı soyad ve kitabın türünü ve kitabın alındığı tarihi listeleyiniz. Kitap almayan öğrenciler de listede görünsün.




     select o.ograd,o.ogrsoyad,k.kitapadi,y.yazarad,y.yazarsoyad,i.atarih,t.turadi from ogrenci as o

left join islem as i on o.ogrno=i.ogrno
left join kitap as k on i.kitapno=k.kitapno
left join yazar as y on y.yazarno=k.yazarno
left join tur as t on t.turno=k.turno

    13) 10A veya 10B sınıfındaki öğrencilerin adı soyadı ve okuduğu kitap sayısını getirin.

     select ogrenci.ograd,ogrenci.ogrsoyad,count(islem.islemno) as "okunan kitap sayısı" from ogrenci left join islem on ogrenci.ogrno=islem.ogrno

where ogrenci.sinif in ("10A","10B") group by ogrenci.ogrno

    14) Tüm kitapların ortalama sayfa sayısını bulunuz.
    #AVG

select avg(sayfasayisi) from kitap

    15) Sayfa sayısı ortalama sayfanın üzerindeki kitapları listeleyin.

select kitapadi,sayfasayisi from kitap
where sayfasayisi >(select avg(sayfasayisi) from kitap)

    16) Öğrenci tablosundaki öğrenci sayısını gösterin

select count(ogrno) from ogrenci

    17) Öğrenci tablosundaki toplam öğrenci sayısını toplam sayı takma(alias kullanımı) adı ile listeleyin.


    18) Öğrenci tablosunda kaç farklı isimde öğrenci olduğunu listeleyiniz.

select count(distinct(ograd)) from ogrenci

    19) En fazla sayfa sayısı olan kitabın sayfa sayısını listeleyiniz.


    20) En fazla sayfası olan kitabın adını ve sayfa sayısını listeleyiniz.

     select kitap.kitapadi,kitap.sayfasayisi from kitap

order by kitap.sayfasayisi desc
limit 1

    21) En az sayfa sayısı olan kitabın sayfa sayısını listeleyiniz.

select kitap.sayfasayisi from kitap
order by kitap.sayfasayisi
limit 1

// ya da

select min(sayfasayisi) as enazsayfa from kitap

    22) En az sayfası olan kitabın adını ve sayfa sayısını listeleyiniz.

select kitap.kitapadi,kitap.sayfasayisi from kitap
order by kitap.sayfasayisi
limit 1
//ya da
select kitapadi,sayfasayisi from kitap
where sayfasayisi=(select min(sayfasayisi) from kitap)

    23) Dram türündeki en fazla sayfası olan kitabın sayfa sayısını bulunuz.

select k.kitapadi,k.sayfasayisi from kitap as k
inner join tur as t on t.turno=k.turno
where t.turadi="dram"
order by k.sayfasayisi desc
limit 1

    24) numarası 15 olan öğrencinin okuduğu toplam sayfa sayısını bulunuz.



    select o.ograd,o.ogrsoyad,sum(k.sayfasayisi) from ogrenci as o

left join islem as i on i.ogrno=o.ogrno
left join kitap as k on k.kitapno=i.kitapno
where o.ogrno=15

    25) İsme göre öğrenci sayılarının adedini bulunuz.(Örn: ali 5 tane, ahmet 8 tane )


    select distinct(ograd),count(ograd) from ogrenci group by ograd


    26) Her sınıftaki öğrenci sayısını bulunuz.

select sinif,count(ogrno) from ogrenci
group by sinif

    27) Her sınıftaki erkek ve kız öğrenci sayısını bulunuz.

    select sinif,cinsiyet,count(cinsiyet) as "öğrenci sayisi" from ogrenci group by sinif,cinsiyet





    28) Her öğrencinin adını, soyadını ve okuduğu toplam sayfa sayısını büyükten küçüğe doğru listeleyiniz.

select o.ograd,o.ogrsoyad,sum(k.sayfasayisi) as"toplamsayfa" from ogrenci as o
left join islem as i on o.ogrno=i.ogrno
left join kitap as k on
i.kitapno=k.kitapno
group by o.ogrno
order by toplamsayfa desc

    29) Her öğrencinin okuduğu kitap sayısını getiriniz.

     select Concat(o.ograd,o.ogrsoyad) as "ad soyad" ,count(i.ogrno) as "okuduğu kitap"from ogrenci as o

inner join islem as i on i.ogrno=o.ogrno
