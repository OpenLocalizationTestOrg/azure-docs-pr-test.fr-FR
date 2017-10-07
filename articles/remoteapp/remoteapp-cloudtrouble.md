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
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a>Résolution des problèmes de création de collections cloud RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Si vous rencontrez des problèmes de la création d’une collection de cloud, consultez hello informations suivantes.

## <a name="your-image-is-invalid"></a>Votre image n'est pas valide
Si vous voyez un message comme « GoldImageInvalid » lorsque vous attendez Azure tooprovision votre collection, cela signifie que votre image de modèle ne répond pas aux hello [défini des exigences de l’image](remoteapp-imagereqs.md). Par conséquent, accédez à lire les [exigences](remoteapp-imagereqs.md), corrigez votre image et essayez toocreate à nouveau votre collection.

## <a name="common-errors-seen-in-hello-azure-management-portal"></a>Erreurs courantes dans le portail de gestion Azure hello
    DNS server could not be reached
    ProvisioningTimeout

La création de collections cloud échoue souvent si vous utilisez des images personnalisées.  Si vous constatez l’un de hello ci-dessus erreurs et que vous utilisez une collection de hello toocreate image personnalisée, consultez hello suivant choses :

* Assurez-vous que vous avez téléchargé image personnalisée de hello répond aux exigences de l’image.
* Plus souvent des problèmes courants hello est que cette image hello n’est pas correctement préparée avec Sysprep.  
* Vérifiez image de hello peut démarrer dans Hyper-V ou essayez de créer une VM IAAS directement dans votre abonnement Azure à l’aide d’image de hello. Si hello VM échoue tooboot et ne démarre pas, cela indique généralement qu’image personnalisée hello n’a pas été préparée correctement.  Vérifiez l’image personnalisée de hello a été généré suite hello comment toocreate un modèle personnalisé de l’image pour RemoteApp

Si vous utilisez l’une des images de Microsoft hello inclus dans votre abonnement, essayez de collection de hello toocreate à nouveau. Si le problème de hello persiste puis support technique de Microsoft.

    PlatformImageTrialModeOnly

Si vous voyez cette erreur cela signifie généralement que vous été mis à niveau tooa payé compte mais que vous essayez de toouse une image fournis par Microsoft qui est valide uniquement pendant le mode d’évaluation du service de hello hello. Dans ce cas, essayez toocreate à nouveau votre collection de cloud, mais être image correcte de toospecify que hello.

