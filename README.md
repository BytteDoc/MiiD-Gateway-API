# MiiD Gateway Api

![N|Solid](https://miid.bio/wp-content/uploads/2021/06/MiID_ico-100x100.png)

**MiiD Gateway** is an API that provides the functionality to connect your platform or system to MiiD Gateway Service 

## Operations

 - [Authorization - Login](#ApiGarewayAutorization).
 - [Genetate Process Token](#ApiGarewayNewToken).
 - [Get Token By Value](#ApiGarewayGetTokenByValue).
 - [GetResultByExternalIdProcess](#ApiGarewayGetResultByExternalIdProcess).
 
**MiiD Gateway**  is a commercial Service, to use it contact info@bytte.com.co for instructions on how to obtain the required resources and access

**MiiD** is a trademark registered by Bytte S.A.S 
 
## Operations:
## <a name="ApiGarewayAutorization"></a>Api Gateway Autorization
To use the API, you must have a valid user assigned by MiiD team!!

Url - Login User - POST
https://services.miid.bio/Login/LoginUser/

```json
{
    "emailAddress": "MyUseraccess@mymail.bio",
    "password": "MyPassword"
}
```
If user/Password are valid, Api returns similar JSON Response

```json
{
    "tokenType": "Bearer",
    "accessToken": "eyJ0eXAiiJKV1QiLCJhbGc....",
    "successOperation": true
}
```

Use Access Token to call the other services provided by this api

## <a name="ApiGarewayNewToken"></a>Generate New Process Token

In your project or system, the first step is generate a new Token In this token, We correlationate your transaction Id with MiiD system

Variables to Send:

* **enterpriseClientId** = Is a Identifier provided by MiiD Team. This Identifier is unique by client 
* **externalId** = Is a current client Identifier (in the client information system)
* **documentType** = Is a document type from user to authenticate 
* **documentNumber** = Is a document number from user to authenticate
* **returnUrl** = Is a URL/URI. When MiiD Process Ends, MiiD system redirect to this Url to continue the client process

Url - GenetateProcessToken - POST
> https://services.miid.bio/Gateway/GenetateProcessToken/

Example Json
```sh
--header Authorization": Bearer eyJ0eXAi......."

```
Body
```json
{   
  "enterpriseClientId": 12,  
  "externalId": "aaA11234",
  "documentType": "1",
  "documentNumber": "1234567890",
  "returnUrl": "http://clientdomain/clientsite/"
}
```
```json
Response:
{
    "processUrl": "http://miid.gateway.bio/w/028092021135547637684341479019124",
    "tokenValue": "028092021135547637684341479019124",
    "creationDate": "2021-09-28T13:55:47.9025853+00:00",
    "successOperation": true,
    "message": "Token generated!"
}
```
With URL in field **processUrl** you can proceed to redirect your application or system to MiiD Authentication process.

When this process completes, the MiiD system will redirect to the URL sent in the **returnUrl** field of the request

------

## <a name="ApiGarewayGetTokenByValue"></a>Get Token By Value
This operation returns detailed information of the token generated previously

Variables to Send:

* **TokenId** = Is a Token Value previously generated

Response fields:

* **id** = MiiD Internal Identifier
* **creationDate** = Creation Date
* **tokenValue** = Token Identifier generated
* **enterpriseClientId** = Is a Identifier provided by MiiD Team. This Identifier is unique by client 
* **externalId** = Is a current client Identifier (in the client information system)
* **documentType** = Is a document type from user to authenticate 
* **documentNumber** = Is a document number from user to authenticate
* **returnUrl** = Is a URL/URI. When MiiD Process Ends, MiiD system redirect to this Url to continue the client process
* **processUrl** = Is the Url to redirect your application or system to MiiD Authentication process.

Url - GenetateProcessToken - GET
> https://services.miid.bio/Gateway/{TokenID}/

Example Json
```sh
--header Authorization": Bearer eyJ0eXAi......."
```
Body: Empty

```json
Response:
{
    "id": "b9f7570b-0e1d-4789-bbd9-...",
    "enterpriseClientId": 0,
    "creationDate": "2021-09-28T13:55:47.903",
    "tokenValue": "028092021135547637684341479019124",
    "externalId": "aaA11234",
    "documentType": "1",
    "documentNumber": "1234567890",
    "returnUrl": "http://clientdomain/clientsite/",
    "processUrl": "http://miid.gateway.bio/w/028092021135547637684341479019124"
}
```
---
## <a name="ApiGarewayGetResultByExternalIdProcess"></a>Get Result By External IdProcess
This operation returns detailed information from a Authentication process

Variables to Send:

* **TokenId** = Is a Token Value previously generated

Response fields:
* **enterpriseClientId** = Is a Identifier provided by MiiD Team. This Identifier is unique by client 
* **id** = MiiD Internal Identifier
* **creationDate** = Creation Date
* **finishDate** = Finish Date
* **personId** = MiiD internal Person Identifier
* **type** = Process Type
* **origin** = Origin Type
* **barcodeMrz** = Barcode/MRZ Base64 From document
* **externalId** = Is a current client Identifier (in the client information system)
* **scoreFingerBarcode** = Score Match fingerprint captured Vs document fingerprint
* **scoreFace** = Score Match Face captured Vs face in document
* **scoreLiveness** = Score Face Liveness
* **scoreOcrBarcode** = Score Match Ocr Vs BarCode
* **scoreAniBarcode** = Score Match Ani Vs BarCode
* **scoreAniOcr** = Score Match Ani Vs Ocr
* **scoreWeigthDocument** = Score Weighted weight greater than configured  
* **scoreBykeeper** = Result ByKeeper Validation (0 - false, 1 true)
* **scoreList** = Score restrictive lists
* **scoreProcess** = General Score

* **Status Values** 
* *0* = Process not executed 
* *1* = Process execute and finish correctly
* *2* = The process runs and does not finish correctly

* **statusFingerBarcode** = Status Match fingerprint captured Vs document fingerprint (0,1,2)
* **statusFace** = Status Match Face captured Vs face in document (0,1,2)
* **statusLiveness** = Status Face Liveness (0,1,2)
* **statusOcrBarcode** = Status Match Ocr Vs BarCode (0,1,2)
* **statusAniBarcode** = Status Match Ani Vs BarCode (0,1,2)
* **statusAniOcr** = Status Match Ani Vs Ocr (0,1,2)
* **statusWeigthDocument** = Status Weighted weight greater than configured (0,1,2)
* **statusBykeeper** = Status ByKeeper (0,1,2)
* **statusList** =  Status restrictive lists
* **statusProcess** = General Process Status (True = User Authenticated)
* **inProcess** =If True, the process has not finished and you must wait for this flag to change to false 

Url - GenetateProcessToken - GET
> https://services.miid.bio/Person/GetResultByExternalIdProcess/{TokenID}/

Example Json
```sh
--header Authorization": Bearer eyJ0eXAi......."
```
Body: Empty

```json
Response:
{
    "id": "5c642638-...",
    "enterpriseClientId": 0,
    "personId": "abf7886b-4a35-4162-...",
    "creationDate": "2021-08-13T18:09:32.157",
    "finishDate": "2021-08-13T18:09:42.587",
    "externalId": "11223344-111123-2010",
    "type": "Enroll",
    "origin": "APP",
    "barcodeMrz": "MDIwMTYyOTAxMTcxQSAgICAgICAgIDAxOTU1NjU3MTQ0ICAgICAgIDA5OTQyNzE3MDA4MDIwODIyM0RJQVogICAgICAgICAgICAgICAgICAgQkFMTEVTVEVST1MgICAgICAgICAgICBBTExBTiAgICAgICAgICAgICAgICAgIFlFSVNTT04gICAgICAgICAgICAgICAgME0xOTgyMTEyOTAxNTAwMUIrIDKxuXhnb3RyfHiIlXOVan6QnmdkioiVWXSUVKR6V3eYUKhhY5dVX3Sjc0Ovfq6FZ6FUkkxhq1agnmFFWZ5zPEaCslm3gEWIVUZMTm2vVEN/NEOMaDa5jUWTPmWUM4S2jS9Hnoy4pa97ulc2xGBESK6ujL9XMDbdObz27PmJKVvq7QAAAlMwQuDNAA/w7VJXOxffA/kxMkbGBcNKPL+VbOpRN7G5do6IcHppZXhtl1+Fj5SXbZqRc6OOn11llWKidnuoXJyXnlB7cqmBVKNvYlplVV6kUJJLe6mEiFCrcX1NWqmsjk+eoliLST91tYJeSZa1WbNMVrVqt3M8hT9jTa6RQo0+VbqmSD9ZvWiKxTlem8BDUDJ860w589ZVW+YbSzAAWECRTB+BDIUQTbETEPTOS8vl7RwKYFRVkOZRr4t6PvPL71bVvsxGS2DhxAcTxyp2GYq/KM5Ahy+WD7rExXOIaaH9pGh0EZVi",    
    "scoreFingerBarcode": 1423,    
    "scoreFace": 76,
    "scoreLiveness": 99,
    "scoreOcrBarcode": 100,
    "scoreAniBarcode": 100,
    "scoreAniOcr": 70,
    "scoreWeigthDocument": 100,   
    "scoreListFingerprint": 0,
    "scoreProcess": 100,   
    "statusFingerBarcode": 1,    
    "statusFace": 1,
    "statusLiveness": 1,
    "statusOcrBarcode": 1,
    "statusAniBarcode": 1,
    "statusAniOcr": 1,
    "statusWeigthDocument": 1,     
    "statusBykeeper": 1,
    "statusList": 1,
    "statusProcess": true,
    "statusReturn": "SUCCESS",
    "inProcess": false
}
```



 
