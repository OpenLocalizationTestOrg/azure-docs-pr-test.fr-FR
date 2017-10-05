---
title: "Création de ContentKeys avec .NET"
description: "Apprenez à créer des clés de contenu qui fournissent un accès sécurisé aux ressources."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 225b05e5-7d30-409c-b5b7-3ef0634310c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 3280a6fcde59bae360da7cb9fea4bb649f984e43
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-contentkeys-with-net"></a><span data-ttu-id="ce83b-103">Création de ContentKeys avec .NET</span><span class="sxs-lookup"><span data-stu-id="ce83b-103">Create ContentKeys with .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ce83b-104">REST</span><span class="sxs-lookup"><span data-stu-id="ce83b-104">REST</span></span>](media-services-rest-create-contentkey.md)
> * [<span data-ttu-id="ce83b-105">.NET</span><span class="sxs-lookup"><span data-stu-id="ce83b-105">.NET</span></span>](media-services-dotnet-create-contentkey.md)
> 
> 

<span data-ttu-id="ce83b-106">Media Services vous permet de créer et de fournir des ressources chiffrées.</span><span class="sxs-lookup"><span data-stu-id="ce83b-106">Media Services enables you to create and deliver encrypted assets.</span></span> <span data-ttu-id="ce83b-107">**ContentKey** fournit un accès sécurisé à vos **éléments multimédias**.</span><span class="sxs-lookup"><span data-stu-id="ce83b-107">A **ContentKey** provides secure access to your **Asset**s.</span></span> 

<span data-ttu-id="ce83b-108">Quand vous créez un élément multimédia (par exemple, avant de [charger des fichiers](media-services-dotnet-upload-files.md)), vous pouvez spécifier les options de chiffrement suivantes : **StorageEncrypted**, **CommonEncryptionProtected** ou **EnvelopeEncryptionProtected**.</span><span class="sxs-lookup"><span data-stu-id="ce83b-108">When you create a new asset (for example, before you [upload files](media-services-dotnet-upload-files.md)), you can specify the following encryption options: **StorageEncrypted**, **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span></span> 

<span data-ttu-id="ce83b-109">Quand vous fournissez des éléments multimédias à vos clients, vous pouvez [configurer les éléments multimédias devant être chiffrés dynamiquement](media-services-dotnet-configure-asset-delivery-policy.md) avec un des deux chiffrements suivants : **DynamicEnvelopeEncryption** ou **DynamicCommonEncryption**.</span><span class="sxs-lookup"><span data-stu-id="ce83b-109">When you deliver assets to your clients, you can [configure for assets to be dynamically encrypted](media-services-dotnet-configure-asset-delivery-policy.md) with one of the following two encryptions: **DynamicEnvelopeEncryption** or **DynamicCommonEncryption**.</span></span>

<span data-ttu-id="ce83b-110">Les ressources chiffrées doivent être associées à des **ContentKey**.</span><span class="sxs-lookup"><span data-stu-id="ce83b-110">Encrypted assets have to be associated with **ContentKey**s.</span></span> <span data-ttu-id="ce83b-111">Cet article décrit comment créer une clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="ce83b-111">This article describes how to create a content key.</span></span>

> [!NOTE]
> <span data-ttu-id="ce83b-112">Quand vous créez un élément multimédia **StorageEncrypted** à l’aide du SDK Media Services .NET, **ContentKey** est automatiquement créé et lié à l’élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="ce83b-112">When creating a new **StorageEncrypted** asset using the Media Services .NET SDK , the **ContentKey** is automatically created and linked with the asset.</span></span>
> 
> 

## <a name="contentkeytype"></a><span data-ttu-id="ce83b-113">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="ce83b-113">ContentKeyType</span></span>
<span data-ttu-id="ce83b-114">Une des valeurs que vous devez définir lors de la création d’une clé de contenu est le type de clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="ce83b-114">One of the values that you must set when create a content key is the content key type.</span></span> <span data-ttu-id="ce83b-115">Choisissez une des valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="ce83b-115">Choose from one of the following values.</span></span> 

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

## <span data-ttu-id="ce83b-116"><a id="envelope_contentkey"></a>Créer une ContentKey de type enveloppe</span><span class="sxs-lookup"><span data-stu-id="ce83b-116"><a id="envelope_contentkey"></a>Create envelope type ContentKey</span></span>
<span data-ttu-id="ce83b-117">L’extrait de code suivant crée une clé de contenu du type de chiffrement d’enveloppe.</span><span class="sxs-lookup"><span data-stu-id="ce83b-117">The following code snippet creates a content key of the envelope encryption type.</span></span> <span data-ttu-id="ce83b-118">Il associe ensuite la clé à l’élément multimédia spécifié.</span><span class="sxs-lookup"><span data-stu-id="ce83b-118">It then associates the key with the specified asset.</span></span>

    static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
    {
        // Create envelope encryption content key
        Guid keyId = Guid.NewGuid();
        byte[] contentKey = GetRandomBuffer(16);

        IContentKey key = _context.ContentKeys.Create(
                                keyId,
                                contentKey,
                                "ContentKey",
                                ContentKeyType.EnvelopeEncryption);

        asset.ContentKeys.Add(key);

        return key;
    }

    static private byte[] GetRandomBuffer(int size)
    {
        byte[] randomBytes = new byte[size];
        using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
        {
            rng.GetBytes(randomBytes);
        }

        return randomBytes;
    }

<span data-ttu-id="ce83b-119">appel</span><span class="sxs-lookup"><span data-stu-id="ce83b-119">call</span></span>

    IContentKey key = CreateEnvelopeTypeContentKey(encryptedsset);



## <span data-ttu-id="ce83b-120"><a id="common_contentkey"></a>Créer une ContentKey de type commun</span><span class="sxs-lookup"><span data-stu-id="ce83b-120"><a id="common_contentkey"></a>Create common type ContentKey</span></span>
<span data-ttu-id="ce83b-121">L’extrait de code suivant crée une clé de contenu du type de chiffrement commun.</span><span class="sxs-lookup"><span data-stu-id="ce83b-121">The following code snippet creates a content key of the common encryption type.</span></span> <span data-ttu-id="ce83b-122">Il associe ensuite la clé à l’élément multimédia spécifié.</span><span class="sxs-lookup"><span data-stu-id="ce83b-122">It then associates the key with the specified asset.</span></span>

    static public IContentKey CreateCommonTypeContentKey(IAsset asset)
    {
        // Create common encryption content key
        Guid keyId = Guid.NewGuid();
        byte[] contentKey = GetRandomBuffer(16);

        IContentKey key = _context.ContentKeys.Create(
                                keyId,
                                contentKey,
                                "ContentKey",
                                ContentKeyType.CommonEncryption);

        // Associate the key with the asset.
        asset.ContentKeys.Add(key);

        return key;
    }

    static private byte[] GetRandomBuffer(int length)
    {
        var returnValue = new byte[length];

        using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
        {
            rng.GetBytes(returnValue);
        }

        return returnValue;
    }
<span data-ttu-id="ce83b-123">appel</span><span class="sxs-lookup"><span data-stu-id="ce83b-123">call</span></span>

    IContentKey key = CreateCommonTypeContentKey(encryptedsset); 


## <a name="media-services-learning-paths"></a><span data-ttu-id="ce83b-124">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="ce83b-124">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ce83b-125">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="ce83b-125">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

