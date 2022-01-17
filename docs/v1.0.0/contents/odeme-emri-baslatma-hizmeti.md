## 6.	Ödeme Emri Başlatma Hizmeti

Ödeme emri başlatma işlemi havale, FAST ya da PÖS ödemesiyle sonuçlanabilir. Ödeme işleminin amacı kişiden kişiye para transferi, e-ticaret ödemesi gibi farklı ödeme türleri olabilir. Ödemenin amacına göre ÖBHS’nin ileteceği veri setinde farklılaşmalar olabilir.

Ödeme Emri Başlatma Hizmeti 5 temel akışdan oluşur:
0.	Ödeme Emri Başlatma İsteğinin tetiklenmesi: ÖHK ÖBHS mobil uygulama ya da websitesinden ödeme emrini başlatır. 
1.	Ödeme Emri Rıza Hazırlanması: ÖBHS, “Ödeme Emri Başlatma” işlemi için izin oluşturulması isteğini HHS’ye iletir. 
2.	Ödeme Emri Rızasının Yetkilendirilmesi: HHS, gerekli gördüğü durumlarda ÖHK’yı GKD ile doğrular ve ödeme emri rızasına erişim için erişim belirteci tanımlanmasını temin eder.
3.	Ödeme Emrinin Başlatılması: ÖBHS, “ödeme emri”ni HHS’ye iletir.
4.	Ödeme Emri Rıza Durumu, Ödeme Emri Durumu, Ödeme Emri Detayı Sorguları: ÖBHS, Ödeme Emri Rıza Durumu, Ödeme Emri Durumu, Ödeme Emri Detayı bilgilerini isteğe bağlı olarak sorgulayabilir.


![Odeme Emri Baslatma Hizmeti Ust Düzey İş Akışı](./images/OdmemeEmriBaslatmaHizmetiUstDuzeyIsAkisi.png)

Şekil 4: Ödeme Emri Başlatma Hizmeti Üst Düzey İş Akışı


#### Ödeme Emri Başlatma Hizmeti için Erişim Adresleri (Endpoints)


| No | Kaynak|HTTP işlemi |Erişim Adresi |Zorunlu / İsteğe Bağlı |Yetkilendirme Türü |İmzalama|İstem Nesnesi |Yanıt Nesnesi |
| --- |--- |--- |--- |--- |--- |--- |--- |--- |
| 1|odeme-emri-rizasi|POST |POST /odeme-emri-rizasi |Z |İstemci Kimlik Bilgileri |İmzalı İstek ve Yanıt |OdemeEmriRizasiIstegi |OdemeEmriRizasi |
| 2|erisim-belirteci (GKD için)|POST |POST/erisim-belirteci /odeme-emri-rizasi |Z |İstemci Kimlik Bilgileri |İmzalı İstek ve Yanıt |ErisimBelirteciIstegi |ErisimBelirteci |
| 2.1 |odeme-emri-rizasi |GET |GET /odeme-emri-rizasi/{rizaNo} |Z |İstemci Kimlik Bilgileri  |İmzalı Yanıt |- |OdemeEmriRizaYaniti |
| 3 |odeme-emri |POST |POST /odeme-emri |Z |İstemci Kimlik Bilgileri & Yetkilendirme Kodu (GKD) |İmzalı Yanıt |OdemeEmriIstegi |OdemeEmri |
| 4 |odeme-emri |GET |GET /odeme-emri/{odemeEmriNo}|Z |İstemci Kimlik Bilgileri & Yetkilendirme Kodu (GKD) |İmzalı Yanıt |- |OdemeEmri |



### POST /odeme-emri-rizasi

#### Request


