---
title: "journaux aaaIntegrate d’Azure Key Vault à l’aide de concentrateurs d’événements | Documents Microsoft"
description: "Didacticiel qui fournit les étapes nécessaires de hello toomake le coffre de clés journaux disponible tooa SIEM grâce à l’intégration des journaux Azure"
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
ms.openlocfilehash: ada2fc846cc6bf09e12cc2c016815b27afef0d50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a><span data-ttu-id="3b8f4-103">Didacticiel sur l’intégration des journaux Azure : traiter les événements Azure Key Vault à l’aide d’Event Hubs</span><span class="sxs-lookup"><span data-stu-id="3b8f4-103">Azure Log Integration tutorial: Process Azure Key Vault events by using Event Hubs</span></span>

<span data-ttu-id="3b8f4-104">Vous pouvez utiliser les événements d’intégration des journaux Azure tooretrieve connecté et les rendre disponibles tooyour événements et des informations système security management (SIEM).</span><span class="sxs-lookup"><span data-stu-id="3b8f4-104">You can use Azure Log Integration tooretrieve logged events and make them available tooyour security information and event management (SIEM) system.</span></span> <span data-ttu-id="3b8f4-105">Ce didacticiel montre comment intégration des journaux Azure peuvent être des journaux tooprocess utilisés qui sont acquis par Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-105">This tutorial shows an example of how Azure Log Integration can be used tooprocess logs that are acquired through Azure Event Hubs.</span></span>
 
<span data-ttu-id="3b8f4-106">Utilisez ce didacticiel tooget connaissance des comment le travail d’intégration des journaux Azure et les concentrateurs d’événements en suivant hello exemples d’étapes et de comprendre comment chaque étape prend en charge les solutions hello.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-106">Use this tutorial tooget acquainted with how Azure Log Integration and Event Hubs work together by following hello example steps and understanding how each step supports hello solution.</span></span> <span data-ttu-id="3b8f4-107">Ensuite, vous pouvez prendre ce que vous avez appris ici toocreate toosupport de vos propres étapes exigences uniques de votre société.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-107">Then you can take what you’ve learned here toocreate your own steps toosupport your company’s unique requirements.</span></span>

>[!WARNING]
<span data-ttu-id="3b8f4-108">étapes de Hello et les commandes de ce didacticiel ne sont pas prévu toobe copiées et collées.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-108">hello steps and commands in this tutorial are not intended toobe copied and pasted.</span></span> <span data-ttu-id="3b8f4-109">Elles sont uniquement indiquées à titre d’exemple.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-109">They're examples only.</span></span> <span data-ttu-id="3b8f4-110">N’utilisez pas les commandes de PowerShell hello « tel quel » dans votre environnement dynamique.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-110">Do not use hello PowerShell commands “as is” in your live environment.</span></span> <span data-ttu-id="3b8f4-111">Vous devez en effet les personnaliser en fonction de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-111">You must customize them based on your unique environment.</span></span>


<span data-ttu-id="3b8f4-112">Ce didacticiel vous guide tout au long des processus hello concentrateur d’événements Azure Key Vault activité tooan connecté et rendre disponible en tant que système SIEM JSON fichiers tooyour de.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-112">This tutorial walks you through hello process of taking Azure Key Vault activity logged tooan event hub and making it available as JSON files tooyour SIEM system.</span></span> <span data-ttu-id="3b8f4-113">Vous pouvez ensuite configurer vos fichiers JSON de SIEM système tooprocess hello.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-113">You can then configure your SIEM system tooprocess hello JSON files.</span></span>

>[!NOTE]
><span data-ttu-id="3b8f4-114">La plupart des étapes hello dans ce didacticiel implique la configuration de coffres de clé, les comptes de stockage et les concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-114">Most of hello steps in this tutorial involve configuring key vaults, storage accounts, and event hubs.</span></span> <span data-ttu-id="3b8f4-115">les étapes d’intégration de journal Azure Hello spécifiques sont à fin hello de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-115">hello specific Azure Log Integration steps are at hello end of this tutorial.</span></span> <span data-ttu-id="3b8f4-116">N’effectuez pas ces étapes dans un environnement de production,</span><span class="sxs-lookup"><span data-stu-id="3b8f4-116">Do not perform these steps in a production environment.</span></span> <span data-ttu-id="3b8f4-117">car elles sont uniquement destinées à un environnement lab.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-117">They are intended for a lab environment only.</span></span> <span data-ttu-id="3b8f4-118">Vous devez personnaliser les étapes hello avant de les utiliser en production.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-118">You must customize hello steps before using them in production.</span></span>

