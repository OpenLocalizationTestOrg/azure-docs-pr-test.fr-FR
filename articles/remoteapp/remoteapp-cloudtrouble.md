---
title: "collections de cloud de RemoteApp aaaTroubleshoot - création | Documents Microsoft"
description: "En savoir plus les échecs de création de collection de cloud tootroubleshoot RemoteApp"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: 95eb7797-7b5e-4781-ad23-f15dd85b213d
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 9484ecbdb048ede8df725215b313e049cc7648f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a><span data-ttu-id="c6428-103">Résolution des problèmes de création de collections cloud RemoteApp</span><span class="sxs-lookup"><span data-stu-id="c6428-103">Troubleshoot creating RemoteApp cloud collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c6428-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="c6428-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="c6428-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="c6428-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="c6428-106">Si vous rencontrez des problèmes de la création d’une collection de cloud, consultez hello informations suivantes.</span><span class="sxs-lookup"><span data-stu-id="c6428-106">If you are having problems creating a cloud collection, check out hello following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="c6428-107">Votre image n'est pas valide</span><span class="sxs-lookup"><span data-stu-id="c6428-107">Your image is invalid</span></span>
<span data-ttu-id="c6428-108">Si vous voyez un message comme « GoldImageInvalid » lorsque vous attendez Azure tooprovision votre collection, cela signifie que votre image de modèle ne répond pas aux hello [défini des exigences de l’image](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="c6428-108">If you see a message like, "GoldImageInvalid" when you are waiting for Azure tooprovision your collection, it means that your template image doesn't meet hello [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="c6428-109">Par conséquent, accédez à lire les [exigences](remoteapp-imagereqs.md), corrigez votre image et essayez toocreate à nouveau votre collection.</span><span class="sxs-lookup"><span data-stu-id="c6428-109">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try toocreate your collection again.</span></span>

## <a name="common-errors-seen-in-hello-azure-management-portal"></a><span data-ttu-id="c6428-110">Erreurs courantes dans le portail de gestion Azure hello</span><span class="sxs-lookup"><span data-stu-id="c6428-110">Common errors seen in hello Azure Management portal</span></span>
    DNS server could not be reached
    ProvisioningTimeout

<span data-ttu-id="c6428-111">La création de collections cloud échoue souvent si vous utilisez des images personnalisées.</span><span class="sxs-lookup"><span data-stu-id="c6428-111">Cloud collections often fail during creation because of you are using custom images.</span></span>  <span data-ttu-id="c6428-112">Si vous constatez l’un de hello ci-dessus erreurs et que vous utilisez une collection de hello toocreate image personnalisée, consultez hello suivant choses :</span><span class="sxs-lookup"><span data-stu-id="c6428-112">If you see one of hello above errors and you are using a custom image toocreate hello collection, please check hello following things:</span></span>

* <span data-ttu-id="c6428-113">Assurez-vous que vous avez téléchargé image personnalisée de hello répond aux exigences de l’image.</span><span class="sxs-lookup"><span data-stu-id="c6428-113">Ensure that hello custom image you uploaded meets image requirements.</span></span>
* <span data-ttu-id="c6428-114">Plus souvent des problèmes courants hello est que cette image hello n’est pas correctement préparée avec Sysprep.</span><span class="sxs-lookup"><span data-stu-id="c6428-114">Most often hello common problem is that hello image was not properly syspreped.</span></span>  
* <span data-ttu-id="c6428-115">Vérifiez image de hello peut démarrer dans Hyper-V ou essayez de créer une VM IAAS directement dans votre abonnement Azure à l’aide d’image de hello.</span><span class="sxs-lookup"><span data-stu-id="c6428-115">Verify hello image can boot within Hyper-V or try creating an IAAS VM directly in your Azure subscription using hello image.</span></span> <span data-ttu-id="c6428-116">Si hello VM échoue tooboot et ne démarre pas, cela indique généralement qu’image personnalisée hello n’a pas été préparée correctement.</span><span class="sxs-lookup"><span data-stu-id="c6428-116">If hello VM fails tooboot and not start, then this usually indicates that hello custom image was not prepared correctly.</span></span>  <span data-ttu-id="c6428-117">Vérifiez l’image personnalisée de hello a été généré suite hello comment toocreate un modèle personnalisé de l’image pour RemoteApp</span><span class="sxs-lookup"><span data-stu-id="c6428-117">Verify hello custom image was built following hello How toocreate a custom template image for RemoteApp</span></span>

<span data-ttu-id="c6428-118">Si vous utilisez l’une des images de Microsoft hello inclus dans votre abonnement, essayez de collection de hello toocreate à nouveau.</span><span class="sxs-lookup"><span data-stu-id="c6428-118">If you are using one of hello Microsoft images included with your subscription, try toocreate hello collection again.</span></span> <span data-ttu-id="c6428-119">Si le problème de hello persiste puis support technique de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c6428-119">If hello issue persists then please contact Microsoft support.</span></span>

    PlatformImageTrialModeOnly

<span data-ttu-id="c6428-120">Si vous voyez cette erreur cela signifie généralement que vous été mis à niveau tooa payé compte mais que vous essayez de toouse une image fournis par Microsoft qui est valide uniquement pendant le mode d’évaluation du service de hello hello.</span><span class="sxs-lookup"><span data-stu-id="c6428-120">If you see this error this usually means that you been upgraded tooa paid account but you are trying toouse a Microsoft provided image that is valid only during hello trial mode of hello service.</span></span> <span data-ttu-id="c6428-121">Dans ce cas, essayez toocreate à nouveau votre collection de cloud, mais être image correcte de toospecify que hello.</span><span class="sxs-lookup"><span data-stu-id="c6428-121">In this case, try toocreate your cloud collection again, but be sure toospecify hello correct image.</span></span>

