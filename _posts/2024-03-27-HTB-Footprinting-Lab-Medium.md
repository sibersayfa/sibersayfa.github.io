---
title: HTB Academy Footprinting Lab - Medium
description: Hack the box academy footprinting medium lab çözümü.
author: sibersayfa
date: 2024-03-25
categories: [HTB Çözüm]
img_path: /assets/content-img/HTB-Footprinting-Lab-Medium/
tags: [hackthebox]
mermaid: true

---

**“10.129.202.41”** ip adresini nmap ile taradığımızda açık olan servisleri görüntülediğimizde **“nfs“** servisinin açık olduğunu görülmektedir.  
![1](1.jpg){: w="400" h="400"}

**“showmount -e ip adresi”** komutu ile nfs paylaşılan klasörleri görülmekte. **“TechSupport”** adında paylaşım olduğu görülmektedir.  
![1](2.jpg){: w="400" h="400"}

**“sudo mount -t nfs ip adresi:/TechSupport /mnt/TechSupport/ -o nolock”** komutu ile **“TechSupport “** adında paylaşılan klasörü kendi oluşturduğumuz **“/mnt/TechSupport/”** bağlıyoruz.
![1](3.jpg)

**“sudo su”** komutu ile root yetkisine geçtikten sonra **“cd /mnt/TechSupport”** dizinine gidiyoruz **“ls -la”** komutu ile içeriği listelediğimizde **“ticket4238791283782.txt”** adında metin belgesi görüntülenmektedir.
![1](4.jpg)

**“cat /mnt/TechSupport/ticket4238791283782.txt“** okunduğunda **“alex”** adında bir kullanıcının credential bilgileri görülmektedir.  
![1](5.jpg){: w="400" h="400"}

Nmap taramasında **rdp 3389** portunun açık olduğunu görülmüştü. Rdp yazılımı ile kullanıcı adı şifre ve ip adresi bağlanmayı deniyoruz.  
![1](6.jpg){: w="400" h="400"}

Bağlanıldığında windows bizi karşılamaktadır klasörler gezindiğimizde **“alex/devshare/”** dizininde **“important.txt”** adında bir metin belgesi kaşılaşıyoruz. İçeriğini görüntülediğimizde sql server yönetici kullanıcı adı ve parolası olduğunu düşündüğümüz **“sa:87N1ns@slls83”** içeriğine sahip bilgi görülmektedir.
![1](7.jpg){: w="400" h="400"}

Rdp uygulamasına tekrardan dönüp bulduğumuğuz **“87N1ns@slls83”** parola ile administrator yetkisinde bağlanmayı deniyoruz.  
![1](8.jpg){: w="400" h="400"}

Sunucuya yönetici olarak bağlandık ardından Sql server çalıştırıyoruz.
![1](9.jpg){: w="400" h="400"}

Veritabanından istenen **“HTB”** adındaki kullanıcının parolasını buluyoruz.
![1](10.jpg){: w="400" h="400"}