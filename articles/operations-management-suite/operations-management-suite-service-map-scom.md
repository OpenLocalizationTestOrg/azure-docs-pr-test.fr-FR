---
title: "Intégration de Service Map avec System Center Operations Manager | Microsoft Docs"
description: "Carte de service est une solution OMS (Operations Management Suite) qui détecte automatiquement les composants d’application sur les systèmes Windows et Linux et mappe la communication entre les services. Cet article décrit l’utilisation de Service Map pour créer automatiquement des diagrammes d’application distribuée dans Operations Manager."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: e8614a5a-9cf8-4c81-8931-896d358ad2cb
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: bwren;dairwin
ms.openlocfilehash: a7dbe54ffb4daa941c19b51ba263dd3d23b7a98b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a><span data-ttu-id="93cd1-104">Intégration de Service Map avec System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="93cd1-104">Service Map integration with System Center Operations Manager</span></span>
  > [!NOTE]
  > <span data-ttu-id="93cd1-105">Cette fonctionnalité est en version préliminaire publique.</span><span class="sxs-lookup"><span data-stu-id="93cd1-105">This feature is in public preview.</span></span>
  > 
  
<span data-ttu-id="93cd1-106">Operations Management Suite Service Map détecte automatiquement les composants d’application sur les systèmes Windows et Linux et mappe la communication entre les services.</span><span class="sxs-lookup"><span data-stu-id="93cd1-106">Operations Management Suite Service Map automatically discovers application components on Windows and Linux systems and maps the communication between services.</span></span> <span data-ttu-id="93cd1-107">Service Map vous permet d’afficher les serveurs comme des systèmes interconnectés qui fournissent des services critiques.</span><span class="sxs-lookup"><span data-stu-id="93cd1-107">Service Map allows you to view your servers the way you think of them, as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="93cd1-108">Carte de service affiche les connexions entre les serveurs, les processus et les ports sur n’importe quelle architecture connectée à TCP, sans configuration requise autre que l’installation d’un agent.</span><span class="sxs-lookup"><span data-stu-id="93cd1-108">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture, with no configuration required besides the installation of an agent.</span></span> <span data-ttu-id="93cd1-109">Pour plus d’informations, consultez la [documentation de Service Map](operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="93cd1-109">For more information, see the [Service Map documentation](operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="93cd1-110">Avec cette intégration entre Service Map et System Center Operations Manager, vous pouvez créer automatiquement des diagrammes d’application distribuée dans Operations Manager basés sur des cartes de dépendance dynamique dans Service Map.</span><span class="sxs-lookup"><span data-stu-id="93cd1-110">With this integration between Service Map and System Center Operations Manager, you can automatically create distributed application diagrams in Operations Manager that are based on the dynamic dependency maps in Service Map.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93cd1-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="93cd1-111">Prerequisites</span></span>
* <span data-ttu-id="93cd1-112">Un groupe d’administration d’Operations Manager qui gère un ensemble de serveurs.</span><span class="sxs-lookup"><span data-stu-id="93cd1-112">An Operations Manager management group that is managing a set of servers.</span></span>
* <span data-ttu-id="93cd1-113">Un espace de travail Operations Management Suite avec la solution Service Map activée.</span><span class="sxs-lookup"><span data-stu-id="93cd1-113">An Operations Management Suite workspace with the Service Map solution enabled.</span></span>
* <span data-ttu-id="93cd1-114">Un ensemble de serveurs (au moins un) gérés par Operations Manager et envoyant des données à Service Map.</span><span class="sxs-lookup"><span data-stu-id="93cd1-114">A set of servers (at least one) that are being managed by Operations Manager and sending data to Service Map.</span></span> <span data-ttu-id="93cd1-115">Les serveurs Windows et Linux sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="93cd1-115">Windows and Linux servers are supported.</span></span>
* <span data-ttu-id="93cd1-116">Un principal de service disposant d’un accès à l’abonnement Azure associé à l’espace de travail Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="93cd1-116">A service principal with access to the Azure subscription that is associated with the Operations Management Suite workspace.</span></span> <span data-ttu-id="93cd1-117">Pour plus d’informations, consultez l’article [Créer un principal du service](#creating-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="93cd1-117">For more information, go to [Create a service principal](#creating-a-service-principal).</span></span>

## <a name="install-the-service-map-management-pack"></a><span data-ttu-id="93cd1-118">Installation du pack d’administration de Service Map</span><span class="sxs-lookup"><span data-stu-id="93cd1-118">Install the Service Map management pack</span></span>
<span data-ttu-id="93cd1-119">Vous activez l’intégration entre Operations Manager et Service Map en important le groupement de packs d’administration Microsoft.SystemCenter.ServiceMap (Microsoft.SystemCenter.ServiceMap.mpb).</span><span class="sxs-lookup"><span data-stu-id="93cd1-119">You enable the integration between Operations Manager and Service Map by importing the Microsoft.SystemCenter.ServiceMap management pack bundle (Microsoft.SystemCenter.ServiceMap.mpb).</span></span> <span data-ttu-id="93cd1-120">Le groupe contient les packs d’administration suivants :</span><span class="sxs-lookup"><span data-stu-id="93cd1-120">The bundle contains the following management packs:</span></span>
* <span data-ttu-id="93cd1-121">Microsoft Service Map - Vues de l’application</span><span class="sxs-lookup"><span data-stu-id="93cd1-121">Microsoft Service Map Application Views</span></span>
* <span data-ttu-id="93cd1-122">Microsoft System Center Service Map - Interne</span><span class="sxs-lookup"><span data-stu-id="93cd1-122">Microsoft System Center Service Map Internal</span></span>
* <span data-ttu-id="93cd1-123">Microsoft System Center Service Map - Valeurs de remplacement</span><span class="sxs-lookup"><span data-stu-id="93cd1-123">Microsoft System Center Service Map Overrides</span></span>
* <span data-ttu-id="93cd1-124">Microsoft System Center Service Map</span><span class="sxs-lookup"><span data-stu-id="93cd1-124">Microsoft System Center Service Map</span></span>

## <a name="configure-the-service-map-integration"></a><span data-ttu-id="93cd1-125">Configuration de l’intégration de Service Map</span><span class="sxs-lookup"><span data-stu-id="93cd1-125">Configure the Service Map integration</span></span>
<span data-ttu-id="93cd1-126">Après avoir installé le pack d’administration Service Map, vous trouverez un nouveau nœud, **Service Map**, dans le volet **Administration** **d’Operations Management Suite**.</span><span class="sxs-lookup"><span data-stu-id="93cd1-126">After you install the Service Map management pack, a new node, **Service Map**, is displayed under **Operations Management Suite** in the **Administration** pane.</span></span> 

<span data-ttu-id="93cd1-127">Pour configurer l’intégration de Service Map, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="93cd1-127">To configure Service Map integration, do the following:</span></span>

1. <span data-ttu-id="93cd1-128">Cliquez sur **Ajouter un espace de travail** dans le volet de **vue d’ensemble de Service Map** pour ouvrir l’Assistant Configuration.</span><span class="sxs-lookup"><span data-stu-id="93cd1-128">To open the configuration wizard, in the **Service Map Overview** pane, click **Add workspace**.</span></span>  

    ![Vue d’ensemble de Service Map](media/oms-service-map/scom-configuration.png)

2. <span data-ttu-id="93cd1-130">Dans la fenêtre **Configuration des connexions**, entrez l’ID ou le nom du client, l’ID d’application (aussi appelé nom d’utilisateur ou ID client) et le mot de passe du principal de service, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="93cd1-130">In the **Connection Configuration** window, enter the tenant name or ID, application ID (also known as the username or clientID), and password of the service principal, and then click **Next**.</span></span> <span data-ttu-id="93cd1-131">Pour plus d’informations, consultez l’article [Créer un principal du service](#creating-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="93cd1-131">For more information, go to [Create a service principal](#creating-a-service-principal).</span></span>

    ![Fenêtre Configuration des connexions](media/oms-service-map/scom-config-spn.png)

3. <span data-ttu-id="93cd1-133">Dans la fenêtre **Sélection d’un abonnement**, sélectionnez l’abonnement Azure, le groupe de ressources Azure (celui qui contient l’espace de travail Operations Management Suite) et l’espace de travail Operations Management Suite, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="93cd1-133">In the **Subscription Selection** window, select the Azure subscription, Azure resource group (the one that contains the Operations Management Suite workspace), and Operations Management Suite workspace, and then click **Next**.</span></span>

    ![Espace de travail de configuration d’Operations Manager](media/oms-service-map/scom-config-workspace.png)

4. <span data-ttu-id="93cd1-135">Dans la fenêtre **Sélection du groupe d’ordinateurs**, choisissez quels groupes d’ordinateurs Service Map vous voulez synchroniser à Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="93cd1-135">In the **Machine Group Selection** window, you choose which Service Map Machine Groups you want to sync to Operations Manager.</span></span> <span data-ttu-id="93cd1-136">Cliquez sur **Ajouter/supprimer des groupes d’ordinateurs**, choisissez des groupes dans la liste des **Groupes d’ordinateurs disponibles**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="93cd1-136">Click **Add/Remove Machine Groups**, choose groups from the list of **Available Machine Groups**, and click **Add**.</span></span>  <span data-ttu-id="93cd1-137">Lorsque vous avez fini de sélectionner des groupes, cliquez sur **Ok** pour terminer.</span><span class="sxs-lookup"><span data-stu-id="93cd1-137">When you are finished selecting groups, click **Ok** to finish.</span></span>
    
    ![Groupes d’ordinateurs de configuration Operations Manager](media/oms-service-map/scom-config-machine-groups.png)
    
5. <span data-ttu-id="93cd1-139">Dans la fenêtre **Sélection du serveur**, vous configurez le groupe de serveurs Service Map avec les serveurs que vous voulez synchroniser entre Operations Manager et Service Map.</span><span class="sxs-lookup"><span data-stu-id="93cd1-139">In the **Server Selection** window, you configure the Service Map Servers Group with the servers that you want to sync between Operations Manager and Service Map.</span></span> <span data-ttu-id="93cd1-140">Cliquez sur **Ajouter/Supprimer des serveurs**.</span><span class="sxs-lookup"><span data-stu-id="93cd1-140">Click **Add/Remove Servers**.</span></span>   
    
    <span data-ttu-id="93cd1-141">Pour que l’intégration crée un diagramme d’application distribuée pour un serveur, le serveur doit être :</span><span class="sxs-lookup"><span data-stu-id="93cd1-141">For the integration to build a distributed application diagram for a server, the server must be:</span></span>

    * <span data-ttu-id="93cd1-142">Géré par Operations Manager</span><span class="sxs-lookup"><span data-stu-id="93cd1-142">Managed by Operations Manager</span></span>
    * <span data-ttu-id="93cd1-143">Géré par Service Map</span><span class="sxs-lookup"><span data-stu-id="93cd1-143">Managed by Service Map</span></span>
    * <span data-ttu-id="93cd1-144">Répertorié dans le groupe de serveurs Service Map</span><span class="sxs-lookup"><span data-stu-id="93cd1-144">Listed in the Service Map Servers Group</span></span>

    ![Groupe de configuration d’Operations Manager](media/oms-service-map/scom-config-group.png)

6. <span data-ttu-id="93cd1-146">Facultatif : sélectionnez le pool de ressources du serveur d’administration pour communiquer avec Operations Management Suite et cliquez sur **Ajouter un espace de travail**.</span><span class="sxs-lookup"><span data-stu-id="93cd1-146">Optional: Select the Management Server resource pool to communicate with Operations Management Suite, and then click **Add Workspace**.</span></span>

    ![Pool de ressources de configuration d’Operations Manager](media/oms-service-map/scom-config-pool.png)

    <span data-ttu-id="93cd1-148">La configuration et l’inscription de l’espace de travail Operations Management Suite peuvent prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="93cd1-148">It might take a minute to configure and register the Operations Management Suite workspace.</span></span> <span data-ttu-id="93cd1-149">Une fois qu’il est configuré, Operations Manager lance la première synchronisation de Service Map à partir d’Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="93cd1-149">After it is configured, Operations Manager initiates the first Service Map sync from Operations Management Suite.</span></span>

    ![Pool de ressources de configuration d’Operations Manager](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a><span data-ttu-id="93cd1-151">Surveillance de Service Map</span><span class="sxs-lookup"><span data-stu-id="93cd1-151">Monitor Service Map</span></span>
<span data-ttu-id="93cd1-152">Une fois l’espace de travail Operations Management Suite connecté, un nouveau dossier, Service Map, s’affiche dans le panneau **Analyse** de la console Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="93cd1-152">After the Operations Management Suite workspace is connected, a new folder, Service Map, is displayed in the **Monitoring** pane of the Operations Manager console.</span></span>

![Panneau Analyse d’Operations Manager](media/oms-service-map/scom-monitoring.png)

<span data-ttu-id="93cd1-154">Le dossier Service Map possède quatre nœuds :</span><span class="sxs-lookup"><span data-stu-id="93cd1-154">The Service Map folder has four nodes:</span></span>
* <span data-ttu-id="93cd1-155">**Alertes actives** : répertorie toutes les alertes actives sur la communication entre Operations Manager et Service Map.</span><span class="sxs-lookup"><span data-stu-id="93cd1-155">**Active Alerts**: Lists all the active alerts about the communication between Operations Manager and Service Map.</span></span>  <span data-ttu-id="93cd1-156">Ces alertes ne correspondent pas aux alertes Operations Management Suite synchronisées à Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="93cd1-156">Note that these alerts are not Operations Management Suite alerts being synced to Operations Manager.</span></span> 

* <span data-ttu-id="93cd1-157">**Serveurs** : répertorie les serveurs analysés configurés pour la synchronisation à partir de Service Map.</span><span class="sxs-lookup"><span data-stu-id="93cd1-157">**Servers**: Lists the monitored servers that are configured to sync from Service Map.</span></span>

    ![Panneau Analyse des serveurs d’Operations Manager](media/oms-service-map/scom-monitoring-servers.png)

* <span data-ttu-id="93cd1-159">**Vues de dépendance de groupe d’ordinateurs** : répertorie tous les groupes d’ordinateurs synchronisés depuis Service Map.</span><span class="sxs-lookup"><span data-stu-id="93cd1-159">**Machine Group Dependency Views**: Lists all machine groups that are synced from Service Map.</span></span> <span data-ttu-id="93cd1-160">Vous pouvez cliquer sur n’importe quel groupe pour afficher son diagramme d’application distribuée.</span><span class="sxs-lookup"><span data-stu-id="93cd1-160">You can click any group to view its distributed application diagram.</span></span>

    ![Diagramme d’application distribuée Operations Manager](media/oms-service-map/scom-group-dad.png)

* <span data-ttu-id="93cd1-162">**Vues de dépendance au serveur** : répertorie tous les serveurs synchronisés à partir de Service Map.</span><span class="sxs-lookup"><span data-stu-id="93cd1-162">**Server Dependency Views**: Lists all servers that are synced from Service Map.</span></span> <span data-ttu-id="93cd1-163">Vous pouvez cliquer sur n’importe quel serveur pour afficher son diagramme d’application distribuée.</span><span class="sxs-lookup"><span data-stu-id="93cd1-163">You can click any server to view its distributed application diagram.</span></span>

    ![Diagramme d’application distribuée Operations Manager](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-the-workspace"></a><span data-ttu-id="93cd1-165">Modification ou suppression de l’espace de travail</span><span class="sxs-lookup"><span data-stu-id="93cd1-165">Edit or delete the workspace</span></span>
<span data-ttu-id="93cd1-166">Vous pouvez modifier ou supprimer l’espace de travail configuré via le volet de **vue d’ensemble de Service Map** (volet **Administration** > **Operations Management Suite** > **Service Map**).</span><span class="sxs-lookup"><span data-stu-id="93cd1-166">You can edit or delete the configured workspace through the **Service Map Overview** pane (**Administration** pane > **Operations Management Suite** > **Service Map**).</span></span> <span data-ttu-id="93cd1-167">Vous ne pouvez configurer qu’un seul espace de travail Operations Management Suite pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="93cd1-167">You can configure only one Operations Management Suite workspace for now.</span></span>

![Volet de modification de l’espace de travail d’Operations Manager](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a><span data-ttu-id="93cd1-169">Configuration des règles et des valeurs de remplacement</span><span class="sxs-lookup"><span data-stu-id="93cd1-169">Configure rules and overrides</span></span>
<span data-ttu-id="93cd1-170">Une règle _Microsoft.SystemCenter.ServiceMapImport.Rule_ est créée pour extraire régulièrement des informations de Service Map.</span><span class="sxs-lookup"><span data-stu-id="93cd1-170">A rule, _Microsoft.SystemCenter.ServiceMapImport.Rule_, is created to periodically fetch information from Service Map.</span></span> <span data-ttu-id="93cd1-171">Pour modifier les intervalles de synchronisation, vous pouvez configurer des valeurs de remplacement pour la règle (volet **Création** > **Règles** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span><span class="sxs-lookup"><span data-stu-id="93cd1-171">To change sync timings, you can configure overrides of the rule (**Authoring** pane > **Rules** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span></span>

![Fenêtre des propriétés des valeurs de remplacement Operations Manager](media/oms-service-map/scom-overrides.png)

* <span data-ttu-id="93cd1-173">**Enabled** : activer ou désactiver les mises à jour automatiques.</span><span class="sxs-lookup"><span data-stu-id="93cd1-173">**Enabled**: Enable or disable automatic updates.</span></span> 
* <span data-ttu-id="93cd1-174">**IntervalMinutes** : réinitialiser la durée entre les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="93cd1-174">**IntervalMinutes**: Reset the time between updates.</span></span> <span data-ttu-id="93cd1-175">L’intervalle par défaut est égal à une heure.</span><span class="sxs-lookup"><span data-stu-id="93cd1-175">The default interval is one hour.</span></span> <span data-ttu-id="93cd1-176">Si vous voulez synchroniser les mappages de serveurs plus régulièrement, vous pouvez modifier la valeur.</span><span class="sxs-lookup"><span data-stu-id="93cd1-176">If you want to sync server maps more frequently, you can change the value.</span></span>
* <span data-ttu-id="93cd1-177">**TimeoutSeconds** : réinitialiser la durée avant l’expiration de la demande.</span><span class="sxs-lookup"><span data-stu-id="93cd1-177">**TimeoutSeconds**: Reset the length of time before the request times out.</span></span> 
* <span data-ttu-id="93cd1-178">**TimeWindowMinutes** : réinitialiser la fenêtre de temps pour l’interrogation des données.</span><span class="sxs-lookup"><span data-stu-id="93cd1-178">**TimeWindowMinutes**: Reset the time window for querying data.</span></span> <span data-ttu-id="93cd1-179">Valeur par défaut : fenêtre de 60 minutes.</span><span class="sxs-lookup"><span data-stu-id="93cd1-179">Default is a 60-minute window.</span></span> <span data-ttu-id="93cd1-180">La valeur maximale autorisée par Service Map est de 60 minutes.</span><span class="sxs-lookup"><span data-stu-id="93cd1-180">The maximum value allowed by Service Map is 60 minutes.</span></span>

## <a name="known-issues-and-limitations"></a><span data-ttu-id="93cd1-181">Problèmes connus et limitations</span><span class="sxs-lookup"><span data-stu-id="93cd1-181">Known issues and limitations</span></span>

<span data-ttu-id="93cd1-182">La conception actuelle présente les problèmes et les limitations suivants :</span><span class="sxs-lookup"><span data-stu-id="93cd1-182">The current design presents the following issues and limitations:</span></span>
* <span data-ttu-id="93cd1-183">Vous ne pouvez vous connecter qu’à un seul espace de travail Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="93cd1-183">You can only connect to a single Operations Management Suite workspace.</span></span>
* <span data-ttu-id="93cd1-184">Bien que vous puissiez ajouter des serveurs au Groupe de serveurs Service Map manuellement via le volet **Création**, les mappages de ces serveurs sont synchronisés immédiatement.</span><span class="sxs-lookup"><span data-stu-id="93cd1-184">Although you can add servers to the Service Map Servers Group manually through the **Authoring** pane, the maps for those servers are not synced immediately.</span></span>  <span data-ttu-id="93cd1-185">Ils seront synchronisés à partir de Service Map lors du prochain cycle de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="93cd1-185">They will be synced from Service Map during the next sync cycle.</span></span>
* <span data-ttu-id="93cd1-186">Si vous apportez des modifications aux diagrammes d’application distribuée créée par le pack d’administration, ces modifications sont probablement remplacées dans la prochaine synchronisation avec Service Map.</span><span class="sxs-lookup"><span data-stu-id="93cd1-186">If you make any changes to the Distributed Application Diagrams created by the management pack, those changes will likely be overwritten on the next sync with Service Map.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="93cd1-187">Créer un principal du service</span><span class="sxs-lookup"><span data-stu-id="93cd1-187">Create a service principal</span></span>
<span data-ttu-id="93cd1-188">Pour obtenir une documentation Azure officielle sur la création d’un principal de service, consultez :</span><span class="sxs-lookup"><span data-stu-id="93cd1-188">For official Azure documentation about creating a service principal, see:</span></span>
* [<span data-ttu-id="93cd1-189">Création d’un principal de service à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="93cd1-189">Create a service principal by using PowerShell</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="93cd1-190">Création d’un principal de service à l’aide d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="93cd1-190">Create a service principal by using Azure CLI</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* [<span data-ttu-id="93cd1-191">Création d’un principal de service à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="93cd1-191">Create a service principal by using the Azure portal</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a><span data-ttu-id="93cd1-192">Commentaires</span><span class="sxs-lookup"><span data-stu-id="93cd1-192">Feedback</span></span>
<span data-ttu-id="93cd1-193">Avez-vous des commentaires à nous transmettre à propos de Service Map ou de sa documentation ?</span><span class="sxs-lookup"><span data-stu-id="93cd1-193">Do you have any feedback for us about Service Map or this documentation?</span></span> <span data-ttu-id="93cd1-194">Consultez notre [page Voix utilisateur](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map) qui vous permet de suggérer des fonctionnalités ou de voter pour les suggestions en cours.</span><span class="sxs-lookup"><span data-stu-id="93cd1-194">Visit our [User Voice page](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), where you can suggest features or vote on existing suggestions.</span></span>
