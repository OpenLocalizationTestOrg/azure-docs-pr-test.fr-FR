---
title: "Automatisation de l’installation du service Mobilité pour Azure Site Recovery à l’aide d’outils de déploiement de logiciels | Microsoft Docs"
description: "Cet article vous aide à automatiser l’installation du service Mobilité à l’aide d’outils de déploiement de logiciels tels que System Center Configuration Manager."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 49b72cd306aa91f114af7688f02d95db6f6eca05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a><span data-ttu-id="7f92b-103">Automatisation de l’installation du service Mobilité à l’aide d’outils de déploiement de logiciels</span><span class="sxs-lookup"><span data-stu-id="7f92b-103">Automate Mobility Service installation by using software deployment tools</span></span>

>[!IMPORTANT]
<span data-ttu-id="7f92b-104">Ce document part du principe que vous utilisez la version **9.9.4510.1** ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="7f92b-104">This document assumes you are using version **9.9.4510.1** or higher.</span></span>

<span data-ttu-id="7f92b-105">Cet article fournit un exemple de l’utilisation de System Center Configuration Manager pour déployer le service Mobilité Azure Site Recovery dans votre centre de données.</span><span class="sxs-lookup"><span data-stu-id="7f92b-105">This article provides you an example of how you can use System Center Configuration Manager to deploy the Azure Site Recovery Mobility Service in your datacenter.</span></span> <span data-ttu-id="7f92b-106">L’utilisation d’un outil de déploiement de logiciels tel que Configuration Manager vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="7f92b-106">Using a software deployment tool like Configuration Manager has the following advantages:</span></span>
* <span data-ttu-id="7f92b-107">Planification du déploiement (nouvelles installations et mises à niveau) pendant votre fenêtre de maintenance planifiée pour les mises à jour logicielles</span><span class="sxs-lookup"><span data-stu-id="7f92b-107">Scheduling deployment of fresh installations and upgrades, during your planned maintenance window for software updates</span></span>
* <span data-ttu-id="7f92b-108">Mise à l’échelle du déploiement pour des centaines de serveurs simultanément</span><span class="sxs-lookup"><span data-stu-id="7f92b-108">Scaling deployment to hundreds of servers simultaneously</span></span>


