---
title: "les clés de contenu aaaCreate avec REST | Documents Microsoft"
description: "Découvrez comment accéder à tooAssets toocreate clés de contenu qui fournissent sécurisé."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 95e9322b-168e-4a9d-8d5d-d7c946103745
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: cb3b74bdb72c43ab5b375c0376b6704f4a93bb8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-content-keys-with-rest"></a><span data-ttu-id="ef2d9-103">Création de clés de contenu avec REST</span><span class="sxs-lookup"><span data-stu-id="ef2d9-103">Create content keys with REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ef2d9-104">REST</span><span class="sxs-lookup"><span data-stu-id="ef2d9-104">REST</span></span>](media-services-rest-create-contentkey.md)
> * [<span data-ttu-id="ef2d9-105">.NET</span><span class="sxs-lookup"><span data-stu-id="ef2d9-105">.NET</span></span>](media-services-dotnet-create-contentkey.md)
> 
> 

<span data-ttu-id="ef2d9-106">Media Services vous permet de toocreate nouvelle et remettre les éléments multimédias chiffrés.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-106">Media Services enables you toocreate new and deliver encrypted assets.</span></span> <span data-ttu-id="ef2d9-107">A **ContentKey** fournit un accès sécurisé tooyour **Asset**s.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-107">A **ContentKey** provides secure access tooyour **Asset**s.</span></span> 

<span data-ttu-id="ef2d9-108">Lorsque vous créez un nouvel élément multimédia (par exemple, avant de vous [télécharger des fichiers](media-services-rest-upload-files.md)), vous pouvez spécifier hello options de chiffrement suivantes : **StorageEncrypted**, **CommonEncryptionProtected**, ou **EnvelopeEncryptionProtected**.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-108">When you create a new asset (for example, before you [upload files](media-services-rest-upload-files.md)), you can specify hello following encryption options: **StorageEncrypted**, **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span></span> 

<span data-ttu-id="ef2d9-109">Lorsque vous fournissez des ressources tooyour clients, vous pouvez [configurer pour toobe actifs dynamiquement chiffré](media-services-rest-configure-asset-delivery-policy.md) avec l’un des hello suivant deux chiffrements : **DynamicEnvelopeEncryption** ou  **DynamicCommonEncryption**.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-109">When you deliver assets tooyour clients, you can [configure for assets toobe dynamically encrypted](media-services-rest-configure-asset-delivery-policy.md) with one of hello following two encryptions: **DynamicEnvelopeEncryption** or **DynamicCommonEncryption**.</span></span>

<span data-ttu-id="ef2d9-110">Les éléments multimédias chiffrés ont toobe associé **ContentKey**s.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-110">Encrypted assets have toobe associated with **ContentKey**s.</span></span> <span data-ttu-id="ef2d9-111">Cet article décrit comment toocreate une clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-111">This article describes how toocreate a content key.</span></span>

<span data-ttu-id="ef2d9-112">Hello Voici les étapes générales pour la génération de clés de contenu que vous associerez avec les composants qui vous voulez toobe chiffré.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-112">hello following are general steps for generating content keys that you will associate with assets that you want toobe encrypted.</span></span> 

1. <span data-ttu-id="ef2d9-113">Générez de façon aléatoire une clé AES de 16 octets (pour le chiffrement commun et d’enveloppe) ou AES de 32 octets (chiffrement de stockage).</span><span class="sxs-lookup"><span data-stu-id="ef2d9-113">Randomly generate a 16-byte AES key (for common and envelope encryption) or a 32-byte AES key (for storage encryption).</span></span> 
   
    <span data-ttu-id="ef2d9-114">Ce sera la clé de contenu hello pour votre élément multimédia, ce qui signifie que tous les fichiers associés à cet élément multimédia sera peut-être toouse hello même clé de contenu pendant le déchiffrement.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-114">This will be hello content key for your asset, which means all files associated with that asset will need toouse hello same content key during decryption.</span></span> 
2. <span data-ttu-id="ef2d9-115">Appelez hello [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) et [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) tooget de méthodes hello certificat X.509 correct doit être utilisé tooencrypt votre clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-115">Call hello [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) and [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methods tooget hello correct X.509 Certificate that must be used tooencrypt your content key.</span></span>
3. <span data-ttu-id="ef2d9-116">Chiffrer votre clé de contenu avec une clé publique du certificat X.509 de hello hello.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-116">Encrypt your content key with hello public key of hello X.509 Certificate.</span></span> 
   
   <span data-ttu-id="ef2d9-117">Media Services .NET SDK utilise RSA avec OAEP lorsque vous effectuez un chiffrement de hello.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-117">Media Services .NET SDK uses RSA with OAEP when doing hello encryption.</span></span>  <span data-ttu-id="ef2d9-118">Vous pouvez voir un exemple Bonjour [EncryptSymmetricKeyData fonction](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="ef2d9-118">You can see an example in hello [EncryptSymmetricKeyData function](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
