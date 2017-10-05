---
title: "Utiliser une capture de paquets pour effectuer une surveillance proactive du réseau avec des alertes et Azure Functions | Microsoft Docs"
description: "Cet article décrit la création d’une capture de paquets déclenchée par des alertes avec Azure Network Watcher"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 75e6e7c4-b3ba-4173-8815-b00d7d824e11
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b813172fc1fc1cc683f463f05370c95bfec10f8d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a><span data-ttu-id="90d3b-103">Utiliser une capture de paquets pour effectuer une surveillance proactive du réseau avec des alertes et Azure Functions</span><span class="sxs-lookup"><span data-stu-id="90d3b-103">Use packet capture for proactive network monitoring with alerts and Azure Functions</span></span>

<span data-ttu-id="90d3b-104">La fonctionnalité de capture de paquets Network Watcher crée des sessions de capture afin d’effectuer le suivi du trafic en direction et en provenance des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="90d3b-104">Network Watcher packet capture creates capture sessions to track traffic in and out of virtual machines.</span></span> <span data-ttu-id="90d3b-105">Le fichier de capture peut contenir un filtre défini pour suivre uniquement le trafic que vous souhaitez analyser.</span><span class="sxs-lookup"><span data-stu-id="90d3b-105">The capture file can have a filter that is defined to track only the traffic that you want to monitor.</span></span> <span data-ttu-id="90d3b-106">Ces données sont ensuite stockées dans un objet blob de stockage ou localement sur l’ordinateur invité.</span><span class="sxs-lookup"><span data-stu-id="90d3b-106">This data is then stored in a storage blob or locally on the guest machine.</span></span>

<span data-ttu-id="90d3b-107">Cette fonctionnalité peut être démarrée à distance à partir d’autres scénarios d’automatisation comme Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="90d3b-107">This capability can be started remotely from other automation scenarios such as Azure Functions.</span></span> <span data-ttu-id="90d3b-108">La capture de paquets vous permet d’exécuter des captures proactives en fonction des anomalies définies sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="90d3b-108">Packet capture gives you the capability to run proactive captures based on defined network anomalies.</span></span> <span data-ttu-id="90d3b-109">Elle permet aussi de collecter des statistiques réseau, d’obtenir des informations sur les intrusions, de déboguer des communications client-serveur, etc.</span><span class="sxs-lookup"><span data-stu-id="90d3b-109">Other uses include gathering network statistics, getting information about network intrusions, debugging client-server communications, and more.</span></span>

<span data-ttu-id="90d3b-110">Les ressources qui sont déployées dans Azure s’exécutent 24 heures sur 24, 7 jours sur 7.</span><span class="sxs-lookup"><span data-stu-id="90d3b-110">Resources that are deployed in Azure run 24/7.</span></span> <span data-ttu-id="90d3b-111">Ni votre équipe ni vous ne pouvez surveiller activement l’état de toutes les ressources 24 heures sur 24, 7 jours sur 7.</span><span class="sxs-lookup"><span data-stu-id="90d3b-111">You and your staff cannot actively monitor the status of all resources 24/7.</span></span> <span data-ttu-id="90d3b-112">Par exemple, que se passe-t-il si un problème se produit à 2 h ?</span><span class="sxs-lookup"><span data-stu-id="90d3b-112">For example, what happens if an issue occurs at 2 AM?</span></span>

<span data-ttu-id="90d3b-113">En utilisant Network Watcher, les alertes et les fonctions dans l’écosystème Azure, vous pouvez répondre de façon proactive aux problèmes de votre réseau avec les données et les outils.</span><span class="sxs-lookup"><span data-stu-id="90d3b-113">By using Network Watcher, alerting, and functions from within the Azure ecosystem, you can proactively respond with the data and tools to solve problems in your network.</span></span>

![Scénario][scenario]

## <a name="prerequisites"></a><span data-ttu-id="90d3b-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="90d3b-115">Prerequisites</span></span>

