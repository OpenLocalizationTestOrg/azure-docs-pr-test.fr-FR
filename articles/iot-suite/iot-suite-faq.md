---
title: aaaAzure IoT Suite FAQ | Documents Microsoft
description: "Forum Aux Questions (FAQ) relatives à IoT Suite"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: cb537749-a8a1-4e53-b3bf-f1b64a38188a
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: cb39e24af6d1ce2afea554285512d05b2d7c721e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a><span data-ttu-id="6aeda-103">Forum Aux Questions (FAQ) relatives à IoT Suite</span><span class="sxs-lookup"><span data-stu-id="6aeda-103">Frequently asked questions for IoT Suite</span></span>

<span data-ttu-id="6aeda-104">Voir aussi, hello fabrique connecté spécifique [FAQ](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="6aeda-104">See also, hello connected factory specific [FAQ](iot-suite-faq-cf.md).</span></span>

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solutions"></a><span data-ttu-id="6aeda-105">Où puis-je trouver code source de hello pour les solutions hello préconfiguré ?</span><span class="sxs-lookup"><span data-stu-id="6aeda-105">Where can I find hello source code for hello preconfigured solutions?</span></span>

<span data-ttu-id="6aeda-106">code source de Hello est stocké dans hello suivant des dépôts GitHub :</span><span class="sxs-lookup"><span data-stu-id="6aeda-106">hello source code is stored in hello following GitHub repositories:</span></span>
* <span data-ttu-id="6aeda-107">[Solution préconfigurée de surveillance à distance][lnk-remote-monitoring-github]</span><span class="sxs-lookup"><span data-stu-id="6aeda-107">[Remote monitoring preconfigured solution][lnk-remote-monitoring-github]</span></span>
* <span data-ttu-id="6aeda-108">[Solution préconfigurée de maintenance prédictive][lnk-predictive-maintenance-github]</span><span class="sxs-lookup"><span data-stu-id="6aeda-108">[Predictive maintenance preconfigured solution][lnk-predictive-maintenance-github]</span></span>
* [<span data-ttu-id="6aeda-109">Solution préconfigurée d’usine connectée</span><span class="sxs-lookup"><span data-stu-id="6aeda-109">Connected factory preconfigured solution</span></span>](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-toohello-latest-version-of-hello-remote-monitoring-preconfigured-solution-that-uses-hello-iot-hub-device-management-features"></a><span data-ttu-id="6aeda-110">Comment mettre à jour toohello version la plus récente de la solution préconfigurée hello surveillance à distance qu’utilise hello des fonctionnalités de gestion des appareils IoT Hub ?</span><span class="sxs-lookup"><span data-stu-id="6aeda-110">How do I update toohello latest version of hello remote monitoring preconfigured solution that uses hello IoT Hub device management features?</span></span>

* <span data-ttu-id="6aeda-111">Si vous déployez une solution préconfigurée à partir du site de https://www.azureiotsuite.com/ hello, il déploie toujours une nouvelle instance de la version la plus récente de la solution de hello hello.</span><span class="sxs-lookup"><span data-stu-id="6aeda-111">If you deploy a preconfigured solution from hello https://www.azureiotsuite.com/ site, it always deploys a new instance of hello latest version of hello solution.</span></span>
* <span data-ttu-id="6aeda-112">Si vous déployez une solution préconfigurée, à l’aide de la ligne de commande hello, vous pouvez mettre à jour un déploiement existant par un nouveau code.</span><span class="sxs-lookup"><span data-stu-id="6aeda-112">If you deploy a preconfigured solution using hello command line, you can update an existing deployment with new code.</span></span> <span data-ttu-id="6aeda-113">Consultez [déploiement de cloud computing] [ lnk-cloud-deployment] Bonjour GitHub [référentiel][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="6aeda-113">See [Cloud deployment][lnk-cloud-deployment] in hello GitHub [repository][lnk-remote-monitoring-github].</span></span>

### <a name="how-can-i-add-support-for-a-new-device-method-toohello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="6aeda-114">Comment puis-je ajouter la prise en charge pour une solution préconfigurée de surveillance à distance appareil méthode toohello nouveau ?</span><span class="sxs-lookup"><span data-stu-id="6aeda-114">How can I add support for a new device method toohello remote monitoring preconfigured solution?</span></span>

<span data-ttu-id="6aeda-115">Consultez la section de hello [ajouter la prise en charge pour un simulateur de toohello nouvelle méthode] [ lnk-add-method] Bonjour [personnaliser une solution préconfigurée] [ lnk-customize] l’article.</span><span class="sxs-lookup"><span data-stu-id="6aeda-115">See hello section [Add support for a new method toohello simulator][lnk-add-method] in hello [Customize a preconfigured solution][lnk-customize] article.</span></span>

### <a name="hello-simulated-device-is-ignoring-my-desired-property-changes-why"></a><span data-ttu-id="6aeda-116">APPAREIL simulé de Hello ignore mes modifications de la propriété souhaitée, pourquoi ?</span><span class="sxs-lookup"><span data-stu-id="6aeda-116">hello simulated device is ignoring my desired property changes, why?</span></span>
<span data-ttu-id="6aeda-117">Bonjour surveillance à distance solution préconfigurée, hello simulée périphérique code utilise uniquement hello **Desired.Config.TemperatureMeanValue** et **Desired.Config.TelemetryInterval** propriétés souhaitée tooupdate hello a signalé des propriétés.</span><span class="sxs-lookup"><span data-stu-id="6aeda-117">In hello remote monitoring preconfigured solution, hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties.</span></span> <span data-ttu-id="6aeda-118">Toutes les autres demandes de modification de propriétés souhaitées sont ignorées.</span><span class="sxs-lookup"><span data-stu-id="6aeda-118">All other desired property change requests are ignored.</span></span>

### <a name="my-device-does-not-appear-in-hello-list-of-devices-in-hello-solution-dashboard-why"></a><span data-ttu-id="6aeda-119">Mon appareil n’apparaît pas dans la liste de hello des périphériques dans le tableau de bord solution hello, pourquoi ?</span><span class="sxs-lookup"><span data-stu-id="6aeda-119">My device does not appear in hello list of devices in hello solution dashboard, why?</span></span>

<span data-ttu-id="6aeda-120">liste de Hello des périphériques dans le tableau de bord hello solution utilise une liste de hello de tooreturn de requête de périphériques.</span><span class="sxs-lookup"><span data-stu-id="6aeda-120">hello list of devices in hello solution dashboard uses a query tooreturn hello list of devices.</span></span> <span data-ttu-id="6aeda-121">Pour le moment, une requête ne peut pas retourner plus de 10 000 appareils.</span><span class="sxs-lookup"><span data-stu-id="6aeda-121">Currently, a query cannot return more than 10K devices.</span></span> <span data-ttu-id="6aeda-122">Essayez de critères de recherche hello pour votre requête plus restrictive.</span><span class="sxs-lookup"><span data-stu-id="6aeda-122">Try making hello search criteria for your query more restrictive.</span></span>

### <a name="whats-hello-difference-between-deleting-a-resource-group-in-hello-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a><span data-ttu-id="6aeda-123">Qu’est la différence de hello entre la suppression d’un groupe de ressources Bonjour Azure portail et en cliquant sur Supprimer une solution préconfigurée dans azureiotsuite.com ?</span><span class="sxs-lookup"><span data-stu-id="6aeda-123">What's hello difference between deleting a resource group in hello Azure portal and clicking delete on a preconfigured solution in azureiotsuite.com?</span></span>

* <span data-ttu-id="6aeda-124">Si vous supprimez la solution hello préconfiguré dans [azureiotsuite.com][lnk-azureiotsuite], vous supprimez toutes les ressources hello qui ont été configurés lors de la création de solutions de hello préconfiguré.</span><span class="sxs-lookup"><span data-stu-id="6aeda-124">If you delete hello preconfigured solution in [azureiotsuite.com][lnk-azureiotsuite], you delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span> <span data-ttu-id="6aeda-125">Si vous avez ajouté le groupe de ressources toohello des ressources supplémentaires, ces ressources sont également supprimés.</span><span class="sxs-lookup"><span data-stu-id="6aeda-125">If you added additional resources toohello resource group, these resources are also deleted.</span></span> 
* <span data-ttu-id="6aeda-126">Si vous supprimez le groupe de ressources hello Bonjour [portail Azure][lnk-azure-portal], vous supprimez uniquement les ressources, hello dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="6aeda-126">If you delete hello resource group in hello [Azure portal][lnk-azure-portal], you only delete hello resources in that resource group.</span></span> <span data-ttu-id="6aeda-127">Vous devez également l’application d’Azure Active Directory hello toodelete associée solution hello préconfiguré Bonjour [portail Azure classic][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="6aeda-127">You also need toodelete hello Azure Active Directory application associated with hello preconfigured solution in hello [Azure classic portal][lnk-classic-portal].</span></span>

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="6aeda-128">Combien d’instances d’IoT Hub puis-je configurer dans un abonnement ?</span><span class="sxs-lookup"><span data-stu-id="6aeda-128">How many IoT Hub instances can I provision in a subscription?</span></span>

<span data-ttu-id="6aeda-129">Par défaut, vous pouvez configurer [10 instances IoT Hub par abonnement][link-azuresublimits].</span><span class="sxs-lookup"><span data-stu-id="6aeda-129">By default you can provision [10 IoT hubs per subscription][link-azuresublimits].</span></span> <span data-ttu-id="6aeda-130">Vous pouvez créer un [ticket de support Azure] [ link-azuresupportticket] tooraise cette limite.</span><span class="sxs-lookup"><span data-stu-id="6aeda-130">You can create an [Azure support ticket][link-azuresupportticket] tooraise this limit.</span></span> <span data-ttu-id="6aeda-131">Par conséquent, depuis chaque dispositions solution préconfigurée un IoT Hub, vous ne pouvez configurer des too10 préconfiguré solutions dans un abonnement donné.</span><span class="sxs-lookup"><span data-stu-id="6aeda-131">As a result, since every preconfigured solution provisions a new IoT Hub, you can only provision up too10 preconfigured solutions in a given subscription.</span></span> 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="6aeda-132">Combien d’instances d’Azure Cosmos DB puis-je configurer dans un abonnement ?</span><span class="sxs-lookup"><span data-stu-id="6aeda-132">How many Azure Cosmos DB instances can I provision in a subscription?</span></span>

<span data-ttu-id="6aeda-133">Cinquante.</span><span class="sxs-lookup"><span data-stu-id="6aeda-133">Fifty.</span></span> <span data-ttu-id="6aeda-134">Vous pouvez créer un [ticket de support Azure] [ link-azuresupportticket] tooraise cette limite, mais par défaut, vous ne pouvez configurer des instances de base de données Cosmos 50 par abonnement.</span><span class="sxs-lookup"><span data-stu-id="6aeda-134">You can create an [Azure support ticket][link-azuresupportticket] tooraise this limit, but by default, you can only provision 50 Cosmos DB instances per subscription.</span></span> 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a><span data-ttu-id="6aeda-135">Combien d’API Bing Maps gratuites puis-je configurer dans un abonnement ?</span><span class="sxs-lookup"><span data-stu-id="6aeda-135">How many Free Bing Maps APIs can I provision in a subscription?</span></span>

<span data-ttu-id="6aeda-136">Deux.</span><span class="sxs-lookup"><span data-stu-id="6aeda-136">Two.</span></span> <span data-ttu-id="6aeda-137">Vous pouvez créer uniquement deux cartes Bing - Transactions internes - Niveau 1 pour les plans d’entreprise dans un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="6aeda-137">You can create only two Internal Transactions Level 1 Bing Maps for Enterprise plans in an Azure subscription.</span></span> <span data-ttu-id="6aeda-138">solution de surveillance à distance Hello est configurée par défaut avec un plan hello interne des Transactions au niveau 1.</span><span class="sxs-lookup"><span data-stu-id="6aeda-138">hello remote monitoring solution is provisioned by default with hello Internal Transactions Level 1 plan.</span></span> <span data-ttu-id="6aeda-139">Par conséquent, vous ne pouvez configurer que des tootwo distant solutions dans un abonnement sans modification de contrôle.</span><span class="sxs-lookup"><span data-stu-id="6aeda-139">As a result, you can only provision up tootwo remote monitoring solutions in a subscription with no modifications.</span></span>

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a><span data-ttu-id="6aeda-140">J’ai mis en place le déploiement d’une solution de surveillance à distance avec une carte statique. Comment faire pour ajouter une carte Bing interactive ?</span><span class="sxs-lookup"><span data-stu-id="6aeda-140">I have a remote monitoring solution deployment with a static map, how do I add an interactive Bing map?</span></span>

1. <span data-ttu-id="6aeda-141">Obtenez votre QueryKey Bing Maps API pour Entreprise sur le [portail Azure][lnk-azure-portal] :</span><span class="sxs-lookup"><span data-stu-id="6aeda-141">Get your Bing Maps API for Enterprise QueryKey from [Azure portal][lnk-azure-portal]:</span></span> 
   
   1. <span data-ttu-id="6aeda-142">Accédez toohello groupe de ressources où votre API Bing Maps pour Enterprise est Bonjour [portail Azure][lnk-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="6aeda-142">Navigate toohello Resource Group where your Bing Maps API for Enterprise is in hello [Azure portal][lnk-azure-portal].</span></span>
   2. <span data-ttu-id="6aeda-143">Cliquez sur **Tous les paramètres**, puis sur **Gestion des clés**.</span><span class="sxs-lookup"><span data-stu-id="6aeda-143">Click **All Settings**, then **Key Management**.</span></span> 
   3. <span data-ttu-id="6aeda-144">Vous voyez deux clés : **MasterKey** et **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="6aeda-144">You can see two keys: **MasterKey** and **QueryKey**.</span></span> <span data-ttu-id="6aeda-145">Copiez la valeur hello pour **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="6aeda-145">Copy hello value for **QueryKey**.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="6aeda-146">Vous n’avez aucun compte Bing Maps API pour Entreprise ?</span><span class="sxs-lookup"><span data-stu-id="6aeda-146">Don't have a Bing Maps API for Enterprise account?</span></span> <span data-ttu-id="6aeda-147">Créer un dans hello [portail Azure] [ lnk-azure-portal] en cliquant sur + Nouveau, recherche de l’API Bing Maps pour Enterprise et suivre invite toocreate.</span><span class="sxs-lookup"><span data-stu-id="6aeda-147">Create one in hello [Azure portal][lnk-azure-portal] by clicking + New, searching for Bing Maps API for Enterprise and follow prompts toocreate.</span></span>
      > 
      > 
2. <span data-ttu-id="6aeda-148">Liste déroulante code dernière hello hello [Azure-IoT-de surveillance à distance][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="6aeda-148">Pull down hello latest code from hello [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span></span>
3. <span data-ttu-id="6aeda-149">Exécuter un local ou cloud de déploiement suivant hello les instructions de déploiement de ligne de commande dans le dossier de /docs/ hello dans le référentiel de hello.</span><span class="sxs-lookup"><span data-stu-id="6aeda-149">Run a local or cloud deployment following hello command-line deployment guidance in hello /docs/ folder in hello repository.</span></span> 
4. <span data-ttu-id="6aeda-150">Une fois que vous avez exécuté un local ou cloud de déploiement, recherchez dans votre dossier racine pour hello *. fichier user.config créé au cours du déploiement.</span><span class="sxs-lookup"><span data-stu-id="6aeda-150">After you've run a local or cloud deployment, look in your root folder for hello *.user.config file created during deployment.</span></span> <span data-ttu-id="6aeda-151">Ouvrez ce fichier dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="6aeda-151">Open this file in a text editor.</span></span> 
5. <span data-ttu-id="6aeda-152">Valeur de hello tooinclude vous avez copié à partir de la ligne suivante de hello de modifier votre **QueryKey**:</span><span class="sxs-lookup"><span data-stu-id="6aeda-152">Change hello following line tooinclude hello value you copied from your **QueryKey**:</span></span> 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a><span data-ttu-id="6aeda-153">Puis-je créer une solution préconfigurée si je dispose de Microsoft Azure pour DreamSpark ?</span><span class="sxs-lookup"><span data-stu-id="6aeda-153">Can I create a preconfigured solution if I have Microsoft Azure for DreamSpark?</span></span>

<span data-ttu-id="6aeda-154">Actuellement, il est impossible de créer une solution préconfigurée avec un compte [Microsoft Azure pour DreamSpark][lnk-dreamspark].</span><span class="sxs-lookup"><span data-stu-id="6aeda-154">Currently, you cannot create a preconfigured solution with a [Microsoft Azure for DreamSpark][lnk-dreamspark] account.</span></span> <span data-ttu-id="6aeda-155">Vous pouvez toutefois créer en quelques minutes un [compte d’évaluation Azure gratuit][lnk-30daytrial], que vous pouvez utiliser pour créer une solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="6aeda-155">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a><span data-ttu-id="6aeda-156">Puis-je créer une solution préconfigurée si j’ai un abonnement du fournisseur de solutions Cloud (CSP) ?</span><span class="sxs-lookup"><span data-stu-id="6aeda-156">Can I create a preconfigured solution if I have Cloud Solution Provider (CSP) subscription?</span></span>

<span data-ttu-id="6aeda-157">Actuellement, vous ne pouvez pas créer de solution préconfigurée avec un abonnement de fournisseur de solutions Cloud (CSP).</span><span class="sxs-lookup"><span data-stu-id="6aeda-157">Currently, you cannot create a preconfigured solution with a Cloud Solution Provider (CSP) subscription.</span></span> <span data-ttu-id="6aeda-158">Vous pouvez toutefois créer en quelques minutes un [compte d’évaluation Azure gratuit][lnk-30daytrial], que vous pouvez utiliser pour créer une solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="6aeda-158">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="how-do-i-delete-an-aad-tenant"></a><span data-ttu-id="6aeda-159">Comment supprimer un client AAS ?</span><span class="sxs-lookup"><span data-stu-id="6aeda-159">How do I delete an AAD tenant?</span></span>

<span data-ttu-id="6aeda-160">Consultez le billet de blog d’Eric Golpe, [Procédure pas à pas pour la suppression d’un client Azure AD][lnk-delete-aad-tennant].</span><span class="sxs-lookup"><span data-stu-id="6aeda-160">See Eric Golpe's blog post [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant].</span></span>

### <a name="next-steps"></a><span data-ttu-id="6aeda-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6aeda-161">Next steps</span></span>

<span data-ttu-id="6aeda-162">Vous pouvez également découvrir hello autres et les fonctionnalités des solutions de IoT Suite préconfiguré hello :</span><span class="sxs-lookup"><span data-stu-id="6aeda-162">You can also explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="6aeda-163">[Présentation de la solution préconfigurée de maintenance prédictive][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="6aeda-163">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* [<span data-ttu-id="6aeda-164">Présentation de la solution préconfigurée d’usine connectée</span><span class="sxs-lookup"><span data-stu-id="6aeda-164">Connected factory preconfigured solution overview</span></span>](iot-suite-connected-factory-overview.md)
* <span data-ttu-id="6aeda-165">[IoT hello d’arrière-plan la sécurité][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="6aeda-165">[IoT security from hello ground up][lnk-security-groundup]</span></span>

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-security-groundup]: securing-iot-ground-up.md

[link-azuresupportticket]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade 
[link-azuresublimits]: https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/#iot-hub-limits
[lnk-azure-portal]: https://portal.azure.com
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring 
[lnk-dreamspark]: https://www.dreamspark.com/Product/Product.aspx?productid=99 
[lnk-30daytrial]: https://azure.microsoft.com/free/
[lnk-delete-aad-tennant]: http://blogs.msdn.com/b/ericgolpe/archive/2015/04/30/walkthrough-of-deleting-an-azure-ad-tenant.aspx
[lnk-cloud-deployment]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
[lnk-add-method]: iot-suite-guidance-on-customizing-preconfigured-solutions.md#add-support-for-a-new-method-to-the-simulator
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-predictive-maintenance-github]: https://github.com/Azure/azure-iot-predictive-maintenance
