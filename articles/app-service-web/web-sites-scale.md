---
title: aaaScale installer une application dans Azure | Documents Microsoft
description: "Découvrez comment tooscale dans Azure App Service tooadd capacité et des fonctionnalités de l’application."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: f7091b25-b2b6-48da-8d4a-dcf9b7baccab
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2016
ms.author: cephalin
ms.openlocfilehash: 97f46f77aeef95aec90d38e8396a023820e3caeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-up-an-app-in-azure"></a>Montée en puissance d’une application dans Azure
Cet article vous montre comment tooscale votre application dans Azure App Service. Il existe deux flux de travail pour la mise à l’échelle, l’échelle des et montée en puissance parallèle et cet article explique la montée en puissance hello du workflow.

* [Montée en puissance](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): bénéficiez d’un surcroît de capacité d’UC, de mémoire et d’espace disque, ainsi que de fonctionnalités supplémentaires, comme des machines virtuelles dédiées, des domaines et des certificats personnalisés, des emplacements intermédiaires, la mise à l’échelle automatique, et bien davantage. Monter en modifiant hello tarification du plan de Service d’application appartenant à votre application.
* [Montée en puissance parallèle](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): augmenter le nombre de hello d’instances de machine virtuelle qui exécutent votre application.
  Vous pouvez faire évoluer tooas comme 20 instances, selon votre niveau tarifaire. [Les environnements App Service](../app-service/app-service-app-service-environments-readme.md) dans **Premium** couche vont augmenter encore davantage vos instances de too50 du nombre de montée en puissance parallèle. Pour plus d’informations sur l’augmentation de la taille des instances, voir [Mise à l’échelle manuelle ou automatique du nombre d’instances](../monitoring-and-diagnostics/insights-how-to-scale.md). Vous y trouverez hors comment échelle toouse, qui est le nombre d’instances tooscale automatiquement en fonction des calendriers et des règles prédéfinies.

