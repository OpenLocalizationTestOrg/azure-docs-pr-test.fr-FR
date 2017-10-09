---
title: "installation du Service mobilité pour Azure Site Recovery à l’aide des outils de déploiement de logiciels d’aaaAutomate | Documents Microsoft"
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
ms.openlocfilehash: 6c883c6d5308dcec6e0628b0c2196b3a12e08ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a><span data-ttu-id="fbdd1-103">Automatisation de l’installation du service Mobilité à l’aide d’outils de déploiement de logiciels</span><span class="sxs-lookup"><span data-stu-id="fbdd1-103">Automate Mobility Service installation by using software deployment tools</span></span>

>[!IMPORTANT]
<span data-ttu-id="fbdd1-104">Ce document part du principe que vous utilisez la version **9.9.4510.1** ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-104">This document assumes you are using version **9.9.4510.1** or higher.</span></span>

<span data-ttu-id="fbdd1-105">Cet article fournit un exemple de la façon dont vous pouvez utiliser System Center Configuration Manager toodeploy hello Service de mobilité d’Azure Site Recovery dans votre centre de données.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-105">This article provides you an example of how you can use System Center Configuration Manager toodeploy hello Azure Site Recovery Mobility Service in your datacenter.</span></span> <span data-ttu-id="fbdd1-106">À l’aide d’un outil de déploiement de logiciel tel que le Gestionnaire de Configuration a hello suivant avantages :</span><span class="sxs-lookup"><span data-stu-id="fbdd1-106">Using a software deployment tool like Configuration Manager has hello following advantages:</span></span>
* <span data-ttu-id="fbdd1-107">Planification du déploiement (nouvelles installations et mises à niveau) pendant votre fenêtre de maintenance planifiée pour les mises à jour logicielles</span><span class="sxs-lookup"><span data-stu-id="fbdd1-107">Scheduling deployment of fresh installations and upgrades, during your planned maintenance window for software updates</span></span>
* <span data-ttu-id="fbdd1-108">Mise à l’échelle toohundreds de déploiement de serveurs simultanément</span><span class="sxs-lookup"><span data-stu-id="fbdd1-108">Scaling deployment toohundreds of servers simultaneously</span></span>


