---
title: "Intégrer les journaux d’Azure Key Vault à l’aide d’Event Hubs | Microsoft Docs"
description: "Didacticiel décrivant la procédure requise pour rendre accessibles les journaux Key Vault à un système SIEM (Security Information and Event Management, système de gestion des événements et des informations de sécurité) grâce à la solution d’intégration des journaux Azure"
services: security
author: barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.topic: article
ms.date: 08/07/2017
ms.author: Barclayn
ms.custom: AzLog
ms.openlocfilehash: 3cd80817bf8b2ef2f66e9942eddc186a3eb5b5e4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a><span data-ttu-id="e399b-103">Didacticiel sur l’intégration des journaux Azure : traiter les événements Azure Key Vault à l’aide d’Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e399b-103">Azure Log Integration tutorial: Process Azure Key Vault events by using Event Hubs</span></span>

<span data-ttu-id="e399b-104">Vous pouvez utiliser la solution d’intégration des journaux Azure pour récupérer des événements journalisés et les rendre accessibles à votre système de gestion des événements et des informations de sécurité (SIEM, Security Information and Event Management).</span><span class="sxs-lookup"><span data-stu-id="e399b-104">You can use Azure Log Integration to retrieve logged events and make them available to your security information and event management (SIEM) system.</span></span> <span data-ttu-id="e399b-105">Ce didacticiel montre comment utiliser Azure Log Integration pour traiter les fichiers journaux qui sont acquis par le service Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="e399b-105">This tutorial shows an example of how Azure Log Integration can be used to process logs that are acquired through Azure Event Hubs.</span></span>
 
<span data-ttu-id="e399b-106">Ce didacticiel aide à mieux comprendre comment Azure Log Integration et Event Hubs peuvent être utilisés conjointement, et explique chacune des étapes impliquées.</span><span class="sxs-lookup"><span data-stu-id="e399b-106">Use this tutorial to get acquainted with how Azure Log Integration and Event Hubs work together by following the example steps and understanding how each step supports the solution.</span></span> <span data-ttu-id="e399b-107">Vous pouvez ensuite vous appuyer sur ce que vous avez appris ici pour répondre aux besoins spécifiques de votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="e399b-107">Then you can take what you’ve learned here to create your own steps to support your company’s unique requirements.</span></span>

>[!WARNING]
<span data-ttu-id="e399b-108">Les étapes et commandes de ce didacticiel ne sont pas destinées à être copiées et collées.</span><span class="sxs-lookup"><span data-stu-id="e399b-108">The steps and commands in this tutorial are not intended to be copied and pasted.</span></span> <span data-ttu-id="e399b-109">Elles sont uniquement indiquées à titre d’exemple.</span><span class="sxs-lookup"><span data-stu-id="e399b-109">They're examples only.</span></span> <span data-ttu-id="e399b-110">N’utilisez pas les commandes PowerShell telles quelles dans votre environnement de production.</span><span class="sxs-lookup"><span data-stu-id="e399b-110">Do not use the PowerShell commands “as is” in your live environment.</span></span> <span data-ttu-id="e399b-111">Vous devez en effet les personnaliser en fonction de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="e399b-111">You must customize them based on your unique environment.</span></span>


<span data-ttu-id="e399b-112">Ce didacticiel vous guide tout au long de la procédure qui consiste à récupérer des activités Azure Key Vault journalisées dans un Event Hub et à mettre ces activités à la disposition de votre système SIEM sous la forme de fichiers JSON.</span><span class="sxs-lookup"><span data-stu-id="e399b-112">This tutorial walks you through the process of taking Azure Key Vault activity logged to an event hub and making it available as JSON files to your SIEM system.</span></span> <span data-ttu-id="e399b-113">Vous pouvez ensuite configurer votre système SIEM pour qu’il procède au traitement de ces fichiers JSON.</span><span class="sxs-lookup"><span data-stu-id="e399b-113">You can then configure your SIEM system to process the JSON files.</span></span>

