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
# <a name="create-contentkeys-with-net"></a>Création de ContentKeys avec .NET
> [!div class="op_single_selector"]
> * [REST](media-services-rest-create-contentkey.md)
> * [.NET](media-services-dotnet-create-contentkey.md)
> 
> 

Media Services vous permet de toocreate et fournir les éléments multimédias chiffrés. A **ContentKey** fournit un accès sécurisé tooyour **Asset**s. 

Lorsque vous créez un nouvel élément multimédia (par exemple, avant de vous [télécharger des fichiers](media-services-dotnet-upload-files.md)), vous pouvez spécifier hello options de chiffrement suivantes : **StorageEncrypted**, **CommonEncryptionProtected**, ou **EnvelopeEncryptionProtected**. 

Lorsque vous fournissez des ressources tooyour clients, vous pouvez [configurer pour toobe actifs dynamiquement chiffré](media-services-dotnet-configure-asset-delivery-policy.md) avec l’un des hello suivant deux chiffrements : **DynamicEnvelopeEncryption** ou  **DynamicCommonEncryption**.

Les éléments multimédias chiffrés ont toobe associé **ContentKey**s. Cet article décrit comment toocreate une clé de contenu.

> [!NOTE]
> Lorsque vous créez un nouveau **StorageEncrypted** à l’aide de l’élément multimédia hello Media Services .NET SDK, hello **ContentKey** est automatiquement créé et lié à l’élément multimédia de hello.
> 
> 

## <a name="contentkeytype"></a>ContentKeyType
Une des valeurs hello que vous devez définir quand créer un contenu clé est de type de clé de contenu hello. Choisissez une des valeurs suivantes de hello. 

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

## <a id="envelope_contentkey"></a>Créer une ContentKey de type enveloppe
Hello extrait de code suivant crée une clé de contenu du type de chiffrement d’enveloppe hello. Il associe ensuite la clé de hello avec l’élément multimédia spécifié de hello.

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

appel

    IContentKey key = CreateEnvelopeTypeContentKey(encryptedsset);



## <a id="common_contentkey"></a>Créer une ContentKey de type commun
Hello extrait de code suivant crée une clé de contenu du type de chiffrement commun hello. Il associe ensuite la clé de hello avec l’élément multimédia spécifié de hello.

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
appel

    IContentKey key = CreateCommonTypeContentKey(encryptedsset); 


## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

