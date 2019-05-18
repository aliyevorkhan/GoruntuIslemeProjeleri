
Yapilan islemler sirasi ile:
1.	Maske gezdirme
2.	B�y�tme islemi (Zoom in)
3.	Histogram �ikarma
4.	Histogram esitleme
5.	Clustering(K-Means)
6.	Morfoloji islemleri
a.	Dilation
b.	Erosion
7.	Nesne algilama
8.	G�r�nt� Geometrisi
a.	G�r�nt�y� tasima
b.	G�r�nt�y� d�nd�rme
c.	G�r�nt�y� d�nd�rme(Alias ile)
d.	G�r�nt�y� aynalama

Maske gezdirme
Gezdirecegimiz maskeyi g�r�nt�n�n �zerine koydugumuzda kenarlardan tasma olacak bu y�zden g�r�nt�n�n kenarlarini sifirlarla dolduruyoruz. Birinci iterasyonda maskenin merkezini g�r�nt�n�n ilk pikseline koyuyoruz, g�r�nt�n�n ilk pikselinin yeni degerini maskenin elemanlarini g�r�nt�de �st�nde durdugu piksellerle �arpip topluyoruz ve g�r�nt�n�n o pikselini bu toplam degeri ile setliyoruz. Devaminda bir saga kaydirip ayni islemi tekrarliyoruz.
           B�y�tme islemi (Zoom in)
G�r�nt� �zerinde belirli bir kismi kesip, �ikartip onu b�y�tme islemini ger�eklestirmek su sekilde ger�eklesir. �rnegin fare ile fotografin i�erisinde herhangi bir noktadan basladik, sol alta dogru kirptik ve fareyi �ektik. Baslangi� konumunu x0, y0 olarak bitis konumunu x1, y1 olarak ele aldik bir d�ng� ile bu kismi kesip �ikardik fakat yeni fotografimiz hen�z b�y�t�lmemis. B�y�tme i�in yeni fotografin piksellerinin aralarini sifirlar ile dolduruyoruz. Sonu�ta yeni fotografimiz g�r�lt�l� gibi g�z�k�yor, bunun sebebi aralari sifirlar ile doldurmamiz. Fotografimiz b�y�k fakat g�r�lt�l� bunu yok etmek i�in maske gezdiriyoruz. Gaussian maskesi ile maske gezdirme fonksiyonundaki adimlari izlersek g�r�lt�y� yok etmis oluruz ve sonuca ulasiriz.
			        Histogram �ikarma
Fotografta 0 ila 255 arasindaki piksel degerlerinin sayisini bir chart �zerinde g�sterebilmek i�in bir d�ng� i�erisinde fotografin her pikseline erisiriz ve o piksel degerine sahip olan ka� tane piksel var ise bu sayiyi chart �zerinde setleriz.
				Histogram esitleme
�ikarmis oldugumuz histogram �zerinden histogram esitleme yapmak i�in ilk olarak running sum hesaplanir, running sum�in son degeri bizim toplam piksel degerimiz oluyor degerimiz oluyor. Her degeri bu toplam piksel degerimize b�lecegiz. Daha sonra her degeri maksimum gri seviye degeri (�rn. 255) ile �arpiyoruz. Ve elde ettigimiz degerler bizim esitlenmis histogram degerlerimiz oluyor. Sonu�lari esitlenmis histogram olarak chart �zerinde isliyoruz.

				Clustering(K-Means)
G�r�nt� �zerinde clustering islemi yapmak i�in ilk olarak g�r�nt�n�n histogramini �ikarmaliyiz daha sonra bu histogram �zerine 2 esik degerini(�rn. T1 ve T2) rastgele setlemeliyiz. Daha sonra ise bir d�ng� i�erisinde bu esik degerlerinin yeni degerlerini bulabilmek i�in her esik degeri i�in ona yakin olan pikseller ile degerlerini �arpip topariz ve toplam piksel degerine b�leriz. Bunu yaparken her iterasyonda bir �nceki esik degerleri ile yeni buldugumuz esik degerleri esit mi diye kontrol ederiz ve sonu� saglanana kadar iterasyon tekrarlanir. En sonda ise esitlik saglandiginda o esik degerlerinin komsularina karar veririz ve binary degerler ile g�r�nt�y� binary g�r�nt�ye d�n�st�r�r�z.
				  	Dilation
