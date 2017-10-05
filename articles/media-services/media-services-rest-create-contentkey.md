---
title: "Création de clés de contenu avec REST | Microsoft Docs"
description: "Apprenez à créer des clés de contenu qui fournissent un accès sécurisé aux ressources."
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
ms.openlocfilehash: ece09277d26fafb7c0eebf62730031c4dc01bfe0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-content-keys-with-rest"></a><span data-ttu-id="bdbcd-103">Création de clés de contenu avec REST</span><span class="sxs-lookup"><span data-stu-id="bdbcd-103">Create content keys with REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bdbcd-104">REST</span><span class="sxs-lookup"><span data-stu-id="bdbcd-104">REST</span></span>](media-services-rest-create-contentkey.md)
> * [<span data-ttu-id="bdbcd-105">.NET</span><span class="sxs-lookup"><span data-stu-id="bdbcd-105">.NET</span></span>](media-services-dotnet-create-contentkey.md)
> 
> 

<span data-ttu-id="bdbcd-106">Media Services vous permet de créer et de fournir des ressources chiffrées.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-106">Media Services enables you to create new and deliver encrypted assets.</span></span> <span data-ttu-id="bdbcd-107">**ContentKey** fournit un accès sécurisé à vos **éléments multimédias**.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-107">A **ContentKey** provides secure access to your **Asset**s.</span></span> 

<span data-ttu-id="bdbcd-108">Quand vous créez un élément multimédia (par exemple, avant de [charger des fichiers](media-services-rest-upload-files.md)), vous pouvez spécifier les options de chiffrement suivantes : **StorageEncrypted**, **CommonEncryptionProtected** ou **EnvelopeEncryptionProtected**.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-108">When you create a new asset (for example, before you [upload files](media-services-rest-upload-files.md)), you can specify the following encryption options: **StorageEncrypted**, **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span></span> 

<span data-ttu-id="bdbcd-109">Quand vous fournissez des éléments multimédias à vos clients, vous pouvez [configurer les éléments multimédias devant être chiffrés dynamiquement](media-services-rest-configure-asset-delivery-policy.md) avec un des deux chiffrements suivants : **DynamicEnvelopeEncryption** ou **DynamicCommonEncryption**.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-109">When you deliver assets to your clients, you can [configure for assets to be dynamically encrypted](media-services-rest-configure-asset-delivery-policy.md) with one of the following two encryptions: **DynamicEnvelopeEncryption** or **DynamicCommonEncryption**.</span></span>

<span data-ttu-id="bdbcd-110">Les ressources chiffrées doivent être associées à des **ContentKey**.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-110">Encrypted assets have to be associated with **ContentKey**s.</span></span> <span data-ttu-id="bdbcd-111">Cet article décrit comment créer une clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-111">This article describes how to create a content key.</span></span>

<span data-ttu-id="bdbcd-112">Voici les étapes générales pour la génération de clés de contenu que vous allez associer à des ressources devant être chiffrées.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-112">The following are general steps for generating content keys that you will associate with assets that you want to be encrypted.</span></span> 

1. <span data-ttu-id="bdbcd-113">Générez de façon aléatoire une clé AES de 16 octets (pour le chiffrement commun et d’enveloppe) ou AES de 32 octets (chiffrement de stockage).</span><span class="sxs-lookup"><span data-stu-id="bdbcd-113">Randomly generate a 16-byte AES key (for common and envelope encryption) or a 32-byte AES key (for storage encryption).</span></span> 
   
    <span data-ttu-id="bdbcd-114">Il s’agit de la clé de contenu de votre ressource, ce qui signifie que tous les fichiers associés à cette ressource doivent utiliser la même clé de contenu lors du déchiffrement.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-114">This will be the content key for your asset, which means all files associated with that asset will need to use the same content key during decryption.</span></span> 