>[!NOTE]
><span data-ttu-id="e399b-114">La plupart des étapes de ce didacticiel impliquent la configuration de coffres de clé, de comptes de stockage et d’Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="e399b-114">Most of the steps in this tutorial involve configuring key vaults, storage accounts, and event hubs.</span></span> <span data-ttu-id="e399b-115">La procédure d’intégration des journaux Azure est décrite à la fin de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="e399b-115">The specific Azure Log Integration steps are at the end of this tutorial.</span></span> <span data-ttu-id="e399b-116">N’effectuez pas ces étapes dans un environnement de production,</span><span class="sxs-lookup"><span data-stu-id="e399b-116">Do not perform these steps in a production environment.</span></span> <span data-ttu-id="e399b-117">car elles sont uniquement destinées à un environnement lab.</span><span class="sxs-lookup"><span data-stu-id="e399b-117">They are intended for a lab environment only.</span></span> <span data-ttu-id="e399b-118">Vous devez les adapter avant de les utiliser dans un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="e399b-118">You must customize the steps before using them in production.</span></span>

<span data-ttu-id="e399b-119">Les informations fournies tout au long de la procédure vous expliquent la finalité de chaque étape.</span><span class="sxs-lookup"><span data-stu-id="e399b-119">Information provided along the way helps you understand the reasons behind each step.</span></span> <span data-ttu-id="e399b-120">Les liens d’accès à d’autres articles offrent des détails complémentaires sur certains sujets.</span><span class="sxs-lookup"><span data-stu-id="e399b-120">Links to other articles give you more detail on certain topics.</span></span>

<span data-ttu-id="e399b-121">Pour plus d’informations sur les services mentionnés par ce didacticiel, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="e399b-121">For more information about the services that this tutorial mentions, see:</span></span> 

