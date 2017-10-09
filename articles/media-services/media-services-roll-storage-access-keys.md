---
title: "clés d’accès aaaUpdate Media Services après la restauration de stockage | Documents Microsoft"
description: "Cet article vous donne des conseils sur les clés d’accès comment tooupdate Media Services après la restauration du stockage."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a892ebb0-0ea0-4fc8-b715-60347cc5c95b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: milanga;cenkdin;juliako
ms.openlocfilehash: 26fa7a75a73397842aaebda59516a00f68ab97f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="update-media-services-after-rolling-storage-access-keys"></a>Mettre à jour Media Services après la substitution de clés d’accès de stockage

Lorsque vous créez un nouveau compte Azure Media Services (AMS), vous êtes également invité tooselect un stockage Azure qui est le compte utilisé toostore votre contenu multimédia. Vous pouvez ajouter plusieurs tooyour de comptes de stockage compte Media Services. Cette rubrique montre comment toorotate les clés de stockage. Il montre également comment les comptes de support tooa de comptes de stockage de tooadd. 

actions de hello tooperform décrites dans cette rubrique, vous devez utiliser [ARM API](https://docs.microsoft.com/rest/api/media/mediaservice) et [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).  Pour plus d’informations, consultez [comment toomanage Azure ressources avec PowerShell et le Gestionnaire de ressources](../azure-resource-manager/powershell-azure-resource-manager.md).

## <a name="overview"></a>Vue d'ensemble

Création d’un compte de stockage, Azure génère deux clés d’accès stockage 512 bits, qui sont utilisé tooauthenticate accéder au compte de stockage tooyour. tookeep vos connexions de stockage plus sécurisées, qu'il est recommandé de tooperiodically régénérer et faire pivoter votre clé d’accès. Deux clés d’accès (principaux et secondaires) sont fournies dans l’ordre tooenable vous toomaintain connexions toohello compte de stockage à l’aide d’un accès clé pendant la régénération de hello autre clé d’accès. Cette procédure est également appelée « substitution des clés d’accès ».

Media Services dépend d’une clé de stockage fournie tooit. Plus précisément, les localisateurs hello toostream utilisé ou téléchargent vos éléments multimédias dépendent de clé d’accès de stockage spécifié de hello. Lors de la création d’un compte AMS prendra une dépendance sur la clé d’accès hello stockage principal par défaut, mais en tant qu’utilisateur vous pouvez mettre à jour de clé de stockage de hello AMS a. Il se peut que vous devez vous assurer que toolet Media Services savoir quelle clé toouse en suivant les étapes décrites dans cette rubrique.  

>[!NOTE]
> Si vous possédez plusieurs comptes de stockage, vous devez effectuer cette procédure pour chacun d’eux. commande Hello dans lequel vous faire tourner les clés de stockage n’est pas fixe. Vous pouvez faire pivoter les clés secondaires hello tout d’abord et puis hello primaire clé ou vice versa.
>
> Avant d’exécuter les étapes décrites dans cette rubrique sur un compte de production, vérifiez les tootest que les sur un compte de préproduction.
>

## <a name="steps-toorotate-storage-keys"></a>Clés de stockage toorotate étapes 
 
 1. Modification hello stockage clé primaire du compte via l’applet de commande powershell hello ou [Azure](https://portal.azure.com/) portal.
 2. Appeler l’applet de commande de synchronisation-AzureRmMediaServiceStorageKeys avec params approprié tooforce media compte toopick des clés de compte de stockage
 
    Bonjour à l’exemple suivant montre comment toosync clés toostorage comptes.
  
         Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId
  
 3. Attendez environ une heure. Vérifiez l’utilisation des scénarios de diffusion en continu de hello.
 4. Modifier la clé secondaire de compte de stockage via l’applet de commande powershell hello ou le portail Azure.
 5. Appelez powershell AzureRmMediaServiceStorageKeys de synchronisation avec params approprié tooforce media compte toopick des nouvelles clés de compte de stockage. 
 6. Attendez environ une heure. Vérifiez l’utilisation des scénarios de diffusion en continu de hello.
 
### <a name="a-powershell-cmdlet-example"></a>Exemple d’applet de commande PowerShell 

Hello exemple suivant montre comment tooget hello compte de stockage et synchroniser avec un compte de hello AMS.

    $regionName = "West US"
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccountName = "skystorage"
    $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

    Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId

 
## <a name="steps-tooadd-storage-accounts-tooyour-ams-account"></a>Les comptes de stockage de tooadd étapes tooyour AMS compte

Hello rubrique suivante indique le mode de stockage de tooadd comptes tooyour AMS compte : [attacher plusieurs tooa de comptes de stockage compte Media Services](meda-services-managing-multiple-storage-accounts.md).

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a>Remerciements
Nous aimerions hello tooacknowledge suivant des personnes qui ont contribué à la création de ce document : Cenk Dingiloglu, Milan Gada, Seva Titov.