<span data-ttu-id="3b8f4-119">Les informations fournies le long de permet de façon hello que comprendre les raisons hello derrière chaque étape.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-119">Information provided along hello way helps you understand hello reasons behind each step.</span></span> <span data-ttu-id="3b8f4-120">Articles tooother de liens pour obtenir plus de détails sur certaines rubriques.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-120">Links tooother articles give you more detail on certain topics.</span></span>

<span data-ttu-id="3b8f4-121">Pour plus d’informations sur les services hello qui mentionne de ce didacticiel, consultez :</span><span class="sxs-lookup"><span data-stu-id="3b8f4-121">For more information about hello services that this tutorial mentions, see:</span></span> 

- [<span data-ttu-id="3b8f4-122">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="3b8f4-122">Azure Key Vault</span></span>](../key-vault/key-vault-whatis.md)
- [<span data-ttu-id="3b8f4-123">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="3b8f4-123">Azure Event Hubs</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="3b8f4-124">Intégration des journaux Azure</span><span class="sxs-lookup"><span data-stu-id="3b8f4-124">Azure Log Integration</span></span>](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a><span data-ttu-id="3b8f4-125">Configuration initiale</span><span class="sxs-lookup"><span data-stu-id="3b8f4-125">Initial setup</span></span>

<span data-ttu-id="3b8f4-126">Avant que vous pouvez effectuer les étapes de hello dans cet article, vous devez suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="3b8f4-126">Before you can complete hello steps in this article, you need hello following:</span></span>

1. <span data-ttu-id="3b8f4-127">Un abonnement Azure et un compte dans cet abonnement avec des droits d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-127">An Azure subscription and account on that subscription with administrator rights.</span></span> <span data-ttu-id="3b8f4-128">Si vous ne disposez d’aucun abonnement, vous pouvez créer [un compte gratuitement](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="3b8f4-128">If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/).</span></span>
 
2. <span data-ttu-id="3b8f4-129">Un système avec accès toohello internet qui répond aux exigences de hello pour l’installation d’intégration du journal Azure.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-129">A system with access toohello internet that meets hello requirements for installing Azure Log Integration.</span></span> <span data-ttu-id="3b8f4-130">système de Hello peut se trouver sur un service cloud ou hébergé localement.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-130">hello system can be on a cloud service or hosted on-premises.</span></span>

3. <span data-ttu-id="3b8f4-131">Solution d’[intégration des journaux Azure](https://www.microsoft.com/download/details.aspx?id=53324) installée.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-131">[Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) installed.</span></span> <span data-ttu-id="3b8f4-132">tooinstall il :</span><span class="sxs-lookup"><span data-stu-id="3b8f4-132">tooinstall it:</span></span>

   <span data-ttu-id="3b8f4-133">a.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-133">a.</span></span> <span data-ttu-id="3b8f4-134">Utilisez Bureau à distance tooconnect toohello système mentionné à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-134">Use Remote Desktop tooconnect toohello system mentioned in step 2.</span></span>   
   <span data-ttu-id="3b8f4-135">b.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-135">b.</span></span> <span data-ttu-id="3b8f4-136">Copiez hello Azure journal d’installation toohello système d’intégration.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-136">Copy hello Azure Log Integration installer toohello system.</span></span> <span data-ttu-id="3b8f4-137">Vous pouvez [télécharger les fichiers d’installation hello](https://www.microsoft.com/download/details.aspx?id=53324).</span><span class="sxs-lookup"><span data-stu-id="3b8f4-137">You can [download hello installation files](https://www.microsoft.com/download/details.aspx?id=53324).</span></span>   
   <span data-ttu-id="3b8f4-138">c.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-138">c.</span></span> <span data-ttu-id="3b8f4-139">Démarrer le programme d’installation hello et accepter le contrat de licence logiciel Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-139">Start hello installer and accept hello Microsoft Software License Terms.</span></span>   
   <span data-ttu-id="3b8f4-140">d.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-140">d.</span></span> <span data-ttu-id="3b8f4-141">Si vous fournit des informations de télémétrie, laissez hello case est cochée.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-141">If you will provide telemetry information, leave hello check box selected.</span></span> <span data-ttu-id="3b8f4-142">Si vous préfère pas envoyer tooMicrosoft des informations d’utilisation, désactivez la case à cocher hello.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-142">If you'd rather not send usage information tooMicrosoft, clear hello check box.</span></span>
   
   <span data-ttu-id="3b8f4-143">Pour plus d’informations sur l’intégration des journaux Azure et comment tooinstall, consultez [intégration du journal Azure avec la journalisation des Diagnostics Windows Azure et le transfert d’événements Windows](security-azure-log-integration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3b8f4-143">For more information about Azure Log Integration and how tooinstall it, see [Azure Log Integration with Azure Diagnostics logging and Windows Event Forwarding](security-azure-log-integration-get-started.md).</span></span>

4. <span data-ttu-id="3b8f4-144">dernière version du PowerShell Hello.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-144">hello latest PowerShell version.</span></span>
 
   <span data-ttu-id="3b8f4-145">Si vous avez installé Windows Server 2016, vous disposez au moins de PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-145">If you have Windows Server 2016 installed, then you have at least PowerShell 5.0.</span></span> <span data-ttu-id="3b8f4-146">Si vous utilisez une autre version de Windows Server, il est possible que vous possédiez une version antérieure de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-146">If you're using any other version of Windows Server, you might have an earlier version of PowerShell installed.</span></span> <span data-ttu-id="3b8f4-147">Vous pouvez vérifier la version de hello en entrant ```get-host``` dans une fenêtre PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-147">You can check hello version by entering ```get-host``` in a PowerShell window.</span></span> <span data-ttu-id="3b8f4-148">Si vous n’avez pas installé PowerShell 5.0, vous pouvez [le télécharger](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="3b8f4-148">If you don't have PowerShell 5.0 installed, you can [download it](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>

   <span data-ttu-id="3b8f4-149">Une fois que vous avez au moins PowerShell 5.0, vous pouvez passer la version la plus récente tooinstall hello :</span><span class="sxs-lookup"><span data-stu-id="3b8f4-149">After you have at least PowerShell 5.0, you can proceed tooinstall hello latest version:</span></span>
   
   <span data-ttu-id="3b8f4-150">a.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-150">a.</span></span> <span data-ttu-id="3b8f4-151">Dans une fenêtre PowerShell, entrez hello ```Install-Module Azure``` commande.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-151">In a PowerShell window, enter hello ```Install-Module Azure``` command.</span></span> <span data-ttu-id="3b8f4-152">Effectuez les étapes d’installation hello.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-152">Complete hello installation steps.</span></span>    
   <span data-ttu-id="3b8f4-153">b.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-153">b.</span></span> <span data-ttu-id="3b8f4-154">Entrez hello ```Install-Module AzureRM``` commande.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-154">Enter hello ```Install-Module AzureRM``` command.</span></span> <span data-ttu-id="3b8f4-155">Effectuez les étapes d’installation hello.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-155">Complete hello installation steps.</span></span>

   <span data-ttu-id="3b8f4-156">Pour plus d’informations, consultez l’article [Installation et configuration d’Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="3b8f4-156">For more information, see [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span>


## <a name="create-supporting-infrastructure-elements"></a><span data-ttu-id="3b8f4-157">Créer les éléments d’infrastructure sous-jacents</span><span class="sxs-lookup"><span data-stu-id="3b8f4-157">Create supporting infrastructure elements</span></span>

1. <span data-ttu-id="3b8f4-158">Ouvrez une fenêtre PowerShell avec élévation de privilèges et accédez trop**C:\Program Files\Microsoft Azure journal intégration**.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-158">Open an elevated PowerShell window and go too**C:\Program Files\Microsoft Azure Log Integration**.</span></span>
2. <span data-ttu-id="3b8f4-159">Importer les applets de commande hello AzLog en exécutant le script hello LoadAzLogModule.ps1.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-159">Import hello AzLog cmdlets by running hello script LoadAzLogModule.ps1.</span></span> <span data-ttu-id="3b8f4-160">Entrez hello `.\LoadAzLogModule.ps1` commande.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-160">Enter hello `.\LoadAzLogModule.ps1` command.</span></span> <span data-ttu-id="3b8f4-161">(Hello d’avis ». \ » dans cette commande.) Le résultat suivant devrait s'afficher :</span><span class="sxs-lookup"><span data-stu-id="3b8f4-161">(Notice hello “.\” in that command.) You should see something like this:</span></span></br>

   ![Liste des modules chargés](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. <span data-ttu-id="3b8f4-163">Entrez hello `Login-AzureRmAccount` commande.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-163">Enter hello `Login-AzureRmAccount` command.</span></span> <span data-ttu-id="3b8f4-164">Dans la fenêtre de connexion hello, entrez les informations d’identification de hello pour l’abonnement hello que vous allez utiliser pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-164">In hello login window, enter hello credential information for hello subscription that you will use for this tutorial.</span></span>

   >[!NOTE]
   ><span data-ttu-id="3b8f4-165">S’il s’agit hello première fois que vous êtes connecté dans tooAzure à partir de cet ordinateur, vous verrez un message pour autoriser les données d’utilisation de Microsoft toocollect PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-165">If this is hello first time that you're logging in tooAzure from this machine, you will see a message about allowing Microsoft toocollect PowerShell usage data.</span></span> <span data-ttu-id="3b8f4-166">Nous vous recommandons d’activer cette collecte de données, car elle sera utilisée tooimprove Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-166">We recommend that you enable this data collection because it will be used tooimprove Azure PowerShell.</span></span>

4. <span data-ttu-id="3b8f4-167">Après une authentification réussie, vous êtes connecté et informations hello hello suivant capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-167">After successful authentication, you're logged in and you see hello information in hello following screenshot.</span></span> <span data-ttu-id="3b8f4-168">Prenez note du nom d’abonnement hello ID et l’abonnement, car vous en aurez besoin toocomplete étapes plus tard.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-168">Take note of hello subscription ID and subscription name, because you'll need them toocomplete later steps.</span></span>

   ![Fenêtre PowerShell](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. <span data-ttu-id="3b8f4-170">Créer des variables toostore les valeurs qui seront utilisés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-170">Create variables toostore values that will be used later.</span></span> <span data-ttu-id="3b8f4-171">Entrez chaque hello PowerShell lignes suivantes.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-171">Enter each of hello following PowerShell lines.</span></span> <span data-ttu-id="3b8f4-172">Vous devrez peut-être tooadjust hello valeurs toomatch votre environnement.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-172">You might need tooadjust hello values toomatch your environment.</span></span>
    - <span data-ttu-id="3b8f4-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (Votre nom d’abonnement peut être différent.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (Your subscription name might be different.</span></span> <span data-ttu-id="3b8f4-174">Vous pouvez voir dans le cadre de la sortie de hello de la commande précédente hello.)</span><span class="sxs-lookup"><span data-stu-id="3b8f4-174">You can see it as part of hello output of hello previous command.)</span></span>
    - <span data-ttu-id="3b8f4-175">```$location = 'West US'```(Cette variable sera utilisé toopass emplacement de hello où les ressources doivent être créés.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-175">```$location = 'West US'``` (This variable will be used toopass hello location where resources should be created.</span></span> <span data-ttu-id="3b8f4-176">Vous pouvez modifier cette variable toobe n’importe quel emplacement de votre choix.)</span><span class="sxs-lookup"><span data-stu-id="3b8f4-176">You can change this variable toobe any location of your choosing.)</span></span>
    - ```$random = Get-Random```
    - <span data-ttu-id="3b8f4-177">``` $name = 'azlogtest' + $random```(nom de hello quoi que ce soit possible, mais il doit inclure uniquement des lettres minuscules et chiffres.)</span><span class="sxs-lookup"><span data-stu-id="3b8f4-177">``` $name = 'azlogtest' + $random``` (hello name can be anything, but it should include only lowercase letters and numbers.)</span></span>
    - <span data-ttu-id="3b8f4-178">``` $storageName = $name```(Cette variable servira pour le nom de compte de stockage hello.)</span><span class="sxs-lookup"><span data-stu-id="3b8f4-178">``` $storageName = $name``` (This variable will be used for hello storage account name.)</span></span>
    - <span data-ttu-id="3b8f4-179">```$rgname = $name ```(Cette variable servira pour le nom de groupe de ressources hello.)</span><span class="sxs-lookup"><span data-stu-id="3b8f4-179">```$rgname = $name ``` (This variable will be used for hello resource group name.)</span></span>
    - <span data-ttu-id="3b8f4-180">``` $eventHubNameSpaceName = $name```(Cela est nom hello d’espace de noms hello événement hub.)</span><span class="sxs-lookup"><span data-stu-id="3b8f4-180">``` $eventHubNameSpaceName = $name``` (This is hello name of hello event hub namespace.)</span></span>
6. <span data-ttu-id="3b8f4-181">Spécifier l’abonnement de hello vous travaillerez avec :</span><span class="sxs-lookup"><span data-stu-id="3b8f4-181">Specify hello subscription that you will be working with:</span></span>
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. <span data-ttu-id="3b8f4-182">Créez un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="3b8f4-182">Create a resource group:</span></span>
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   <span data-ttu-id="3b8f4-183">Si vous entrez `$rg` à ce stade, vous devez voir la capture d’écran toothis similaire de sortie :</span><span class="sxs-lookup"><span data-stu-id="3b8f4-183">If you enter `$rg` at this point, you should see output similar toothis screenshot:</span></span>

   ![Sortie après la création d’un groupe de ressources](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. <span data-ttu-id="3b8f4-185">Créer un compte de stockage qui sera suivi tookeep utilisé des informations d’état :</span><span class="sxs-lookup"><span data-stu-id="3b8f4-185">Create a storage account that will be used tookeep track of state information:</span></span>
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. <span data-ttu-id="3b8f4-186">Créer un espace de noms hello événement hub.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-186">Create hello event hub namespace.</span></span> <span data-ttu-id="3b8f4-187">Il s’agit d’un concentrateur d’événements de toocreate requis.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-187">This is required toocreate an event hub.</span></span>
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. <span data-ttu-id="3b8f4-188">Obtenir l’ID de règle hello qui est utilisée avec le fournisseur d’insights hello :</span><span class="sxs-lookup"><span data-stu-id="3b8f4-188">Get hello rule ID that will be used with hello insights provider:</span></span>
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. <span data-ttu-id="3b8f4-189">Obtenir tous les emplacements Azure possibles et ajoutez hello noms tooa variable qui peut être utilisé dans une étape ultérieure :</span><span class="sxs-lookup"><span data-stu-id="3b8f4-189">Get all possible Azure locations and add hello names tooa variable that can be used in a later step:</span></span>
    
    <span data-ttu-id="3b8f4-190">a.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-190">a.</span></span> ```$locationObjects = Get-AzureRMLocation```    
    <span data-ttu-id="3b8f4-191">b.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-191">b.</span></span> ```$locations = @('global') + $locationobjects.location```
    
    <span data-ttu-id="3b8f4-192">Si vous entrez `$locations` à ce stade, vous voyez des noms d’emplacement hello sans information supplémentaire de hello retournée par Get-AzureRmLocation.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-192">If you enter `$locations` at this point, you see hello location names without hello additional information returned by Get-AzureRmLocation.</span></span>
12. <span data-ttu-id="3b8f4-193">Créez un profil de journal Azure Resource Manager :</span><span class="sxs-lookup"><span data-stu-id="3b8f4-193">Create an Azure Resource Manager log profile:</span></span> 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    <span data-ttu-id="3b8f4-194">Pour plus d’informations sur hello profil journal Azure, consultez [vue d’ensemble du journal des activités Azure de hello](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="3b8f4-194">For more information about hello Azure log profile, see [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3b8f4-195">Vous pouvez obtenir un message d’erreur lorsque vous essayez de toocreate un profil de journal.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-195">You might get an error message when you try toocreate a log profile.</span></span> <span data-ttu-id="3b8f4-196">Vous pouvez ensuite vérifier documentation hello pour Get-AzureRmLogProfile et Remove-AzureRmLogProfile.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-196">You can then review hello documentation for Get-AzureRmLogProfile and Remove-AzureRmLogProfile.</span></span> <span data-ttu-id="3b8f4-197">Si vous exécutez Get-AzureRmLogProfile, vous consultez des informations sur le profil du journal hello.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-197">If you run Get-AzureRmLogProfile, you see information about hello log profile.</span></span> <span data-ttu-id="3b8f4-198">Vous pouvez supprimer le profil du journal existant hello en entrant hello ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` commande.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-198">You can delete hello existing log profile by entering hello ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` command.</span></span>
>
>![Erreur de profil Resource Manager](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a><span data-ttu-id="3b8f4-200">Création d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="3b8f4-200">Create a key vault</span></span>

1. <span data-ttu-id="3b8f4-201">Créez un coffre de clés hello :</span><span class="sxs-lookup"><span data-stu-id="3b8f4-201">Create hello key vault:</span></span>

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. <span data-ttu-id="3b8f4-202">Configurer la journalisation pour le coffre de clés hello :</span><span class="sxs-lookup"><span data-stu-id="3b8f4-202">Configure logging for hello key vault:</span></span>

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a><span data-ttu-id="3b8f4-203">Générer l’activité de journalisation</span><span class="sxs-lookup"><span data-stu-id="3b8f4-203">Generate log activity</span></span>

<span data-ttu-id="3b8f4-204">Demandes doivent toobe envoyé tooKey coffre toogenerate journalisation de l’activité.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-204">Requests need toobe sent tooKey Vault toogenerate log activity.</span></span> <span data-ttu-id="3b8f4-205">Des actions telles que la génération de clés, le stockage de secrets ou la lecture de secrets à partir de Key Vault entraînent la création d’entrées de journal.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-205">Actions like key generation, storing secrets, or reading secrets from Key Vault will create log entries.</span></span>

1. <span data-ttu-id="3b8f4-206">Afficher les clés de stockage actuel hello :</span><span class="sxs-lookup"><span data-stu-id="3b8f4-206">Display hello current storage keys:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. <span data-ttu-id="3b8f4-207">Générez une nouvelle valeur **key2** :</span><span class="sxs-lookup"><span data-stu-id="3b8f4-207">Generate a new **key2**:</span></span>
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. <span data-ttu-id="3b8f4-208">Afficher les clés hello et vous constatez que **key2** contient une valeur différente :</span><span class="sxs-lookup"><span data-stu-id="3b8f4-208">Display hello keys again and see that **key2** holds a different value:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. <span data-ttu-id="3b8f4-209">Définir et lire des entrées de journal supplémentaires d’un secret toogenerate :</span><span class="sxs-lookup"><span data-stu-id="3b8f4-209">Set and read a secret toogenerate additional log entries:</span></span>
    
   <span data-ttu-id="3b8f4-210">a.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-210">a.</span></span> <span data-ttu-id="3b8f4-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span></span> ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![Secret renvoyé](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a><span data-ttu-id="3b8f4-213">Configurer l’intégration des journaux Azure</span><span class="sxs-lookup"><span data-stu-id="3b8f4-213">Configure Azure Log Integration</span></span>

<span data-ttu-id="3b8f4-214">Maintenant que vous avez configuré le concentrateur d’événements hello éléments requis toohave journalisation du coffre de clés tooan tous les, vous devez tooconfigure intégration des journaux Azure :</span><span class="sxs-lookup"><span data-stu-id="3b8f4-214">Now that you have configured all hello required elements toohave Key Vault logging tooan event hub, you need tooconfigure Azure Log Integration:</span></span>

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

<span data-ttu-id="3b8f4-215">Exécutez la commande de AzLog hello pour chaque concentrateur d’événements :</span><span class="sxs-lookup"><span data-stu-id="3b8f4-215">Run hello AzLog command for each event hub:</span></span>

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

<span data-ttu-id="3b8f4-216">Après une minute de l’exécution des deux dernières commandes hello, vous devez voir les fichiers au format JSON en cours de génération.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-216">After a minute or so of running hello last two commands, you should see JSON files being generated.</span></span> <span data-ttu-id="3b8f4-217">Vous pouvez confirmer que par l’analyse du répertoire de hello **C:\users\AzLog\EventHubJson**.</span><span class="sxs-lookup"><span data-stu-id="3b8f4-217">You can confirm that by monitoring hello directory **C:\users\AzLog\EventHubJson**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b8f4-218">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3b8f4-218">Next steps</span></span>

- [<span data-ttu-id="3b8f4-219">Forum aux questions sur l’intégration des journaux Azure</span><span class="sxs-lookup"><span data-stu-id="3b8f4-219">Azure Log Integration FAQ</span></span>](security-azure-log-integration-faq.md)
- [<span data-ttu-id="3b8f4-220">Bien démarrer avec l’intégration des journaux Azure</span><span class="sxs-lookup"><span data-stu-id="3b8f4-220">Get started with Azure Log Integration</span></span>](security-azure-log-integration-get-started.md)
- [<span data-ttu-id="3b8f4-221">Intégrer des journaux à partir de ressources Azure dans vos systèmes SIEM</span><span class="sxs-lookup"><span data-stu-id="3b8f4-221">Integrate logs from Azure resources into your SIEM systems</span></span>](security-azure-log-integration-overview.md)
