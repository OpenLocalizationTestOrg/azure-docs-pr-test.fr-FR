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
# <a name="encrypting-your-content-with-storage-encryption"></a><span data-ttu-id="ccde6-103">Chiffrer votre contenu avec le chiffrement de stockage</span><span class="sxs-lookup"><span data-stu-id="ccde6-103">Encrypting your content with storage encryption</span></span>

<span data-ttu-id="ccde6-104">Il est vivement recommandé tooencrypt votre contenu localement avec AES-256 bits de chiffrement, puis le télécharger tooAzure Storage où il sera stocké et chiffré au repos.</span><span class="sxs-lookup"><span data-stu-id="ccde6-104">It is highly recommended tooencrypt your content locally using AES-256 bit encryption and then upload it tooAzure Storage where it will be stored encrypted at rest.</span></span>

<span data-ttu-id="ccde6-105">Cet article donne une vue d’ensemble du chiffrement de stockage AMS et vous montre comment tooupload hello stockage chiffré dans le contenu :</span><span class="sxs-lookup"><span data-stu-id="ccde6-105">This article gives an overview of AMS storage encryption and shows you how tooupload hello storage encrypted content:</span></span>

* <span data-ttu-id="ccde6-106">Créez une clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="ccde6-106">Create a content key.</span></span>
* <span data-ttu-id="ccde6-107">Créez une ressource.</span><span class="sxs-lookup"><span data-stu-id="ccde6-107">Create an Asset.</span></span> <span data-ttu-id="ccde6-108">Définissez hello AssetCreationOption tooStorageEncryption lors de la création de hello actif.</span><span class="sxs-lookup"><span data-stu-id="ccde6-108">Set hello AssetCreationOption tooStorageEncryption when creating hello Asset.</span></span>
  
     <span data-ttu-id="ccde6-109">Les éléments multimédias chiffrés ont toobe associé aux clés de contenu.</span><span class="sxs-lookup"><span data-stu-id="ccde6-109">Encrypted assets have toobe associated with content keys.</span></span>
* <span data-ttu-id="ccde6-110">Ressource de contenu toohello clé lien hello.</span><span class="sxs-lookup"><span data-stu-id="ccde6-110">Link hello content key toohello asset.</span></span>  
* <span data-ttu-id="ccde6-111">Définir le chiffrement hello les paramètres sur les entités AssetFile hello.</span><span class="sxs-lookup"><span data-stu-id="ccde6-111">Set hello encryption related parameters on hello AssetFile entities.</span></span>

## <a name="considerations"></a><span data-ttu-id="ccde6-112">Considérations</span><span class="sxs-lookup"><span data-stu-id="ccde6-112">Considerations</span></span> 

<span data-ttu-id="ccde6-113">Si vous voulez toodeliver un élément multimédia chiffré de stockage, vous devez configurer la stratégie de remise de l’élément multimédia hello.</span><span class="sxs-lookup"><span data-stu-id="ccde6-113">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="ccde6-114">Avant que votre élément multimédia peut être transmis en continu, hello de diffusion en continu flux et chiffrement de stockage de serveur supprime hello votre contenu à l’aide de hello spécifié de stratégie de remise.</span><span class="sxs-lookup"><span data-stu-id="ccde6-114">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="ccde6-115">Pour plus d'informations, consultez [Configuration des stratégies de distribution de ressources](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="ccde6-115">For more information, see [Configuring Asset Delivery Policies](media-services-rest-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="ccde6-116">Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="ccde6-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="ccde6-117">Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="ccde6-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="ccde6-118">Connecter les Services de tooMedia</span><span class="sxs-lookup"><span data-stu-id="ccde6-118">Connect tooMedia Services</span></span>

