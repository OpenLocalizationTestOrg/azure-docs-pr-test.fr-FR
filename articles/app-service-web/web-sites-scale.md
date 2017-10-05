---
title: "Montée en puissance d’une application dans Azure | Microsoft Docs"
description: "Découvrez comment activer la montée en puissance d’une application dans Azure App Service pour ajouter des capacités et des fonctionnalités."
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
ms.openlocfilehash: 75ddbacbd4dd14597b786d26f0730477f6c85811
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-up-an-app-in-azure"></a><span data-ttu-id="2ebe1-103">Montée en puissance d’une application dans Azure</span><span class="sxs-lookup"><span data-stu-id="2ebe1-103">Scale up an app in Azure</span></span>
<span data-ttu-id="2ebe1-104">Cet article décrit la mise à l’échelle d’une application web dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-104">This article shows you how to scale your app in Azure App Service.</span></span> <span data-ttu-id="2ebe1-105">Il existe deux workflows de mise à l’échelle : montée en puissance et augmentation de la taille des instances. Cet article décrit le workflow de montée en puissance.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-105">There are two workflows for scaling, scale up and scale out, and this article explains the scale up workflow.</span></span>

* <span data-ttu-id="2ebe1-106">[Montée en puissance](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): bénéficiez d’un surcroît de capacité d’UC, de mémoire et d’espace disque, ainsi que de fonctionnalités supplémentaires, comme des machines virtuelles dédiées, des domaines et des certificats personnalisés, des emplacements intermédiaires, la mise à l’échelle automatique, et bien davantage.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-106">[Scale up](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Get more CPU, memory, disk space, and extra features like dedicated virtual machines (VMs), custom domains and certificates, staging slots, autoscaling, and more.</span></span> <span data-ttu-id="2ebe1-107">Pour monter en puissance en modifiant le niveau tarifaire du plan App Service auquel appartient votre application.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-107">You scale up by changing the pricing tier of the App Service plan that your app belongs to.</span></span>
* <span data-ttu-id="2ebe1-108">[Augmentation de la taille des instances](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): augmentez le nombre d’instances de machine virtuelle qui exécutent votre application.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-108">[Scale out](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Increase the number of VM instances that run your app.</span></span>
  <span data-ttu-id="2ebe1-109">Ce nombre peut atteindre 20 instances, en fonction de votre niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-109">You can scale out to as many as 20 instances, depending on your pricing tier.</span></span> <span data-ttu-id="2ebe1-110">[d’environnements App Service](../app-service/app-service-app-service-environments-readme.md) au niveau **Premium** tier will further au niveaucrease your scale-out count to 50 au niveaustances.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-110">[App Service Environments](../app-service/app-service-app-service-environments-readme.md) in **Premium** tier will further increase your scale-out count to 50 instances.</span></span> <span data-ttu-id="2ebe1-111">Pour plus d’informations sur l’augmentation de la taille des instances, voir [Mise à l’échelle manuelle ou automatique du nombre d’instances](../monitoring-and-diagnostics/insights-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="2ebe1-111">For more information about scaling out, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md).</span></span> <span data-ttu-id="2ebe1-112">Vous y trouverez comment utiliser la mise à l’échelle automatique, qui permet de mettre à l’échelle le nombre d’instances automatiquement en fonction des planifications et des règles prédéfinies.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-112">There you will find out how to use autoscaling, which is to scale instance count automatically based on predefined rules and schedules.</span></span>

