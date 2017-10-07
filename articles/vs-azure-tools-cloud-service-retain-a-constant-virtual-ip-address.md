---
title: aaaHow tooretain une adresse IP virtuelle constante pour un service cloud Azure | Documents Microsoft
description: "Découvrez comment tooensure qui hello adresse IP virtuelle (VIP) de votre service cloud Azure ne change pas."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4a58e2c6-7a79-4051-8a2c-99182ff8b881
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 9e27121797ffb61517b8d2c2661ec44ff7298968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="retain-a-constant-virtual-ip-address-for-an-azure-cloud-service"></a>Conserver une adresse IP virtuelle constante pour un service cloud Azure
Lorsque vous mettez à jour un service cloud qui est hébergé dans Azure, vous devrez peut-être tooensure hello virtuel adresse (VIP) du service de hello ne change pas. De nombreux services de gestion de domaine utilisent hello système DNS (Domain Name) pour l’inscription des noms de domaine. DNS fonctionne uniquement si hello adresse IP virtuelle reste hello identiques. Vous pouvez utiliser hello **Assistant Publication** dans Windows Azure Tools tooensure qui hello l’adresse IP virtuelle de votre service cloud ne change pas quand vous mettre à jour. Pour plus d’informations sur la gestion de domaine DNS toouse services de cloud computing, consultez [configuration d’un nom de domaine personnalisé pour un service cloud Azure](cloud-services/cloud-services-custom-domain-name.md).

## <a name="publish-a-cloud-service-without-changing-its-vip"></a>Publier un service cloud sans modifier son adresse IP virtuelle
Hello adresse IP virtuelle d’un service cloud est alloué lors de son premier déploiement tooAzure dans un environnement spécifique, comme l’environnement de production hello. modifications d’adresse IP virtuelle Hello uniquement si vous supprimez le déploiement de hello explicitement ou hello déploiement est implicitement supprimé par le déploiement de hello mettre à jour le processus. tooretain hello VIP, vous ne devez pas supprimer votre déploiement, et vous devez vous assurer que Visual Studio ne supprime pas votre déploiement automatiquement. 

Vous pouvez spécifier des paramètres de déploiement Bonjour **Assistant Publication**, qui prend en charge plusieurs options de déploiement. Vous pouvez spécifier un nouveau déploiement ou une mise à jour de déploiement, qui peut être incrémentielle ou simultanée. Les deux types de déploiement de mise à jour conservent hello VIP. Pour les définitions de ces différents types de déploiement, consultez [Assistant Publication d’application Azure](vs-azure-tools-publish-azure-application-wizard.md). En outre, vous pouvez contrôler si le déploiement précédent de hello d’un service cloud est supprimée si une erreur se produit. Si vous ne définissez pas cette option correctement, hello VIP peut changer de façon inattendue.

## <a name="update-a-cloud-service-without-changing-its-vip"></a>Mettre à jour un service cloud sans modifier son adresse IP virtuelle
1. Créez ou ouvrez un projet de service cloud Azure dans Visual Studio. 

2. Dans **l’Explorateur de solutions**, projet de hello avec le bouton droit. Dans le menu contextuel de hello, sélectionnez **publier**.

    ![Publish menu](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/solution-explorer-publish-menu.png)

3. Bonjour **publier l’Application Azure** boîte de dialogue, toowhich d’abonnement Azure hello sélectionnez souhaité toodeploy. Connectez-vous si nécessaire, puis sélectionnez **Suivant**.

    ![Publication d’application Azure : page de connexion](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-signin.png)

4. Sur hello **paramètres communs** , vérifiez que le nom hello du hello cloud service toowhich vous déployez, hello **environnement**, hello **configuration de Build**et hello **Configuration du Service** sont tous corrects.

    ![Publication d’application Azure : onglet Paramètres communs](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-common-settings.png)

5. Sur hello **paramètres avancés** , vérifiez que hello **étiquette de déploiement** et hello **compte de stockage** sont corrects. Vérifiez que hello **supprimer le déploiement en cas d’échec** case à cocher est désactivée et vérifiez que hello **mise à jour de déploiement** case à cocher est activée. En désactivant le hello **supprimer le déploiement en cas d’échec** case à cocher, assurez-vous que votre adresse IP virtuelle n’est pas perdu si une erreur se produit pendant le déploiement. En sélectionnant hello **mise à jour de déploiement** case à cocher, assurez-vous que votre déploiement n’est pas supprimé et que votre adresse IP virtuelle n’est perdue lorsque vous republiez votre application. 

    ![Publication d’application Azure : onglet Paramètres avancés](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-advanced-settings.png)

6. toofurther Indiquez de quelle manière hello rôles toobe est mis à jour, sélectionnez **paramètres** suivant trop**mise à jour de déploiement**. Sélectionnez **Mise à jour incrémentielle** ou **Mise à jour simultanée** et sélectionnez **OK**. Choisissez **mise à jour incrémentielle** tooupdate chaque instance de votre application, une après l’autre, afin que hello application est toujours disponible. Choisissez **mise à jour simultanée** tooupdate toutes les instances de votre application à hello même temps. Mise à jour simultanée est plus rapide, mais votre service ne soient pas disponible pendant le processus de mise à jour hello. Quand vous avez terminé, cliquez sur **Suivant**.

    ![Publication d’application Azure : page Paramètres du déploiement](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-deployment-update-settings.png)

7. Bonjour **publier l’Application Azure** boîte de dialogue, sélectionnez **suivant** jusqu'à hello **Résumé** page s’affiche. Vérifiez vos paramètres, puis sélectionnez **Publier**.
   
    ![Publication d’application Azure : page Résumé](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-summary.png)

## <a name="next-steps"></a>Étapes suivantes
- [À l’aide de Visual Studio Assistant Publication d’Azure Application de hello](vs-azure-tools-publish-azure-application-wizard.md)

