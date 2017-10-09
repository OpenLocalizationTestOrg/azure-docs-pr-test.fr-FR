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
# <a name="update-media-services-after-rolling-storage-access-keys"></a><span data-ttu-id="68c73-103">Mettre à jour Media Services après la substitution de clés d’accès de stockage</span><span class="sxs-lookup"><span data-stu-id="68c73-103">Update Media Services after rolling storage access keys</span></span>

<span data-ttu-id="68c73-104">Lorsque vous créez un nouveau compte Azure Media Services (AMS), vous êtes également invité tooselect un stockage Azure qui est le compte utilisé toostore votre contenu multimédia.</span><span class="sxs-lookup"><span data-stu-id="68c73-104">When you create a new Azure Media Services (AMS) account, you are also asked tooselect an Azure Storage account that is used toostore your media content.</span></span> <span data-ttu-id="68c73-105">Vous pouvez ajouter plusieurs tooyour de comptes de stockage compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="68c73-105">You can add more than one storage accounts tooyour Media Services account.</span></span> <span data-ttu-id="68c73-106">Cette rubrique montre comment toorotate les clés de stockage.</span><span class="sxs-lookup"><span data-stu-id="68c73-106">This topic shows how toorotate storage keys.</span></span> <span data-ttu-id="68c73-107">Il montre également comment les comptes de support tooa de comptes de stockage de tooadd.</span><span class="sxs-lookup"><span data-stu-id="68c73-107">It also shows how tooadd storage accounts tooa media account.</span></span> 