> [!NOTE]
> <span data-ttu-id="7f92b-109">Cet article utilise System Center Configuration Manager 2012 R2 pour illustrer l’activité de déploiement.</span><span class="sxs-lookup"><span data-stu-id="7f92b-109">This article uses System Center Configuration Manager 2012 R2 to demonstrate the deployment activity.</span></span> <span data-ttu-id="7f92b-110">Vous pouvez également automatiser l’installation du service Mobilité à l’aide [d’Azure Automation et de la Configuration de l’état souhaité](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="7f92b-110">You could also automate Mobility Service installation by using [Azure Automation and Desired State Configuration](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f92b-111">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="7f92b-111">Prerequisites</span></span>
1. <span data-ttu-id="7f92b-112">Un outil de déploiement de logiciels tel que Configuration Manager qui est déjà déployé dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="7f92b-112">A software deployment tool, like Configuration Manager, that is already deployed in your environment.</span></span>
  <span data-ttu-id="7f92b-113">Créez deux [regroupements d’appareils](https://technet.microsoft.com/library/gg682169.aspx), un pour tous les **serveurs Windows** et l’autre pour tous les **serveurs Linux** que vous souhaitez protéger à l’aide de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="7f92b-113">Create two [device collections](https://technet.microsoft.com/library/gg682169.aspx), one for all **Windows servers**, and another for all **Linux servers**, that you want to protect by using Site Recovery.</span></span>
3. <span data-ttu-id="7f92b-114">Un serveur de configuration qui est déjà inscrit auprès Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="7f92b-114">A configuration server that is already registered with Site Recovery.</span></span>
4. <span data-ttu-id="7f92b-115">Un partage de fichiers réseau sécurisé (partage SMB) qui est accessible par le serveur Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="7f92b-115">A secure network file share (Server Message Block share) that can be accessed by the Configuration Manager server.</span></span>

## <a name="deploy-mobility-service-on-computers-running-windows"></a><span data-ttu-id="7f92b-116">Déploiement du service Mobilité sur des ordinateurs exécutant Windows</span><span class="sxs-lookup"><span data-stu-id="7f92b-116">Deploy Mobility Service on computers running Windows</span></span>
> [!NOTE]
> <span data-ttu-id="7f92b-117">Cet article part du principe que l’adresse IP du serveur de configuration est 192.168.3.121, et que le partage de fichiers réseau sécurisé est \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="7f92b-117">This article assumes that the IP address of the configuration server is 192.168.3.121, and that the secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="7f92b-118">Étape 1 : Préparation du déploiement</span><span class="sxs-lookup"><span data-stu-id="7f92b-118">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="7f92b-119">Créez un dossier sur le partage réseau et nommez-le **MobSvcWindows**.</span><span class="sxs-lookup"><span data-stu-id="7f92b-119">Create a folder on the network share, and name it **MobSvcWindows**.</span></span>
2. <span data-ttu-id="7f92b-120">Ouvrez une session sur votre serveur de configuration et ouvrez une invite de commandes d’administration.</span><span class="sxs-lookup"><span data-stu-id="7f92b-120">Sign in to your configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="7f92b-121">Exécutez les commandes suivantes pour générer un fichier de phrase secrète :</span><span class="sxs-lookup"><span data-stu-id="7f92b-121">Run the following commands to generate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="7f92b-122">Copiez le fichier **MobSvc.passphrase** dans le dossier **MobSvcWindows** sur le partage réseau.</span><span class="sxs-lookup"><span data-stu-id="7f92b-122">Copy the **MobSvc.passphrase** file into the **MobSvcWindows** folder on your network share.</span></span>
5. <span data-ttu-id="7f92b-123">Naviguez jusqu’au référentiel du programme d’installation sur le serveur de configuration en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7f92b-123">Browse to the installer repository on the configuration server by running the following command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="7f92b-124">Copiez **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe** dans le dossier **MobSvcWindows** sur votre partage réseau.</span><span class="sxs-lookup"><span data-stu-id="7f92b-124">Copy the **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe** to the **MobSvcWindows** folder on your network share.</span></span>
7. <span data-ttu-id="7f92b-125">Copiez le code ci-dessous et enregistrez-le en tant que **install.bat** dans le dossier **MobSvcWindows**.</span><span class="sxs-lookup"><span data-stu-id="7f92b-125">Copy the following code, and save it as **install.bat** into the **MobSvcWindows** folder.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7f92b-126">Remplacez les espaces réservés [CSIP] dans le script ci-dessous par les valeurs réelles de l’adresse IP de votre serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="7f92b-126">Replace the [CSIP] placeholders in this script with the actual values of the IP address of your configuration server.</span></span>

```DOS
Time /t >> C:\Temp\logfile.log
REM ==================================================
REM ==== Clean up the folders ========================
RMDIR /S /q %temp%\MobSvc
MKDIR %Temp%\MobSvc
MKDIR C:\Temp
REM ==================================================

REM ==== Copy new files ==============================
COPY M*.* %Temp%\MobSvc
CD %Temp%\MobSvc
REN Micro*.exe MobSvcInstaller.exe
REM ==================================================

REM ==== Extract the installer =======================
MobSvcInstaller.exe /q /x:%Temp%\MobSvc\Extracted
REM ==== Wait 10s for extraction to complete =========
TIMEOUT /t 10
REM =================================================

REM ==== Perform installation =======================
REM =================================================

CD %Temp%\MobSvc\Extracted
whoami >> C:\Temp\logfile.log
SET PRODKEY=HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall
REG QUERY %PRODKEY%\{275197FC-14FD-4560-A5EB-38217F80CBD1}
IF NOT %ERRORLEVEL% EQU 0 (
    echo "Product is not installed. Goto INSTALL." >> C:\Temp\logfile.log
    GOTO :INSTALL
) ELSE (
    echo "Product is installed." >> C:\Temp\logfile.log

    echo "Checking for Post-install action status." >> C:\Temp\logfile.log
    GOTO :POSTINSTALLCHECK
)

:POSTINSTALLCHECK
    REG QUERY "HKLM\SOFTWARE\Wow6432Node\InMage Systems\Installed Products\5" /v "PostInstallActions" | Find "Succeeded"
    If %ERRORLEVEL% EQU 0 (
        echo "Post-install actions succeeded. Checking for Configuration status." >> C:\Temp\logfile.log
        GOTO :CONFIGURATIONCHECK
    ) ELSE (
        echo "Post-install actions didn't succeed. Goto INSTALL." >> C:\Temp\logfile.log
        GOTO :INSTALL
    )

:CONFIGURATIONCHECK
    REG QUERY "HKLM\SOFTWARE\Wow6432Node\InMage Systems\Installed Products\5" /v "AgentConfigurationStatus" | Find "Succeeded"
    If %ERRORLEVEL% EQU 0 (
        echo "Configuration has succeeded. Goto UPGRADE." >> C:\Temp\logfile.log
        GOTO :UPGRADE
    ) ELSE (
        echo "Configuration didn't succeed. Goto CONFIGURE." >> C:\Temp\logfile.log
        GOTO :CONFIGURE
    )


:INSTALL
    echo "Perform installation." >> C:\Temp\logfile.log
    UnifiedAgent.exe /Role MS /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
    IF %ERRORLEVEL% EQU 0 (
        echo "Installation has succeeded." >> C:\Temp\logfile.log
        (GOTO :CONFIGURE)
    ) ELSE (
        echo "Installation has failed." >> C:\Temp\logfile.log
        GOTO :ENDSCRIPT
    )

:CONFIGURE
    echo "Perform configuration." >> C:\Temp\logfile.log
    cd "C:\Program Files (x86)\Microsoft Azure Site Recovery\agent"
    UnifiedAgentConfigurator.exe  /CSEndPoint "[CSIP]" /PassphraseFilePath %Temp%\MobSvc\MobSvc.passphrase
    IF %ERRORLEVEL% EQU 0 (
        echo "Configuration has succeeded." >> C:\Temp\logfile.log
    ) ELSE (
        echo "Configuration has failed." >> C:\Temp\logfile.log
    )
    GOTO :ENDSCRIPT

:UPGRADE
    echo "Perform upgrade." >> C:\Temp\logfile.log
    UnifiedAgent.exe /Platform "VmWare" /Silent
    IF %ERRORLEVEL% EQU 0 (
        echo "Upgrade has succeeded." >> C:\Temp\logfile.log
    ) ELSE (
        echo "Upgrade has failed." >> C:\Temp\logfile.log
    )
    GOTO :ENDSCRIPT

:ENDSCRIPT
    echo "End of script." >> C:\Temp\logfile.log


```

### <a name="step-2-create-a-package"></a><span data-ttu-id="7f92b-127">Étape 2 : Création d’un package</span><span class="sxs-lookup"><span data-stu-id="7f92b-127">Step 2: Create a package</span></span>

1. <span data-ttu-id="7f92b-128">Connectez-vous à votre console Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="7f92b-128">Sign in to your Configuration Manager console.</span></span>
2. <span data-ttu-id="7f92b-129">Accédez à **Bibliothèque de logiciels** > **Gestion des applications** > **Packages**.</span><span class="sxs-lookup"><span data-stu-id="7f92b-129">Browse to **Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="7f92b-130">Cliquez avec le bouton droit sur **Packages** et sélectionnez **Créer un package**.</span><span class="sxs-lookup"><span data-stu-id="7f92b-130">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="7f92b-131">Fournissez des valeurs pour le Nom, la Description, le Fabricant, la Langue et la Version.</span><span class="sxs-lookup"><span data-stu-id="7f92b-131">Provide values for the name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="7f92b-132">Cochez la case **Ce package contient des fichiers sources**.</span><span class="sxs-lookup"><span data-stu-id="7f92b-132">Select the **This package contains source files** check box.</span></span>
6. <span data-ttu-id="7f92b-133">Cliquez sur **Parcourir** et sélectionnez le partage réseau où se trouve le programme d’installation (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span><span class="sxs-lookup"><span data-stu-id="7f92b-133">Click **Browse**, and select the network share where the installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span></span>

  ![Capture d’écran de l’assistant Création d’un package et d’un programme](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. <span data-ttu-id="7f92b-135">Dans la page **Choisissez le type de programme que vous voulez créer**, sélectionnez **Programme standard**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7f92b-135">On the **Choose the program type that you want to create** page, select **Standard Program**, and click **Next**.</span></span>

  ![Capture d’écran de l’assistant Création d’un package et d’un programme](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="7f92b-137">Dans la page **Spécifier les informations concernant ce programme standard**, renseignez les entrées suivantes, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7f92b-137">On the **Specify information about this standard program** page, provide the following inputs, and click **Next**.</span></span> <span data-ttu-id="7f92b-138">(Les autres entrées peuvent utiliser leurs valeurs par défaut.)</span><span class="sxs-lookup"><span data-stu-id="7f92b-138">(The other inputs can use their default values.)</span></span>

  | <span data-ttu-id="7f92b-139">**Nom du paramètre**</span><span class="sxs-lookup"><span data-stu-id="7f92b-139">**Parameter name**</span></span> | <span data-ttu-id="7f92b-140">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="7f92b-140">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="7f92b-141">Nom</span><span class="sxs-lookup"><span data-stu-id="7f92b-141">Name</span></span> | <span data-ttu-id="7f92b-142">Installer le service Mobilité de Microsoft Azure (Windows)</span><span class="sxs-lookup"><span data-stu-id="7f92b-142">Install Microsoft Azure Mobility Service (Windows)</span></span> |
  | <span data-ttu-id="7f92b-143">Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="7f92b-143">Command line</span></span> | <span data-ttu-id="7f92b-144">install.bat</span><span class="sxs-lookup"><span data-stu-id="7f92b-144">install.bat</span></span> |
  | <span data-ttu-id="7f92b-145">Le programme peut s’exécuter</span><span class="sxs-lookup"><span data-stu-id="7f92b-145">Program can run</span></span> | <span data-ttu-id="7f92b-146">Qu’un utilisateur ait ouvert une session ou non</span><span class="sxs-lookup"><span data-stu-id="7f92b-146">Whether or not a user is logged on</span></span> |

  ![Capture d’écran de l’assistant Création d’un package et d’un programme](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. <span data-ttu-id="7f92b-148">Dans la page suivante, sélectionnez les systèmes d’exploitation cible.</span><span class="sxs-lookup"><span data-stu-id="7f92b-148">On the next page, select the target operating systems.</span></span> <span data-ttu-id="7f92b-149">Le service Mobilité ne peut être installé que sur Windows Server 2012 R2, Windows Server 2012 et Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="7f92b-149">Mobility Service can be installed only on Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2.</span></span>

  ![Capture d’écran de l’assistant Création d’un package et d’un programme](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png)

10. <span data-ttu-id="7f92b-151">Cliquez deux fois sur **Suivant** pour terminer l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="7f92b-151">To complete the wizard, click **Next** twice.</span></span>


> [!NOTE]
> <span data-ttu-id="7f92b-152">Le script prend en charge les nouvelles installations des Agents du service Mobilité et les mises à jour sur les agents déjà installés.</span><span class="sxs-lookup"><span data-stu-id="7f92b-152">The script supports both new installations of Mobility Service agents and updates to agents that are already installed.</span></span>

### <a name="step-3-deploy-the-package"></a><span data-ttu-id="7f92b-153">Étape 3 : Déploiement du package</span><span class="sxs-lookup"><span data-stu-id="7f92b-153">Step 3: Deploy the package</span></span>
1. <span data-ttu-id="7f92b-154">Dans la console Configuration Manager, cliquez avec le bouton droit sur votre package et sélectionnez **Distribuer du contenu**.</span><span class="sxs-lookup"><span data-stu-id="7f92b-154">In the Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="7f92b-155">![Capture d’écran de la console Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="7f92b-155">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="7f92b-156">Sélectionnez les **[Points de distribution](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** vers lesquels les packages doivent être copiés.</span><span class="sxs-lookup"><span data-stu-id="7f92b-156">Select the **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on to which the packages should be copied.</span></span>
3. <span data-ttu-id="7f92b-157">Terminez l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="7f92b-157">Complete the wizard.</span></span> <span data-ttu-id="7f92b-158">Le package démarre ensuite la réplication sur les points de distribution spécifiés.</span><span class="sxs-lookup"><span data-stu-id="7f92b-158">The package then starts replicating to the specified distribution points.</span></span>
4. <span data-ttu-id="7f92b-159">Une fois la distribution du package terminée, cliquez avec le bouton droit sur le package et sélectionnez **Déployer**.</span><span class="sxs-lookup"><span data-stu-id="7f92b-159">After the package distribution is done, right-click the package, and select **Deploy**.</span></span>
  <span data-ttu-id="7f92b-160">![Capture d’écran de la console Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="7f92b-160">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="7f92b-161">Sélectionnez le regroupement d’appareils Windows Server que vous avez créé dans la section des composants requis en tant que regroupement cible du déploiement.</span><span class="sxs-lookup"><span data-stu-id="7f92b-161">Select the Windows Server device collection you created in the prerequisites section as the target collection for deployment.</span></span>

  ![Capture d’écran de l’assistant Déploiement du logiciel](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. <span data-ttu-id="7f92b-163">Dans la page **Spécifier la destination du contenu**, sélectionnez vos **Points de distribution**.</span><span class="sxs-lookup"><span data-stu-id="7f92b-163">On the **Specify the content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="7f92b-164">Dans la page **Spécifier un paramètre pour contrôler la manière dont ce logiciel est déployé**, vérifiez que l’objectif est **Requis**.</span><span class="sxs-lookup"><span data-stu-id="7f92b-164">On the **Specify settings to control how this software is deployed** page, ensure that the purpose is **Required**.</span></span>

  ![Capture d’écran de l’assistant Déploiement du logiciel](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="7f92b-166">Spécifiez une planification sur la page **Spécifier la planification de ce déploiement**.</span><span class="sxs-lookup"><span data-stu-id="7f92b-166">On the **Specify the schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="7f92b-167">Pour plus d’informations, consultez [Planification de packages](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f92b-167">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="7f92b-168">Sur la page **Points de distribution**, configurez les propriétés selon les besoins de votre centre de données.</span><span class="sxs-lookup"><span data-stu-id="7f92b-168">On the **Distribution Points** page, configure the properties according to the needs of your datacenter.</span></span> <span data-ttu-id="7f92b-169">Terminez ensuite l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="7f92b-169">Then complete the wizard.</span></span>

> [!TIP]
> <span data-ttu-id="7f92b-170">Pour éviter les redémarrages inutiles, planifiez l’installation du package pendant votre fenêtre de maintenance mensuelle ou votre fenêtre de mises à jour logicielles.</span><span class="sxs-lookup"><span data-stu-id="7f92b-170">To avoid unnecessary reboots, schedule the package installation during your monthly maintenance window or software updates window.</span></span>

<span data-ttu-id="7f92b-171">Vous pouvez surveiller la progression du déploiement à l’aide de la console Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="7f92b-171">You can monitor the deployment progress by using the Configuration Manager console.</span></span> <span data-ttu-id="7f92b-172">Accédez à **Surveillance** > **Déploiements** > *[nom de votre package]*.</span><span class="sxs-lookup"><span data-stu-id="7f92b-172">Go to **Monitoring** > **Deployments** > *[your package name]*.</span></span>

  ![Capture d’écran de l’option de Configuration Manager pour contrôler les déploiements](./media/site-recovery-install-mobility-service-using-sccm/report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a><span data-ttu-id="7f92b-174">Déploiement du service Mobilité sur des ordinateurs exécutant Linux</span><span class="sxs-lookup"><span data-stu-id="7f92b-174">Deploy Mobility Service on computers running Linux</span></span>
> [!NOTE]
> <span data-ttu-id="7f92b-175">Cet article part du principe que l’adresse IP du serveur de configuration est 192.168.3.121, et que le partage de fichiers réseau sécurisé est \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="7f92b-175">This article assumes that the IP address of the configuration server is 192.168.3.121, and that the secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="7f92b-176">Étape 1 : Préparation du déploiement</span><span class="sxs-lookup"><span data-stu-id="7f92b-176">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="7f92b-177">Créez un dossier sur le partage réseau et nommez-le **MobSvcLinux**.</span><span class="sxs-lookup"><span data-stu-id="7f92b-177">Create a folder on the network share, and name it as **MobSvcLinux**.</span></span>
2. <span data-ttu-id="7f92b-178">Ouvrez une session sur votre serveur de configuration et ouvrez une invite de commandes d’administration.</span><span class="sxs-lookup"><span data-stu-id="7f92b-178">Sign in to your configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="7f92b-179">Exécutez les commandes suivantes pour générer un fichier de phrase secrète :</span><span class="sxs-lookup"><span data-stu-id="7f92b-179">Run the following commands to generate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="7f92b-180">Copiez le fichier **MobSvc.passphrase** dans le dossier **MobSvcLinux** sur le partage réseau.</span><span class="sxs-lookup"><span data-stu-id="7f92b-180">Copy the **MobSvc.passphrase** file into the **MobSvcLinux** folder on your network share.</span></span>
5. <span data-ttu-id="7f92b-181">Naviguez jusqu’au référentiel du programme d’installation sur le serveur de configuration en exécutant la commande :</span><span class="sxs-lookup"><span data-stu-id="7f92b-181">Browse to the installer repository on the configuration server by running the command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="7f92b-182">Copiez les fichiers suivants dans le dossier **MobSvcLinux** sur le partage réseau :</span><span class="sxs-lookup"><span data-stu-id="7f92b-182">Copy the following files to the **MobSvcLinux** folder on your network share:</span></span>
   * <span data-ttu-id="7f92b-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="7f92b-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>
   * <span data-ttu-id="7f92b-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="7f92b-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span>
   * <span data-ttu-id="7f92b-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="7f92b-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>
   * <span data-ttu-id="7f92b-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="7f92b-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>
   * <span data-ttu-id="7f92b-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="7f92b-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span>
   * <span data-ttu-id="7f92b-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="7f92b-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span>


7. <span data-ttu-id="7f92b-189">Copiez le code suivant et enregistrez-le en tant que **install_linux.sh** dans le dossier **MobSvcLinux**.</span><span class="sxs-lookup"><span data-stu-id="7f92b-189">Copy the following code, and save it as **install_linux.sh** into the **MobSvcLinux** folder.</span></span>
   > [!NOTE]
   > <span data-ttu-id="7f92b-190">Remplacez les espaces réservés [CSIP] dans le script ci-dessous par les valeurs réelles de l’adresse IP de votre serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="7f92b-190">Replace the [CSIP] placeholders in this script with the actual values of the IP address of your configuration server.</span></span>

```Bash
#!/usr/bin/env bash

rm -rf /tmp/MobSvc
mkdir -p /tmp/MobSvc
INSTALL_DIR='/usr/local/ASR'
VX_VERSION_FILE='/usr/local/.vx_version'

echo "=============================" >> /tmp/MobSvc/sccm.log
echo `date` >> /tmp/MobSvc/sccm.log
echo "=============================" >> /tmp/MobSvc/sccm.log

if [ -f /etc/oracle-release ] && [ -f /etc/redhat-release ]; then
    if grep -q 'Oracle Linux Server release 6.*' /etc/oracle-release; then
        if uname -a | grep -q x86_64; then
            OS="OL6-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *OL6*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/redhat-release ]; then
    if grep -q 'Red Hat Enterprise Linux Server release 6.* (Santiago)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 6.* (Final)' /etc/redhat-release || \
        grep -q 'CentOS release 6.* (Final)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL6-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *RHEL6*.tar.gz /tmp/MobSvc
        fi
    elif grep -q 'Red Hat Enterprise Linux Server release 7.* (Maipo)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 7.* (Core)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL7-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *RHEL7*.tar.gz /tmp/MobSvc
                fi
    fi
elif [ -f /etc/SuSE-release ] && grep -q 'VERSION = 11' /etc/SuSE-release; then
    if grep -q "SUSE Linux Enterprise Server 11" /etc/SuSE-release && grep -q 'PATCHLEVEL = 3' /etc/SuSE-release; then
        if uname -a | grep -q x86_64; then
            OS="SLES11-SP3-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *SLES11-SP3*.tar.gz /tmp/MobSvc
        fi
    elif grep -q "SUSE Linux Enterprise Server 11" /etc/SuSE-release && grep -q 'PATCHLEVEL = 4' /etc/SuSE-release; then
        if uname -a | grep -q x86_64; then
            OS="SLES11-SP4-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *SLES11-SP4*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/lsb-release ] ; then
    if grep -q 'DISTRIB_RELEASE=14.04' /etc/lsb-release ; then
       if uname -a | grep -q x86_64; then
           OS="UBUNTU-14.04-64"
           echo $OS >> /tmp/MobSvc/sccm.log
           cp *UBUNTU-14*.tar.gz /tmp/MobSvc
       fi
    fi
else
    exit 1
fi

if [ -z "$OS" ]; then
    exit 1
fi

Install()
{
    echo "Perform Installation." >> /tmp/MobSvc/sccm.log
    ./install -q -d ${INSTALL_DIR} -r MS -v VmWare
    RET_VAL=$?
    echo "Installation Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Installation has succeeded. Proceed to configuration." >> /tmp/MobSvc/sccm.log
        Configure
    else
        echo "Installation has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

Configure()
{
    echo "Perform configuration." >> /tmp/MobSvc/sccm.log
    ${INSTALL_DIR}/Vx/bin/UnifiedAgentConfigurator.sh -i [CSIP] -P MobSvc.passphrase
    RET_VAL=$?
    echo "Configuration Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Configuration has succeeded." >> /tmp/MobSvc/sccm.log
    else
        echo "Configuration has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

Upgrade()
{
    echo "Perform Upgrade." >> /tmp/MobSvc/sccm.log
    ./install -q -v VmWare
    RET_VAL=$?
    echo "Upgrade Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Upgrade has succeeded." >> /tmp/MobSvc/sccm.log
    else
        echo "Upgrade has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

cp MobSvc.passphrase /tmp/MobSvc
cd /tmp/MobSvc

tar -zxvf *.tar.gz

if [ -e ${VX_VERSION_FILE} ]; then
    echo "${VX_VERSION_FILE} exists. Checking for configuration status." >> /tmp/MobSvc/sccm.log
    agent_configuration=$(grep ^AGENT_CONFIGURATION_STATUS "${VX_VERSION_FILE}" | cut -d"=" -f2 | tr -d " ")
    echo "agent_configuration=$agent_configuration" >> /tmp/MobSvc/sccm.log
     if [ "$agent_configuration" == "Succeeded" ]; then
        echo "Agent is already configured. Proceed to Upgrade." >> /tmp/MobSvc/sccm.log
        Upgrade
    else
        echo "Agent is not configured. Proceed to Configure." >> /tmp/MobSvc/sccm.log
        Configure
    fi
else
    Install
fi

cd /tmp

```

### <a name="step-2-create-a-package"></a><span data-ttu-id="7f92b-191">Étape 2 : Création d’un package</span><span class="sxs-lookup"><span data-stu-id="7f92b-191">Step 2: Create a package</span></span>

1. <span data-ttu-id="7f92b-192">Connectez-vous à votre console Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="7f92b-192">Sign in  to your Configuration Manager console.</span></span>
2. <span data-ttu-id="7f92b-193">Accédez à **Bibliothèque de logiciels** > **Gestion des applications** > **Packages**.</span><span class="sxs-lookup"><span data-stu-id="7f92b-193">Browse to **Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="7f92b-194">Cliquez avec le bouton droit sur **Packages** et sélectionnez **Créer un package**.</span><span class="sxs-lookup"><span data-stu-id="7f92b-194">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="7f92b-195">Fournissez des valeurs pour le Nom, la Description, le Fabricant, la Langue et la Version.</span><span class="sxs-lookup"><span data-stu-id="7f92b-195">Provide values for the name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="7f92b-196">Cochez la case **Ce package contient des fichiers sources**.</span><span class="sxs-lookup"><span data-stu-id="7f92b-196">Select the **This package contains source files** check box.</span></span>
6. <span data-ttu-id="7f92b-197">Cliquez sur **Parcourir** et sélectionnez le partage réseau où se trouve le programme d’installation (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="7f92b-197">Click **Browse**, and select the network share where the installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span></span>

  ![Capture d’écran de l’assistant Création d’un package et d’un programme](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. <span data-ttu-id="7f92b-199">Dans la page **Choisissez le type de programme que vous voulez créer**, sélectionnez **Programme standard**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7f92b-199">On the **Choose the program type that you want to create** page, select **Standard Program**, and click **Next**.</span></span>

  ![Capture d’écran de l’assistant Création d’un package et d’un programme](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="7f92b-201">Dans la page **Spécifier les informations concernant ce programme standard**, renseignez les entrées suivantes, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7f92b-201">On the **Specify information about this standard program** page, provide the following inputs, and click **Next**.</span></span> <span data-ttu-id="7f92b-202">(Les autres entrées peuvent utiliser leurs valeurs par défaut.)</span><span class="sxs-lookup"><span data-stu-id="7f92b-202">(The other inputs can use their default values.)</span></span>

    | <span data-ttu-id="7f92b-203">**Nom du paramètre**</span><span class="sxs-lookup"><span data-stu-id="7f92b-203">**Parameter name**</span></span> | <span data-ttu-id="7f92b-204">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="7f92b-204">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="7f92b-205">Nom</span><span class="sxs-lookup"><span data-stu-id="7f92b-205">Name</span></span> | <span data-ttu-id="7f92b-206">Installer le service Mobilité de Microsoft Azure (Linux)</span><span class="sxs-lookup"><span data-stu-id="7f92b-206">Install Microsoft Azure Mobility Service (Linux)</span></span> |
  | <span data-ttu-id="7f92b-207">Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="7f92b-207">Command line</span></span> | <span data-ttu-id="7f92b-208">./install_linux.sh</span><span class="sxs-lookup"><span data-stu-id="7f92b-208">./install_linux.sh</span></span> |
  | <span data-ttu-id="7f92b-209">Le programme peut s’exécuter</span><span class="sxs-lookup"><span data-stu-id="7f92b-209">Program can run</span></span> | <span data-ttu-id="7f92b-210">Qu’un utilisateur ait ouvert une session ou non</span><span class="sxs-lookup"><span data-stu-id="7f92b-210">Whether or not a user is logged on</span></span> |

  ![Capture d’écran de l’assistant Création d’un package et d’un programme](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. <span data-ttu-id="7f92b-212">Sur la page suivante, sélectionnez **Ce programme peut être exécuté sur n'importe quelle plateforme**.</span><span class="sxs-lookup"><span data-stu-id="7f92b-212">On the next page, select **This program can run on any platform**.</span></span>
  <span data-ttu-id="7f92b-213">![Capture d’écran de l’assistant Création d’un package et d’un programme](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span><span class="sxs-lookup"><span data-stu-id="7f92b-213">![Screenshot of Create Package and Program wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span></span>

10. <span data-ttu-id="7f92b-214">Cliquez deux fois sur **Suivant** pour terminer l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="7f92b-214">To complete the wizard, click **Next** twice.</span></span>

> [!NOTE]
> <span data-ttu-id="7f92b-215">Le script prend en charge les nouvelles installations des Agents du service Mobilité et les mises à jour sur les agents déjà installés.</span><span class="sxs-lookup"><span data-stu-id="7f92b-215">The script supports both new installations of Mobility Service agents and updates to agents that are already installed.</span></span>

### <a name="step-3-deploy-the-package"></a><span data-ttu-id="7f92b-216">Étape 3 : Déploiement du package</span><span class="sxs-lookup"><span data-stu-id="7f92b-216">Step 3: Deploy the package</span></span>
1. <span data-ttu-id="7f92b-217">Dans la console Configuration Manager, cliquez avec le bouton droit sur votre package et sélectionnez **Distribuer du contenu**.</span><span class="sxs-lookup"><span data-stu-id="7f92b-217">In the Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="7f92b-218">![Capture d’écran de la console Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="7f92b-218">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="7f92b-219">Sélectionnez les **[Points de distribution](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** vers lesquels les packages doivent être copiés.</span><span class="sxs-lookup"><span data-stu-id="7f92b-219">Select the **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on to which the packages should be copied.</span></span>
3. <span data-ttu-id="7f92b-220">Terminez l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="7f92b-220">Complete the wizard.</span></span> <span data-ttu-id="7f92b-221">Le package démarre ensuite la réplication sur les points de distribution spécifiés.</span><span class="sxs-lookup"><span data-stu-id="7f92b-221">The package then starts replicating to the specified distribution points.</span></span>
4. <span data-ttu-id="7f92b-222">Une fois la distribution du package terminée, cliquez avec le bouton droit sur le package et sélectionnez **Déployer**.</span><span class="sxs-lookup"><span data-stu-id="7f92b-222">After the package distribution is done, right-click the package, and select **Deploy**.</span></span>
  <span data-ttu-id="7f92b-223">![Capture d’écran de la console Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="7f92b-223">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="7f92b-224">Sélectionnez le regroupement d’appareils Linux Server que vous avez créé dans la section Conditions préalables en tant que regroupement cible du déploiement.</span><span class="sxs-lookup"><span data-stu-id="7f92b-224">Select the Linux Server device collection you created in the prerequisites section as the target collection for deployment.</span></span>

  ![Capture d’écran de l’assistant Déploiement du logiciel](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. <span data-ttu-id="7f92b-226">Dans la page **Spécifier la destination du contenu**, sélectionnez vos **Points de distribution**.</span><span class="sxs-lookup"><span data-stu-id="7f92b-226">On the **Specify the content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="7f92b-227">Dans la page **Spécifier un paramètre pour contrôler la manière dont ce logiciel est déployé**, vérifiez que l’objectif est **Requis**.</span><span class="sxs-lookup"><span data-stu-id="7f92b-227">On the **Specify settings to control how this software is deployed** page, ensure that the purpose is **Required**.</span></span>

  ![Capture d’écran de l’assistant Déploiement du logiciel](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="7f92b-229">Spécifiez une planification sur la page **Spécifier la planification de ce déploiement**.</span><span class="sxs-lookup"><span data-stu-id="7f92b-229">On the **Specify the schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="7f92b-230">Pour plus d’informations, consultez [Planification de packages](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f92b-230">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="7f92b-231">Sur la page **Points de distribution**, configurez les propriétés selon les besoins de votre centre de données.</span><span class="sxs-lookup"><span data-stu-id="7f92b-231">On the **Distribution Points** page, configure the properties according to the needs of your datacenter.</span></span> <span data-ttu-id="7f92b-232">Terminez ensuite l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="7f92b-232">Then complete the wizard.</span></span>

<span data-ttu-id="7f92b-233">Le service Mobilité est installé sur le regroupement d’appareils Linux Server conformément à la planification configurée.</span><span class="sxs-lookup"><span data-stu-id="7f92b-233">Mobility Service gets installed on the Linux Server Device Collection, according to the schedule you configured.</span></span>

## <a name="other-methods-to-install-mobility-service"></a><span data-ttu-id="7f92b-234">Autres méthodes d’installation des services Mobilité</span><span class="sxs-lookup"><span data-stu-id="7f92b-234">Other methods to install Mobility Service</span></span>
<span data-ttu-id="7f92b-235">Voici d’autres options pour l’installation du service Mobilité :</span><span class="sxs-lookup"><span data-stu-id="7f92b-235">Here are some other options for installing Mobility Service:</span></span>
* [<span data-ttu-id="7f92b-236">Installation manuelle à l’aide de l’interface utilisateur graphique</span><span class="sxs-lookup"><span data-stu-id="7f92b-236">Manual Installation using GUI</span></span>](http://aka.ms/mobsvcmanualinstall)
* [<span data-ttu-id="7f92b-237">Installation manuelle à l’aide de la ligne de commande</span><span class="sxs-lookup"><span data-stu-id="7f92b-237">Manual Installation using command-line</span></span>](http://aka.ms/mobsvcmanualinstallcli)
* [<span data-ttu-id="7f92b-238">Installation Push à l’aide du serveur de configuration</span><span class="sxs-lookup"><span data-stu-id="7f92b-238">Push Installation using configuration server </span></span>](http://aka.ms/pushinstall)
* [<span data-ttu-id="7f92b-239">Installation automatisée à l’aide d’Azure Automation et de la Configuration de l’état souhaité</span><span class="sxs-lookup"><span data-stu-id="7f92b-239">Automated Installation using Azure Automation & Desired State Configuration </span></span>](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a><span data-ttu-id="7f92b-240">Désinstaller le service Mobilité</span><span class="sxs-lookup"><span data-stu-id="7f92b-240">Uninstall Mobility Service</span></span>
<span data-ttu-id="7f92b-241">Vous pouvez créer des packages Configuration Manager pour désinstaller le service Mobilité.</span><span class="sxs-lookup"><span data-stu-id="7f92b-241">You can create Configuration Manager packages to uninstall Mobility Service.</span></span> <span data-ttu-id="7f92b-242">Pour ce faire, utilisez le script suivant :</span><span class="sxs-lookup"><span data-stu-id="7f92b-242">Use the following script to do so:</span></span>

```
Time /t >> C:\logfile.log
REM ==================================================
REM ==== Check if Mob Svc is already installed =======
REM ==== If not installed no operation required ========
REM ==== Else run uninstall command =====================
REM ==== {275197FC-14FD-4560-A5EB-38217F80CBD1} is ====
REM ==== guid for Mob Svc Installer ====================
whoami >> C:\logfile.log
NET START | FIND "InMage Scout Application Service"
IF  %ERRORLEVEL% EQU 1 (GOTO :INSTALL) ELSE GOTO :UNINSTALL
:NOOPERATION
                echo "No Operation Required." >> c:\logfile.log
                GOTO :ENDSCRIPT
:UNINSTALL
                echo "Uninstall" >> C:\logfile.log
                MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
:ENDSCRIPT

```

## <a name="next-steps"></a><span data-ttu-id="7f92b-243">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7f92b-243">Next steps</span></span>
<span data-ttu-id="7f92b-244">Vous êtes désormais prêt à [activer la protection](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) de vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="7f92b-244">You are now ready to [enable protection](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) for your virtual machines.</span></span>
