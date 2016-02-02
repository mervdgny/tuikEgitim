---
layout: page
title: Proje Kodları
---

```{r}
dosya=file.choose()
read.csv2(dosya)
getwd()

df=read.csv2(dosya) 
str(df)

#plot1 kodu kullanılarak ilköğretim ve ortaöğretim için okullaşma oranları yıllara göre bir çizgi grafiği çizilmiştir. Kod sayesinde türleri farklı renklerde göstererek grafiğin okunması kolaylaştırılmıştır.
df=df %>%
  mutate(yil=as.numeric(substr(ogretim_yili, 1, 4)))
plot1<-ggplot(data=df,aes(x=yil)) + geom_line(aes(y=net_okullasma_orani,color=tur))

#plot2 kodu kullanılarak ilköğretim ve ortaöğretim için öğretim yıllarına göre şube başına düşen öğrenci sayıları gösterilmiştir. Bu kod okul ve öğretmen başına düşen öğrenci sayılarını görebilmek için de küçük bir modifikasyon yapılarak elde edilebilir.
plot2<-ggplot(data=df,aes(x=ogretim_yili,y=sbd_ogrenci_sayisi)) + geom_bar(stat="identity",aes(fill=tur))

#plot3 kodu kullanılarak ilköğretim ve ortaöğretime farklı şekiller vererek, renk değişimi ile hangi yıllarda olduklarını belirleyerek Şube ve okul başına düşen öğrenci sayılarını karşılaştırabildik.
plot3<-ggplot(data=df) + geom_point(aes(x=obd_ogrenci_sayisi,y=sbd_ogrenci_sayisi,color=yil,shape=tur), size=3)

#plot4 de ise plot3’de yaptığımız şube ve okul karşılaştırmasına öğretmen başına düşen öğrenci sayısını da ekledik. Bunu da kodunda görüldüğü gibi ‘alpha= oobd_ogrenci_sayısı’ değişkenini ekleyerek elde ettik. 
plot4<-ggplot(data=df) + geom_point(aes(x=obd_ogrenci_sayisi,y=sbd_ogrenci_sayisi,color=tur,shape=tur, alpha=oobd_ogrenci_sayisi), size=4)

#plot5 kodu ile öğretmen başına düşen öğrenci sayısının 15’in üzerinde olduğu öğretim yıllarını görebiliyoruz. Bunu da ayrıca ilköğretim ve ortaöğretim olmasına göre farklı renklerle düzenliyoruz.
plot5<-ggplot(data=df %>% filter(oobd_ogrenci_sayisi>=15)) + geom_point(aes(x=oobd_ogrenci_sayisi,y=ogretim_yili, color=tur), size=2)
ggplot(data=df,aes(x=ogretim_yili,y=oobd_ogrenci_sayisi)) + geom_bar(stat="identity",aes(fill=tur))


#plot kodunu kullanarak bütün öğretim yıllarını (1997-2012 yılları arasında) baz alarak ilköğretim ve ortaöğretimde bulunan ortalama okul sayısını vermektedir. Bu kodu öğretmen ve öğrenci sayısı için de küçük bir değişiklikle uygulayabilliriz.
ozet1<-df %>% 
  group_by(tur) %>% 
  summarise(okul_sayisi=mean(okul_sayisi))
plot<-ggplot(data=ozet1,aes(x=tur,y=okul_sayisi)) + geom_bar(stat="identity",aes(fill=tur))


ggsave("~/Documents/grafik.png",plot)
ggsave("~/Documents/grafik.png",plot1)
ggsave("~/Documents/grafik1.png",plot2)
ggsave("~/Documents/grafik2.png",plot3)
ggsave("~/Documents/grafik3.png",plot4)
ggsave("~/Documents/grafik4.png",plot5)


```