```
:method: POST
:path: /yos-simulator-service/api/odeme-emri-rizasi/
Authorization: Bearer 2YotnFZFEjr1zCsicMWpAA
x-aspsp-code: 8000
x-group-id: f18e683a-aa60-40f9-830f-1896f26fea5f
x-request-id: 45d5efd1-b0ca-4c53-88ef-b1994c328841
x-tpp-code: 8000
x-xsrf-token: CfDJ8F4tcYI0Y1BPi1GNm73SibeeI2zX8LUcvsnOPfS_8OE4GRZ7hD9OcyMLOHlZxHLdIDbytMPGa-a3Cr51KG8hM3B4b51IV6FRSWEKexyqCwSCh1Hc02MmHk2GL8CF4gOSvhnwwaXB52my_JRr_nhLqCGuUzeyuUY5qYCdgTx3p1Yu-vMY_DNdY7l_HyydJ_2PK
psu-initiated: E
psu-ip-adress: 127.0.0.1
psu-ip-port: 443
Content-Type: application/json
Accept: application/json
```



```json
{
  "gkd": {
    "yetYntm": "Y",
    "yonAdr": "https://boss-test.bkm.com.tr/boss/ab/yosSimulator/8000/odeme-emri-rizasi/onay"
  },
  "odmBsltm": {
    "kmlk": {
      "kmlkTur": "K",
      "kmlkVrs": "77121323400",
      "ohkTur": "B"
    },
    "islTtr": {
      "prBrm": "TRY",
      "ttr": 1321
    },
    "gon": {
      "unv": "AHMET YILMAZ",
      "hspNo": "TR1000010XP9UDWM4Z6LVJKS45"
    },
    "alc": {
      "unv": "AHMET YILMAZ",
      "hspNo": "TR1000010XP9UDWM4Z6LVJKS45"
    },
    "odmAyr": {
      "odmKynk": "A",
      "odmAmc": "01",
      "yosKod": "0010",
      "refBlg": "Y-2701852-202011",
      "odmAcklm": "Kira bedeli"
    },
    "obhsMsrfTtr": {
      "prBrm": "TRY",
      "ttr": 100
    }
  }
}
```


#### Response


```
HTTP/1.1 201 Created
x-aspsp-code: 8000
x-content-type-options: nosniff
x-frame-options: DENY
x-group-id: f18e683a-aa60-40f9-830f-1896f26fea5f
x-jws-signature: eyJhbGciOiJSUzI1NiJ9.eyJpc3MiOiJodHRwczovL2FwaWd3LmJrbS5jb20udHIiLCJleHAiOjE2NDE5MTA0NzUsImlhdCI6MTY0MTgyNDA3NSwiYm9keSI6IjFkMjRlYzdkOWRhODdiYjczNzc2M2NhNjdjMGY3OTBlNTQyZTU4NTdhMWI2NjA4NDM1YWNmMGQwMmYzOTIxMDUifQ.ZcqrmH-HvBu9I-islB1vN6TExAhJfMRDbRX8Eil4VO7NuoO1NiHS0W8Sc28BZthqhjpygaAfvf3F6wpyIPKf8VXsusc_9PRpeSdWyvQIhrrmYFPVTIgTt3F8XpLZMPkB2eoPB7gMnKxe2iWdQN8Wrji7ZEJTSKQ5d2QkGSsH96N68Al_1cg8cixaTlw3k29bjWt_wzmf75VjsOiPpn9SNWw_LFErd21onnPITEEMwTmPFBYf0Rs4gpj59UzwYyy0sWkfiOF1gLJi3nke_J1jGO5_oqlhB5P4tP_FS8CAYxLyNnl2WI_-dYvw8kIHo7LszDeKGEK9Xhd3X2kncA4H-w
x-request-id: 45d5efd1-b0ca-4c53-88ef-b1994c328841
x-tpp-code: 8000
Content-Type: application/json
```



