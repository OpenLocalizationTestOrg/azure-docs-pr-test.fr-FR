---
title: FAQ sur IoT Azure Suite | Microsoft Docs
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
ms.openlocfilehash: 85867fb8d18377637b3aa848555831a8d9b53512
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a><span data-ttu-id="b1f7c-103">Forum Aux Questions (FAQ) relatives à IoT Suite</span><span class="sxs-lookup"><span data-stu-id="b1f7c-103">Frequently asked questions for IoT Suite</span></span>

<span data-ttu-id="b1f7c-104">Voir aussi les [questions fréquentes (FAQ)](iot-suite-faq-cf.md) spécifiques sur l’usine connectée.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-104">See also, the connected factory specific [FAQ](iot-suite-faq-cf.md).</span></span>

### <a name="where-can-i-find-the-source-code-for-the-preconfigured-solutions"></a><span data-ttu-id="b1f7c-105">Où trouver le code source des solutions préconfigurées ?</span><span class="sxs-lookup"><span data-stu-id="b1f7c-105">Where can I find the source code for the preconfigured solutions?</span></span>

<span data-ttu-id="b1f7c-106">Le code source est stocké dans les référentiels GitHub suivants :</span><span class="sxs-lookup"><span data-stu-id="b1f7c-106">The source code is stored in the following GitHub repositories:</span></span>
* <span data-ttu-id="b1f7c-107">[Solution préconfigurée de surveillance à distance][lnk-remote-monitoring-github]</span><span class="sxs-lookup"><span data-stu-id="b1f7c-107">[Remote monitoring preconfigured solution][lnk-remote-monitoring-github]</span></span>
* <span data-ttu-id="b1f7c-108">[Solution préconfigurée de maintenance prédictive][lnk-predictive-maintenance-github]</span><span class="sxs-lookup"><span data-stu-id="b1f7c-108">[Predictive maintenance preconfigured solution][lnk-predictive-maintenance-github]</span></span>
* [<span data-ttu-id="b1f7c-109">Solution préconfigurée d’usine connectée</span><span class="sxs-lookup"><span data-stu-id="b1f7c-109">Connected factory preconfigured solution</span></span>](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-to-the-latest-version-of-the-remote-monitoring-preconfigured-solution-that-uses-the-iot-hub-device-management-features"></a><span data-ttu-id="b1f7c-110">Comment procéder à une mise à jour vers la dernière version de la solution préconfigurée de surveillance à distance qui utilise les fonctionnalités de gestion d’appareils IoT Hub ?</span><span class="sxs-lookup"><span data-stu-id="b1f7c-110">How do I update to the latest version of the remote monitoring preconfigured solution that uses the IoT Hub device management features?</span></span>

* <span data-ttu-id="b1f7c-111">Si vous déployez une solution préconfigurée à partir du site https://www.azureiotsuite.com/, elle déploie toujours une nouvelle instance de la version la plus récente de la solution.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-111">If you deploy a preconfigured solution from the https://www.azureiotsuite.com/ site, it always deploys a new instance of the latest version of the solution.</span></span>
* <span data-ttu-id="b1f7c-112">Si vous déployez une solution préconfigurée à l’aide de la ligne de commande, vous pouvez mettre à jour un déploiement existant avec le nouveau code.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-112">If you deploy a preconfigured solution using the command line, you can update an existing deployment with new code.</span></span> <span data-ttu-id="b1f7c-113">Consultez la page [Cloud deployment (Déploiement cloud)][lnk-cloud-deployment] dans le [référentiel][lnk-remote-monitoring-github] GitHub.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-113">See [Cloud deployment][lnk-cloud-deployment] in the GitHub [repository][lnk-remote-monitoring-github].</span></span>

### <a name="how-can-i-add-support-for-a-new-device-method-to-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="b1f7c-114">Comment ajouter la prise en charge d’une nouvelle méthode de périphérique à la solution préconfigurée de surveillance à distance ?</span><span class="sxs-lookup"><span data-stu-id="b1f7c-114">How can I add support for a new device method to the remote monitoring preconfigured solution?</span></span>

<span data-ttu-id="b1f7c-115">Consultez la section [Add support for a new method to the simulator (Ajouter la prise en charge d’une nouvelle méthode au simulateur)][lnk-add-method] de l’article [Personnaliser une solution préconfigurée][lnk-customize].</span><span class="sxs-lookup"><span data-stu-id="b1f7c-115">See the section [Add support for a new method to the simulator][lnk-add-method] in the [Customize a preconfigured solution][lnk-customize] article.</span></span>

### <a name="the-simulated-device-is-ignoring-my-desired-property-changes-why"></a><span data-ttu-id="b1f7c-116">L’appareil simulé ignore mes modifications de propriété souhaitées. Pourquoi ?</span><span class="sxs-lookup"><span data-stu-id="b1f7c-116">The simulated device is ignoring my desired property changes, why?</span></span>
<span data-ttu-id="b1f7c-117">Dans la solution préconfigurée de surveillance à distance, le code d’appareil simulé utilise uniquement les propriétés souhaitées **Desired.Config.TemperatureMeanValue** et **Desired.Config.TelemetryInterval** pour mettre à jour les propriétés signalées.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-117">In the remote monitoring preconfigured solution, the simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties.</span></span> <span data-ttu-id="b1f7c-118">Toutes les autres demandes de modification de propriétés souhaitées sont ignorées.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-118">All other desired property change requests are ignored.</span></span>

### <a name="my-device-does-not-appear-in-the-list-of-devices-in-the-solution-dashboard-why"></a><span data-ttu-id="b1f7c-119">Mon appareil n’apparaît pas dans la liste des appareils du tableau de bord de la solution. Pourquoi ?</span><span class="sxs-lookup"><span data-stu-id="b1f7c-119">My device does not appear in the list of devices in the solution dashboard, why?</span></span>

<span data-ttu-id="b1f7c-120">La liste des appareils du tableau de bord de la solution utilise une requête pour retourner la liste des appareils.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-120">The list of devices in the solution dashboard uses a query to return the list of devices.</span></span> <span data-ttu-id="b1f7c-121">Pour le moment, une requête ne peut pas retourner plus de 10 000 appareils.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-121">Currently, a query cannot return more than 10K devices.</span></span> <span data-ttu-id="b1f7c-122">Essayez de rendre les critères de recherche de votre requête plus restrictifs.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-122">Try making the search criteria for your query more restrictive.</span></span>

### <a name="whats-the-difference-between-deleting-a-resource-group-in-the-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a><span data-ttu-id="b1f7c-123">Quelle est la différence entre la suppression d’un groupe de ressources dans le portail Azure et un clic sur l’option supprimer d’une solution préconfigurée dans azureiotsuite.com ?</span><span class="sxs-lookup"><span data-stu-id="b1f7c-123">What's the difference between deleting a resource group in the Azure portal and clicking delete on a preconfigured solution in azureiotsuite.com?</span></span>

* <span data-ttu-id="b1f7c-124">Si vous supprimez la solution préconfigurée dans [azureiotsuite.com][lnk-azureiotsuite], vous supprimez toutes les ressources qui ont été configurées lors de la création de la solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-124">If you delete the preconfigured solution in [azureiotsuite.com][lnk-azureiotsuite], you delete all the resources that were provisioned when you created the preconfigured solution.</span></span> <span data-ttu-id="b1f7c-125">Si vous avez ajouté des ressources supplémentaires au groupe de ressources, elles sont également supprimées.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-125">If you added additional resources to the resource group, these resources are also deleted.</span></span> 
* <span data-ttu-id="b1f7c-126">Si vous supprimez le groupe de ressources sur le [portail Azure][lnk-azure-portal], vous supprimez uniquement les ressources de ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-126">If you delete the resource group in the [Azure portal][lnk-azure-portal], you only delete the resources in that resource group.</span></span> <span data-ttu-id="b1f7c-127">Vous devez également supprimer l’application Azure Active Directory associée à la solution préconfigurée sur le [Portail Azure Classic][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="b1f7c-127">You also need to delete the Azure Active Directory application associated with the preconfigured solution in the [Azure classic portal][lnk-classic-portal].</span></span>

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="b1f7c-128">Combien d’instances d’IoT Hub puis-je configurer dans un abonnement ?</span><span class="sxs-lookup"><span data-stu-id="b1f7c-128">How many IoT Hub instances can I provision in a subscription?</span></span>

<span data-ttu-id="b1f7c-129">Par défaut, vous pouvez configurer [10 instances IoT Hub par abonnement][link-azuresublimits].</span><span class="sxs-lookup"><span data-stu-id="b1f7c-129">By default you can provision [10 IoT hubs per subscription][link-azuresublimits].</span></span> <span data-ttu-id="b1f7c-130">Vous pouvez créer un [ticket de support Azure][link-azuresupportticket] pour augmenter cette limite.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-130">You can create an [Azure support ticket][link-azuresupportticket] to raise this limit.</span></span> <span data-ttu-id="b1f7c-131">Par conséquent, étant donné que chaque solution préconfigurée approvisionne un nouvel IoT Hub, vous ne pouvez configurer que 10 solutions préconfigurées au maximum dans un abonnement.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-131">As a result, since every preconfigured solution provisions a new IoT Hub, you can only provision up to 10 preconfigured solutions in a given subscription.</span></span> 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="b1f7c-132">Combien d’instances d’Azure Cosmos DB puis-je configurer dans un abonnement ?</span><span class="sxs-lookup"><span data-stu-id="b1f7c-132">How many Azure Cosmos DB instances can I provision in a subscription?</span></span>

<span data-ttu-id="b1f7c-133">Cinquante.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-133">Fifty.</span></span> <span data-ttu-id="b1f7c-134">Vous pouvez créer un [ticket de support Azure][link-azuresupportticket] pour augmenter cette limite, mais par défaut, vous ne pouvez approvisionner que 50 instances de Cosmos DB par abonnement.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-134">You can create an [Azure support ticket][link-azuresupportticket] to raise this limit, but by default, you can only provision 50 Cosmos DB instances per subscription.</span></span> 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a><span data-ttu-id="b1f7c-135">Combien d’API Bing Maps gratuites puis-je configurer dans un abonnement ?</span><span class="sxs-lookup"><span data-stu-id="b1f7c-135">How many Free Bing Maps APIs can I provision in a subscription?</span></span>

<span data-ttu-id="b1f7c-136">Deux.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-136">Two.</span></span> <span data-ttu-id="b1f7c-137">Vous pouvez créer uniquement deux cartes Bing - Transactions internes - Niveau 1 pour les plans d’entreprise dans un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-137">You can create only two Internal Transactions Level 1 Bing Maps for Enterprise plans in an Azure subscription.</span></span> <span data-ttu-id="b1f7c-138">La solution de surveillance à distance est configurée par défaut avec le plan Transactions internes - Niveau 1.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-138">The remote monitoring solution is provisioned by default with the Internal Transactions Level 1 plan.</span></span> <span data-ttu-id="b1f7c-139">Par conséquent, vous pouvez configurer au maximum deux solutions de surveillance à distance préconfigurées sans modification.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-139">As a result, you can only provision up to two remote monitoring solutions in a subscription with no modifications.</span></span>

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a><span data-ttu-id="b1f7c-140">J’ai mis en place le déploiement d’une solution de surveillance à distance avec une carte statique. Comment faire pour ajouter une carte Bing interactive ?</span><span class="sxs-lookup"><span data-stu-id="b1f7c-140">I have a remote monitoring solution deployment with a static map, how do I add an interactive Bing map?</span></span>

1. <span data-ttu-id="b1f7c-141">Obtenez votre QueryKey Bing Maps API pour Entreprise sur le [portail Azure][lnk-azure-portal] :</span><span class="sxs-lookup"><span data-stu-id="b1f7c-141">Get your Bing Maps API for Enterprise QueryKey from [Azure portal][lnk-azure-portal]:</span></span> 
   
   1. <span data-ttu-id="b1f7c-142">Accédez au groupe de ressources contenant Bing Maps API pour Entreprise dans le [portail Azure][lnk-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="b1f7c-142">Navigate to the Resource Group where your Bing Maps API for Enterprise is in the [Azure portal][lnk-azure-portal].</span></span>
   2. <span data-ttu-id="b1f7c-143">Cliquez sur **Tous les paramètres**, puis sur **Gestion des clés**.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-143">Click **All Settings**, then **Key Management**.</span></span> 
   3. <span data-ttu-id="b1f7c-144">Vous voyez deux clés : **MasterKey** et **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-144">You can see two keys: **MasterKey** and **QueryKey**.</span></span> <span data-ttu-id="b1f7c-145">Copiez la valeur de **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-145">Copy the value for **QueryKey**.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="b1f7c-146">Vous n’avez aucun compte Bing Maps API pour Entreprise ?</span><span class="sxs-lookup"><span data-stu-id="b1f7c-146">Don't have a Bing Maps API for Enterprise account?</span></span> <span data-ttu-id="b1f7c-147">Créez-le sur le [portail Azure][lnk-azure-portal] en cliquant sur +Nouveau, en recherchant Bing Maps API pour Entreprise et en suivant la procédure.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-147">Create one in the [Azure portal][lnk-azure-portal] by clicking + New, searching for Bing Maps API for Enterprise and follow prompts to create.</span></span>
      > 
      > 
2. <span data-ttu-id="b1f7c-148">Déroulez le code le plus récent dans [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="b1f7c-148">Pull down the latest code from the [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span></span>
3. <span data-ttu-id="b1f7c-149">Effectuez un déploiement local ou dans le cloud selon les instructions de déploiement par ligne de commande dans le dossier /docs/ du référentiel.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-149">Run a local or cloud deployment following the command-line deployment guidance in the /docs/ folder in the repository.</span></span> 
4. <span data-ttu-id="b1f7c-150">Une fois le déploiement local ou cloud effectué, recherchez dans votre dossier racine le fichier *.user.config créé.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-150">After you've run a local or cloud deployment, look in your root folder for the *.user.config file created during deployment.</span></span> <span data-ttu-id="b1f7c-151">Ouvrez ce fichier dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-151">Open this file in a text editor.</span></span> 
5. <span data-ttu-id="b1f7c-152">Modifiez la ligne suivante en y incluant la valeur que vous avez copiée de votre clé **QueryKey** :</span><span class="sxs-lookup"><span data-stu-id="b1f7c-152">Change the following line to include the value you copied from your **QueryKey**:</span></span> 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a><span data-ttu-id="b1f7c-153">Puis-je créer une solution préconfigurée si je dispose de Microsoft Azure pour DreamSpark ?</span><span class="sxs-lookup"><span data-stu-id="b1f7c-153">Can I create a preconfigured solution if I have Microsoft Azure for DreamSpark?</span></span>

<span data-ttu-id="b1f7c-154">Actuellement, il est impossible de créer une solution préconfigurée avec un compte [Microsoft Azure pour DreamSpark][lnk-dreamspark].</span><span class="sxs-lookup"><span data-stu-id="b1f7c-154">Currently, you cannot create a preconfigured solution with a [Microsoft Azure for DreamSpark][lnk-dreamspark] account.</span></span> <span data-ttu-id="b1f7c-155">Vous pouvez toutefois créer en quelques minutes un [compte d’évaluation Azure gratuit][lnk-30daytrial], que vous pouvez utiliser pour créer une solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-155">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a><span data-ttu-id="b1f7c-156">Puis-je créer une solution préconfigurée si j’ai un abonnement du fournisseur de solutions Cloud (CSP) ?</span><span class="sxs-lookup"><span data-stu-id="b1f7c-156">Can I create a preconfigured solution if I have Cloud Solution Provider (CSP) subscription?</span></span>

<span data-ttu-id="b1f7c-157">Actuellement, vous ne pouvez pas créer de solution préconfigurée avec un abonnement de fournisseur de solutions Cloud (CSP).</span><span class="sxs-lookup"><span data-stu-id="b1f7c-157">Currently, you cannot create a preconfigured solution with a Cloud Solution Provider (CSP) subscription.</span></span> <span data-ttu-id="b1f7c-158">Vous pouvez toutefois créer en quelques minutes un [compte d’évaluation Azure gratuit][lnk-30daytrial], que vous pouvez utiliser pour créer une solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="b1f7c-158">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="how-do-i-delete-an-aad-tenant"></a><span data-ttu-id="b1f7c-159">Comment supprimer un client AAS ?</span><span class="sxs-lookup"><span data-stu-id="b1f7c-159">How do I delete an AAD tenant?</span></span>

<span data-ttu-id="b1f7c-160">Consultez le billet de blog d’Eric Golpe, [Procédure pas à pas pour la suppression d’un client Azure AD][lnk-delete-aad-tennant].</span><span class="sxs-lookup"><span data-stu-id="b1f7c-160">See Eric Golpe's blog post [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant].</span></span>

### <a name="next-steps"></a><span data-ttu-id="b1f7c-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b1f7c-161">Next steps</span></span>

<span data-ttu-id="b1f7c-162">Vous pouvez également explorer certaines des autres fonctionnalités et capacités des solutions préconfigurées IoT Suite :</span><span class="sxs-lookup"><span data-stu-id="b1f7c-162">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="b1f7c-163">[Présentation de la solution préconfigurée de maintenance prédictive][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="b1f7c-163">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* [<span data-ttu-id="b1f7c-164">Présentation de la solution préconfigurée d’usine connectée</span><span class="sxs-lookup"><span data-stu-id="b1f7c-164">Connected factory preconfigured solution overview</span></span>](iot-suite-connected-factory-overview.md)
* <span data-ttu-id="b1f7c-165">[Sécurisation de l’Internet des objets de bout en bout][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="b1f7c-165">[IoT security from the ground up][lnk-security-groundup]</span></span>

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
