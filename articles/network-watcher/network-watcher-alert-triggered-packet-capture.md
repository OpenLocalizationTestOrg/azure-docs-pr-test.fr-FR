---
title: "toodo de capture de paquet aaaUse proactive de la surveillance des alertes et les fonctions d’Azure réseau | Documents Microsoft"
description: "Cet article décrit comment toocreate une alerte déclenchée capture de paquet avec l’Observateur de réseau Azure"
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
ms.openlocfilehash: 4722a831f3a9d5537c0e6f53daba4dfc35d0cf24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a><span data-ttu-id="8c364-103">Utiliser une capture de paquets pour effectuer une surveillance proactive du réseau avec des alertes et Azure Functions</span><span class="sxs-lookup"><span data-stu-id="8c364-103">Use packet capture for proactive network monitoring with alerts and Azure Functions</span></span>

<span data-ttu-id="8c364-104">Capture des paquets réseau Observateur crée des sessions de capture tootrack un trafic vers et depuis des ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="8c364-104">Network Watcher packet capture creates capture sessions tootrack traffic in and out of virtual machines.</span></span> <span data-ttu-id="8c364-105">Hello fichier de capture peut avoir un filtre défini tootrack hello uniquement le trafic que vous souhaitez toomonitor.</span><span class="sxs-lookup"><span data-stu-id="8c364-105">hello capture file can have a filter that is defined tootrack only hello traffic that you want toomonitor.</span></span> <span data-ttu-id="8c364-106">Ces données sont ensuite stockées dans un objet blob de stockage ou localement sur l’ordinateur invité de hello.</span><span class="sxs-lookup"><span data-stu-id="8c364-106">This data is then stored in a storage blob or locally on hello guest machine.</span></span>

<span data-ttu-id="8c364-107">Cette fonctionnalité peut être démarrée à distance à partir d’autres scénarios d’automatisation comme Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="8c364-107">This capability can be started remotely from other automation scenarios such as Azure Functions.</span></span> <span data-ttu-id="8c364-108">Permet de capture de paquets sur que Hello de captures proactive de la fonctionnalité toorun basés définie anomalies réseau.</span><span class="sxs-lookup"><span data-stu-id="8c364-108">Packet capture gives you hello capability toorun proactive captures based on defined network anomalies.</span></span> <span data-ttu-id="8c364-109">Elle permet aussi de collecter des statistiques réseau, d’obtenir des informations sur les intrusions, de déboguer des communications client-serveur, etc.</span><span class="sxs-lookup"><span data-stu-id="8c364-109">Other uses include gathering network statistics, getting information about network intrusions, debugging client-server communications, and more.</span></span>

<span data-ttu-id="8c364-110">Les ressources qui sont déployées dans Azure s’exécutent 24 heures sur 24, 7 jours sur 7.</span><span class="sxs-lookup"><span data-stu-id="8c364-110">Resources that are deployed in Azure run 24/7.</span></span> <span data-ttu-id="8c364-111">Vous et votre équipe ne peut pas analyser activement état hello de toutes les ressources 24/7.</span><span class="sxs-lookup"><span data-stu-id="8c364-111">You and your staff cannot actively monitor hello status of all resources 24/7.</span></span> <span data-ttu-id="8c364-112">Par exemple, que se passe-t-il si un problème se produit à 2 h ?</span><span class="sxs-lookup"><span data-stu-id="8c364-112">For example, what happens if an issue occurs at 2 AM?</span></span>

<span data-ttu-id="8c364-113">Par l’Observateur réseau, d’alerte et fonctions à partir de hello écosystème Azure, vous pouvez répondre proactive hello données et outils toosolve aux problèmes dans votre réseau.</span><span class="sxs-lookup"><span data-stu-id="8c364-113">By using Network Watcher, alerting, and functions from within hello Azure ecosystem, you can proactively respond with hello data and tools toosolve problems in your network.</span></span>

![Scénario][scenario]

## <a name="prerequisites"></a><span data-ttu-id="8c364-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8c364-115">Prerequisites</span></span>