```json
{
  "rzBlg": {
    "rizaNo": "58af49355aee43e08c1b4e5aaca7d726",
    "olusZmn": "2021-07-09T15:19:12+03:00",
    "gnclZmn": "2021-07-09T16:19:12+03:00",
    "rizaDrm": "B"
  },
  "gkd": {
    "yetYntm": "Y",
    "yonAdr": "https://boss-test.bkm.com.tr/boss/ab/yosSimulator/8000/odeme-emri-rizasi/onay",
    "yetTmmZmn": "2021-07-09T12:42:44+03:00",
    "hhsYonAdr": "https://boss-test.bkm.com.tr/boss/ab/hhsSimulator/8000/odeme-emri-rizasi/58af49355aee43e08c1b4e5aaca7d726/goruntule"
  },
  "odmBsltm": {
    "kmlk": {
      "kmlkTur": "K",
      "kmlkVrs": "77121323400",
      "ohkTur": "B"
    },
    "islTtr": {
      "prBrm": "TRY",
      "ttr": 1321
    },
    "gon": {
      "unv": "AHMET YILMAZ",
      "hspNo": "TR1000010XP9UDWM4Z6LVJKS45"
    },
    "alc": {
      "unv": "AHMET YILMAZ",
      "hspNo": "TR1000010XP9UDWM4Z6LVJKS45"
    },
    "odmAyr": {
      "odmKynk": "A",
      "odmAmc": "01",
      "yosKod": "0010",
      "refBlg": "Y-2701852-202011",
      "odmAcklm": "Kira bedeli",
      "ohkMsj": "Ödeme rızası talebi alındı",
      "odmStm": "H",
      "bekOdmZmn": "2021-01-28T12:42:44+03:00"
    },
    "obhsMsrfTtr": {
      "prBrm": "TRY",
      "ttr": 100
    },
    "hhsMsrfTtr": {
      "prBrm": "TRY",
      "ttr": 100
    }
  }
}
```


```
HTTP/1.1 400 Bad Request
Content-Type: application/json
```


```json
{
  "id": "2b5f0fb2-730b-11e8-adc0-fa7ae01bbebc",
  "path": "/obh/odeme-emri",
  "timestamp": "2021-08-13T09:55:23+03:00",
  "httpCode": 401,
  "httpMessage": "Not Found",
  "moreInformation": "Resource Schema validation error",
  "moreInformationTr": "Alan doğrulama hatası",
  "errorCode": "TR.OBHS.Resource.InvalidFormat",
  "fieldErrors": [
    {
      "objectName": "odemeEmriRizasi",
      "field": "rizaNo",
      "messageTr": "boyut '1' ile '128' arasında olmalı",
      "message": "size must be between '1' and '128'",
      "code": "TR.OBHS.Field.Invalid"
    }
  ]
}
```




```
HTTP/1.1 401 Unauthorized
Content-Type: application/json
```


```json
{
  "id": "2b5f0fb2-730b-11e8-adc0-fa7ae01bbebc",
  "path": "/obh/odeme-emri",
  "timestamp": "2021-08-13T09:55:23+03:00",
  "httpCode": 401,
  "httpMessage": "Not Found",
  "moreInformation": "Resource Schema validation error",
  "moreInformationTr": "Alan doğrulama hatası",
  "errorCode": "TR.OBHS.Resource.InvalidFormat",
  "fieldErrors": [
    {
      "objectName": "odemeEmriRizasi",
      "field": "rizaNo",
      "messageTr": "boyut '1' ile '128' arasında olmalı",
      "message": "size must be between '1' and '128'",
      "code": "TR.OBHS.Field.Invalid"
    }
  ]
}
```


```
HTTP/1.1 403 Forbidden
Content-Type: application/json
```


```json
{
  "id": "2b5f0fb2-730b-11e8-adc0-fa7ae01bbebc",
  "path": "/obh/odeme-emri",
  "timestamp": "2021-08-13T09:55:23+03:00",
  "httpCode": 401,
  "httpMessage": "Not Found",
  "moreInformation": "Resource Schema validation error",
  "moreInformationTr": "Alan doğrulama hatası",
  "errorCode": "TR.OBHS.Resource.InvalidFormat",
  "fieldErrors": [
    {
      "objectName": "odemeEmriRizasi",
      "field": "rizaNo",
      "messageTr": "boyut '1' ile '128' arasında olmalı",
      "message": "size must be between '1' and '128'",
      "code": "TR.OBHS.Field.Invalid"
    }
  ]
}
```