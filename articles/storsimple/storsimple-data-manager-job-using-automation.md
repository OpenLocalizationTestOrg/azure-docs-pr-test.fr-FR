---
title: aaaUse Azure Automation tootrigger un travail | Documents Microsoft
description: "Découvrez comment toouse Azure Automation pour déclencher des travaux du Gestionnaire de données de StorSimple (aperçu privé)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 0d9d6e5e6d52ed27ca759ed7e949b5f5dfd319c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-automation-tootrigger-a-job-private-preview"></a><span data-ttu-id="8546a-103">Utilisez Azure Automation tootrigger un travail (aperçu privé)</span><span class="sxs-lookup"><span data-stu-id="8546a-103">Use Azure Automation tootrigger a job (Private Preview)</span></span>

<span data-ttu-id="8546a-104">Cet article explique comment toouse Azure Automation tootrigger une tâche du Gestionnaire de données de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="8546a-104">This articles describes how toouse Azure Automation tootrigger a StorSimple Data Manager job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8546a-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8546a-105">Prerequisites</span></span>

<span data-ttu-id="8546a-106">Avant de commencer, assurez-vous de satisfaire les exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="8546a-106">Before you begin, ensure that you have:</span></span>

*   <span data-ttu-id="8546a-107">Azure Powershell installé.</span><span class="sxs-lookup"><span data-stu-id="8546a-107">Azure Powershell installed.</span></span> <span data-ttu-id="8546a-108">[Téléchargez Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="8546a-108">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="8546a-109">Configuration travail paramètres de tooinitialize hello Transformation de données (instructions tooobtain ces paramètres sont inclus ici).</span><span class="sxs-lookup"><span data-stu-id="8546a-109">Configuration settings tooinitialize hello Data Transformation job (instructions tooobtain these settings are included here).</span></span>
*   <span data-ttu-id="8546a-110">Une définition de travail qui a été configurée correctement dans une ressource de données hybride dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8546a-110">A job definition that has been correctly configured in a Hybrid Data Resource within a resource group.</span></span>
*   <span data-ttu-id="8546a-111">Télécharger `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) fichier à partir du référentiel github de hello.</span><span class="sxs-lookup"><span data-stu-id="8546a-111">Download `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) file from hello github repository.</span></span>
*   <span data-ttu-id="8546a-112">Télécharger `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) à partir du référentiel github de hello.</span><span class="sxs-lookup"><span data-stu-id="8546a-112">Download `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) from hello github repository.</span></span>
*   <span data-ttu-id="8546a-113">Télécharger `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) à partir du référentiel github de hello.</span><span class="sxs-lookup"><span data-stu-id="8546a-113">Download `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) from hello github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="8546a-114">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="8546a-114">Step-by-step</span></span>

### <a name="get-azure-active-directory-permissions-for-hello-automation-job-toorun-hello-job-definition"></a><span data-ttu-id="8546a-115">Obtenir les autorisations de Azure Active Directory pour la définition de tâche du travail toorun hello hello automation</span><span class="sxs-lookup"><span data-stu-id="8546a-115">Get Azure Active Directory permissions for hello automation job toorun hello job definition</span></span>