> [!NOTE]
> <span data-ttu-id="fbdd1-109">Cet article utilise l’activité de déploiement de System Center Configuration Manager 2012 R2 toodemonstrate hello.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-109">This article uses System Center Configuration Manager 2012 R2 toodemonstrate hello deployment activity.</span></span> <span data-ttu-id="fbdd1-110">Vous pouvez également automatiser l’installation du service Mobilité à l’aide [d’Azure Automation et de la Configuration de l’état souhaité](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="fbdd1-110">You could also automate Mobility Service installation by using [Azure Automation and Desired State Configuration](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbdd1-111">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="fbdd1-111">Prerequisites</span></span>
1. <span data-ttu-id="fbdd1-112">Un outil de déploiement de logiciels tel que Configuration Manager qui est déjà déployé dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-112">A software deployment tool, like Configuration Manager, that is already deployed in your environment.</span></span>
  <span data-ttu-id="fbdd1-113">Créez deux [regroupements de périphériques](https://technet.microsoft.com/library/gg682169.aspx), un pour tous les **serveurs Windows**et l’autre pour toutes les **des serveurs Linux**, que vous souhaitez tooprotect à l’aide de récupération de Site.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-113">Create two [device collections](https://technet.microsoft.com/library/gg682169.aspx), one for all **Windows servers**, and another for all **Linux servers**, that you want tooprotect by using Site Recovery.</span></span>
3. <span data-ttu-id="fbdd1-114">Un serveur de configuration qui est déjà inscrit auprès Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-114">A configuration server that is already registered with Site Recovery.</span></span>
4. <span data-ttu-id="fbdd1-115">Un réseau sécurisé partage de fichiers (partage Server Message Block) qui sont accessibles par le serveur de Configuration Manager hello.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-115">A secure network file share (Server Message Block share) that can be accessed by hello Configuration Manager server.</span></span>

## <a name="deploy-mobility-service-on-computers-running-windows"></a><span data-ttu-id="fbdd1-116">Déploiement du service Mobilité sur des ordinateurs exécutant Windows</span><span class="sxs-lookup"><span data-stu-id="fbdd1-116">Deploy Mobility Service on computers running Windows</span></span>
> [!NOTE]
> <span data-ttu-id="fbdd1-117">Cet article suppose qu’adresse hello hello du serveur de configuration est 192.168.3.121, et que ce partage de fichiers réseau sécurisé hello est \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-117">This article assumes that hello IP address of hello configuration server is 192.168.3.121, and that hello secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="fbdd1-118">Étape 1 : Préparation du déploiement</span><span class="sxs-lookup"><span data-stu-id="fbdd1-118">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="fbdd1-119">Créez un dossier sur un partage de réseau hello et nommez-le **MobSvcWindows**.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-119">Create a folder on hello network share, and name it **MobSvcWindows**.</span></span>
2. <span data-ttu-id="fbdd1-120">Connectez-vous au serveur de configuration tooyour et ouvrez une invite de commandes d’administration.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-120">Sign in tooyour configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="fbdd1-121">Exécutez hello suivant de commandes toogenerate un fichier de mot de passe :</span><span class="sxs-lookup"><span data-stu-id="fbdd1-121">Run hello following commands toogenerate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="fbdd1-122">Hello de copie **MobSvc.passphrase** fichier hello **MobSvcWindows** dossier sur votre partage réseau.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-122">Copy hello **MobSvc.passphrase** file into hello **MobSvcWindows** folder on your network share.</span></span>
5. <span data-ttu-id="fbdd1-123">Parcourir le référentiel du programme d’installation toohello sur le serveur de configuration hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="fbdd1-123">Browse toohello installer repository on hello configuration server by running hello following command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="fbdd1-124">Hello de copie  **Microsoft ASR\_UA\_*version*\_Windows\_GA\_*date* \_ Release.exe** toohello **MobSvcWindows** dossier sur votre partage réseau.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-124">Copy hello **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe** toohello **MobSvcWindows** folder on your network share.</span></span>
7. <span data-ttu-id="fbdd1-125">Copier hello suivant de code et l’enregistrer en tant que **install.bat** dans hello **MobSvcWindows** dossier.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-125">Copy hello following code, and save it as **install.bat** into hello **MobSvcWindows** folder.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fbdd1-126">Remplacez les espaces réservés de hello [CSIP] dans ce script avec des valeurs réelles de hello d’adresse IP de hello de votre serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-126">Replace hello [CSIP] placeholders in this script with hello actual values of hello IP address of your configuration server.</span></span>

```DOS
Time /t >> C:\Temp\logfile.log
REM ==================================================
REM ==== Clean up hello folders ========================
RMDIR /S /q %temp%\MobSvc
MKDIR %Temp%\MobSvc
MKDIR C:\Temp
REM ==================================================

REM ==== Copy new files ==============================
COPY M*.* %Temp%\MobSvc
CD %Temp%\MobSvc
REN Micro*.exe MobSvcInstaller.exe
REM ==================================================

REM ==== Extract hello installer =======================
MobSvcInstaller.exe /q /x:%Temp%\MobSvc\Extracted
REM ==== Wait 10s for extraction toocomplete =========
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

### <a name="step-2-create-a-package"></a><span data-ttu-id="fbdd1-127">Étape 2 : Création d’un package</span><span class="sxs-lookup"><span data-stu-id="fbdd1-127">Step 2: Create a package</span></span>

1. <span data-ttu-id="fbdd1-128">Se connecter dans la console Configuration Manager tooyour.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-128">Sign in tooyour Configuration Manager console.</span></span>
2. <span data-ttu-id="fbdd1-129">Parcourir trop**bibliothèque de logiciels** > **gestion des applications** > **Packages**.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-129">Browse too**Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="fbdd1-130">Cliquez avec le bouton droit sur **Packages** et sélectionnez **Créer un package**.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-130">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="fbdd1-131">Fournir des valeurs pour la version, la description, fabricant, langue et nom de hello.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-131">Provide values for hello name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="fbdd1-132">Sélectionnez hello **ce package contient des fichiers sources** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-132">Select hello **This package contains source files** check box.</span></span>
6. <span data-ttu-id="fbdd1-133">Cliquez sur **Parcourir**et sélectionnez hello partage de réseau où se trouve le programme d’installation de hello (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span><span class="sxs-lookup"><span data-stu-id="fbdd1-133">Click **Browse**, and select hello network share where hello installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span></span>

  ![Capture d’écran de l’assistant Création d’un package et d’un programme](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. <span data-ttu-id="fbdd1-135">Sur hello **type de programme hello choisir que vous souhaitez toocreate** page, sélectionnez **programme Standard**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-135">On hello **Choose hello program type that you want toocreate** page, select **Standard Program**, and click **Next**.</span></span>

  ![Capture d’écran de l’assistant Création d’un package et d’un programme](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="fbdd1-137">Sur hello **spécifier des informations sur ce programme standard** page, fournissez hello suivant des entrées, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-137">On hello **Specify information about this standard program** page, provide hello following inputs, and click **Next**.</span></span> <span data-ttu-id="fbdd1-138">(hello autres entrées peuvent utiliser leurs valeurs par défaut.)</span><span class="sxs-lookup"><span data-stu-id="fbdd1-138">(hello other inputs can use their default values.)</span></span>

  | <span data-ttu-id="fbdd1-139">**Nom du paramètre**</span><span class="sxs-lookup"><span data-stu-id="fbdd1-139">**Parameter name**</span></span> | <span data-ttu-id="fbdd1-140">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="fbdd1-140">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="fbdd1-141">Nom</span><span class="sxs-lookup"><span data-stu-id="fbdd1-141">Name</span></span> | <span data-ttu-id="fbdd1-142">Installer le service Mobilité de Microsoft Azure (Windows)</span><span class="sxs-lookup"><span data-stu-id="fbdd1-142">Install Microsoft Azure Mobility Service (Windows)</span></span> |
  | <span data-ttu-id="fbdd1-143">Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="fbdd1-143">Command line</span></span> | <span data-ttu-id="fbdd1-144">install.bat</span><span class="sxs-lookup"><span data-stu-id="fbdd1-144">install.bat</span></span> |
  | <span data-ttu-id="fbdd1-145">Le programme peut s’exécuter</span><span class="sxs-lookup"><span data-stu-id="fbdd1-145">Program can run</span></span> | <span data-ttu-id="fbdd1-146">Qu’un utilisateur ait ouvert une session ou non</span><span class="sxs-lookup"><span data-stu-id="fbdd1-146">Whether or not a user is logged on</span></span> |

  ![Capture d’écran de l’assistant Création d’un package et d’un programme](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. <span data-ttu-id="fbdd1-148">Sur la page suivante de hello, sélectionnez les systèmes d’exploitation cible hello.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-148">On hello next page, select hello target operating systems.</span></span> <span data-ttu-id="fbdd1-149">Le service Mobilité ne peut être installé que sur Windows Server 2012 R2, Windows Server 2012 et Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-149">Mobility Service can be installed only on Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2.</span></span>

  ![Capture d’écran de l’assistant Création d’un package et d’un programme](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png)

10. <span data-ttu-id="fbdd1-151">Assistant de hello toocomplete, cliquez sur **suivant** à deux reprises.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-151">toocomplete hello wizard, click **Next** twice.</span></span>


> [!NOTE]
> <span data-ttu-id="fbdd1-152">script de Hello prend en charge les nouvelles installations d’agents de Service mobilité et met à jour tooagents qui sont déjà installés.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-152">hello script supports both new installations of Mobility Service agents and updates tooagents that are already installed.</span></span>

### <a name="step-3-deploy-hello-package"></a><span data-ttu-id="fbdd1-153">Étape 3 : Déployer le package de hello</span><span class="sxs-lookup"><span data-stu-id="fbdd1-153">Step 3: Deploy hello package</span></span>
1. <span data-ttu-id="fbdd1-154">Dans la console Configuration Manager hello, avec le bouton droit de votre package, puis sélectionnez **distribuer du contenu**.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-154">In hello Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="fbdd1-155">![Capture d’écran de la console Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="fbdd1-155">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="fbdd1-156">Sélectionnez hello  **[les points de distribution](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  sur toowhich les packages hello doivent être copiés.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-156">Select hello **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on toowhich hello packages should be copied.</span></span>
3. <span data-ttu-id="fbdd1-157">Assistant hello terminée.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-157">Complete hello wizard.</span></span> <span data-ttu-id="fbdd1-158">package de Hello puis le démarrage de la réplication toohello spécifié de points de distribution.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-158">hello package then starts replicating toohello specified distribution points.</span></span>
4. <span data-ttu-id="fbdd1-159">Une fois que la distribution de package hello est terminée, cliquez sur le package de hello, puis sélectionnez **déployer**.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-159">After hello package distribution is done, right-click hello package, and select **Deploy**.</span></span>
  <span data-ttu-id="fbdd1-160">![Capture d’écran de la console Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="fbdd1-160">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="fbdd1-161">Sélectionnez le regroupement de périphériques Windows Server hello que vous avez créé dans la section conditions préalables de hello en tant que regroupement cible de hello pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-161">Select hello Windows Server device collection you created in hello prerequisites section as hello target collection for deployment.</span></span>

  ![Capture d’écran de l’assistant Déploiement du logiciel](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. <span data-ttu-id="fbdd1-163">Sur hello **spécifier la destination de contenu hello** page, sélectionnez votre **les Points de Distribution**.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-163">On hello **Specify hello content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="fbdd1-164">Sur hello **toocontrol de paramètres de spécifier comment ce logiciel est déployé** , vérifiez que hello vise **requis**.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-164">On hello **Specify settings toocontrol how this software is deployed** page, ensure that hello purpose is **Required**.</span></span>

  ![Capture d’écran de l’assistant Déploiement du logiciel](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="fbdd1-166">Sur hello **spécifier la planification pour ce déploiement hello** , spécifiez une planification.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-166">On hello **Specify hello schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="fbdd1-167">Pour plus d’informations, consultez [Planification de packages](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="fbdd1-167">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="fbdd1-168">Sur hello **les Points de Distribution** page, configurez les propriétés de hello selon les besoins de toohello de votre centre de données.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-168">On hello **Distribution Points** page, configure hello properties according toohello needs of your datacenter.</span></span> <span data-ttu-id="fbdd1-169">Puis terminer hello.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-169">Then complete hello wizard.</span></span>

> [!TIP]
> <span data-ttu-id="fbdd1-170">tooavoid inutile a redémarré, planifier l’installation package hello pendant votre fenêtre de maintenance mensuelle ou d’une fenêtre de mises à jour logicielles.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-170">tooavoid unnecessary reboots, schedule hello package installation during your monthly maintenance window or software updates window.</span></span>

<span data-ttu-id="fbdd1-171">Vous pouvez surveiller la progression du déploiement hello en utilisant la console de Configuration Manager hello.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-171">You can monitor hello deployment progress by using hello Configuration Manager console.</span></span> <span data-ttu-id="fbdd1-172">Accédez trop**analyse** > **déploiements** > *[nom de votre package]*.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-172">Go too**Monitoring** > **Deployments** > *[your package name]*.</span></span>

  ![Déploiements de toomonitor option de capture d’écran de Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a><span data-ttu-id="fbdd1-174">Déploiement du service Mobilité sur des ordinateurs exécutant Linux</span><span class="sxs-lookup"><span data-stu-id="fbdd1-174">Deploy Mobility Service on computers running Linux</span></span>
> [!NOTE]
> <span data-ttu-id="fbdd1-175">Cet article suppose qu’adresse hello hello du serveur de configuration est 192.168.3.121, et que ce partage de fichiers réseau sécurisé hello est \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-175">This article assumes that hello IP address of hello configuration server is 192.168.3.121, and that hello secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="fbdd1-176">Étape 1 : Préparation du déploiement</span><span class="sxs-lookup"><span data-stu-id="fbdd1-176">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="fbdd1-177">Créez un dossier sur un partage de réseau hello et nommez-le en tant que **MobSvcLinux**.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-177">Create a folder on hello network share, and name it as **MobSvcLinux**.</span></span>
2. <span data-ttu-id="fbdd1-178">Connectez-vous au serveur de configuration tooyour et ouvrez une invite de commandes d’administration.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-178">Sign in tooyour configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="fbdd1-179">Exécutez hello suivant de commandes toogenerate un fichier de mot de passe :</span><span class="sxs-lookup"><span data-stu-id="fbdd1-179">Run hello following commands toogenerate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="fbdd1-180">Hello de copie **MobSvc.passphrase** fichier hello **MobSvcLinux** dossier sur votre partage réseau.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-180">Copy hello **MobSvc.passphrase** file into hello **MobSvcLinux** folder on your network share.</span></span>
5. <span data-ttu-id="fbdd1-181">Parcourir le référentiel du programme d’installation toohello sur le serveur de configuration hello en exécutant la commande hello :</span><span class="sxs-lookup"><span data-stu-id="fbdd1-181">Browse toohello installer repository on hello configuration server by running hello command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="fbdd1-182">Suit hello de copie des fichiers toohello **MobSvcLinux** dossier sur votre partage réseau :</span><span class="sxs-lookup"><span data-stu-id="fbdd1-182">Copy hello following files toohello **MobSvcLinux** folder on your network share:</span></span>
   * <span data-ttu-id="fbdd1-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="fbdd1-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>
   * <span data-ttu-id="fbdd1-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="fbdd1-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span>
   * <span data-ttu-id="fbdd1-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="fbdd1-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>
   * <span data-ttu-id="fbdd1-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="fbdd1-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>
   * <span data-ttu-id="fbdd1-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="fbdd1-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span>
   * <span data-ttu-id="fbdd1-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="fbdd1-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span>


7. <span data-ttu-id="fbdd1-189">Copier hello suivant de code et l’enregistrer en tant que **install_linux.sh** dans hello **MobSvcLinux** dossier.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-189">Copy hello following code, and save it as **install_linux.sh** into hello **MobSvcLinux** folder.</span></span>
   > [!NOTE]
   > <span data-ttu-id="fbdd1-190">Remplacez les espaces réservés de hello [CSIP] dans ce script avec des valeurs réelles de hello d’adresse IP de hello de votre serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-190">Replace hello [CSIP] placeholders in this script with hello actual values of hello IP address of your configuration server.</span></span>

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
        echo "Installation has succeeded. Proceed tooconfiguration." >> /tmp/MobSvc/sccm.log
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
        echo "Agent is already configured. Proceed tooUpgrade." >> /tmp/MobSvc/sccm.log
        Upgrade
    else
        echo "Agent is not configured. Proceed tooConfigure." >> /tmp/MobSvc/sccm.log
        Configure
    fi
else
    Install
fi

cd /tmp

```

### <a name="step-2-create-a-package"></a><span data-ttu-id="fbdd1-191">Étape 2 : Création d’un package</span><span class="sxs-lookup"><span data-stu-id="fbdd1-191">Step 2: Create a package</span></span>

1. <span data-ttu-id="fbdd1-192">Se connecter dans la console Configuration Manager tooyour.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-192">Sign in  tooyour Configuration Manager console.</span></span>
2. <span data-ttu-id="fbdd1-193">Parcourir trop**bibliothèque de logiciels** > **gestion des applications** > **Packages**.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-193">Browse too**Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="fbdd1-194">Cliquez avec le bouton droit sur **Packages** et sélectionnez **Créer un package**.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-194">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="fbdd1-195">Fournir des valeurs pour la version, la description, fabricant, langue et nom de hello.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-195">Provide values for hello name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="fbdd1-196">Sélectionnez hello **ce package contient des fichiers sources** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-196">Select hello **This package contains source files** check box.</span></span>
6. <span data-ttu-id="fbdd1-197">Cliquez sur **Parcourir**et sélectionnez hello partage de réseau où se trouve le programme d’installation de hello (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="fbdd1-197">Click **Browse**, and select hello network share where hello installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span></span>

  ![Capture d’écran de l’assistant Création d’un package et d’un programme](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. <span data-ttu-id="fbdd1-199">Sur hello **type de programme hello choisir que vous souhaitez toocreate** page, sélectionnez **programme Standard**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-199">On hello **Choose hello program type that you want toocreate** page, select **Standard Program**, and click **Next**.</span></span>

  ![Capture d’écran de l’assistant Création d’un package et d’un programme](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="fbdd1-201">Sur hello **spécifier des informations sur ce programme standard** page, fournissez hello suivant des entrées, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-201">On hello **Specify information about this standard program** page, provide hello following inputs, and click **Next**.</span></span> <span data-ttu-id="fbdd1-202">(hello autres entrées peuvent utiliser leurs valeurs par défaut.)</span><span class="sxs-lookup"><span data-stu-id="fbdd1-202">(hello other inputs can use their default values.)</span></span>

    | <span data-ttu-id="fbdd1-203">**Nom du paramètre**</span><span class="sxs-lookup"><span data-stu-id="fbdd1-203">**Parameter name**</span></span> | <span data-ttu-id="fbdd1-204">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="fbdd1-204">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="fbdd1-205">Nom</span><span class="sxs-lookup"><span data-stu-id="fbdd1-205">Name</span></span> | <span data-ttu-id="fbdd1-206">Installer le service Mobilité de Microsoft Azure (Linux)</span><span class="sxs-lookup"><span data-stu-id="fbdd1-206">Install Microsoft Azure Mobility Service (Linux)</span></span> |
  | <span data-ttu-id="fbdd1-207">Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="fbdd1-207">Command line</span></span> | <span data-ttu-id="fbdd1-208">./install_linux.sh</span><span class="sxs-lookup"><span data-stu-id="fbdd1-208">./install_linux.sh</span></span> |
  | <span data-ttu-id="fbdd1-209">Le programme peut s’exécuter</span><span class="sxs-lookup"><span data-stu-id="fbdd1-209">Program can run</span></span> | <span data-ttu-id="fbdd1-210">Qu’un utilisateur ait ouvert une session ou non</span><span class="sxs-lookup"><span data-stu-id="fbdd1-210">Whether or not a user is logged on</span></span> |

  ![Capture d’écran de l’assistant Création d’un package et d’un programme](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. <span data-ttu-id="fbdd1-212">Sur la page suivante de hello, sélectionnez **ce programme peut s’exécuter sur n’importe quelle plateforme**.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-212">On hello next page, select **This program can run on any platform**.</span></span>
  <span data-ttu-id="fbdd1-213">![Capture d’écran de l’assistant Création d’un package et d’un programme](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span><span class="sxs-lookup"><span data-stu-id="fbdd1-213">![Screenshot of Create Package and Program wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span></span>

10. <span data-ttu-id="fbdd1-214">Assistant de hello toocomplete, cliquez sur **suivant** à deux reprises.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-214">toocomplete hello wizard, click **Next** twice.</span></span>

> [!NOTE]
> <span data-ttu-id="fbdd1-215">script de Hello prend en charge les nouvelles installations d’agents de Service mobilité et met à jour tooagents qui sont déjà installés.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-215">hello script supports both new installations of Mobility Service agents and updates tooagents that are already installed.</span></span>

### <a name="step-3-deploy-hello-package"></a><span data-ttu-id="fbdd1-216">Étape 3 : Déployer le package de hello</span><span class="sxs-lookup"><span data-stu-id="fbdd1-216">Step 3: Deploy hello package</span></span>
1. <span data-ttu-id="fbdd1-217">Dans la console Configuration Manager hello, avec le bouton droit de votre package, puis sélectionnez **distribuer du contenu**.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-217">In hello Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="fbdd1-218">![Capture d’écran de la console Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="fbdd1-218">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="fbdd1-219">Sélectionnez hello  **[les points de distribution](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  sur toowhich les packages hello doivent être copiés.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-219">Select hello **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on toowhich hello packages should be copied.</span></span>
3. <span data-ttu-id="fbdd1-220">Assistant hello terminée.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-220">Complete hello wizard.</span></span> <span data-ttu-id="fbdd1-221">package de Hello puis le démarrage de la réplication toohello spécifié de points de distribution.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-221">hello package then starts replicating toohello specified distribution points.</span></span>
4. <span data-ttu-id="fbdd1-222">Une fois que la distribution de package hello est terminée, cliquez sur le package de hello, puis sélectionnez **déployer**.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-222">After hello package distribution is done, right-click hello package, and select **Deploy**.</span></span>
  <span data-ttu-id="fbdd1-223">![Capture d’écran de la console Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="fbdd1-223">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="fbdd1-224">Sélectionnez hello regroupement de périphériques serveur Linux vous avez créé dans la section conditions préalables de hello en tant que regroupement cible de hello pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-224">Select hello Linux Server device collection you created in hello prerequisites section as hello target collection for deployment.</span></span>

  ![Capture d’écran de l’assistant Déploiement du logiciel](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. <span data-ttu-id="fbdd1-226">Sur hello **spécifier la destination de contenu hello** page, sélectionnez votre **les Points de Distribution**.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-226">On hello **Specify hello content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="fbdd1-227">Sur hello **toocontrol de paramètres de spécifier comment ce logiciel est déployé** , vérifiez que hello vise **requis**.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-227">On hello **Specify settings toocontrol how this software is deployed** page, ensure that hello purpose is **Required**.</span></span>

  ![Capture d’écran de l’assistant Déploiement du logiciel](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="fbdd1-229">Sur hello **spécifier la planification pour ce déploiement hello** , spécifiez une planification.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-229">On hello **Specify hello schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="fbdd1-230">Pour plus d’informations, consultez [Planification de packages](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="fbdd1-230">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="fbdd1-231">Sur hello **les Points de Distribution** page, configurez les propriétés de hello selon les besoins de toohello de votre centre de données.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-231">On hello **Distribution Points** page, configure hello properties according toohello needs of your datacenter.</span></span> <span data-ttu-id="fbdd1-232">Puis terminer hello.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-232">Then complete hello wizard.</span></span>

<span data-ttu-id="fbdd1-233">Service mobilité est installé sur hello regroupement de périphériques serveur Linux, selon la planification toohello que vous avez configuré.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-233">Mobility Service gets installed on hello Linux Server Device Collection, according toohello schedule you configured.</span></span>

## <a name="other-methods-tooinstall-mobility-service"></a><span data-ttu-id="fbdd1-234">Autres méthodes de tooinstall Service mobilité</span><span class="sxs-lookup"><span data-stu-id="fbdd1-234">Other methods tooinstall Mobility Service</span></span>
<span data-ttu-id="fbdd1-235">Voici d’autres options pour l’installation du service Mobilité :</span><span class="sxs-lookup"><span data-stu-id="fbdd1-235">Here are some other options for installing Mobility Service:</span></span>
* [<span data-ttu-id="fbdd1-236">Installation manuelle à l’aide de l’interface utilisateur graphique</span><span class="sxs-lookup"><span data-stu-id="fbdd1-236">Manual Installation using GUI</span></span>](http://aka.ms/mobsvcmanualinstall)
* [<span data-ttu-id="fbdd1-237">Installation manuelle à l’aide de la ligne de commande</span><span class="sxs-lookup"><span data-stu-id="fbdd1-237">Manual Installation using command-line</span></span>](http://aka.ms/mobsvcmanualinstallcli)
* [<span data-ttu-id="fbdd1-238">Installation Push à l’aide du serveur de configuration</span><span class="sxs-lookup"><span data-stu-id="fbdd1-238">Push Installation using configuration server </span></span>](http://aka.ms/pushinstall)
* [<span data-ttu-id="fbdd1-239">Installation automatisée à l’aide d’Azure Automation et de la Configuration de l’état souhaité</span><span class="sxs-lookup"><span data-stu-id="fbdd1-239">Automated Installation using Azure Automation & Desired State Configuration </span></span>](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a><span data-ttu-id="fbdd1-240">Désinstaller le service Mobilité</span><span class="sxs-lookup"><span data-stu-id="fbdd1-240">Uninstall Mobility Service</span></span>
<span data-ttu-id="fbdd1-241">Vous pouvez créer des packages de Configuration Manager toouninstall Service mobilité.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-241">You can create Configuration Manager packages toouninstall Mobility Service.</span></span> <span data-ttu-id="fbdd1-242">Utilisez hello suivant script toodo ainsi :</span><span class="sxs-lookup"><span data-stu-id="fbdd1-242">Use hello following script toodo so:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="fbdd1-243">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fbdd1-243">Next steps</span></span>
<span data-ttu-id="fbdd1-244">Vous êtes maintenant prêt trop[activer la protection](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) pour vos ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="fbdd1-244">You are now ready too[enable protection](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) for your virtual machines.</span></span>
