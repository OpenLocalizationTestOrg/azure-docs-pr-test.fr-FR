---
title: "aaaEncrypting votre contenu avec chiffrement de stockage à l’aide des API REST de AMS"
description: "Découvrez comment tooencrypt votre contenu avec chiffrement de stockage à l’aide des API REST de AMS."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a0a79f3d-76a1-4994-9202-59b91a2230e0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: d5f8cb8dd1dcded76c9fededccc772d8102ccbad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypting-your-content-with-storage-encryption"></a>Chiffrer votre contenu avec le chiffrement de stockage

Il est vivement recommandé tooencrypt votre contenu localement avec AES-256 bits de chiffrement, puis le télécharger tooAzure Storage où il sera stocké et chiffré au repos.

Cet article donne une vue d’ensemble du chiffrement de stockage AMS et vous montre comment tooupload hello stockage chiffré dans le contenu :

* Créez une clé de contenu.
* Créez une ressource. Définissez hello AssetCreationOption tooStorageEncryption lors de la création de hello actif.
  
     Les éléments multimédias chiffrés ont toobe associé aux clés de contenu.
* Ressource de contenu toohello clé lien hello.  
* Définir le chiffrement hello les paramètres sur les entités AssetFile hello.

## <a name="considerations"></a>Considérations 

Si vous voulez toodeliver un élément multimédia chiffré de stockage, vous devez configurer la stratégie de remise de l’élément multimédia hello. Avant que votre élément multimédia peut être transmis en continu, hello de diffusion en continu flux et chiffrement de stockage de serveur supprime hello votre contenu à l’aide de hello spécifié de stratégie de remise. Pour plus d'informations, consultez [Configuration des stratégies de distribution de ressources](media-services-rest-configure-asset-delivery-policy.md).

Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP. Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md). 

## <a name="connect-toomedia-services"></a>Connecter les Services de tooMedia

