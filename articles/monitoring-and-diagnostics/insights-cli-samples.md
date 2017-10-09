---
title: "exemples de démarrage rapide d’aaaAzure moniteur CLI 1.0. | Microsoft Docs"
description: "Exemples de commandes de l’interface CLI 1.0 pour accéder aux fonctionnalités d’Azure Monitor. Moniteur de Azure est un service Microsoft Azure qui vous permet de toosend des notifications d’alerte, des URL web appel en fonction des valeurs de données de télémétrie configuré et les Services de cloud computing de mise à l’échelle, les ordinateurs virtuels et les applications Web."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1653aa81-0ee6-4622-9c65-d4801ed9006f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6cd9cd62b3a1977276563f5e43f5384ccca66247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a><span data-ttu-id="cf19f-105">Exemple de démarrage rapide de l’interface CLI 1.0 multiplateforme pour Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="cf19f-105">Azure Monitor  Cross-platform CLI 1.0 quick start samples</span></span>
<span data-ttu-id="cf19f-106">Cet article explique les exemples de toohelp de commandes de l’interface de ligne de commande (CLI) vous accéder aux fonctionnalités du moniteur de Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="cf19f-106">This article shows you sample command-line interface (CLI) commands toohelp you access Azure Monitor features.</span></span> <span data-ttu-id="cf19f-107">Moniteur de Azure vous permet de tooAutoScale Services de cloud computing, Machines virtuelles et les applications Web et toosend des notifications d’alerte ou des URL web appel en fonction des valeurs de données de télémétrie configuré.</span><span class="sxs-lookup"><span data-stu-id="cf19f-107">Azure Monitor allows you tooAutoScale Cloud Services, Virtual Machines, and Web Apps and toosend alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="cf19f-108">Moniteur de Azure est hello nouveau nom pour ce qui a été appelé « Azure Insights » jusqu'à 25 septembre 2016.</span><span class="sxs-lookup"><span data-stu-id="cf19f-108">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="cf19f-109">Toutefois, les espaces de noms hello et, par conséquent, les commandes hello ci-dessous encore contient insights » l’hello ».</span><span class="sxs-lookup"><span data-stu-id="cf19f-109">However, hello namespaces and thus hello commands below still contain hello "insights".</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="cf19f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="cf19f-110">Prerequisites</span></span>
<span data-ttu-id="cf19f-111">Si vous n’avez pas déjà installé hello CLI d’Azure, consultez [installation Bonjour Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="cf19f-111">If you haven't already installed hello Azure CLI, see [Install hello Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="cf19f-112">Si vous n’êtes pas familiarisé avec l’interface CLI d’Azure, vous pouvez en savoir plus sur à l’adresse [hello d’utilisation CLI d’Azure pour Mac, Linux et Windows avec Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="cf19f-112">If you're unfamiliar with Azure CLI, you can read more about it at [Use hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span></span>

<span data-ttu-id="cf19f-113">Dans Windows, installez npm de hello [site Web Node.js](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="cf19f-113">In Windows, install npm from hello [Node.js website](https://nodejs.org/).</span></span> <span data-ttu-id="cf19f-114">Au terme de l’installation de hello, à l’aide de CMD.exe avec des privilèges d’exécution en tant qu’administrateur, exécutez les hello qui suit à partir du dossier hello où npm est installé :</span><span class="sxs-lookup"><span data-stu-id="cf19f-114">After you complete hello installation, using CMD.exe with Run As Administrator privileges, execute hello following from hello folder where npm is installed:</span></span>

```console
npm install azure-cli --global
```

<span data-ttu-id="cf19f-115">Ensuite, accédez tooany/emplacement du dossier souhaitée, puis tapez sur hello de ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="cf19f-115">Next, navigate tooany folder/location you want and type at hello command-line:</span></span>

```console
azure help
```

## <a name="log-in-tooazure"></a><span data-ttu-id="cf19f-116">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="cf19f-116">Log in tooAzure</span></span>
<span data-ttu-id="cf19f-117">première étape de Hello est toologin tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="cf19f-117">hello first step is toologin tooyour Azure account.</span></span>

```console
azure login
```

<span data-ttu-id="cf19f-118">Après avoir exécuté cette commande, vous avez toosign dans via des instructions sur l’écran hello hello.</span><span class="sxs-lookup"><span data-stu-id="cf19f-118">After running this command, you have toosign in via hello instructions on hello screen.</span></span> <span data-ttu-id="cf19f-119">Une fois cette opération effectuée, vos compte, ID de locataire et ID d’abonnement par défaut s’affichent. Toutes les commandes de travail dans le contexte de hello de votre abonnement par défaut.</span><span class="sxs-lookup"><span data-stu-id="cf19f-119">Afterward, you see your Account, TenantId, and default Subscription Id. All commands work in hello context of your default subscription.</span></span>

<span data-ttu-id="cf19f-120">Détails de hello toolist de votre abonnement actuel, utilisez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="cf19f-120">toolist hello details of your current subscription, use hello following command.</span></span>

```console
azure account show
```

<span data-ttu-id="cf19f-121">toochange travail contexte tooa autre abonnement, hello utilisez commande suivante.</span><span class="sxs-lookup"><span data-stu-id="cf19f-121">toochange working context tooa different subscription, use hello following command.</span></span>

```console
azure account set "subscription ID or subscription name"
```

<span data-ttu-id="cf19f-122">toouse Azure Resource Manager et Azure moniteur des commandes, vous devez toobe en mode Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cf19f-122">toouse Azure Resource Manager and Azure Monitor commands, you need toobe in Azure Resource Manager mode.</span></span>

```console
azure config mode arm
```

<span data-ttu-id="cf19f-123">tooview une liste de toutes les commandes prises en charge de moniteur de Windows Azure, effectuez des opérations suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="cf19f-123">tooview a list of all supported Azure Monitor commands, perform hello following.</span></span>

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a><span data-ttu-id="cf19f-124">Afficher le journal d’activité pour un abonnement</span><span class="sxs-lookup"><span data-stu-id="cf19f-124">View activity log for a subscription</span></span>
<span data-ttu-id="cf19f-125">tooview une liste des événements de journal d’activité, effectuez des opérations suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="cf19f-125">tooview a list of activity log events, perform hello following.</span></span>

```console
azure insights logs list [options]
```

<span data-ttu-id="cf19f-126">Essayez de hello suivant tooview toutes les options disponibles.</span><span class="sxs-lookup"><span data-stu-id="cf19f-126">Try hello following tooview all available options.</span></span>

```console
azure insights logs list -help
```

<span data-ttu-id="cf19f-127">Voici un exemple des journaux de toolist par un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="cf19f-127">Here is an example toolist logs by a resourceGroup</span></span>

```console
azure insights logs list --resourceGroup "myrg1"
```

<span data-ttu-id="cf19f-128">Journaux de toolist exemple par l’appelant</span><span class="sxs-lookup"><span data-stu-id="cf19f-128">Example toolist logs by caller</span></span>

```console
azure insights logs list --caller "myname@company.com"
```

<span data-ttu-id="cf19f-129">Journaux de toolist exemple par l’appelant sur un type de ressource au sein d’une date de début et de fin</span><span class="sxs-lookup"><span data-stu-id="cf19f-129">Example toolist logs by caller on a resource type, within a start and end date</span></span>

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a><span data-ttu-id="cf19f-130">Utilisation des alertes</span><span class="sxs-lookup"><span data-stu-id="cf19f-130">Work with alerts</span></span>
<span data-ttu-id="cf19f-131">Vous pouvez utiliser les informations de hello dans toowork de section hello des alertes.</span><span class="sxs-lookup"><span data-stu-id="cf19f-131">You can use hello information in hello section toowork with alerts.</span></span>

### <a name="get-alert-rules-in-a-resource-group"></a><span data-ttu-id="cf19f-132">Obtenir des règles d’alerte dans un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="cf19f-132">Get alert rules in a resource group</span></span>
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a><span data-ttu-id="cf19f-133">Créer une règle d’alerte métrique</span><span class="sxs-lookup"><span data-stu-id="cf19f-133">Create a metric alert rule</span></span>
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a><span data-ttu-id="cf19f-134">Créer une règle d’alerte de test web</span><span class="sxs-lookup"><span data-stu-id="cf19f-134">Create webtest alert rule</span></span>
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a><span data-ttu-id="cf19f-135">Supprimer une règle d’alerte</span><span class="sxs-lookup"><span data-stu-id="cf19f-135">Delete an alert rule</span></span>
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a><span data-ttu-id="cf19f-136">Profils de journal</span><span class="sxs-lookup"><span data-stu-id="cf19f-136">Log profiles</span></span>
<span data-ttu-id="cf19f-137">Utilisez les informations de hello toowork de cette section avec des profils de journal.</span><span class="sxs-lookup"><span data-stu-id="cf19f-137">Use hello information in this section toowork with log profiles.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="cf19f-138">Obtenir un profil de journal</span><span class="sxs-lookup"><span data-stu-id="cf19f-138">Get a log profile</span></span>
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a><span data-ttu-id="cf19f-139">Ajouter un profil de journal sans rétention</span><span class="sxs-lookup"><span data-stu-id="cf19f-139">Add a log profile without retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="cf19f-140">Supprimer un profil de journal</span><span class="sxs-lookup"><span data-stu-id="cf19f-140">Remove a log profile</span></span>
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a><span data-ttu-id="cf19f-141">Ajouter un profil de journal avec rétention</span><span class="sxs-lookup"><span data-stu-id="cf19f-141">Add a log profile with retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="cf19f-142">Ajouter un profil de journal avec rétention et EventHub</span><span class="sxs-lookup"><span data-stu-id="cf19f-142">Add a log profile with retention and EventHub</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a><span data-ttu-id="cf19f-143">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="cf19f-143">Diagnostics</span></span>
<span data-ttu-id="cf19f-144">Utilisez les informations de hello toowork de cette section avec les paramètres de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="cf19f-144">Use hello information in this section toowork with diagnostic settings.</span></span>

### <a name="get-a-diagnostic-setting"></a><span data-ttu-id="cf19f-145">Obtenir un paramètre de diagnostic</span><span class="sxs-lookup"><span data-stu-id="cf19f-145">Get a diagnostic setting</span></span>
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a><span data-ttu-id="cf19f-146">Désactiver un paramètre de diagnostic</span><span class="sxs-lookup"><span data-stu-id="cf19f-146">Disable a diagnostic setting</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a><span data-ttu-id="cf19f-147">Activer un paramètre de diagnostic sans rétention</span><span class="sxs-lookup"><span data-stu-id="cf19f-147">Enable a diagnostic setting without retention</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a><span data-ttu-id="cf19f-148">Autoscale</span><span class="sxs-lookup"><span data-stu-id="cf19f-148">Autoscale</span></span>
<span data-ttu-id="cf19f-149">Utilisez les informations de hello toowork de cette section avec les paramètres de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="cf19f-149">Use hello information in this section toowork with autoscale settings.</span></span> <span data-ttu-id="cf19f-150">Vous devez toomodify ces exemples.</span><span class="sxs-lookup"><span data-stu-id="cf19f-150">You need toomodify these examples.</span></span>

### <a name="get-autoscale-settings-for-a-resource-group"></a><span data-ttu-id="cf19f-151">Obtenir les paramètres de mise à l’échelle automatique pour un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="cf19f-151">Get autoscale settings for a resource group</span></span>
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a><span data-ttu-id="cf19f-152">Obtenir les paramètres de mise à l’échelle automatique par nom dans un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="cf19f-152">Get autoscale settings by name in a resource group</span></span>
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a><span data-ttu-id="cf19f-153">Définir les paramètres de mise à l’échelle automatique</span><span class="sxs-lookup"><span data-stu-id="cf19f-153">Set auotoscale settings</span></span>
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