<span data-ttu-id="68c73-108">actions de hello tooperform décrites dans cette rubrique, vous devez utiliser [ARM API](https://docs.microsoft.com/rest/api/media/mediaservice) et [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span><span class="sxs-lookup"><span data-stu-id="68c73-108">tooperform hello actions described in this topic, you should be using [ARM APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span></span>  <span data-ttu-id="68c73-109">Pour plus d’informations, consultez [comment toomanage Azure ressources avec PowerShell et le Gestionnaire de ressources](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="68c73-109">For more information, see [How toomanage Azure resources with PowerShell and Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

## <a name="overview"></a><span data-ttu-id="68c73-110">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="68c73-110">Overview</span></span>

<span data-ttu-id="68c73-111">Création d’un compte de stockage, Azure génère deux clés d’accès stockage 512 bits, qui sont utilisé tooauthenticate accéder au compte de stockage tooyour.</span><span class="sxs-lookup"><span data-stu-id="68c73-111">When a new storage account is created, Azure generates two 512-bit storage access keys, which are used tooauthenticate access tooyour storage account.</span></span> <span data-ttu-id="68c73-112">tookeep vos connexions de stockage plus sécurisées, qu'il est recommandé de tooperiodically régénérer et faire pivoter votre clé d’accès.</span><span class="sxs-lookup"><span data-stu-id="68c73-112">tookeep your storage connections more secure, it is recommended tooperiodically regenerate and rotate your storage access key.</span></span> <span data-ttu-id="68c73-113">Deux clés d’accès (principaux et secondaires) sont fournies dans l’ordre tooenable vous toomaintain connexions toohello compte de stockage à l’aide d’un accès clé pendant la régénération de hello autre clé d’accès.</span><span class="sxs-lookup"><span data-stu-id="68c73-113">Two access keys (primary and secondary) are provided in order tooenable you toomaintain connections toohello storage account using one access key while you regenerate hello other access key.</span></span> <span data-ttu-id="68c73-114">Cette procédure est également appelée « substitution des clés d’accès ».</span><span class="sxs-lookup"><span data-stu-id="68c73-114">This procedure is also called "rolling access keys".</span></span>

<span data-ttu-id="68c73-115">Media Services dépend d’une clé de stockage fournie tooit.</span><span class="sxs-lookup"><span data-stu-id="68c73-115">Media Services depends on a storage key provided tooit.</span></span> <span data-ttu-id="68c73-116">Plus précisément, les localisateurs hello toostream utilisé ou téléchargent vos éléments multimédias dépendent de clé d’accès de stockage spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="68c73-116">Specifically, hello locators that are used toostream or download your assets depend on hello specified storage access key.</span></span> <span data-ttu-id="68c73-117">Lors de la création d’un compte AMS prendra une dépendance sur la clé d’accès hello stockage principal par défaut, mais en tant qu’utilisateur vous pouvez mettre à jour de clé de stockage de hello AMS a.</span><span class="sxs-lookup"><span data-stu-id="68c73-117">When an AMS account is created it takes a dependency on hello primary storage access key by default but as a user you can update hello storage key that AMS has.</span></span> <span data-ttu-id="68c73-118">Il se peut que vous devez vous assurer que toolet Media Services savoir quelle clé toouse en suivant les étapes décrites dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="68c73-118">You must make sure toolet Media Services know which key toouse by following steps described in this topic.</span></span>  

>[!NOTE]
> <span data-ttu-id="68c73-119">Si vous possédez plusieurs comptes de stockage, vous devez effectuer cette procédure pour chacun d’eux.</span><span class="sxs-lookup"><span data-stu-id="68c73-119">If you have multiple storage accounts, you would perform this procedure with each storage account.</span></span> <span data-ttu-id="68c73-120">commande Hello dans lequel vous faire tourner les clés de stockage n’est pas fixe.</span><span class="sxs-lookup"><span data-stu-id="68c73-120">hello order in which you rotate storage keys is not fixed.</span></span> <span data-ttu-id="68c73-121">Vous pouvez faire pivoter les clés secondaires hello tout d’abord et puis hello primaire clé ou vice versa.</span><span class="sxs-lookup"><span data-stu-id="68c73-121">You can rotate hello secondary key first and then hello primary key or vice versa.</span></span>
>
> <span data-ttu-id="68c73-122">Avant d’exécuter les étapes décrites dans cette rubrique sur un compte de production, vérifiez les tootest que les sur un compte de préproduction.</span><span class="sxs-lookup"><span data-stu-id="68c73-122">Before executing steps described in this topic on a production account, make sure tootest them on a pre-production account.</span></span>
>

## <a name="steps-toorotate-storage-keys"></a><span data-ttu-id="68c73-123">Clés de stockage toorotate étapes</span><span class="sxs-lookup"><span data-stu-id="68c73-123">Steps toorotate storage keys</span></span> 
 
 1. <span data-ttu-id="68c73-124">Modification hello stockage clé primaire du compte via l’applet de commande powershell hello ou [Azure](https://portal.azure.com/) portal.</span><span class="sxs-lookup"><span data-stu-id="68c73-124">Change hello storage account Primary key through hello powershell cmdlet or [Azure](https://portal.azure.com/) portal.</span></span>
 2. <span data-ttu-id="68c73-125">Appeler l’applet de commande de synchronisation-AzureRmMediaServiceStorageKeys avec params approprié tooforce media compte toopick des clés de compte de stockage</span><span class="sxs-lookup"><span data-stu-id="68c73-125">Call Sync-AzureRmMediaServiceStorageKeys cmdlet with appropriate params tooforce media account toopick up storage account keys</span></span>
 
    <span data-ttu-id="68c73-126">Bonjour à l’exemple suivant montre comment toosync clés toostorage comptes.</span><span class="sxs-lookup"><span data-stu-id="68c73-126">hello following example shows how toosync keys toostorage accounts.</span></span>
  
         Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId
  
 3. <span data-ttu-id="68c73-127">Attendez environ une heure.</span><span class="sxs-lookup"><span data-stu-id="68c73-127">Wait an hour or so.</span></span> <span data-ttu-id="68c73-128">Vérifiez l’utilisation des scénarios de diffusion en continu de hello.</span><span class="sxs-lookup"><span data-stu-id="68c73-128">Verify hello streaming scenarios are working.</span></span>
 4. <span data-ttu-id="68c73-129">Modifier la clé secondaire de compte de stockage via l’applet de commande powershell hello ou le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="68c73-129">Change storage account secondary key through hello powershell cmdlet or Azure portal.</span></span>
 5. <span data-ttu-id="68c73-130">Appelez powershell AzureRmMediaServiceStorageKeys de synchronisation avec params approprié tooforce media compte toopick des nouvelles clés de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="68c73-130">Call Sync-AzureRmMediaServiceStorageKeys powershell with appropriate params tooforce media account toopick up new storage account keys.</span></span> 
 6. <span data-ttu-id="68c73-131">Attendez environ une heure.</span><span class="sxs-lookup"><span data-stu-id="68c73-131">Wait an hour or so.</span></span> <span data-ttu-id="68c73-132">Vérifiez l’utilisation des scénarios de diffusion en continu de hello.</span><span class="sxs-lookup"><span data-stu-id="68c73-132">Verify hello streaming scenarios are working.</span></span>
 
### <a name="a-powershell-cmdlet-example"></a><span data-ttu-id="68c73-133">Exemple d’applet de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="68c73-133">A powershell cmdlet example</span></span> 

<span data-ttu-id="68c73-134">Hello exemple suivant montre comment tooget hello compte de stockage et synchroniser avec un compte de hello AMS.</span><span class="sxs-lookup"><span data-stu-id="68c73-134">hello following example demonstrates how tooget hello storage account and sync it with hello AMS account.</span></span>

    $regionName = "West US"
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccountName = "skystorage"
    $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

    Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId

 
## <a name="steps-tooadd-storage-accounts-tooyour-ams-account"></a><span data-ttu-id="68c73-135">Les comptes de stockage de tooadd étapes tooyour AMS compte</span><span class="sxs-lookup"><span data-stu-id="68c73-135">Steps tooadd storage accounts tooyour AMS account</span></span>

<span data-ttu-id="68c73-136">Hello rubrique suivante indique le mode de stockage de tooadd comptes tooyour AMS compte : [attacher plusieurs tooa de comptes de stockage compte Media Services](meda-services-managing-multiple-storage-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="68c73-136">hello following topic shows how tooadd storage accounts tooyour AMS account: [Attach multiple storage accounts tooa Media Services account](meda-services-managing-multiple-storage-accounts.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="68c73-137">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="68c73-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="68c73-138">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="68c73-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="68c73-139">Remerciements</span><span class="sxs-lookup"><span data-stu-id="68c73-139">Acknowledgments</span></span>
<span data-ttu-id="68c73-140">Nous aimerions hello tooacknowledge suivant des personnes qui ont contribué à la création de ce document : Cenk Dingiloglu, Milan Gada, Seva Titov.</span><span class="sxs-lookup"><span data-stu-id="68c73-140">We would like tooacknowledge hello following people who contributed towards creating this document: Cenk Dingiloglu, Milan Gada, Seva Titov.</span></span>
