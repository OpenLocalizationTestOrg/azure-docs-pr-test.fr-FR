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
# <a name="scale-up-an-app-in-azure"></a><span data-ttu-id="de883-103">Montée en puissance d’une application dans Azure</span><span class="sxs-lookup"><span data-stu-id="de883-103">Scale up an app in Azure</span></span>
<span data-ttu-id="de883-104">Cet article vous montre comment tooscale votre application dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="de883-104">This article shows you how tooscale your app in Azure App Service.</span></span> <span data-ttu-id="de883-105">Il existe deux flux de travail pour la mise à l’échelle, l’échelle des et montée en puissance parallèle et cet article explique la montée en puissance hello du workflow.</span><span class="sxs-lookup"><span data-stu-id="de883-105">There are two workflows for scaling, scale up and scale out, and this article explains hello scale up workflow.</span></span>

* <span data-ttu-id="de883-106">[Montée en puissance](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): bénéficiez d’un surcroît de capacité d’UC, de mémoire et d’espace disque, ainsi que de fonctionnalités supplémentaires, comme des machines virtuelles dédiées, des domaines et des certificats personnalisés, des emplacements intermédiaires, la mise à l’échelle automatique, et bien davantage.</span><span class="sxs-lookup"><span data-stu-id="de883-106">[Scale up](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Get more CPU, memory, disk space, and extra features like dedicated virtual machines (VMs), custom domains and certificates, staging slots, autoscaling, and more.</span></span> <span data-ttu-id="de883-107">Monter en modifiant hello tarification du plan de Service d’application appartenant à votre application.</span><span class="sxs-lookup"><span data-stu-id="de883-107">You scale up by changing hello pricing tier of the App Service plan that your app belongs to.</span></span>
* <span data-ttu-id="de883-108">[Montée en puissance parallèle](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): augmenter le nombre de hello d’instances de machine virtuelle qui exécutent votre application.</span><span class="sxs-lookup"><span data-stu-id="de883-108">[Scale out](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Increase hello number of VM instances that run your app.</span></span>
  <span data-ttu-id="de883-109">Vous pouvez faire évoluer tooas comme 20 instances, selon votre niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="de883-109">You can scale out tooas many as 20 instances, depending on your pricing tier.</span></span> <span data-ttu-id="de883-110">[Les environnements App Service](../app-service/app-service-app-service-environments-readme.md) dans **Premium** couche vont augmenter encore davantage vos instances de too50 du nombre de montée en puissance parallèle.</span><span class="sxs-lookup"><span data-stu-id="de883-110">[App Service Environments](../app-service/app-service-app-service-environments-readme.md) in **Premium** tier will further increase your scale-out count too50 instances.</span></span> <span data-ttu-id="de883-111">Pour plus d’informations sur l’augmentation de la taille des instances, voir [Mise à l’échelle manuelle ou automatique du nombre d’instances](../monitoring-and-diagnostics/insights-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="de883-111">For more information about scaling out, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md).</span></span> <span data-ttu-id="de883-112">Vous y trouverez hors comment échelle toouse, qui est le nombre d’instances tooscale automatiquement en fonction des calendriers et des règles prédéfinies.</span><span class="sxs-lookup"><span data-stu-id="de883-112">There you will find out how toouse autoscaling, which is tooscale instance count automatically based on predefined rules and schedules.</span></span>

<span data-ttu-id="de883-113">Hello échelle paramètres prennent uniquement secondes tooapply et concernent toutes les applications dans votre [plan App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="de883-113">hello scale settings take only seconds tooapply and affect all apps in your [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
<span data-ttu-id="de883-114">Ils ne nécessitent vous toochange votre code ou redéployer votre application.</span><span class="sxs-lookup"><span data-stu-id="de883-114">They do not require you toochange your code or redeploy your application.</span></span>

<span data-ttu-id="de883-115">Pour plus d’informations sur la tarification de hello et les fonctionnalités de plans de Service d’application individuels, consultez [tarification de Service d’application](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="de883-115">For information about hello pricing and features of individual App Service plans, see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>  

> [!NOTE]
> <span data-ttu-id="de883-116">Avant de basculer un plan App Service à partir de hello **libre** couche, vous devez d’abord supprimer hello [limites de dépense](https://azure.microsoft.com/pricing/spending-limits/) en place pour votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="de883-116">Before you switch an App Service plan from hello **Free** tier, you must first remove hello [spending limits](https://azure.microsoft.com/pricing/spending-limits/) in place for your Azure subscription.</span></span> <span data-ttu-id="de883-117">tooview ou modifier les options de votre abonnement Microsoft Azure App Service, consultez [abonnements Microsoft Azure][azuresubscriptions].</span><span class="sxs-lookup"><span data-stu-id="de883-117">tooview or change options for your Microsoft Azure App Service subscription, see [Microsoft Azure Subscriptions][azuresubscriptions].</span></span>
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a><span data-ttu-id="de883-118">Montée en puissance de votre niveau de tarification</span><span class="sxs-lookup"><span data-stu-id="de883-118">Scale up your pricing tier</span></span>
1. <span data-ttu-id="de883-119">Dans votre navigateur, ouvrez hello [portail Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="de883-119">In your browser, open hello [Azure portal][portal].</span></span>
2. <span data-ttu-id="de883-120">Dans le panneau de votre application, cliquez sur **Tous les paramètres**, puis sur **Monter en puissance**.</span><span class="sxs-lookup"><span data-stu-id="de883-120">In your app's blade, click **All settings**, and then click **Scale Up**.</span></span>
   
    ![Accédez tooscale votre application Azure.][ChooseWHP]
3. <span data-ttu-id="de883-122">Choisissez votre niveau, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="de883-122">Choose your tier, and then click **Select**.</span></span>
   
    <span data-ttu-id="de883-123">Hello **Notifications** un vert clignote en onglet **réussite** après l’opération hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="de883-123">hello **Notifications** tab will flash a green **SUCCESS** after hello operation is complete.</span></span>

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a><span data-ttu-id="de883-124">Mettre à l’échelle des ressources associées</span><span class="sxs-lookup"><span data-stu-id="de883-124">Scale related resources</span></span>
<span data-ttu-id="de883-125">Si votre application dépend d’autres services, tels que Azure SQL Database ou Azure Storage, vous pouvez également faire monter en puissance ces ressources selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="de883-125">If your app depends on other services, such as Azure SQL Database or Azure Storage, you can also scale up those resources based on your needs.</span></span> <span data-ttu-id="de883-126">Ces ressources ne sont pas mis à l’échelle par hello plan App Service et doivent être mis à l’échelle séparément.</span><span class="sxs-lookup"><span data-stu-id="de883-126">These resources are not scaled with hello App Service plan and must be scaled separately.</span></span>

1. <span data-ttu-id="de883-127">Dans **Essentials**, cliquez sur hello **groupe de ressources** lien.</span><span class="sxs-lookup"><span data-stu-id="de883-127">In **Essentials**, click hello **Resource group** link.</span></span>
   
    ![Montée en puissance des ressources connexes de votre application Azure](./media/web-sites-scale/RGEssentialsLink.png)
2. <span data-ttu-id="de883-129">Bonjour **Résumé** dans le cadre du hello **groupe de ressources** panneau, cliquez sur une ressource que vous souhaitez tooscale.</span><span class="sxs-lookup"><span data-stu-id="de883-129">In hello **Summary** part of hello **Resource group** blade, click a resource that you want tooscale.</span></span> <span data-ttu-id="de883-130">Hello suivant capture d’écran montre une ressource de base de données SQL et une ressource de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="de883-130">hello following screenshot shows a SQL Database resource and an Azure Storage resource.</span></span>
   
    ![Accédez tooresource groupe panneau tooscale votre application Azure](./media/web-sites-scale/ResourceGroup.png)
3. <span data-ttu-id="de883-132">Pour une ressource de base de données SQL, cliquez sur **paramètres** > **niveau tarifaire** hello tooscale niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="de883-132">For a SQL Database resource, click **Settings** > **Pricing tier** tooscale hello pricing tier.</span></span>
   
    ![Montée en puissance principal de base de données SQL hello pour votre application Azure](./media/web-sites-scale/ScaleDatabase.png)
   
    <span data-ttu-id="de883-134">Vous pouvez également activer la [géoréplication](../sql-database/sql-database-geo-replication-overview.md) pour votre instance de base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="de883-134">You can also turn on [geo-replication](../sql-database/sql-database-geo-replication-overview.md) for your SQL Database instance.</span></span>
   
    <span data-ttu-id="de883-135">Pour une ressource de stockage Azure, cliquez sur **paramètres** > **Configuration** tooscale des options de stockage.</span><span class="sxs-lookup"><span data-stu-id="de883-135">For an Azure Storage resource, click **Settings** > **Configuration** tooscale up your storage options.</span></span>
   
    ![Montée en puissance compte de stockage Azure hello utilisé par votre application Azure](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a><span data-ttu-id="de883-137">En savoir plus sur les fonctionnalités de développement</span><span class="sxs-lookup"><span data-stu-id="de883-137">Learn about developer features</span></span>
<span data-ttu-id="de883-138">Selon le niveau de tarification de hello, hello destinées aux développeurs fonctionnalités suivantes sont disponibles :</span><span class="sxs-lookup"><span data-stu-id="de883-138">Depending on hello pricing tier, hello following developer-oriented features are available:</span></span>

### <a name="bitness"></a><span data-ttu-id="de883-139">Nombre de bits</span><span class="sxs-lookup"><span data-stu-id="de883-139">Bitness</span></span>
* <span data-ttu-id="de883-140">Hello **base**, **Standard**, et **Premium** niveaux prennent en charge les applications 32 bits et 64 bits.</span><span class="sxs-lookup"><span data-stu-id="de883-140">hello **Basic**, **Standard**, and **Premium** tiers support 64-bit and 32-bit applications.</span></span>
* <span data-ttu-id="de883-141">Hello **libre** et **Shared** plan niveaux prennent en charge les applications 32 bits uniquement.</span><span class="sxs-lookup"><span data-stu-id="de883-141">hello **Free** and **Shared** plan tiers support 32-bit applications only.</span></span>

### <a name="debugger-support"></a><span data-ttu-id="de883-142">Prise en charge du débogueur</span><span class="sxs-lookup"><span data-stu-id="de883-142">Debugger support</span></span>
* <span data-ttu-id="de883-143">Prise en charge du débogueur est disponible pour hello **libre**, **Shared**, et **base** modes à une seule connexion par plan App Service.</span><span class="sxs-lookup"><span data-stu-id="de883-143">Debugger support is available for hello **Free**, **Shared**, and **Basic** modes at one connection per App Service plan.</span></span>
* <span data-ttu-id="de883-144">Prise en charge du débogueur est disponible pour hello **Standard** et **Premium** modes à cinq connexions simultanées par plan App Service.</span><span class="sxs-lookup"><span data-stu-id="de883-144">Debugger support is available for hello **Standard** and **Premium** modes at five concurrent connections per App Service plan.</span></span>

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a><span data-ttu-id="de883-145">En savoir plus sur les autres fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="de883-145">Learn about other features</span></span>
* <span data-ttu-id="de883-146">Pour plus d’informations sur l’ensemble des hello restant fonctionnalités Bonjour du Service d’applications plans, y compris de prix et les caractéristiques des utilisateurs de tooall intérêt (y compris les développeurs), consultez [tarification de Service d’application](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="de883-146">For detailed information about all of hello remaining features in hello App Service plans, including pricing and features of interest tooall users (including developers), see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>

> [!NOTE]
> <span data-ttu-id="de883-147">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de vous inscrivez pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/) où vous pouvez créer une application web de courte durée de vie starter immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="de883-147">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/) where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="de883-148">Aucune carte de crédit n’est nécessaire, et vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="de883-148">No credit cards are required and there are no commitments.</span></span>
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a><span data-ttu-id="de883-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="de883-149">Next steps</span></span>
* <span data-ttu-id="de883-150">tooget main d’Azure, consultez [version d’évaluation gratuite de Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="de883-150">tooget started with Azure, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="de883-151">Pour plus d’informations sur la tarification, prise en charge et contrat SLA, visitez hello suivant liens.</span><span class="sxs-lookup"><span data-stu-id="de883-151">For information about pricing, support, and SLA, visit hello following links.</span></span>
  
    [<span data-ttu-id="de883-152">Détails de la tarification – Transferts de données</span><span class="sxs-lookup"><span data-stu-id="de883-152">Data Transfers Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [<span data-ttu-id="de883-153">Plans de support Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="de883-153">Microsoft Azure Support Plans</span></span>](https://azure.microsoft.com/support/plans/)
  
    [<span data-ttu-id="de883-154">Contrats de niveau de service</span><span class="sxs-lookup"><span data-stu-id="de883-154">Service Level Agreements</span></span>](https://azure.microsoft.com/support/legal/sla/)
  
    [<span data-ttu-id="de883-155">Tarification – Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="de883-155">SQL Database Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/sql-database/)
  
    <span data-ttu-id="de883-156">[Tailles des machines virtuelles et de Service cloud pour Microsoft Azure][vmsizes]</span><span class="sxs-lookup"><span data-stu-id="de883-156">[Virtual Machine and Cloud Service Sizes for Microsoft Azure][vmsizes]</span></span>
  
    [<span data-ttu-id="de883-157">Détails de la tarification – App Service</span><span class="sxs-lookup"><span data-stu-id="de883-157">App Service Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/app-service/)
  
    [<span data-ttu-id="de883-158">Détails de la tarification – App Service - Connexions SSL</span><span class="sxs-lookup"><span data-stu-id="de883-158">App Service Pricing Details - SSL Connections</span></span>](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* <span data-ttu-id="de883-159">Pour plus d’informations sur les meilleures pratiques liées à Azure App Service, notamment la création d’une architecture évolutive et résiliente, voir [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx)(Meilleures pratiques : Azure App Service Web Apps).</span><span class="sxs-lookup"><span data-stu-id="de883-159">For information about Azure App Service best practices, including building a scalable and resilient architecture, see [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span></span>
* <span data-ttu-id="de883-160">Pour les vidéos sur la mise à l’échelle des applications de Service d’applications, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="de883-160">For videos about scaling App Service apps, see hello following resources:</span></span>
  
  * [<span data-ttu-id="de883-161">Lorsque des sites Web Azure - avec Stefan Schackow de tooScale</span><span class="sxs-lookup"><span data-stu-id="de883-161">When tooScale Azure Websites - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [<span data-ttu-id="de883-162">Mise à l’échelle automatique de Sites Web Azure, unité centrale ou planification - avec Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="de883-162">Auto Scaling Azure Websites, CPU or Scheduled - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [<span data-ttu-id="de883-163">Mise à l’échelle de Sites Web Azure - avec Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="de883-163">How Azure Websites Scale - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

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