1. <span data-ttu-id="8546a-116">paramètres de configuration tooretrieve hello pour Active Directory, procédez comme hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8546a-116">tooretrieve hello configuration parameters for Active Directory, do hello following steps:</span></span>

    1. <span data-ttu-id="8546a-117">Ouvrez Windows PowerShell sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="8546a-117">Open Windows PowerShell in your local machine.</span></span> <span data-ttu-id="8546a-118">Vérifiez que [Azure PowerShell](https://azure.microsoft.com/downloads/) est installé.</span><span class="sxs-lookup"><span data-stu-id="8546a-118">Ensure that [Azure PowerShell](https://azure.microsoft.com/downloads/) is installed.</span></span>
    1. <span data-ttu-id="8546a-119">Exécutez hello `Get-ConfigurationParams.ps1` script (dans le dossier hello vous avez téléchargé).</span><span class="sxs-lookup"><span data-stu-id="8546a-119">Run hello `Get-ConfigurationParams.ps1` script (in hello folder you downloaded above).</span></span> <span data-ttu-id="8546a-120">Tapez hello commande dans la fenêtre de hello PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="8546a-120">Type hello following command in hello PowerShell window:</span></span>

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        <span data-ttu-id="8546a-121">Hello ActiveDirectoryKey est un mot de passe que vous utilisez plus tard.</span><span class="sxs-lookup"><span data-stu-id="8546a-121">hello ActiveDirectoryKey is a password that you use later.</span></span> <span data-ttu-id="8546a-122">Entrez un mot de passe de votre choix.</span><span class="sxs-lookup"><span data-stu-id="8546a-122">Enter a password of your choice.</span></span> <span data-ttu-id="8546a-123">N’importe quelle chaîne peut être utilisée pour AppName.</span><span class="sxs-lookup"><span data-stu-id="8546a-123">AppName can be any string.</span></span>

2. <span data-ttu-id="8546a-124">Ce script génère hello valeurs qui doivent être utilisés lors du déclenchement du runbook automation de hello suivantes.</span><span class="sxs-lookup"><span data-stu-id="8546a-124">This script outputs hello following values that should be used while triggering hello automation runbook.</span></span> <span data-ttu-id="8546a-125">Prenez note de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="8546a-125">Make a note of these values.</span></span>

    - <span data-ttu-id="8546a-126">ID client</span><span class="sxs-lookup"><span data-stu-id="8546a-126">Client ID</span></span>
    - <span data-ttu-id="8546a-127">ID client</span><span class="sxs-lookup"><span data-stu-id="8546a-127">Tenant ID</span></span>
    - <span data-ttu-id="8546a-128">Clé Active Directory (identique à une entrée ci-dessus hello)</span><span class="sxs-lookup"><span data-stu-id="8546a-128">Active Directory key (same as hello one entered above)</span></span>
    - <span data-ttu-id="8546a-129">Identifiant d’abonnement</span><span class="sxs-lookup"><span data-stu-id="8546a-129">Subscription ID</span></span>

### <a name="set-up-hello-automation-account"></a><span data-ttu-id="8546a-130">Configurer hello compte Automation</span><span class="sxs-lookup"><span data-stu-id="8546a-130">Set up hello Automation Account</span></span>

1. <span data-ttu-id="8546a-131">Connectez-vous à tooAzure et ouvrez votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="8546a-131">Log on tooAzure and open your Automation account.</span></span>
2. <span data-ttu-id="8546a-132">Cliquez sur **actifs** vignette tooopen hello liste de ressources.</span><span class="sxs-lookup"><span data-stu-id="8546a-132">Click **Assets** tile tooopen hello list of assets.</span></span>
3. <span data-ttu-id="8546a-133">Cliquez sur **Modules** vignette tooopen hello liste des modules.</span><span class="sxs-lookup"><span data-stu-id="8546a-133">Click **Modules** tile tooopen hello list of modules.</span></span>
4. <span data-ttu-id="8546a-134">Cliquez sur **+ ajouter un module** Panneau de module ajouter bouton et hello est lancée.</span><span class="sxs-lookup"><span data-stu-id="8546a-134">Click **+ Add a module** button and hello Add module blade is launched.</span></span>

    ![Paramètres du compte Automation](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. <span data-ttu-id="8546a-136">Une fois que vous avez sélectionné hello `DataTransformationApp.zip` de fichiers à partir de votre ordinateur local, cliquez sur **OK** module de hello tooimport.</span><span class="sxs-lookup"><span data-stu-id="8546a-136">After you have selected hello `DataTransformationApp.zip` file from your local computer, click **OK** tooimport hello module.</span></span>

   <span data-ttu-id="8546a-137">Lorsque Azure Automation importe un compte tooyour de module, il extrait les métadonnées sur le module de hello.</span><span class="sxs-lookup"><span data-stu-id="8546a-137">When Azure Automation imports a module tooyour account, it extracts metadata about hello module.</span></span> <span data-ttu-id="8546a-138">Cette opération peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="8546a-138">This operation may take a couple of minutes.</span></span>

   ![Paramètres du compte Automation](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. <span data-ttu-id="8546a-140">Vous recevez une notification indiquant que le module hello est en cours de déploiement et une autre notification lorsque hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="8546a-140">You receive a notification that hello module is being deployed and another notification when hello process is complete.</span></span>  <span data-ttu-id="8546a-141">Vous pouvez également vérifier l’état de hello **Modules** vignette.</span><span class="sxs-lookup"><span data-stu-id="8546a-141">You can also check hello status in **Modules** tile.</span></span>

### <a name="tooimport-hello-runbook-that-triggers-hello-job-definition"></a><span data-ttu-id="8546a-142">tooimport hello runbook qui déclenche la définition de la tâche hello</span><span class="sxs-lookup"><span data-stu-id="8546a-142">tooimport hello runbook that triggers hello job definition</span></span>

1. <span data-ttu-id="8546a-143">Bonjour portail Azure, ouvrez votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="8546a-143">In hello Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="8546a-144">Cliquez sur **Runbooks** vignette tooopen hello liste des runbooks.</span><span class="sxs-lookup"><span data-stu-id="8546a-144">Click **Runbooks** tile tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="8546a-145">Cliquez sur **+ Ajouter un runbook**, puis sur **Importer un Runbook existant**.</span><span class="sxs-lookup"><span data-stu-id="8546a-145">Click **+ Add a runbook** and then **Import an existing runbook**.</span></span>

   ![Importer un runbook existant](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. <span data-ttu-id="8546a-147">Cliquez sur **fichier de Runbook** et sélectionnez hello fichier tooimport `Trigger-DataTransformation-Job.ps1`.</span><span class="sxs-lookup"><span data-stu-id="8546a-147">Click **Runbook file** and select hello file tooimport `Trigger-DataTransformation-Job.ps1`.</span></span>
5. <span data-ttu-id="8546a-148">Cliquez sur **créer** tooimport hello runbook.</span><span class="sxs-lookup"><span data-stu-id="8546a-148">Click **Create** tooimport hello runbook.</span></span> <span data-ttu-id="8546a-149">Hello nouveau runbook apparaît dans la liste hello des procédures opérationnelles pour hello compte Automation.</span><span class="sxs-lookup"><span data-stu-id="8546a-149">hello new runbook appears in hello list of runbooks for hello Automation account.</span></span>
7. <span data-ttu-id="8546a-150">Cliquez sur le runbook **Trigger-DataTransformation-Job**, puis sur **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="8546a-150">Click **Trigger-DataTransformation-Job** runbook and then click **Edit**.</span></span>
8. <span data-ttu-id="8546a-151">Cliquez sur **Publier**, puis sur **Oui** lorsque vous êtes invité à confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="8546a-151">Click **Publish** and then **Yes** when prompted for confirmation.</span></span>


### <a name="toorun-hello-runbook"></a><span data-ttu-id="8546a-152">toorun hello runbook :</span><span class="sxs-lookup"><span data-stu-id="8546a-152">toorun hello runbook:</span></span>
1. <span data-ttu-id="8546a-153">Bonjour portail Azure, ouvrez votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="8546a-153">In hello Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="8546a-154">Cliquez sur hello **Runbooks** vignette tooopen hello liste des runbooks.</span><span class="sxs-lookup"><span data-stu-id="8546a-154">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="8546a-155">Cliquez sur **Trigger-DataTransformation-Job**.</span><span class="sxs-lookup"><span data-stu-id="8546a-155">Click **Trigger-DataTransformation-Job**.</span></span>
4. <span data-ttu-id="8546a-156">Cliquez sur **Démarrer** toostart hello runbook.</span><span class="sxs-lookup"><span data-stu-id="8546a-156">Click **Start** toostart hello runbook.</span></span>

   ![Démarrer un Runbook](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. <span data-ttu-id="8546a-158">Bonjour **démarrer runbook** panneau, entrez tous les paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="8546a-158">In hello **Start runbook** blade, enter all hello parameters.</span></span> <span data-ttu-id="8546a-159">Cliquez sur **OK** tâche de Transformation des données toosubmit hello.</span><span class="sxs-lookup"><span data-stu-id="8546a-159">Click **OK** toosubmit hello Data Transformation job.</span></span>

   ![Démarrer un Runbook](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a><span data-ttu-id="8546a-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8546a-161">Next steps</span></span>

<span data-ttu-id="8546a-162">[Utilisez l’interface utilisateur de gestionnaire de données StorSimple tootransform vos données](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="8546a-162">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
