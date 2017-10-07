---
title: aaaCreate un compte Azure Media Services avec hello portail Azure | Documents Microsoft
description: "Ce didacticiel vous guide tout au long des étapes de hello de création d’un compte Azure Media Services avec hello portail Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: c551e158-aad6-47b4-931e-b46260b3ee4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: juliako
ms.openlocfilehash: fdad93d5d470fc08380670ec0f6c2d33468b1492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-media-services-account-using-hello-azure-portal"></a>Créer un compte Azure Media Services à l’aide de hello portail Azure
> [!div class="op_single_selector"]
> * [Portail](media-services-portal-create-account.md)
> * [PowerShell](media-services-manage-with-powershell.md)
> * [REST](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> toocomplete ce didacticiel, vous avez besoin d’un compte Azure. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

Hello portail Azure fournit un moyen tooquickly créer un compte Azure Media Services (AMS). Vous pouvez utiliser votre tooaccess compte Media Services qui vous toostore, chiffrer, Encoder, gérer et diffuser du contenu multimédia dans Azure. Au moment de hello vous créez un compte Media Services, vous également créer un compte de stockage associé (ou utilisez-en un existant) Bonjour même zone géographique que hello compte Media Services.

Cet article explique certains concepts courantes et montre comment toocreate un Media Services compte avec hello portail Azure.

## <a name="concepts"></a>Concepts
L'accès à Media Services requiert deux comptes associés :

* Un compte Media Services. Votre compte vous donne accès ensemble tooa de Media Services cloud qui sont disponibles dans Azure. Un compte Media Services ne stocke pas de contenu multimédia à proprement parler. Au lieu de cela, il stocke les métadonnées sur le contenu multimédia de hello et les travaux de traitement multimédia dans votre compte. Au moment de hello que créer de compte de hello, vous sélectionnez une région de Media Services disponibles. vous sélectionnez la région Hello est un centre de données qui stocke les enregistrements de métadonnées hello pour votre compte.
  
* Un compte de stockage Azure. Comptes de stockage doivent se trouver dans hello même zone géographique que hello compte Media Services. Lorsque vous créez un compte Media Services, vous pouvez choisir un compte de stockage existant dans hello même région, ou vous pouvez créer un nouveau compte de stockage dans hello même région. Si vous supprimez un compte Media Services, les objets BLOB de hello dans votre compte de stockage associées ne sont pas supprimés.

> [!NOTE]
> Pour plus d’informations sur la disponibilité des fonctionnalités Azure Media Services dans des régions différentes, consultez la [disponibilité des fonctionnalités AMS entre les centres de données](scenarios-and-availability.md#availability).

## <a name="create-an-ams-account"></a>Création d’un compte AMS
étapes Hello dans cette section indiquent comment toocreate un AMS compte.

1. Connectez-vous à l’adresse hello [portail Azure](https://portal.azure.com/).
2. Cliquez sur **+Nouveau** > **Web + Mobile** > **Media Services**.
   
    ![Media Services Créer](./media/media-services-create-account/media-services-new1.png)
3. Dans **CREATE MEDIA SERVICES ACCOUNT** (CRÉER UN COMPTE MEDIA SERVICES), entrez les valeurs requises.
   
    ![Media Services Créer](./media/media-services-create-account/media-services-new3.png)
   
   1. Dans **nom de compte**, entrez le nom hello du nouveau compte de AMS hello. Un nom de compte Media Services est toutes les lettres minuscules ou chiffres sans espaces et est de 3 caractères too24.
   2. Abonnement, sélectionner les hello différents abonnements Azure que vous avez accès.
   3. Dans **groupe de ressources**, sélectionnez hello ressources nouvelles ou existantes.  Un groupe de ressources désigne une collection de ressources qui partagent un cycle de vie, des autorisations et des stratégies. En savoir plus [ici](../azure-resource-manager/resource-group-overview.md#resource-groups).
   4. Dans **emplacement**, sélectionnez hello région géographique qui sera utilisé toostore hello supports et des métadonnées enregistrements pour votre compte Media Services. Cette région sera utilisé tooprocess et diffuser vos contenus multimédias. Uniquement hello Media Services régions disponibles s’affichent dans la zone de liste déroulante hello. 
   5. Dans **compte de stockage**, sélectionnez un stockage d’objets blob de tooprovide de compte de stockage hello du contenu du média à partir de votre compte Media Services. Vous pouvez sélectionner un compte de stockage existant dans hello même zone géographique que votre compte Media Services, ou vous pouvez créer un compte de stockage. Un compte de stockage est créé dans hello même région. règles Hello pour le compte de stockage sont des noms hello même que pour les comptes Media Services.
      
       Pour en savoir plus sur le stockage, cliquez [ici](../storage/common/storage-introduction.md).
   6. Sélectionnez **toodashboard du code confidentiel** progression de hello toosee du déploiement de compte hello.
4. Cliquez sur **créer** bas hello sous forme de hello.
   
    Une fois que le compte de hello est créé avec succès, le chargement de la page Vue d’ensemble. Bonjour compte de hello de table de point de terminaison de diffusion en continu aura une valeur par défaut de diffusion en continu de point de terminaison dans hello **arrêté** état. 

    >[!NOTE]
    >Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état. toostart de diffusion en continu de votre contenu et profitez de l’empaquetage dynamique et chiffrement dynamique, hello de point de terminaison de diffusion en continu à partir de laquelle vous souhaitez que le contenu toostream a toobe Bonjour **en cours d’exécution** état. 
   
## <a name="toomanage-your-ams-account"></a>toomanage votre compte AMS

toomanage votre compte AMS (par exemple, connecter toohello AMS API par programme, télécharger des vidéos, Encoder actifs, configurer la protection du contenu, surveiller la progression du travail) sélectionnez **paramètres** sur hello gauche du portail de hello. À partir de hello **paramètres**, accédez tooone de panneaux de disposition hello (par exemple : **l’accès aux API**, **actifs**, **travaux**, **Protection du contenu**).


## <a name="next-steps"></a>Étapes suivantes

Vous pouvez maintenant télécharger des fichiers dans votre compte AMS. Pour plus d’informations, consultez la section [Téléchargement de fichiers dans un compte Media Services à l’aide du portail Azure](media-services-portal-upload-files.md).

Si vous prévoyez tooaccess AMS API par programme, consultez [hello accès API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