2. <span data-ttu-id="bdbcd-115">Appelez les méthodes [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) et [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) pour obtenir le certificat X.509 approprié qui doit être utilisé pour chiffrer votre clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-115">Call the [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) and [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methods to get the correct X.509 Certificate that must be used to encrypt your content key.</span></span>
3. <span data-ttu-id="bdbcd-116">Chiffrez votre clé de contenu avec la clé publique du certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-116">Encrypt your content key with the public key of the X.509 Certificate.</span></span> 
   
   <span data-ttu-id="bdbcd-117">Le Kit de développement logiciel (SDK) Media Services pour .NET utilise RSA avec OAEP lorsque vous effectuez le chiffrement.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-117">Media Services .NET SDK uses RSA with OAEP when doing the encryption.</span></span>  <span data-ttu-id="bdbcd-118">Vous trouverez un exemple dans la [fonction EncryptSymmetricKeyData](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="bdbcd-118">You can see an example in the [EncryptSymmetricKeyData function](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
4. <span data-ttu-id="bdbcd-119">Créez une valeur de somme de contrôle (basée sur l’algorithme de somme de contrôle de clé AES PlayReady), calculée à l’aide de l’identificateur de clé et de la clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-119">Create a checksum value (based on the PlayReady AES key checksum algorithm) calculated using the key identifier and content key.</span></span> <span data-ttu-id="bdbcd-120">Pour plus d’informations, consultez la section relative à l’algorithme de somme de contrôle de clé AES PlayReady du document décrivant l’objet d’en-tête PlayReady situé [ici](http://www.microsoft.com/playready/documents/).</span><span class="sxs-lookup"><span data-stu-id="bdbcd-120">For more information, see the “PlayReady AES Key Checksum Algorithm” section of the PlayReady Header Object document located [here](http://www.microsoft.com/playready/documents/).</span></span>
   
   <span data-ttu-id="bdbcd-121">L’exemple .NET suivant calcule la somme de contrôle à l’aide de la partie GUID de l’identificateur de clé et de la clé de contenu en clair.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-121">The following is a .NET example that calculates the checksum using the GUID part of the key identifier and the clear content key.</span></span>

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
5. <span data-ttu-id="bdbcd-122">Créez la clé de contenu avec les valeurs **EncryptedContentKey** (convertie en chaîne codée en Base64), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType** et **Checksum** que vous avez obtenues lors des étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-122">Create the Content key with the **EncryptedContentKey** (converted to base64-encoded string), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType**, and **Checksum** values you have received in previous steps.</span></span>
6. <span data-ttu-id="bdbcd-123">Associez l’entité **ContentKey** avec votre entité **Asset** par le biais de l’opération $links.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-123">Associate the **ContentKey** entity with your **Asset** entity through the $links operation.</span></span>

<span data-ttu-id="bdbcd-124">Notez que cette rubrique n’explique pas comment générer une clé AES, chiffrer la clé puis calculer la somme de contrôle.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-124">Note that this topic does not show how to generate an AES key, encrypt the key, and calculate the checksum.</span></span> 

>[!NOTE]

><span data-ttu-id="bdbcd-125">Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-125">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="bdbcd-126">Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="bdbcd-126">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="bdbcd-127">Connexion à Media Services</span><span class="sxs-lookup"><span data-stu-id="bdbcd-127">Connect to Media Services</span></span>