<span data-ttu-id="ccde6-119">Pour plus d’informations sur la façon dont tooconnect toohello AMS API, consultez [hello accès API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="ccde6-119">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="ccde6-120">Après vous être connecté toohttps://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI de Media Services.</span><span class="sxs-lookup"><span data-stu-id="ccde6-120">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="ccde6-121">Vous devez effectuer les appels suivants toohello nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="ccde6-121">You must make subsequent calls toohello new URI.</span></span>

## <a name="storage-encryption-overview"></a><span data-ttu-id="ccde6-122">Vue d’ensemble du chiffrement du stockage</span><span class="sxs-lookup"><span data-stu-id="ccde6-122">Storage encryption overview</span></span>
<span data-ttu-id="ccde6-123">s’applique le chiffrement de stockage Hello AMS **AES-CTR** mode chiffrement toohello intégralité du fichier.</span><span class="sxs-lookup"><span data-stu-id="ccde6-123">hello AMS storage encryption applies **AES-CTR** mode encryption toohello entire file.</span></span>  <span data-ttu-id="ccde6-124">Le mode AES-CTR est un chiffrement par blocs qui permet de chiffrer des données de longueur arbitraire sans avoir besoin de remplissage.</span><span class="sxs-lookup"><span data-stu-id="ccde6-124">AES-CTR mode is a block cipher that can encrypt arbitrary length data without need for padding.</span></span> <span data-ttu-id="ccde6-125">Il s’exécute par chiffrement un bloc de compteur avec l’algorithme AES de hello et ensuite la sortie de hello XOR-effectue une opération d’AES avec hello données tooencrypt ou de déchiffrer.</span><span class="sxs-lookup"><span data-stu-id="ccde6-125">It operates by encrypting a counter block with hello AES algorithm and then XOR-ing hello output of AES with hello data tooencrypt or decrypt.</span></span>  <span data-ttu-id="ccde6-126">bloc de compteur Hello utilisé est construit en copiant la valeur hello hello InitializationVector toobytes 0 too7 de la valeur du compteur hello et too15 octets 8 de la valeur du compteur hello sont définies toozero.</span><span class="sxs-lookup"><span data-stu-id="ccde6-126">hello counter block used is constructed by copying hello value of hello InitializationVector toobytes 0 too7 of hello counter value and bytes 8 too15 of hello counter value are set toozero.</span></span> <span data-ttu-id="ccde6-127">Du bloc de compteur de 16 octets hello, octets 8 too15 (c'est-à-dire hello octets les moins significatifs) sont utilisés comme un entier non signé simple 64 bits qui est incrémenté d’un pour chaque bloc de données traitées et est conservé dans l’ordre d’octet du réseau.</span><span class="sxs-lookup"><span data-stu-id="ccde6-127">Of hello 16 byte counter block, bytes 8 too15 (i.e. hello least significant bytes) are used as a simple 64 bit unsigned integer that is incremented by one for each subsequent block of data processed and is kept in network byte order.</span></span> <span data-ttu-id="ccde6-128">Notez que si cet entier atteint la valeur maximale hello (0xFFFFFFFFFFFFFFFF) puis incrémenter réinitialise hello bloc compteur toozero (too15 octets 8) sans affecter hello autres 64 bits du compteur de hello (autrement dit, les too7 octets 0).</span><span class="sxs-lookup"><span data-stu-id="ccde6-128">Note that if this integer reaches hello maximum value (0xFFFFFFFFFFFFFFFF) then incrementing it resets hello block counter toozero (bytes 8 too15) without affecting hello other 64 bits of hello counter (i.e. bytes 0 too7).</span></span>   <span data-ttu-id="ccde6-129">Dans l’ordre toomaintain hello la sécurité de chiffrement de mode hello AES-CTR, hello InitializationVector valeur pour un identificateur de clé donnée pour chaque clé de contenu doit être unique pour chaque fichier et de fichiers doivent être inférieure à 2 ^ 64 blocs de longueur.</span><span class="sxs-lookup"><span data-stu-id="ccde6-129">In order toomaintain hello security of hello AES-CTR mode encryption, hello InitializationVector value for a given Key Identifier for each content key shall be unique for each file and files shall be less than 2^64 blocks in length.</span></span>  <span data-ttu-id="ccde6-130">Il s’agit de tooensure une valeur de compteur n’est jamais réutilisé avec une clé donnée.</span><span class="sxs-lookup"><span data-stu-id="ccde6-130">This is tooensure that a counter value is never reused with a given key.</span></span> <span data-ttu-id="ccde6-131">Pour plus d’informations sur le mode CTR hello, consultez [cette page wiki](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (article wiki de hello utilise le terme hello « Nonce » au lieu de « InitializationVector »).</span><span class="sxs-lookup"><span data-stu-id="ccde6-131">For more information about hello CTR mode, see [this wiki page](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (hello wiki article uses hello term "Nonce" instead of "InitializationVector").</span></span>

<span data-ttu-id="ccde6-132">Utilisez **le chiffrement de stockage** tooencrypt votre contenu en clair localement avec AES-256 bits de chiffrement, puis le télécharger tooAzure Storage où il est stocké et chiffré au repos.</span><span class="sxs-lookup"><span data-stu-id="ccde6-132">Use **Storage Encryption** tooencrypt your clear content locally using AES-256 bit encryption and then upload it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="ccde6-133">Les éléments multimédias protégés par chiffrement de stockage sont automatiquement déchiffrés et placés dans un tooencoding préalable de système de fichiers chiffrés et éventuellement RE-chiffrée toouploading préalable comme un nouvel élément multimédia de sortie.</span><span class="sxs-lookup"><span data-stu-id="ccde6-133">Assets protected with storage encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="ccde6-134">Hello est principalement utilisé pour le chiffrement de stockage lorsque vous souhaitez toosecure vos fichiers multimédias d’entrée de haute qualité avec un chiffrement renforcé au reste sur le disque.</span><span class="sxs-lookup"><span data-stu-id="ccde6-134">hello primary use case for storage encryption is when you want toosecure your high quality input media files with strong encryption at rest on disk.</span></span>

<span data-ttu-id="ccde6-135">Dans l’ordre toodeliver un élément multimédia chiffré de stockage, vous devez configurer la stratégie de remise de hello actif afin que Media Services sache comment vous souhaitez que toodeliver votre contenu.</span><span class="sxs-lookup"><span data-stu-id="ccde6-135">In order toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy so Media Services knows how you want toodeliver your content.</span></span> <span data-ttu-id="ccde6-136">Avant que votre élément multimédia peut être transmis en continu, hello de diffusion en continu flux et chiffrement de stockage de serveur supprime hello votre contenu à l’aide de hello spécifié de stratégie de remise (par exemple, AES, chiffrement commun ou aucun chiffrement).</span><span class="sxs-lookup"><span data-stu-id="ccde6-136">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy (for example, AES, common encryption, or no encryption).</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="ccde6-137">Créer des ContentKeys utilisées pour le chiffrement</span><span class="sxs-lookup"><span data-stu-id="ccde6-137">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="ccde6-138">Les éléments multimédias chiffrés ont toobe associé à la clé de chiffrement de stockage.</span><span class="sxs-lookup"><span data-stu-id="ccde6-138">Encrypted assets have toobe associated with Storage Encryption key.</span></span> <span data-ttu-id="ccde6-139">Vous devez créer hello contenu toobe clé utilisé pour le chiffrement avant de créer des fichiers d’éléments multimédias hello.</span><span class="sxs-lookup"><span data-stu-id="ccde6-139">You must create hello content key toobe used for encryption before creating hello asset files.</span></span> <span data-ttu-id="ccde6-140">Cette section décrit comment toocreate une clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="ccde6-140">This section describes how toocreate a content key.</span></span>

<span data-ttu-id="ccde6-141">Hello Voici les étapes générales pour la génération de clés de contenu que vous associerez avec les composants qui vous voulez toobe chiffré.</span><span class="sxs-lookup"><span data-stu-id="ccde6-141">hello following are general steps for generating content keys that you will associate with assets that you want toobe encrypted.</span></span> 

1. <span data-ttu-id="ccde6-142">Pour le chiffrement du stockage, générez de façon aléatoire une clé AES de 32 octets.</span><span class="sxs-lookup"><span data-stu-id="ccde6-142">For storage encryption, randomly generate a 32-byte AES key.</span></span> 
   
    <span data-ttu-id="ccde6-143">Ce sera la clé de contenu hello pour votre élément multimédia, ce qui signifie que tous les fichiers associés à cet élément multimédia sera peut-être toouse hello même clé de contenu pendant le déchiffrement.</span><span class="sxs-lookup"><span data-stu-id="ccde6-143">This will be hello content key for your asset, which means all files associated with that asset will need toouse hello same content key during decryption.</span></span> 
2. <span data-ttu-id="ccde6-144">Appelez hello [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) et [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) tooget de méthodes hello certificat X.509 correct doit être utilisé tooencrypt votre clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="ccde6-144">Call hello [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) and [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methods tooget hello correct X.509 Certificate that must be used tooencrypt your content key.</span></span>
3. <span data-ttu-id="ccde6-145">Chiffrer votre clé de contenu avec une clé publique du certificat X.509 de hello hello.</span><span class="sxs-lookup"><span data-stu-id="ccde6-145">Encrypt your content key with hello public key of hello X.509 Certificate.</span></span> 
   
   <span data-ttu-id="ccde6-146">Media Services .NET SDK utilise RSA avec OAEP lorsque vous effectuez un chiffrement de hello.</span><span class="sxs-lookup"><span data-stu-id="ccde6-146">Media Services .NET SDK uses RSA with OAEP when doing hello encryption.</span></span>  <span data-ttu-id="ccde6-147">Vous pouvez voir un exemple .NET Bonjour [EncryptSymmetricKeyData fonction](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="ccde6-147">You can see a .NET example in hello [EncryptSymmetricKeyData function](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
4. <span data-ttu-id="ccde6-148">Créez une valeur de somme de contrôle calculée à l’aide d’identificateur de clé hello et clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="ccde6-148">Create a checksum value calculated using hello key identifier and content key.</span></span> <span data-ttu-id="ccde6-149">Hello .NET l’exemple suivant calcule la somme de contrôle hello à l’aide de la partie GUID de hello d’identificateur de clé hello et hello effacer la clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="ccde6-149">hello following .NET example calculates hello checksum using hello GUID part of hello key identifier and hello clear content key.</span></span>

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

1. <span data-ttu-id="ccde6-150">Créer la clé de contenu hello avec hello **EncryptedContentKey** (converties en chaîne encodée toobase64), **ProtectionKeyId**, **ProtectionKeyType**,  **ContentKeyType**, et **Checksum** valeurs que vous avez reçu dans les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="ccde6-150">Create hello Content key with hello **EncryptedContentKey** (converted toobase64-encoded string), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType**, and **Checksum** values you have received in previous steps.</span></span>

    <span data-ttu-id="ccde6-151">Pour le chiffrement de stockage, hello propriétés suivantes doivent être incluses dans le corps de la demande hello.</span><span class="sxs-lookup"><span data-stu-id="ccde6-151">For storage encryption, hello following properties should be included in hello request body.</span></span>

    <span data-ttu-id="ccde6-152">Propriété du corps de la demande</span><span class="sxs-lookup"><span data-stu-id="ccde6-152">Request body property</span></span>    | <span data-ttu-id="ccde6-153">Description</span><span class="sxs-lookup"><span data-stu-id="ccde6-153">Description</span></span>
    ---|---
    <span data-ttu-id="ccde6-154">Id</span><span class="sxs-lookup"><span data-stu-id="ccde6-154">Id</span></span> | <span data-ttu-id="ccde6-155">Hello Id de ContentKey que nous générons nous-mêmes hello suivant à l’aide de mettre en forme, « Kid :<NEW GUID>».</span><span class="sxs-lookup"><span data-stu-id="ccde6-155">hello ContentKey Id which we generate ourselves using hello following format, “nb:kid:UUID:<NEW GUID>”.</span></span>
    <span data-ttu-id="ccde6-156">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="ccde6-156">ContentKeyType</span></span> | <span data-ttu-id="ccde6-157">Type de clé de contenu hello il s’agit en tant qu’entier pour cette clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="ccde6-157">This is hello content key type as an integer for this content key.</span></span> <span data-ttu-id="ccde6-158">Nous transmettons la valeur hello 1 pour le chiffrement de stockage.</span><span class="sxs-lookup"><span data-stu-id="ccde6-158">We pass hello value 1 for storage encryption.</span></span>
    <span data-ttu-id="ccde6-159">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="ccde6-159">EncryptedContentKey</span></span> | <span data-ttu-id="ccde6-160">Nous créons une valeur de clé de contenu qui est une valeur de 256 bits (32 octets).</span><span class="sxs-lookup"><span data-stu-id="ccde6-160">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="ccde6-161">clé de Hello est chiffré à l’aide de hello stockage certificat X.509 de chiffrement que nous récupérons à partir de Microsoft Azure Media Services en exécutant une demande HTTP GET hello GetProtectionKeyId et GetProtectionKey méthodes.</span><span class="sxs-lookup"><span data-stu-id="ccde6-161">hello key is encrypted using hello storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for hello GetProtectionKeyId and GetProtectionKey Methods.</span></span> <span data-ttu-id="ccde6-162">Par exemple, consultez hello suivant le code .NET : hello **EncryptSymmetricKeyData** méthode définie [ici](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="ccde6-162">As an example, see hello following .NET code: hello  **EncryptSymmetricKeyData** method defined [here](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
    <span data-ttu-id="ccde6-163">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="ccde6-163">ProtectionKeyId</span></span> | <span data-ttu-id="ccde6-164">Cela est hello id de clé de protection pour le certificat X.509 de chiffrement de stockage de hello a été utilisé tooencrypt notre clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="ccde6-164">This is hello protection key id for hello storage encryption X.509 certificate that was used tooencrypt our content key.</span></span>
    <span data-ttu-id="ccde6-165">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="ccde6-165">ProtectionKeyType</span></span> | <span data-ttu-id="ccde6-166">Il s’agit de type de chiffrement de hello pour la clé de protection hello clé de contenu utilisés tooencrypt hello.</span><span class="sxs-lookup"><span data-stu-id="ccde6-166">This is hello encryption type for hello protection key that was used tooencrypt hello content key.</span></span> <span data-ttu-id="ccde6-167">Cette valeur est StorageEncryption(1) dans notre exemple.</span><span class="sxs-lookup"><span data-stu-id="ccde6-167">This value is StorageEncryption(1) for our example.</span></span>
    <span data-ttu-id="ccde6-168">Somme de contrôle</span><span class="sxs-lookup"><span data-stu-id="ccde6-168">Checksum</span></span> |<span data-ttu-id="ccde6-169">somme de contrôle calculée Hello MD5 pour la clé de contenu hello.</span><span class="sxs-lookup"><span data-stu-id="ccde6-169">hello MD5 calculated checksum for hello content key.</span></span> <span data-ttu-id="ccde6-170">Elle est calculée en chiffrant l’Id de contenu hello avec la clé de contenu hello.</span><span class="sxs-lookup"><span data-stu-id="ccde6-170">It is computed by encrypting hello content Id with hello content key.</span></span> <span data-ttu-id="ccde6-171">Hello exemple de code montre comment toocalculate hello somme de contrôle.</span><span class="sxs-lookup"><span data-stu-id="ccde6-171">hello example code demonstrates how toocalculate hello checksum.</span></span>


### <a name="retrieve-hello-protectionkeyid"></a><span data-ttu-id="ccde6-172">Récupérer hello ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="ccde6-172">Retrieve hello ProtectionKeyId</span></span>
<span data-ttu-id="ccde6-173">Bonjour à l’exemple suivant montre comment tooretrieve hello ProtectionKeyId, une empreinte de certificat pour le certificat hello vous devez utiliser lors du chiffrement de votre clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="ccde6-173">hello following example shows how tooretrieve hello ProtectionKeyId, a certificate thumbprint, for hello certificate you must use when encrypting your content key.</span></span> <span data-ttu-id="ccde6-174">Effectuez cette étape toomake que vous avez déjà les certificats appropriés hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ccde6-174">Do this step toomake sure that you already have hello appropriate certificate on your machine.</span></span>

<span data-ttu-id="ccde6-175">Demande :</span><span class="sxs-lookup"><span data-stu-id="ccde6-175">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="ccde6-176">Réponse :</span><span class="sxs-lookup"><span data-stu-id="ccde6-176">Response:</span></span>

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

### <a name="retrieve-hello-protectionkey-for-hello-protectionkeyid"></a><span data-ttu-id="ccde6-177">Récupérer ProtectionKey de hello pour hello ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="ccde6-177">Retrieve hello ProtectionKey for hello ProtectionKeyId</span></span>
<span data-ttu-id="ccde6-178">Hello suivant montre comment le certificat X.509 de tooretrieve hello à l’aide de hello ProtectionKeyId vous avez reçu dans l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="ccde6-178">hello following example shows how tooretrieve hello X.509 certificate using hello ProtectionKeyId you received in hello previous step.</span></span>

<span data-ttu-id="ccde6-179">Demande :</span><span class="sxs-lookup"><span data-stu-id="ccde6-179">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net

<span data-ttu-id="ccde6-180">Réponse :</span><span class="sxs-lookup"><span data-stu-id="ccde6-180">Response:</span></span>

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

### <a name="create-hello-content-key"></a><span data-ttu-id="ccde6-181">Créer la clé de contenu hello</span><span class="sxs-lookup"><span data-stu-id="ccde6-181">Create hello content key</span></span>
<span data-ttu-id="ccde6-182">Après avoir récupéré le certificat X.509 de hello et utilisé son tooencrypt de clé publique de votre clé de contenu, créez un **ContentKey** entité et définissez sa propriété de valeurs en conséquence.</span><span class="sxs-lookup"><span data-stu-id="ccde6-182">After you have retrieved hello X.509 certificate and used its public key tooencrypt your content key, create a **ContentKey** entity and set its property values accordingly.</span></span>

<span data-ttu-id="ccde6-183">Une des valeurs hello que vous devez définir quand créer hello contenu clé est de type de hello.</span><span class="sxs-lookup"><span data-stu-id="ccde6-183">One of hello values that you must set when create hello content key is hello type.</span></span> <span data-ttu-id="ccde6-184">En cas de chiffrement de stockage hello, valeur de hello est « 1 ».</span><span class="sxs-lookup"><span data-stu-id="ccde6-184">In case of hello storage encryption, hello value is '1'.</span></span> 

<span data-ttu-id="ccde6-185">Hello suivant montre l’exemple de comment toocreate un **ContentKey** avec un **ContentKeyType** définie pour le chiffrement de stockage (« 1 ») et hello **ProtectionKeyType** défini trop « 0 » tooindicate qui hello Id de clé de protection est l’empreinte de certificat X.509 hello.</span><span class="sxs-lookup"><span data-stu-id="ccde6-185">hello following example shows how toocreate a **ContentKey** with a **ContentKeyType** set for storage encryption ("1") and hello **ProtectionKeyType** set too"0" tooindicate that hello protection key Id is hello X.509 certificate thumbprint.</span></span>  

<span data-ttu-id="ccde6-186">Demande</span><span class="sxs-lookup"><span data-stu-id="ccde6-186">Request</span></span>

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

<span data-ttu-id="ccde6-187">Réponse :</span><span class="sxs-lookup"><span data-stu-id="ccde6-187">Response:</span></span>

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

## <a name="create-an-asset"></a><span data-ttu-id="ccde6-188">Créer une ressource</span><span class="sxs-lookup"><span data-stu-id="ccde6-188">Create an asset</span></span>
<span data-ttu-id="ccde6-189">Hello suivant montre l’exemple de comment toocreate un élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="ccde6-189">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="ccde6-190">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="ccde6-190">**HTTP Request**</span></span>

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

<span data-ttu-id="ccde6-191">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="ccde6-191">**HTTP Response**</span></span>

<span data-ttu-id="ccde6-192">En cas de réussite, suivant de hello est retournée :</span><span class="sxs-lookup"><span data-stu-id="ccde6-192">If successful, hello following is returned:</span></span>

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

## <a name="associate-hello-contentkey-with-an-asset"></a><span data-ttu-id="ccde6-193">Associer des hello ContentKey à un élément multimédia</span><span class="sxs-lookup"><span data-stu-id="ccde6-193">Associate hello ContentKey with an Asset</span></span>
<span data-ttu-id="ccde6-194">Après avoir créé le hello ContentKey, associez-le à votre élément multimédia à l’aide de l’opération de hello $links, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="ccde6-194">After creating hello ContentKey, associate it with your Asset using hello $links operation, as shown in hello following example:</span></span>

<span data-ttu-id="ccde6-195">Demande :</span><span class="sxs-lookup"><span data-stu-id="ccde6-195">Request:</span></span>

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

<span data-ttu-id="ccde6-196">Réponse :</span><span class="sxs-lookup"><span data-stu-id="ccde6-196">Response:</span></span>

    HTTP/1.1 204 No Content 

## <a name="create-an-assetfile"></a><span data-ttu-id="ccde6-197">Création d’un AssetFile</span><span class="sxs-lookup"><span data-stu-id="ccde6-197">Create an AssetFile</span></span>
<span data-ttu-id="ccde6-198">Hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entité représente un fichier vidéo ou audio qui est stocké dans un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="ccde6-198">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="ccde6-199">Un fichier de ressources est toujours associé à une ressource et une ressource peut contenir un ou plusieurs fichiers de ressources.</span><span class="sxs-lookup"><span data-stu-id="ccde6-199">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="ccde6-200">tâche d’encodeur Media Services Hello échoue si un objet de fichier actif n’est pas associé à un fichier numérique dans un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="ccde6-200">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="ccde6-201">Notez que hello **AssetFile** instance et le fichier multimédia lui-même de hello sont deux objets distincts.</span><span class="sxs-lookup"><span data-stu-id="ccde6-201">Note that hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="ccde6-202">instance AssetFile de Hello contient des métadonnées sur le fichier du média hello, tandis que le fichier du média hello contient le contenu du média réel hello.</span><span class="sxs-lookup"><span data-stu-id="ccde6-202">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

<span data-ttu-id="ccde6-203">Après avoir téléchargé votre fichier multimédia numérique sur un conteneur d’objets blob, vous allez utiliser hello **fusion** tooupdate hello AssetFile HTTP demande des informations sur votre fichier de support (non illustré dans cette rubrique).</span><span class="sxs-lookup"><span data-stu-id="ccde6-203">After you upload your digital media file into a blob container, you will use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (not shown in this topic).</span></span> 

<span data-ttu-id="ccde6-204">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="ccde6-204">**HTTP Request**</span></span>

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

<span data-ttu-id="ccde6-205">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="ccde6-205">**HTTP Response**</span></span>

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
