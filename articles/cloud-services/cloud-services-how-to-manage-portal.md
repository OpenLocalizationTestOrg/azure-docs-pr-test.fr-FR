---
title: "tâches de gestion de service de cloud aaaCommon | Documents Microsoft"
description: "Découvrez comment toomanage cloud services Bonjour portail Azure. Ces exemples utilisent hello portail Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: cb218ad9-77d4-4149-83db-71159c00767e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: ade8a18a7754edbaae4903230c26c009fef63ed7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-cloud-services"></a>Comment les Services de cloud computing tooManage
> [!div class="op_single_selector"]
> * [Portail Azure](cloud-services-how-to-manage-portal.md)
> * [portail Azure Classic](cloud-services-how-to-manage.md)
>
>

Bonjour **Services Cloud (classiques)** zone Hello Azure portail, vous pouvez mettre à jour un rôle de service ou d’un déploiement, promouvoir une tooproduction de déploiement par étapes, service de cloud de tooyour de ressources de liaison afin que vous puissiez voir les ressources hello dépendances et l’échelle hello ensemble de ressources et supprimer un service cloud ou un déploiement.

Plus d’informations sur la façon dont tooscale votre service cloud est disponible [ici](cloud-services-how-to-scale-portal.md).

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a>Mise à jour d’un rôle ou d’un déploiement de service cloud
Si vous avez besoin de code de l’application hello tooupdate pour votre service cloud, utilisez **mise à jour** sur le panneau de service cloud hello. Vous pouvez mettre à jour un ou plusieurs rôles. tooupdate, vous pouvez télécharger un nouveau package de service ou d’un fichier de configuration de service.

1. Bonjour [portail Azure][Azure portal], sélectionnez hello cloud service tooupdate. Cette étape ouvre le panneau d’instance de service de cloud hello.
2. Dans le panneau de hello, cliquez sur hello **mise à jour** bouton.

    ![Bouton Update](./media/cloud-services-how-to-manage-portal/update-button.png)

