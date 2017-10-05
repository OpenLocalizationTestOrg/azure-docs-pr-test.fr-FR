---
title: "Chiffrer votre contenu avec le chiffrement de stockage à l'aide de l'API REST AMS"
description: "Découvrez comment chiffrer votre contenu avec le chiffrement de stockage à l'aide des API REST AMS."
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
ms.openlocfilehash: 1979f5bf5e8cab88dab5fba49018afacf24504b3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="encrypting-your-content-with-storage-encryption"></a><span data-ttu-id="47ca2-103">Chiffrer votre contenu avec le chiffrement de stockage</span><span class="sxs-lookup"><span data-stu-id="47ca2-103">Encrypting your content with storage encryption</span></span>

<span data-ttu-id="47ca2-104">Il est fortement recommandé de chiffrer votre contenu localement à l’aide du chiffrement AES 256 bits, puis de le charger vers Azure Storage où il sera stocké au repos sous forme chiffrée.</span><span class="sxs-lookup"><span data-stu-id="47ca2-104">It is highly recommended to encrypt your content locally using AES-256 bit encryption and then upload it to Azure Storage where it will be stored encrypted at rest.</span></span>

<span data-ttu-id="47ca2-105">Cet article donne une vue d'ensemble du chiffrement de stockage AMS et vous montre comment télécharger le contenu chiffré du stockage :</span><span class="sxs-lookup"><span data-stu-id="47ca2-105">This article gives an overview of AMS storage encryption and shows you how to upload the storage encrypted content:</span></span>

* <span data-ttu-id="47ca2-106">Créez une clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="47ca2-106">Create a content key.</span></span>
* <span data-ttu-id="47ca2-107">Créez une ressource.</span><span class="sxs-lookup"><span data-stu-id="47ca2-107">Create an Asset.</span></span> <span data-ttu-id="47ca2-108">Définissez AssetCreationOption sur StorageEncryption lors de la création de la ressource.</span><span class="sxs-lookup"><span data-stu-id="47ca2-108">Set the AssetCreationOption to StorageEncryption when creating the Asset.</span></span>
  
     <span data-ttu-id="47ca2-109">Les ressources chiffrées doivent être associées à des clés de contenu.</span><span class="sxs-lookup"><span data-stu-id="47ca2-109">Encrypted assets have to be associated with content keys.</span></span>
* <span data-ttu-id="47ca2-110">Liez la clé de contenu à la ressource.</span><span class="sxs-lookup"><span data-stu-id="47ca2-110">Link the content key to the asset.</span></span>  
* <span data-ttu-id="47ca2-111">Définissez les paramètres liés au chiffrement sur les entités AssetFile.</span><span class="sxs-lookup"><span data-stu-id="47ca2-111">Set the encryption related parameters on the AssetFile entities.</span></span>

## <a name="considerations"></a><span data-ttu-id="47ca2-112">Considérations</span><span class="sxs-lookup"><span data-stu-id="47ca2-112">Considerations</span></span> 

<span data-ttu-id="47ca2-113">Si vous souhaitez remettre une ressource à chiffrement de stockage, vous devez configurer la stratégie de remise de la ressource.</span><span class="sxs-lookup"><span data-stu-id="47ca2-113">If you want to deliver a storage encrypted asset, you must configure the asset’s delivery policy.</span></span> <span data-ttu-id="47ca2-114">Avant de pouvoir diffuser votre ressource en continu, le serveur de diffusion supprime le chiffrement de stockage et transmet en continu votre contenu à l’aide de la stratégie de remise spécifiée.</span><span class="sxs-lookup"><span data-stu-id="47ca2-114">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy.</span></span> <span data-ttu-id="47ca2-115">Pour plus d'informations, consultez [Configuration des stratégies de distribution de ressources](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="47ca2-115">For more information, see [Configuring Asset Delivery Policies](media-services-rest-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="47ca2-116">Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="47ca2-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="47ca2-117">Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="47ca2-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span> 

