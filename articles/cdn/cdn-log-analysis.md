---
title: "analyse d’aaaLog d’Azure CDN | Documents Microsoft"
description: "Le client peut activer l’analyse des journaux pour Azure CDN."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: v-semcev
ms.openlocfilehash: 56e5a4fec46fd156cf38252732afb4522741d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a><span data-ttu-id="2fb57-103">Journaux de diagnostic pour Azure CDN</span><span class="sxs-lookup"><span data-stu-id="2fb57-103">Diagnostics Logs for Azure CDN</span></span>

<span data-ttu-id="2fb57-104">Après avoir activé le CDN pour votre application, vous serez probablement choix de l’utilisation de toomonitor hello CDN, vérifier l’intégrité de hello de remise de votre et résoudre les problèmes potentiels.</span><span class="sxs-lookup"><span data-stu-id="2fb57-104">After enabling CDN for your application, you will likely want toomonitor hello CDN usage, check hello health of your delivery, and troubleshoot potential issues.</span></span> <span data-ttu-id="2fb57-105">Azure CDN fournit ces fonctionnalités avec [l’Analytique principale CDN](cdn-analyze-usage-patterns.md) et les [journaux de diagnostic](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs).</span><span class="sxs-lookup"><span data-stu-id="2fb57-105">Azure CDN provides these capabilities with [CDN Core Analytics](cdn-analyze-usage-patterns.md) and [Diagnostic Logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span></span>

## <a name="cdn-core-analytics"></a><span data-ttu-id="2fb57-106">Analytique principale CDN</span><span class="sxs-lookup"><span data-stu-id="2fb57-106">CDN Core Analytics</span></span>
<span data-ttu-id="2fb57-107">Comme un utilisateur d’Azure CDN actuel avec Verizon standard ou un profil de premium, vous êtes déjà analytique de noyaux tooview en mesure de dans le portail supplémentaire du hello accessible via l’option de « Gérer » hello de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2fb57-107">As a current Azure CDN user with Verizon standard or premium profile, you are already able tooview core analytics in hello supplemental portal accessible via hello "Manage" option from hello Azure portal.</span></span> 

## <a name="azure-diagnostic-logs"></a><span data-ttu-id="2fb57-108">Journaux de diagnostic Azure</span><span class="sxs-lookup"><span data-stu-id="2fb57-108">Azure Diagnostic Logs</span></span>

<span data-ttu-id="2fb57-109">Avec cette nouvelle fonctionnalité, vous pouvez maintenant afficher l’analytique principale et l’enregistrer dans une ou plusieurs destinations, dont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="2fb57-109">Azure With this new feature, you can now view core analytics and save them into one or more destinations including:</span></span>

 - <span data-ttu-id="2fb57-110">Compte de Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="2fb57-110">Azure Storage account</span></span>
 - <span data-ttu-id="2fb57-111">Hubs d'événements Azure</span><span class="sxs-lookup"><span data-stu-id="2fb57-111">Azure Event Hubs</span></span>
 - [<span data-ttu-id="2fb57-112">Référentiel OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="2fb57-112">OMS Log Analytics repository</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 <span data-ttu-id="2fb57-113">Cette fonctionnalité est disponible pour tous les points de terminaison CDN appartenant tooVerizon (Standard et Premium) et les profils du CDN Akamai (Standard).</span><span class="sxs-lookup"><span data-stu-id="2fb57-113">This feature is available for all CDN endpoints belonging tooVerizon (Standard & Premium) and Akamai (Standard) CDN Profiles.</span></span>

<span data-ttu-id="2fb57-114">Les journaux de diagnostic permettent de tooexport les métriques de l’utilisation de base à partir de votre CDN point de terminaison tooa de diverses sources afin que vous pouvez les utiliser de façon personnalisée.</span><span class="sxs-lookup"><span data-stu-id="2fb57-114">Diagnostics logs allow you tooexport basic usage metrics from your CDN endpoint tooa variety of sources so that you can consume them in a customized way.</span></span> <span data-ttu-id="2fb57-115">Par exemple, vous pouvez effectuer hello les types d’exportation de données suivants :</span><span class="sxs-lookup"><span data-stu-id="2fb57-115">For example, you can do hello following types of data export:</span></span>

- <span data-ttu-id="2fb57-116">Exporter le stockage des données tooblob, exporter tooCSV et générer des graphiques dans excel.</span><span class="sxs-lookup"><span data-stu-id="2fb57-116">Export data tooblob storage, export tooCSV, and generate graphs in excel.</span></span>
- <span data-ttu-id="2fb57-117">Exporter des concentrateurs tooevent de données et mettre en corrélation avec des données provenant d’autres services azure.</span><span class="sxs-lookup"><span data-stu-id="2fb57-117">Export data tooevent hubs and correlate with data from other azure services.</span></span>
- <span data-ttu-id="2fb57-118">Exporter des données toolog analytique et afficher les données dans votre propre espace de travail OMS</span><span class="sxs-lookup"><span data-stu-id="2fb57-118">Export data toolog analytics and view data in your own OMS work space</span></span>

<span data-ttu-id="2fb57-119">Hello figure suivante montre une vue Analytique de noyaux CDN classique dans les données.</span><span class="sxs-lookup"><span data-stu-id="2fb57-119">hello following figure shows a typical CDN Core Analytics view into data.</span></span>

![Portail - Journaux de diagnostics](./media/cdn-diagnostics-log/01_OMS-workspace.png)

<span data-ttu-id="2fb57-121">*Figure 1 : vue avec l’analytique principale CDN*</span><span class="sxs-lookup"><span data-stu-id="2fb57-121">*Figure 1 - CDN Core Analytics view*</span></span>

<span data-ttu-id="2fb57-122">Hello, procédure pas à pas passe par schéma hello de données analytique de hello core, les étapes impliquées dans l’activation de fonctionnalité de hello et leur remise toovarious destinations et la consommation de ces destinations.</span><span class="sxs-lookup"><span data-stu-id="2fb57-122">hello following walkthrough goes through hello schema of hello core analytics data, steps involved in enabling hello feature and delivering them toovarious destinations, and consuming from these destinations.</span></span>

## <a name="enable-logging-with-azure-portal"></a><span data-ttu-id="2fb57-123">Activation de la journalisation avec le portail Azure</span><span class="sxs-lookup"><span data-stu-id="2fb57-123">Enable logging with Azure portal</span></span>

> [!NOTE]
> <span data-ttu-id="2fb57-124">Hello les journaux de diagnostic sont activés **hors** par défaut.</span><span class="sxs-lookup"><span data-stu-id="2fb57-124">hello diagnostics logs are turned **off** by default.</span></span> 

<span data-ttu-id="2fb57-125">Suivez les étapes de hello ci-après journalisation tooenable avec CDN Core Analytique :</span><span class="sxs-lookup"><span data-stu-id="2fb57-125">Follow hello steps below tooenable logging with CDN Core Analytics:</span></span>

<span data-ttu-id="2fb57-126">Connectez-vous à toohello [portail Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2fb57-126">Sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="2fb57-127">Si vous n’avez pas activé CDN pour votre flux de travail, [activez Azure CDN](cdn-create-new-endpoint.md) avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="2fb57-127">If you don't already have CDN enabled for your workflow, [Enable Azure CDN](cdn-create-new-endpoint.md) before you continue.</span></span>

1. <span data-ttu-id="2fb57-128">Dans le portail de hello, accédez trop**profil CDN**.</span><span class="sxs-lookup"><span data-stu-id="2fb57-128">In hello portal, navigate too**CDN profile**.</span></span>
2. <span data-ttu-id="2fb57-129">Sélectionnez un profil CDN, puis sélectionnez le point de terminaison CDN hello que vous souhaitez tooenable **les journaux de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="2fb57-129">Select a CDN profile, then select hello CDN endpoint that you want tooenable **Diagnostics Logs**.</span></span>

    ![Portail - Journaux de diagnostics](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. <span data-ttu-id="2fb57-131">Accédez trop**les journaux de diagnostic** panneau sous **analyse** section, puis modifier le statut de hello trop**sur**.</span><span class="sxs-lookup"><span data-stu-id="2fb57-131">Go too**Diagnostics Logs** blade Under **Monitoring** section, then change hello status too**On**.</span></span>

    ![Portail - Journaux de diagnostics](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a><span data-ttu-id="2fb57-133">Activation de la journalisation avec Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="2fb57-133">Enable logging with Azure Storage</span></span>
    
<span data-ttu-id="2fb57-134">journaux de hello toostore toouse le stockage Azure, sélectionnez **archiver le compte de stockage tooa**, sélectionnez les jours de rétention, puis cliquez sur **CoreAnalytics** sous **journal**.</span><span class="sxs-lookup"><span data-stu-id="2fb57-134">toouse Azure Storage toostore hello logs, select **Archive tooa storage account**, select retention days, and click **CoreAnalytics** under **Log**.</span></span>

![Portail - Journaux de diagnostics](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

<span data-ttu-id="2fb57-136">*Figure 2 : activation de la journalisation avec Stockage Azure*</span><span class="sxs-lookup"><span data-stu-id="2fb57-136">*Figure 2 - Logging with Azure Storage*</span></span>

### <a name="logging-with-oms-log-analytics"></a><span data-ttu-id="2fb57-137">Journalisation avec OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="2fb57-137">Logging with OMS Log Analytics</span></span>

<span data-ttu-id="2fb57-138">journaux de hello toostore toouse Analytique des journaux OMS, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2fb57-138">toouse OMS Log Analytics toostore hello logs, follow these steps:</span></span>

1. <span data-ttu-id="2fb57-139">À partir de hello **les journaux de diagnostic** panneau sous **analyse**, sélectionnez **envoyer tooLog Analytique** à partir de</span><span class="sxs-lookup"><span data-stu-id="2fb57-139">From hello **Diagnostics Logs** blade Under **Monitoring**, select **Send tooLog Analytics** from</span></span> 

    ![Portail - Journaux de diagnostics](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. <span data-ttu-id="2fb57-141">Configurer l’enregistrement de journal Analytique de hello en cliquant sur Configurer.</span><span class="sxs-lookup"><span data-stu-id="2fb57-141">Configure hello Log Analytics logging by clicking on Configure.</span></span> <span data-ttu-id="2fb57-142">Vous accédez tooa la boîte de dialogue où vous pouvez sélectionner un espace de travail précédent ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="2fb57-142">This takes you tooa dialog where you can select a previous workspace or create a new one.</span></span>

    ![Portail - Journaux de diagnostics](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. <span data-ttu-id="2fb57-144">Cliquez sur **Créer un espace de travail**.</span><span class="sxs-lookup"><span data-stu-id="2fb57-144">Click **Create New Workspace**.</span></span>

    ![Portail - Journaux de diagnostics](./media/cdn-diagnostics-log/07_Create-new.png)

4. <span data-ttu-id="2fb57-146">Ensuite, vous devez sélectionner un nouveau nom d’espace de travail, un abonnement existant, un groupe de ressources (nouveau ou existant), un emplacement et un niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="2fb57-146">Next you must select a new workspace name, existing subscription, resource group (new or existing), location, and pricing tier.</span></span> <span data-ttu-id="2fb57-147">Vous pouvez hello épinglage de ce tableau de bord de tooyour de configuration.</span><span class="sxs-lookup"><span data-stu-id="2fb57-147">You have hello option of pinning this configuration tooyour dashboard.</span></span> <span data-ttu-id="2fb57-148">Cliquez sur OK toocomplete hello configuration.</span><span class="sxs-lookup"><span data-stu-id="2fb57-148">Click OK toocomplete hello configuration.</span></span>

    <span data-ttu-id="2fb57-149">Votre espace de travail doit ensuite apparaître, avec vos noms de groupe de ressources et d’espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="2fb57-149">Next you should see your workspace with your OMS Workspace and Resource group names.</span></span> <span data-ttu-id="2fb57-150">Les noms doivent être uniques et ne peuvent contenir que des lettres, des chiffres et des traits d’union.</span><span class="sxs-lookup"><span data-stu-id="2fb57-150">Names must be unique and can only use letters, numbers, and hyphens.</span></span> <span data-ttu-id="2fb57-151">Les espaces et les traits de soulignement ne sont pas autorisés.</span><span class="sxs-lookup"><span data-stu-id="2fb57-151">Spaces and underscores are not allowed.</span></span> 

    ![Portail - Journaux de diagnostics](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. <span data-ttu-id="2fb57-153">Ensuite, vous obtenez un bref message indiquant que votre espace de travail a été créé et que vous retournez tooyour journalisation de l’écran de configuration.</span><span class="sxs-lookup"><span data-stu-id="2fb57-153">You next get a short message saying that your workspace has been created and you are returned tooyour logging configuration screen.</span></span> <span data-ttu-id="2fb57-154">Vous pouvez vérifier le nom hello de votre espace de travail Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="2fb57-154">You can confirm hello name of your Log Analytics workspace.</span></span>

    ![Portail - Journaux de diagnostics](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    <span data-ttu-id="2fb57-156">Une fois la configuration du journal Analytique hello, assurez-vous que vous également case hello CoreAnalytics pour la journalisation du CDN.</span><span class="sxs-lookup"><span data-stu-id="2fb57-156">Once you have set up hello Log Analytics configuration, make sure you also check hello CoreAnalytics box for CDN logging.</span></span>

6. <span data-ttu-id="2fb57-157">Si tout est tooyour convenance, cliquez sur hello **enregistrer** bouton en haut de hello de boîte de dialogue de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="2fb57-157">If everything is tooyour liking, click hello **Save** button at hello top of hello configuration dialog.</span></span>

    ![Portail - Journaux de diagnostics](./media/cdn-diagnostics-log/10_Save-me.png)

    <span data-ttu-id="2fb57-159">Hello **enregistrer** bouton n’est plus actif et que hello/désactiver le bouton est désormais ON mais bleu au lieu de violet.</span><span class="sxs-lookup"><span data-stu-id="2fb57-159">hello **Save** button is no longer active and that hello ON/OFF button is now ON, but blue instead of purple.</span></span>

7. <span data-ttu-id="2fb57-160">Si vous souhaitez toosee votre nouvel espace de travail OMS, accédez tooyour portail Azure tableau de bord, cliquez sur nom hello votre espace de travail Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="2fb57-160">If you want toosee your new OMS workspace, go tooyour Azure portal Dashboard, click hello name of your Log Analytics workspace.</span></span> <span data-ttu-id="2fb57-161">Ensuite, vous verrez votre espace de travail (Assurez-vous qu’espace de travail OMS est mis en surbrillance sur hello gauche).</span><span class="sxs-lookup"><span data-stu-id="2fb57-161">Next you will see your workspace (make sure that OMS Workspace is highlighted on hello left).</span></span> <span data-ttu-id="2fb57-162">Cliquez sur hello portail OMS vignette toosee votre espace de travail dans le référentiel d’OMS hello.</span><span class="sxs-lookup"><span data-stu-id="2fb57-162">Click on hello OMS Portal tile toosee your workspace in hello OMS repository.</span></span> 

    ![Portail - Journaux de diagnostics](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    <span data-ttu-id="2fb57-164">Votre référentiel OMS est maintenant prêt toolog données.</span><span class="sxs-lookup"><span data-stu-id="2fb57-164">Your OMS repository is now ready toolog data.</span></span> <span data-ttu-id="2fb57-165">Dans commande tooconsume que les données, vous devez utiliser un [Solution OMS](#consuming-oms-log-analytics-data), couvert plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="2fb57-165">In order tooconsume that data, you must use an [OMS Solution](#consuming-oms-log-analytics-data), covered later in this article.</span></span>

<span data-ttu-id="2fb57-166">Vous trouverez plus d’informations sur les retards des données de journal [ici](#log-data-delays).</span><span class="sxs-lookup"><span data-stu-id="2fb57-166">For more information about log data delays, go [here](#log-data-delays).</span></span>

## <a name="enable-logging-with-powershell"></a><span data-ttu-id="2fb57-167">Activation de la journalisation avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fb57-167">Enable logging with PowerShell</span></span>

<span data-ttu-id="2fb57-168">Voici un exemple sur la façon dont les journaux de Diagnostic tooenable et get via hello applets de commande PowerShell Azure.</span><span class="sxs-lookup"><span data-stu-id="2fb57-168">Below is an example on how tooenable and get Diagnostic Logs via hello Azure PowerShell Cmdlets.</span></span>

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a><span data-ttu-id="2fb57-169">Activation des journaux de diagnostic dans un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="2fb57-169">Enabling Diagnostic Logs in a Storage Account</span></span>

<span data-ttu-id="2fb57-170">Commencez par vous connecter et sélectionner un abonnement :</span><span class="sxs-lookup"><span data-stu-id="2fb57-170">First log in and select a subscription:</span></span>

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


<span data-ttu-id="2fb57-171">tooEnable journaux de Diagnostic dans un compte de stockage, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="2fb57-171">tooEnable Diagnostic Logs in a Storage Account, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
<span data-ttu-id="2fb57-172">tooEnable des journaux de Diagnostics dans un espace de travail OMS, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="2fb57-172">tooEnable Diagnostics Logs in an OMS workspace, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a><span data-ttu-id="2fb57-173">Utilisation des journaux de diagnostic à partir de Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="2fb57-173">Consuming diagnostics logs from Azure Storage</span></span>
<span data-ttu-id="2fb57-174">Cette section décrit le schéma hello d’analytique de noyaux hello CDN et comment elles sont organisées à l’intérieur d’un compte de stockage Azure et fournit les journaux de hello de toodownload code exemple dans un fichier CSV tooa.</span><span class="sxs-lookup"><span data-stu-id="2fb57-174">This section describes hello schema of hello CDN core analytics, how these are organized inside of an Azure Storage Account and provides sample code toodownload hello logs in tooa CSV file.</span></span>

### <a name="using-microsoft-azure-storage-explorer"></a><span data-ttu-id="2fb57-175">Utilisation de l’explorateur de stockage Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="2fb57-175">Using Microsoft Azure Storage Explorer</span></span>
<span data-ttu-id="2fb57-176">Vous pouvez accéder aux hello core analytique données hello compte de stockage Azure, vous devez tout d’abord un contenu de hello outil tooaccess dans un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="2fb57-176">Before you can access hello core analytics data from hello Azure Storage Account, you first need a tool tooaccess hello contents in a storage account.</span></span> <span data-ttu-id="2fb57-177">Lorsqu’il existe plusieurs outils disponibles dans le marché de hello, hello un que nous recommandons est hello Microsoft Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="2fb57-177">While there are several tools available in hello market, hello one that we recommend is hello Microsoft Azure Storage Explorer.</span></span> <span data-ttu-id="2fb57-178">Vous pouvez télécharger hello à partir [ici](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="2fb57-178">You can download hello tool from [here](http://storageexplorer.com/).</span></span> <span data-ttu-id="2fb57-179">Une fois le téléchargement et l’installation des logiciels de hello, configurez-le toouse hello même compte de stockage Azure qui a été configuré comme un toohello destination CDN les journaux de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="2fb57-179">After downloading and installing hello software, configure it toouse hello same Azure Storage Account that was configured as a destination toohello CDN Diagnostics Logs.</span></span>

1.  <span data-ttu-id="2fb57-180">Ouvrez **l’explorateur de stockage Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="2fb57-180">Open **Microsoft Azure Storage Explorer**</span></span>
2.  <span data-ttu-id="2fb57-181">Recherchez le compte de stockage hello</span><span class="sxs-lookup"><span data-stu-id="2fb57-181">Locate hello storage account</span></span>
3.  <span data-ttu-id="2fb57-182">Accédez toohello **« Conteneurs d’objets Blob »** nœud sous stockage de ce compte et développez le nœud de hello</span><span class="sxs-lookup"><span data-stu-id="2fb57-182">Go toohello **“Blob Containers”** node under this storage account and expand hello node</span></span>
4.  <span data-ttu-id="2fb57-183">Conteneur de sélection hello nommé **« insights-journaux coreanalytics »** et double-cliquez dessus</span><span class="sxs-lookup"><span data-stu-id="2fb57-183">Select hello container named **“insights-logs-coreanalytics”** and double-click it</span></span>
5.  <span data-ttu-id="2fb57-184">Afficher les résultats sur hello volet de droite en commençant avec hello premier niveau, qui ressemble à **« resourceId = «**.</span><span class="sxs-lookup"><span data-stu-id="2fb57-184">Results show up on hello right-hand pane starting with hello first level, which looks like **“resourceId=”**.</span></span> <span data-ttu-id="2fb57-185">Continuez de cliquer sur tous les moyen de hello jusqu'à ce que vous voyez hello fichier **PT1H.json**.</span><span class="sxs-lookup"><span data-stu-id="2fb57-185">Continue clicking all hello way until you see hello file **PT1H.json**.</span></span> <span data-ttu-id="2fb57-186">Consultez hello Remarque pour une explication du chemin d’accès hello suivante.</span><span class="sxs-lookup"><span data-stu-id="2fb57-186">See hello following note for explanation of hello path.</span></span>
6.  <span data-ttu-id="2fb57-187">Chaque objet blob **PT1H.json** représente hello journaux d’analytique pendant une heure pour un point de terminaison CDN spécifique ou de son domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="2fb57-187">Each blob **PT1H.json** represents hello analytics logs for one hour for a specific CDN endpoint or its custom domain.</span></span>
7.  <span data-ttu-id="2fb57-188">schéma de Hello du contenu hello de ce fichier JSON est décrit dans la section hello schéma Hello Core, Analytique des journaux</span><span class="sxs-lookup"><span data-stu-id="2fb57-188">hello schema of hello contents of this JSON file is described in hello section Schema of hello Core Analytics Logs</span></span>


> [!NOTE]
> <span data-ttu-id="2fb57-189">**Format du chemin d’accès des objets blob**</span><span class="sxs-lookup"><span data-stu-id="2fb57-189">**Blob path format**</span></span>
> 
> <span data-ttu-id="2fb57-190">Les journaux Core Analytics sont générés toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="2fb57-190">Core Analytics logs are generated every hour.</span></span> <span data-ttu-id="2fb57-191">Toutes les données pendant une heure sont collectées et stockées à l’intérieur d’un objet blob Azure en tant que charge utile JSON.</span><span class="sxs-lookup"><span data-stu-id="2fb57-191">All data for an hour are collected and stored inside a single Azure Blob as a JSON payload.</span></span> <span data-ttu-id="2fb57-192">chemin d’accès de Hello toothis objets Blob Azure apparaît comme s’il est une structure hiérarchique.</span><span class="sxs-lookup"><span data-stu-id="2fb57-192">hello path toothis Azure Blob appears as if there is a hierarchical structure.</span></span> <span data-ttu-id="2fb57-193">Étant donné que l’outil Explorateur de stockage hello interprète « / » comme séparateur de répertoires, affiche la hiérarchie de hello pour des raisons pratiques.</span><span class="sxs-lookup"><span data-stu-id="2fb57-193">This is because hello Storage explorer tool interprets '/' as a directory separator and shows hello hierarchy for convenience.</span></span> <span data-ttu-id="2fb57-194">En fait, chemin d’accès complet de hello représente simplement des nom d’objet blob hello.</span><span class="sxs-lookup"><span data-stu-id="2fb57-194">Actually, hello whole path just represents hello blob name.</span></span> <span data-ttu-id="2fb57-195">Ce nom d’objet blob de hello suit hello respectent les conventions d’affectation de noms</span><span class="sxs-lookup"><span data-stu-id="2fb57-195">This name of hello blob follows hello following naming convention</span></span> 
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

<span data-ttu-id="2fb57-196">**Description des champs :**</span><span class="sxs-lookup"><span data-stu-id="2fb57-196">**Description of fields:**</span></span>

|<span data-ttu-id="2fb57-197">value</span><span class="sxs-lookup"><span data-stu-id="2fb57-197">value</span></span>|<span data-ttu-id="2fb57-198">description</span><span class="sxs-lookup"><span data-stu-id="2fb57-198">description</span></span>|
|-------|---------|
|<span data-ttu-id="2fb57-199">Identifiant d’abonnement</span><span class="sxs-lookup"><span data-stu-id="2fb57-199">Subscription ID</span></span>    |<span data-ttu-id="2fb57-200">ID de hello abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="2fb57-200">ID of hello Azure Subscription.</span></span> <span data-ttu-id="2fb57-201">Il est au format de Guid hello.</span><span class="sxs-lookup"><span data-stu-id="2fb57-201">This is in hello Guid format.</span></span>|
|<span data-ttu-id="2fb57-202">Ressource</span><span class="sxs-lookup"><span data-stu-id="2fb57-202">Resource</span></span> |<span data-ttu-id="2fb57-203">Nom de groupe de ressources du CDN hello toowhich groupe de ressources hello appartient.</span><span class="sxs-lookup"><span data-stu-id="2fb57-203">Group Name   Name of hello resource group toowhich hello CDN resources belong.</span></span>|
|<span data-ttu-id="2fb57-204">Nom de profil</span><span class="sxs-lookup"><span data-stu-id="2fb57-204">Profile Name</span></span> |<span data-ttu-id="2fb57-205">Nom de hello profil CDN</span><span class="sxs-lookup"><span data-stu-id="2fb57-205">Name of hello CDN Profile</span></span>|
|<span data-ttu-id="2fb57-206">Nom du point de terminaison</span><span class="sxs-lookup"><span data-stu-id="2fb57-206">Endpoint Name</span></span> |<span data-ttu-id="2fb57-207">Nom du point de terminaison CDN de hello</span><span class="sxs-lookup"><span data-stu-id="2fb57-207">Name of hello CDN Endpoint</span></span>|
|<span data-ttu-id="2fb57-208">Year</span><span class="sxs-lookup"><span data-stu-id="2fb57-208">Year</span></span>|  <span data-ttu-id="2fb57-209">représentation sous forme de 4 chiffres de l’année hello 2017, par exemple,</span><span class="sxs-lookup"><span data-stu-id="2fb57-209">4-digit representation of hello year for example, 2017</span></span>|
|<span data-ttu-id="2fb57-210">Mois</span><span class="sxs-lookup"><span data-stu-id="2fb57-210">Month</span></span>| <span data-ttu-id="2fb57-211">représentation sous forme de 2 chiffres du numéro du mois hello.</span><span class="sxs-lookup"><span data-stu-id="2fb57-211">2-digit representation of hello month number.</span></span> <span data-ttu-id="2fb57-212">01 = Janvier ... 12 = Décembre</span><span class="sxs-lookup"><span data-stu-id="2fb57-212">01=January ... 12=December</span></span>|
|<span data-ttu-id="2fb57-213">jour</span><span class="sxs-lookup"><span data-stu-id="2fb57-213">Day</span></span>|   <span data-ttu-id="2fb57-214">représentation sous forme de 2 chiffres de la journée hello du mois de hello</span><span class="sxs-lookup"><span data-stu-id="2fb57-214">2 digit representation of hello day of hello month</span></span>|
|<span data-ttu-id="2fb57-215">PT1H.json</span><span class="sxs-lookup"><span data-stu-id="2fb57-215">PT1H.json</span></span>| <span data-ttu-id="2fb57-216">Fichier JSON réel où sont stockées les données d’analytique hello</span><span class="sxs-lookup"><span data-stu-id="2fb57-216">Actual JSON file where hello analytics data is stored</span></span>|

### <a name="exporting-hello-core-analytics-data-tooa-csv-file"></a><span data-ttu-id="2fb57-217">Exportation de données Analytique de noyaux de hello tooa fichier CSV</span><span class="sxs-lookup"><span data-stu-id="2fb57-217">Exporting hello Core Analytics Data tooa CSV File</span></span>

<span data-ttu-id="2fb57-218">toomake informatique tooaccess facile hello Core Analytique, nous fournissons un exemple de code pour un outil qui permet de télécharger les fichiers JSON hello au format de fichier de plat séparées par des virgules, qui peut être utilisé tooeasily créer des graphiques ou autres agrégations.</span><span class="sxs-lookup"><span data-stu-id="2fb57-218">toomake it easy tooaccess hello Core Analytics, we provide a sample code for a tool, which allows downloading hello JSON files into a flat comma-separated file format, which can be used tooeasily create charts or other aggregations.</span></span>

<span data-ttu-id="2fb57-219">Voici comment vous pouvez utiliser l’outil de hello :</span><span class="sxs-lookup"><span data-stu-id="2fb57-219">Here is how you can use hello tool:</span></span>

1.  <span data-ttu-id="2fb57-220">Lien de github hello : [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span><span class="sxs-lookup"><span data-stu-id="2fb57-220">Visit hello github link: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv ](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span></span>
2.  <span data-ttu-id="2fb57-221">Télécharger le code de hello</span><span class="sxs-lookup"><span data-stu-id="2fb57-221">Download hello code</span></span>
3.  <span data-ttu-id="2fb57-222">Suivez les instructions toocompile et configurer</span><span class="sxs-lookup"><span data-stu-id="2fb57-222">Follow instructions toocompile and configure</span></span>
4.  <span data-ttu-id="2fb57-223">Exécutez l’outil de hello</span><span class="sxs-lookup"><span data-stu-id="2fb57-223">Run hello tool</span></span>
5.  <span data-ttu-id="2fb57-224">Fichier CSV résultant affiche les données d’analytique hello dans une hiérarchie de plate simple.</span><span class="sxs-lookup"><span data-stu-id="2fb57-224">Resulting CSV file shows hello analytics data in a simple flat hierarchy.</span></span>

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a><span data-ttu-id="2fb57-225">Utilisation des journaux de diagnostics à partir d’un référentiel OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="2fb57-225">Consuming diagnostics logs from an OMS Log Analytics repository</span></span>
<span data-ttu-id="2fb57-226">Analytique de journal est un service dans Operations Management Suite (OMS) qui surveille votre toomaintain environnements locaux et cloud leur disponibilité et les performances.</span><span class="sxs-lookup"><span data-stu-id="2fb57-226">Log Analytics is a service in Operations Management Suite (OMS) that monitors your cloud and on-premises environments toomaintain their availability and performance.</span></span> <span data-ttu-id="2fb57-227">Il collecte les données générées par les ressources dans vos environnements locaux et cloud et à partir d’autres analyses de tooprovide outils analyse à plusieurs sources.</span><span class="sxs-lookup"><span data-stu-id="2fb57-227">It collects data generated by resources in your cloud and on-premises environments and from other monitoring tools tooprovide analysis across multiple sources.</span></span> 

<span data-ttu-id="2fb57-228">toouse Analytique de journal, vous devez [activer la journalisation](#enable-logging-with-azure-storage) référentiel toohello Analytique de journal Azure OMS, qui est décrite plus haut dans cet article.</span><span class="sxs-lookup"><span data-stu-id="2fb57-228">toouse Log Analytics, you must [enable logging](#enable-logging-with-azure-storage) toohello Azure OMS Log Analytics repository, which is discussed earlier in this article.</span></span>

### <a name="using-hello-oms-repository"></a><span data-ttu-id="2fb57-229">À l’aide de hello référentiel OMS</span><span class="sxs-lookup"><span data-stu-id="2fb57-229">Using hello OMS Repository</span></span>

 <span data-ttu-id="2fb57-230">Hello suivant schéma montre l’architecture hello d’entrées de hello et les sorties de référentiel de hello :</span><span class="sxs-lookup"><span data-stu-id="2fb57-230">hello following diagram shows hello architecture of hello inputs and outputs of hello repository:</span></span>

![Référentiel OMS Log Analytics](./media/cdn-diagnostics-log/12_Repo-overview.png)

<span data-ttu-id="2fb57-232">*Figure 3 : référentiel OMS Log Analytics*</span><span class="sxs-lookup"><span data-stu-id="2fb57-232">*Figure 3 - Log Analytics Repository*</span></span>

<span data-ttu-id="2fb57-233">Vous pouvez afficher les données de salutation de manières différentes à l’aide de Solutions de gestion.</span><span class="sxs-lookup"><span data-stu-id="2fb57-233">You can display hello data in a variety of ways by using Management Solutions.</span></span> <span data-ttu-id="2fb57-234">Vous pouvez obtenir des Solutions de gestion à partir de hello [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span><span class="sxs-lookup"><span data-stu-id="2fb57-234">You can obtain Management Solutions from hello [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span></span>

<span data-ttu-id="2fb57-235">Vous pouvez installer des solutions de gestion à partir d’Azure marketplace en cliquant sur hello **maintenant** lien en bas de hello de chaque solution.</span><span class="sxs-lookup"><span data-stu-id="2fb57-235">You can install management solutions from Azure marketplace by clicking hello **Get it now** link at hello bottom of each solution.</span></span>

### <a name="adding-an-oms-cdn-management-solution"></a><span data-ttu-id="2fb57-236">Ajout d’une solution de gestion CDN d’OMS</span><span class="sxs-lookup"><span data-stu-id="2fb57-236">Adding an OMS CDN Management Solution</span></span>

<span data-ttu-id="2fb57-237">Suivez ces étapes de tooadd une Solution de gestion :</span><span class="sxs-lookup"><span data-stu-id="2fb57-237">Follow these steps tooadd a Management Solution:</span></span>

1.   <span data-ttu-id="2fb57-238">Si vous n’avez pas déjà fait, connectez-vous toohello portail Azure à l’aide de votre abonnement Azure et accédez tooyour du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="2fb57-238">If you haven't already done so, sign in toohello Azure portal using your Azure subscription and go tooyour Dashboard.</span></span>
    <span data-ttu-id="2fb57-239">![Tableau de bord Azure](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="2fb57-239">![Azure Dashboard](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span></span>

2. <span data-ttu-id="2fb57-240">Bonjour **nouveau** panneau sous **Marketplace**, sélectionnez **analyse + gestion**.</span><span class="sxs-lookup"><span data-stu-id="2fb57-240">In hello **New** blade under **Marketplace**, select **Monitoring + management**.</span></span>

    ![Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. <span data-ttu-id="2fb57-242">Bonjour **analyse + gestion** panneau, cliquez sur **afficher tous les**.</span><span class="sxs-lookup"><span data-stu-id="2fb57-242">In hello **Monitoring + management** blade, click **See all**.</span></span>

    ![Afficher tout](./media/cdn-diagnostics-log/15_See-all.png)

4.  <span data-ttu-id="2fb57-244">Recherchez le CDN dans la zone de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="2fb57-244">Search for CDN in hello search box.</span></span>

    ![Afficher tout](./media/cdn-diagnostics-log/16_Search-for.png)

5.  <span data-ttu-id="2fb57-246">Sélectionnez **Analytique principale Azure CDN**.</span><span class="sxs-lookup"><span data-stu-id="2fb57-246">Select **Azure CDN Core Analytics**.</span></span> 

    ![Afficher tout](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  <span data-ttu-id="2fb57-248">Après avoir cliqué sur **créer**, vous serez invité toocreate un espace de travail OMS ou utilisez-en un existant.</span><span class="sxs-lookup"><span data-stu-id="2fb57-248">After clicking **Create**, you will be asked toocreate a new OMS workspace or use an existing one.</span></span> 

    ![Afficher tout](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  <span data-ttu-id="2fb57-250">Sélectionnez l’espace de travail hello créé avant.</span><span class="sxs-lookup"><span data-stu-id="2fb57-250">Select hello workspace you created before.</span></span> <span data-ttu-id="2fb57-251">Vous devez ensuite tooadd un compte automation.</span><span class="sxs-lookup"><span data-stu-id="2fb57-251">You then need tooadd an automation account.</span></span>

    ![Afficher tout](./media/cdn-diagnostics-log/19_Add-automation.png)

8. <span data-ttu-id="2fb57-253">Hello d’écran suivante affiche hello automation compte formulaire que vous devez remplir.</span><span class="sxs-lookup"><span data-stu-id="2fb57-253">hello following screen shows hello automation account form you must fill out.</span></span> 

    ![Afficher tout](./media/cdn-diagnostics-log/20_Automation.png)

9. <span data-ttu-id="2fb57-255">Une fois que vous avez créé le compte d’automatisation hello, vous êtes prêt tooadd votre solution.</span><span class="sxs-lookup"><span data-stu-id="2fb57-255">Once you have created hello automation account, you are ready tooadd your solution.</span></span> <span data-ttu-id="2fb57-256">Cliquez sur hello **créer** bouton.</span><span class="sxs-lookup"><span data-stu-id="2fb57-256">Click hello **Create** button.</span></span>

    ![Afficher tout](./media/cdn-diagnostics-log/21_Ready.png)

10. <span data-ttu-id="2fb57-258">Espace de travail tooyour a maintenant été ajoutée à votre solution.</span><span class="sxs-lookup"><span data-stu-id="2fb57-258">Your solution has now been added tooyour workspace.</span></span> <span data-ttu-id="2fb57-259">Revenir en arrière tooyour du tableau de bord de portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2fb57-259">Go back tooyour Azure portal Dashboard.</span></span>

    ![Afficher tout](./media/cdn-diagnostics-log/22_Dashboard.png)

    <span data-ttu-id="2fb57-261">Cliquez sur hello Analytique de journal espace de travail créé toogo tooyour espace de travail.</span><span class="sxs-lookup"><span data-stu-id="2fb57-261">Click hello Log Analytics workspace you created toogo tooyour workspace.</span></span> 

11. <span data-ttu-id="2fb57-262">Cliquez sur hello **portail OMS** vignette toosee votre nouvelle solution dans le portail OMS est hello.</span><span class="sxs-lookup"><span data-stu-id="2fb57-262">Click hello **OMS Portal** tile toosee your new solution in hello OMS portal.</span></span>

    ![Afficher tout](./media/cdn-diagnostics-log/23_workspace.png)

12. <span data-ttu-id="2fb57-264">Votre portail OMS doit maintenant ressembler à hello suivant d’écran :</span><span class="sxs-lookup"><span data-stu-id="2fb57-264">Your OMS portal should now look like hello following screen:</span></span>

    ![Afficher tout](./media/cdn-diagnostics-log/24_OMS-solution.png)

    <span data-ttu-id="2fb57-266">Cliquez sur une de hello vignettes toosee plusieurs vues de vos données.</span><span class="sxs-lookup"><span data-stu-id="2fb57-266">Click one of hello tiles toosee several views into your data.</span></span>

    ![Afficher tout](./media/cdn-diagnostics-log/25_Interior-view.png)

    <span data-ttu-id="2fb57-268">Vous pouvez faire défiler à gauche ou droite toosee davantage les vignettes représentant des vues dans les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="2fb57-268">You can scroll left or right toosee further tiles representing individual views into hello data.</span></span> 

    <span data-ttu-id="2fb57-269">En cliquant sur une des vignettes de hello vous donne plus de détails sur vos données.</span><span class="sxs-lookup"><span data-stu-id="2fb57-269">Clicking one of hello tiles gives you more details about your data.</span></span>

     ![Afficher tout](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a><span data-ttu-id="2fb57-271">Offres et niveaux tarifaires</span><span class="sxs-lookup"><span data-stu-id="2fb57-271">Offers and pricing tiers</span></span>

<span data-ttu-id="2fb57-272">Vous pouvez voir des offres et des niveaux tarifaires pour les solutions de gestion OMS [ici](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span><span class="sxs-lookup"><span data-stu-id="2fb57-272">You can see offers and pricing tiers for OMS management solutions [here](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span></span>

### <a name="customizing-views"></a><span data-ttu-id="2fb57-273">Personnalisation des vues</span><span class="sxs-lookup"><span data-stu-id="2fb57-273">Customizing views</span></span>

<span data-ttu-id="2fb57-274">Vous pouvez personnaliser hello afficher vos données à l’aide de hello **Concepteur de vue**.</span><span class="sxs-lookup"><span data-stu-id="2fb57-274">You can customize hello view into your data by using hello **View Designer**.</span></span> <span data-ttu-id="2fb57-275">Atteindre l’espace de travail OMS tooyour et commencez à créer en cliquant sur hello **Concepteur de vue** vignette.</span><span class="sxs-lookup"><span data-stu-id="2fb57-275">Go tooyour OMS workspace and begin designing by clicking hello **View Designer** tile.</span></span>

![Concepteur de vues](./media/cdn-diagnostics-log/27_Designer.png)

<span data-ttu-id="2fb57-277">Vous pouvez faire glisser et supprimer les types de graphiques de hello gauche et renseignez hello données détails tooanalyze sur hello gauche.</span><span class="sxs-lookup"><span data-stu-id="2fb57-277">You can drag and drop types of charts from hello left and fill in hello data details you want tooanalyze on hello left.</span></span>

![Concepteur de vues](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a><span data-ttu-id="2fb57-279">Retards des données de journal</span><span class="sxs-lookup"><span data-stu-id="2fb57-279">Log data delays</span></span>

<span data-ttu-id="2fb57-280">Retards des données de journal Verizon</span><span class="sxs-lookup"><span data-stu-id="2fb57-280">Verizon log data delays</span></span> | <span data-ttu-id="2fb57-281">Retards des données de journal Akamai</span><span class="sxs-lookup"><span data-stu-id="2fb57-281">Akamai log data delays</span></span>
--- | ---
<span data-ttu-id="2fb57-282">Les données de journal Verizon sont retardées de 1 heure et prennent toostart d’heures too2 qui apparaissent après l’achèvement de la propagation de point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="2fb57-282">Verizon log data is 1 hour delayed, and take up too2 hours toostart appearing after endpoint propagation completion.</span></span> | <span data-ttu-id="2fb57-283">Les données de journal Akamai sont retardées de 24 heures et occupe toostart d’heures too2 apparaissant si elle a été créé il y a plus de 24 heures.</span><span class="sxs-lookup"><span data-stu-id="2fb57-283">Akamai log data is 24 hours delayed, and takes up too2 hours toostart appearing if it was created more than 24 hours ago.</span></span> <span data-ttu-id="2fb57-284">Si elle a été créé récemment, peut prendre des heures de too25 pour toostart de journaux hello qui apparaissent.</span><span class="sxs-lookup"><span data-stu-id="2fb57-284">If it was recently created, it can take up too25 hours for hello logs toostart appearing.</span></span>

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a><span data-ttu-id="2fb57-285">Types de journaux de diagnostic pour l’analytique principale CDN</span><span class="sxs-lookup"><span data-stu-id="2fb57-285">Diagnostic log types for CDN Core Analytics</span></span>

<span data-ttu-id="2fb57-286">Nous proposons actuellement uniquement Core Analytique des journaux, qui contiennent des métriques affichant les statistiques de réponse HTTP et sortie comme hello CDN POP/bords.</span><span class="sxs-lookup"><span data-stu-id="2fb57-286">We currently offer only Core Analytics logs, which contain metrics showing HTTP response statistics and egress statistics as seen from hello CDN POPs/edges.</span></span>

### <a name="core-analytics-metrics-details"></a><span data-ttu-id="2fb57-287">Détails des métriques de Core Analytics</span><span class="sxs-lookup"><span data-stu-id="2fb57-287">Core Analytics Metrics Details</span></span>
<span data-ttu-id="2fb57-288">Hello tableau suivant affiche une liste des mesures disponibles dans hello que Core Analytique se connecte.</span><span class="sxs-lookup"><span data-stu-id="2fb57-288">hello following table shows a list of metrics available in hello Core Analytics logs.</span></span> <span data-ttu-id="2fb57-289">Toutes les métriques ne sont pas disponibles auprès tous les fournisseurs, même si ces différences sont minimes.</span><span class="sxs-lookup"><span data-stu-id="2fb57-289">Not all metrics are available from all providers, although such differences are minimal.</span></span> <span data-ttu-id="2fb57-290">Hello tableau suivant également indique si une mesure donnée est disponible à partir d’un fournisseur.</span><span class="sxs-lookup"><span data-stu-id="2fb57-290">hello following table also shows if a given metric is available from a provider.</span></span> <span data-ttu-id="2fb57-291">Veuillez noter que les métriques de hello sont disponibles pour uniquement ces points de terminaison CDN que le trafic sur ces derniers.</span><span class="sxs-lookup"><span data-stu-id="2fb57-291">Please note that hello metrics are available for only those CDN endpoints that have traffic on them.</span></span>


|<span data-ttu-id="2fb57-292">Mesure</span><span class="sxs-lookup"><span data-stu-id="2fb57-292">Metric</span></span>                     | <span data-ttu-id="2fb57-293">Description</span><span class="sxs-lookup"><span data-stu-id="2fb57-293">Description</span></span>   | <span data-ttu-id="2fb57-294">Verizon</span><span class="sxs-lookup"><span data-stu-id="2fb57-294">Verizon</span></span>  | <span data-ttu-id="2fb57-295">Akamai</span><span class="sxs-lookup"><span data-stu-id="2fb57-295">Akamai</span></span> 
|---------------------------|---------------|---|---|
| <span data-ttu-id="2fb57-296">RequestCountTotal</span><span class="sxs-lookup"><span data-stu-id="2fb57-296">RequestCountTotal</span></span>         |<span data-ttu-id="2fb57-297">Nombre total d’occurrences de requêtes pendant cette période</span><span class="sxs-lookup"><span data-stu-id="2fb57-297">Total number of request hits during this period</span></span>| <span data-ttu-id="2fb57-298">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-298">Yes</span></span>  |<span data-ttu-id="2fb57-299">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-299">Yes</span></span>   |
| <span data-ttu-id="2fb57-300">RequestCountHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="2fb57-300">RequestCountHttpStatus2xx</span></span> |<span data-ttu-id="2fb57-301">Nombre de toutes les requêtes qui ont abouti à un code 2xx (par ex. 200, 202)</span><span class="sxs-lookup"><span data-stu-id="2fb57-301">Count of all requests that resulted in a 2xx HTTP code (e.g. 200, 202)</span></span>              | <span data-ttu-id="2fb57-302">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-302">Yes</span></span>  |<span data-ttu-id="2fb57-303">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-303">Yes</span></span>   |
| <span data-ttu-id="2fb57-304">RequestCountHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="2fb57-304">RequestCountHttpStatus3xx</span></span> | <span data-ttu-id="2fb57-305">Nombre de toutes les requêtes qui ont abouti à un code 3xx (par ex. 300, 302)</span><span class="sxs-lookup"><span data-stu-id="2fb57-305">Count of all requests that resulted in a 3xx HTTP code (e.g. 300, 302)</span></span>              | <span data-ttu-id="2fb57-306">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-306">Yes</span></span>  |<span data-ttu-id="2fb57-307">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-307">Yes</span></span>   |
| <span data-ttu-id="2fb57-308">RequestCountHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="2fb57-308">RequestCountHttpStatus4xx</span></span> |<span data-ttu-id="2fb57-309">Nombre de toutes les requêtes qui ont abouti à un code 4xx (par ex. 400, 404)</span><span class="sxs-lookup"><span data-stu-id="2fb57-309">Count of all requests that resulted in a 4xx HTTP code (e.g. 400, 404)</span></span>               | <span data-ttu-id="2fb57-310">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-310">Yes</span></span>   |<span data-ttu-id="2fb57-311">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-311">Yes</span></span>   |
| <span data-ttu-id="2fb57-312">RequestCountHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="2fb57-312">RequestCountHttpStatus5xx</span></span> | <span data-ttu-id="2fb57-313">Nombre de toutes les requêtes qui ont abouti à un code 5xx (par ex. 500, 504)</span><span class="sxs-lookup"><span data-stu-id="2fb57-313">Count of all requests that resulted in a 5xx HTTP code (e.g. 500, 504)</span></span>              | <span data-ttu-id="2fb57-314">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-314">Yes</span></span>  |<span data-ttu-id="2fb57-315">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-315">Yes</span></span>   |
| <span data-ttu-id="2fb57-316">RequestCountHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="2fb57-316">RequestCountHttpStatusOthers</span></span> |  <span data-ttu-id="2fb57-317">Nombre d’occurrences de tous les autres codes HTTP (en dehors de 2xx-5xx)</span><span class="sxs-lookup"><span data-stu-id="2fb57-317">Count of all other HTTP codes (outside of 2xx-5xx)</span></span> | <span data-ttu-id="2fb57-318">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-318">Yes</span></span>  |<span data-ttu-id="2fb57-319">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-319">Yes</span></span>   |
| <span data-ttu-id="2fb57-320">RequestCountHttpStatus200</span><span class="sxs-lookup"><span data-stu-id="2fb57-320">RequestCountHttpStatus200</span></span> | <span data-ttu-id="2fb57-321">Nombre de toutes les requêtes qui ont abouti au code de réponse HTTP 200</span><span class="sxs-lookup"><span data-stu-id="2fb57-321">Count of all requests that resulted in a 200 HTTP code response</span></span>              |<span data-ttu-id="2fb57-322">Non</span><span class="sxs-lookup"><span data-stu-id="2fb57-322">No</span></span>   |<span data-ttu-id="2fb57-323">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-323">Yes</span></span>   |
| <span data-ttu-id="2fb57-324">RequestCountHttpStatus206</span><span class="sxs-lookup"><span data-stu-id="2fb57-324">RequestCountHttpStatus206</span></span> | <span data-ttu-id="2fb57-325">Nombre de toutes les requêtes qui ont abouti au code de réponse HTTP 206</span><span class="sxs-lookup"><span data-stu-id="2fb57-325">Count of all requests that resulted in a 206 HTTP code response</span></span>              |<span data-ttu-id="2fb57-326">Non</span><span class="sxs-lookup"><span data-stu-id="2fb57-326">No</span></span>   |<span data-ttu-id="2fb57-327">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-327">Yes</span></span>   |
| <span data-ttu-id="2fb57-328">RequestCountHttpStatus302</span><span class="sxs-lookup"><span data-stu-id="2fb57-328">RequestCountHttpStatus302</span></span> | <span data-ttu-id="2fb57-329">Nombre de toutes les requêtes qui ont abouti au code de réponse HTTP 302</span><span class="sxs-lookup"><span data-stu-id="2fb57-329">Count of all requests that resulted in a 302 HTTP code response</span></span>              |<span data-ttu-id="2fb57-330">Non</span><span class="sxs-lookup"><span data-stu-id="2fb57-330">No</span></span>   |<span data-ttu-id="2fb57-331">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-331">Yes</span></span>   |
| <span data-ttu-id="2fb57-332">RequestCountHttpStatus304</span><span class="sxs-lookup"><span data-stu-id="2fb57-332">RequestCountHttpStatus304</span></span> |  <span data-ttu-id="2fb57-333">Nombre de toutes les requêtes qui ont abouti au code de réponse HTTP 304</span><span class="sxs-lookup"><span data-stu-id="2fb57-333">Count of all requests that resulted in a 304 HTTP code response</span></span>             |<span data-ttu-id="2fb57-334">Non</span><span class="sxs-lookup"><span data-stu-id="2fb57-334">No</span></span>   |<span data-ttu-id="2fb57-335">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-335">Yes</span></span>   |
| <span data-ttu-id="2fb57-336">RequestCountHttpStatus404</span><span class="sxs-lookup"><span data-stu-id="2fb57-336">RequestCountHttpStatus404</span></span> | <span data-ttu-id="2fb57-337">Nombre de toutes les requêtes qui ont abouti au code de réponse HTTP 404</span><span class="sxs-lookup"><span data-stu-id="2fb57-337">Count of all requests that resulted in a 404 HTTP code response</span></span>              |<span data-ttu-id="2fb57-338">Non</span><span class="sxs-lookup"><span data-stu-id="2fb57-338">No</span></span>   |<span data-ttu-id="2fb57-339">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-339">Yes</span></span>   |
| <span data-ttu-id="2fb57-340">RequestCountCacheHit</span><span class="sxs-lookup"><span data-stu-id="2fb57-340">RequestCountCacheHit</span></span> |<span data-ttu-id="2fb57-341">Nombre de toutes les requêtes qui ont abouti à un accès au cache.</span><span class="sxs-lookup"><span data-stu-id="2fb57-341">Count of all requests that resulted in a Cache Hit.</span></span> <span data-ttu-id="2fb57-342">Cela signifie que les actifs hello honorée directement à partir de hello POP toohello Client.</span><span class="sxs-lookup"><span data-stu-id="2fb57-342">This means hello asset was served directly from hello POP toohello Client.</span></span>               | <span data-ttu-id="2fb57-343">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-343">Yes</span></span>  |<span data-ttu-id="2fb57-344">Non</span><span class="sxs-lookup"><span data-stu-id="2fb57-344">No</span></span>   |
| <span data-ttu-id="2fb57-345">RequestCountCacheMiss</span><span class="sxs-lookup"><span data-stu-id="2fb57-345">RequestCountCacheMiss</span></span> | <span data-ttu-id="2fb57-346">Nombre de toutes les requêtes qui ont abouti à un échec de cache.</span><span class="sxs-lookup"><span data-stu-id="2fb57-346">Count of all requests that resulted in a Cache Miss.</span></span> <span data-ttu-id="2fb57-347">Cela signifie que les biens de hello sont introuvable sur le client de toohello hello POP le plus proche et par conséquent, a été récupéré à partir de l’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="2fb57-347">This means hello asset was not found on hello POP closest toohello client, and therefore was retrieved from hello Origin.</span></span>              |<span data-ttu-id="2fb57-348">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-348">Yes</span></span>   | <span data-ttu-id="2fb57-349">Non</span><span class="sxs-lookup"><span data-stu-id="2fb57-349">No</span></span>  |
| <span data-ttu-id="2fb57-350">RequestCountCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="2fb57-350">RequestCountCacheNoCache</span></span> | <span data-ttu-id="2fb57-351">Nombre de toutes les demandes tooan actifs qui ne peuvent pas être mis en cache en raison de la configuration de l’utilisateur tooa sur les bords de hello.</span><span class="sxs-lookup"><span data-stu-id="2fb57-351">Count of all requests tooan asset that are prevented from being cached due tooa user configuration on hello edge.</span></span>              |<span data-ttu-id="2fb57-352">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-352">Yes</span></span>   | <span data-ttu-id="2fb57-353">Non</span><span class="sxs-lookup"><span data-stu-id="2fb57-353">No</span></span>  |
| <span data-ttu-id="2fb57-354">RequestCountCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="2fb57-354">RequestCountCacheUncacheable</span></span> | <span data-ttu-id="2fb57-355">Nombre total de demandes tooassets ne peuvent pas être mis en cache par Cache-Control l’élément multimédia hello et en-têtes, ce qui indiquent qu’il ne doit pas être mis en cache sur un POP ou hello HTTP client arrive à expiration</span><span class="sxs-lookup"><span data-stu-id="2fb57-355">Count of all requests tooassets that are prevented from being cached by hello asset's Cache-Control and Expires headers, which indicate that it should not be cached on a POP or by hello HTTP client</span></span>                |<span data-ttu-id="2fb57-356">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-356">Yes</span></span>   |<span data-ttu-id="2fb57-357">Non</span><span class="sxs-lookup"><span data-stu-id="2fb57-357">No</span></span>   |
| <span data-ttu-id="2fb57-358">RequestCountCacheOthers</span><span class="sxs-lookup"><span data-stu-id="2fb57-358">RequestCountCacheOthers</span></span> | <span data-ttu-id="2fb57-359">Nombre de toutes les requêtes avec un état du cache non traité ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="2fb57-359">Count of all requests with cache status not covered by above.</span></span>              |<span data-ttu-id="2fb57-360">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-360">Yes</span></span>   | <span data-ttu-id="2fb57-361">Non</span><span class="sxs-lookup"><span data-stu-id="2fb57-361">No</span></span>  |
| <span data-ttu-id="2fb57-362">EgressTotal</span><span class="sxs-lookup"><span data-stu-id="2fb57-362">EgressTotal</span></span> | <span data-ttu-id="2fb57-363">Transfert de données sortantes en Go</span><span class="sxs-lookup"><span data-stu-id="2fb57-363">Outbound data transfer in GB</span></span>              |<span data-ttu-id="2fb57-364">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-364">Yes</span></span>   |<span data-ttu-id="2fb57-365">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-365">Yes</span></span>   |
| <span data-ttu-id="2fb57-366">EgressHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="2fb57-366">EgressHttpStatus2xx</span></span> | <span data-ttu-id="2fb57-367">Transfert de données sortantes * pour les réponses avec des codes d’état HTTP 2xx en Go</span><span class="sxs-lookup"><span data-stu-id="2fb57-367">Outbound data transfer* for responses with 2xx HTTP status codes in GB</span></span>            |<span data-ttu-id="2fb57-368">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-368">Yes</span></span>   |<span data-ttu-id="2fb57-369">Non</span><span class="sxs-lookup"><span data-stu-id="2fb57-369">No</span></span>   |
| <span data-ttu-id="2fb57-370">EgressHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="2fb57-370">EgressHttpStatus3xx</span></span> | <span data-ttu-id="2fb57-371">Transfert de données sortantes pour les réponses avec des codes d’état HTTP 3xx en Go</span><span class="sxs-lookup"><span data-stu-id="2fb57-371">Outbound data transfer for responses with 3xx HTTP status codes in GB</span></span>              |<span data-ttu-id="2fb57-372">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-372">Yes</span></span>   |<span data-ttu-id="2fb57-373">Non</span><span class="sxs-lookup"><span data-stu-id="2fb57-373">No</span></span>   |
| <span data-ttu-id="2fb57-374">EgressHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="2fb57-374">EgressHttpStatus4xx</span></span> | <span data-ttu-id="2fb57-375">Transfert de données sortantes pour les réponses avec des codes d’état HTTP 4xx en Go</span><span class="sxs-lookup"><span data-stu-id="2fb57-375">Outbound data transfer for responses with 4xx HTTP status codes in GB</span></span>               |<span data-ttu-id="2fb57-376">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-376">Yes</span></span>   | <span data-ttu-id="2fb57-377">Non</span><span class="sxs-lookup"><span data-stu-id="2fb57-377">No</span></span>  |
| <span data-ttu-id="2fb57-378">EgressHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="2fb57-378">EgressHttpStatus5xx</span></span> | <span data-ttu-id="2fb57-379">Transfert de données sortantes pour les réponses avec des codes d’état HTTP 5xx en Go</span><span class="sxs-lookup"><span data-stu-id="2fb57-379">Outbound data transfer for responses with 5xx HTTP status codes in GB</span></span>               |<span data-ttu-id="2fb57-380">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-380">Yes</span></span>   |  <span data-ttu-id="2fb57-381">Non</span><span class="sxs-lookup"><span data-stu-id="2fb57-381">No</span></span> |
| <span data-ttu-id="2fb57-382">EgressHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="2fb57-382">EgressHttpStatusOthers</span></span> | <span data-ttu-id="2fb57-383">Transfert de données sortantes pour les réponses avec d’autres codes d’état HTTP en Go</span><span class="sxs-lookup"><span data-stu-id="2fb57-383">Outbound data transfer for responses with other HTTP status codes in GB</span></span>                |<span data-ttu-id="2fb57-384">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-384">Yes</span></span>   |<span data-ttu-id="2fb57-385">Non</span><span class="sxs-lookup"><span data-stu-id="2fb57-385">No</span></span>   |
| <span data-ttu-id="2fb57-386">EgressCacheHit</span><span class="sxs-lookup"><span data-stu-id="2fb57-386">EgressCacheHit</span></span> |  <span data-ttu-id="2fb57-387">Transfert de données sortantes pour les réponses qui ont été remis directement à partir du cache CDN hello sur hello CDN POP/bords</span><span class="sxs-lookup"><span data-stu-id="2fb57-387">Outbound data transfer for responses that were delivered directly from hello CDN cache on hello CDN POPs/Edges</span></span>  |<span data-ttu-id="2fb57-388">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-388">Yes</span></span>   |  <span data-ttu-id="2fb57-389">Non</span><span class="sxs-lookup"><span data-stu-id="2fb57-389">No</span></span> |
| <span data-ttu-id="2fb57-390">EgressCacheMiss</span><span class="sxs-lookup"><span data-stu-id="2fb57-390">EgressCacheMiss</span></span> | <span data-ttu-id="2fb57-391">Transfert de données sortantes pour les réponses qui ont été pas été trouvées sur hello plus proche du serveur POP et récupérées à partir du serveur d’origine hello</span><span class="sxs-lookup"><span data-stu-id="2fb57-391">Outbound data transfer for responses that were not found on hello nearest POP server, and retrieved from hello origin server</span></span>              |<span data-ttu-id="2fb57-392">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-392">Yes</span></span>   |  <span data-ttu-id="2fb57-393">Non</span><span class="sxs-lookup"><span data-stu-id="2fb57-393">No</span></span> |
| <span data-ttu-id="2fb57-394">EgressCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="2fb57-394">EgressCacheNoCache</span></span> | <span data-ttu-id="2fb57-395">Transfert de données sortantes pour les ressources qui ne peuvent pas être mis en cache en raison de la configuration de l’utilisateur tooa sur les bords de hello.</span><span class="sxs-lookup"><span data-stu-id="2fb57-395">Outbound data transfer for assets that are prevented from being cached due tooa user configuration on hello edge.</span></span>                |<span data-ttu-id="2fb57-396">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-396">Yes</span></span>   |<span data-ttu-id="2fb57-397">Non</span><span class="sxs-lookup"><span data-stu-id="2fb57-397">No</span></span>   |
| <span data-ttu-id="2fb57-398">EgressCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="2fb57-398">EgressCacheUncacheable</span></span> | <span data-ttu-id="2fb57-399">Transfert de données sortantes pour les ressources qui ne peuvent pas être mis en cache par l’élément multimédia hello Cache-Control et/ou en-têtes expire, ce qui indiquent qu’il ne doit pas être mis en cache sur un POP ou hello HTTP client</span><span class="sxs-lookup"><span data-stu-id="2fb57-399">Outbound data transfer for assets that are prevented from being cached by hello asset's Cache-Control and/or Expires headers, which indicate that it should not be cached on a POP or by hello HTTP client</span></span>                    |<span data-ttu-id="2fb57-400">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-400">Yes</span></span>   | <span data-ttu-id="2fb57-401">Non</span><span class="sxs-lookup"><span data-stu-id="2fb57-401">No</span></span>  |
| <span data-ttu-id="2fb57-402">EgressCacheOthers</span><span class="sxs-lookup"><span data-stu-id="2fb57-402">EgressCacheOthers</span></span> |  <span data-ttu-id="2fb57-403">Transfère les données sortantes pour d’autres scénarios de cache.</span><span class="sxs-lookup"><span data-stu-id="2fb57-403">Outbound data transfers for other cache scenarios.</span></span>             |<span data-ttu-id="2fb57-404">Oui</span><span class="sxs-lookup"><span data-stu-id="2fb57-404">Yes</span></span>   | <span data-ttu-id="2fb57-405">Non</span><span class="sxs-lookup"><span data-stu-id="2fb57-405">No</span></span>  |

<span data-ttu-id="2fb57-406">* Transfert de données sortant fait référence tootraffic remis à partir du client de toohello serveurs serveur POP du CDN.</span><span class="sxs-lookup"><span data-stu-id="2fb57-406">*Outbound data transfer refers tootraffic delivered from CDN POP servers toohello client.</span></span>


### <a name="schema-of-hello-core-analytics-logs"></a><span data-ttu-id="2fb57-407">Schéma de hello Core, Analytique des journaux</span><span class="sxs-lookup"><span data-stu-id="2fb57-407">Schema of hello Core Analytics Logs</span></span> 

<span data-ttu-id="2fb57-408">Tous les journaux sont stockés au format JSON, et chaque entrée comporte des champs de chaîne suivant hello schéma ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2fb57-408">All logs are stored in JSON format and each entry has string fields following hello below schema:</span></span>

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of hello CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of hello domain for which hello statistics is reported>",
                "RequestCountTotal": integer value,
                "RequestCountHttpStatus2xx": integer value,
                "RequestCountHttpStatus3xx": integer value,
                "RequestCountHttpStatus4xx": integer value,
                "RequestCountHttpStatus5xx": integer value,
                "RequestCountHttpStatusOthers": integer value,
                "RequestCountHttpStatus200": integer value,
                "RequestCountHttpStatus206": integer value,
                "RequestCountHttpStatus302": integer value,
                "RequestCountHttpStatus304": integer value,
                "RequestCountHttpStatus404": integer value,
                "RequestCountCacheHit": integer value,
                "RequestCountCacheMiss": integer value,
                "RequestCountCacheNoCache": integer value,
                "RequestCountCacheUncacheable": integer value,
                "RequestCountCacheOthers": integer value,
                "EgressTotal": double value,
                "EgressHttpStatus2xx": double value,
                "EgressHttpStatus3xx": double value,
                "EgressHttpStatus4xx": double value,
                "EgressHttpStatus5xx": double value,
                "EgressHttpStatusOthers": double value,
                "EgressCacheHit": double value,
                "EgressCacheMiss": double value,
                "EgressCacheNoCache": double value,
                "EgressCacheUncacheable": double value,
                "EgressCacheOthers": double value,
            }
        }

    ]
}
```

<span data-ttu-id="2fb57-409">Où « temps de hello » représente hello heure de début de limite d’heure hello pour laquelle les statistiques hello sont signalée.</span><span class="sxs-lookup"><span data-stu-id="2fb57-409">Where hello ‘time’ represents hello start time of hello hour boundary for which hello statistics is reported.</span></span> <span data-ttu-id="2fb57-410">Quand une métrique n’est pas prise en charge par un fournisseur CDN, il y a une valeur null au lieu d’un entier ou d’un double.</span><span class="sxs-lookup"><span data-stu-id="2fb57-410">When a metric is not supported by a CDN provider, instead of a double or integer value, there will be a null value.</span></span> <span data-ttu-id="2fb57-411">Cette valeur null indique l’absence de hello d’une mesure, et il diffère de la valeur 0.</span><span class="sxs-lookup"><span data-stu-id="2fb57-411">This null value indicates hello absence of a metric, and this is different from a 0 value.</span></span> <span data-ttu-id="2fb57-412">Notez également qu’il y aura un ensemble de ces mesures par domaine configuré sur le point de terminaison hello.</span><span class="sxs-lookup"><span data-stu-id="2fb57-412">Also note that there will be one set of these metrics per domain configured on hello endpoint.</span></span>

<span data-ttu-id="2fb57-413">Exemple de propriétés ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2fb57-413">Example properties below:</span></span>

```json
{
     "DomainName": "manlingakamaitest2.azureedge.net",
     "RequestCountTotal": 480,
     "RequestCountHttpStatus2xx": 480,
     "RequestCountHttpStatus3xx": 0,
     "RequestCountHttpStatus4xx": 0,
     "RequestCountHttpStatus5xx": 0,
     "RequestCountHttpStatusOthers": 0,
     "RequestCountHttpStatus200": 480,
     "RequestCountHttpStatus206": 0,
     "RequestCountHttpStatus302": 0,
     "RequestCountHttpStatus304": 0,
     "RequestCountHttpStatus404": 0,
     "RequestCountCacheHit": null,
     "RequestCountCacheMiss": null,
     "RequestCountCacheNoCache": null,
     "RequestCountCacheUncacheable": null,
     "RequestCountCacheOthers": null,
     "EgressTotal": 0.09,
     "EgressHttpStatus2xx": null,
     "EgressHttpStatus3xx": null,
     "EgressHttpStatus4xx": null,
     "EgressHttpStatus5xx": null,
     "EgressHttpStatusOthers": null,
     "EgressCacheHit": null,
     "EgressCacheMiss": null,
     "EgressCacheNoCache": null,
     "EgressCacheUncacheable": null,
     "EgressCacheOthers": null
}

```

## <a name="additional-resources"></a><span data-ttu-id="2fb57-414">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2fb57-414">Additional resources</span></span>

* [<span data-ttu-id="2fb57-415">Journaux de diagnostic Azure</span><span class="sxs-lookup"><span data-stu-id="2fb57-415">Azure Diagnostic logs</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [<span data-ttu-id="2fb57-416">Core Analytics via le portail supplémentaire Azure CDN</span><span class="sxs-lookup"><span data-stu-id="2fb57-416">Core analytics via Azure CDN supplemental portal</span></span>](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [<span data-ttu-id="2fb57-417">Azure OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="2fb57-417">Azure OMS Log Analytics</span></span>](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [<span data-ttu-id="2fb57-418">API REST Azure Log Analytics</span><span class="sxs-lookup"><span data-stu-id="2fb57-418">Azure Log Analytics REST API</span></span>](https://docs.microsoft.com/en-us/rest/api/loganalytics)