3. Mettre à jour le déploiement de hello avec un nouveau fichier de package de service (.cspkg) et le fichier de configuration de service (.cscfg).

    ![UpdateDeployment](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. **Si vous le souhaitez** mettre à jour d’étiquette de déploiement hello et compte de stockage hello.
5. Si tous les rôles ont une seule instance de rôle, sélectionnez hello **déployer même si un ou plusieurs rôles contiennent une seule instance** tooproceed de mise à niveau tooenable hello.

    Azure ne peut garantir 99,95 % de disponibilité du service pendant la mise à jour du service cloud que si chaque rôle dispose d'au moins deux instances de rôle (machines virtuelles). Avec deux instances de rôle, un ordinateur virtuel traite les demandes des clients pendant la mise à jour de hello autres.

6. Vérifiez **démarrer le déploiement** toohave hello mise à jour appliquée une fois le téléchargement hello du package de hello terminée.
7. Cliquez sur **OK** toobegin hello service mises à jour.

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a>Comment : permuter les déploiements toopromote une tooproduction de déploiement par étapes
Lorsque vous décidez de toodeploy une nouvelle version d’un service cloud, étape et testez votre nouvelle version dans votre environnement intermédiaire du service cloud. Utilisez **échanger** tooswitch hello URL par le hello deux déploiements sont traitées et promouvoir une nouveau tooproduction de mise en production.

Vous pouvez permuter les déploiements de hello **Services de cloud computing** hello ou la page tableau de bord.

1. Bonjour [portail Azure][Azure portal], sélectionnez hello cloud service tooupdate. Cette étape ouvre le panneau d’instance de service de cloud hello.
2. Dans le panneau de hello, cliquez sur hello **échanger** bouton.

    ![Inverser les services cloud](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. Hello de confirmation suivant s’ouvre.

    ![Inverser les services cloud](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. Après avoir vérifié les informations relatives au déploiement hello, cliquez sur **OK** tooswap des déploiements hello.

    permutation de déploiement Hello se produit rapidement, car seul hello change est hello virtuels adresses IP (VIP) pour les déploiements de hello.

    toosave les coûts de calcul, vous pouvez supprimer hello déploiement intermédiaire après avoir vérifié que votre déploiement de production fonctionne comme prévu.

### <a name="common-questions-about-swapping-deployments"></a>Questions courantes sur l’échange de déploiements

**Quelles sont les conditions préalables de hello pour l’échange des déploiements ?**

Il existe deux conditions préalables principales pour qu’un échange de déploiements réussisse :

- Si vous souhaitez que toouse une adresse IP statique pour votre emplacement de production, vous devez réserver une pour votre emplacement de mise en lots. Sinon, échange de hello échoue.

- Toutes les instances de vos rôles doivent exécuter avant que vous pouvez effectuer hello. Vous pouvez vérifier l’état de hello de vos instances dans le panneau de vue d’ensemble de hello Hello portail Azure. Vous pouvez également utiliser hello [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) commande dans Windows PowerShell.

Notez que les mises à jour du système d’exploitation invité de déploiement peut également engendrer des opérations de réparation de service échange toofail. Pour plus d’informations, consultez [Résoudre les problèmes de déploiement de service cloud](cloud-services-troubleshoot-deployment-problems.md).

**Un échange implique-t-il un temps d’arrêt pour mon application ? Comment dois-je le gérer ?**

Comme décrit dans la dernière section de hello, une permutation de déploiement est généralement rapide, car elle est simplement une modification de configuration de l’équilibrage de charge Azure hello. Toutefois, dans certains cas, il peut prendre au moins dix secondes et entraîner des échecs de connexion temporaires. clients de tooyour toolimit impact, envisagez d’implémenter [logique de nouvelle tentative client](../best-practices-retry-general.md).

## <a name="how-to-link-a-resource-tooa-cloud-service"></a>Comment : lier un service de cloud de ressource tooa
Hello portail Azure ne contient pas de liens ressources ensemble comme portail classique Azure actuel hello. Au lieu de cela, déployer des ressources supplémentaires toohello même groupe de ressources utilisé par hello Service Cloud.

## <a name="how-to-delete-deployments-and-a-cloud-service"></a>Suppression de déploiements et d’un service cloud
Avant de pouvoir supprimer un service cloud, vous devez supprimer tous les déploiements existants.

toosave les coûts de calcul, vous pouvez supprimer hello déploiement intermédiaire après avoir vérifié que votre déploiement de production fonctionne comme prévu. Vous êtes facturé pour les coûts de calcul des instances de rôle déployées qui ont été arrêtées.

Utilisez hello suivant la procédure toodelete un déploiement ou votre service cloud.

1. Bonjour [portail Azure][Azure portal], sélectionnez hello cloud service toodelete. Cette étape ouvre le panneau d’instance de service de cloud hello.
2. Dans le panneau de hello, cliquez sur hello **supprimer** bouton.

    ![Inverser les services cloud](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. Vous pouvez supprimer le service de cloud entière hello en vérifiant **le service Cloud et ses déploiements** ou choisissez soit hello **déploiement de Production** ou hello **déploiement intermédiaire**.

    ![Inverser les services cloud](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. Cliquez sur hello **supprimer** bouton bas hello.
5. service de cloud toodelete hello, cliquez sur **supprimer le service cloud**. Ensuite, à l’invite de confirmation hello, cliquez sur **Oui**.

> [!NOTE]
> Lorsqu’un service cloud est supprimé, et la surveillance détaillée est configurée, vous devez supprimer manuellement les données de salutation à partir de votre compte de stockage. Pour savoir où toofind hello tables de métriques, consultez [cela](cloud-services-how-to-monitor.md) l’article.


## <a name="how-to-find-more-information-about-failed-deployments"></a>Comment trouver plus d’informations sur les déploiements échoués
Hello **vue d’ensemble** panneau a une barre d’état en haut de hello. Lorsque vous cliquez sur la barre de hello, un nouveau panneau s’ouvre et affiche des informations sur l’erreur. Si le déploiement de hello ne contient pas toutes les erreurs, le panneau d’informations hello est vide.

![Inverser les services cloud](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a>Étapes suivantes
* [Configuration générale de votre service cloud](cloud-services-how-to-configure-portal.md).
* Découvrez comment trop[déployer un service cloud](cloud-services-how-to-create-deploy-portal.md).
* Configurez un [nom de domaine personnalisé](cloud-services-custom-domain-name-portal.md).
* Configurez des [certificats SSL](cloud-services-configure-ssl-certificate-portal.md).