## <a name="connect-to-media-services"></a><span data-ttu-id="47ca2-118">Connexion à Media Services</span><span class="sxs-lookup"><span data-stu-id="47ca2-118">Connect to Media Services</span></span>

<span data-ttu-id="47ca2-119">Pour savoir comment vous connecter à l’API AMS, consultez [Accéder à l’API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="47ca2-119">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="47ca2-120">Après vous être connecté à https://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI Media Services.</span><span class="sxs-lookup"><span data-stu-id="47ca2-120">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="47ca2-121">Vous devez faire d’autres appels au nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="47ca2-121">You must make subsequent calls to the new URI.</span></span>

## <a name="storage-encryption-overview"></a><span data-ttu-id="47ca2-122">Vue d’ensemble du chiffrement du stockage</span><span class="sxs-lookup"><span data-stu-id="47ca2-122">Storage encryption overview</span></span>
<span data-ttu-id="47ca2-123">Le chiffrement de stockage AMS applique le mode de chiffrement **AES-CTR** à la totalité du fichier.</span><span class="sxs-lookup"><span data-stu-id="47ca2-123">The AMS storage encryption applies **AES-CTR** mode encryption to the entire file.</span></span>  <span data-ttu-id="47ca2-124">Le mode AES-CTR est un chiffrement par blocs qui permet de chiffrer des données de longueur arbitraire sans avoir besoin de remplissage.</span><span class="sxs-lookup"><span data-stu-id="47ca2-124">AES-CTR mode is a block cipher that can encrypt arbitrary length data without need for padding.</span></span> <span data-ttu-id="47ca2-125">Il fonctionne en chiffrant un bloc de compteur avec l'algorithme AES, puis en appliquant l’opération XOR à la sortie d’AES avec les données à chiffrer ou déchiffrer.</span><span class="sxs-lookup"><span data-stu-id="47ca2-125">It operates by encrypting a counter block with the AES algorithm and then XOR-ing the output of AES with the data to encrypt or decrypt.</span></span>  <span data-ttu-id="47ca2-126">Le bloc de compteur utilisé est construit en copiant la valeur InitializationVector sur les octets 0 à 7 de la valeur du compteur et les octets 8 à 15 de la valeur du compteur ont la valeur zéro.</span><span class="sxs-lookup"><span data-stu-id="47ca2-126">The counter block used is constructed by copying the value of the InitializationVector to bytes 0 to 7 of the counter value and bytes 8 to 15 of the counter value are set to zero.</span></span> <span data-ttu-id="47ca2-127">Dans le bloc de compteur de 16 octets, les octets 8 à 15 (c'est-à-dire les octets les moins significatifs) sont utilisés comme simple entier non signé de 64 bits, incrémenté de un pour chacun des blocs suivants de données traitées et conservé dans l'ordre des octets du réseau.</span><span class="sxs-lookup"><span data-stu-id="47ca2-127">Of the 16 byte counter block, bytes 8 to 15 (i.e. the least significant bytes) are used as a simple 64 bit unsigned integer that is incremented by one for each subsequent block of data processed and is kept in network byte order.</span></span> <span data-ttu-id="47ca2-128">Notez que, si cet entier atteint la valeur maximale (0xFFFFFFFFFFFFFFFF), son incrémentation réinitialise le compteur de blocs à zéro (octets 8 à 15) sans affecter les autres 64 bits du compteur (c'est-à-dire les octets 0 à 7).</span><span class="sxs-lookup"><span data-stu-id="47ca2-128">Note that if this integer reaches the maximum value (0xFFFFFFFFFFFFFFFF) then incrementing it resets the block counter to zero (bytes 8 to 15) without affecting the other 64 bits of the counter (i.e. bytes 0 to 7).</span></span>   <span data-ttu-id="47ca2-129">Pour maintenir la sécurité du mode de chiffrement AES-CTR, la valeur InitializationVector pour un identificateur de clé donné pour chaque clé de contenu doit être unique pour chaque fichier et les fichiers doivent avoir une longueur inférieure à 2^64 blocs.</span><span class="sxs-lookup"><span data-stu-id="47ca2-129">In order to maintain the security of the AES-CTR mode encryption, the InitializationVector value for a given Key Identifier for each content key shall be unique for each file and files shall be less than 2^64 blocks in length.</span></span>  <span data-ttu-id="47ca2-130">Cela permet de faire en sorte qu'aucune valeur de compteur ne soit jamais réutilisée avec une clé donnée.</span><span class="sxs-lookup"><span data-stu-id="47ca2-130">This is to ensure that a counter value is never reused with a given key.</span></span> <span data-ttu-id="47ca2-131">Pour plus d'informations sur le mode CTR, consultez [cette page wiki](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (l'article wiki utilise le terme « Nonce » au lieu de « InitializationVector »).</span><span class="sxs-lookup"><span data-stu-id="47ca2-131">For more information about the CTR mode, see [this wiki page](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (the wiki article uses the term "Nonce" instead of "InitializationVector").</span></span>

<span data-ttu-id="47ca2-132">Utilisez le **chiffrement du stockage** pour chiffrer votre contenu localement à l’aide du chiffrement AES 256 bits, puis chargez-le vers Azure Storage où il est stocké au repos sous forme chiffrée.</span><span class="sxs-lookup"><span data-stu-id="47ca2-132">Use **Storage Encryption** to encrypt your clear content locally using AES-256 bit encryption and then upload it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="47ca2-133">Les éléments multimédias protégés par le chiffrement de stockage sont automatiquement déchiffrés et placés dans un système de fichiers chiffré avant d’être encodés, puis éventuellement rechiffrés avant d’être rechargés sous la forme d’un nouvel élément multimédia de sortie.</span><span class="sxs-lookup"><span data-stu-id="47ca2-133">Assets protected with storage encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="47ca2-134">Le principal cas d’utilisation du chiffrement de stockage concerne la sécurisation des fichiers multimédias d’entrée de haute qualité avec un chiffrement renforcé au repos sur le disque.</span><span class="sxs-lookup"><span data-stu-id="47ca2-134">The primary use case for storage encryption is when you want to secure your high quality input media files with strong encryption at rest on disk.</span></span>

<span data-ttu-id="47ca2-135">Pour fournir un élément multimédia avec chiffrement de stockage, vous devez configurer la stratégie de remise de l'élément multimédia afin que Media Services sache comment vous souhaitez remettre votre contenu.</span><span class="sxs-lookup"><span data-stu-id="47ca2-135">In order to deliver a storage encrypted asset, you must configure the asset’s delivery policy so Media Services knows how you want to deliver your content.</span></span> <span data-ttu-id="47ca2-136">Pour que votre élément multimédia puisse être diffusé en continu, le serveur de diffusion supprime le chiffrement de stockage et diffuse votre contenu à l'aide de la stratégie de remise spécifiée (par exemple AES, chiffrement commun ou aucun chiffrement).</span><span class="sxs-lookup"><span data-stu-id="47ca2-136">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy (for example, AES, common encryption, or no encryption).</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="47ca2-137">Créer des ContentKeys utilisées pour le chiffrement</span><span class="sxs-lookup"><span data-stu-id="47ca2-137">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="47ca2-138">Les ressources chiffrées doivent être associées à une clé de chiffrement du stockage.</span><span class="sxs-lookup"><span data-stu-id="47ca2-138">Encrypted assets have to be associated with Storage Encryption key.</span></span> <span data-ttu-id="47ca2-139">Vous devez créer la clé de contenu à utiliser pour le chiffrement avant de créer les fichiers de ressources.</span><span class="sxs-lookup"><span data-stu-id="47ca2-139">You must create the content key to be used for encryption before creating the asset files.</span></span> <span data-ttu-id="47ca2-140">Cet article décrit la création d’une clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="47ca2-140">This section describes how to create a content key.</span></span>

<span data-ttu-id="47ca2-141">Voici les étapes générales pour la génération de clés de contenu que vous allez associer à des ressources devant être chiffrées.</span><span class="sxs-lookup"><span data-stu-id="47ca2-141">The following are general steps for generating content keys that you will associate with assets that you want to be encrypted.</span></span> 

1. <span data-ttu-id="47ca2-142">Pour le chiffrement du stockage, générez de façon aléatoire une clé AES de 32 octets.</span><span class="sxs-lookup"><span data-stu-id="47ca2-142">For storage encryption, randomly generate a 32-byte AES key.</span></span> 
   
    <span data-ttu-id="47ca2-143">Il s’agit de la clé de contenu de votre ressource, ce qui signifie que tous les fichiers associés à cette ressource doivent utiliser la même clé de contenu lors du déchiffrement.</span><span class="sxs-lookup"><span data-stu-id="47ca2-143">This will be the content key for your asset, which means all files associated with that asset will need to use the same content key during decryption.</span></span> 
2. <span data-ttu-id="47ca2-144">Appelez les méthodes [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) et [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) pour obtenir le certificat X.509 approprié qui doit être utilisé pour chiffrer votre clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="47ca2-144">Call the [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) and [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methods to get the correct X.509 Certificate that must be used to encrypt your content key.</span></span>
3. <span data-ttu-id="47ca2-145">Chiffrez votre clé de contenu avec la clé publique du certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="47ca2-145">Encrypt your content key with the public key of the X.509 Certificate.</span></span> 
   
   <span data-ttu-id="47ca2-146">Le Kit de développement logiciel (SDK) Media Services pour .NET utilise RSA avec OAEP lorsque vous effectuez le chiffrement.</span><span class="sxs-lookup"><span data-stu-id="47ca2-146">Media Services .NET SDK uses RSA with OAEP when doing the encryption.</span></span>  <span data-ttu-id="47ca2-147">Vous trouverez un exemple .NET dans la [fonction EncryptSymmetricKeyData](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="47ca2-147">You can see a .NET example in the [EncryptSymmetricKeyData function](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
4. <span data-ttu-id="47ca2-148">Créez une valeur de somme de contrôle calculée à l'aide de l'identificateur de clé et de la clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="47ca2-148">Create a checksum value calculated using the key identifier and content key.</span></span> <span data-ttu-id="47ca2-149">L’exemple .NET suivant calcule la somme de contrôle à l’aide de la partie GUID de l’identificateur de clé et de la clé de contenu en clair.</span><span class="sxs-lookup"><span data-stu-id="47ca2-149">The following .NET example calculates the checksum using the GUID part of the key identifier and the clear content key.</span></span>

        public static string CalculateChecksum(byte[] contentKey, Guid keyId)
        {
            const int ChecksumLength = 8;
            const int KeyIdLength = 16;

            byte[] encryptedKeyId = null;

            // Checksum is computed by AES-ECB encrypting the KID
            // with the content key.
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

1. <span data-ttu-id="47ca2-150">Créez la clé de contenu avec les valeurs **EncryptedContentKey** (convertie en chaîne codée en Base64), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType** et **Checksum** que vous avez obtenues lors des étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="47ca2-150">Create the Content key with the **EncryptedContentKey** (converted to base64-encoded string), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType**, and **Checksum** values you have received in previous steps.</span></span>

    <span data-ttu-id="47ca2-151">Pour le chiffrement du stockage, les propriétés suivantes doivent être incluses dans le corps de la demande.</span><span class="sxs-lookup"><span data-stu-id="47ca2-151">For storage encryption, the following properties should be included in the request body.</span></span>

    <span data-ttu-id="47ca2-152">Propriété du corps de la demande</span><span class="sxs-lookup"><span data-stu-id="47ca2-152">Request body property</span></span>    | <span data-ttu-id="47ca2-153">Description</span><span class="sxs-lookup"><span data-stu-id="47ca2-153">Description</span></span>
    ---|---
    <span data-ttu-id="47ca2-154">Id</span><span class="sxs-lookup"><span data-stu-id="47ca2-154">Id</span></span> | <span data-ttu-id="47ca2-155">ID de ContentKey que nous générons nous-mêmes en utilisant le format suivant : « nb:kid:UUID:<NEW GUID> ».</span><span class="sxs-lookup"><span data-stu-id="47ca2-155">The ContentKey Id which we generate ourselves using the following format, “nb:kid:UUID:<NEW GUID>”.</span></span>
    <span data-ttu-id="47ca2-156">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="47ca2-156">ContentKeyType</span></span> | <span data-ttu-id="47ca2-157">Il s’agit du type de clé de contenu en tant qu’entier pour cette clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="47ca2-157">This is the content key type as an integer for this content key.</span></span> <span data-ttu-id="47ca2-158">Nous transmettons la valeur 1 pour le chiffrement du stockage.</span><span class="sxs-lookup"><span data-stu-id="47ca2-158">We pass the value 1 for storage encryption.</span></span>
    <span data-ttu-id="47ca2-159">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="47ca2-159">EncryptedContentKey</span></span> | <span data-ttu-id="47ca2-160">Nous créons une valeur de clé de contenu qui est une valeur de 256 bits (32 octets).</span><span class="sxs-lookup"><span data-stu-id="47ca2-160">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="47ca2-161">La clé est chiffrée à l’aide du certificat X.509 de chiffrement du stockage que nous récupérons à partir de Microsoft Azure Media Services en exécutant une demande HTTP GET pour les méthodes GetProtectionKeyId et GetProtectionKey.</span><span class="sxs-lookup"><span data-stu-id="47ca2-161">The key is encrypted using the storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for the GetProtectionKeyId and GetProtectionKey Methods.</span></span> <span data-ttu-id="47ca2-162">À titre d’exemple, consultez le code .NET suivant : la méthode **EncryptSymmetricKeyData** définie [ici](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="47ca2-162">As an example, see the following .NET code: the  **EncryptSymmetricKeyData** method defined [here](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
    <span data-ttu-id="47ca2-163">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="47ca2-163">ProtectionKeyId</span></span> | <span data-ttu-id="47ca2-164">Il s’agit de l’ID de clé de protection pour le certificat X.509 de chiffrement de stockage qui a été utilisé pour chiffrer notre clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="47ca2-164">This is the protection key id for the storage encryption X.509 certificate that was used to encrypt our content key.</span></span>
    <span data-ttu-id="47ca2-165">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="47ca2-165">ProtectionKeyType</span></span> | <span data-ttu-id="47ca2-166">Il s’agit du type de chiffrement de la clé de protection qui a été utilisé pour chiffrer la clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="47ca2-166">This is the encryption type for the protection key that was used to encrypt the content key.</span></span> <span data-ttu-id="47ca2-167">Cette valeur est StorageEncryption(1) dans notre exemple.</span><span class="sxs-lookup"><span data-stu-id="47ca2-167">This value is StorageEncryption(1) for our example.</span></span>
    <span data-ttu-id="47ca2-168">Somme de contrôle</span><span class="sxs-lookup"><span data-stu-id="47ca2-168">Checksum</span></span> |<span data-ttu-id="47ca2-169">La somme de contrôle calculée MD5 pour la clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="47ca2-169">The MD5 calculated checksum for the content key.</span></span> <span data-ttu-id="47ca2-170">Elle est calculée en chiffrant l’ID de contenu avec la clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="47ca2-170">It is computed by encrypting the content Id with the content key.</span></span> <span data-ttu-id="47ca2-171">L’exemple de code montre comment calculer la somme de contrôle.</span><span class="sxs-lookup"><span data-stu-id="47ca2-171">The example code demonstrates how to calculate the checksum.</span></span>


### <a name="retrieve-the-protectionkeyid"></a><span data-ttu-id="47ca2-172">Récupération de ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="47ca2-172">Retrieve the ProtectionKeyId</span></span>
<span data-ttu-id="47ca2-173">L’exemple suivant montre comment récupérer ProtectionKeyId, une empreinte de certificat, pour le certificat que vous devez utiliser pour chiffrer votre clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="47ca2-173">The following example shows how to retrieve the ProtectionKeyId, a certificate thumbprint, for the certificate you must use when encrypting your content key.</span></span> <span data-ttu-id="47ca2-174">Effectuez cette étape pour vous assurer que vous possédez déjà le certificat approprié sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="47ca2-174">Do this step to make sure that you already have the appropriate certificate on your machine.</span></span>

<span data-ttu-id="47ca2-175">Demande :</span><span class="sxs-lookup"><span data-stu-id="47ca2-175">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="47ca2-176">Réponse :</span><span class="sxs-lookup"><span data-stu-id="47ca2-176">Response:</span></span>

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

### <a name="retrieve-the-protectionkey-for-the-protectionkeyid"></a><span data-ttu-id="47ca2-177">Récupération de ProtectionKey pour ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="47ca2-177">Retrieve the ProtectionKey for the ProtectionKeyId</span></span>
<span data-ttu-id="47ca2-178">L’exemple suivant montre comment récupérer le certificat X.509 à l’aide de ProtectionKeyId, que vous avez reçue lors de l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="47ca2-178">The following example shows how to retrieve the X.509 certificate using the ProtectionKeyId you received in the previous step.</span></span>

<span data-ttu-id="47ca2-179">Demande :</span><span class="sxs-lookup"><span data-stu-id="47ca2-179">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net

<span data-ttu-id="47ca2-180">Réponse :</span><span class="sxs-lookup"><span data-stu-id="47ca2-180">Response:</span></span>

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

### <a name="create-the-content-key"></a><span data-ttu-id="47ca2-181">Créez la clé de contenu</span><span class="sxs-lookup"><span data-stu-id="47ca2-181">Create the content key</span></span>
<span data-ttu-id="47ca2-182">Après avoir récupéré le certificat X.509 et utilisé sa clé publique pour chiffrer votre clé de contenu, créez une entité **ContentKey** et définissez ses valeurs de propriété en conséquence.</span><span class="sxs-lookup"><span data-stu-id="47ca2-182">After you have retrieved the X.509 certificate and used its public key to encrypt your content key, create a **ContentKey** entity and set its property values accordingly.</span></span>

<span data-ttu-id="47ca2-183">Une des valeurs que vous devez définir lors de la création d’une clé de contenu est son type.</span><span class="sxs-lookup"><span data-stu-id="47ca2-183">One of the values that you must set when create the content key is the type.</span></span> <span data-ttu-id="47ca2-184">Dans le cas du chiffrement de stockage, la valeur est « 1 ».</span><span class="sxs-lookup"><span data-stu-id="47ca2-184">In case of the storage encryption, the value is '1'.</span></span> 

<span data-ttu-id="47ca2-185">L’exemple suivant montre comment créer une **ContentKey** avec un **ContentKeyType** défini pour le chiffrement du stockage (« 1 ») et le **ProtectionKeyType** défini sur « 0 » pour indiquer que l’ID de la clé de protection est l’empreinte numérique du certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="47ca2-185">The following example shows how to create a **ContentKey** with a **ContentKeyType** set for storage encryption ("1") and the **ProtectionKeyType** set to "0" to indicate that the protection key Id is the X.509 certificate thumbprint.</span></span>  

<span data-ttu-id="47ca2-186">Demande</span><span class="sxs-lookup"><span data-stu-id="47ca2-186">Request</span></span>

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

<span data-ttu-id="47ca2-187">Réponse :</span><span class="sxs-lookup"><span data-stu-id="47ca2-187">Response:</span></span>

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

## <a name="create-an-asset"></a><span data-ttu-id="47ca2-188">Création d’une ressource</span><span class="sxs-lookup"><span data-stu-id="47ca2-188">Create an asset</span></span>
<span data-ttu-id="47ca2-189">L’exemple suivant montre comment créer une ressource.</span><span class="sxs-lookup"><span data-stu-id="47ca2-189">The following example shows how to create an asset.</span></span>

<span data-ttu-id="47ca2-190">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="47ca2-190">**HTTP Request**</span></span>

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

<span data-ttu-id="47ca2-191">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="47ca2-191">**HTTP Response**</span></span>

<span data-ttu-id="47ca2-192">Si l’opération réussit, l’élément suivant est retourné :</span><span class="sxs-lookup"><span data-stu-id="47ca2-192">If successful, the following is returned:</span></span>

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

## <a name="associate-the-contentkey-with-an-asset"></a><span data-ttu-id="47ca2-193">Association de la ContentKey avec une ressource</span><span class="sxs-lookup"><span data-stu-id="47ca2-193">Associate the ContentKey with an Asset</span></span>
<span data-ttu-id="47ca2-194">Après avoir créé la ContentKey, associez-la à votre ressource à l’aide de l’opération $links, comme illustré dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="47ca2-194">After creating the ContentKey, associate it with your Asset using the $links operation, as shown in the following example:</span></span>

<span data-ttu-id="47ca2-195">Demande :</span><span class="sxs-lookup"><span data-stu-id="47ca2-195">Request:</span></span>

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

<span data-ttu-id="47ca2-196">Réponse :</span><span class="sxs-lookup"><span data-stu-id="47ca2-196">Response:</span></span>

    HTTP/1.1 204 No Content 

## <a name="create-an-assetfile"></a><span data-ttu-id="47ca2-197">Création d’un AssetFile</span><span class="sxs-lookup"><span data-stu-id="47ca2-197">Create an AssetFile</span></span>
<span data-ttu-id="47ca2-198">L’entité [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) représente un fichier audio ou vidéo stocké dans un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="47ca2-198">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="47ca2-199">Un fichier de ressources est toujours associé à une ressource et une ressource peut contenir un ou plusieurs fichiers de ressources.</span><span class="sxs-lookup"><span data-stu-id="47ca2-199">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="47ca2-200">La tâche de Media Services Encoder échoue si un objet de fichier de ressources n’est pas associé à un fichier numérique dans un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="47ca2-200">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="47ca2-201">Notez que l’instance **AssetFile** et le fichier multimédia réel sont deux objets distincts.</span><span class="sxs-lookup"><span data-stu-id="47ca2-201">Note that the **AssetFile** instance and the actual media file are two distinct objects.</span></span> <span data-ttu-id="47ca2-202">L’instance AssetFile contient des métadonnées concernant le fichier multimédia, tandis que le fichier multimédia contient le contenu multimédia réel.</span><span class="sxs-lookup"><span data-stu-id="47ca2-202">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span></span>

<span data-ttu-id="47ca2-203">Après avoir téléchargé le fichier multimédia numérique dans un conteneur d’objets blob, vous utiliserez la demande HTTP **MERGE** pour mettre à jour AssetFile avec des informations sur votre fichier multimédia (non indiqué dans cette rubrique).</span><span class="sxs-lookup"><span data-stu-id="47ca2-203">After you upload your digital media file into a blob container, you will use the **MERGE** HTTP request to update the AssetFile with information about your media file (not shown in this topic).</span></span> 

<span data-ttu-id="47ca2-204">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="47ca2-204">**HTTP Request**</span></span>

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

<span data-ttu-id="47ca2-205">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="47ca2-205">**HTTP Response**</span></span>

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
