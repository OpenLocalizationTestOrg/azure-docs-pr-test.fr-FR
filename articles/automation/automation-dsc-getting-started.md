---
title: "aaaGetting main d’Azure Automation DSC | Documents Microsoft"
description: "Explication et des exemples de tâches les plus courantes de hello dans Azure Automation état Configuration souhaité (DSC)"
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
ms.openlocfilehash: 82910c96e928b9264c2e1b52a5c98dc47273dcc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a><span data-ttu-id="644c7-103">Prise en main d’Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="644c7-103">Getting started with Azure Automation DSC</span></span>
<span data-ttu-id="644c7-104">Cette rubrique explique comment toodo hello tâches les plus courantes avec Azure Automation état Configuration souhaité (DSC), telles que la création, l’importation et la compilation des configurations, l’intégration trop gérer les ordinateurs et l’affichage de rapports.</span><span class="sxs-lookup"><span data-stu-id="644c7-104">This topic explains how toodo hello most common tasks with Azure Automation Desired State Configuration (DSC), such as creating, importing, and compiling configurations, onboarding machines too manage, and viewing reports.</span></span> <span data-ttu-id="644c7-105">Pour une vue d’ensemble d’Azure Automation DSC, consultez [Vue d’ensemble d’Azure Automation DSC](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="644c7-105">For an overview of what Azure Automation DSC is, see [Azure Automation DSC Overview](automation-dsc-overview.md).</span></span> <span data-ttu-id="644c7-106">Pour la documentation DSC, consultez l’article [Vue d’ensemble de la fonctionnalité Desired State Configuration de Windows PowerShell](https://msdn.microsoft.com/PowerShell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="644c7-106">For DSC documentation, see [Windows PowerShell Desired State Configuration Overview](https://msdn.microsoft.com/PowerShell/dsc/overview).</span></span>

<span data-ttu-id="644c7-107">Cette rubrique fournit un guide pas à pas de toousing Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="644c7-107">This topic provides a step-by-step guide toousing Azure Automation DSC.</span></span> <span data-ttu-id="644c7-108">Si vous souhaitez un exemple d’environnement qui est déjà configuré sans suivant hello les étapes décrites dans cette rubrique, vous pouvez utiliser [hello suivant un modèle ARM](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span><span class="sxs-lookup"><span data-stu-id="644c7-108">If you want a sample environment that is already set up without following hello steps described in this topic, you can use [hello following ARM template](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span></span> <span data-ttu-id="644c7-109">Ce modèle configure un environnement Azure Automation DSC complet, comprenant une machine virtuelle Azure gérée par Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="644c7-109">This template sets up a completed Azure Automation DSC environment, including an Azure VM that is managed by Azure Automation DSC.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="644c7-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="644c7-110">Prerequisites</span></span>
<span data-ttu-id="644c7-111">exemples de hello toocomplete dans cette rubrique, hello Voici requis :</span><span class="sxs-lookup"><span data-stu-id="644c7-111">toocomplete hello examples in this topic, hello following are required:</span></span>

* <span data-ttu-id="644c7-112">Un compte Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="644c7-112">An Azure Automation account.</span></span> <span data-ttu-id="644c7-113">Pour obtenir des instructions sur la création d’un compte d’identification Azure Automation, consultez [Authentifier des Runbooks avec un compte d’identification Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="644c7-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>
* <span data-ttu-id="644c7-114">Une machine virtuelle Azure Resource Manager (non classique) exécutant Windows Server 2008 R2 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="644c7-114">An Azure Resource Manager VM (not Classic) running Windows Server 2008 R2 or later.</span></span> <span data-ttu-id="644c7-115">Pour obtenir des instructions sur la création d’une machine virtuelle, consultez [créer votre première machine virtuelle de Windows Bonjour portail Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="644c7-115">For instructions on creating a VM, see [Create your first Windows virtual machine in hello Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span></span>

## <a name="creating-a-dsc-configuration"></a><span data-ttu-id="644c7-116">Création d’une configuration DSC</span><span class="sxs-lookup"><span data-stu-id="644c7-116">Creating a DSC configuration</span></span>
<span data-ttu-id="644c7-117">Nous allons créer une simple [configuration DSC](https://msdn.microsoft.com/powershell/dsc/configurations) qui garantit la présence de hello ou d’absence de hello **Web-Server** Windows fonctionnalité (IIS), en fonction de l’attribution des nœuds.</span><span class="sxs-lookup"><span data-stu-id="644c7-117">We will create a simple [DSC configuration](https://msdn.microsoft.com/powershell/dsc/configurations) that ensures either hello presence or absence of hello **Web-Server** Windows Feature (IIS), depending on how you assign nodes.</span></span>

1. <span data-ttu-id="644c7-118">Démarrer Windows PowerShell ISE de hello (ou n’importe quel éditeur de texte).</span><span class="sxs-lookup"><span data-stu-id="644c7-118">Start hello Windows PowerShell ISE (or any text editor).</span></span>
2. <span data-ttu-id="644c7-119">Tapez hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="644c7-119">Type hello following text:</span></span>
   
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
3. <span data-ttu-id="644c7-120">Enregistrer le fichier hello sous `TestConfig.ps1`.</span><span class="sxs-lookup"><span data-stu-id="644c7-120">Save hello file as `TestConfig.ps1`.</span></span>

<span data-ttu-id="644c7-121">Cette configuration appelle une ressource dans chaque bloc de nœud, hello [ressource WindowsFeature](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), qui garantit la présence de hello ou d’absence de hello **Web-Server** fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="644c7-121">This configuration calls one resource in each node block, hello [WindowsFeature resource](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), that ensures either hello presence or absence of hello **Web-Server** feature.</span></span>

## <a name="importing-a-configuration-into-azure-automation"></a><span data-ttu-id="644c7-122">Importation d’une configuration dans Azure Automation</span><span class="sxs-lookup"><span data-stu-id="644c7-122">Importing a configuration into Azure Automation</span></span>
<span data-ttu-id="644c7-123">Ensuite, nous allons importer configuration de hello dans hello compte Automation.</span><span class="sxs-lookup"><span data-stu-id="644c7-123">Next, we'll import hello configuration into hello Automation account.</span></span>

1. <span data-ttu-id="644c7-124">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="644c7-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="644c7-125">Dans le menu du Hub hello, cliquez sur **toutes les ressources** , puis hello nom de votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="644c7-125">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="644c7-126">Sur hello **compte Automation** panneau, cliquez sur **les Configurations DSC**.</span><span class="sxs-lookup"><span data-stu-id="644c7-126">On hello **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="644c7-127">Sur hello **les Configurations DSC** panneau, cliquez sur **ajouter une configuration**.</span><span class="sxs-lookup"><span data-stu-id="644c7-127">On hello **DSC Configurations** blade, click **Add a configuration**.</span></span>
5. <span data-ttu-id="644c7-128">Sur hello **importer la Configuration** toohello de parcourir les lames, `TestConfig.ps1` fichier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="644c7-128">On hello **Import Configuration** blade, browse toohello `TestConfig.ps1` file on your computer.</span></span>
   
    ![Capture d’écran de hello ** Panneau de Configuration d’importation **](./media/automation-dsc-getting-started/AddConfig.png)
6. <span data-ttu-id="644c7-130">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="644c7-130">Click **OK**.</span></span>

## <a name="viewing-a-configuration-in-azure-automation"></a><span data-ttu-id="644c7-131">Affichage d’une configuration dans Azure Automation</span><span class="sxs-lookup"><span data-stu-id="644c7-131">Viewing a configuration in Azure Automation</span></span>
<span data-ttu-id="644c7-132">Après avoir importé une configuration, vous pouvez l’afficher dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="644c7-132">After you have imported a configuration, you can view it in hello Azure portal.</span></span>

1. <span data-ttu-id="644c7-133">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="644c7-133">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="644c7-134">Dans le menu du Hub hello, cliquez sur **toutes les ressources** , puis hello nom de votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="644c7-134">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="644c7-135">Sur hello **compte Automation** panneau, cliquez sur **les Configurations DSC**</span><span class="sxs-lookup"><span data-stu-id="644c7-135">On hello **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="644c7-136">Sur hello **les Configurations DSC** panneau, cliquez sur **TestConfig** (il s’agit hello nom de configuration hello vous avez importé dans la procédure précédente de hello).</span><span class="sxs-lookup"><span data-stu-id="644c7-136">On hello **DSC Configurations** blade, click **TestConfig** (this is hello name of hello configuration you imported in hello previous procedure).</span></span>
5. <span data-ttu-id="644c7-137">Sur hello **TestConfig Configuration** panneau, cliquez sur **afficher la source configuration**.</span><span class="sxs-lookup"><span data-stu-id="644c7-137">On hello **TestConfig Configuration** blade, click **View configuration source**.</span></span>
   
    ![Capture d’écran du Panneau de configuration hello TestConfig](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    <span data-ttu-id="644c7-139">A **source de Configuration de TestConfig** s’ouvre le panneau, affichage du code de PowerShell hello pour la configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="644c7-139">A **TestConfig Configuration source** blade opens, displaying hello PowerShell code for hello configuration.</span></span>

## <a name="compiling-a-configuration-in-azure-automation"></a><span data-ttu-id="644c7-140">Compilation d’une configuration dans Azure Automation</span><span class="sxs-lookup"><span data-stu-id="644c7-140">Compiling a configuration in Azure Automation</span></span>
<span data-ttu-id="644c7-141">Avant de pouvoir appliquer un nœud de tooa d’état souhaité, une configuration DSC définissant cet état doit être compilée dans un ou plusieurs configurations de nœuds (document MOF) et placée sur hello serveur d’extraction Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="644c7-141">Before you can apply a desired state tooa node, a DSC configuration defining that state must be compiled into one or more node configurations (MOF document), and placed on hello Automation DSC Pull Server.</span></span> <span data-ttu-id="644c7-142">Pour obtenir une description plus détaillée de la compilation des configurations dans Azure Automation DSC, consultez [Compilation de configurations dans Azure Automation DSC](automation-dsc-compile.md).</span><span class="sxs-lookup"><span data-stu-id="644c7-142">For a more detailed description of compiling configurations in Azure Automation DSC, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md).</span></span> <span data-ttu-id="644c7-143">Pour plus d’informations sur la compilation des configurations, consultez [Configurations DSC](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span><span class="sxs-lookup"><span data-stu-id="644c7-143">For more information about compiling configurations, see [DSC Configurations](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span></span>

1. <span data-ttu-id="644c7-144">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="644c7-144">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="644c7-145">Dans le menu du Hub hello, cliquez sur **toutes les ressources** , puis hello nom de votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="644c7-145">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="644c7-146">Sur hello **compte Automation** panneau, cliquez sur **les Configurations DSC**</span><span class="sxs-lookup"><span data-stu-id="644c7-146">On hello **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="644c7-147">Sur hello **les Configurations DSC** panneau, cliquez sur **TestConfig** (nom hello Hello précédemment importé configuration).</span><span class="sxs-lookup"><span data-stu-id="644c7-147">On hello **DSC Configurations** blade, click **TestConfig** (hello name of hello previously imported configuration).</span></span>
5. <span data-ttu-id="644c7-148">Sur hello **TestConfig Configuration** panneau, cliquez sur **compiler**, puis cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="644c7-148">On hello **TestConfig Configuration** blade, click **Compile**, and then click **Yes**.</span></span> <span data-ttu-id="644c7-149">Une tâche de compilation démarre.</span><span class="sxs-lookup"><span data-stu-id="644c7-149">This starts a compilation job.</span></span>
   
    ![Capture d’écran du Panneau de configuration hello TestConfig mise en surbrillance le bouton de la compilation](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> <span data-ttu-id="644c7-151">Lorsque vous compilez une configuration dans Azure Automation, il déploie automatiquement n’importe quel serveur collecteur toohello de MOF de configuration nœud créé.</span><span class="sxs-lookup"><span data-stu-id="644c7-151">When you compile a configuration in Azure Automation, it automatically deploys any created node configuration MOFs toohello pull server.</span></span>
> 
> 

## <a name="viewing-a-compilation-job"></a><span data-ttu-id="644c7-152">Affichage d’une tâche de compilation</span><span class="sxs-lookup"><span data-stu-id="644c7-152">Viewing a compilation job</span></span>
<span data-ttu-id="644c7-153">Une fois que vous démarrez une compilation, vous pouvez les consulter dans hello **travaux de Compilation** vignette Bonjour **Configuration** panneau.</span><span class="sxs-lookup"><span data-stu-id="644c7-153">After you start a compilation, you can view it in hello **Compilation jobs** tile in hello **Configuration** blade.</span></span> <span data-ttu-id="644c7-154">Hello **travaux de Compilation** vignette montre en cours d’exécution, terminé et travaux en échec.</span><span class="sxs-lookup"><span data-stu-id="644c7-154">hello **Compilation jobs** tile shows currently running, completed, and failed jobs.</span></span> <span data-ttu-id="644c7-155">Lorsque vous ouvrez un panneau de tâche de compilation, elle affiche des informations sur cette tâche, y compris les erreurs ou les avertissements rencontrés, paramètres d’entrée utilisés dans hello, compilation et la configuration des journaux.</span><span class="sxs-lookup"><span data-stu-id="644c7-155">When you open a compilation job blade, it shows information about that job including any errors or warnings encountered, input parameters used in hello configuration, and compilation logs.</span></span>

1. <span data-ttu-id="644c7-156">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="644c7-156">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="644c7-157">Dans le menu du Hub hello, cliquez sur **toutes les ressources** , puis hello nom de votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="644c7-157">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="644c7-158">Sur hello **compte Automation** panneau, cliquez sur **les Configurations DSC**.</span><span class="sxs-lookup"><span data-stu-id="644c7-158">On hello **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="644c7-159">Sur hello **les Configurations DSC** panneau, cliquez sur **TestConfig** (nom hello Hello précédemment importé configuration).</span><span class="sxs-lookup"><span data-stu-id="644c7-159">On hello **DSC Configurations** blade, click **TestConfig** (hello name of hello previously imported configuration).</span></span>
5. <span data-ttu-id="644c7-160">Sur hello **travaux de Compilation** vignette Hello **TestConfig Configuration** panneau, cliquez sur un des travaux hello répertoriés.</span><span class="sxs-lookup"><span data-stu-id="644c7-160">On hello **Compilation jobs** tile of hello **TestConfig Configuration** blade, click on any of hello jobs listed.</span></span> <span data-ttu-id="644c7-161">A **tâche de Compilation** s’ouvre le panneau, étiquetés avec la date de hello hello la tâche de compilation a été démarré.</span><span class="sxs-lookup"><span data-stu-id="644c7-161">A **Compilation Job** blade opens, labeled with hello date that hello compilation job was started.</span></span>
   
    ![Capture d’écran du Panneau de tâche de Compilation hello](./media/automation-dsc-getting-started/CompilationJob.png)
6. <span data-ttu-id="644c7-163">Cliquez sur n’importe quelle vignette Bonjour **tâche de Compilation** toosee panneau davantage des détails sur les travaux hello.</span><span class="sxs-lookup"><span data-stu-id="644c7-163">Click on any tile in hello **Compilation Job** blade toosee further details about hello job.</span></span>

## <a name="viewing-node-configurations"></a><span data-ttu-id="644c7-164">Affichage des configurations de nœuds</span><span class="sxs-lookup"><span data-stu-id="644c7-164">Viewing node configurations</span></span>
<span data-ttu-id="644c7-165">La réussite d’une tâche de compilation a pour effet de créer une ou plusieurs configurations de nœud.</span><span class="sxs-lookup"><span data-stu-id="644c7-165">Successful completion of a compilation job creates one or more new node configurations.</span></span> <span data-ttu-id="644c7-166">Une configuration de nœud est un document MOF est le serveur du collecteur toohello déployé et prêt toobe extraites et appliquées par un ou plusieurs nœuds.</span><span class="sxs-lookup"><span data-stu-id="644c7-166">A node configuration is a MOF document that is deployed toohello pull server and ready toobe pulled and applied by one or more nodes.</span></span> <span data-ttu-id="644c7-167">Vous pouvez afficher les configurations de nœuds hello dans votre compte Automation Bonjour **Configurations de nœuds DSC** panneau.</span><span class="sxs-lookup"><span data-stu-id="644c7-167">You can view hello node configurations in your Automation account in hello **DSC Node Configurations** blade.</span></span> <span data-ttu-id="644c7-168">Une configuration de nœud a un nom de la forme de hello *ConfigurationName*. *NodeName*.</span><span class="sxs-lookup"><span data-stu-id="644c7-168">A node configuration has a name with hello form *ConfigurationName*.*NodeName*.</span></span>

1. <span data-ttu-id="644c7-169">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="644c7-169">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="644c7-170">Dans le menu du Hub hello, cliquez sur **toutes les ressources** , puis hello nom de votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="644c7-170">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="644c7-171">Sur hello **compte Automation** panneau, cliquez sur **Configurations de nœuds DSC**.</span><span class="sxs-lookup"><span data-stu-id="644c7-171">On hello **Automation account** blade, click **DSC Node Configurations**.</span></span>
   
    ![Capture d’écran du Panneau de configuration de nœuds DSC hello](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a><span data-ttu-id="644c7-173">Intégration d’une machine virtuelle Azure pour la gérer avec Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="644c7-173">Onboarding an Azure VM for management with Azure Automation DSC</span></span>
<span data-ttu-id="644c7-174">Vous pouvez utiliser Azure Automation DSC toomanage machines virtuelles de Azure (classique et le Gestionnaire de ressources), machines virtuelles de local, machines Linux, machines virtuelles de AWS et machines physiques locales.</span><span class="sxs-lookup"><span data-stu-id="644c7-174">You can use Azure Automation DSC toomanage Azure VMs (both Classic and Resource Manager), on-premises VMs, Linux machines, AWS VMs, and on-premises physical machines.</span></span> <span data-ttu-id="644c7-175">Dans cette rubrique, nous abordons la tooonboard uniquement machines virtuelles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="644c7-175">In this topic, we cover how tooonboard only Azure Resource Manager VMs.</span></span> <span data-ttu-id="644c7-176">Pour plus d’informations sur l’intégration d’autres types d’ordinateur, consultez [Gestion de machines avec Azure Automation DSC](automation-dsc-onboarding.md).</span><span class="sxs-lookup"><span data-stu-id="644c7-176">For information about onboarding other types of machines, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md).</span></span>

### <a name="tooonboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a><span data-ttu-id="644c7-177">tooonboard un gestionnaire de ressources d’Azure VM pour la gestion par Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="644c7-177">tooonboard an Azure Resource Manager VM for management by Azure Automation DSC</span></span>
1. <span data-ttu-id="644c7-178">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="644c7-178">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="644c7-179">Dans le menu du Hub hello, cliquez sur **toutes les ressources** , puis hello nom de votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="644c7-179">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="644c7-180">Sur hello **compte Automation** panneau, cliquez sur **nœuds DSC**.</span><span class="sxs-lookup"><span data-stu-id="644c7-180">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="644c7-181">Bonjour **nœuds DSC** panneau, cliquez sur **ajouter Azure VM**.</span><span class="sxs-lookup"><span data-stu-id="644c7-181">In hello **DSC Nodes** blade, click **Add Azure VM**.</span></span>
   
    ![Capture d’écran du Panneau de nœuds DSC hello mise en surbrillance le bouton d’ajout de machine virtuelle Azure hello](./media/automation-dsc-getting-started/OnboardVM.png)
5. <span data-ttu-id="644c7-183">Bonjour **ajouter des machines virtuelles Azure** panneau, cliquez sur **sélectionner des machines virtuelles tooonboard**.</span><span class="sxs-lookup"><span data-stu-id="644c7-183">In hello **Add Azure VMs** blade, click **Select virtual machines tooonboard**.</span></span>
6. <span data-ttu-id="644c7-184">Bonjour **sélectionner les machines virtuelles** panneau, sélectionnez hello machine virtuelle que vous souhaitez tooonboard, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="644c7-184">In hello **Select VMs** blade, select hello VM you want tooonboard, and click **OK**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="644c7-185">Il doit s’agir d’une machine virtuelle Azure Resource Manager exécutant Windows Server 2008 R2 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="644c7-185">This must be an Azure Resource Manager VM running Windows Server 2008 R2 or later.</span></span>
   > 
   > 
7. <span data-ttu-id="644c7-186">Bonjour **ajouter des machines virtuelles Azure** panneau, cliquez sur **configurer les données d’inscription**.</span><span class="sxs-lookup"><span data-stu-id="644c7-186">In hello **Add Azure VMs** blade, click **Configure registration data**.</span></span>
8. <span data-ttu-id="644c7-187">Bonjour **inscription** panneau, entrez le nom de hello de configuration du nœud hello souhaité tooapply toohello VM Bonjour **nom de Configuration de nœud** boîte.</span><span class="sxs-lookup"><span data-stu-id="644c7-187">In hello **Registration** blade, enter hello name of hello node configuration you want tooapply toohello VM in hello **Node Configuration Name** box.</span></span> <span data-ttu-id="644c7-188">Cela doit correspondre exactement à nom hello d’une configuration de nœud Bonjour compte Automation.</span><span class="sxs-lookup"><span data-stu-id="644c7-188">This must exactly match hello name of a node configuration in hello Automation account.</span></span> <span data-ttu-id="644c7-189">Vous n’êtes pas obligé de fournir un nom à ce stade.</span><span class="sxs-lookup"><span data-stu-id="644c7-189">Providing a name at this point is optional.</span></span> <span data-ttu-id="644c7-190">Vous pouvez modifier la configuration du nœud hello affecté après le nœud de hello d’intégration.</span><span class="sxs-lookup"><span data-stu-id="644c7-190">You can change hello assigned node configuration after onboarding hello node.</span></span>
   <span data-ttu-id="644c7-191">Cochez la case **Redémarrer le nœud si nécessaire**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="644c7-191">Check **Reboot Node if Needed**, and then click **OK**.</span></span>
   
    ![Capture d’écran du Panneau de l’inscription de hello](./media/automation-dsc-getting-started/RegisterVM.png)
   
    <span data-ttu-id="644c7-193">configuration de nœud Hello spécifiée sera appliqué toohello VM selon l’intervalle spécifié par hello **fréquence de Mode de Configuration**, et vérifie pour la configuration du nœud toohello mises à jour selon l’intervalle spécifié par hello hellomachinevirtuelle **Fréquence d’actualisation**.</span><span class="sxs-lookup"><span data-stu-id="644c7-193">hello node configuration you specified will be applied toohello VM at intervals specified by hello **Configuration Mode Frequency**, and hello VM will check for updates toohello node configuration at intervals specified by hello **Refresh Frequency**.</span></span> <span data-ttu-id="644c7-194">Pour plus d’informations sur la façon dont ces valeurs sont utilisées, consultez [configuration hello Gestionnaire de Configuration Local](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span><span class="sxs-lookup"><span data-stu-id="644c7-194">For more information about how these values are used, see [Configuring hello Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span></span>
9. <span data-ttu-id="644c7-195">Bonjour **ajouter des machines virtuelles Azure** panneau, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="644c7-195">In hello **Add Azure VMs** blade, click **Create**.</span></span>

<span data-ttu-id="644c7-196">Azure démarre processus hello de l’intégration hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="644c7-196">Azure will start hello process of onboarding hello VM.</span></span> <span data-ttu-id="644c7-197">Lorsqu’il est terminé, hello machine virtuelle s’afficheront dans hello **nœuds DSC** panneau Bonjour compte Automation.</span><span class="sxs-lookup"><span data-stu-id="644c7-197">When it is complete, hello VM will show up in hello **DSC Nodes** blade in hello Automation account.</span></span>

## <a name="viewing-hello-list-of-dsc-nodes"></a><span data-ttu-id="644c7-198">Affichage de liste de hello de nœuds DSC</span><span class="sxs-lookup"><span data-stu-id="644c7-198">Viewing hello list of DSC nodes</span></span>
<span data-ttu-id="644c7-199">Vous pouvez afficher la liste de hello de tous les ordinateurs qui ont été intégrées pour la gestion de votre compte Automation Bonjour **nœuds DSC** panneau.</span><span class="sxs-lookup"><span data-stu-id="644c7-199">You can view hello list of all machines that have been onboarded for management in your Automation account in hello **DSC Nodes** blade.</span></span>

1. <span data-ttu-id="644c7-200">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="644c7-200">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="644c7-201">Dans le menu du Hub hello, cliquez sur **toutes les ressources** , puis hello nom de votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="644c7-201">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="644c7-202">Sur hello **compte Automation** panneau, cliquez sur **nœuds DSC**.</span><span class="sxs-lookup"><span data-stu-id="644c7-202">On hello **Automation account** blade, click **DSC Nodes**.</span></span>

## <a name="viewing-reports-for-dsc-nodes"></a><span data-ttu-id="644c7-203">Affichage des rapports de nœuds DSC</span><span class="sxs-lookup"><span data-stu-id="644c7-203">Viewing reports for DSC nodes</span></span>
<span data-ttu-id="644c7-204">Chaque fois que Azure Automation DSC effectue une vérification de cohérence sur un nœud géré, nœud de hello envoie un état rapport toohello différé par extraction de données serveur.</span><span class="sxs-lookup"><span data-stu-id="644c7-204">Each time Azure Automation DSC performs a consistency check on a managed node, hello node sends a status report back toohello pull server.</span></span> <span data-ttu-id="644c7-205">Vous pouvez consulter ces rapports sur le panneau hello pour ce nœud.</span><span class="sxs-lookup"><span data-stu-id="644c7-205">You can view these reports on hello blade for that node.</span></span>

1. <span data-ttu-id="644c7-206">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="644c7-206">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="644c7-207">Dans le menu du Hub hello, cliquez sur **toutes les ressources** , puis hello nom de votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="644c7-207">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="644c7-208">Sur hello **compte Automation** panneau, cliquez sur **nœuds DSC**.</span><span class="sxs-lookup"><span data-stu-id="644c7-208">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="644c7-209">Sur hello **rapports** vignette, cliquez sur un des rapports hello dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="644c7-209">On hello **Reports** tile, click on any of hello reports in hello list.</span></span>
   
    ![Capture d’écran du Panneau de rapport hello](./media/automation-dsc-getting-started/NodeReport.png)

<span data-ttu-id="644c7-211">Dans Panneau de hello pour un rapport individuel, vous pouvez voir hello suit les informations d’état de cohérence correspondante de hello vérifier :</span><span class="sxs-lookup"><span data-stu-id="644c7-211">On hello blade for an individual report, you can see hello following status information for hello corresponding consistency check:</span></span>

* <span data-ttu-id="644c7-212">Hello état — si le nœud de hello est « Conforme », la configuration de hello « Failed », ou nœud de hello est « Non conforme » (lorsque le nœud de hello est à **applyandmonitor** mode et hello machine n’est pas en état de hello souhaité).</span><span class="sxs-lookup"><span data-stu-id="644c7-212">hello report status — whether hello node is "Compliant", hello configuration "Failed", or hello node is "Not Compliant" (when hello node is in **applyandmonitor** mode and hello machine is not in hello desired state).</span></span>
* <span data-ttu-id="644c7-213">Hello heure de début de la vérification de cohérence hello.</span><span class="sxs-lookup"><span data-stu-id="644c7-213">hello start time for hello consistency check.</span></span>
* <span data-ttu-id="644c7-214">temps total d’exécution Hello par souci de cohérence hello vérifier.</span><span class="sxs-lookup"><span data-stu-id="644c7-214">hello total runtime for hello consistency check.</span></span>
* <span data-ttu-id="644c7-215">vérification de type Hello de cohérence.</span><span class="sxs-lookup"><span data-stu-id="644c7-215">hello type of consistency check.</span></span>
* <span data-ttu-id="644c7-216">Toutes les erreurs, y compris le message d’erreur et le code erreur hello.</span><span class="sxs-lookup"><span data-stu-id="644c7-216">Any errors, including hello error code and error message.</span></span> 
* <span data-ttu-id="644c7-217">Toutes les ressources DSC utilisées dans la configuration de hello et état hello de chaque ressource (si hello nœud est en état hello souhaité pour cette ressource) : vous pouvez cliquer sur chaque ressource tooget des informations plus détaillées pour cette ressource.</span><span class="sxs-lookup"><span data-stu-id="644c7-217">Any DSC resources used in hello configuration, and hello state of each resource (whether hello node is in hello desired state for that resource) — you can click on each resource tooget more detailed information for that resource.</span></span>
* <span data-ttu-id="644c7-218">nom de Hello, adresse IP et le mode de configuration du nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="644c7-218">hello name, IP address, and configuration mode of hello node.</span></span>

<span data-ttu-id="644c7-219">Vous pouvez également cliquer sur **affichage brut** toosee hello données effectivement hello nœud envoie toohello server.</span><span class="sxs-lookup"><span data-stu-id="644c7-219">You can also click **View raw report** toosee hello actual data that hello node sends toohello server.</span></span> <span data-ttu-id="644c7-220">Pour plus d’informations sur l’utilisation de ces données, consultez la page [Utilisation d’un serveur de rapports DSC](https://msdn.microsoft.com/powershell/dsc/reportserver).</span><span class="sxs-lookup"><span data-stu-id="644c7-220">For more information about using that data, see [Using a DSC report server](https://msdn.microsoft.com/powershell/dsc/reportserver).</span></span>

<span data-ttu-id="644c7-221">Il peut prendre un certain temps, une fois un nœud embarquées avant hello premier état est disponible.</span><span class="sxs-lookup"><span data-stu-id="644c7-221">It can take some time after a node is onboarded before hello first report is available.</span></span> <span data-ttu-id="644c7-222">Vous devrez peut-être toowait des too30 minutes pour le premier rapport de hello après avoir intégrer un nœud.</span><span class="sxs-lookup"><span data-stu-id="644c7-222">You might need toowait up too30 minutes for hello first report after you onboard a node.</span></span>

## <a name="reassigning-a-node-tooa-different-node-configuration"></a><span data-ttu-id="644c7-223">Réaffectation d’une configuration de nœud différents nœuds tooa</span><span class="sxs-lookup"><span data-stu-id="644c7-223">Reassigning a node tooa different node configuration</span></span>
<span data-ttu-id="644c7-224">Vous pouvez affecter un toouse nœud une configuration de nœud autre que hello une qu'initialement affecté.</span><span class="sxs-lookup"><span data-stu-id="644c7-224">You can assign a node toouse a different node configuration than hello one you initially assigned.</span></span>

1. <span data-ttu-id="644c7-225">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="644c7-225">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="644c7-226">Dans le menu du Hub hello, cliquez sur **toutes les ressources** , puis hello nom de votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="644c7-226">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="644c7-227">Sur hello **compte Automation** panneau, cliquez sur **nœuds DSC**.</span><span class="sxs-lookup"><span data-stu-id="644c7-227">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="644c7-228">Sur hello **nœuds DSC** panneau, cliquez sur le nom hello du nœud de hello souhaité tooreassign.</span><span class="sxs-lookup"><span data-stu-id="644c7-228">On hello **DSC Nodes** blade, click on hello name of hello node you want tooreassign.</span></span>
5. <span data-ttu-id="644c7-229">Dans le panneau de hello pour ce nœud, cliquez sur **nœud Assign**.</span><span class="sxs-lookup"><span data-stu-id="644c7-229">On hello blade for that node, click **Assign node**.</span></span>
   
    ![Capture d’écran du Panneau de nœud hello mise en surbrillance le bouton d’attribuer un nœud hello](./media/automation-dsc-getting-started/AssignNode.png)
6. <span data-ttu-id="644c7-231">Sur hello **attribuer une Configuration de nœud** panneau, sélectionnez hello nœud configuration toowhich vous souhaitez tooassign hello nœud, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="644c7-231">On hello **Assign Node Configuration** blade, select hello node configuration toowhich you want tooassign hello node, and then click **OK**.</span></span>
   
    ![Capture d’écran du Panneau de Configuration du nœud affecter hello](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a><span data-ttu-id="644c7-233">Annulation de l’inscription d’un nœud</span><span class="sxs-lookup"><span data-stu-id="644c7-233">Unregistering a node</span></span>
<span data-ttu-id="644c7-234">Si vous ne voulez plus un toobe de nœud géré par Azure Automation DSC, vous pouvez annuler son inscription.</span><span class="sxs-lookup"><span data-stu-id="644c7-234">If you no longer want a node toobe managed by Azure Automation DSC, you can unregister it.</span></span>

1. <span data-ttu-id="644c7-235">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="644c7-235">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="644c7-236">Dans le menu du Hub hello, cliquez sur **toutes les ressources** , puis hello nom de votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="644c7-236">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="644c7-237">Sur hello **compte Automation** panneau, cliquez sur **nœuds DSC**.</span><span class="sxs-lookup"><span data-stu-id="644c7-237">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="644c7-238">Sur hello **nœuds DSC** panneau, cliquez sur le nom hello du nœud de hello souhaité toounregister.</span><span class="sxs-lookup"><span data-stu-id="644c7-238">On hello **DSC Nodes** blade, click on hello name of hello node you want toounregister.</span></span>
5. <span data-ttu-id="644c7-239">Dans le panneau de hello pour ce nœud, cliquez sur **Unregister**.</span><span class="sxs-lookup"><span data-stu-id="644c7-239">On hello blade for that node, click **Unregister**.</span></span>
   
    ![Capture d’écran du Panneau de nœud hello mise en surbrillance le bouton Annuler l’enregistrement de hello](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a><span data-ttu-id="644c7-241">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="644c7-241">Related Articles</span></span>
* [<span data-ttu-id="644c7-242">Vue d’ensemble d’Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="644c7-242">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="644c7-243">Gestion de machines avec Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="644c7-243">Onboarding machines for management by Azure Automation DSC</span></span>](automation-dsc-onboarding.md)
* [<span data-ttu-id="644c7-244">Vue d’ensemble d’Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="644c7-244">Windows PowerShell Desired State Configuration Overview</span></span>](https://msdn.microsoft.com/powershell/dsc/overview)
* [<span data-ttu-id="644c7-245">Applets de commande Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="644c7-245">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="644c7-246">Tarification d’Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="644c7-246">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)