Dilation islemini yaparken fotografin binary halini kullaniyoruz. G�r�nt�deki 1�ler �zerinden ilerliyoruz ve genisletme i�in OR�lama islemi yapiyoruz. Bu islem sonucunda genisletilmis g�r�nt�y� elde ederiz. 
					Erosion
Dilation islemi gibi bu islemi de binary g�r�nt� �zerinde yapariz. Fakat tek fark OR�lama islemi yerine AND�leme islemi yapmamiz. Bu islem sonucunda eroziyona ugramis g�r�nt�y� elde ederiz.
				 Nesne algilama
 
G�r�nt� �zerinde 4�l� veya 8�li sekilde geziyoruz, komsularin etiket degerlerini kontrol ediyoruz, eger etiket almamissa yeni etiket degerini veriyoruz veya komsularinda etiket alan varsa onun degerine setliyoruz. Fakat komsularinda 2 veya daha fazla etiket almis komsu olabilir bu duruma �collision� diyoruz ve bu durumda ��z�m olarak komsularini ve kendisini en k���k etiketli degere setliyoruz. Bu sekilde d�ng� sonuna kadar ilerliyoruz. Ka� etiketimiz var ise o kadar da nesne oldugu anlamina gelir. Ve bu etiket sayisini nesne sayisi olarak ekranda g�steririz.
			      G�r�nt�y� tasima
Tasima operat�r�, giris resmindeki her pikseli, �ikis resmindeki yeni bir konuma tasima islemidir. Orjinal resimdeki (x1,y1) koordinatindaki her piksel belli bir �teleme mesafesi (�x, �y) boyunca tasinarak yeni konumu olan (x2,y2) koordinatina yerlestirilir
 
Yukaridaki form�lden yaralaniriz.
Yeni olusan koordinatlar (x2,y2) resmin sinirlari disina �iktiysa ya yok sayilir veya sinirlar genisletilerek, ilgili alan doldurulur.  
          G�r�nt�y� d�nd�rme
D�nd�rme islemi bir nokta etrafinda belli bir a�i (?) degerinde �evirerek giris resmindeki (x1,y1) koordinatini �ikis resmindeki (x2,y2) noktasina tasima islemidir. D�nd�rme isleminde sinirlarin disina �ikan kisimlar yok sayiyoruz. 
 
Yukaridaki form�lden yararlanarak d�nd�rme islemini ger�eklestiririz. G�r�lt�s�z g�r�nt� elde edemeyiz bunu elde etmek i�in alias ile d�nd�rmeye ihtiya� duyariz.
		       G�r�nt�y� d�nd�rme(Alias ile)
Yukaridaki islemlerin aynisini uygulariz fakat Alias�siz islemde bazi piksellerden ge�ilmiyordu(vekt�r bazinda baktigimizda) ve bu y�zden piksellerin degerleri belirsiz kaliyordu Alias ile d�nd�rmede bu sorun ��z�l�yor. Piksellerden ge�ilmese de komsularinin degerlerine yakin degerler alinirsa bu sorun ��z�l�r.
Not: Bunu kaydirma islemleri ile de yapabiliriz. Fakat iyi ��z�m olmaz.
			                        Aynalama
G�r�nt�y�  orijinal (x1, y1) konumundan alarak, belirlenen eksen etrafinda yansitarak yeni bir konuma (x2, y2)yerlestiririz. (x0,y0) noktasi resmin tam orta noktasidir.
�	x0 noktasindan ge�en dikey eksen etrafinda yansitma;
 
�	y0 noktasindan ge�en yatay eksen etrafinda yansitma,
    


�	(x0,y0) noktasindan ge�en herhangi bir ? a�isina sahip bir eksen etrafinda yansitma.
 
 
