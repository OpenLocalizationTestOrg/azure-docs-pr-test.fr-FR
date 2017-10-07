---
title: "fichiers aaaUpload dans un compte Media Services à l’aide de REST | Documents Microsoft"
description: "Découvrez comment tooget média du contenu dans Media Services création et téléchargement d’éléments multimédias."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 41df7cbe-b8e2-48c1-a86c-361ec4e5251f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 2a92cecdc32d747d7a478946f069c15931eb32b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-rest"></a>Charger des fichiers dans un compte Media Services à l’aide de REST
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> * [Portail](media-services-portal-upload-files.md)
> 
> 

Dans Media Services, vous téléchargez vos fichiers numériques dans une ressource. Hello [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entité peut contenir vidéo, audio, images, collections de miniatures, texte assure le suivi et sous-titres fichiers (et les métadonnées hello sur ces fichiers.)  Une fois que les fichiers de hello sont téléchargés en ressource de hello, votre contenu est stocké en toute sécurité dans le cloud hello pour le traitement et la diffusion en continu. 

> [!NOTE]
> Hello suivant considérations s’appliquent :
> 
> * Media Services utilise la valeur hello hello IAssetFile.Name propriété lors de la génération d’URL pour hello de diffusion en continu de contenu (par exemple, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Pour cette raison, l’encodage par pourcentage n’est pas autorisé. Hello valeur Hello **nom** propriété ne peut pas avoir un des éléments suivants de hello [% réservés d’encodage de caractères](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): ! *' () ; : @& = + $, / ? % # [] ». En outre, il ne peut exister un '.' pour l’extension de nom de fichier hello.
> * la longueur du nom de hello Hello ne doit pas dépasser 260 caractères.
> * Il existe une taille de fichier maximale toohello limite pris en charge pour le traitement dans Media Services. Consultez [cela](media-services-quotas-and-limitations.md) pour plus d’informations sur la limite de taille de fichier hello.
> 

flux de travail Hello pour le téléchargement des éléments multimédias est divisé en hello les sections suivantes :

* Créer une ressource
* Chiffrer une ressource (facultatif)
* Télécharger un stockage tooblob de fichier

AMS vous permet également de ressources tooupload en bloc. Pour plus d’informations, consultez [cette](media-services-rest-upload-files.md#upload_in_bulk) section.

> [!NOTE]
> Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP. Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).
> 

## <a name="connect-toomedia-services"></a>Connecter les Services de tooMedia

Pour plus d’informations sur la façon dont tooconnect toohello AMS API, consultez [hello accès API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Après vous être connecté toohttps://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI de Media Services. Vous devez effectuer les appels suivants toohello nouvel URI.

## <a name="upload-assets"></a>Téléchargement de ressources

### <a name="create-an-asset"></a>Créer une ressource

Une ressource est un conteneur pour plusieurs types ou ensembles d’objets dans Media Services, y compris des fichiers vidéo, audio, des images, des collections de miniatures, des pistes textuelles et des légendes. Bonjour API REST, création d’un élément multimédia requiert l’envoi de POST solliciter des Services de tooMedia et placer toutes les informations de propriété concernant votre élément multimédia dans le corps de la demande hello.

Une des propriétés hello que vous pouvez spécifier lorsque la création d’un élément multimédia est **Options**. **Options** est une valeur d’énumération qui décrit les options de chiffrement hello un élément multimédia peut être créé avec. Une valeur valide est une des valeurs hello dans liste hello ci-dessous, pas une combinaison de valeurs. 

* **None** = **0** : Aucun chiffrement ne sera utilisé. Il s’agit de valeur par défaut de hello. À noter que quand vous utilisez cette option, votre contenu n’est pas protégé pendant le transit ou le repos dans le stockage.
    Si vous envisagez de toodeliver un fichier MP4 à l’aide d’un téléchargement progressif, utilisez cette option. 
* **StorageEncrypted** = **1**: spécifiez si vous souhaitez pour votre toobe de fichiers chiffré avec chiffrement AES-256 bits pour le téléchargement et de stockage.
  
    Si votre ressource est stockée sous forme chiffrée, vous devez configurer une stratégie de remise de ressources. Pour plus d'informations, consultez [Configuration de la stratégie de remise de ressources](media-services-rest-configure-asset-delivery-policy.md).
* **CommonEncryptionProtected** = **2** : spécifie si vous téléchargez des fichiers protégés par une méthode de chiffrement commune (comme PlayReady). 
* **EnvelopeEncryptionProtected** = **4** : indique si vous téléchargez un contenu au format HLS chiffré avec des fichiers AES. Notez que les fichiers hello doivent avoir été codés et chiffrés par Transform Manager.

> [!NOTE]
> Si votre élément multimédia utilise le chiffrement, vous devez créer un **ContentKey** et liez-la tooyour actifs comme décrit dans la rubrique suivante de hello :[comment toocreate une ContentKey](media-services-rest-create-contentkey.md). Notez que, après avoir téléchargé les fichiers hello en ressource de hello, vous devez tooupdate propriétés de chiffrement hello sur hello **AssetFile** entité avec les valeurs hello que vous avez obtenus lors de hello **Asset** chiffrement. Cela à l’aide de hello **fusion** requête HTTP. 
> 
> 

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

    {"Name":"BigBuckBunny.mp4"}

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
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a>Création d’un AssetFile
Hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entité représente un fichier vidéo ou audio qui est stocké dans un conteneur d’objets blob. Un fichier de ressources est toujours associé à une ressource et une ressource peut contenir un ou plusieurs fichiers de ressources. tâche d’encodeur Media Services Hello échoue si un objet de fichier actif n’est pas associé à un fichier numérique dans un conteneur d’objets blob.

Notez que hello **AssetFile** instance et le fichier multimédia lui-même de hello sont deux objets distincts. instance AssetFile de Hello contient des métadonnées sur le fichier du média hello, tandis que le fichier du média hello contient le contenu du média réel hello.

Après avoir téléchargé votre fichier multimédia numérique sur un conteneur d’objets blob, vous allez utiliser hello **fusion** tooupdate hello AssetFile HTTP demande des informations sur votre fichier multimédia (comme indiqué plus loin dans la rubrique de hello). 

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
       "IsEncrypted":"false",
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
       "EncryptionVersion":null,
       "EncryptionScheme":null,
       "IsEncrypted":false,
       "EncryptionKeyId":null,
       "InitializationVector":null,
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }

### <a name="creating-hello-accesspolicy-with-write-permission"></a>Création de hello AccessPolicy avec autorisation d’écriture.

>[!NOTE]
>Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy). Vous devez utiliser hello ID de stratégie même si vous utilisez toujours hello même jours / autorisations d’accès, par exemple, les stratégies pour les localisateurs sont tooremain prévue en place pendant une longue période (non-téléchargement stratégies). Pour plus d’informations, consultez [cette rubrique](media-services-dotnet-manage-entities.md#limit-access-policies) .

Avant de télécharger des fichiers dans le stockage d’objets blob, définissez l’accès de hello droits de stratégie pour l’écriture de tooan actif. toodo que, VALIDEZ un toohello de demande HTTP entité de stratégies d’accès défini. N’oubliez pas de définir une valeur DurationInMinutes après la création ou vous recevrez en réponse un message d’erreur interne de serveur 500. Pour plus d’informations sur AccessPolicies, consultez [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).

Hello suivant montre l’exemple de comment toocreate une stratégie d’accès :

**Demande HTTP**

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"} 

**Demande HTTP**

    If successful, hello following response is returned:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 312
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae')
    Server: Microsoft-IIS/8.5
    request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    x-ms-request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:18:06 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#AccessPolicies/@Element",
       "Id":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "Created":"2015-01-18T22:18:06.6370575Z",
       "LastModified":"2015-01-18T22:18:06.6370575Z",
       "Name":"NewUploadPolicy",
       "DurationInMinutes":440.0,
       "Permissions":2
    }

### <a name="get-hello-upload-url"></a>Obtenir hello télécharger l’URL
tooreceive hello URL de téléchargement réelle, créer un localisateur SAS. Les localisateurs définissent l’heure de début de hello et le type du point de terminaison de connexion pour les clients qui tooaccess des fichiers dans un élément multimédia. Vous pouvez créer plusieurs entités Locator pour une donnée AccessPolicy et Asset paire toohandle client différents besoins et demandes. Chacun de ces localisateurs utilisent la valeur de StartTime hello plus la valeur DurationInMinutes hello hello AccessPolicy toodetermine hello durée une URL peut être utilisée. Pour plus d’informations, consultez la rubrique [Localisateur](https://docs.microsoft.com/rest/api/media/operations/locator).

Une URL SAS a hello suivant le format :

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

Certaines considérations s’appliquent :

* Vous ne pouvez avoir plus de cinq localisateurs uniques associés à une ressource donnée. Pour plus d’informations, consultez la rubrique Localisateur.
* Si vous avez besoin de tooupload vos fichiers immédiatement, vous devez définir les minutes de toofive valeur StartTime avant hello heure actuelle. Cela vient du fait qu’il peut exister un décalage horaire entre votre ordinateur client et Media Services. En outre, votre valeur StartTime doit être hello respectant le format de date/heure : AAAA-MM-JJThh (par exemple, « 2014-05-23T17:53:50Z »).    
* Il peut y avoir un 30 à 40 secondes après la création d’un localisateur toowhen, il est disponible pour une utilisation de retarder. Ce problème s’applique tooboth URL SAS et les localisateurs d’origine.

Bonjour à l’exemple suivant montre comment toocreate un localisateur d’URL SAS, tel que défini par hello la propriété de Type dans le corps de la demande hello (« 1 » pour un localisateur SAS) et « 2 » pour un localisateur d’origine à la demande. Hello **chemin d’accès** propriété retournée contient les URL de hello que vous devez utiliser tooupload votre fichier.

**Demande HTTP**

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }

**Réponse HTTP**

En cas de réussite, hello suivant la réponse est retournée :

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 949
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54')
    Server: Microsoft-IIS/8.5
    request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    x-ms-request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 03:01:29 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Locators/@Element",
       "Id":"nb:lid:UUID:af57bdd8-6751-4e84-b403-f3c140444b54",
       "ExpirationDateTime":"2015-02-19T00:05:53",
       "Type":1,
       "Path":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "BaseUri":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247",
       "ContentAccessComponent":"?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Name":null
    }

