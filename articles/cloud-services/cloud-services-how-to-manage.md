---
title: "aaaCommon des tâches de gestion de service cloud (classiques) | Documents Microsoft"
description: "Découvrez comment toomanage cloud services Bonjour portail Azure classic."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 41a30e50-067c-485b-96fd-434a6d057abc
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 03b1d632f1480d0f65c87b7f8ffc747417acf7b5
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

Bonjour **Services de cloud computing** zone Hello Azure classic portail, vous pouvez mettre à jour un rôle de service ou d’un déploiement, promouvoir une tooproduction de déploiement par étapes, service de cloud de tooyour de ressources de liaison afin que vous puissiez voir les ressources hello dépendances et l’échelle hello ensemble de ressources et supprimer un service cloud ou un déploiement.

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a>Mise à jour d’un rôle ou d’un déploiement de service cloud
Si vous avez besoin de code de l’application hello tooupdate pour votre service cloud, utilisez **mise à jour** sur le tableau de bord hello, **Services de cloud computing** page, ou **Instances** page. Vous pouvez mettre à jour un ou plusieurs rôles. Vous devez tooupload un nouveau package de service et fichier de configuration de service.

1. Bonjour [portail Azure classic](https://manage.windowsazure.com/), tableau de bord de hello, **Services de cloud computing** page, ou **Instances** , cliquez sur **mise à jour**.

    ![UpdateDeployment](./media/cloud-services-how-to-manage/CloudServices_UpdateDeployment.png)

2. Dans **étiquette de déploiement**, entrez un déploiement de hello tooidentify nom (par exemple, mycloudservice4). Vous trouverez une étiquette de déploiement hello sous **démarrage rapide** sur le tableau de bord hello.
3. Dans **Package**, utilisez **Parcourir** tooupload hello service du package (.cspkg).
4. Dans **Configuration**, utilisez **Parcourir** fichier de configuration tooupload hello service (.cscfg).
5. Dans **rôle**, sélectionnez **tous les** si vous souhaitez tooupgrade tous les rôles de hello le service cloud. mettre à jour de tooperform un seul rôle, sélectionnez hello rôle de tooupdate. Même si vous sélectionnez un rôle spécifique de tooupdate, mises à jour de hello dans le fichier de configuration de service hello sont appliqués tooall rôles.
6. Si les modifications de mise à jour hello hello nombre de rôles ou de taille hello de n’importe quel rôle, sélectionnez hello **autoriser la mise à jour si des tailles de rôle ou le nombre de rôles change** tooproceed de mise à jour de case à cocher tooenable hello.

    Sachez que si vous modifiez la taille d’un rôle (autrement dit, taille de hello d’une machine virtuelle qui héberge une instance de rôle) hello ou hello du nombre de rôles, chaque instance de rôle (machine virtuelle) doit être une nouvelle image, et toutes les données locales seront perdues.

7. Si tous les rôles de service ont une seule instance de rôle, sélectionnez hello **mettre à jour même si un ou plusieurs rôles contiennent une seule instance case à cocher** tooproceed de mise à niveau tooenable hello.

    Azure ne peut garantir 99,95 % de disponibilité du service pendant la mise à jour du service cloud que si chaque rôle dispose d'au moins deux instances de rôle (machines virtuelles). Qui permet de demandes de client d’ordinateur virtuel tooprocess pendant hello autres est en cours de mise à jour.

8. Cliquez sur **OK** toobegin (coche) mise à jour de service de hello.

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a>Comment : permuter les déploiements toopromote une tooproduction de déploiement par étapes
Utilisez **échanger** toopromote un déploiement intermédiaire d’un tooproduction de service cloud. Lorsque vous décidez toodeploy une nouvelle version d’un service cloud, vous pouvez l’étape et tester votre nouvelle version dans votre environnement intermédiaire du service cloud, tandis que vos clients sont à l’aide de version actuelle de hello en production. Lorsque vous êtes prêt toopromote hello nouvelles release tooproduction, vous pouvez utiliser **échanger** URL de hello tooswitch par le hello deux déploiements.

Vous pouvez permuter les déploiements de hello **Services de cloud computing** hello ou la page tableau de bord.

1. Bonjour [portail Azure classic](https://manage.windowsazure.com/), cliquez sur **Services de cloud computing**.
2. Dans hello de services de cloud computing, cliquez sur hello cloud service tooselect il.
3. Cliquez sur **Swap**.

    Hello de confirmation suivant s’ouvre.

    ![Inverser les services cloud](./media/cloud-services-how-to-manage/CloudServices_Swap.png)

4. Après avoir vérifié les informations relatives au déploiement hello, cliquez sur **Oui** tooswap des déploiements hello.

    permutation de déploiement Hello se produit rapidement, car seul hello change est hello virtuels adresses IP (VIP) pour les déploiements de hello.

    toosave les coûts de calcul, vous pouvez supprimer le déploiement hello Bonjour environnement de test après avoir vérifié que le nouveau déploiement de production hello s’exécute comme prévu.

### <a name="common-questions-about-swapping-deployments"></a>Questions courantes sur l’échange de déploiements

**Quelles sont les conditions préalables de hello pour l’échange des déploiements ?**

Il existe deux conditions préalables principales pour qu’un échange de déploiements réussisse :

- Si vous souhaitez que toouse une adresse IP statique pour votre emplacement de production, vous devez réserver une pour votre emplacement de mise en lots. Sinon, échange de hello risque d’échouer.

- Toutes les instances de vos rôles doivent exécuter avant que vous pouvez effectuer hello. Vous pouvez vérifier le statut de hello de vos instances Bonjour portail Azure classic ou à l’aide de [hello de commande Get-AzureRole dans Windows PowerShell](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0).

Notez que les mises à jour du système d’exploitation invité et les opérations de réparation de service peuvent également engendrer toofail permutations de déploiement. Consultez [Résoudre les problèmes de déploiement de service cloud](cloud-services-troubleshoot-deployment-problems.md) pour plus de détails.

**Un échange implique-t-il un temps d’arrêt pour mon application ? Comment dois-je le gérer ?**

Comme décrit dans la dernière section de hello, une permutation de déploiement est généralement très rapide, car elle est simplement une modification de configuration de l’équilibrage de charge Azure hello. Toutefois, dans certains cas, il peut prendre au moins dix secondes et entraîner des échecs de connexion temporaires. clients de tooyour toolimit impact, envisagez d’implémenter [logique de nouvelle tentative client](../best-practices-retry-general.md).

## <a name="how-to-link-a-resource-tooa-cloud-service"></a>Comment : lier un service de cloud de ressource tooa
tooshow les dépendances de votre service cloud à d’autres ressources, vous pouvez lier une instance de la base de données SQL Azure ou un service de cloud de stockage compte toohello. Vous pouvez lier et supprimer la liaison de ressources sur hello **ressources liées** page et puis surveiller leur utilisation sur le tableau de bord hello cloud service. Si un compte de stockage lié a analyse activée, vous pouvez surveiller le nombre Total de demandes sur le tableau de bord hello cloud service.

Utilisez **lien** toolink un nouveau ou existant de la base de données SQL instance ou le stockage compte tooyour service cloud. Vous pouvez faire ensuite évoluer de la base de données hello en même temps que le rôle du service cloud hello qui l’utilise sur hello **échelle** page. (Le compte de stockage s'étend automatiquement avec l'augmentation de l'utilisation.) Pour plus d’informations, consultez [comment tooScale un Service Cloud et les ressources liées](cloud-services-how-to-scale.md).

Vous également pouvez surveiller, gérer et l’échelle de la base de données hello en hello **bases de données** nœud Hello portail Azure classic.

« Liaison » d’une ressource en ce sens ne connecte pas la ressource de toohello de votre application. Si vous créez une nouvelle base de données à l’aide **lien**, vous aurez besoin de code d’application de connexion chaînes tooyour tooadd hello et service de cloud computing hello puis mise à niveau. Vous aurez également besoin des chaînes de connexion tooadd si votre application utilise des ressources dans un compte de stockage.

Hello procédure décrit comment toolink une nouvelle instance de base de données SQL, déployé sur un nouveau serveur de base de données SQL, service de cloud computing tooa.

### <a name="toolink-a-sql-database-instance-tooa-cloud-service"></a>toolink un service de cloud de base de données SQL instance tooa
1. Bonjour [portail Azure classic](http://manage.windowsazure.com/), cliquez sur **Services de cloud computing**. Ensuite, cliquez sur nom hello hello cloud service tooopen hello du tableau de bord.
2. Cliquez sur **Linked Resources**.

    Hello **ressources liées** ouvrir la page.

    ![LinkedResourcesPage](./media/cloud-services-how-to-manage/CloudServices_LinkedResourcesPage.png)

3. Cliquez sur **Lier une ressource** ou sur **Lier**.

    Hello **lier une ressource** Assistant démarre.

    ![Link Page1](./media/cloud-services-how-to-manage/CloudServices_LinkedResources_LinkPage1.png)

4. Cliquez sur **Créer une ressource** ou **Lier une ressource existante**.
5. Choisissez le type hello de ressource toolink. Bonjour [portail Azure classic](http://manage.windowsazure.com/), cliquez sur **base de données SQL**. (Uniquement hello portail Azure classic prend en charge la liaison d’un service de cloud de stockage compte tooa.)
6. configuration de base de données toocomplete hello, suivez les instructions dans l’aide de hello **bases de données SQL** zone Hello portail Azure classic.

    Vous pouvez suivre la progression hello Hello liaison d’opération dans la zone de message hello.

    Lors de la liaison est terminée, vous pouvez surveiller l’état hello de ressource hello lié sur le tableau de bord hello cloud service. Pour plus d’informations sur la mise à l’échelle d’une base de données SQL liée, consultez [comment tooScale un Service Cloud et les ressources liées](cloud-services-how-to-scale.md).

### <a name="toounlink-a-linked-resource"></a>toounlink une ressource liée
1. Bonjour [portail Azure classic](http://manage.windowsazure.com/), cliquez sur **Services de cloud computing**. Ensuite, cliquez sur nom hello hello cloud service tooopen hello du tableau de bord.
2. Cliquez sur **ressources liées**, puis sélectionnez les ressources hello.
3. Cliquez sur **Unlink**. Puis cliquez sur **Oui** à l’invite de confirmation hello.

    Dissociation d’une base de données SQL n’a aucun effet sur la base de données hello ou l’application hello connexions toohello. Vous pouvez toujours gérer la base de données hello Bonjour **bases de données SQL** zone Hello portail Azure classic.

## <a name="how-to-delete-deployments-and-a-cloud-service"></a>Suppression de déploiements et d’un service cloud
Avant de pouvoir supprimer un service cloud, vous devez supprimer tous les déploiements existants.

toosave les coûts de calcul, vous pouvez supprimer votre déploiement intermédiaire après avoir vérifié que votre déploiement de production fonctionne comme prévu. Les coûts de calcul vous seront facturés pour les instances de rôle, même si le service cloud ne s'exécute pas.

Utilisez hello suivant la procédure toodelete un déploiement ou votre service cloud.

1. Bonjour [portail Azure classic](http://manage.windowsazure.com/), cliquez sur **Services de cloud computing**.
2. Sélectionnez le service de cloud computing hello, puis cliquez sur **supprimer**. (tooselect un service cloud sans ouvrir le tableau de bord hello, cliquez n’importe où à l’exception du nom hello dans l’entrée du service cloud hello.)

    Si vous avez un déploiement de production ou intermédiaire, vous verrez un menu de toohello similaire de choix suivant un bas hello de fenêtre hello. Avant de pouvoir supprimer le service cloud hello, vous devez supprimer tous les déploiements existants.

    ![Menu Delete](./media/cloud-services-how-to-manage/CloudServices_DeleteMenu.png)

3. toodelete un déploiement, cliquez sur **supprimer le déploiement de production** ou **supprimer le déploiement intermédiaire**. Ensuite, à l’invite de confirmation hello, cliquez sur **Oui**.
4. Si vous envisagez de service de cloud toodelete hello, répétez l’étape 3, si nécessaire, toodelete votre autre déploiement.
5. service de cloud toodelete hello, cliquez sur **supprimer le service cloud**. Ensuite, à l’invite de confirmation hello, cliquez sur **Oui**.

> [!NOTE]
> Si la surveillance détaillée est configurée pour votre service cloud, Azure ne supprime pas hello analyse les données à partir de votre compte de stockage lorsque vous supprimez le service de cloud computing hello. Vous devez manuellement les données de salutation toodelete. Pour savoir où toofind hello tables de métriques, consultez « Comment : accéder aux données de surveillance détaillées à l’extérieur de hello portail Azure classic » dans [comment les Services de cloud computing tooMonitor](cloud-services-how-to-monitor.md).
>
>

## <a name="next-steps"></a>Étapes suivantes
* [Configuration générale de votre service cloud](cloud-services-how-to-configure.md).
* Découvrez comment trop[déployer un service cloud](cloud-services-how-to-create-deploy.md).
* Configurez un [nom de domaine personnalisé](cloud-services-custom-domain-name.md).
* Configurez des [certificats SSL](cloud-services-configure-ssl-certificate.md).
