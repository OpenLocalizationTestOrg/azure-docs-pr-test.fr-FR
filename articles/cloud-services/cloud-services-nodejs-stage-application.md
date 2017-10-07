---
title: "aaaStage un déploiement de service cloud (Node.js) | Documents Microsoft"
description: "Découvrez comment toodeploy votre tooa d’application Windows Azure mise en lots d’environnement, puis déployer tooa environnement de production à l’aide de la permutation d’adresse IP virtuelle (VIP)."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d65d26a6-b424-49cd-a88c-7ef46bb112a8
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 0656c84ac444a10f152f441265f85141347bf1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="staging-an-application-in-azure"></a>Déploiement intermédiaire d'une application dans Azure
Une application peut être déployée toohello environnement dans Azure toobe testé avant de le déplacer toohello production intermédiaire environnement dans le hello application est accessible sur Internet de hello. L’environnement intermédiaire est exactement comme environnement de production hello, sauf que vous pouvez uniquement hello d’accès intermédiaire application avec une URL masquée qui est générée par Azure. Après avoir vérifié que votre application fonctionne correctement, il peut être l’environnement de production toohello déployé en effectuant un échange d’adresse IP virtuelle (VIP).

> [!NOTE]
> Hello étapes décrites dans cet article s’appliquent uniquement les applications toonode hébergées comme un Service Cloud Azure.
> 
> 

## <a name="step-1-stage-an-application"></a>Étape 1 : déploiement intermédiaire d'une application
Cette tâche concerne la façon dont une application à l’aide de toostage hello **Microsoft Azure PowerShell**.

1. Lorsque vous publiez un service, transmettez simplement hello **-emplacement** paramètre Hello **AzureServiceProject de publication** applet de commande.
   
   ```powershell
   Publish-AzureServiceProject -Slot staging
   ```
2. Ouvrez une session sur toohello [portail Azure classic] et sélectionnez **Services de cloud computing**. Une fois le service cloud hello est créé et hello **intermédiaire** état de la colonne a été mis à jour trop**en cours d’exécution**, cliquez sur le nom du service hello.
   
   ![portail affichant un service en cours d'exécution][cloud-service]
3. Sélectionnez hello **tableau de bord**, puis sélectionnez **intermédiaire**.
   
   ![tableau de bord du service cloud][cloud-service-dashboard]
4. Notez la valeur hello Bonjour **URL du Site** droite de toohello d’entrée. nom DNS de Hello est un ID interne obscurci Azure générée.
   
    ![URL du site][cloud-service-staging-url]

Maintenant, vous pouvez vérifier que l’application de hello fonctionne correctement dans hello environnement intermédiaire à l’aide de hello URL du site de mise en lots.

## <a name="step-2-upgrade-an-application-in-production-by-swapping-vips"></a>Étape 2 : mise à niveau d'une application en production en échangeant les adresses IP virtuelles
Après avoir vérifié hello la version mise à niveau d’une application dans l’environnement intermédiaire, vous pouvez rapidement rendre disponible en production en échangeant hello des adresses IP virtuelles (VIP) des environnements intermédiaire et de production de hello.

> [!NOTE]
> Cette étape suppose que vous avez déjà déployé une application tooproduction et intermédiaire hello la version mise à niveau de l’application.
> 
> 

1. Ouvrez une session sur hello [portail Azure classic], cliquez sur **Services de cloud computing** , puis sélectionnez le nom du service hello.
2. À partir de hello **tableau de bord**, sélectionnez **intermédiaire**, puis cliquez sur **échanger** bas hello de page de hello. Hello VIP Swap la boîte de dialogue s’ouvre.
   
   ![boîte de dialogue Échange d'adresses IP virtuelles][vip-swap-dialog]
3. Passez en revue les informations de hello, puis cliquez sur **OK**. deux déploiements de Hello commencent la mise à jour comme hello déploiement commutateurs tooproduction et hello production déploiement commutateurs toostaging de mise en lots.

Vous avez un déploiement par étapes et mis à niveau un déploiement de production en échangeant les adresses IP virtuelles avec le déploiement hello intermédiaire.

## <a name="additional-resources"></a>Ressources supplémentaires
* [Comment tooDeploy une tooProduction mise à niveau de Service en échangeant les adresses IP virtuelles dans Azure]

[portail Azure classic]: http://manage.windowsazure.com
[cloud-service]: ./media/cloud-services-nodejs-stage-application/staging-cloud-service-running.png
[cloud-service-dashboard]: ./media/cloud-services-nodejs-stage-application/cloud-service-dashboard-staging.png
[cloud-service-staging-url]: ./media/cloud-services-nodejs-stage-application/cloud-service-staging-url.png
[vip-swap-dialog]: ./media/cloud-services-nodejs-stage-application/vip-swap-dialog.png
[Comment tooDeploy une tooProduction mise à niveau de Service en échangeant les adresses IP virtuelles dans Azure]: cloud-services-how-to-manage.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