Hello échelle paramètres prennent uniquement secondes tooapply et concernent toutes les applications dans votre [plan App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
Ils ne nécessitent vous toochange votre code ou redéployer votre application.

Pour plus d’informations sur la tarification de hello et les fonctionnalités de plans de Service d’application individuels, consultez [tarification de Service d’application](https://azure.microsoft.com/pricing/details/web-sites/).  

> [!NOTE]
> Avant de basculer un plan App Service à partir de hello **libre** couche, vous devez d’abord supprimer hello [limites de dépense](https://azure.microsoft.com/pricing/spending-limits/) en place pour votre abonnement Azure. tooview ou modifier les options de votre abonnement Microsoft Azure App Service, consultez [abonnements Microsoft Azure][azuresubscriptions].
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a>Montée en puissance de votre niveau de tarification
1. Dans votre navigateur, ouvrez hello [portail Azure][portal].
2. Dans le panneau de votre application, cliquez sur **Tous les paramètres**, puis sur **Monter en puissance**.
   
    ![Accédez tooscale votre application Azure.][ChooseWHP]
3. Choisissez votre niveau, puis cliquez sur **Sélectionner**.
   
    Hello **Notifications** un vert clignote en onglet **réussite** après l’opération hello est terminée.

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a>Mettre à l’échelle des ressources associées
Si votre application dépend d’autres services, tels que Azure SQL Database ou Azure Storage, vous pouvez également faire monter en puissance ces ressources selon vos besoins. Ces ressources ne sont pas mis à l’échelle par hello plan App Service et doivent être mis à l’échelle séparément.

1. Dans **Essentials**, cliquez sur hello **groupe de ressources** lien.
   
    ![Montée en puissance des ressources connexes de votre application Azure](./media/web-sites-scale/RGEssentialsLink.png)
2. Bonjour **Résumé** dans le cadre du hello **groupe de ressources** panneau, cliquez sur une ressource que vous souhaitez tooscale. Hello suivant capture d’écran montre une ressource de base de données SQL et une ressource de stockage Azure.
   
    ![Accédez tooresource groupe panneau tooscale votre application Azure](./media/web-sites-scale/ResourceGroup.png)
3. Pour une ressource de base de données SQL, cliquez sur **paramètres** > **niveau tarifaire** hello tooscale niveau tarifaire.
   
    ![Montée en puissance principal de base de données SQL hello pour votre application Azure](./media/web-sites-scale/ScaleDatabase.png)
   
    Vous pouvez également activer la [géoréplication](../sql-database/sql-database-geo-replication-overview.md) pour votre instance de base de données SQL.
   
    Pour une ressource de stockage Azure, cliquez sur **paramètres** > **Configuration** tooscale des options de stockage.
   
    ![Montée en puissance compte de stockage Azure hello utilisé par votre application Azure](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a>En savoir plus sur les fonctionnalités de développement
Selon le niveau de tarification de hello, hello destinées aux développeurs fonctionnalités suivantes sont disponibles :

### <a name="bitness"></a>Nombre de bits
* Hello **base**, **Standard**, et **Premium** niveaux prennent en charge les applications 32 bits et 64 bits.
* Hello **libre** et **Shared** plan niveaux prennent en charge les applications 32 bits uniquement.

### <a name="debugger-support"></a>Prise en charge du débogueur
* Prise en charge du débogueur est disponible pour hello **libre**, **Shared**, et **base** modes à une seule connexion par plan App Service.
* Prise en charge du débogueur est disponible pour hello **Standard** et **Premium** modes à cinq connexions simultanées par plan App Service.

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a>En savoir plus sur les autres fonctionnalités
* Pour plus d’informations sur l’ensemble des hello restant fonctionnalités Bonjour du Service d’applications plans, y compris de prix et les caractéristiques des utilisateurs de tooall intérêt (y compris les développeurs), consultez [tarification de Service d’application](https://azure.microsoft.com/pricing/details/web-sites/).

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de vous inscrivez pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/) où vous pouvez créer une application web de courte durée de vie starter immédiatement dans le Service d’applications. Aucune carte de crédit n’est nécessaire, et vous ne prenez aucun engagement.
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a>Étapes suivantes
* tooget main d’Azure, consultez [version d’évaluation gratuite de Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/).
* Pour plus d’informations sur la tarification, prise en charge et contrat SLA, visitez hello suivant liens.
  
    [Détails de la tarification – Transferts de données](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [Plans de support Microsoft Azure](https://azure.microsoft.com/support/plans/)
  
    [Contrats de niveau de service](https://azure.microsoft.com/support/legal/sla/)
  
    [Tarification – Base de données SQL](https://azure.microsoft.com/pricing/details/sql-database/)
  
    [Tailles des machines virtuelles et de Service cloud pour Microsoft Azure][vmsizes]
  
    [Détails de la tarification – App Service](https://azure.microsoft.com/pricing/details/app-service/)
  
    [Détails de la tarification – App Service - Connexions SSL](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* Pour plus d’informations sur les meilleures pratiques liées à Azure App Service, notamment la création d’une architecture évolutive et résiliente, voir [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx)(Meilleures pratiques : Azure App Service Web Apps).
* Pour les vidéos sur la mise à l’échelle des applications de Service d’applications, consultez hello suivant des ressources :
  
  * [Lorsque des sites Web Azure - avec Stefan Schackow de tooScale](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [Mise à l’échelle automatique de Sites Web Azure, unité centrale ou planification - avec Stefan Schackow](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [Mise à l’échelle de Sites Web Azure - avec Stefan Schackow](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

<!-- LINKS -->
[vmsizes]:/pricing/details/app-service/
[SQLaccountsbilling]:http://go.microsoft.com/fwlink/?LinkId=234930
[azuresubscriptions]:http://go.microsoft.com/fwlink/?LinkID=235288
[portal]: https://portal.azure.com/

<!-- IMAGES -->
[ChooseWHP]: ./media/web-sites-scale/scale1ChooseWHP.png
[ChooseBasicInstances]: ./media/web-sites-scale/scale2InstancesBasic.png
[SaveButton]: ./media/web-sites-scale/05SaveButton.png
[BasicComplete]: ./media/web-sites-scale/06BasicComplete.png
[ScaleStandard]: ./media/web-sites-scale/scale3InstancesStandard.png
[Autoscale]: ./media/web-sites-scale/scale4AutoScale.png
[SetTargetMetrics]: ./media/web-sites-scale/scale5AutoScaleTargetMetrics.png
[SetFirstRule]: ./media/web-sites-scale/scale6AutoScaleFirstRule.png
[SetSecondRule]: ./media/web-sites-scale/scale7AutoScaleSecondRule.png
[SetThirdRule]: ./media/web-sites-scale/scale8AutoScaleThirdRule.png
[SetRulesFinal]: ./media/web-sites-scale/scale9AutoScaleFinal.png
[ResourceGroup]: ./media/web-sites-scale/scale10ResourceGroup.png
[ScaleDatabase]: ./media/web-sites-scale/scale11SQLScale.png
[GeoReplication]: ./media/web-sites-scale/scale12SQLGeoReplication.png