### <a name="upload-a-file-into-a-blob-storage-container"></a>Téléchargement d’un fichier dans un conteneur de stockage d’objets blob
Une fois que vous avez hello AccessPolicy et l’ensemble de la recherche, le fichier hello est tooan téléchargé conteneur de stockage d’objets Blob Azure à l’aide de hello API REST de stockage Azure. Vous devez télécharger les fichiers hello en tant qu’objets BLOB de blocs. Les objets blob de pages ne sont pas pris en charge par Azure Media Services.  

> [!NOTE]
> Vous devez ajouter le nom de fichier hello pour le fichier de hello souhaité tooupload toohello recherche **chemin d’accès** valeur reçue dans la section précédente de hello. Par exemple, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4? . . . 
> 
> 

Pour plus d’informations sur l’utilisation d’objets blob de stockage Microsoft Azure, consultez [API REST du service BLOB](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).

### <a name="update-hello-assetfile"></a>Mettre à jour hello AssetFile
Maintenant que vous avez téléchargé votre fichier, mettre à jour des informations hello FileAsset taille (et autres). Par exemple :

    MERGE https://media.windows.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


**Réponse HTTP**

Si la réussite, suivant de hello est retournée : HTTP/1.1 204 No Content

### <a name="delete-hello-locator-and-accesspolicy"></a>Supprimer hello recherche et la stratégie d’accès
**Demande HTTP**

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