Pour plus d’informations sur la façon dont tooconnect toohello AMS API, consultez [hello accès API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Après vous être connecté toohttps://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI de Media Services. Vous devez effectuer les appels suivants toohello nouvel URI.

## <a name="storage-encryption-overview"></a>Vue d’ensemble du chiffrement du stockage
s’applique le chiffrement de stockage Hello AMS **AES-CTR** mode chiffrement toohello intégralité du fichier.  Le mode AES-CTR est un chiffrement par blocs qui permet de chiffrer des données de longueur arbitraire sans avoir besoin de remplissage. Il s’exécute par chiffrement un bloc de compteur avec l’algorithme AES de hello et ensuite la sortie de hello XOR-effectue une opération d’AES avec hello données tooencrypt ou de déchiffrer.  bloc de compteur Hello utilisé est construit en copiant la valeur hello hello InitializationVector toobytes 0 too7 de la valeur du compteur hello et too15 octets 8 de la valeur du compteur hello sont définies toozero. Du bloc de compteur de 16 octets hello, octets 8 too15 (c'est-à-dire hello octets les moins significatifs) sont utilisés comme un entier non signé simple 64 bits qui est incrémenté d’un pour chaque bloc de données traitées et est conservé dans l’ordre d’octet du réseau. Notez que si cet entier atteint la valeur maximale hello (0xFFFFFFFFFFFFFFFF) puis incrémenter réinitialise hello bloc compteur toozero (too15 octets 8) sans affecter hello autres 64 bits du compteur de hello (autrement dit, les too7 octets 0).   Dans l’ordre toomaintain hello la sécurité de chiffrement de mode hello AES-CTR, hello InitializationVector valeur pour un identificateur de clé donnée pour chaque clé de contenu doit être unique pour chaque fichier et de fichiers doivent être inférieure à 2 ^ 64 blocs de longueur.  Il s’agit de tooensure une valeur de compteur n’est jamais réutilisé avec une clé donnée. Pour plus d’informations sur le mode CTR hello, consultez [cette page wiki](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (article wiki de hello utilise le terme hello « Nonce » au lieu de « InitializationVector »).

Utilisez **le chiffrement de stockage** tooencrypt votre contenu en clair localement avec AES-256 bits de chiffrement, puis le télécharger tooAzure Storage où il est stocké et chiffré au repos. Les éléments multimédias protégés par chiffrement de stockage sont automatiquement déchiffrés et placés dans un tooencoding préalable de système de fichiers chiffrés et éventuellement RE-chiffrée toouploading préalable comme un nouvel élément multimédia de sortie. Hello est principalement utilisé pour le chiffrement de stockage lorsque vous souhaitez toosecure vos fichiers multimédias d’entrée de haute qualité avec un chiffrement renforcé au reste sur le disque.

Dans l’ordre toodeliver un élément multimédia chiffré de stockage, vous devez configurer la stratégie de remise de hello actif afin que Media Services sache comment vous souhaitez que toodeliver votre contenu. Avant que votre élément multimédia peut être transmis en continu, hello de diffusion en continu flux et chiffrement de stockage de serveur supprime hello votre contenu à l’aide de hello spécifié de stratégie de remise (par exemple, AES, chiffrement commun ou aucun chiffrement).

## <a name="create-contentkeys-used-for-encryption"></a>Créer des ContentKeys utilisées pour le chiffrement
Les éléments multimédias chiffrés ont toobe associé à la clé de chiffrement de stockage. Vous devez créer hello contenu toobe clé utilisé pour le chiffrement avant de créer des fichiers d’éléments multimédias hello. Cette section décrit comment toocreate une clé de contenu.

Hello Voici les étapes générales pour la génération de clés de contenu que vous associerez avec les composants qui vous voulez toobe chiffré. 

1. Pour le chiffrement du stockage, générez de façon aléatoire une clé AES de 32 octets. 
   
    Ce sera la clé de contenu hello pour votre élément multimédia, ce qui signifie que tous les fichiers associés à cet élément multimédia sera peut-être toouse hello même clé de contenu pendant le déchiffrement. 
2. Appelez hello [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) et [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) tooget de méthodes hello certificat X.509 correct doit être utilisé tooencrypt votre clé de contenu.
3. Chiffrer votre clé de contenu avec une clé publique du certificat X.509 de hello hello. 
   
   Media Services .NET SDK utilise RSA avec OAEP lorsque vous effectuez un chiffrement de hello.  Vous pouvez voir un exemple .NET Bonjour [EncryptSymmetricKeyData fonction](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).
4. Créez une valeur de somme de contrôle calculée à l’aide d’identificateur de clé hello et clé de contenu. Hello .NET l’exemple suivant calcule la somme de contrôle hello à l’aide de la partie GUID de hello d’identificateur de clé hello et hello effacer la clé de contenu.

        public static string CalculateChecksum(byte[] contentKey, Guid keyId)
        {
            const int ChecksumLength = 8;
            const int KeyIdLength = 16;

            byte[] encryptedKeyId = null;

            // Checksum is computed by AES-ECB encrypting hello KID
            // with hello content key.
            using (AesCryptoServiceProvider rijndael = new AesCryptoServiceProvider())
            {
                rijndael.Mode = CipherMode.ECB;
                rijndael.Key = contentKey;
                rijndael.Padding = PaddingMode.None;

                ICryptoTransform encryptor = rijndael.CreateEncryptor();
                encryptedKeyId = new byte[KeyIdLength];
                encryptor.TransformBlock(keyId.ToByteArray(), 0, KeyIdLength, encryptedKeyId, 0);
            }

            byte[] retVal = new byte[ChecksumLength];
            Array.Copy(encryptedKeyId, retVal, ChecksumLength);

            return Convert.ToBase64String(retVal);
        }

1. Créer la clé de contenu hello avec hello **EncryptedContentKey** (converties en chaîne encodée toobase64), **ProtectionKeyId**, **ProtectionKeyType**,  **ContentKeyType**, et **Checksum** valeurs que vous avez reçu dans les étapes précédentes.

    Pour le chiffrement de stockage, hello propriétés suivantes doivent être incluses dans le corps de la demande hello.

    Propriété du corps de la demande    | Description
    ---|---
    Id | Hello Id de ContentKey que nous générons nous-mêmes hello suivant à l’aide de mettre en forme, « Kid :<NEW GUID>».
    ContentKeyType | Type de clé de contenu hello il s’agit en tant qu’entier pour cette clé de contenu. Nous transmettons la valeur hello 1 pour le chiffrement de stockage.
    EncryptedContentKey | Nous créons une valeur de clé de contenu qui est une valeur de 256 bits (32 octets). clé de Hello est chiffré à l’aide de hello stockage certificat X.509 de chiffrement que nous récupérons à partir de Microsoft Azure Media Services en exécutant une demande HTTP GET hello GetProtectionKeyId et GetProtectionKey méthodes. Par exemple, consultez hello suivant le code .NET : hello **EncryptSymmetricKeyData** méthode définie [ici](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).
    ProtectionKeyId | Cela est hello id de clé de protection pour le certificat X.509 de chiffrement de stockage de hello a été utilisé tooencrypt notre clé de contenu.
    ProtectionKeyType | Il s’agit de type de chiffrement de hello pour la clé de protection hello clé de contenu utilisés tooencrypt hello. Cette valeur est StorageEncryption(1) dans notre exemple.
    Somme de contrôle |somme de contrôle calculée Hello MD5 pour la clé de contenu hello. Elle est calculée en chiffrant l’Id de contenu hello avec la clé de contenu hello. Hello exemple de code montre comment toocalculate hello somme de contrôle.


### <a name="retrieve-hello-protectionkeyid"></a>Récupérer hello ProtectionKeyId
Bonjour à l’exemple suivant montre comment tooretrieve hello ProtectionKeyId, une empreinte de certificat pour le certificat hello vous devez utiliser lors du chiffrement de votre clé de contenu. Effectuez cette étape toomake que vous avez déjà les certificats appropriés hello sur votre ordinateur.

Demande :

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net

Réponse :

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 139
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    x-ms-request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:42:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String","value":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C"}

### <a name="retrieve-hello-protectionkey-for-hello-protectionkeyid"></a>Récupérer ProtectionKey de hello pour hello ProtectionKeyId
Hello suivant montre comment le certificat X.509 de tooretrieve hello à l’aide de hello ProtectionKeyId vous avez reçu dans l’étape précédente de hello.

Demande :

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net

Réponse :

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1227
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    x-ms-request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 05 Feb 2015 07:52:30 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String",
    "value":"MIIDSTCCAjGgAwIBAgIQqf92wku/HLJGCbMAU8GEnDANBgkqhkiG9w0BAQQFADAuMSwwKgYDVQQDEyN3YW1zYmx1cmVnMDAxZW5jcnlwdGFsbHNlY3JldHMtY2VydDAeFw0xMjA1MjkwNzAwMDBaFw0zMjA1MjkwNzAwMDBaMC4xLDAqBgNVBAMTI3dhbXNibHVyZWcwMDFlbmNyeXB0YWxsc2VjcmV0cy1jZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzR0SEbXefvUjb9wCUfkEiKtGQ5Gc328qFPrhMjSo+YHe0AVviZ9YaxPPb0m1AaaRV4dqWpST2+JtDhLOmGpWmmA60tbATJDdmRzKi2eYAyhhE76MgJgL3myCQLP42jDusWXWSMabui3/tMDQs+zfi1sJ4Ch/lm5EvksYsu6o8sCv29VRwxfDLJPBy2NlbV4GbWz5Qxp2tAmHoROnfaRhwp6WIbquk69tEtu2U50CpPN2goLAqx2PpXAqA+prxCZYGTHqfmFJEKtZHhizVBTFPGS3ncfnQC9QIEwFbPw6E5PO5yNaB68radWsp5uvDg33G1i8IT39GstMW6zaaG7cNQIDAQABo2MwYTBfBgNVHQEEWDBWgBCOGT2hPhsvQioZimw8M+jOoTAwLjEsMCoGA1UEAxMjd2Ftc2JsdXJlZzAwMWVuY3J5cHRhbGxzZWNyZXRzLWNlcnSCEKn/dsJLvxyyRgmzAFPBhJwwDQYJKoZIhvcNAQEEBQADggEBABcrQPma2ekNS3Wc5wGXL/aHyQaQRwFGymnUJ+VR8jVUZaC/U/f6lR98eTlwycjVwRL7D15BfClGEHw66QdHejaViJCjbEIJJ3p2c9fzBKhjLhzB3VVNiLIaH6RSI1bMPd2eddSCqhDIn3VBN605GcYXMzhYp+YA6g9+YMNeS1b+LxX3fqixMQIxSHOLFZ1G/H2xfNawv0VikH3djNui3EKT1w/8aRkUv/AAV0b3rYkP/jA1I0CPn0XFk7STYoiJ3gJoKq9EMXhit+Iwfz0sMkfhWG12/XO+TAWqsK1ZxEjuC9OzrY7pFnNxs4Mu4S8iinehduSpY+9mDd3dHynNwT4="}

