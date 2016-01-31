---
layout: post
title: Proje Sayfası
date: 2016-01-30 12:00:00 +02:00
---

Aşağıdaki kodlar yardımı ile proje ilerleme durumunu görebilirsiniz.

```{r}
#Başlangıç kodlarımız :)
dosya=file.choose()
read.csv('mm.csv')
veri=read.csv2('mm.csv')
str(veri)
veri=veri %>% mutate(yil=as.numeric(substr(ogretim_yili,1,4)))
ggplot(data=veri,aes(x=yil))+ geom_line(aes(y=net_okullasma_orani,color=tur))

```