* <span data-ttu-id="8c364-116">version la plus récente de Hello [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="8c364-116">hello latest version of [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>
* <span data-ttu-id="8c364-117">Une instance existante de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="8c364-117">An existing instance of Network Watcher.</span></span> <span data-ttu-id="8c364-118">Si vous n’en avez pas, [créez une instance de Network Watcher](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="8c364-118">If you don't already have one, [create an instance of Network Watcher](network-watcher-create.md).</span></span>
* <span data-ttu-id="8c364-119">Un ordinateur virtuel existant dans hello même région qu’Observateur réseau avec hello [extension Windows](../virtual-machines/windows/extensions-nwa.md) ou [extension de machine virtuelle Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="8c364-119">An existing virtual machine in hello same region as Network Watcher with hello [Windows extension](../virtual-machines/windows/extensions-nwa.md) or [Linux virtual machine extension](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="8c364-120">Scénario</span><span class="sxs-lookup"><span data-stu-id="8c364-120">Scenario</span></span>

<span data-ttu-id="8c364-121">Dans cet exemple, votre machine virtuelle envoie des segments TCP plus que d’habitude, et vous souhaitez toobe alerté.</span><span class="sxs-lookup"><span data-stu-id="8c364-121">In this example, your VM is sending more TCP segments than usual, and you want toobe alerted.</span></span> <span data-ttu-id="8c364-122">Les segments TCP sont utilisés ici à titre d’exemple, mais vous pouvez utiliser n’importe quelle condition d’alerte.</span><span class="sxs-lookup"><span data-stu-id="8c364-122">TCP segments are used as an example here, but you can use any alert condition.</span></span>

<span data-ttu-id="8c364-123">Lorsque vous êtes averti, vous souhaitez toounderstand de données au niveau du paquet tooreceive pourquoi la communication a augmenté.</span><span class="sxs-lookup"><span data-stu-id="8c364-123">When you are alerted, you want tooreceive packet-level data toounderstand why communication has increased.</span></span> <span data-ttu-id="8c364-124">Puis vous pouvez prendre des mesures communication de tooregular tooreturn hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8c364-124">Then you can take steps tooreturn hello virtual machine tooregular communication.</span></span>

<span data-ttu-id="8c364-125">Ce scénario suppose que vous possédez une instance existante de Network Watcher, ainsi qu’un groupe de ressources avec une machine virtuelle valide.</span><span class="sxs-lookup"><span data-stu-id="8c364-125">This scenario assumes that you have an existing instance of Network Watcher and a resource group with a valid virtual machine.</span></span>

<span data-ttu-id="8c364-126">Hello suivant liste est une vue d’ensemble du flux de travail hello qui a lieu :</span><span class="sxs-lookup"><span data-stu-id="8c364-126">hello following list is an overview of hello workflow that takes place:</span></span>

1. <span data-ttu-id="8c364-127">Une alerte est déclenchée sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8c364-127">An alert is triggered on your VM.</span></span>
1. <span data-ttu-id="8c364-128">alerte de Hello appelle votre fonction Azure via un webhook.</span><span class="sxs-lookup"><span data-stu-id="8c364-128">hello alert calls your Azure function via a webhook.</span></span>
1. <span data-ttu-id="8c364-129">Votre fonction Azure traite l’alerte de hello et démarre une session de capture de paquet réseau Observateur.</span><span class="sxs-lookup"><span data-stu-id="8c364-129">Your Azure function processes hello alert and starts a Network Watcher packet capture session.</span></span>
1. <span data-ttu-id="8c364-130">capture des paquets Hello s’exécute sur hello machine virtuelle et le trafic de collecte.</span><span class="sxs-lookup"><span data-stu-id="8c364-130">hello packet capture runs on hello VM and collects traffic.</span></span>
1. <span data-ttu-id="8c364-131">Hello fichier de capture de paquet est téléchargé tooa compte de stockage pour la révision et de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="8c364-131">hello packet capture file is uploaded tooa storage account for review and diagnosis.</span></span>

<span data-ttu-id="8c364-132">tooautomate ce processus, nous créons et connecter une alerte sur notre tootrigger de machine virtuelle lors de l’incident de hello se produit.</span><span class="sxs-lookup"><span data-stu-id="8c364-132">tooautomate this process, we create and connect an alert on our VM tootrigger when hello incident occurs.</span></span> <span data-ttu-id="8c364-133">Nous permet également de créer une fonction toocall dans l’Observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="8c364-133">We also create a function toocall into Network Watcher.</span></span>

<span data-ttu-id="8c364-134">Ce scénario hello suivant :</span><span class="sxs-lookup"><span data-stu-id="8c364-134">This scenario does hello following:</span></span>

* <span data-ttu-id="8c364-135">crée une fonction Azure qui démarrera une capture de paquets ;</span><span class="sxs-lookup"><span data-stu-id="8c364-135">Creates an Azure function that starts a packet capture.</span></span>
* <span data-ttu-id="8c364-136">Crée une règle d’alerte sur un ordinateur virtuel et configure hello toocall de règle d’alerte hello fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="8c364-136">Creates an alert rule on a virtual machine and configures hello alert rule toocall hello Azure function.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="8c364-137">Création d’une fonction Azure</span><span class="sxs-lookup"><span data-stu-id="8c364-137">Create an Azure function</span></span>

<span data-ttu-id="8c364-138">première étape de Hello est toocreate une alerte de hello tooprocess fonction Azure et créer une capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="8c364-138">hello first step is toocreate an Azure function tooprocess hello alert and create a packet capture.</span></span>

1. <span data-ttu-id="8c364-139">Bonjour [portail Azure](https://portal.azure.com), sélectionnez **nouveau** > **de calcul** > **fonction application**.</span><span class="sxs-lookup"><span data-stu-id="8c364-139">In hello [Azure portal](https://portal.azure.com), select **New** > **Compute** > **Function App**.</span></span>

    ![Création d’une application de fonction][1-1]

2. <span data-ttu-id="8c364-141">Sur hello **fonction application** panneau, entrez des valeurs suivantes de hello, puis sélectionnez **OK** toocreate hello application :</span><span class="sxs-lookup"><span data-stu-id="8c364-141">On hello **Function App** blade, enter hello following values, and then select **OK** toocreate hello app:</span></span>

    |<span data-ttu-id="8c364-142">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="8c364-142">**Setting**</span></span> | <span data-ttu-id="8c364-143">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="8c364-143">**Value**</span></span> | <span data-ttu-id="8c364-144">**Détails**</span><span class="sxs-lookup"><span data-stu-id="8c364-144">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="8c364-145">**Nom de l’application**</span><span class="sxs-lookup"><span data-stu-id="8c364-145">**App name**</span></span>|<span data-ttu-id="8c364-146">PacketCaptureExample</span><span class="sxs-lookup"><span data-stu-id="8c364-146">PacketCaptureExample</span></span>|<span data-ttu-id="8c364-147">nom Hello d’application de fonction hello.</span><span class="sxs-lookup"><span data-stu-id="8c364-147">hello name of hello function app.</span></span>|
    |<span data-ttu-id="8c364-148">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="8c364-148">**Subscription**</span></span>|<span data-ttu-id="8c364-149">[Votre abonnement] hello d’abonnement pour l’application de fonction toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="8c364-149">[Your subscription]hello subscription for which toocreate hello function app.</span></span>||
    |<span data-ttu-id="8c364-150">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="8c364-150">**Resource Group**</span></span>|<span data-ttu-id="8c364-151">PacketCaptureRG</span><span class="sxs-lookup"><span data-stu-id="8c364-151">PacketCaptureRG</span></span>|<span data-ttu-id="8c364-152">ressource groupe toocontain hello fonction application Hello.</span><span class="sxs-lookup"><span data-stu-id="8c364-152">hello resource group toocontain hello function app.</span></span>|
    |<span data-ttu-id="8c364-153">**Plan d’hébergement**</span><span class="sxs-lookup"><span data-stu-id="8c364-153">**Hosting Plan**</span></span>|<span data-ttu-id="8c364-154">Plan de consommation</span><span class="sxs-lookup"><span data-stu-id="8c364-154">Consumption Plan</span></span>| <span data-ttu-id="8c364-155">type Hello du plan par votre application de fonction.</span><span class="sxs-lookup"><span data-stu-id="8c364-155">hello type of plan your function app uses.</span></span> <span data-ttu-id="8c364-156">Deux options sont disponibles : Consommation ou Plan Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="8c364-156">Options are Consumption or Azure App Service plan.</span></span> |
    |<span data-ttu-id="8c364-157">**Emplacement**</span><span class="sxs-lookup"><span data-stu-id="8c364-157">**Location**</span></span>|<span data-ttu-id="8c364-158">Centre des États-Unis</span><span class="sxs-lookup"><span data-stu-id="8c364-158">Central US</span></span>| <span data-ttu-id="8c364-159">région Hello toocreate hello fonction application.</span><span class="sxs-lookup"><span data-stu-id="8c364-159">hello region in which toocreate hello function app.</span></span>|
    |<span data-ttu-id="8c364-160">**Compte de stockage**</span><span class="sxs-lookup"><span data-stu-id="8c364-160">**Storage Account**</span></span>|<span data-ttu-id="8c364-161">{généré automatiquement}</span><span class="sxs-lookup"><span data-stu-id="8c364-161">{autogenerated}</span></span>| <span data-ttu-id="8c364-162">compte de stockage Hello nécessitant des fonctions de Azure pour le stockage à usage général.</span><span class="sxs-lookup"><span data-stu-id="8c364-162">hello storage account that Azure Functions needs for general-purpose storage.</span></span>|

3. <span data-ttu-id="8c364-163">Sur hello **PacketCaptureExample fonction applications** panneau, sélectionnez **fonctions** > **fonction personnalisée**  >  **+**.</span><span class="sxs-lookup"><span data-stu-id="8c364-163">On hello **PacketCaptureExample Function Apps** blade, select **Functions** > **Custom function** >**+**.</span></span>

4. <span data-ttu-id="8c364-164">Sélectionnez **HttpTrigger-Powershell**, puis entrez hello restant d’informations.</span><span class="sxs-lookup"><span data-stu-id="8c364-164">Select **HttpTrigger-Powershell**, and then enter hello remaining information.</span></span> <span data-ttu-id="8c364-165">Enfin, toocreate fonction hello, sélectionnez **créer**.</span><span class="sxs-lookup"><span data-stu-id="8c364-165">Finally, toocreate hello function, select **Create**.</span></span>

    |<span data-ttu-id="8c364-166">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="8c364-166">**Setting**</span></span> | <span data-ttu-id="8c364-167">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="8c364-167">**Value**</span></span> | <span data-ttu-id="8c364-168">**Détails**</span><span class="sxs-lookup"><span data-stu-id="8c364-168">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="8c364-169">**Scénario**</span><span class="sxs-lookup"><span data-stu-id="8c364-169">**Scenario**</span></span>|<span data-ttu-id="8c364-170">Expérimental</span><span class="sxs-lookup"><span data-stu-id="8c364-170">Experimental</span></span>|<span data-ttu-id="8c364-171">Type de scénario</span><span class="sxs-lookup"><span data-stu-id="8c364-171">Type of scenario</span></span>|
    |<span data-ttu-id="8c364-172">**Nommer votre fonction**</span><span class="sxs-lookup"><span data-stu-id="8c364-172">**Name your function**</span></span>|<span data-ttu-id="8c364-173">AlertPacketCapturePowerShell</span><span class="sxs-lookup"><span data-stu-id="8c364-173">AlertPacketCapturePowerShell</span></span>|<span data-ttu-id="8c364-174">Nom de la fonction hello</span><span class="sxs-lookup"><span data-stu-id="8c364-174">Name of hello function</span></span>|
    |<span data-ttu-id="8c364-175">**Niveau d’autorisation**</span><span class="sxs-lookup"><span data-stu-id="8c364-175">**Authorization level**</span></span>|<span data-ttu-id="8c364-176">Fonction</span><span class="sxs-lookup"><span data-stu-id="8c364-176">Function</span></span>|<span data-ttu-id="8c364-177">Niveau d’autorisation pour la fonction hello</span><span class="sxs-lookup"><span data-stu-id="8c364-177">Authorization level for hello function</span></span>|

![Exemples de fonctions][functions1]

> [!NOTE]
> <span data-ttu-id="8c364-179">modèle de PowerShell Hello est expérimentale et n’a pas de prise en charge complète.</span><span class="sxs-lookup"><span data-stu-id="8c364-179">hello PowerShell template is experimental and does not have full support.</span></span>

<span data-ttu-id="8c364-180">Les personnalisations sont requises pour cet exemple, ils sont expliquées dans hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="8c364-180">Customizations are required for this example and are explained in hello following steps.</span></span>

### <a name="add-modules"></a><span data-ttu-id="8c364-181">Ajouter des modules</span><span class="sxs-lookup"><span data-stu-id="8c364-181">Add modules</span></span>

<span data-ttu-id="8c364-182">toouse applets de commande PowerShell de l’Observateur réseau, téléchargez hello dernière PowerShell module toohello fonction application.</span><span class="sxs-lookup"><span data-stu-id="8c364-182">toouse Network Watcher PowerShell cmdlets, upload hello latest PowerShell module toohello function app.</span></span>

1. <span data-ttu-id="8c364-183">Sur votre ordinateur local avec des modules Azure PowerShell dernière hello installé, exécutez hello suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="8c364-183">On your local machine with hello latest Azure PowerShell modules installed, run hello following PowerShell command:</span></span>

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    <span data-ttu-id="8c364-184">Cela donne exemple hello de chemin d’accès local de vos modules Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8c364-184">This example gives you hello local path of your Azure PowerShell modules.</span></span> <span data-ttu-id="8c364-185">Ces dossiers sont utilisés dans une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="8c364-185">These folders are used in a later step.</span></span> <span data-ttu-id="8c364-186">modules de Hello sont utilisées dans ce scénario sont :</span><span class="sxs-lookup"><span data-stu-id="8c364-186">hello modules that are used in this scenario are:</span></span>

    * <span data-ttu-id="8c364-187">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="8c364-187">AzureRM.Network</span></span>

    * <span data-ttu-id="8c364-188">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="8c364-188">AzureRM.Profile</span></span>

    * <span data-ttu-id="8c364-189">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="8c364-189">AzureRM.Resources</span></span>

    ![Dossiers PowerShell][functions5]

1. <span data-ttu-id="8c364-191">Sélectionnez **paramètres de l’application de la fonction** > **accédez tooApp éditeur Service**.</span><span class="sxs-lookup"><span data-stu-id="8c364-191">Select **Function app settings** > **Go tooApp Service Editor**.</span></span>

    ![Paramètres Function App][functions2]

1. <span data-ttu-id="8c364-193">Avec le bouton hello **AlertPacketCapturePowershell** dossier, puis créez un dossier appelé **azuremodules**.</span><span class="sxs-lookup"><span data-stu-id="8c364-193">Right-click hello **AlertPacketCapturePowershell** folder, and then create a folder called **azuremodules**.</span></span> 

4. <span data-ttu-id="8c364-194">Créez un sous-dossier pour chacun des modules dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="8c364-194">Create a subfolder for each module that you need.</span></span>

    ![Dossier et sous-dossiers][functions3]

    * <span data-ttu-id="8c364-196">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="8c364-196">AzureRM.Network</span></span>

    * <span data-ttu-id="8c364-197">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="8c364-197">AzureRM.Profile</span></span>

    * <span data-ttu-id="8c364-198">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="8c364-198">AzureRM.Resources</span></span>

1. <span data-ttu-id="8c364-199">Avec le bouton hello **AzureRM.Network** sous-dossier, puis sélectionnez **télécharger des fichiers**.</span><span class="sxs-lookup"><span data-stu-id="8c364-199">Right-click hello **AzureRM.Network** subfolder, and then select **Upload Files**.</span></span> 

6. <span data-ttu-id="8c364-200">Accédez tooyour Azure modules.</span><span class="sxs-lookup"><span data-stu-id="8c364-200">Go tooyour Azure modules.</span></span> <span data-ttu-id="8c364-201">Hello local **AzureRM.Network** dossier, sélectionnez tous les fichiers hello dans le dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="8c364-201">In hello local **AzureRM.Network** folder, select all hello files in hello folder.</span></span> <span data-ttu-id="8c364-202">Sélectionnez ensuite **OK**.</span><span class="sxs-lookup"><span data-stu-id="8c364-202">Then select **OK**.</span></span> 

7. <span data-ttu-id="8c364-203">Répétez ces étapes pour **AzureRM.Profile** et **AzureRM.Resources**.</span><span class="sxs-lookup"><span data-stu-id="8c364-203">Repeat these steps for **AzureRM.Profile** and **AzureRM.Resources**.</span></span>

    ![Charger des fichiers][functions6]

1. <span data-ttu-id="8c364-205">Après avoir terminé, chaque dossier doit avoir des fichiers de module PowerShell hello à partir de votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="8c364-205">After you've finished, each folder should have hello PowerShell module files from your local machine.</span></span>

    ![Fichiers PowerShell][functions7]

### <a name="authentication"></a><span data-ttu-id="8c364-207">Authentification</span><span class="sxs-lookup"><span data-stu-id="8c364-207">Authentication</span></span>

<span data-ttu-id="8c364-208">applets de commande PowerShell de hello toouse, vous devez vous authentifier.</span><span class="sxs-lookup"><span data-stu-id="8c364-208">toouse hello PowerShell cmdlets, you must authenticate.</span></span> <span data-ttu-id="8c364-209">Vous configurez l’authentification dans l’application de fonction hello.</span><span class="sxs-lookup"><span data-stu-id="8c364-209">You configure authentication in hello function app.</span></span> <span data-ttu-id="8c364-210">l’authentification tooconfigure, vous devez configurer les variables d’environnement et charger une application de fonction toohello un fichier de clé chiffrée.</span><span class="sxs-lookup"><span data-stu-id="8c364-210">tooconfigure authentication, you must configure environment variables and upload an encrypted key file toohello function app.</span></span>

> [!NOTE]
> <span data-ttu-id="8c364-211">Ce scénario fournit simplement un exemple d’authentification tooimplement avec des fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="8c364-211">This scenario provides just one example of how tooimplement authentication with Azure Functions.</span></span> <span data-ttu-id="8c364-212">Il existe autres façons toodo cela.</span><span class="sxs-lookup"><span data-stu-id="8c364-212">There are other ways toodo this.</span></span>

#### <a name="encrypted-credentials"></a><span data-ttu-id="8c364-213">Informations d’identification chiffrées</span><span class="sxs-lookup"><span data-stu-id="8c364-213">Encrypted credentials</span></span>

<span data-ttu-id="8c364-214">Hello PowerShell script suivant crée un fichier de clé appelé **PassEncryptKey.key**.</span><span class="sxs-lookup"><span data-stu-id="8c364-214">hello following PowerShell script creates a key file called **PassEncryptKey.key**.</span></span> <span data-ttu-id="8c364-215">Il fournit également une version chiffrée du mot de passe hello qui est fourni.</span><span class="sxs-lookup"><span data-stu-id="8c364-215">It also provides an encrypted version of hello password that's supplied.</span></span> <span data-ttu-id="8c364-216">Ce mot de passe est hello même mot de passe est défini pour l’application hello Azure Active Directory qui est utilisée pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="8c364-216">This password is hello same password that is defined for hello Azure Active Directory application that's used for authentication.</span></span>

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

<span data-ttu-id="8c364-217">Dans l’éditeur de Service d’application de l’application de fonction hello de hello, créez un dossier appelé **clés** sous **AlertPacketCapturePowerShell**.</span><span class="sxs-lookup"><span data-stu-id="8c364-217">In hello App Service Editor of hello function app, create a folder called **keys** under **AlertPacketCapturePowerShell**.</span></span> <span data-ttu-id="8c364-218">Puis téléchargez hello **PassEncryptKey.key** fichier que vous avez créé dans l’exemple PowerShell précédent de hello.</span><span class="sxs-lookup"><span data-stu-id="8c364-218">Then upload hello **PassEncryptKey.key** file that you created in hello previous PowerShell sample.</span></span>

![Clé de fonctions][functions8]

### <a name="retrieve-values-for-environment-variables"></a><span data-ttu-id="8c364-220">Récupérer des valeurs pour les variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="8c364-220">Retrieve values for environment variables</span></span>

<span data-ttu-id="8c364-221">spécification finale de Hello est tooset les variables d’environnement hello qui sont des valeurs hello tooaccess nécessaire pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="8c364-221">hello final requirement is tooset up hello environment variables that are necessary tooaccess hello values for authentication.</span></span> <span data-ttu-id="8c364-222">Hello liste suivante montre les variables d’environnement hello qui sont créés :</span><span class="sxs-lookup"><span data-stu-id="8c364-222">hello following list shows hello environment variables that are created:</span></span>

* <span data-ttu-id="8c364-223">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="8c364-223">AzureClientID</span></span>

* <span data-ttu-id="8c364-224">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="8c364-224">AzureTenant</span></span>

* <span data-ttu-id="8c364-225">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="8c364-225">AzureCredPassword</span></span>


#### <a name="azureclientid"></a><span data-ttu-id="8c364-226">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="8c364-226">AzureClientID</span></span>

<span data-ttu-id="8c364-227">ID de client Hello est hello ID d’Application d’une application dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8c364-227">hello client ID is hello Application ID of an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="8c364-228">Si vous n’avez pas encore un toouse de l’application, vous pouvez exécuter hello suivant exemple toocreate une application.</span><span class="sxs-lookup"><span data-stu-id="8c364-228">If you don't already have an application toouse, run hello following example toocreate an application.</span></span>

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > <span data-ttu-id="8c364-229">mot de passe Hello que vous utilisez lors de la création d’application hello doit être hello même mot de passe que vous avez créé précédemment lors de l’enregistrement du fichier de clé hello.</span><span class="sxs-lookup"><span data-stu-id="8c364-229">hello password that you use when creating hello application should be hello same password that you created earlier when saving hello key file.</span></span>

1. <span data-ttu-id="8c364-230">Bonjour portail Azure, sélectionnez **abonnements**.</span><span class="sxs-lookup"><span data-stu-id="8c364-230">In hello Azure portal, select **Subscriptions**.</span></span> <span data-ttu-id="8c364-231">Sélectionnez hello abonnement toouse, puis **(IAM) de contrôle d’accès**.</span><span class="sxs-lookup"><span data-stu-id="8c364-231">Select hello subscription toouse, and then select **Access control (IAM)**.</span></span>

    ![IAM de fonctions][functions9]

1. <span data-ttu-id="8c364-233">Choisissez hello compte toouse, puis sélectionnez **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="8c364-233">Choose hello account toouse, and then select **Properties**.</span></span> <span data-ttu-id="8c364-234">Copiez hello ID d’Application.</span><span class="sxs-lookup"><span data-stu-id="8c364-234">Copy hello Application ID.</span></span>

    ![ID de l’application de fonctions][functions10]

#### <a name="azuretenant"></a><span data-ttu-id="8c364-236">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="8c364-236">AzureTenant</span></span>

<span data-ttu-id="8c364-237">Obtenir l’ID du locataire hello en exécutant hello suivant l’exemple PowerShell :</span><span class="sxs-lookup"><span data-stu-id="8c364-237">Obtain hello tenant ID  by running hello following PowerShell sample:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a><span data-ttu-id="8c364-238">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="8c364-238">AzureCredPassword</span></span>

<span data-ttu-id="8c364-239">valeur Hello de variable d’environnement AzureCredPassword hello est la valeur hello que vous obtenez à partir de hello suivant l’exemple PowerShell en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="8c364-239">hello value of hello AzureCredPassword environment variable is hello value that you get from running hello following PowerShell sample.</span></span> <span data-ttu-id="8c364-240">Cet exemple est hello identique à celui illustré hello précédent **informations d’identification chiffrées** section.</span><span class="sxs-lookup"><span data-stu-id="8c364-240">This example is hello same one that's shown in hello preceding **Encrypted credentials** section.</span></span> <span data-ttu-id="8c364-241">Hello valeur suffisant est sortie hello Hello `$Encryptedpassword` variable.</span><span class="sxs-lookup"><span data-stu-id="8c364-241">hello value that's needed is hello output of hello `$Encryptedpassword` variable.</span></span>  <span data-ttu-id="8c364-242">Il s’agit de hello service principal mot de passe que vous avez chiffré à l’aide du script PowerShell de hello.</span><span class="sxs-lookup"><span data-stu-id="8c364-242">This is hello service principal password that you encrypted by using hello PowerShell script.</span></span>

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

### <a name="store-hello-environment-variables"></a><span data-ttu-id="8c364-243">Enregistrer les variables d’environnement hello</span><span class="sxs-lookup"><span data-stu-id="8c364-243">Store hello environment variables</span></span>

1. <span data-ttu-id="8c364-244">Application de fonction toohello accédez.</span><span class="sxs-lookup"><span data-stu-id="8c364-244">Go toohello function app.</span></span> <span data-ttu-id="8c364-245">Sélectionnez ensuite **Paramètres Function App** > **Configurer les paramètres de l’application**.</span><span class="sxs-lookup"><span data-stu-id="8c364-245">Then select **Function app settings** > **Configure app settings**.</span></span>

    ![Configuration des paramètres d’application][functions11]

1. <span data-ttu-id="8c364-247">Ajouter des variables d’environnement hello et leurs paramètres de l’application toohello valeurs, puis sélectionnez **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="8c364-247">Add hello environment variables and their values toohello app settings, and then select **Save**.</span></span>

    ![Paramètres de l’application][functions12]

### <a name="add-powershell-toohello-function"></a><span data-ttu-id="8c364-249">Ajouter la fonction toohello de PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c364-249">Add PowerShell toohello function</span></span>

<span data-ttu-id="8c364-250">Il est maintenant temps toomake appelle dans l’Observateur réseau à partir de hello fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="8c364-250">It's now time toomake calls into Network Watcher from within hello Azure function.</span></span> <span data-ttu-id="8c364-251">Selon les spécifications de hello, implémentation hello de cette fonction peut varier.</span><span class="sxs-lookup"><span data-stu-id="8c364-251">Depending on hello requirements, hello implementation of this function can vary.</span></span> <span data-ttu-id="8c364-252">Toutefois, le flux général de hello du code de hello est comme suit :</span><span class="sxs-lookup"><span data-stu-id="8c364-252">However, hello general flow of hello code is as follows:</span></span>

1. <span data-ttu-id="8c364-253">Traiter les paramètres d’entrée.</span><span class="sxs-lookup"><span data-stu-id="8c364-253">Process input parameters.</span></span>
2. <span data-ttu-id="8c364-254">Paquet de requête existant tooverify limites de capture et résoudre les conflits de nom.</span><span class="sxs-lookup"><span data-stu-id="8c364-254">Query existing packet captures tooverify limits and resolve name conflicts.</span></span>
3. <span data-ttu-id="8c364-255">Créer une capture de paquets avec les paramètres appropriés.</span><span class="sxs-lookup"><span data-stu-id="8c364-255">Create a packet capture with appropriate parameters.</span></span>
4. <span data-ttu-id="8c364-256">Sonder régulièrement la capture de paquets jusqu’à la fin.</span><span class="sxs-lookup"><span data-stu-id="8c364-256">Poll packet capture periodically until it's complete.</span></span>
5. <span data-ttu-id="8c364-257">Avertir les utilisateurs hello que la session de capture de paquets hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="8c364-257">Notify hello user that hello packet capture session is complete.</span></span>

<span data-ttu-id="8c364-258">Hello exemple suivant est le code PowerShell qui peut être utilisé dans la fonction hello.</span><span class="sxs-lookup"><span data-stu-id="8c364-258">hello following example is PowerShell code that can be used in hello function.</span></span> <span data-ttu-id="8c364-259">Il existe des valeurs qui doivent toobe remplacé pour **subscriptionId**, **resourceGroupName**, et **storageAccountName**.</span><span class="sxs-lookup"><span data-stu-id="8c364-259">There are values that need toobe replaced for **subscriptionId**, **resourceGroupName**, and **storageAccountName**.</span></span>

```powershell
            #Import Azure PowerShell modules required toomake calls tooNetwork Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID toosave captures in
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


            #Get hello VM that fired hello alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get hello Network Watcher in hello VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by hello function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on hello VM that fired hello alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-hello-function-url"></a><span data-ttu-id="8c364-260">Récupérer l’URL de fonction hello</span><span class="sxs-lookup"><span data-stu-id="8c364-260">Retrieve hello function URL</span></span> 
1. <span data-ttu-id="8c364-261">Une fois que vous avez créé votre fonction, configurez votre URL hello toocall alerte associée à la fonction hello.</span><span class="sxs-lookup"><span data-stu-id="8c364-261">After you've created your function, configure your alert toocall hello URL that's associated with hello function.</span></span> <span data-ttu-id="8c364-262">tooget cette valeur, la fonction hello copier l’URL à partir de votre application de la fonction.</span><span class="sxs-lookup"><span data-stu-id="8c364-262">tooget this value, copy hello function URL from your function app.</span></span>

    ![URL de recherche hello (fonction)][functions13]

2. <span data-ttu-id="8c364-264">Copier l’URL fonction hello pour votre application de la fonction.</span><span class="sxs-lookup"><span data-stu-id="8c364-264">Copy hello function URL for your function app.</span></span>

    ![Copie l’URL de hello (fonction)][2]

<span data-ttu-id="8c364-266">Si vous avez besoin des propriétés personnalisées dans la charge utile de hello de requête de publication de webhook hello, consultez trop[configurer un webhook sur une alerte de métrique Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="8c364-266">If you require custom properties in hello payload of hello webhook POST request, refer too[Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="configure-an-alert-on-a-vm"></a><span data-ttu-id="8c364-267">Configurer une alerte sur une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="8c364-267">Configure an alert on a VM</span></span>

<span data-ttu-id="8c364-268">Les alertes peuvent être configurés toonotify personnes lorsqu’une métrique spécifique dépasse un seuil affecté tooit.</span><span class="sxs-lookup"><span data-stu-id="8c364-268">Alerts can be configured toonotify individuals when a specific metric crosses a threshold that's assigned tooit.</span></span> <span data-ttu-id="8c364-269">Dans cet exemple, alerte de hello est sur hello segments TCP envoyés, mais les alerte hello peuvent être déclenchée pour nombreuses autres métriques.</span><span class="sxs-lookup"><span data-stu-id="8c364-269">In this example, hello alert is on hello TCP segments that are sent, but hello alert can be triggered for many other metrics.</span></span> <span data-ttu-id="8c364-270">Dans cet exemple, une alerte est configuré toocall une fonction de hello toocall webhook.</span><span class="sxs-lookup"><span data-stu-id="8c364-270">In this example, an alert is configured toocall a webhook toocall hello function.</span></span>

### <a name="create-hello-alert-rule"></a><span data-ttu-id="8c364-271">Créer une règle d’alerte hello</span><span class="sxs-lookup"><span data-stu-id="8c364-271">Create hello alert rule</span></span>

<span data-ttu-id="8c364-272">Atteindre l’ordinateur virtuel existant de tooan, puis ajoutez une règle d’alerte.</span><span class="sxs-lookup"><span data-stu-id="8c364-272">Go tooan existing virtual machine, and then add an alert rule.</span></span> <span data-ttu-id="8c364-273">Pour accéder à une documentation plus détaillée sur la configuration des alertes, consultez l’article [Créer des alertes dans Azure Monitor pour les services Azure - Portail Azure](../monitoring-and-diagnostics/insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8c364-273">More detailed documentation about configuring alerts can be found at [Create alerts in Azure Monitor for Azure services - Azure portal](../monitoring-and-diagnostics/insights-alerts-portal.md).</span></span> <span data-ttu-id="8c364-274">Entrez les valeurs Bonjour suivantes de hello **une règle d’alerte** panneau, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="8c364-274">Enter hello following values in hello **Alert rule** blade, and then select **OK**.</span></span>

  |<span data-ttu-id="8c364-275">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="8c364-275">**Setting**</span></span> | <span data-ttu-id="8c364-276">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="8c364-276">**Value**</span></span> | <span data-ttu-id="8c364-277">**Détails**</span><span class="sxs-lookup"><span data-stu-id="8c364-277">**Details**</span></span> |
  |---|---|---|
  |<span data-ttu-id="8c364-278">**Nom**</span><span class="sxs-lookup"><span data-stu-id="8c364-278">**Name**</span></span>|<span data-ttu-id="8c364-279">TCP_Segments_Sent_Exceeded</span><span class="sxs-lookup"><span data-stu-id="8c364-279">TCP_Segments_Sent_Exceeded</span></span>|<span data-ttu-id="8c364-280">Nom de règle d’alerte hello.</span><span class="sxs-lookup"><span data-stu-id="8c364-280">Name of hello alert rule.</span></span>|
  |<span data-ttu-id="8c364-281">**Description**</span><span class="sxs-lookup"><span data-stu-id="8c364-281">**Description**</span></span>|<span data-ttu-id="8c364-282">Les segments TCP envoyés ont dépassé le seuil</span><span class="sxs-lookup"><span data-stu-id="8c364-282">TCP segments sent exceeded threshold</span></span>|<span data-ttu-id="8c364-283">description de Hello pour la règle d’alerte hello.</span><span class="sxs-lookup"><span data-stu-id="8c364-283">hello description for hello alert rule.</span></span>||
  |<span data-ttu-id="8c364-284">**Mesure**</span><span class="sxs-lookup"><span data-stu-id="8c364-284">**Metric**</span></span>|<span data-ttu-id="8c364-285">Segments TCP envoyés</span><span class="sxs-lookup"><span data-stu-id="8c364-285">TCP segments sent</span></span>| <span data-ttu-id="8c364-286">alerte de hello tootrigger Hello toouse métrique.</span><span class="sxs-lookup"><span data-stu-id="8c364-286">hello metric toouse tootrigger hello alert.</span></span> |
  |<span data-ttu-id="8c364-287">**Condition**</span><span class="sxs-lookup"><span data-stu-id="8c364-287">**Condition**</span></span>|<span data-ttu-id="8c364-288">Supérieur à</span><span class="sxs-lookup"><span data-stu-id="8c364-288">Greater than</span></span>| <span data-ttu-id="8c364-289">Hello condition toouse lors de l’évaluation de métrique de hello.</span><span class="sxs-lookup"><span data-stu-id="8c364-289">hello condition toouse when evaluating hello metric.</span></span>|
  |<span data-ttu-id="8c364-290">**Seuil**</span><span class="sxs-lookup"><span data-stu-id="8c364-290">**Threshold**</span></span>|<span data-ttu-id="8c364-291">100</span><span class="sxs-lookup"><span data-stu-id="8c364-291">100</span></span>| <span data-ttu-id="8c364-292">valeur Hello de métrique hello qui a déclenché l’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="8c364-292">hello  value of hello metric that triggers hello alert.</span></span> <span data-ttu-id="8c364-293">Cette valeur doit être définie tooa de valeur valide pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="8c364-293">This value should be set tooa valid value for your environment.</span></span>|
  |<span data-ttu-id="8c364-294">**Période**</span><span class="sxs-lookup"><span data-stu-id="8c364-294">**Period**</span></span>|<span data-ttu-id="8c364-295">Sur hello cinq dernières minutes</span><span class="sxs-lookup"><span data-stu-id="8c364-295">Over hello last five minutes</span></span>| <span data-ttu-id="8c364-296">Détermine la période dans le toolook hello pour le seuil de hello sur métrique de hello.</span><span class="sxs-lookup"><span data-stu-id="8c364-296">Determines hello period in which toolook for hello threshold on hello metric.</span></span>|
  |<span data-ttu-id="8c364-297">**Webhook**</span><span class="sxs-lookup"><span data-stu-id="8c364-297">**Webhook**</span></span>|<span data-ttu-id="8c364-298">[URL du webhook de l’application de fonction]</span><span class="sxs-lookup"><span data-stu-id="8c364-298">[webhook URL from function app]</span></span>| <span data-ttu-id="8c364-299">URL du webhook Hello à partir de l’application hello fonction qui a été créée dans les étapes précédentes hello.</span><span class="sxs-lookup"><span data-stu-id="8c364-299">hello webhook URL from hello function app that was created in hello previous steps.</span></span>|

> [!NOTE]
> <span data-ttu-id="8c364-300">métrique de segments TCP Hello n’est pas activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="8c364-300">hello TCP segments metric is not enabled by default.</span></span> <span data-ttu-id="8c364-301">En savoir plus sur la façon tooenable des métriques supplémentaires en vous rendant sur [activation de la surveillance et de diagnostics](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="8c364-301">Learn more about how tooenable additional metrics by visiting [Enable monitoring and diagnostics](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span></span>

## <a name="review-hello-results"></a><span data-ttu-id="8c364-302">Passez en revue les résultats de hello</span><span class="sxs-lookup"><span data-stu-id="8c364-302">Review hello results</span></span>

<span data-ttu-id="8c364-303">Une fois les critères hello pour les déclencheurs d’alerte hello, une capture de paquets est créée.</span><span class="sxs-lookup"><span data-stu-id="8c364-303">After hello criteria for hello alert triggers, a packet capture is created.</span></span> <span data-ttu-id="8c364-304">Accédez tooNetwork Observateur, puis sélectionnez **capture des paquets**.</span><span class="sxs-lookup"><span data-stu-id="8c364-304">Go tooNetwork Watcher, and then select **Packet capture**.</span></span> <span data-ttu-id="8c364-305">Dans cette page, vous pouvez sélectionner la capture des paquets hello fichier lien toodownload hello paquet capture.</span><span class="sxs-lookup"><span data-stu-id="8c364-305">On this page, you can select hello packet capture file link toodownload hello packet capture.</span></span>

![Afficher une capture de paquets][functions14]

<span data-ttu-id="8c364-307">Si le fichier de capture hello est stockée localement, vous pouvez le récupérer en vous connectant toohello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8c364-307">If hello capture file is stored locally, you can retrieve it by signing in toohello virtual machine.</span></span>

<span data-ttu-id="8c364-308">Pour obtenir des instructions sur le téléchargement de fichiers à partir de comptes de stockage Azure, consultez [Prise en main du stockage d’objets blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="8c364-308">For instructions about downloading files from Azure storage accounts, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="8c364-309">Vous pouvez aussi utiliser [l’Explorateur de stockage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="8c364-309">Another tool you can use is [Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="8c364-310">Une fois la capture téléchargée, vous pouvez l’afficher à l’aide de n’importe quel outil en mesure de lire un fichier **.cap**.</span><span class="sxs-lookup"><span data-stu-id="8c364-310">After your capture has been downloaded, you can view it by using any tool that can read a **.cap** file.</span></span> <span data-ttu-id="8c364-311">Voici les tootwo des liens de ces outils :</span><span class="sxs-lookup"><span data-stu-id="8c364-311">Following are links tootwo of these tools:</span></span>

- [<span data-ttu-id="8c364-312">Microsoft Message Analyzer</span><span class="sxs-lookup"><span data-stu-id="8c364-312">Microsoft Message Analyzer</span></span>](https://technet.microsoft.com/library/jj649776.aspx)
- [<span data-ttu-id="8c364-313">WireShark</span><span class="sxs-lookup"><span data-stu-id="8c364-313">WireShark</span></span>](https://www.wireshark.org/)

## <a name="next-steps"></a><span data-ttu-id="8c364-314">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8c364-314">Next steps</span></span>

<span data-ttu-id="8c364-315">Découvrez comment tooview vos captures de paquets en vous rendant sur [analyse des paquets de capture avec Wireshark](network-watcher-deep-packet-inspection.md).</span><span class="sxs-lookup"><span data-stu-id="8c364-315">Learn how tooview your packet captures by visiting [Packet capture analysis with Wireshark](network-watcher-deep-packet-inspection.md).</span></span>


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