### <a name="create-hello-content-key"></a>Créer la clé de contenu hello
Après avoir récupéré le certificat X.509 de hello et utilisé son tooencrypt de clé publique de votre clé de contenu, créez un **ContentKey** entité et définissez sa propriété de valeurs en conséquence.

Une des valeurs hello que vous devez définir quand créer hello contenu clé est de type de hello. En cas de chiffrement de stockage hello, valeur de hello est « 1 ». 

Hello suivant montre l’exemple de comment toocreate un **ContentKey** avec un **ContentKeyType** définie pour le chiffrement de stockage (« 1 ») et hello **ProtectionKeyType** défini trop « 0 » tooindicate qui hello Id de clé de protection est l’empreinte de certificat X.509 hello.  

Demande

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net
    {
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C", 
    "ContentKeyType":"1", 
    "ProtectionKeyType":"0",
    "EncryptedContentKey":"your encrypted content key",
    "Checksum":"calculated checksum"
    }

Réponse :

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 777
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A9c8ea9c6-52bd-4232-8a43-8e43d8564a99')
    Server: Microsoft-IIS/8.5
    request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    x-ms-request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:37:46 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeys/@Element",
    "Id":"nb:kid:UUID:9c8ea9c6-52bd-4232-8a43-8e43d8564a99","Created":"2015-02-04T02:37:46.9684379Z",
    "LastModified":"2015-02-04T02:37:46.9684379Z",
    "ContentKeyType":1,
    "EncryptedContentKey":"your encrypted content key",
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C",
    "ProtectionKeyType":0,
    "Checksum":"calculated checksum"}