4. <span data-ttu-id="ef2d9-119">Créez une valeur de somme de contrôle (basée sur hello algorithme de somme de contrôle de clé AES PlayReady) calculée à l’aide d’identificateur de clé hello et clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-119">Create a checksum value (based on hello PlayReady AES key checksum algorithm) calculated using hello key identifier and content key.</span></span> <span data-ttu-id="ef2d9-120">Pour plus d’informations, consultez hello section « Algorithme de somme de contrôle clé PlayReady AES » du document d’objet d’en-tête PlayReady hello trouve [ici](http://www.microsoft.com/playready/documents/).</span><span class="sxs-lookup"><span data-stu-id="ef2d9-120">For more information, see hello “PlayReady AES Key Checksum Algorithm” section of hello PlayReady Header Object document located [here](http://www.microsoft.com/playready/documents/).</span></span>
   
   <span data-ttu-id="ef2d9-121">Hello Voici un exemple .NET qui calcule la somme de contrôle hello à l’aide de la partie GUID de hello d’identificateur de clé hello et hello effacer la clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-121">hello following is a .NET example that calculates hello checksum using hello GUID part of hello key identifier and hello clear content key.</span></span>

         public static string CalculateChecksum(byte[] contentKey, Guid keyId)
         {

            byte[] array = null;
            using (AesCryptoServiceProvider aesCryptoServiceProvider = new AesCryptoServiceProvider())
            {
                aesCryptoServiceProvider.Mode = CipherMode.ECB;
                aesCryptoServiceProvider.Key = contentKey;
                aesCryptoServiceProvider.Padding = PaddingMode.None;
                ICryptoTransform cryptoTransform = aesCryptoServiceProvider.CreateEncryptor();
                array = new byte[16];
                cryptoTransform.TransformBlock(keyId.ToByteArray(), 0, 16, array, 0);
            }
            byte[] array2 = new byte[8];
            Array.Copy(array, array2, 8);
            return Convert.ToBase64String(array2);
         }
5. <span data-ttu-id="ef2d9-122">Créer la clé de contenu hello avec hello **EncryptedContentKey** (converties en chaîne encodée toobase64), **ProtectionKeyId**, **ProtectionKeyType**,  **ContentKeyType**, et **Checksum** valeurs que vous avez reçu dans les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-122">Create hello Content key with hello **EncryptedContentKey** (converted toobase64-encoded string), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType**, and **Checksum** values you have received in previous steps.</span></span>
6. <span data-ttu-id="ef2d9-123">Associer hello **ContentKey** entité avec votre **Asset** entité via une opération de hello $links.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-123">Associate hello **ContentKey** entity with your **Asset** entity through hello $links operation.</span></span>

<span data-ttu-id="ef2d9-124">Notez que cette rubrique ne s’affiche pas comment toogenerate une clé AES, chiffrer la clé de hello et calculer la somme de contrôle hello.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-124">Note that this topic does not show how toogenerate an AES key, encrypt hello key, and calculate hello checksum.</span></span> 

>[!NOTE]

><span data-ttu-id="ef2d9-125">Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-125">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="ef2d9-126">Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="ef2d9-126">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="ef2d9-127">Connecter les Services de tooMedia</span><span class="sxs-lookup"><span data-stu-id="ef2d9-127">Connect tooMedia Services</span></span>