**Réponse HTTP**

En cas de réussite, suivant de hello est retournée :

    HTTP/1.1 204 No Content 
    ...

**Demande HTTP**

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

**Réponse HTTP**

En cas de réussite, suivant de hello est retournée :

    HTTP/1.1 204 No Content 
    ...

## <a id="upload_in_bulk"></a>Téléchargement de ressources en bloc
### <a name="create-hello-ingestmanifest"></a>Créer hello IngestManifest
Hello IngestManifest est un conteneur pour un ensemble de ressources, des fichiers et des informations statistiques qui peuvent être utilisés progression de hello toodetermine de réception en bloc pour hello ensemble.

**Demande HTTP**

    POST https:// media.windows.net/API/IngestManifests HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 36
    Expect: 100-continue

    { "Name" : "ExampleManifestREST" }

### <a name="create-assets"></a>Création de ressources
Avant de créer hello IngestManifestAsset, vous devez toocreate hello actif qui sera achevé à l’aide de la réception en bloc. Une ressource est un conteneur pour plusieurs types ou ensembles d’objets dans Media Services, y compris des fichiers vidéo, audio, des images, des collections de miniatures, des pistes textuelles et des légendes. Bonjour API REST, création d’un élément multimédia requiert envoyant un tooMicrosoft de demande HTTP POST Azure Media Services et en plaçant toutes les informations de propriété concernant votre élément multimédia dans le corps de la demande hello. Dans cet exemple, hello actif est créé à l’aide de l’option storageencrption (1) hello incluse avec le corps de la demande hello.