<span data-ttu-id="2ebe1-113">Ces paramètres de mise à l’échelle sont applicables en quelques secondes et affectent toutes les applications de votre [plan App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2ebe1-113">The scale settings take only seconds to apply and affect all apps in your [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
<span data-ttu-id="2ebe1-114">Ils ne nécessitent pas de modifier votre code ou de redéployer votre application.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-114">They do not require you to change your code or redeploy your application.</span></span>

<span data-ttu-id="2ebe1-115">Pour plus d’informations sur la tarification et les fonctionnalités de chaque plan App Service, voir [Détails de la tarification - App Service](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="2ebe1-115">For information about the pricing and features of individual App Service plans, see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>  

> [!NOTE]
> <span data-ttu-id="2ebe1-116">Avant de changer le niveau **Gratuit** d’un plan App Service, commencez par supprimer les [limites de dépense](https://azure.microsoft.com/pricing/spending-limits/) en place pour votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-116">Before you switch an App Service plan from the **Free** tier, you must first remove the [spending limits](https://azure.microsoft.com/pricing/spending-limits/) in place for your Azure subscription.</span></span> <span data-ttu-id="2ebe1-117">Pour voir ou modifier les options de votre abonnement Microsoft Azure App Service, consultez la page [Abonnements Microsoft Azure][azuresubscriptions].</span><span class="sxs-lookup"><span data-stu-id="2ebe1-117">To view or change options for your Microsoft Azure App Service subscription, see [Microsoft Azure Subscriptions][azuresubscriptions].</span></span>
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a><span data-ttu-id="2ebe1-118">Montée en puissance de votre niveau de tarification</span><span class="sxs-lookup"><span data-stu-id="2ebe1-118">Scale up your pricing tier</span></span>
1. <span data-ttu-id="2ebe1-119">Dans votre navigateur, ouvrez le [portail Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="2ebe1-119">In your browser, open the [Azure portal][portal].</span></span>
2. <span data-ttu-id="2ebe1-120">Dans le panneau de votre application, cliquez sur **Tous les paramètres**, puis sur **Monter en puissance**.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-120">In your app's blade, click **All settings**, and then click **Scale Up**.</span></span>
   
    ![Accédez à la montée en puissance pour votre application Azure.][ChooseWHP]
3. <span data-ttu-id="2ebe1-122">Choisissez votre niveau, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-122">Choose your tier, and then click **Select**.</span></span>
   
    <span data-ttu-id="2ebe1-123">Dans l’onglet **Notifications**, la mention **RÉUSSITTE** clignote en vert une fois l’opération terminée.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-123">The **Notifications** tab will flash a green **SUCCESS** after the operation is complete.</span></span>

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a><span data-ttu-id="2ebe1-124">Mettre à l’échelle des ressources associées</span><span class="sxs-lookup"><span data-stu-id="2ebe1-124">Scale related resources</span></span>
<span data-ttu-id="2ebe1-125">Si votre application dépend d’autres services, tels que Azure SQL Database ou Azure Storage, vous pouvez également faire monter en puissance ces ressources selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-125">If your app depends on other services, such as Azure SQL Database or Azure Storage, you can also scale up those resources based on your needs.</span></span> <span data-ttu-id="2ebe1-126">Ces ressources ne sont pas mises à l’échelle avec le plan App Service et doivent être mises à l’échelle séparément.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-126">These resources are not scaled with the App Service plan and must be scaled separately.</span></span>

1. <span data-ttu-id="2ebe1-127">Dans **Essentials**, cliquez sur le lien **Groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-127">In **Essentials**, click the **Resource group** link.</span></span>
   
    ![Montée en puissance des ressources connexes de votre application Azure](./media/web-sites-scale/RGEssentialsLink.png)
2. <span data-ttu-id="2ebe1-129">Dans la partie **Résumé** du panneau **Groupe de ressources**, cliquez sur une ressource à mettre à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-129">In the **Summary** part of the **Resource group** blade, click a resource that you want to scale.</span></span> <span data-ttu-id="2ebe1-130">La capture d’écran ci-après illustre une ressource Base de données SQL et une ressource Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-130">The following screenshot shows a SQL Database resource and an Azure Storage resource.</span></span>
   
    ![Accédez au panneau du groupe de ressources pour activer la montée en puissance de votre application Azure](./media/web-sites-scale/ResourceGroup.png)
3. <span data-ttu-id="2ebe1-132">Pour une ressource Base de données SQL, cliquez sur **Paramètres** > **Niveau tarifaire** pour mettre à l’échelle le niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-132">For a SQL Database resource, click **Settings** > **Pricing tier** to scale the pricing tier.</span></span>
   
    ![Montée en puissance de la base de données SQL principale pour votre application Azure](./media/web-sites-scale/ScaleDatabase.png)
   
    <span data-ttu-id="2ebe1-134">Vous pouvez également activer la [géoréplication](../sql-database/sql-database-geo-replication-overview.md) pour votre instance de base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-134">You can also turn on [geo-replication](../sql-database/sql-database-geo-replication-overview.md) for your SQL Database instance.</span></span>
   
    <span data-ttu-id="2ebe1-135">Dans le cas d’une ressource Azure Storage, cliquez sur **Paramètres** > **Configuration** pour faire évoluer vos options de stockage.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-135">For an Azure Storage resource, click **Settings** > **Configuration** to scale up your storage options.</span></span>
   
    ![Montée en puissance du compte de stockage Azure utilisé par votre application Azure](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a><span data-ttu-id="2ebe1-137">En savoir plus sur les fonctionnalités de développement</span><span class="sxs-lookup"><span data-stu-id="2ebe1-137">Learn about developer features</span></span>
<span data-ttu-id="2ebe1-138">Selon le niveau de tarification, les fonctionnalités orientées développeur disponibles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ebe1-138">Depending on the pricing tier, the following developer-oriented features are available:</span></span>

### <a name="bitness"></a><span data-ttu-id="2ebe1-139">Nombre de bits</span><span class="sxs-lookup"><span data-stu-id="2ebe1-139">Bitness</span></span>
* <span data-ttu-id="2ebe1-140">Les modes **De base**, **Standard** et **Premium** prennent en charge les applications 64 bits et 32 bits.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-140">The **Basic**, **Standard**, and **Premium** tiers support 64-bit and 32-bit applications.</span></span>
* <span data-ttu-id="2ebe1-141">Les niveaux de plan **Gratuit** et **Partagé** prennent uniquement en charge les applications 32 bits.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-141">The **Free** and **Shared** plan tiers support 32-bit applications only.</span></span>

### <a name="debugger-support"></a><span data-ttu-id="2ebe1-142">Prise en charge du débogueur</span><span class="sxs-lookup"><span data-stu-id="2ebe1-142">Debugger support</span></span>
* <span data-ttu-id="2ebe1-143">Une prise en charge du débogueur est disponible en modes **Gratuit**, **Partagé** et **De base** pour une connexion par plan App Service.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-143">Debugger support is available for the **Free**, **Shared**, and **Basic** modes at one connection per App Service plan.</span></span>
* <span data-ttu-id="2ebe1-144">Une prise en charge du débogueur est disponible en modes **Standard** et **Premium** pour cinq connexions simultanées par plan App Service.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-144">Debugger support is available for the **Standard** and **Premium** modes at five concurrent connections per App Service plan.</span></span>

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a><span data-ttu-id="2ebe1-145">En savoir plus sur les autres fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="2ebe1-145">Learn about other features</span></span>
* <span data-ttu-id="2ebe1-146">Pour obtenir des informations détaillées sur toutes les autres fonctionnalités des plans App Service, notamment concernant la tarification et les fonctionnalités présentant de l’intérêt pour tous les utilisateurs (y compris les développeurs), consultez la page [Détails de la tarification - App Service](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="2ebe1-146">For detailed information about all of the remaining features in the App Service plans, including pricing and features of interest to all users (including developers), see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>

> [!NOTE]
> <span data-ttu-id="2ebe1-147">Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [d’essai d’App Service](https://azure.microsoft.com/try/app-service/) , qui vous permet de créer immédiatement une application web temporaire dans App Service.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-147">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/) where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="2ebe1-148">Aucune carte de crédit n’est nécessaire, et vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-148">No credit cards are required and there are no commitments.</span></span>
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a><span data-ttu-id="2ebe1-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2ebe1-149">Next steps</span></span>
* <span data-ttu-id="2ebe1-150">Pour la prise en main d'Azure, consultez la page [Version d'évaluation gratuite de Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2ebe1-150">To get started with Azure, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2ebe1-151">Pour plus d’informations sur la tarification, le support et les contrats SLA, accédez aux liens suivants.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-151">For information about pricing, support, and SLA, visit the following links.</span></span>
  
    [<span data-ttu-id="2ebe1-152">Détails de la tarification – Transferts de données</span><span class="sxs-lookup"><span data-stu-id="2ebe1-152">Data Transfers Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [<span data-ttu-id="2ebe1-153">Plans de support Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="2ebe1-153">Microsoft Azure Support Plans</span></span>](https://azure.microsoft.com/support/plans/)
  
    [<span data-ttu-id="2ebe1-154">Contrats de niveau de service</span><span class="sxs-lookup"><span data-stu-id="2ebe1-154">Service Level Agreements</span></span>](https://azure.microsoft.com/support/legal/sla/)
  
    [<span data-ttu-id="2ebe1-155">Tarification – Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="2ebe1-155">SQL Database Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/sql-database/)
  
    <span data-ttu-id="2ebe1-156">[Tailles des machines virtuelles et de Service cloud pour Microsoft Azure][vmsizes]</span><span class="sxs-lookup"><span data-stu-id="2ebe1-156">[Virtual Machine and Cloud Service Sizes for Microsoft Azure][vmsizes]</span></span>
  
    [<span data-ttu-id="2ebe1-157">Détails de la tarification – App Service</span><span class="sxs-lookup"><span data-stu-id="2ebe1-157">App Service Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/app-service/)
  
    [<span data-ttu-id="2ebe1-158">Détails de la tarification – App Service - Connexions SSL</span><span class="sxs-lookup"><span data-stu-id="2ebe1-158">App Service Pricing Details - SSL Connections</span></span>](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* <span data-ttu-id="2ebe1-159">Pour plus d’informations sur les meilleures pratiques liées à Azure App Service, notamment la création d’une architecture évolutive et résiliente, voir [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx)(Meilleures pratiques : Azure App Service Web Apps).</span><span class="sxs-lookup"><span data-stu-id="2ebe1-159">For information about Azure App Service best practices, including building a scalable and resilient architecture, see [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span></span>
* <span data-ttu-id="2ebe1-160">Pour visionner des vidéos concernant la mise à l’échelle des applications App Service, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ebe1-160">For videos about scaling App Service apps, see the following resources:</span></span>
  
  * [<span data-ttu-id="2ebe1-161">Quand mettre à l’échelle Sites Web Azure - avec Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="2ebe1-161">When to Scale Azure Websites - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [<span data-ttu-id="2ebe1-162">Mise à l’échelle automatique de Sites Web Azure, unité centrale ou planification - avec Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="2ebe1-162">Auto Scaling Azure Websites, CPU or Scheduled - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [<span data-ttu-id="2ebe1-163">Mise à l’échelle de Sites Web Azure - avec Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="2ebe1-163">How Azure Websites Scale - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

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