<span data-ttu-id="ef2d9-128">Pour plus d’informations sur la façon dont tooconnect toohello AMS API, consultez [hello accès API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="ef2d9-128">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="ef2d9-129">Après vous être connecté toohttps://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI de Media Services.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-129">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="ef2d9-130">Vous devez effectuer les appels suivants toohello nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-130">You must make subsequent calls toohello new URI.</span></span>

## <a name="retrieve-hello-protectionkeyid"></a><span data-ttu-id="ef2d9-131">Récupérer hello ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="ef2d9-131">Retrieve hello ProtectionKeyId</span></span>
<span data-ttu-id="ef2d9-132">Bonjour à l’exemple suivant montre comment tooretrieve hello ProtectionKeyId, une empreinte de certificat pour le certificat hello vous devez utiliser lors du chiffrement de votre clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-132">hello following example shows how tooretrieve hello ProtectionKeyId, a certificate thumbprint, for hello certificate you must use when encrypting your content key.</span></span> <span data-ttu-id="ef2d9-133">Effectuez cette étape toomake que vous avez déjà les certificats appropriés hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-133">Do this step toomake sure that you already have hello appropriate certificate on your machine.</span></span>

<span data-ttu-id="ef2d9-134">Demande :</span><span class="sxs-lookup"><span data-stu-id="ef2d9-134">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net


<span data-ttu-id="ef2d9-135">Réponse :</span><span class="sxs-lookup"><span data-stu-id="ef2d9-135">Response:</span></span>

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

## <a name="retrieve-hello-protectionkey-for-hello-protectionkeyid"></a><span data-ttu-id="ef2d9-136">Récupérer ProtectionKey de hello pour hello ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="ef2d9-136">Retrieve hello ProtectionKey for hello ProtectionKeyId</span></span>
<span data-ttu-id="ef2d9-137">Hello suivant montre comment le certificat X.509 de tooretrieve hello à l’aide de hello ProtectionKeyId vous avez reçu dans l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-137">hello following example shows how tooretrieve hello X.509 certificate using hello ProtectionKeyId you received in hello previous step.</span></span>

<span data-ttu-id="ef2d9-138">Demande :</span><span class="sxs-lookup"><span data-stu-id="ef2d9-138">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net



<span data-ttu-id="ef2d9-139">Réponse :</span><span class="sxs-lookup"><span data-stu-id="ef2d9-139">Response:</span></span>

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

## <a name="create-hello-contentkey"></a><span data-ttu-id="ef2d9-140">Créer hello ContentKey</span><span class="sxs-lookup"><span data-stu-id="ef2d9-140">Create hello ContentKey</span></span>
<span data-ttu-id="ef2d9-141">Après avoir récupéré le certificat X.509 de hello et utilisé son tooencrypt de clé publique de votre clé de contenu, créez un **ContentKey** entité et définissez sa propriété de valeurs en conséquence.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-141">After you have retrieved hello X.509 certificate and used its public key tooencrypt your content key, create a **ContentKey** entity and set its property values accordingly.</span></span>

<span data-ttu-id="ef2d9-142">Une des valeurs hello que vous devez définir quand créer hello contenu clé est de type de hello.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-142">One of hello values that you must set when create hello content key is hello type.</span></span> <span data-ttu-id="ef2d9-143">Choisissez une des valeurs suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-143">Choose from one of hello following values.</span></span>

    public enum ContentKeyType
    {
        /// <summary>
        /// Specifies a content key for common encryption.
        /// </summary>
        /// <remarks>This is hello default value.</remarks>
        CommonEncryption = 0,

        /// <summary>
        /// Specifies a content key for storage encryption.
        /// </summary>
        StorageEncryption = 1,

        /// <summary>
        /// Specifies a content key for configuration encryption.
        /// </summary>
        ConfigurationEncryption = 2,

        /// <summary>
        /// Specifies a content key for Envelope encryption.  Only used internally.
        /// </summary>
        EnvelopeEncryption = 4
    }


<span data-ttu-id="ef2d9-144">Hello suivant montre l’exemple de comment toocreate un **ContentKey** avec un **ContentKeyType** définie pour le chiffrement de stockage (« 1 ») et hello **ProtectionKeyType** défini trop « 0 » tooindicate qui hello Id de clé de protection est l’empreinte de certificat X.509 hello.</span><span class="sxs-lookup"><span data-stu-id="ef2d9-144">hello following example shows how toocreate a **ContentKey** with a **ContentKeyType** set for storage encryption ("1") and hello **ProtectionKeyType** set too"0" tooindicate that hello protection key Id is hello X.509 certificate thumbprint.</span></span>  

<span data-ttu-id="ef2d9-145">Demande</span><span class="sxs-lookup"><span data-stu-id="ef2d9-145">Request</span></span>

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


<span data-ttu-id="ef2d9-146">Réponse :</span><span class="sxs-lookup"><span data-stu-id="ef2d9-146">Response:</span></span>

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

## <a name="associate-hello-contentkey-with-an-asset"></a><span data-ttu-id="ef2d9-147">Associer des hello ContentKey à un élément multimédia</span><span class="sxs-lookup"><span data-stu-id="ef2d9-147">Associate hello ContentKey with an Asset</span></span>
<span data-ttu-id="ef2d9-148">Après avoir créé le hello ContentKey, associez-le à votre élément multimédia à l’aide de l’opération de hello $links, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="ef2d9-148">After creating hello ContentKey, associate it with your Asset using hello $links operation, as shown in hello following example:</span></span>

<span data-ttu-id="ef2d9-149">Demande :</span><span class="sxs-lookup"><span data-stu-id="ef2d9-149">Request:</span></span>

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

<span data-ttu-id="ef2d9-150">Réponse :</span><span class="sxs-lookup"><span data-stu-id="ef2d9-150">Response:</span></span>

    HTTP/1.1 204 No Content 


## <a name="media-services-learning-paths"></a><span data-ttu-id="ef2d9-151">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="ef2d9-151">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ef2d9-152">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="ef2d9-152">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