**Réponse HTTP**

    POST https://media.windows.net/API/Assets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 55
    Expect: 100-continue

    { "Name" : "ExampleManifestREST_Asset", "Options" : 1 }

### <a name="create-hello-ingestmanifestassets"></a>Créer hello IngestManifestAssets
IngestManifestAssets représente les ressources dans un IngestManifest qui sont utilisées avec la réception en bloc. manifeste de hello asset toohello Hello essentiellement de lier. Azure Media Services surveille en interne pour le téléchargement du fichier hello selon les IngestManifestFiles collection associée toohello IngestManifestAsset. Une fois ces fichiers sont téléchargés, asset de hello est terminée. Vous pouvez créer un IngestManifestAsset avec une demande HTTP POST. Dans le corps de la demande hello, inclure hello Id d’IngestManifest et hello Id d’élément multimédia que hello IngestManifestAsset doit lier pour la réception en bloc.

**Réponse HTTP**

    POST https://media.windows.net/API/IngestManifestAssets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 152
    Expect: 100-continue
    { "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "Asset" : { "Id" : "nb:cid:UUID:b757929a-5a57-430b-b33e-c05c6cbef02e"}}


### <a name="create-hello-ingestmanifestfiles-for-each-asset"></a>Créer hello IngestManifestFiles pour chaque élément multimédia
Un IngestManifestFile représente un objet blob réel vidéo ou audio qui sera téléchargé dans le cadre de la réception en bloc pour une ressource. Propriétés ne sont pas requises, sauf si l’élément multimédia de hello utilise une option de chiffrement liées au chiffrement. exemple Hello utilisé dans cette section illustre la création d’un IngestManifestFile qui fait appel au StorageEncryption pour hello que élément multimédia créé précédemment.

**Réponse HTTP**

    POST https://media.windows.net/API/IngestManifestFiles HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 367
    Expect: 100-continue

    { "Name" : "REST_Example_File.wmv", "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "ParentIngestManifestAssetId" : "nb:maid:UUID:beed8531-9a03-9043-b1d8-6a6d1044cdda", "IsEncrypted" : "true", "EncryptionScheme" : "StorageEncryption", "EncryptionVersion" : "1.0", "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510" }

### <a name="upload-hello-files-tooblob-storage"></a>Télécharger les fichiers de hello tooBlob stockage
Vous pouvez utiliser n’importe quelle application de client haute vitesse capable de télécharger le conteneur de stockage blob pour les fichiers actifs hello toohello Uri fourni par hello propriété BlobStorageUriForUpload Hello IngestManifest. [Aspera On Demand pour l'Application Azure](http://go.microsoft.com/fwlink/?LinkId=272001)est un service de téléchargement à grande vitesse intéressant.

### <a name="monitor-bulk-ingest-progress"></a>Surveillance de la progression de la réception en bloc
Vous pouvez surveiller la progression de hello de réception des opérations pour un IngestManifest en interrogeant la propriété de statistiques hello Hello IngestManifest en bloc. Cette propriété est de type complexe [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics). toopoll hello propriété Statistics, soumettre une demande HTTP GET en passant hello ID d’IngestManifest.

## <a name="create-contentkeys-used-for-encryption"></a>Créer des ContentKeys utilisées pour le chiffrement
Si votre élément multimédia utilise le chiffrement, vous devez créer hello ContentKey toobe est utilisé pour le chiffrement avant de créer des fichiers d’éléments multimédias hello. Pour le chiffrement de stockage, hello propriétés suivantes doivent être incluses dans le corps de la demande hello.

| Propriété du corps de la demande | Description |
| --- | --- |
| Id |Hello Id de ContentKey que nous générons nous-mêmes hello suivant à l’aide de mettre en forme, « Kid :<NEW GUID>». |
| ContentKeyType |Type de clé de contenu hello il s’agit en tant qu’entier pour cette clé de contenu. Nous transmettons la valeur hello 1 pour le chiffrement de stockage. |
| EncryptedContentKey |Nous créons une valeur de clé de contenu qui est une valeur de 256 bits (32 octets). clé de Hello est chiffré à l’aide de hello stockage certificat X.509 de chiffrement que nous récupérons à partir de Microsoft Azure Media Services en exécutant une demande HTTP GET hello GetProtectionKeyId et GetProtectionKey méthodes. |
| ProtectionKeyId |Cela est hello id de clé de protection pour le certificat X.509 de chiffrement de stockage de hello a été utilisé tooencrypt notre clé de contenu. |
| ProtectionKeyType |Il s’agit de type de chiffrement de hello pour la clé de protection hello clé de contenu utilisés tooencrypt hello. Cette valeur est StorageEncryption(1) dans notre exemple. |
| Somme de contrôle |somme de contrôle calculée Hello MD5 pour la clé de contenu hello. Elle est calculée en chiffrant l’Id de contenu hello avec la clé de contenu hello. Hello exemple de code montre comment toocalculate hello somme de contrôle. |

**Réponse HTTP**

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 572
    Expect: 100-continue

    {"Id" : "nb:kid:UUID:316d14d4-b603-4d90-b8db-0fede8aa48f8", "ContentKeyType" : 1, "EncryptedContentKey" : "Y4NPej7heOFa2vsd8ZEOcjjpu/qOq3RJ6GRfxa8CCwtAM83d6J2mKOeQFUmMyVXUSsBCCOdufmieTKi+hOUtNAbyNM4lY4AXI537b9GaY8oSeje0NGU8+QCOuf7jGdRac5B9uIk7WwD76RAJnqyep6U/OdvQV4RLvvZ9w7nO4bY8RHaUaLxC2u4aIRRaZtLu5rm8GKBPy87OzQVXNgnLM01I8s3Z4wJ3i7jXqkknDy4VkIyLBSQvIvUzxYHeNdMVWDmS+jPN9ScVmolUwGzH1A23td8UWFHOjTjXHLjNm5Yq+7MIOoaxeMlKPYXRFKofRY8Qh5o5tqvycSAJ9KUqfg==", "ProtectionKeyId" : "7D9BB04D9D0A4A24800CADBFEF232689E048F69C", "ProtectionKeyType" : 1, "Checksum" : "TfXtjCIlq1Y=" }

### <a name="link-hello-contentkey-toohello-asset"></a>Lien hello ContentKey toohello actif
Hello ContentKey est tooone associé ou les plus actifs en envoyant une demande HTTP POST. Hello demande suivante est un exemple toolink hello exemple ContentKey toohello exemple d’élément multimédia par Id.

**Réponse HTTP**

    POST https://media.windows.net/API/Assets('nb:cid:UUID:b3023475-09b4-4647-9d6d-6fc242822e68')/$links/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 113
    Expect: 100-continue

    { "uri": "https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A32e6efaf-5fba-4538-b115-9d1cefe43510')"}

**Réponse HTTP**

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a>Étapes suivantes

Vous pouvez désormais encoder vos éléments multimédias téléchargés. Pour plus d'informations, consultez [Encode an asset using Media Encoder Standard with the Azure portal (Encoder un élément multimédia à l’aide de Media Encoder Standard avec le portail Azure)](media-services-portal-encode.md).

Vous pouvez également utiliser les fonctions Azure tootrigger un travail d’encodage basé sur un fichier qui arrivent dans le conteneur de hello configuré. Pour plus d’informations, consultez [cet exemple](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How tooGet a Media Processor]: media-services-get-media-processor.md