## <a name="create-an-asset"></a>Créer une ressource
Hello suivant montre l’exemple de comment toocreate un élément multimédia.

**Demande HTTP**

    POST https://media.windows.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"BigBuckBunny" "Options":1}

**Réponse HTTP**

En cas de réussite, suivant de hello est retournée :

    HTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 452
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    request-id: e98be122-ae09-473a-8072-0ccd234a0657
    x-ms-request-id: e98be122-ae09-473a-8072-0ccd234a0657
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT
    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny.mp4",
       "Options":1,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

## <a name="associate-hello-contentkey-with-an-asset"></a>Associer des hello ContentKey à un élément multimédia
Après avoir créé le hello ContentKey, associez-le à votre élément multimédia à l’aide de l’opération de hello $links, comme indiqué dans hello l’exemple suivant :

Demande :

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Afbd7ce05-1087-401b-aaae-29f16383c801')/$links/ContentKeys HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeys('nb%3Akid%3AUUID%3A01e6ea36-2285-4562-91f1-82c45736047c')"}

Réponse :

    HTTP/1.1 204 No Content 

## <a name="create-an-assetfile"></a>Création d’un AssetFile
Hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entité représente un fichier vidéo ou audio qui est stocké dans un conteneur d’objets blob. Un fichier de ressources est toujours associé à une ressource et une ressource peut contenir un ou plusieurs fichiers de ressources. tâche d’encodeur Media Services Hello échoue si un objet de fichier actif n’est pas associé à un fichier numérique dans un conteneur d’objets blob.

Notez que hello **AssetFile** instance et le fichier multimédia lui-même de hello sont deux objets distincts. instance AssetFile de Hello contient des métadonnées sur le fichier du média hello, tandis que le fichier du média hello contient le contenu du média réel hello.

Après avoir téléchargé votre fichier multimédia numérique sur un conteneur d’objets blob, vous allez utiliser hello **fusion** tooupdate hello AssetFile HTTP demande des informations sur votre fichier de support (non illustré dans cette rubrique). 

**Demande HTTP**

    POST https://media.windows.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    Content-Length: 164

    {  
       "IsEncrypted":"true",
       "EncryptionScheme" : "StorageEncryption", 
       "EncryptionVersion" : "1.0",       
       "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector" : "397304628502661816</d:InitializationVector",
       "Options":0,
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }

**Réponse HTTP**

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 535
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5')
    Server: Microsoft-IIS/8.5
    request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    x-ms-request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 00:34:07 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Files/@Element",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "Name":"BigBuckBunny.mp4",
       "ContentFileSize":"0",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "EncryptionVersion": "1.0",
       "EncryptionScheme": "StorageEncryption",
       "IsEncrypted":true,
       "EncryptionKeyId":"nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector":"397304628502661816</d:InitializationVector",
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }
