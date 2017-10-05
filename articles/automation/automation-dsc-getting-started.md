---
title: "Prise en main d’Azure Automation DSC | Microsoft Docs"
description: "Explication et exemples de tâches les plus courantes dans Azure Automation Desired State Configuration (DSC)"
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: a3816593-70a3-403b-9a43-d5555fd2cee2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/21/2016
ms.author: magoedte;eslesar
ms.openlocfilehash: 8a10d961ad7c107c68b57c64ee6c88544ff8832b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a><span data-ttu-id="b5c8f-103">Prise en main d’Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="b5c8f-103">Getting started with Azure Automation DSC</span></span>
<span data-ttu-id="b5c8f-104">Cette rubrique explique comment effectuer les tâches les plus courantes avec Azure Automation Desired State Configuration (DSC), comme la création, l’importation et la compilation de configurations, l’intégration des ordinateurs à gérer et l’affichage des rapports.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-104">This topic explains how to do the most common tasks with Azure Automation Desired State Configuration (DSC), such as creating, importing, and compiling configurations, onboarding machines to manage, and viewing reports.</span></span> <span data-ttu-id="b5c8f-105">Pour une vue d’ensemble d’Azure Automation DSC, consultez [Vue d’ensemble d’Azure Automation DSC](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b5c8f-105">For an overview of what Azure Automation DSC is, see [Azure Automation DSC Overview](automation-dsc-overview.md).</span></span> <span data-ttu-id="b5c8f-106">Pour la documentation DSC, consultez l’article [Vue d’ensemble de la fonctionnalité Desired State Configuration de Windows PowerShell](https://msdn.microsoft.com/PowerShell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="b5c8f-106">For DSC documentation, see [Windows PowerShell Desired State Configuration Overview](https://msdn.microsoft.com/PowerShell/dsc/overview).</span></span>

<span data-ttu-id="b5c8f-107">Cette rubrique fournit des instructions détaillées sur l’utilisation d’Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-107">This topic provides a step-by-step guide to using Azure Automation DSC.</span></span> <span data-ttu-id="b5c8f-108">Si vous souhaitez obtenir un exemple d’environnement préconfiguré sans avoir à suivre les étapes décrites dans cette rubrique, vous pouvez utiliser [le modèle ARM suivant](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span><span class="sxs-lookup"><span data-stu-id="b5c8f-108">If you want a sample environment that is already set up without following the steps described in this topic, you can use [the following ARM template](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span></span> <span data-ttu-id="b5c8f-109">Ce modèle configure un environnement Azure Automation DSC complet, comprenant une machine virtuelle Azure gérée par Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-109">This template sets up a completed Azure Automation DSC environment, including an Azure VM that is managed by Azure Automation DSC.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5c8f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b5c8f-110">Prerequisites</span></span>
<span data-ttu-id="b5c8f-111">Pour exécuter les exemples de cette rubrique, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b5c8f-111">To complete the examples in this topic, the following are required:</span></span>

* <span data-ttu-id="b5c8f-112">Un compte Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-112">An Azure Automation account.</span></span> <span data-ttu-id="b5c8f-113">Pour obtenir des instructions sur la création d’un compte d’identification Azure Automation, consultez [Authentifier des Runbooks avec un compte d’identification Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="b5c8f-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>
* <span data-ttu-id="b5c8f-114">Une machine virtuelle Azure Resource Manager (non classique) exécutant Windows Server 2008 R2 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-114">An Azure Resource Manager VM (not Classic) running Windows Server 2008 R2 or later.</span></span> <span data-ttu-id="b5c8f-115">Pour obtenir des instructions sur la création d’une machine virtuelle, consultez [Créer votre première machine virtuelle Windows dans le portail Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="b5c8f-115">For instructions on creating a VM, see [Create your first Windows virtual machine in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span></span>

## <a name="creating-a-dsc-configuration"></a><span data-ttu-id="b5c8f-116">Création d’une configuration DSC</span><span class="sxs-lookup"><span data-stu-id="b5c8f-116">Creating a DSC configuration</span></span>
<span data-ttu-id="b5c8f-117">Nous allons créer une simple [configuration DSC](https://msdn.microsoft.com/powershell/dsc/configurations) qui garantit la présence ou l’absence de la fonctionnalité Windows **Serveur web** , selon le mode d’attribution des nœuds.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-117">We will create a simple [DSC configuration](https://msdn.microsoft.com/powershell/dsc/configurations) that ensures either the presence or absence of the **Web-Server** Windows Feature (IIS), depending on how you assign nodes.</span></span>

1. <span data-ttu-id="b5c8f-118">Démarrez Windows PowerShell ISE (ou n’importe quel éditeur de texte).</span><span class="sxs-lookup"><span data-stu-id="b5c8f-118">Start the Windows PowerShell ISE (or any text editor).</span></span>
2. <span data-ttu-id="b5c8f-119">Saisissez le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="b5c8f-119">Type the following text:</span></span>
   
    ```powershell
    configuration TestConfig
    {
        Node WebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Present'
                Name                 = 'Web-Server'
                IncludeAllSubFeature = $true
   
            }
        }
   
        Node NotWebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Absent'
                Name                 = 'Web-Server'
   
            }
        }
        }
    ```
3. <span data-ttu-id="b5c8f-120">Enregistrez le fichier sous le nom `TestConfig.ps1`.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-120">Save the file as `TestConfig.ps1`.</span></span>

<span data-ttu-id="b5c8f-121">Cette configuration appelle une ressource dans chaque bloc de nœuds, la [ressource WindowsFeature](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), qui garantit la présence ou l’absence de la fonctionnalité **Serveur web** .</span><span class="sxs-lookup"><span data-stu-id="b5c8f-121">This configuration calls one resource in each node block, the [WindowsFeature resource](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), that ensures either the presence or absence of the **Web-Server** feature.</span></span>

## <a name="importing-a-configuration-into-azure-automation"></a><span data-ttu-id="b5c8f-122">Importation d’une configuration dans Azure Automation</span><span class="sxs-lookup"><span data-stu-id="b5c8f-122">Importing a configuration into Azure Automation</span></span>
<span data-ttu-id="b5c8f-123">Nous allons ensuite importer la configuration dans le compte Automation.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-123">Next, we'll import the configuration into the Automation account.</span></span>

1. <span data-ttu-id="b5c8f-124">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b5c8f-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b5c8f-125">Dans le menu Hub, cliquez sur **Toutes les ressources** , puis sur le nom de votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-125">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="b5c8f-126">Dans le panneau **Compte Automation**, cliquez sur **Configurations DSC**.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-126">On the **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="b5c8f-127">Dans le panneau **Configurations DSC**, cliquez sur **Ajouter une configuration**.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-127">On the **DSC Configurations** blade, click **Add a configuration**.</span></span>
5. <span data-ttu-id="b5c8f-128">Dans le panneau **Importer la configuration**, recherchez le fichier `TestConfig.ps1` sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-128">On the **Import Configuration** blade, browse to the `TestConfig.ps1` file on your computer.</span></span>
   
    ![Capture d’écran du panneau **Importer la configuration**](./media/automation-dsc-getting-started/AddConfig.png)
6. <span data-ttu-id="b5c8f-130">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-130">Click **OK**.</span></span>

## <a name="viewing-a-configuration-in-azure-automation"></a><span data-ttu-id="b5c8f-131">Affichage d’une configuration dans Azure Automation</span><span class="sxs-lookup"><span data-stu-id="b5c8f-131">Viewing a configuration in Azure Automation</span></span>
<span data-ttu-id="b5c8f-132">Après avoir importé une configuration, vous pouvez l’afficher dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-132">After you have imported a configuration, you can view it in the Azure portal.</span></span>

1. <span data-ttu-id="b5c8f-133">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b5c8f-133">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b5c8f-134">Dans le menu Hub, cliquez sur **Toutes les ressources** , puis sur le nom de votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-134">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="b5c8f-135">Dans le panneau **Compte Automation**, cliquez sur **Configurations DSC**.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-135">On the **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="b5c8f-136">Dans le panneau **Configurations DSC**, cliquez sur **TestConfig** (il s’agit du nom de la configuration que vous avez importée dans la procédure précédente).</span><span class="sxs-lookup"><span data-stu-id="b5c8f-136">On the **DSC Configurations** blade, click **TestConfig** (this is the name of the configuration you imported in the previous procedure).</span></span>
5. <span data-ttu-id="b5c8f-137">Dans le panneau **Configuration de TestConfig**, cliquez sur **Afficher la source de configuration**.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-137">On the **TestConfig Configuration** blade, click **View configuration source**.</span></span>
   
    ![Capture d’écran du panneau Configuration de TestConfig](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    <span data-ttu-id="b5c8f-139">Dans le panneau **Source de configuration de TestConfig** qui s’affiche, vous accédez au code PowerShell de configuration.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-139">A **TestConfig Configuration source** blade opens, displaying the PowerShell code for the configuration.</span></span>

## <a name="compiling-a-configuration-in-azure-automation"></a><span data-ttu-id="b5c8f-140">Compilation d’une configuration dans Azure Automation</span><span class="sxs-lookup"><span data-stu-id="b5c8f-140">Compiling a configuration in Azure Automation</span></span>
<span data-ttu-id="b5c8f-141">Avant de pouvoir appliquer un état souhaité à un nœud, vous devez compiler une configuration DSC définissant cet état dans une ou plusieurs configurations de nœuds (documents MOF) et la placer sur le serveur Pull Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-141">Before you can apply a desired state to a node, a DSC configuration defining that state must be compiled into one or more node configurations (MOF document), and placed on the Automation DSC Pull Server.</span></span> <span data-ttu-id="b5c8f-142">Pour obtenir une description plus détaillée de la compilation des configurations dans Azure Automation DSC, consultez [Compilation de configurations dans Azure Automation DSC](automation-dsc-compile.md).</span><span class="sxs-lookup"><span data-stu-id="b5c8f-142">For a more detailed description of compiling configurations in Azure Automation DSC, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md).</span></span> <span data-ttu-id="b5c8f-143">Pour plus d’informations sur la compilation des configurations, consultez [Configurations DSC](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span><span class="sxs-lookup"><span data-stu-id="b5c8f-143">For more information about compiling configurations, see [DSC Configurations](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span></span>

1. <span data-ttu-id="b5c8f-144">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b5c8f-144">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b5c8f-145">Dans le menu Hub, cliquez sur **Toutes les ressources** , puis sur le nom de votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-145">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="b5c8f-146">Dans le panneau **Compte Automation**, cliquez sur **Configurations DSC**.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-146">On the **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="b5c8f-147">Dans le panneau **Configurations DSC**, cliquez sur **TestConfig** (le nom de la configuration que vous avez précédemment importée).</span><span class="sxs-lookup"><span data-stu-id="b5c8f-147">On the **DSC Configurations** blade, click **TestConfig** (the name of the previously imported configuration).</span></span>
5. <span data-ttu-id="b5c8f-148">Dans le panneau **Configuration de TestConfig**, cliquez sur **Compiler**, puis sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-148">On the **TestConfig Configuration** blade, click **Compile**, and then click **Yes**.</span></span> <span data-ttu-id="b5c8f-149">Une tâche de compilation démarre.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-149">This starts a compilation job.</span></span>
   
    ![Capture d’écran du panneau Configuration de TestConfig mettant en évidence le bouton de compilation](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> <span data-ttu-id="b5c8f-151">Lorsque vous compilez une configuration dans Azure Automation, tous les fichiers MOF de configuration de nœuds créés sont automatiquement déployés sur le serveur Pull.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-151">When you compile a configuration in Azure Automation, it automatically deploys any created node configuration MOFs to the pull server.</span></span>
> 
> 

## <a name="viewing-a-compilation-job"></a><span data-ttu-id="b5c8f-152">Affichage d’une tâche de compilation</span><span class="sxs-lookup"><span data-stu-id="b5c8f-152">Viewing a compilation job</span></span>
<span data-ttu-id="b5c8f-153">Après avoir démarré une compilation, vous pouvez l’afficher sur la vignette **Travaux de compilation** du panneau **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-153">After you start a compilation, you can view it in the **Compilation jobs** tile in the **Configuration** blade.</span></span> <span data-ttu-id="b5c8f-154">La mosaïque **Tâches de compilation** affiche les tâches en cours d’exécution, terminées et en échec.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-154">The **Compilation jobs** tile shows currently running, completed, and failed jobs.</span></span> <span data-ttu-id="b5c8f-155">Lorsque vous ouvrez un volet de tâche de compilation, vous obtenez des informations sur cette tâche, notamment les erreurs ou les avertissements rencontrés, les paramètres d’entrée utilisés dans la configuration et les journaux de compilation.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-155">When you open a compilation job blade, it shows information about that job including any errors or warnings encountered, input parameters used in the configuration, and compilation logs.</span></span>

1. <span data-ttu-id="b5c8f-156">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b5c8f-156">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b5c8f-157">Dans le menu Hub, cliquez sur **Toutes les ressources** , puis sur le nom de votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-157">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="b5c8f-158">Dans le panneau **Compte Automation**, cliquez sur **Configurations DSC**.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-158">On the **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="b5c8f-159">Dans le panneau **Configurations DSC**, cliquez sur **TestConfig** (le nom de la configuration que vous avez précédemment importée).</span><span class="sxs-lookup"><span data-stu-id="b5c8f-159">On the **DSC Configurations** blade, click **TestConfig** (the name of the previously imported configuration).</span></span>
5. <span data-ttu-id="b5c8f-160">Sur la vignette **Travaux de compilation** du panneau **Configuration de TestConfig**, cliquez sur l’un des travaux répertoriés.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-160">On the **Compilation jobs** tile of the **TestConfig Configuration** blade, click on any of the jobs listed.</span></span> <span data-ttu-id="b5c8f-161">Un panneau **Tâche de compilation** s’ouvre en indiquant la date de démarrage de la tâche de compilation.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-161">A **Compilation Job** blade opens, labeled with the date that the compilation job was started.</span></span>
   
    ![Capture d’écran du panneau Tâche de compilation](./media/automation-dsc-getting-started/CompilationJob.png)
6. <span data-ttu-id="b5c8f-163">Cliquez sur n’importe quelle mosaïque du panneau **Tâche de compilation** pour afficher des détails supplémentaires sur la tâche.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-163">Click on any tile in the **Compilation Job** blade to see further details about the job.</span></span>

## <a name="viewing-node-configurations"></a><span data-ttu-id="b5c8f-164">Affichage des configurations de nœuds</span><span class="sxs-lookup"><span data-stu-id="b5c8f-164">Viewing node configurations</span></span>
<span data-ttu-id="b5c8f-165">La réussite d’une tâche de compilation a pour effet de créer une ou plusieurs configurations de nœud.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-165">Successful completion of a compilation job creates one or more new node configurations.</span></span> <span data-ttu-id="b5c8f-166">Une configuration de nœud est un document MOF déployé sur le serveur Pull et prêt à être extrait et appliqué par un ou plusieurs nœuds.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-166">A node configuration is a MOF document that is deployed to the pull server and ready to be pulled and applied by one or more nodes.</span></span> <span data-ttu-id="b5c8f-167">Vous pouvez afficher les configurations de nœud de votre compte Automation dans le panneau **Configurations de nœuds DSC** .</span><span class="sxs-lookup"><span data-stu-id="b5c8f-167">You can view the node configurations in your Automation account in the **DSC Node Configurations** blade.</span></span> <span data-ttu-id="b5c8f-168">Une configuration de nœud possède un nom au format *NomConfiguration*.*NomNœud*.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-168">A node configuration has a name with the form *ConfigurationName*.*NodeName*.</span></span>

1. <span data-ttu-id="b5c8f-169">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b5c8f-169">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b5c8f-170">Dans le menu Hub, cliquez sur **Toutes les ressources** , puis sur le nom de votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-170">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="b5c8f-171">Dans le panneau **Compte Automation**, cliquez sur **Configurations de nœuds DSC**.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-171">On the **Automation account** blade, click **DSC Node Configurations**.</span></span>
   
    ![Capture d’écran du panneau Configurations de nœuds DSC](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a><span data-ttu-id="b5c8f-173">Intégration d’une machine virtuelle Azure pour la gérer avec Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="b5c8f-173">Onboarding an Azure VM for management with Azure Automation DSC</span></span>
<span data-ttu-id="b5c8f-174">Azure Automation DSC vous permet de gérer vos machines virtuelles Azure (via les modèles de déploiement classique et Resource Manager), vos machines virtuelles locales, vos machines virtuelles Linux, vos machines virtuelles AWS et vos ordinateurs physiques en local.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-174">You can use Azure Automation DSC to manage Azure VMs (both Classic and Resource Manager), on-premises VMs, Linux machines, AWS VMs, and on-premises physical machines.</span></span> <span data-ttu-id="b5c8f-175">Dans cette rubrique, nous allons voir comment intégrer uniquement des machines virtuelles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-175">In this topic, we cover how to onboard only Azure Resource Manager VMs.</span></span> <span data-ttu-id="b5c8f-176">Pour plus d’informations sur l’intégration d’autres types d’ordinateur, consultez [Gestion de machines avec Azure Automation DSC](automation-dsc-onboarding.md).</span><span class="sxs-lookup"><span data-stu-id="b5c8f-176">For information about onboarding other types of machines, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md).</span></span>

### <a name="to-onboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a><span data-ttu-id="b5c8f-177">Pour intégrer une machine virtuelle Azure Resource Manager pour la gérer via Azure Automation DSC, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-177">To onboard an Azure Resource Manager VM for management by Azure Automation DSC</span></span>
1. <span data-ttu-id="b5c8f-178">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b5c8f-178">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b5c8f-179">Dans le menu Hub, cliquez sur **Toutes les ressources** , puis sur le nom de votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-179">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="b5c8f-180">Dans le panneau **Compte Automation**, cliquez sur **Nœuds DSC**.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-180">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="b5c8f-181">Dans le panneau **Nœuds DSC**, cliquez sur **Ajouter une machine virtuelle Azure**.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-181">In the **DSC Nodes** blade, click **Add Azure VM**.</span></span>
   
    ![Capture d’écran du panneau Nœuds DSC mettant en évidence le bouton Ajouter des machines virtuelles Azure](./media/automation-dsc-getting-started/OnboardVM.png)
5. <span data-ttu-id="b5c8f-183">Dans le panneau **Ajouter des machines virtuelles Azure**, cliquez sur **Sélectionner les machines virtuelles à intégrer**.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-183">In the **Add Azure VMs** blade, click **Select virtual machines to onboard**.</span></span>
6. <span data-ttu-id="b5c8f-184">Dans le panneau **Sélectionner des machines virtuelles**, sélectionnez la machine virtuelle que vous souhaitez intégrer et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-184">In the **Select VMs** blade, select the VM you want to onboard, and click **OK**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="b5c8f-185">Il doit s’agir d’une machine virtuelle Azure Resource Manager exécutant Windows Server 2008 R2 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-185">This must be an Azure Resource Manager VM running Windows Server 2008 R2 or later.</span></span>
   > 
   > 
7. <span data-ttu-id="b5c8f-186">Dans le panneau **Ajouter des machines virtuelles Azure**, cliquez sur **Configurer les données d’inscription**.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-186">In the **Add Azure VMs** blade, click **Configure registration data**.</span></span>
8. <span data-ttu-id="b5c8f-187">Dans le panneau **Inscription**, entrez le nom de la configuration de nœud que vous souhaitez appliquer à la machine virtuelle dans la zone **Nom de la configuration de nœuds**.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-187">In the **Registration** blade, enter the name of the node configuration you want to apply to the VM in the **Node Configuration Name** box.</span></span> <span data-ttu-id="b5c8f-188">Ce nom doit correspondre exactement au nom d’une configuration de nœud dans le compte Automation.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-188">This must exactly match the name of a node configuration in the Automation account.</span></span> <span data-ttu-id="b5c8f-189">Vous n’êtes pas obligé de fournir un nom à ce stade.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-189">Providing a name at this point is optional.</span></span> <span data-ttu-id="b5c8f-190">Vous pouvez modifier la configuration de nœud assignée une fois l’intégration du nœud effectuée.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-190">You can change the assigned node configuration after onboarding the node.</span></span>
   <span data-ttu-id="b5c8f-191">Cochez la case **Redémarrer le nœud si nécessaire**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-191">Check **Reboot Node if Needed**, and then click **OK**.</span></span>
   
    ![Capture d’écran du panneau Inscription](./media/automation-dsc-getting-started/RegisterVM.png)
   
    <span data-ttu-id="b5c8f-193">La configuration de nœud spécifiée s’appliquera à la machine virtuelle aux intervalles spécifiés par la **Fréquence du mode de configuration**. La machine virtuelle recherchera les mises à jour de la configuration du nœud selon un intervalle spécifié par la **Fréquence d’actualisation**.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-193">The node configuration you specified will be applied to the VM at intervals specified by the **Configuration Mode Frequency**, and the VM will check for updates to the node configuration at intervals specified by the **Refresh Frequency**.</span></span> <span data-ttu-id="b5c8f-194">Pour plus d’informations sur la façon dont ces valeurs sont utilisées, consultez [Configuration du Gestionnaire de configuration local](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span><span class="sxs-lookup"><span data-stu-id="b5c8f-194">For more information about how these values are used, see [Configuring the Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span></span>
9. <span data-ttu-id="b5c8f-195">Dans le panneau **Ajouter des machines virtuelles Azure**, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-195">In the **Add Azure VMs** blade, click **Create**.</span></span>

<span data-ttu-id="b5c8f-196">Azure démarre le processus d’intégration de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-196">Azure will start the process of onboarding the VM.</span></span> <span data-ttu-id="b5c8f-197">Une fois le processus terminé, la machine virtuelle s’affiche dans le panneau **Nœuds DSC** du compte Automation.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-197">When it is complete, the VM will show up in the **DSC Nodes** blade in the Automation account.</span></span>

## <a name="viewing-the-list-of-dsc-nodes"></a><span data-ttu-id="b5c8f-198">Affichage de la liste des nœuds DSC</span><span class="sxs-lookup"><span data-stu-id="b5c8f-198">Viewing the list of DSC nodes</span></span>
<span data-ttu-id="b5c8f-199">Vous pouvez utiliser le panneau **Nœuds DSC** pour afficher la liste de tous les ordinateurs qui ont été intégrés afin d’être gérés dans votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-199">You can view the list of all machines that have been onboarded for management in your Automation account in the **DSC Nodes** blade.</span></span>

1. <span data-ttu-id="b5c8f-200">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b5c8f-200">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b5c8f-201">Dans le menu Hub, cliquez sur **Toutes les ressources** , puis sur le nom de votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-201">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="b5c8f-202">Dans le panneau **Compte Automation**, cliquez sur **Nœuds DSC**.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-202">On the **Automation account** blade, click **DSC Nodes**.</span></span>

## <a name="viewing-reports-for-dsc-nodes"></a><span data-ttu-id="b5c8f-203">Affichage des rapports de nœuds DSC</span><span class="sxs-lookup"><span data-stu-id="b5c8f-203">Viewing reports for DSC nodes</span></span>
<span data-ttu-id="b5c8f-204">Chaque fois qu’azure Automation DSC effectue une vérification de cohérence sur un nœud géré, le nœud envoie un rapport d’état sur le serveur Pull.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-204">Each time Azure Automation DSC performs a consistency check on a managed node, the node sends a status report back to the pull server.</span></span> <span data-ttu-id="b5c8f-205">Vous pouvez consulter ces rapports dans le panneau correspondant à ce nœud.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-205">You can view these reports on the blade for that node.</span></span>

1. <span data-ttu-id="b5c8f-206">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b5c8f-206">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b5c8f-207">Dans le menu Hub, cliquez sur **Toutes les ressources** , puis sur le nom de votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-207">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="b5c8f-208">Dans le panneau **Compte Automation**, cliquez sur **Nœuds DSC**.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-208">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="b5c8f-209">Dans la mosaïque **Rapports** , cliquez sur l’un des rapports de la liste.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-209">On the **Reports** tile, click on any of the reports in the list.</span></span>
   
    ![Capture d’écran du panneau Rapport](./media/automation-dsc-getting-started/NodeReport.png)

<span data-ttu-id="b5c8f-211">Le panneau d’un rapport vous permet d’accéder aux informations d’état suivantes pour vous permettre d’effectuer la vérification de cohérence correspondante :</span><span class="sxs-lookup"><span data-stu-id="b5c8f-211">On the blade for an individual report, you can see the following status information for the corresponding consistency check:</span></span>

* <span data-ttu-id="b5c8f-212">L’état du rapport : si le nœud est « Conforme », si la configuration a « Échoué » ou si le nœud est « Non conforme » (lorsque le nœud est en mode **applyandmonitor** et que l’ordinateur ne se trouve pas à l’état souhaité).</span><span class="sxs-lookup"><span data-stu-id="b5c8f-212">The report status — whether the node is "Compliant", the configuration "Failed", or the node is "Not Compliant" (when the node is in **applyandmonitor** mode and the machine is not in the desired state).</span></span>
* <span data-ttu-id="b5c8f-213">L’heure de début de la vérification de cohérence.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-213">The start time for the consistency check.</span></span>
* <span data-ttu-id="b5c8f-214">Le temps total d’exécution de la vérification de cohérence.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-214">The total runtime for the consistency check.</span></span>
* <span data-ttu-id="b5c8f-215">Le type de vérification de cohérence.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-215">The type of consistency check.</span></span>
* <span data-ttu-id="b5c8f-216">Toute erreur rencontrée, avec code d’erreur et message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-216">Any errors, including the error code and error message.</span></span> 
* <span data-ttu-id="b5c8f-217">Toutes les ressources DSC utilisées dans la configuration, ainsi que l’état de chaque ressource (si le nœud est à l’état souhaité pour cette ressource) : vous pouvez cliquer sur chaque ressource pour obtenir des informations plus détaillées sur cette ressource.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-217">Any DSC resources used in the configuration, and the state of each resource (whether the node is in the desired state for that resource) — you can click on each resource to get more detailed information for that resource.</span></span>
* <span data-ttu-id="b5c8f-218">Le nom, l’adresse IP et le mode de configuration du nœud.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-218">The name, IP address, and configuration mode of the node.</span></span>

<span data-ttu-id="b5c8f-219">Vous pouvez également cliquer sur **Afficher le rapport brut** pour afficher les données que le nœud envoie effectivement au serveur.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-219">You can also click **View raw report** to see the actual data that the node sends to the server.</span></span> <span data-ttu-id="b5c8f-220">Pour plus d’informations sur l’utilisation de ces données, consultez la page [Utilisation d’un serveur de rapports DSC](https://msdn.microsoft.com/powershell/dsc/reportserver).</span><span class="sxs-lookup"><span data-stu-id="b5c8f-220">For more information about using that data, see [Using a DSC report server](https://msdn.microsoft.com/powershell/dsc/reportserver).</span></span>

<span data-ttu-id="b5c8f-221">Vous risquez de devoir attendre un certain temps après l’intégration d’un nœud pour pouvoir accéder au premier rapport.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-221">It can take some time after a node is onboarded before the first report is available.</span></span> <span data-ttu-id="b5c8f-222">Vous devrez peut-être attendre jusqu’à 30 minutes pour obtenir le premier rapport après avoir effectué l’intégration.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-222">You might need to wait up to 30 minutes for the first report after you onboard a node.</span></span>

## <a name="reassigning-a-node-to-a-different-node-configuration"></a><span data-ttu-id="b5c8f-223">Réaffectation d’un nœud à une configuration de nœud différent</span><span class="sxs-lookup"><span data-stu-id="b5c8f-223">Reassigning a node to a different node configuration</span></span>
<span data-ttu-id="b5c8f-224">Vous pouvez attribuer un nœud à une configuration de nœud différente de celle qui lui a été initialement affectée.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-224">You can assign a node to use a different node configuration than the one you initially assigned.</span></span>

1. <span data-ttu-id="b5c8f-225">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b5c8f-225">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b5c8f-226">Dans le menu Hub, cliquez sur **Toutes les ressources** , puis sur le nom de votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-226">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="b5c8f-227">Dans le panneau **Compte Automation**, cliquez sur **Nœuds DSC**.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-227">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="b5c8f-228">Dans le panneau **Nœuds DSC** , cliquez sur le nom du nœud que vous souhaitez réaffecter.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-228">On the **DSC Nodes** blade, click on the name of the node you want to reassign.</span></span>
5. <span data-ttu-id="b5c8f-229">Dans le panneau de ce nœud, cliquez sur **Assign node**(Attribuer le nœud).</span><span class="sxs-lookup"><span data-stu-id="b5c8f-229">On the blade for that node, click **Assign node**.</span></span>
   
    ![Capture d’écran du panneau Nœud mettant en évidence le bouton Attribuer un nœud](./media/automation-dsc-getting-started/AssignNode.png)
6. <span data-ttu-id="b5c8f-231">Dans le panneau **Affecter une configuration de nœuds**, sélectionnez la configuration de nœuds à laquelle vous souhaitez affecter le nœud, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-231">On the **Assign Node Configuration** blade, select the node configuration to which you want to assign the node, and then click **OK**.</span></span>
   
    ![Capture d’écran du panneau Attribuer une configuration de nœuds](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a><span data-ttu-id="b5c8f-233">Annulation de l’inscription d’un nœud</span><span class="sxs-lookup"><span data-stu-id="b5c8f-233">Unregistering a node</span></span>
<span data-ttu-id="b5c8f-234">Si vous ne souhaitez plus qu’un nœud soit géré par Azure Automation DSC, vous pouvez annuler son inscription.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-234">If you no longer want a node to be managed by Azure Automation DSC, you can unregister it.</span></span>

1. <span data-ttu-id="b5c8f-235">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b5c8f-235">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b5c8f-236">Dans le menu Hub, cliquez sur **Toutes les ressources** , puis sur le nom de votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-236">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="b5c8f-237">Dans le panneau **Compte Automation**, cliquez sur **Nœuds DSC**.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-237">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="b5c8f-238">Dans le panneau **Nœuds DSC** , cliquez sur le nom du nœud dont vous souhaitez annuler l’inscription.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-238">On the **DSC Nodes** blade, click on the name of the node you want to unregister.</span></span>
5. <span data-ttu-id="b5c8f-239">Dans le panneau de ce nœud, cliquez sur **Annuler l’inscription**.</span><span class="sxs-lookup"><span data-stu-id="b5c8f-239">On the blade for that node, click **Unregister**.</span></span>
   
    ![Capture d’écran du panneau Nœud mettant en évidence le bouton Annuler l’inscription](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a><span data-ttu-id="b5c8f-241">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="b5c8f-241">Related Articles</span></span>
* [<span data-ttu-id="b5c8f-242">Vue d’ensemble d’Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="b5c8f-242">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="b5c8f-243">Gestion de machines avec Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="b5c8f-243">Onboarding machines for management by Azure Automation DSC</span></span>](automation-dsc-onboarding.md)
* [<span data-ttu-id="b5c8f-244">Vue d’ensemble d’Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="b5c8f-244">Windows PowerShell Desired State Configuration Overview</span></span>](https://msdn.microsoft.com/powershell/dsc/overview)
* [<span data-ttu-id="b5c8f-245">Applets de commande Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="b5c8f-245">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="b5c8f-246">Tarification d’Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="b5c8f-246">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)