- [<span data-ttu-id="e399b-122">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="e399b-122">Azure Key Vault</span></span>](../key-vault/key-vault-whatis.md)
- [<span data-ttu-id="e399b-123">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e399b-123">Azure Event Hubs</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="e399b-124">Intégration des journaux Azure</span><span class="sxs-lookup"><span data-stu-id="e399b-124">Azure Log Integration</span></span>](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a><span data-ttu-id="e399b-125">Configuration initiale</span><span class="sxs-lookup"><span data-stu-id="e399b-125">Initial setup</span></span>

<span data-ttu-id="e399b-126">Pour exécuter la procédure décrite dans cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e399b-126">Before you can complete the steps in this article, you need the following:</span></span>

1. <span data-ttu-id="e399b-127">Un abonnement Azure et un compte dans cet abonnement avec des droits d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="e399b-127">An Azure subscription and account on that subscription with administrator rights.</span></span> <span data-ttu-id="e399b-128">Si vous ne disposez d’aucun abonnement, vous pouvez créer [un compte gratuitement](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="e399b-128">If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/).</span></span>
 
2. <span data-ttu-id="e399b-129">Un système doté d’un accès à Internet qui présente la configuration requise pour l’installation d’Azure Log Integration.</span><span class="sxs-lookup"><span data-stu-id="e399b-129">A system with access to the internet that meets the requirements for installing Azure Log Integration.</span></span> <span data-ttu-id="e399b-130">Ce système peut se trouver dans un service cloud ou être hébergé localement.</span><span class="sxs-lookup"><span data-stu-id="e399b-130">The system can be on a cloud service or hosted on-premises.</span></span>

3. <span data-ttu-id="e399b-131">Solution d’[intégration des journaux Azure](https://www.microsoft.com/download/details.aspx?id=53324) installée.</span><span class="sxs-lookup"><span data-stu-id="e399b-131">[Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) installed.</span></span> <span data-ttu-id="e399b-132">Pour l’installer :</span><span class="sxs-lookup"><span data-stu-id="e399b-132">To install it:</span></span>

   <span data-ttu-id="e399b-133">a.</span><span class="sxs-lookup"><span data-stu-id="e399b-133">a.</span></span> <span data-ttu-id="e399b-134">Utilisez la fonctionnalité Bureau à distance pour vous connecter au système mentionné à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="e399b-134">Use Remote Desktop to connect to the system mentioned in step 2.</span></span>   
   <span data-ttu-id="e399b-135">b.</span><span class="sxs-lookup"><span data-stu-id="e399b-135">b.</span></span> <span data-ttu-id="e399b-136">Copiez le programme d’installation de l’intégration des journaux Azure sur le système.</span><span class="sxs-lookup"><span data-stu-id="e399b-136">Copy the Azure Log Integration installer to the system.</span></span> <span data-ttu-id="e399b-137">Vous pouvez [télécharger les fichiers d’installation](https://www.microsoft.com/download/details.aspx?id=53324).</span><span class="sxs-lookup"><span data-stu-id="e399b-137">You can [download the installation files](https://www.microsoft.com/download/details.aspx?id=53324).</span></span>   
   <span data-ttu-id="e399b-138">c.</span><span class="sxs-lookup"><span data-stu-id="e399b-138">c.</span></span> <span data-ttu-id="e399b-139">Démarrez le programme d’installation et acceptez les Termes du contrat de licence logiciel Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e399b-139">Start the installer and accept the Microsoft Software License Terms.</span></span>   
   <span data-ttu-id="e399b-140">d.</span><span class="sxs-lookup"><span data-stu-id="e399b-140">d.</span></span> <span data-ttu-id="e399b-141">Si vous souhaitez fournir des informations de télémétrie, laissez la case cochée.</span><span class="sxs-lookup"><span data-stu-id="e399b-141">If you will provide telemetry information, leave the check box selected.</span></span> <span data-ttu-id="e399b-142">Si vous préférez ne pas envoyer d’informations d’utilisation à Microsoft, décochez la case.</span><span class="sxs-lookup"><span data-stu-id="e399b-142">If you'd rather not send usage information to Microsoft, clear the check box.</span></span>
   
   <span data-ttu-id="e399b-143">Pour plus d’informations sur Azure Log Integration et sur son installation, consultez l’article [Intégration des journaux Azure avec Azure Diagnostics Logging et Windows Event Forwarding](security-azure-log-integration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e399b-143">For more information about Azure Log Integration and how to install it, see [Azure Log Integration with Azure Diagnostics logging and Windows Event Forwarding](security-azure-log-integration-get-started.md).</span></span>

4. <span data-ttu-id="e399b-144">La dernière version de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e399b-144">The latest PowerShell version.</span></span>
 
   <span data-ttu-id="e399b-145">Si vous avez installé Windows Server 2016, vous disposez au moins de PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="e399b-145">If you have Windows Server 2016 installed, then you have at least PowerShell 5.0.</span></span> <span data-ttu-id="e399b-146">Si vous utilisez une autre version de Windows Server, il est possible que vous possédiez une version antérieure de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e399b-146">If you're using any other version of Windows Server, you might have an earlier version of PowerShell installed.</span></span> <span data-ttu-id="e399b-147">Pour vérifier la version que vous utilisez, tapez ```get-host``` dans une fenêtre PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e399b-147">You can check the version by entering ```get-host``` in a PowerShell window.</span></span> <span data-ttu-id="e399b-148">Si vous n’avez pas installé PowerShell 5.0, vous pouvez [le télécharger](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="e399b-148">If you don't have PowerShell 5.0 installed, you can [download it](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>

   <span data-ttu-id="e399b-149">Une fois que vous disposez de PowerShell 5.0 ou d’une version supérieure, vous pouvez procéder à l’installation de la dernière version :</span><span class="sxs-lookup"><span data-stu-id="e399b-149">After you have at least PowerShell 5.0, you can proceed to install the latest version:</span></span>
   
   <span data-ttu-id="e399b-150">a.</span><span class="sxs-lookup"><span data-stu-id="e399b-150">a.</span></span> <span data-ttu-id="e399b-151">Dans une fenêtre PowerShell, entrez la commande ```Install-Module Azure```.</span><span class="sxs-lookup"><span data-stu-id="e399b-151">In a PowerShell window, enter the ```Install-Module Azure``` command.</span></span> <span data-ttu-id="e399b-152">Suivez la procédure d’installation.</span><span class="sxs-lookup"><span data-stu-id="e399b-152">Complete the installation steps.</span></span>    
   <span data-ttu-id="e399b-153">b.</span><span class="sxs-lookup"><span data-stu-id="e399b-153">b.</span></span> <span data-ttu-id="e399b-154">Entrez la commande ```Install-Module AzureRM```.</span><span class="sxs-lookup"><span data-stu-id="e399b-154">Enter the ```Install-Module AzureRM``` command.</span></span> <span data-ttu-id="e399b-155">Suivez la procédure d’installation.</span><span class="sxs-lookup"><span data-stu-id="e399b-155">Complete the installation steps.</span></span>

   <span data-ttu-id="e399b-156">Pour plus d’informations, consultez l’article [Installation et configuration d’Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="e399b-156">For more information, see [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span>


## <a name="create-supporting-infrastructure-elements"></a><span data-ttu-id="e399b-157">Créer les éléments d’infrastructure sous-jacents</span><span class="sxs-lookup"><span data-stu-id="e399b-157">Create supporting infrastructure elements</span></span>

1. <span data-ttu-id="e399b-158">Ouvrez une fenêtre PowerShell avec élévation de privilèges et accédez à **C:\Program Files\Microsoft Azure Log Integration**.</span><span class="sxs-lookup"><span data-stu-id="e399b-158">Open an elevated PowerShell window and go to **C:\Program Files\Microsoft Azure Log Integration**.</span></span>
2. <span data-ttu-id="e399b-159">Importez les applets de commande AzLog en exécutant le script LoadAzLogModule.ps1.</span><span class="sxs-lookup"><span data-stu-id="e399b-159">Import the AzLog cmdlets by running the script LoadAzLogModule.ps1.</span></span> <span data-ttu-id="e399b-160">Entrez la commande `.\LoadAzLogModule.ps1`.</span><span class="sxs-lookup"><span data-stu-id="e399b-160">Enter the `.\LoadAzLogModule.ps1` command.</span></span> <span data-ttu-id="e399b-161">(Notez la présence des caractères « .\ » dans cette commande.) Le résultat suivant devrait s'afficher :</span><span class="sxs-lookup"><span data-stu-id="e399b-161">(Notice the “.\” in that command.) You should see something like this:</span></span></br>

   ![Liste des modules chargés](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. <span data-ttu-id="e399b-163">Entrez la commande `Login-AzureRmAccount`.</span><span class="sxs-lookup"><span data-stu-id="e399b-163">Enter the `Login-AzureRmAccount` command.</span></span> <span data-ttu-id="e399b-164">Dans la fenêtre de connexion, entrez les informations d’identification de l’abonnement que vous allez utiliser dans le cadre de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="e399b-164">In the login window, enter the credential information for the subscription that you will use for this tutorial.</span></span>

   >[!NOTE]
   ><span data-ttu-id="e399b-165">S’il s’agit de votre première connexion à Azure à partir de cette machine, vous verrez un message destiné à autoriser Microsoft à collecter les données d’utilisation de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e399b-165">If this is the first time that you're logging in to Azure from this machine, you will see a message about allowing Microsoft to collect PowerShell usage data.</span></span> <span data-ttu-id="e399b-166">Nous vous recommandons d’autoriser cette collecte de données, car elle nous permettra d’améliorer Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e399b-166">We recommend that you enable this data collection because it will be used to improve Azure PowerShell.</span></span>

4. <span data-ttu-id="e399b-167">Après vous être authentifié, vous êtes connecté et voyez apparaître les informations figurant dans la capture d’écran ci-après.</span><span class="sxs-lookup"><span data-stu-id="e399b-167">After successful authentication, you're logged in and you see the information in the following screenshot.</span></span> <span data-ttu-id="e399b-168">Notez l’ID et le nom de l’abonnement, car vous aurez besoin de ces éléments dans la suite de cette procédure.</span><span class="sxs-lookup"><span data-stu-id="e399b-168">Take note of the subscription ID and subscription name, because you'll need them to complete later steps.</span></span>

   ![Fenêtre PowerShell](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. <span data-ttu-id="e399b-170">Créez des variables pour stocker les valeurs qui seront utilisées par la suite.</span><span class="sxs-lookup"><span data-stu-id="e399b-170">Create variables to store values that will be used later.</span></span> <span data-ttu-id="e399b-171">Entrez chacune des lignes PowerShell suivantes.</span><span class="sxs-lookup"><span data-stu-id="e399b-171">Enter each of the following PowerShell lines.</span></span> <span data-ttu-id="e399b-172">Vous devrez peut-être ajuster les valeurs pour les faire correspondre à votre environnement.</span><span class="sxs-lookup"><span data-stu-id="e399b-172">You might need to adjust the values to match your environment.</span></span>
    - <span data-ttu-id="e399b-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (Votre nom d’abonnement peut être différent.</span><span class="sxs-lookup"><span data-stu-id="e399b-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (Your subscription name might be different.</span></span> <span data-ttu-id="e399b-174">Vous pouvez le voir apparaître dans la sortie de la commande précédente.)</span><span class="sxs-lookup"><span data-stu-id="e399b-174">You can see it as part of the output of the previous command.)</span></span>
    - <span data-ttu-id="e399b-175">```$location = 'West US'``` (Cette variable est utilisée pour transmettre l’emplacement où les ressources doivent être créées.</span><span class="sxs-lookup"><span data-stu-id="e399b-175">```$location = 'West US'``` (This variable will be used to pass the location where resources should be created.</span></span> <span data-ttu-id="e399b-176">Vous pouvez redéfinir cette variable sur tout autre emplacement de votre choix.)</span><span class="sxs-lookup"><span data-stu-id="e399b-176">You can change this variable to be any location of your choosing.)</span></span>
    - ```$random = Get-Random```
    - <span data-ttu-id="e399b-177">``` $name = 'azlogtest' + $random``` (Le nom peut correspondre à une chaîne quelconque, mais doit uniquement inclure des lettres minuscules et des chiffres.)</span><span class="sxs-lookup"><span data-stu-id="e399b-177">``` $name = 'azlogtest' + $random``` (The name can be anything, but it should include only lowercase letters and numbers.)</span></span>
    - <span data-ttu-id="e399b-178">``` $storageName = $name``` (Cette variable est utilisée pour le nom du compte de stockage.)</span><span class="sxs-lookup"><span data-stu-id="e399b-178">``` $storageName = $name``` (This variable will be used for the storage account name.)</span></span>
    - <span data-ttu-id="e399b-179">```$rgname = $name ``` (Cette variable est utilisée pour le nom du groupe de ressources.)</span><span class="sxs-lookup"><span data-stu-id="e399b-179">```$rgname = $name ``` (This variable will be used for the resource group name.)</span></span>
    - <span data-ttu-id="e399b-180">``` $eventHubNameSpaceName = $name``` (Cette variable correspond au nom de l’espace de noms Event Hub.)</span><span class="sxs-lookup"><span data-stu-id="e399b-180">``` $eventHubNameSpaceName = $name``` (This is the name of the event hub namespace.)</span></span>
6. <span data-ttu-id="e399b-181">Spécifiez l’abonnement que vous allez utiliser :</span><span class="sxs-lookup"><span data-stu-id="e399b-181">Specify the subscription that you will be working with:</span></span>
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. <span data-ttu-id="e399b-182">Créez un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="e399b-182">Create a resource group:</span></span>
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   <span data-ttu-id="e399b-183">Si vous tapez `$rg` à ce stade, vous verrez apparaître une sortie semblable à la capture d’écran ci-après :</span><span class="sxs-lookup"><span data-stu-id="e399b-183">If you enter `$rg` at this point, you should see output similar to this screenshot:</span></span>

   ![Sortie après la création d’un groupe de ressources](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. <span data-ttu-id="e399b-185">Créez un compte de stockage qui servira à effectuer le suivi des informations d’état :</span><span class="sxs-lookup"><span data-stu-id="e399b-185">Create a storage account that will be used to keep track of state information:</span></span>
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. <span data-ttu-id="e399b-186">Créez l’espace de noms Event Hub.</span><span class="sxs-lookup"><span data-stu-id="e399b-186">Create the event hub namespace.</span></span> <span data-ttu-id="e399b-187">Cette opération est requise pour la création d’un Event Hub.</span><span class="sxs-lookup"><span data-stu-id="e399b-187">This is required to create an event hub.</span></span>
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. <span data-ttu-id="e399b-188">Obtenez l’ID de règle qui sera utilisé avec le fournisseur d’informations :</span><span class="sxs-lookup"><span data-stu-id="e399b-188">Get the rule ID that will be used with the insights provider:</span></span>
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. <span data-ttu-id="e399b-189">Obtenez tous les emplacements Azure possibles et ajoutez les noms à une variable que vous pourrez utiliser à une étape ultérieure :</span><span class="sxs-lookup"><span data-stu-id="e399b-189">Get all possible Azure locations and add the names to a variable that can be used in a later step:</span></span>
    
    <span data-ttu-id="e399b-190">a.</span><span class="sxs-lookup"><span data-stu-id="e399b-190">a.</span></span> ```$locationObjects = Get-AzureRMLocation```    
    <span data-ttu-id="e399b-191">b.</span><span class="sxs-lookup"><span data-stu-id="e399b-191">b.</span></span> ```$locations = @('global') + $locationobjects.location```
    
    <span data-ttu-id="e399b-192">Si vous tapez `$locations` à ce stade, vous verrez apparaître les noms d’emplacement sans les informations supplémentaires renvoyées par Get-AzureRmLocation.</span><span class="sxs-lookup"><span data-stu-id="e399b-192">If you enter `$locations` at this point, you see the location names without the additional information returned by Get-AzureRmLocation.</span></span>
12. <span data-ttu-id="e399b-193">Créez un profil de journal Azure Resource Manager :</span><span class="sxs-lookup"><span data-stu-id="e399b-193">Create an Azure Resource Manager log profile:</span></span> 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    <span data-ttu-id="e399b-194">Pour plus d’informations sur le profil de journal Azure, consultez l’article [Présentation du journal d’activité Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="e399b-194">For more information about the Azure log profile, see [Overview of the Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e399b-195">Il est possible que vous obteniez un message d’erreur lorsque vous essayez de créer un profil de journal.</span><span class="sxs-lookup"><span data-stu-id="e399b-195">You might get an error message when you try to create a log profile.</span></span> <span data-ttu-id="e399b-196">Vous pouvez alors consulter la documentation des commandes Get-AzureRmLogProfile et Remove-AzureRmLogProfile.</span><span class="sxs-lookup"><span data-stu-id="e399b-196">You can then review the documentation for Get-AzureRmLogProfile and Remove-AzureRmLogProfile.</span></span> <span data-ttu-id="e399b-197">Si vous exécutez Get-AzureRmLogProfile, vous obtenez des informations sur le profil de journal.</span><span class="sxs-lookup"><span data-stu-id="e399b-197">If you run Get-AzureRmLogProfile, you see information about the log profile.</span></span> <span data-ttu-id="e399b-198">Vous pouvez supprimer le profil de journal existant en entrant la commande ```Remove-AzureRmLogProfile -name 'Log Profile Name' ```.</span><span class="sxs-lookup"><span data-stu-id="e399b-198">You can delete the existing log profile by entering the ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` command.</span></span>
>
>![Erreur de profil Resource Manager](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a><span data-ttu-id="e399b-200">Création d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="e399b-200">Create a key vault</span></span>

1. <span data-ttu-id="e399b-201">Créez le coffre de clés :</span><span class="sxs-lookup"><span data-stu-id="e399b-201">Create the key vault:</span></span>

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. <span data-ttu-id="e399b-202">Configurez la journalisation relative au coffre de clés :</span><span class="sxs-lookup"><span data-stu-id="e399b-202">Configure logging for the key vault:</span></span>

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a><span data-ttu-id="e399b-203">Générer l’activité de journalisation</span><span class="sxs-lookup"><span data-stu-id="e399b-203">Generate log activity</span></span>

<span data-ttu-id="e399b-204">La génération de l’activité de journalisation nécessite l’envoi de requêtes à Key Vault.</span><span class="sxs-lookup"><span data-stu-id="e399b-204">Requests need to be sent to Key Vault to generate log activity.</span></span> <span data-ttu-id="e399b-205">Des actions telles que la génération de clés, le stockage de secrets ou la lecture de secrets à partir de Key Vault entraînent la création d’entrées de journal.</span><span class="sxs-lookup"><span data-stu-id="e399b-205">Actions like key generation, storing secrets, or reading secrets from Key Vault will create log entries.</span></span>

1. <span data-ttu-id="e399b-206">Affichez les clés de stockage actuelles :</span><span class="sxs-lookup"><span data-stu-id="e399b-206">Display the current storage keys:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. <span data-ttu-id="e399b-207">Générez une nouvelle valeur **key2** :</span><span class="sxs-lookup"><span data-stu-id="e399b-207">Generate a new **key2**:</span></span>
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. <span data-ttu-id="e399b-208">Réaffichez les clés et notez que l’élément **key2** présente une autre valeur :</span><span class="sxs-lookup"><span data-stu-id="e399b-208">Display the keys again and see that **key2** holds a different value:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. <span data-ttu-id="e399b-209">Définissez et lisez un secret pour générer des entrées de journal supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="e399b-209">Set and read a secret to generate additional log entries:</span></span>
    
   <span data-ttu-id="e399b-210">a.</span><span class="sxs-lookup"><span data-stu-id="e399b-210">a.</span></span> <span data-ttu-id="e399b-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span><span class="sxs-lookup"><span data-stu-id="e399b-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span></span> ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![Secret renvoyé](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a><span data-ttu-id="e399b-213">Configurer l’intégration des journaux Azure</span><span class="sxs-lookup"><span data-stu-id="e399b-213">Configure Azure Log Integration</span></span>

<span data-ttu-id="e399b-214">À présent que vous avez configuré tous les éléments nécessaires pour activer la journalisation Key Vault dans un Event Hub, vous devez configurer l’intégration des journaux Azure :</span><span class="sxs-lookup"><span data-stu-id="e399b-214">Now that you have configured all the required elements to have Key Vault logging to an event hub, you need to configure Azure Log Integration:</span></span>

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

<span data-ttu-id="e399b-215">Exécutez la commande AzLog pour chaque Event Hub :</span><span class="sxs-lookup"><span data-stu-id="e399b-215">Run the AzLog command for each event hub:</span></span>

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

<span data-ttu-id="e399b-216">Au bout d’une minute environ après l’exécution des deux dernières commandes, vous devriez voir les fichiers JSON en cours de génération.</span><span class="sxs-lookup"><span data-stu-id="e399b-216">After a minute or so of running the last two commands, you should see JSON files being generated.</span></span> <span data-ttu-id="e399b-217">Pour vérifier ce point, surveillez le répertoire **C:\users\AzLog\EventHubJson**.</span><span class="sxs-lookup"><span data-stu-id="e399b-217">You can confirm that by monitoring the directory **C:\users\AzLog\EventHubJson**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e399b-218">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e399b-218">Next steps</span></span>

- [<span data-ttu-id="e399b-219">Forum aux questions sur l’intégration des journaux Azure</span><span class="sxs-lookup"><span data-stu-id="e399b-219">Azure Log Integration FAQ</span></span>](security-azure-log-integration-faq.md)
- [<span data-ttu-id="e399b-220">Bien démarrer avec l’intégration des journaux Azure</span><span class="sxs-lookup"><span data-stu-id="e399b-220">Get started with Azure Log Integration</span></span>](security-azure-log-integration-get-started.md)
- [<span data-ttu-id="e399b-221">Intégrer des journaux à partir de ressources Azure dans vos systèmes SIEM</span><span class="sxs-lookup"><span data-stu-id="e399b-221">Integrate logs from Azure resources into your SIEM systems</span></span>](security-azure-log-integration-overview.md)
