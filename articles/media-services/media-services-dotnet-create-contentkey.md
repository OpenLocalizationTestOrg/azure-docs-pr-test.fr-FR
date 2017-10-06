---
title: aaaCreate ContentKeys avec .NET
description: "Découvrez comment accéder à tooAssets toocreate clés de contenu qui fournissent sécurisé."
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
ms.openlocfilehash: 35909c64e8393e228be75c464a034ffc40122952
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-contentkeys-with-net"></a><span data-ttu-id="d3037-103">Création de ContentKeys avec .NET</span><span class="sxs-lookup"><span data-stu-id="d3037-103">Create ContentKeys with .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d3037-104">REST</span><span class="sxs-lookup"><span data-stu-id="d3037-104">REST</span></span>](media-services-rest-create-contentkey.md)
> * [<span data-ttu-id="d3037-105">.NET</span><span class="sxs-lookup"><span data-stu-id="d3037-105">.NET</span></span>](media-services-dotnet-create-contentkey.md)
> 
> 

<span data-ttu-id="d3037-106">Media Services vous permet de toocreate et fournir les éléments multimédias chiffrés.</span><span class="sxs-lookup"><span data-stu-id="d3037-106">Media Services enables you toocreate and deliver encrypted assets.</span></span> <span data-ttu-id="d3037-107">A **ContentKey** fournit un accès sécurisé tooyour **Asset**s.</span><span class="sxs-lookup"><span data-stu-id="d3037-107">A **ContentKey** provides secure access tooyour **Asset**s.</span></span> 

<span data-ttu-id="d3037-108">Lorsque vous créez un nouvel élément multimédia (par exemple, avant de vous [télécharger des fichiers](media-services-dotnet-upload-files.md)), vous pouvez spécifier hello options de chiffrement suivantes : **StorageEncrypted**, **CommonEncryptionProtected**, ou **EnvelopeEncryptionProtected**.</span><span class="sxs-lookup"><span data-stu-id="d3037-108">When you create a new asset (for example, before you [upload files](media-services-dotnet-upload-files.md)), you can specify hello following encryption options: **StorageEncrypted**, **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span></span> 

<span data-ttu-id="d3037-109">Lorsque vous fournissez des ressources tooyour clients, vous pouvez [configurer pour toobe actifs dynamiquement chiffré](media-services-dotnet-configure-asset-delivery-policy.md) avec l’un des hello suivant deux chiffrements : **DynamicEnvelopeEncryption** ou  **DynamicCommonEncryption**.</span><span class="sxs-lookup"><span data-stu-id="d3037-109">When you deliver assets tooyour clients, you can [configure for assets toobe dynamically encrypted](media-services-dotnet-configure-asset-delivery-policy.md) with one of hello following two encryptions: **DynamicEnvelopeEncryption** or **DynamicCommonEncryption**.</span></span>

<span data-ttu-id="d3037-110">Les éléments multimédias chiffrés ont toobe associé **ContentKey**s.</span><span class="sxs-lookup"><span data-stu-id="d3037-110">Encrypted assets have toobe associated with **ContentKey**s.</span></span> <span data-ttu-id="d3037-111">Cet article décrit comment toocreate une clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="d3037-111">This article describes how toocreate a content key.</span></span>

> [!NOTE]
> <span data-ttu-id="d3037-112">Lorsque vous créez un nouveau **StorageEncrypted** à l’aide de l’élément multimédia hello Media Services .NET SDK, hello **ContentKey** est automatiquement créé et lié à l’élément multimédia de hello.</span><span class="sxs-lookup"><span data-stu-id="d3037-112">When creating a new **StorageEncrypted** asset using hello Media Services .NET SDK , hello **ContentKey** is automatically created and linked with hello asset.</span></span>
> 
> 

## <a name="contentkeytype"></a><span data-ttu-id="d3037-113">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="d3037-113">ContentKeyType</span></span>
<span data-ttu-id="d3037-114">Une des valeurs hello que vous devez définir quand créer un contenu clé est de type de clé de contenu hello.</span><span class="sxs-lookup"><span data-stu-id="d3037-114">One of hello values that you must set when create a content key is hello content key type.</span></span> <span data-ttu-id="d3037-115">Choisissez une des valeurs suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="d3037-115">Choose from one of hello following values.</span></span> 

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

## <span data-ttu-id="d3037-116"><a id="envelope_contentkey"></a>Créer une ContentKey de type enveloppe</span><span class="sxs-lookup"><span data-stu-id="d3037-116"><a id="envelope_contentkey"></a>Create envelope type ContentKey</span></span>
<span data-ttu-id="d3037-117">Hello extrait de code suivant crée une clé de contenu du type de chiffrement d’enveloppe hello.</span><span class="sxs-lookup"><span data-stu-id="d3037-117">hello following code snippet creates a content key of hello envelope encryption type.</span></span> <span data-ttu-id="d3037-118">Il associe ensuite la clé de hello avec l’élément multimédia spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="d3037-118">It then associates hello key with hello specified asset.</span></span>

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

<span data-ttu-id="d3037-119">appel</span><span class="sxs-lookup"><span data-stu-id="d3037-119">call</span></span>

    IContentKey key = CreateEnvelopeTypeContentKey(encryptedsset);



## <span data-ttu-id="d3037-120"><a id="common_contentkey"></a>Créer une ContentKey de type commun</span><span class="sxs-lookup"><span data-stu-id="d3037-120"><a id="common_contentkey"></a>Create common type ContentKey</span></span>
<span data-ttu-id="d3037-121">Hello extrait de code suivant crée une clé de contenu du type de chiffrement commun hello.</span><span class="sxs-lookup"><span data-stu-id="d3037-121">hello following code snippet creates a content key of hello common encryption type.</span></span> <span data-ttu-id="d3037-122">Il associe ensuite la clé de hello avec l’élément multimédia spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="d3037-122">It then associates hello key with hello specified asset.</span></span>

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

        // Associate hello key with hello asset.
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
<span data-ttu-id="d3037-123">appel</span><span class="sxs-lookup"><span data-stu-id="d3037-123">call</span></span>

    IContentKey key = CreateCommonTypeContentKey(encryptedsset); 


## <a name="media-services-learning-paths"></a><span data-ttu-id="d3037-124">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="d3037-124">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d3037-125">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="d3037-125">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