<span data-ttu-id="bdbcd-128">Pour savoir comment vous connecter à l’API AMS, consultez [Accéder à l’API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="bdbcd-128">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="bdbcd-129">Après vous être connecté à https://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI Media Services.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-129">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="bdbcd-130">Vous devez faire d’autres appels au nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-130">You must make subsequent calls to the new URI.</span></span>

## <a name="retrieve-the-protectionkeyid"></a><span data-ttu-id="bdbcd-131">Récupération de ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="bdbcd-131">Retrieve the ProtectionKeyId</span></span>
<span data-ttu-id="bdbcd-132">L’exemple suivant montre comment récupérer ProtectionKeyId, une empreinte de certificat, pour le certificat que vous devez utiliser pour chiffrer votre clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-132">The following example shows how to retrieve the ProtectionKeyId, a certificate thumbprint, for the certificate you must use when encrypting your content key.</span></span> <span data-ttu-id="bdbcd-133">Effectuez cette étape pour vous assurer que vous possédez déjà le certificat approprié sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-133">Do this step to make sure that you already have the appropriate certificate on your machine.</span></span>

<span data-ttu-id="bdbcd-134">Demande :</span><span class="sxs-lookup"><span data-stu-id="bdbcd-134">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net


<span data-ttu-id="bdbcd-135">Réponse :</span><span class="sxs-lookup"><span data-stu-id="bdbcd-135">Response:</span></span>

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

## <a name="retrieve-the-protectionkey-for-the-protectionkeyid"></a><span data-ttu-id="bdbcd-136">Récupération de ProtectionKey pour ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="bdbcd-136">Retrieve the ProtectionKey for the ProtectionKeyId</span></span>
<span data-ttu-id="bdbcd-137">L’exemple suivant montre comment récupérer le certificat X.509 à l’aide de ProtectionKeyId, que vous avez reçue lors de l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-137">The following example shows how to retrieve the X.509 certificate using the ProtectionKeyId you received in the previous step.</span></span>

<span data-ttu-id="bdbcd-138">Demande :</span><span class="sxs-lookup"><span data-stu-id="bdbcd-138">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net



<span data-ttu-id="bdbcd-139">Réponse :</span><span class="sxs-lookup"><span data-stu-id="bdbcd-139">Response:</span></span>

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

## <a name="create-the-contentkey"></a><span data-ttu-id="bdbcd-140">Création de ContentKey</span><span class="sxs-lookup"><span data-stu-id="bdbcd-140">Create the ContentKey</span></span>
<span data-ttu-id="bdbcd-141">Après avoir récupéré le certificat X.509 et utilisé sa clé publique pour chiffrer votre clé de contenu, créez une entité **ContentKey** et définissez ses valeurs de propriété en conséquence.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-141">After you have retrieved the X.509 certificate and used its public key to encrypt your content key, create a **ContentKey** entity and set its property values accordingly.</span></span>

<span data-ttu-id="bdbcd-142">Une des valeurs que vous devez définir lors de la création d’une clé de contenu est son type.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-142">One of the values that you must set when create the content key is the type.</span></span> <span data-ttu-id="bdbcd-143">Choisissez une des valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-143">Choose from one of the following values.</span></span>

    public enum ContentKeyType
    {
        /// <summary>
        /// Specifies a content key for common encryption.
        /// </summary>
        /// <remarks>This is the default value.</remarks>
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


<span data-ttu-id="bdbcd-144">L’exemple suivant montre comment créer une **ContentKey** avec un **ContentKeyType** défini pour le chiffrement du stockage (« 1 ») et le **ProtectionKeyType** avec la valeur « 0 » pour indiquer que l’ID de la clé de protection est l’empreinte numérique du certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="bdbcd-144">The following example shows how to create a **ContentKey** with a **ContentKeyType** set for storage encryption ("1") and the **ProtectionKeyType** set to "0" to indicate that the protection key Id is the X.509 certificate thumbprint.</span></span>  

<span data-ttu-id="bdbcd-145">Demande</span><span class="sxs-lookup"><span data-stu-id="bdbcd-145">Request</span></span>

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


<span data-ttu-id="bdbcd-146">Réponse :</span><span class="sxs-lookup"><span data-stu-id="bdbcd-146">Response:</span></span>

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

## <a name="associate-the-contentkey-with-an-asset"></a><span data-ttu-id="bdbcd-147">Association de la ContentKey avec une ressource</span><span class="sxs-lookup"><span data-stu-id="bdbcd-147">Associate the ContentKey with an Asset</span></span>
<span data-ttu-id="bdbcd-148">Après avoir créé la ContentKey, associez-la à votre ressource à l’aide de l’opération $links, comme illustré dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="bdbcd-148">After creating the ContentKey, associate it with your Asset using the $links operation, as shown in the following example:</span></span>

<span data-ttu-id="bdbcd-149">Demande :</span><span class="sxs-lookup"><span data-stu-id="bdbcd-149">Request:</span></span>

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

<span data-ttu-id="bdbcd-150">Réponse :</span><span class="sxs-lookup"><span data-stu-id="bdbcd-150">Response:</span></span>

    HTTP/1.1 204 No Content 


## <a name="media-services-learning-paths"></a><span data-ttu-id="bdbcd-151">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="bdbcd-151">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="bdbcd-152">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="bdbcd-152">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

