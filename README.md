# COVID-19 GÖĞÜS RÖNTGEN GÖRÜNTÜLERİNİN DERİN ÖĞRENME İLE SINIFLANDIRILMASI
Bu çalışmada veri seti olarak, kullanıma açık olan COVID-19 röntgen fotoğraflarından oluşan veri seti kullandık.[31] Bu röntgen görüntüleri farklı boyut ve çözünürlüğe sahip olduğundan bunları 299 x 299 olarak yeniden boyutlandırdık. Bu çalışmada DenseNet201, VGG16, ResNet50, InceptionV3 gibi CNN mimarileri üzerinden sınıflandırma yaparak bu modellerin, doğruluk, kesinlik, kayıp, geri çağırma verileri ile kayıp ve doğruluk grafikleri bulunarak karşılaştırma tabloları hazırlanmıştır. Aşağıdaki şekilde modelin mimarisi gösterilmektedir ve adımlar aşağıda açıklanmıştır. 
![grafik](https://user-images.githubusercontent.com/43973257/180061022-641eacbc-218f-477f-b3f4-77ca6dd0c2c9.png)
Adım1: Görüntüleri Elde Etme COVID-19 ve COVID-19 olmayan hastaların röntgen görüntüleri Kaggle[31] gibi kullanıma açık sitelerden toplandı. 
Adım2: Veri Güncelleme Veri setini yükledikten sonra etiketler çıkartıldı. Tüm görüntüler BGR'den RGB kanallarına dönüştürüldü ve ardından 299 × 299 olarak yeniden boyutlandırıldı.
Adım3: Veri Seti Bölme Bu adımda veri seti sırayla %70, %20, %10 olmak üzere eğitim, test ve doğrulama olarak 3’e bölündü. 
Adım4: Temel Modelin Oluşturulması VGG16, ResNet50, DenseNet gibi önceden eğitilmiş modelleri kullanarak temel modelimizi oluşturduk. 
Adım5: Modelin Derlenmesi Model, Adam optimizer ile derlendi. Seçilen öğrenme oranı 0.001. 
Adım6: Modelin Eğitilmesi Model, 1000 COVID-19 negatif ve 904 COVID-19 pozitif röntgen fotoğrafı üzerinden 50 ‘epoch’ ve 32 ‘batch size’ ile eğitildi. 
Adım7: Modelin Test Edilmesi Daha sonra model, veri setinin kalan %20'si(176 adet pozitif ve 200 adet negatif) üzerinde test edildi ve doğruluk, geri çağırma, F1 puanı, özgüllük, duyarlılık vb. için gerekli sonuçlar elde edildi.
# Veri Seti:
Bu çalışmada COVID-19 hastalarına ve normal hastalara ait göğüs röntgen fotoğrafları kullandık. Bu modelde 1000 tanesi normal akciğer ve 904 tanesi COVID-19’dan etkilenen akciğer olmak üzere toplam 1904 göğüs röntgen fotoğrafı kullanıldı. Veri seti eğitim için %70, test için %20 ve onaylama için %10 olarak ayrıldı. Tüm röntgen görüntüleri şekil ve boyut olarak farklı olduğu için görüntüler 299 × 299 olarak yeniden boyutlandırıldı.
![veri](https://user-images.githubusercontent.com/43973257/180061386-66634001-7cac-4f96-8edd-c124177ab7b7.png)
# Sonuçlar ve Değerlendirme:
![degerlendirme](https://user-images.githubusercontent.com/43973257/180061470-48ccdead-5fcb-4c8b-b02f-a2a7f5db5672.png)
Yukarıdaki tablo, COVID-19'u tanımlamada her bir transfer modeli için performans sonuçlarını göstermektedir. Çeşitli modeller farklı sonuçlar verdi, InceptionV3 ve DenseNet201 modelleri ile maksimum doğruluk elde edildi. Karışıklık matrisi yardımı ile diğer ölçerler olan F1-Skoru, duyarlılık ve kesinlik elde edildi. Kesinlik, model tarafından tahmin edilen toplam pozitiflerin (TP+FP) gerçek pozitiflere olan yüzdesidir. Yani modelin hasta olarak tanımladığı tüm röntgen fotoğraflarının gerçekten hastalıklı olan fotoğraflara oranıdır. Duyarlılık, COVID-19 pozitif olan fotoğrafları doğru tespit etme oranıdır. F-1 Skoru ise kesinlik ve duyarlılık arasındaki harmonik bir ortalamadır. Doğruluk, tüm tahminler arasında doğru yapılan tahminleri belirtir. Yüksek hassaslık(gerçek pozitif oran olarak da bilinir) modelin pozitif bir COVID-19 vakasını ne sıklıkla doğru ve pozitif olarak sınıflandırdığının bir ölçüsüdür. Tüm hasta kişilerin doğru olarak tanımlanabilmesi için modelin yüksek hassaslık vermesi önemlidir. Bir diğer taraftan, yüksek özgüllük, modelin negatif COVID-19 vakalarını ne sıklıkla doğru bir şekilde sınıflandırdığını ölçer.
![dense](https://user-images.githubusercontent.com/43973257/180061674-0ba2dca1-4634-4384-82a2-6c35f6b8e50d.png)
![inception](https://user-images.githubusercontent.com/43973257/180061682-8e5a453b-12c0-455a-aaf5-da8fd4309026.png)
![vgg](https://user-images.githubusercontent.com/43973257/180061692-1ee99859-5468-4103-a319-de92350ba4cc.png)
![resnet](https://user-images.githubusercontent.com/43973257/180061704-6ccf86f9-ec3b-422f-bfa0-68549c03ea04.png)
Matrisler, Tablodaki performans sonuçlarını hesaplamak için kullanılan 4 farklı modelin karmaşıklık matrislerini göstermektedir. Matrisler, oluşturduğumuz %20’lik test veri setimize dayalı olarak hesaplandı ve değerler kullanılarak kesinlik, duyarlılık, F1-skoru, doğruluk, hassaslık ve özgüllük hesaplandı. Matrisin satırları röntgen fotoğraflarının gerçek değerlerini, matrisin sütunları modelin tahmin ettiği değerleri göstermektedir.
# Sonuçlar ve Öneriler:
Bu çalışma, X-ışını görüntülerinin kullanılarak COVID-19 pozitif ve normal hastaların sınıflandırılmasını ve önceden eğitilmiş dört modelin(VGG19, ResNet50, InceptionV3, DenseNet201) karmaşıklık matrislerinin oluşturulmasını ve kıyaslanmasını içermektedir. En yüksek doğruluk DenseNet201(%89) ve InceptionV3(%89) modellerinden elde edilmiştir. VGG19, %88 ve ResNet50, %65 doğruluk değerleri göstermiştir. InceptionV3, DenseNet201, VGG19 ve ResNet50 modelleri sırasıyla %89, %88, %87 ve %58 F1-skoru açısından performans göstermiştir. Gelecekteki çalışmalarda, röntgen görüntüleri gerekli ön işlem süreçlerine sokularak daha iyi sonuçlar elde edilebilir.