* <span data-ttu-id="90d3b-116">La version la plus récente [d’Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="90d3b-116">The latest version of [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>
* <span data-ttu-id="90d3b-117">Une instance existante de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="90d3b-117">An existing instance of Network Watcher.</span></span> <span data-ttu-id="90d3b-118">Si vous n’en avez pas, [créez une instance de Network Watcher](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="90d3b-118">If you don't already have one, [create an instance of Network Watcher](network-watcher-create.md).</span></span>
* <span data-ttu-id="90d3b-119">Une machine virtuelle existante dans la même région que Network Watcher, avec [l’extension Windows](../virtual-machines/windows/extensions-nwa.md) ou [l’extension de machine virtuelle Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="90d3b-119">An existing virtual machine in the same region as Network Watcher with the [Windows extension](../virtual-machines/windows/extensions-nwa.md) or [Linux virtual machine extension](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="90d3b-120">Scénario</span><span class="sxs-lookup"><span data-stu-id="90d3b-120">Scenario</span></span>

<span data-ttu-id="90d3b-121">Dans cet exemple, votre machine virtuelle envoie plus de segments TCP que d’habitude, et vous souhaitez être alerté.</span><span class="sxs-lookup"><span data-stu-id="90d3b-121">In this example, your VM is sending more TCP segments than usual, and you want to be alerted.</span></span> <span data-ttu-id="90d3b-122">Les segments TCP sont utilisés ici à titre d’exemple, mais vous pouvez utiliser n’importe quelle condition d’alerte.</span><span class="sxs-lookup"><span data-stu-id="90d3b-122">TCP segments are used as an example here, but you can use any alert condition.</span></span>

<span data-ttu-id="90d3b-123">Lorsque vous recevez une alerte, il est intéressant d’obtenir des données au niveau des paquets afin de comprendre pourquoi la communication a augmenté.</span><span class="sxs-lookup"><span data-stu-id="90d3b-123">When you are alerted, you want to receive packet-level data to understand why communication has increased.</span></span> <span data-ttu-id="90d3b-124">Vous pouvez ensuite prendre des mesures pour rétablir une communication régulière sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="90d3b-124">Then you can take steps to return the virtual machine to regular communication.</span></span>

<span data-ttu-id="90d3b-125">Ce scénario suppose que vous possédez une instance existante de Network Watcher, ainsi qu’un groupe de ressources avec une machine virtuelle valide.</span><span class="sxs-lookup"><span data-stu-id="90d3b-125">This scenario assumes that you have an existing instance of Network Watcher and a resource group with a valid virtual machine.</span></span>

<span data-ttu-id="90d3b-126">La liste suivante est une vue d’ensemble du flux de travail qui se produit :</span><span class="sxs-lookup"><span data-stu-id="90d3b-126">The following list is an overview of the workflow that takes place:</span></span>

1. <span data-ttu-id="90d3b-127">Une alerte est déclenchée sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="90d3b-127">An alert is triggered on your VM.</span></span>
1. <span data-ttu-id="90d3b-128">L’alerte appelle votre fonction Azure via un webhook.</span><span class="sxs-lookup"><span data-stu-id="90d3b-128">The alert calls your Azure function via a webhook.</span></span>
1. <span data-ttu-id="90d3b-129">Votre fonction Azure traite l’alerte et démarre une session de capture de paquets Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="90d3b-129">Your Azure function processes the alert and starts a Network Watcher packet capture session.</span></span>
1. <span data-ttu-id="90d3b-130">La capture de paquets s’exécute sur la machine virtuelle et collecte le trafic.</span><span class="sxs-lookup"><span data-stu-id="90d3b-130">The packet capture runs on the VM and collects traffic.</span></span>
1. <span data-ttu-id="90d3b-131">Le fichier de capture de paquets est chargé vers un compte de stockage afin de subir un examen et un diagnostic.</span><span class="sxs-lookup"><span data-stu-id="90d3b-131">The packet capture file is uploaded to a storage account for review and diagnosis.</span></span>

<span data-ttu-id="90d3b-132">Pour automatiser ce processus, nous créons et connectons une alerte sur notre machine virtuelle pour qu’elle se déclenche lorsque l’incident se produit.</span><span class="sxs-lookup"><span data-stu-id="90d3b-132">To automate this process, we create and connect an alert on our VM to trigger when the incident occurs.</span></span> <span data-ttu-id="90d3b-133">Nous créons également une fonction pour appeler Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="90d3b-133">We also create a function to call into Network Watcher.</span></span>

<span data-ttu-id="90d3b-134">Ce scénario :</span><span class="sxs-lookup"><span data-stu-id="90d3b-134">This scenario does the following:</span></span>

* <span data-ttu-id="90d3b-135">crée une fonction Azure qui démarrera une capture de paquets ;</span><span class="sxs-lookup"><span data-stu-id="90d3b-135">Creates an Azure function that starts a packet capture.</span></span>
* <span data-ttu-id="90d3b-136">crée une règle d’alerte sur une machine virtuelle et configure la règle d’alerte pour appeler la fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="90d3b-136">Creates an alert rule on a virtual machine and configures the alert rule to call the Azure function.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="90d3b-137">Création d’une fonction Azure</span><span class="sxs-lookup"><span data-stu-id="90d3b-137">Create an Azure function</span></span>

<span data-ttu-id="90d3b-138">La première étape consiste à créer une fonction Azure pour traiter l’alerte et créer une capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="90d3b-138">The first step is to create an Azure function to process the alert and create a packet capture.</span></span>

1. <span data-ttu-id="90d3b-139">Dans le [portail Azure](https://portal.azure.com), sélectionnez **Nouveau** > **Compute** > **Function App**.</span><span class="sxs-lookup"><span data-stu-id="90d3b-139">In the [Azure portal](https://portal.azure.com), select **New** > **Compute** > **Function App**.</span></span>

    ![Création d’une application de fonction][1-1]

2. <span data-ttu-id="90d3b-141">Dans le panneau **Function App**, entrez les valeurs suivantes puis sélectionnez **OK** pour créer l’application :</span><span class="sxs-lookup"><span data-stu-id="90d3b-141">On the **Function App** blade, enter the following values, and then select **OK** to create the app:</span></span>

    |<span data-ttu-id="90d3b-142">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="90d3b-142">**Setting**</span></span> | <span data-ttu-id="90d3b-143">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="90d3b-143">**Value**</span></span> | <span data-ttu-id="90d3b-144">**Détails**</span><span class="sxs-lookup"><span data-stu-id="90d3b-144">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="90d3b-145">**Nom de l’application**</span><span class="sxs-lookup"><span data-stu-id="90d3b-145">**App name**</span></span>|<span data-ttu-id="90d3b-146">PacketCaptureExample</span><span class="sxs-lookup"><span data-stu-id="90d3b-146">PacketCaptureExample</span></span>|<span data-ttu-id="90d3b-147">Le nom de l’application de fonction.</span><span class="sxs-lookup"><span data-stu-id="90d3b-147">The name of the function app.</span></span>|
    |<span data-ttu-id="90d3b-148">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="90d3b-148">**Subscription**</span></span>|<span data-ttu-id="90d3b-149">[Votre abonnement] L’abonnement dans lequel créer l’application de fonction.</span><span class="sxs-lookup"><span data-stu-id="90d3b-149">[Your subscription]The subscription for which to create the function app.</span></span>||
    |<span data-ttu-id="90d3b-150">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="90d3b-150">**Resource Group**</span></span>|<span data-ttu-id="90d3b-151">PacketCaptureRG</span><span class="sxs-lookup"><span data-stu-id="90d3b-151">PacketCaptureRG</span></span>|<span data-ttu-id="90d3b-152">Le groupe de ressources qui contiendra l’application de fonction.</span><span class="sxs-lookup"><span data-stu-id="90d3b-152">The resource group to contain the function app.</span></span>|
    |<span data-ttu-id="90d3b-153">**Plan d’hébergement**</span><span class="sxs-lookup"><span data-stu-id="90d3b-153">**Hosting Plan**</span></span>|<span data-ttu-id="90d3b-154">Plan de consommation</span><span class="sxs-lookup"><span data-stu-id="90d3b-154">Consumption Plan</span></span>| <span data-ttu-id="90d3b-155">Le type de plan qu’utilise votre application de fonction.</span><span class="sxs-lookup"><span data-stu-id="90d3b-155">The type of plan your function app uses.</span></span> <span data-ttu-id="90d3b-156">Deux options sont disponibles : Consommation ou Plan Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="90d3b-156">Options are Consumption or Azure App Service plan.</span></span> |
    |<span data-ttu-id="90d3b-157">**Emplacement**</span><span class="sxs-lookup"><span data-stu-id="90d3b-157">**Location**</span></span>|<span data-ttu-id="90d3b-158">Centre des États-Unis</span><span class="sxs-lookup"><span data-stu-id="90d3b-158">Central US</span></span>| <span data-ttu-id="90d3b-159">La région dans laquelle créer l’application de fonction.</span><span class="sxs-lookup"><span data-stu-id="90d3b-159">The region in which to create the function app.</span></span>|
    |<span data-ttu-id="90d3b-160">**Compte de stockage**</span><span class="sxs-lookup"><span data-stu-id="90d3b-160">**Storage Account**</span></span>|<span data-ttu-id="90d3b-161">{généré automatiquement}</span><span class="sxs-lookup"><span data-stu-id="90d3b-161">{autogenerated}</span></span>| <span data-ttu-id="90d3b-162">Le compte de stockage dont Azure Functions a besoin pour le stockage général.</span><span class="sxs-lookup"><span data-stu-id="90d3b-162">The storage account that Azure Functions needs for general-purpose storage.</span></span>|

3. <span data-ttu-id="90d3b-163">Dans le panneau **Function App PacketCaptureExample**, sélectionnez **Fonctions** > **Fonction personnalisée** >**+**.</span><span class="sxs-lookup"><span data-stu-id="90d3b-163">On the **PacketCaptureExample Function Apps** blade, select **Functions** > **Custom function** >**+**.</span></span>

4. <span data-ttu-id="90d3b-164">Sélectionnez **HttpTrigger-Powershell**, puis entrez les informations restantes.</span><span class="sxs-lookup"><span data-stu-id="90d3b-164">Select **HttpTrigger-Powershell**, and then enter the remaining information.</span></span> <span data-ttu-id="90d3b-165">Enfin, pour créer la fonction, sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="90d3b-165">Finally, to create the function, select **Create**.</span></span>

    |<span data-ttu-id="90d3b-166">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="90d3b-166">**Setting**</span></span> | <span data-ttu-id="90d3b-167">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="90d3b-167">**Value**</span></span> | <span data-ttu-id="90d3b-168">**Détails**</span><span class="sxs-lookup"><span data-stu-id="90d3b-168">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="90d3b-169">**Scénario**</span><span class="sxs-lookup"><span data-stu-id="90d3b-169">**Scenario**</span></span>|<span data-ttu-id="90d3b-170">Expérimental</span><span class="sxs-lookup"><span data-stu-id="90d3b-170">Experimental</span></span>|<span data-ttu-id="90d3b-171">Type de scénario</span><span class="sxs-lookup"><span data-stu-id="90d3b-171">Type of scenario</span></span>|
    |<span data-ttu-id="90d3b-172">**Nommer votre fonction**</span><span class="sxs-lookup"><span data-stu-id="90d3b-172">**Name your function**</span></span>|<span data-ttu-id="90d3b-173">AlertPacketCapturePowerShell</span><span class="sxs-lookup"><span data-stu-id="90d3b-173">AlertPacketCapturePowerShell</span></span>|<span data-ttu-id="90d3b-174">Nom de la fonction</span><span class="sxs-lookup"><span data-stu-id="90d3b-174">Name of the function</span></span>|
    |<span data-ttu-id="90d3b-175">**Niveau d’autorisation**</span><span class="sxs-lookup"><span data-stu-id="90d3b-175">**Authorization level**</span></span>|<span data-ttu-id="90d3b-176">Fonction</span><span class="sxs-lookup"><span data-stu-id="90d3b-176">Function</span></span>|<span data-ttu-id="90d3b-177">Niveau d’autorisation de la fonction</span><span class="sxs-lookup"><span data-stu-id="90d3b-177">Authorization level for the function</span></span>|

![Exemples de fonctions][functions1]

> [!NOTE]
> <span data-ttu-id="90d3b-179">Le modèle PowerShell est expérimental et n’a pas de prise en charge complète.</span><span class="sxs-lookup"><span data-stu-id="90d3b-179">The PowerShell template is experimental and does not have full support.</span></span>

<span data-ttu-id="90d3b-180">Les personnalisations sont requises pour cet exemple et sont décrites dans les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="90d3b-180">Customizations are required for this example and are explained in the following steps.</span></span>

### <a name="add-modules"></a><span data-ttu-id="90d3b-181">Ajouter des modules</span><span class="sxs-lookup"><span data-stu-id="90d3b-181">Add modules</span></span>

<span data-ttu-id="90d3b-182">Pour utiliser les cmdlets PowerShell de Network Watcher, chargez le module PowerShell le plus récent dans l’application de fonction.</span><span class="sxs-lookup"><span data-stu-id="90d3b-182">To use Network Watcher PowerShell cmdlets, upload the latest PowerShell module to the function app.</span></span>

1. <span data-ttu-id="90d3b-183">Sur votre ordinateur local avec les derniers modules Azure PowerShell installés, exécutez la commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="90d3b-183">On your local machine with the latest Azure PowerShell modules installed, run the following PowerShell command:</span></span>

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    <span data-ttu-id="90d3b-184">Cet exemple vous donne le chemin local de vos modules Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="90d3b-184">This example gives you the local path of your Azure PowerShell modules.</span></span> <span data-ttu-id="90d3b-185">Ces dossiers sont utilisés dans une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="90d3b-185">These folders are used in a later step.</span></span> <span data-ttu-id="90d3b-186">Les modules utilisés dans ce scénario sont :</span><span class="sxs-lookup"><span data-stu-id="90d3b-186">The modules that are used in this scenario are:</span></span>

    * <span data-ttu-id="90d3b-187">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="90d3b-187">AzureRM.Network</span></span>

    * <span data-ttu-id="90d3b-188">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="90d3b-188">AzureRM.Profile</span></span>

    * <span data-ttu-id="90d3b-189">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="90d3b-189">AzureRM.Resources</span></span>

    ![Dossiers PowerShell][functions5]

1. <span data-ttu-id="90d3b-191">Sélectionnez **Paramètres Function App** > **Accéder à l’Éditeur App Service**.</span><span class="sxs-lookup"><span data-stu-id="90d3b-191">Select **Function app settings** > **Go to App Service Editor**.</span></span>

    ![Paramètres Function App][functions2]

1. <span data-ttu-id="90d3b-193">Cliquez avec le bouton droit sur le dossier **AlertPacketCapturePowershell** et créez un dossier nommé **azuremodules**.</span><span class="sxs-lookup"><span data-stu-id="90d3b-193">Right-click the **AlertPacketCapturePowershell** folder, and then create a folder called **azuremodules**.</span></span> 

4. <span data-ttu-id="90d3b-194">Créez un sous-dossier pour chacun des modules dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="90d3b-194">Create a subfolder for each module that you need.</span></span>

    ![Dossier et sous-dossiers][functions3]

    * <span data-ttu-id="90d3b-196">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="90d3b-196">AzureRM.Network</span></span>

    * <span data-ttu-id="90d3b-197">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="90d3b-197">AzureRM.Profile</span></span>

    * <span data-ttu-id="90d3b-198">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="90d3b-198">AzureRM.Resources</span></span>

1. <span data-ttu-id="90d3b-199">Cliquez avec le bouton droit sur le sous-dossier **AzureRM.Network**, puis sélectionnez **Charger des fichiers**.</span><span class="sxs-lookup"><span data-stu-id="90d3b-199">Right-click the **AzureRM.Network** subfolder, and then select **Upload Files**.</span></span> 

6. <span data-ttu-id="90d3b-200">Accédez à vos modules Azure.</span><span class="sxs-lookup"><span data-stu-id="90d3b-200">Go to your Azure modules.</span></span> <span data-ttu-id="90d3b-201">Dans le dossier **AzureRM.Network** local, sélectionnez tous les fichiers.</span><span class="sxs-lookup"><span data-stu-id="90d3b-201">In the local **AzureRM.Network** folder, select all the files in the folder.</span></span> <span data-ttu-id="90d3b-202">Sélectionnez ensuite **OK**.</span><span class="sxs-lookup"><span data-stu-id="90d3b-202">Then select **OK**.</span></span> 

7. <span data-ttu-id="90d3b-203">Répétez ces étapes pour **AzureRM.Profile** et **AzureRM.Resources**.</span><span class="sxs-lookup"><span data-stu-id="90d3b-203">Repeat these steps for **AzureRM.Profile** and **AzureRM.Resources**.</span></span>

    ![Charger des fichiers][functions6]

1. <span data-ttu-id="90d3b-205">Lorsque vous avez terminé, chaque dossier doit contenir les fichiers du module PowerShell de votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="90d3b-205">After you've finished, each folder should have the PowerShell module files from your local machine.</span></span>

    ![Fichiers PowerShell][functions7]

### <a name="authentication"></a><span data-ttu-id="90d3b-207">Authentification</span><span class="sxs-lookup"><span data-stu-id="90d3b-207">Authentication</span></span>

<span data-ttu-id="90d3b-208">Pour utiliser les applets de commande PowerShell, vous devez vous authentifier.</span><span class="sxs-lookup"><span data-stu-id="90d3b-208">To use the PowerShell cmdlets, you must authenticate.</span></span> <span data-ttu-id="90d3b-209">Vous configurez l’authentification dans l’application de fonction.</span><span class="sxs-lookup"><span data-stu-id="90d3b-209">You configure authentication in the function app.</span></span> <span data-ttu-id="90d3b-210">Pour ce faire, vous devez configurer les variables d’environnement et charger un fichier de clé chiffré dans l’application de fonction.</span><span class="sxs-lookup"><span data-stu-id="90d3b-210">To configure authentication, you must configure environment variables and upload an encrypted key file to the function app.</span></span>

> [!NOTE]
> <span data-ttu-id="90d3b-211">Ce scénario ne fournit qu’un exemple d’implémentation de l’authentification avec Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="90d3b-211">This scenario provides just one example of how to implement authentication with Azure Functions.</span></span> <span data-ttu-id="90d3b-212">Il existe d’autres façons de procéder.</span><span class="sxs-lookup"><span data-stu-id="90d3b-212">There are other ways to do this.</span></span>

#### <a name="encrypted-credentials"></a><span data-ttu-id="90d3b-213">Informations d’identification chiffrées</span><span class="sxs-lookup"><span data-stu-id="90d3b-213">Encrypted credentials</span></span>

<span data-ttu-id="90d3b-214">Le script PowerShell suivant crée un fichier de clé appelé **PassEncryptKey.key**.</span><span class="sxs-lookup"><span data-stu-id="90d3b-214">The following PowerShell script creates a key file called **PassEncryptKey.key**.</span></span> <span data-ttu-id="90d3b-215">Il fournit également une version chiffrée du mot de passe qui est donné.</span><span class="sxs-lookup"><span data-stu-id="90d3b-215">It also provides an encrypted version of the password that's supplied.</span></span> <span data-ttu-id="90d3b-216">Ce mot de passe est le même que celui défini pour l’application Azure Active Directory qui est utilisée pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="90d3b-216">This password is the same password that is defined for the Azure Active Directory application that's used for authentication.</span></span>

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

<span data-ttu-id="90d3b-217">Dans l’éditeur App Service de l’application de fonction, créez un dossier nommé **clés** sous **AlertPacketCapturePowerShell**.</span><span class="sxs-lookup"><span data-stu-id="90d3b-217">In the App Service Editor of the function app, create a folder called **keys** under **AlertPacketCapturePowerShell**.</span></span> <span data-ttu-id="90d3b-218">Chargez ensuite le fichier **PassEncryptKey.key** que vous avez créé dans l’exemple PowerShell précédent.</span><span class="sxs-lookup"><span data-stu-id="90d3b-218">Then upload the **PassEncryptKey.key** file that you created in the previous PowerShell sample.</span></span>

![Clé de fonctions][functions8]

### <a name="retrieve-values-for-environment-variables"></a><span data-ttu-id="90d3b-220">Récupérer des valeurs pour les variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="90d3b-220">Retrieve values for environment variables</span></span>

<span data-ttu-id="90d3b-221">La dernière exigence consiste à configurer les variables d’environnement nécessaires pour accéder aux valeurs pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="90d3b-221">The final requirement is to set up the environment variables that are necessary to access the values for authentication.</span></span> <span data-ttu-id="90d3b-222">Voici une liste des variables d’environnement qui sont créées :</span><span class="sxs-lookup"><span data-stu-id="90d3b-222">The following list shows the environment variables that are created:</span></span>

* <span data-ttu-id="90d3b-223">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="90d3b-223">AzureClientID</span></span>

* <span data-ttu-id="90d3b-224">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="90d3b-224">AzureTenant</span></span>

* <span data-ttu-id="90d3b-225">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="90d3b-225">AzureCredPassword</span></span>


#### <a name="azureclientid"></a><span data-ttu-id="90d3b-226">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="90d3b-226">AzureClientID</span></span>

<span data-ttu-id="90d3b-227">L’ID client est l’ID d’application d’une application dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="90d3b-227">The client ID is the Application ID of an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="90d3b-228">Si vous ne disposez pas d’une application à utiliser, exécutez l’exemple suivant pour créer une application.</span><span class="sxs-lookup"><span data-stu-id="90d3b-228">If you don't already have an application to use, run the following example to create an application.</span></span>

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > <span data-ttu-id="90d3b-229">Le mot de passe que vous utilisez lors de la création de l’application doit être le même que celui créé précédemment lors de l’enregistrement du fichier de clé.</span><span class="sxs-lookup"><span data-stu-id="90d3b-229">The password that you use when creating the application should be the same password that you created earlier when saving the key file.</span></span>

1. <span data-ttu-id="90d3b-230">Dans le portail Azure, sélectionnez **Abonnements**.</span><span class="sxs-lookup"><span data-stu-id="90d3b-230">In the Azure portal, select **Subscriptions**.</span></span> <span data-ttu-id="90d3b-231">Sélectionnez l’abonnement à utiliser, puis sélectionnez **Contrôle d’accès (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="90d3b-231">Select the subscription to use, and then select **Access control (IAM)**.</span></span>

    ![IAM de fonctions][functions9]

1. <span data-ttu-id="90d3b-233">Choisissez le compte à utiliser, puis sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="90d3b-233">Choose the account to use, and then select **Properties**.</span></span> <span data-ttu-id="90d3b-234">Copiez l’ID de l’application.</span><span class="sxs-lookup"><span data-stu-id="90d3b-234">Copy the Application ID.</span></span>

    ![ID de l’application de fonctions][functions10]

#### <a name="azuretenant"></a><span data-ttu-id="90d3b-236">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="90d3b-236">AzureTenant</span></span>

<span data-ttu-id="90d3b-237">Obtenez l’ID de locataire en exécutant l’exemple PowerShell suivant :</span><span class="sxs-lookup"><span data-stu-id="90d3b-237">Obtain the tenant ID  by running the following PowerShell sample:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a><span data-ttu-id="90d3b-238">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="90d3b-238">AzureCredPassword</span></span>

<span data-ttu-id="90d3b-239">La valeur de la variable d’environnement AzureCredPassword est celle obtenue en exécutant l’exemple PowerShell suivant.</span><span class="sxs-lookup"><span data-stu-id="90d3b-239">The value of the AzureCredPassword environment variable is the value that you get from running the following PowerShell sample.</span></span> <span data-ttu-id="90d3b-240">Cet exemple est identique à celui indiqué dans la section **Informations d’identification chiffrées** précédente.</span><span class="sxs-lookup"><span data-stu-id="90d3b-240">This example is the same one that's shown in the preceding **Encrypted credentials** section.</span></span> <span data-ttu-id="90d3b-241">La valeur requise est le résultat de la variable `$Encryptedpassword`.</span><span class="sxs-lookup"><span data-stu-id="90d3b-241">The value that's needed is the output of the `$Encryptedpassword` variable.</span></span>  <span data-ttu-id="90d3b-242">Ceci est le mot de passe du principal de service que vous avez chiffré à l’aide du script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="90d3b-242">This is the service principal password that you encrypted by using the PowerShell script.</span></span>

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

### <a name="store-the-environment-variables"></a><span data-ttu-id="90d3b-243">Stocker les variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="90d3b-243">Store the environment variables</span></span>

1. <span data-ttu-id="90d3b-244">Accédez à l’application de fonction.</span><span class="sxs-lookup"><span data-stu-id="90d3b-244">Go to the function app.</span></span> <span data-ttu-id="90d3b-245">Sélectionnez ensuite **Paramètres Function App** > **Configurer les paramètres de l’application**.</span><span class="sxs-lookup"><span data-stu-id="90d3b-245">Then select **Function app settings** > **Configure app settings**.</span></span>

    ![Configuration des paramètres d’application][functions11]

1. <span data-ttu-id="90d3b-247">Ajoutez les variables d’environnement et leurs valeurs aux paramètres de l’application, puis sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="90d3b-247">Add the environment variables and their values to the app settings, and then select **Save**.</span></span>

    ![Paramètres de l’application][functions12]

### <a name="add-powershell-to-the-function"></a><span data-ttu-id="90d3b-249">Ajout de PowerShell à la fonction</span><span class="sxs-lookup"><span data-stu-id="90d3b-249">Add PowerShell to the function</span></span>

<span data-ttu-id="90d3b-250">À présent, il est temps d’appeler Network Watcher à partir de la fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="90d3b-250">It's now time to make calls into Network Watcher from within the Azure function.</span></span> <span data-ttu-id="90d3b-251">Selon les besoins, l’implémentation de cette fonction peut varier.</span><span class="sxs-lookup"><span data-stu-id="90d3b-251">Depending on the requirements, the implementation of this function can vary.</span></span> <span data-ttu-id="90d3b-252">Toutefois, le flux général du code est comme suit :</span><span class="sxs-lookup"><span data-stu-id="90d3b-252">However, the general flow of the code is as follows:</span></span>

1. <span data-ttu-id="90d3b-253">Traiter les paramètres d’entrée.</span><span class="sxs-lookup"><span data-stu-id="90d3b-253">Process input parameters.</span></span>
2. <span data-ttu-id="90d3b-254">Interroger les captures de paquets existantes pour vérifier les limites et résoudre les conflits de noms.</span><span class="sxs-lookup"><span data-stu-id="90d3b-254">Query existing packet captures to verify limits and resolve name conflicts.</span></span>
3. <span data-ttu-id="90d3b-255">Créer une capture de paquets avec les paramètres appropriés.</span><span class="sxs-lookup"><span data-stu-id="90d3b-255">Create a packet capture with appropriate parameters.</span></span>
4. <span data-ttu-id="90d3b-256">Sonder régulièrement la capture de paquets jusqu’à la fin.</span><span class="sxs-lookup"><span data-stu-id="90d3b-256">Poll packet capture periodically until it's complete.</span></span>
5. <span data-ttu-id="90d3b-257">Informer l’utilisateur de la fin de la session de capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="90d3b-257">Notify the user that the packet capture session is complete.</span></span>

<span data-ttu-id="90d3b-258">L’exemple suivant correspond à du code PowerShell qui peut être utilisé dans la fonction.</span><span class="sxs-lookup"><span data-stu-id="90d3b-258">The following example is PowerShell code that can be used in the function.</span></span> <span data-ttu-id="90d3b-259">Il y a des valeurs qui doivent être remplacées pour **subscriptionId**, **resourceGroupName** et **storageAccountName**.</span><span class="sxs-lookup"><span data-stu-id="90d3b-259">There are values that need to be replaced for **subscriptionId**, **resourceGroupName**, and **storageAccountName**.</span></span>

```powershell
            #Import Azure PowerShell modules required to make calls to Network Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID to save captures in
            $storageaccountid = "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}"

            #Packet capture vars
            $packetcapturename = "PSAzureFunction"
            $packetCaptureLimit = 10
            $packetCaptureDuration = 10

            #Credentials
            $tenant = $env:AzureTenant
            $pw = $env:AzureCredPassword
            $clientid = $env:AzureClientId
            $keypath = "D:\home\site\wwwroot\AlertPacketCapturePowerShell\keys\PassEncryptKey.key"

            #Authentication
            $secpassword = $pw | ConvertTo-SecureString -Key (Get-Content $keypath)
            $credential = New-Object System.Management.Automation.PSCredential ($clientid, $secpassword)
            Add-AzureRMAccount -ServicePrincipal -Tenant $tenant -Credential $credential #-WarningAction SilentlyContinue | out-null


            #Get the VM that fired the alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get the Network Watcher in the VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by the function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on the VM that fired the alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-the-function-url"></a><span data-ttu-id="90d3b-260">Récupérer l’URL de fonction</span><span class="sxs-lookup"><span data-stu-id="90d3b-260">Retrieve the function URL</span></span> 
1. <span data-ttu-id="90d3b-261">Une fois que vous avez créé votre fonction, configurez votre alerte pour appeler l’URL associée à la fonction.</span><span class="sxs-lookup"><span data-stu-id="90d3b-261">After you've created your function, configure your alert to call the URL that's associated with the function.</span></span> <span data-ttu-id="90d3b-262">Pour obtenir cette valeur, copiez l’URL de la fonction à partir de votre Function App.</span><span class="sxs-lookup"><span data-stu-id="90d3b-262">To get this value, copy the function URL from your function app.</span></span>

    ![Recherche de l’URL de la fonction][functions13]

2. <span data-ttu-id="90d3b-264">Copiez l’URL de la fonction pour votre application de fonction.</span><span class="sxs-lookup"><span data-stu-id="90d3b-264">Copy the function URL for your function app.</span></span>

    ![Copie de l’URL de la fonction][2]

<span data-ttu-id="90d3b-266">Si vous avez besoin de propriétés personnalisées dans la charge utile de la demande POST du webhook, consultez l’article [Configurer un webhook sur une alerte de métrique Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="90d3b-266">If you require custom properties in the payload of the webhook POST request, refer to [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="configure-an-alert-on-a-vm"></a><span data-ttu-id="90d3b-267">Configurer une alerte sur une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="90d3b-267">Configure an alert on a VM</span></span>

<span data-ttu-id="90d3b-268">Des alertes peuvent être configurées pour informer qu’une mesure spécifique dépasse un seuil qui lui a été affecté.</span><span class="sxs-lookup"><span data-stu-id="90d3b-268">Alerts can be configured to notify individuals when a specific metric crosses a threshold that's assigned to it.</span></span> <span data-ttu-id="90d3b-269">Dans cet exemple, l’alerte est définie sur les segments TCP envoyés, mais elle peut être déclenchée pour plusieurs autres mesures.</span><span class="sxs-lookup"><span data-stu-id="90d3b-269">In this example, the alert is on the TCP segments that are sent, but the alert can be triggered for many other metrics.</span></span> <span data-ttu-id="90d3b-270">Dans cet exemple, une alerte est configurée pour appeler un webhook afin qu’il appelle la fonction.</span><span class="sxs-lookup"><span data-stu-id="90d3b-270">In this example, an alert is configured to call a webhook to call the function.</span></span>

### <a name="create-the-alert-rule"></a><span data-ttu-id="90d3b-271">Créer la règle d’alerte</span><span class="sxs-lookup"><span data-stu-id="90d3b-271">Create the alert rule</span></span>

<span data-ttu-id="90d3b-272">Accédez à une machine virtuelle existante, puis ajoutez une règle d’alerte.</span><span class="sxs-lookup"><span data-stu-id="90d3b-272">Go to an existing virtual machine, and then add an alert rule.</span></span> <span data-ttu-id="90d3b-273">Pour accéder à une documentation plus détaillée sur la configuration des alertes, consultez l’article [Créer des alertes dans Azure Monitor pour les services Azure - Portail Azure](../monitoring-and-diagnostics/insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="90d3b-273">More detailed documentation about configuring alerts can be found at [Create alerts in Azure Monitor for Azure services - Azure portal](../monitoring-and-diagnostics/insights-alerts-portal.md).</span></span> <span data-ttu-id="90d3b-274">Entrez les valeurs suivantes dans le panneau **Règle d’alerte**, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="90d3b-274">Enter the following values in the **Alert rule** blade, and then select **OK**.</span></span>

  |<span data-ttu-id="90d3b-275">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="90d3b-275">**Setting**</span></span> | <span data-ttu-id="90d3b-276">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="90d3b-276">**Value**</span></span> | <span data-ttu-id="90d3b-277">**Détails**</span><span class="sxs-lookup"><span data-stu-id="90d3b-277">**Details**</span></span> |
  |---|---|---|
  |<span data-ttu-id="90d3b-278">**Nom**</span><span class="sxs-lookup"><span data-stu-id="90d3b-278">**Name**</span></span>|<span data-ttu-id="90d3b-279">TCP_Segments_Sent_Exceeded</span><span class="sxs-lookup"><span data-stu-id="90d3b-279">TCP_Segments_Sent_Exceeded</span></span>|<span data-ttu-id="90d3b-280">Nom de la règle d’alerte.</span><span class="sxs-lookup"><span data-stu-id="90d3b-280">Name of the alert rule.</span></span>|
  |<span data-ttu-id="90d3b-281">**Description**</span><span class="sxs-lookup"><span data-stu-id="90d3b-281">**Description**</span></span>|<span data-ttu-id="90d3b-282">Les segments TCP envoyés ont dépassé le seuil</span><span class="sxs-lookup"><span data-stu-id="90d3b-282">TCP segments sent exceeded threshold</span></span>|<span data-ttu-id="90d3b-283">Description de la règle d’alerte.</span><span class="sxs-lookup"><span data-stu-id="90d3b-283">The description for the alert rule.</span></span>||
  |<span data-ttu-id="90d3b-284">**Mesure**</span><span class="sxs-lookup"><span data-stu-id="90d3b-284">**Metric**</span></span>|<span data-ttu-id="90d3b-285">Segments TCP envoyés</span><span class="sxs-lookup"><span data-stu-id="90d3b-285">TCP segments sent</span></span>| <span data-ttu-id="90d3b-286">Mesure à utiliser pour déclencher l’alerte.</span><span class="sxs-lookup"><span data-stu-id="90d3b-286">The metric to use to trigger the alert.</span></span> |
  |<span data-ttu-id="90d3b-287">**Condition**</span><span class="sxs-lookup"><span data-stu-id="90d3b-287">**Condition**</span></span>|<span data-ttu-id="90d3b-288">Supérieur à</span><span class="sxs-lookup"><span data-stu-id="90d3b-288">Greater than</span></span>| <span data-ttu-id="90d3b-289">Condition à utiliser lors de l’évaluation de la mesure.</span><span class="sxs-lookup"><span data-stu-id="90d3b-289">The condition to use when evaluating the metric.</span></span>|
  |<span data-ttu-id="90d3b-290">**Seuil**</span><span class="sxs-lookup"><span data-stu-id="90d3b-290">**Threshold**</span></span>|<span data-ttu-id="90d3b-291">100</span><span class="sxs-lookup"><span data-stu-id="90d3b-291">100</span></span>| <span data-ttu-id="90d3b-292">La valeur de la métrique qui déclenche l’alerte.</span><span class="sxs-lookup"><span data-stu-id="90d3b-292">The  value of the metric that triggers the alert.</span></span> <span data-ttu-id="90d3b-293">Cette valeur doit être définie sur une valeur valide pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="90d3b-293">This value should be set to a valid value for your environment.</span></span>|
  |<span data-ttu-id="90d3b-294">**Période**</span><span class="sxs-lookup"><span data-stu-id="90d3b-294">**Period**</span></span>|<span data-ttu-id="90d3b-295">Dans les cinq dernières minutes</span><span class="sxs-lookup"><span data-stu-id="90d3b-295">Over the last five minutes</span></span>| <span data-ttu-id="90d3b-296">Détermine la période pendant laquelle rechercher le seuil de la mesure.</span><span class="sxs-lookup"><span data-stu-id="90d3b-296">Determines the period in which to look for the threshold on the metric.</span></span>|
  |<span data-ttu-id="90d3b-297">**Webhook**</span><span class="sxs-lookup"><span data-stu-id="90d3b-297">**Webhook**</span></span>|<span data-ttu-id="90d3b-298">[URL du webhook de l’application de fonction]</span><span class="sxs-lookup"><span data-stu-id="90d3b-298">[webhook URL from function app]</span></span>| <span data-ttu-id="90d3b-299">L’URL du webhook de l’application de fonction créée dans les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="90d3b-299">The webhook URL from the function app that was created in the previous steps.</span></span>|

> [!NOTE]
> <span data-ttu-id="90d3b-300">Par défaut, la métrique des segments TCP n’est pas activée.</span><span class="sxs-lookup"><span data-stu-id="90d3b-300">The TCP segments metric is not enabled by default.</span></span> <span data-ttu-id="90d3b-301">Pour en savoir plus sur l’activation de métriques supplémentaires, consultez [Prise en main d’Azure Monitor](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="90d3b-301">Learn more about how to enable additional metrics by visiting [Enable monitoring and diagnostics](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span></span>

## <a name="review-the-results"></a><span data-ttu-id="90d3b-302">Passer en revue les résultats.</span><span class="sxs-lookup"><span data-stu-id="90d3b-302">Review the results</span></span>

<span data-ttu-id="90d3b-303">Une fois les critères d’alerte remplis, une capture de paquets est créée.</span><span class="sxs-lookup"><span data-stu-id="90d3b-303">After the criteria for the alert triggers, a packet capture is created.</span></span> <span data-ttu-id="90d3b-304">Accédez à Network Watcher, puis sélectionnez **Capture de paquets**.</span><span class="sxs-lookup"><span data-stu-id="90d3b-304">Go to Network Watcher, and then select **Packet capture**.</span></span> <span data-ttu-id="90d3b-305">Sur cette page, vous pouvez sélectionner le lien de fichier de capture de paquets pour télécharger la capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="90d3b-305">On this page, you can select the packet capture file link to download the packet capture.</span></span>

![Afficher une capture de paquets][functions14]

<span data-ttu-id="90d3b-307">Si le fichier de capture est stocké en local, vous pouvez le récupérer en vous connectant à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="90d3b-307">If the capture file is stored locally, you can retrieve it by signing in to the virtual machine.</span></span>

<span data-ttu-id="90d3b-308">Pour obtenir des instructions sur le téléchargement de fichiers à partir de comptes de stockage Azure, consultez [Prise en main du stockage d’objets blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="90d3b-308">For instructions about downloading files from Azure storage accounts, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="90d3b-309">Vous pouvez aussi utiliser [l’Explorateur de stockage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="90d3b-309">Another tool you can use is [Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="90d3b-310">Une fois la capture téléchargée, vous pouvez l’afficher à l’aide de n’importe quel outil en mesure de lire un fichier **.cap**.</span><span class="sxs-lookup"><span data-stu-id="90d3b-310">After your capture has been downloaded, you can view it by using any tool that can read a **.cap** file.</span></span> <span data-ttu-id="90d3b-311">Les liens de deux de ces outils sont indiqués ci-après :</span><span class="sxs-lookup"><span data-stu-id="90d3b-311">Following are links to two of these tools:</span></span>

- [<span data-ttu-id="90d3b-312">Microsoft Message Analyzer</span><span class="sxs-lookup"><span data-stu-id="90d3b-312">Microsoft Message Analyzer</span></span>](https://technet.microsoft.com/library/jj649776.aspx)
- [<span data-ttu-id="90d3b-313">WireShark</span><span class="sxs-lookup"><span data-stu-id="90d3b-313">WireShark</span></span>](https://www.wireshark.org/)

## <a name="next-steps"></a><span data-ttu-id="90d3b-314">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="90d3b-314">Next steps</span></span>

<span data-ttu-id="90d3b-315">Découvrez comment afficher vos captures de paquets en consultant l’article [Packet capture analysis with Wireshark (Analyse de la capture de paquets avec Wireshark)](network-watcher-deep-packet-inspection.md).</span><span class="sxs-lookup"><span data-stu-id="90d3b-315">Learn how to view your packet captures by visiting [Packet capture analysis with Wireshark](network-watcher-deep-packet-inspection.md).</span></span>


[1]: ./media/network-watcher-alert-triggered-packet-capture/figure1.png
[1-1]: ./media/network-watcher-alert-triggered-packet-capture/figure1-1.png
[2]: ./media/network-watcher-alert-triggered-packet-capture/figure2.png
[3]: ./media/network-watcher-alert-triggered-packet-capture/figure3.png
[functions1]:./media/network-watcher-alert-triggered-packet-capture/functions1.png
[functions2]:./media/network-watcher-alert-triggered-packet-capture/functions2.png
[functions3]:./media/network-watcher-alert-triggered-packet-capture/functions3.png
[functions4]:./media/network-watcher-alert-triggered-packet-capture/functions4.png
[functions5]:./media/network-watcher-alert-triggered-packet-capture/functions5.png
[functions6]:./media/network-watcher-alert-triggered-packet-capture/functions6.png
[functions7]:./media/network-watcher-alert-triggered-packet-capture/functions7.png
[functions8]:./media/network-watcher-alert-triggered-packet-capture/functions8.png
[functions9]:./media/network-watcher-alert-triggered-packet-capture/functions9.png
[functions10]:./media/network-watcher-alert-triggered-packet-capture/functions10.png
[functions11]:./media/network-watcher-alert-triggered-packet-capture/functions11.png
[functions12]:./media/network-watcher-alert-triggered-packet-capture/functions12.png
[functions13]:./media/network-watcher-alert-triggered-packet-capture/functions13.png
[functions14]:./media/network-watcher-alert-triggered-packet-capture/functions14.png
[scenario]:./media/network-watcher-alert-triggered-packet-capture/scenario.png
