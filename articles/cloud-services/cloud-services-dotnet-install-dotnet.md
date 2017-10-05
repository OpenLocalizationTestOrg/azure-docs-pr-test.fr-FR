---
title: "Installer .NET sur des rôles d’Azure Cloud Services | Microsoft Docs"
description: "Cet article explique comment installer manuellement .NET Framework sur vos rôles web et rôles de travail de Cloud Services."
services: cloud-services
documentationcenter: .net
author: thraka
manager: timlt
editor: 
ms.assetid: 8d1243dc-879c-4d1f-9ed0-eecd1f6a6653
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: adegeo
ms.openlocfilehash: a9cffa275ae6b9315b821d3160b17a997a1523f7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="install-net-on-azure-cloud-services-roles"></a><span data-ttu-id="4628f-103">Installer .NET sur des rôles d’Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="4628f-103">Install .NET on Azure Cloud Services roles</span></span>
<span data-ttu-id="4628f-104">Cet article décrit comment installer des versions de .NET Framework qui ne sont fournies avec le SE invité Azure.</span><span class="sxs-lookup"><span data-stu-id="4628f-104">This article describes how to install versions of .NET Framework that don't come with the Azure Guest OS.</span></span> <span data-ttu-id="4628f-105">Vous pouvez utiliser .NET sur le SE invité pour configurer vos rôles web et rôles de travail de Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="4628f-105">You can use .NET on the Guest OS to configure your cloud service web and worker roles.</span></span>

<span data-ttu-id="4628f-106">Par exemple, vous pouvez installer .NET 4.6.1 sur la famille de SE invités 4, qui n’est fournie avec une version de .NET 4.6.</span><span class="sxs-lookup"><span data-stu-id="4628f-106">For example, you can install .NET 4.6.1 on the Guest OS family 4, which doesn't come with any release of .NET 4.6.</span></span> <span data-ttu-id="4628f-107">(La famille de SE invités 5 est fournie avec .NET 4.6.) Pour obtenir les dernières informations sur les versions de SE invité Azure, consultez les [Actualités concernant les versions de SE invité Azure](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="4628f-107">(The Guest OS family 5 does come with .NET 4.6.) For the latest information on the Azure Guest OS releases, see the [Azure Guest OS release news](cloud-services-guestos-update-matrix.md).</span></span> 

>[!IMPORTANT]
><span data-ttu-id="4628f-108">Azure SDK 2.9 contient une restriction sur le déploiement de .NET 4.6 sur la famille de SE invités 4 ou version antérieure.</span><span class="sxs-lookup"><span data-stu-id="4628f-108">The Azure SDK 2.9 contains a restriction on deploying .NET 4.6 on the Guest OS family 4 or earlier.</span></span> <span data-ttu-id="4628f-109">Un correctif pour la restriction est disponible sur le site [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span><span class="sxs-lookup"><span data-stu-id="4628f-109">A fix for the restriction is available on the [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.</span></span>

<span data-ttu-id="4628f-110">Pour installer .NET sur vos rôles web et rôles de travail, incluez le programme d’installation web de .NET dans le cadre de votre projet de service cloud.</span><span class="sxs-lookup"><span data-stu-id="4628f-110">To install .NET on your web and worker roles, include the .NET web installer as part of your cloud service project.</span></span> <span data-ttu-id="4628f-111">Démarrez le programme d’installation dans le cadre des tâches de démarrage des rôles.</span><span class="sxs-lookup"><span data-stu-id="4628f-111">Start the installer as part of the role's startup tasks.</span></span> 

## <a name="add-the-net-installer-to-your-project"></a><span data-ttu-id="4628f-112">Ajouter le programme d'installation de .NET à votre projet</span><span class="sxs-lookup"><span data-stu-id="4628f-112">Add the .NET installer to your project</span></span>
<span data-ttu-id="4628f-113">Pour télécharger le programme d'installation web de .NET Framework, sélectionnez la version à installer :</span><span class="sxs-lookup"><span data-stu-id="4628f-113">To download the web installer for the .NET Framework, choose the version that you want to install:</span></span>

* [<span data-ttu-id="4628f-114">Programme d’installation web de .NET 4.7</span><span class="sxs-lookup"><span data-stu-id="4628f-114">.NET 4.7 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=825298)
* [<span data-ttu-id="4628f-115">Programme d’installation web de.NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="4628f-115">.NET 4.6.1 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=671729)

<span data-ttu-id="4628f-116">Pour ajouter le programme d’installation pour un rôle *web* :</span><span class="sxs-lookup"><span data-stu-id="4628f-116">To add the installer for a *web* role:</span></span>
  1. <span data-ttu-id="4628f-117">Dans l’**Explorateur de solutions**, dans votre projet de service cloud, sous **Rôles**, cliquez avec le bouton droit sur votre rôle *web*, puis sélectionnez **Ajouter** > **Nouveau dossier**.</span><span class="sxs-lookup"><span data-stu-id="4628f-117">In **Solution Explorer**, under **Roles** in your cloud service project, right-click your *web* role and select **Add** > **New Folder**.</span></span> <span data-ttu-id="4628f-118">Créez un dossier intitulé **bin**.</span><span class="sxs-lookup"><span data-stu-id="4628f-118">Create a folder named **bin**.</span></span>
  2. <span data-ttu-id="4628f-119">Cliquez avec le bouton droit sur le dossier bin, puis sélectionnez **Ajouter** > **Élément existant**.</span><span class="sxs-lookup"><span data-stu-id="4628f-119">Right-click the bin folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="4628f-120">Sélectionnez le programme d'installation de .NET, puis ajoutez-le au dossier bin.</span><span class="sxs-lookup"><span data-stu-id="4628f-120">Select the .NET installer and add it to the bin folder.</span></span>
  
<span data-ttu-id="4628f-121">Pour ajouter le programme d’installation pour un rôle *de travail* :</span><span class="sxs-lookup"><span data-stu-id="4628f-121">To add the installer for a *worker* role:</span></span>
* <span data-ttu-id="4628f-122">Cliquez avec le bouton droit sur votre rôle *de travail*, puis sélectionnez **Ajouter** > **Élément existant**.</span><span class="sxs-lookup"><span data-stu-id="4628f-122">Right-click your *worker* role and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="4628f-123">Sélectionnez le programme d'installation de .NET, puis ajoutez-le au rôle.</span><span class="sxs-lookup"><span data-stu-id="4628f-123">Select the .NET installer and add it to the role.</span></span> 

<span data-ttu-id="4628f-124">Les fichiers ajoutés de cette façon dans le dossier de contenu du rôle sont automatiquement ajoutés à votre package de service cloud</span><span class="sxs-lookup"><span data-stu-id="4628f-124">When files are added in this way to the role content folder, they're automatically added to your cloud service package.</span></span> <span data-ttu-id="4628f-125">et déployés dans un emplacement similaire sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4628f-125">The files are then deployed to a consistent location on the virtual machine.</span></span> <span data-ttu-id="4628f-126">Répétez ce processus pour chaque rôle web et chaque rôle de travail de service cloud afin que tous les rôles disposent d'une copie du programme d'installation.</span><span class="sxs-lookup"><span data-stu-id="4628f-126">Repeat this process for each web and worker role in your cloud service so that all roles have a copy of the installer.</span></span>

> [!NOTE]
> <span data-ttu-id="4628f-127">Même si votre application cible .NET 4.6, nous vous conseillons d’installer .NET 4.6.1 sur votre rôle de service cloud.</span><span class="sxs-lookup"><span data-stu-id="4628f-127">You should install .NET 4.6.1 on your cloud service role even if your application targets .NET 4.6.</span></span> <span data-ttu-id="4628f-128">Le SE invité inclut les mises à jour [ 3098779](https://support.microsoft.com/kb/3098779) et [3097997](https://support.microsoft.com/kb/3097997) de la base de connaissances.</span><span class="sxs-lookup"><span data-stu-id="4628f-128">The Guest OS includes the Knowledge Base [update 3098779](https://support.microsoft.com/kb/3098779) and [update 3097997](https://support.microsoft.com/kb/3097997).</span></span> <span data-ttu-id="4628f-129">L’installation de NET 4.6 en plus de ces mises à jour peut causer des problèmes lors de l’exécution de vos applications .NET.</span><span class="sxs-lookup"><span data-stu-id="4628f-129">Issues can occur when you run your .NET applications if .NET 4.6 is installed on top of the Knowledge Base updates.</span></span> <span data-ttu-id="4628f-130">Pour éviter ces problèmes, installez .NET 4.6.1 au lieu de la version 4.6.</span><span class="sxs-lookup"><span data-stu-id="4628f-130">To avoid these issues, install .NET 4.6.1 rather than version 4.6.</span></span> <span data-ttu-id="4628f-131">Pour plus d’informations, consultez cet [article sur la base de connaissances 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="4628f-131">For more information, see the [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
> 
> 

![Contenu du rôle avec les fichiers d'installation][1]

## <a name="define-startup-tasks-for-your-roles"></a><span data-ttu-id="4628f-133">Définir des tâches de démarrage pour vos rôles</span><span class="sxs-lookup"><span data-stu-id="4628f-133">Define startup tasks for your roles</span></span>
<span data-ttu-id="4628f-134">Vous pouvez utiliser des tâches de démarrage pour exécuter des opérations avant le démarrage d’un rôle.</span><span class="sxs-lookup"><span data-stu-id="4628f-134">You can use startup tasks to perform operations before a role starts.</span></span> <span data-ttu-id="4628f-135">L’installation de .NET Framework dans le cadre de la tâche de démarrage permet de garantir qu’il sera installé avant l’exécution du code de votre application.</span><span class="sxs-lookup"><span data-stu-id="4628f-135">Installing the .NET Framework as part of the startup task ensures that the framework is installed before any application code is run.</span></span> <span data-ttu-id="4628f-136">Pour plus d’informations sur les tâches de démarrage, consultez [Exécuter des tâches de démarrage dans Azure](cloud-services-startup-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="4628f-136">For more information on startup tasks, see [Run startup tasks in Azure](cloud-services-startup-tasks.md).</span></span> 

1. <span data-ttu-id="4628f-137">Ajoutez le contenu suivant au fichier ServiceDefinition.csdef sous le nœud **WebRole** ou **WorkerRole** pour tous les rôles :</span><span class="sxs-lookup"><span data-stu-id="4628f-137">Add the following content to the ServiceDefinition.csdef file under the **WebRole** or **WorkerRole** node for all roles:</span></span>
   
    ```xml
    <LocalResources>
      <LocalStorage name="NETFXInstall" sizeInMB="1024" cleanOnRoleRecycle="false" />
    </LocalResources>    
    <Startup>
      <Task commandLine="install.cmd" executionContext="elevated" taskType="simple">
        <Environment>
          <Variable name="PathToNETFXInstall">
            <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='NETFXInstall']/@path" />
          </Variable>
          <Variable name="ComputeEmulatorRunning">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
        </Environment>
      </Task>
    </Startup>
    ```
   
    <span data-ttu-id="4628f-138">La configuration précédente exécute la commande de console `install.cmd` avec des privilèges d’administrateur pour installer .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="4628f-138">The preceding configuration runs the console command `install.cmd` with administrator privileges to install the .NET Framework.</span></span> <span data-ttu-id="4628f-139">La configuration crée également un élément **LocalStorage** nommé **NETFXInstall**.</span><span class="sxs-lookup"><span data-stu-id="4628f-139">The configuration also creates a **LocalStorage** element named **NETFXInstall**.</span></span> <span data-ttu-id="4628f-140">Le script de démarrage configure le dossier temporaire pour qu’il utilise cette ressource de stockage local.</span><span class="sxs-lookup"><span data-stu-id="4628f-140">The startup script sets the temp folder to use this local storage resource.</span></span> 
    
    > [!IMPORTANT]
    > <span data-ttu-id="4628f-141">Afin de garantir l’installation correcte de Framework, définissez la taille de cette ressource sur 1 024 Mo au minimum.</span><span class="sxs-lookup"><span data-stu-id="4628f-141">To ensure correct installation of the framework, set the size of this resource to at least 1,024 MB.</span></span>
    
    <span data-ttu-id="4628f-142">Pour plus d’informations sur les tâches de démarrage, consultez [Tâches courantes de démarrage dans Azure Cloud Services](cloud-services-startup-tasks-common.md).</span><span class="sxs-lookup"><span data-stu-id="4628f-142">For more information about startup tasks, see [Common Azure Cloud Services startup tasks](cloud-services-startup-tasks-common.md).</span></span>

2. <span data-ttu-id="4628f-143">Créez un fichier nommé **install.cmd** et ajoutez le script d’installation suivant au fichier.</span><span class="sxs-lookup"><span data-stu-id="4628f-143">Create a file named **install.cmd** and add the following install script to the file.</span></span>

    <span data-ttu-id="4628f-144">Le script vérifie si la version de .NET Framework spécifiée est déjà installée sur l'ordinateur en interrogeant le Registre.</span><span class="sxs-lookup"><span data-stu-id="4628f-144">The script checks whether the specified version of the .NET Framework is already installed on the machine by querying the registry.</span></span> <span data-ttu-id="4628f-145">Si la version de .NET n'est pas installée, le programme d'installation web de .NET est lancé.</span><span class="sxs-lookup"><span data-stu-id="4628f-145">If the .NET version is not installed, then the .NET web installer is opened.</span></span> <span data-ttu-id="4628f-146">Pour résoudre les éventuels problèmes, le script enregistre toutes les activités dans le fichier startuptasklog-(date et heures actuelles).txt qui est conservé dans le stockage local **InstallLogs**.</span><span class="sxs-lookup"><span data-stu-id="4628f-146">To help troubleshoot any issues, the script logs all activity to the file startuptasklog-(current date and time).txt that is stored in **InstallLogs** local storage.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4628f-147">Utilisez un éditeur de texte de base tel que le Bloc-notes de Windows pour créer le fichier install.cmd.</span><span class="sxs-lookup"><span data-stu-id="4628f-147">Use a basic text editor like Windows Notepad to create the install.cmd file.</span></span> <span data-ttu-id="4628f-148">Si vous utilisez Visual Studio pour créer un fichier texte dont vous changez ensuite l’extension à .cmd, le fichier risque de toujours contenir une marque d’ordre d’octet UTF-8</span><span class="sxs-lookup"><span data-stu-id="4628f-148">If you use Visual Studio to create a text file and change the extension to .cmd, the file might still contain a UTF-8 byte order mark.</span></span> <span data-ttu-id="4628f-149">qui pourrait générer une erreur lors de l’exécution de la première ligne du script.</span><span class="sxs-lookup"><span data-stu-id="4628f-149">This mark can cause an error when the first line of the script is run.</span></span> <span data-ttu-id="4628f-150">Pour éviter cette erreur, assurez-vous que la première ligne du script est une instruction REM qui peut être ignorée par le traitement de la marque d’ordre d’octet.</span><span class="sxs-lookup"><span data-stu-id="4628f-150">To avoid this error, make the first line of the script a REM statement that can be skipped by the byte order processing.</span></span> 
    > 
    >
   
    ```cmd
    REM Set the value of netfx to install appropriate .NET Framework. 
    REM ***** To install .NET 4.5.2 set the variable netfx to "NDP452" *****
    REM ***** To install .NET 4.6 set the variable netfx to "NDP46" *****
    REM ***** To install .NET 4.6.1 set the variable netfx to "NDP461" *****
    REM ***** To install .NET 4.6.2 set the variable netfx to "NDP462" *****
    REM ***** To install .NET 4.7 set the variable netfx to "NDP47" *****
    set netfx="NDP47"

    REM ***** Set script start timestamp *****
    set timehour=%time:~0,2%
    set timestamp=%date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2%
    set "log=install.cmd started %timestamp%."

    REM ***** Exit script if running in Emulator *****
    if %ComputeEmulatorRunning%=="true" goto exit

    REM ***** Needed to correctly install .NET 4.6.1, otherwise you may see an out of disk space error *****
    set TMP=%PathToNETFXInstall%
    set TEMP=%PathToNETFXInstall%

    REM ***** Setup .NET filenames and registry keys *****
    if %netfx%=="NDP47" goto NDP47
    if %netfx%=="NDP462" goto NDP462
    if %netfx%=="NDP461" goto NDP461
    if %netfx%=="NDP46" goto NDP46
        set "netfxinstallfile=NDP452-KB2901954-Web.exe"
        set netfxregkey="0x5cbf5"
        goto logtimestamp

    :NDP46
    set "netfxinstallfile=NDP46-KB3045560-Web.exe"
    set netfxregkey="0x6004f"
    goto logtimestamp

    :NDP461
    set "netfxinstallfile=NDP461-KB3102438-Web.exe"
    set netfxregkey="0x6040e"
    goto logtimestamp

    :NDP462
    set "netfxinstallfile=NDP462-KB3151802-Web.exe"
    set netfxregkey="0x60632"

    :NDP47
    set "netfxinstallfile=NDP47-KB3186500-Web.exe"
    set netfxregkey="0x707FE"

    :logtimestamp
    REM ***** Setup LogFile with timestamp *****
    md "%PathToNETFXInstall%\log"
    set startuptasklog="%PathToNETFXInstall%log\startuptasklog-%timestamp%.txt"
    set netfxinstallerlog="%PathToNETFXInstall%log\NetFXInstallerLog-%timestamp%"
    echo %log% >> %startuptasklog%
    echo Logfile generated at: %startuptasklog% >> %startuptasklog%
    echo TMP set to: %TMP% >> %startuptasklog%
    echo TEMP set to: %TEMP% >> %startuptasklog%

    REM ***** Check if .NET is installed *****
    echo Checking if .NET (%netfx%) is installed >> %startuptasklog%
    set /A netfxregkeydecimal=%netfxregkey%
    set foundkey=0
    FOR /F "usebackq skip=2 tokens=1,2*" %%A in (`reg query "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full" /v Release 2^>nul`) do @set /A foundkey=%%C
    echo Minimum required key: %netfxregkeydecimal% -- found key: %foundkey% >> %startuptasklog%
    if %foundkey% GEQ %netfxregkeydecimal% goto installed

    REM ***** Installing .NET *****
    echo Installing .NET with commandline: start /wait %~dp0%netfxinstallfile% /q /serialdownload /log %netfxinstallerlog%  /chainingpackage "CloudService Startup Task" >> %startuptasklog%
    start /wait %~dp0%netfxinstallfile% /q /serialdownload /log %netfxinstallerlog% /chainingpackage "CloudService Startup Task" >> %startuptasklog% 2>>&1
    if %ERRORLEVEL%== 0 goto installed
        echo .NET installer exited with code %ERRORLEVEL% >> %startuptasklog%    
        if %ERRORLEVEL%== 3010 goto restart
        if %ERRORLEVEL%== 1641 goto restart
        echo .NET (%netfx%) install failed with Error Code %ERRORLEVEL%. Further logs can be found in %netfxinstallerlog% >> %startuptasklog%

    :restart
    echo Restarting to complete .NET (%netfx%) installation >> %startuptasklog%
    EXIT /B %ERRORLEVEL%

    :installed
    echo .NET (%netfx%) is installed >> %startuptasklog%

    :end
    echo install.cmd completed: %date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2% >> %startuptasklog%

    :exit
    EXIT /B 0
    ```
   
   > [!NOTE]
   > <span data-ttu-id="4628f-151">Le script vous indique comment installer la version .NET 4.5.2 ou .4.6 à des fins de continuité, même si la version .NET 4.5.2 est déjà disponible sur le SE invité Azure.</span><span class="sxs-lookup"><span data-stu-id="4628f-151">This script shows how to install .NET 4.5.2 or version 4.6 for continuity, even though .NET 4.5.2 is already available on the Azure Guest OS.</span></span> <span data-ttu-id="4628f-152">Nous vous conseillons d’installer directement .NET 4.6.1 au lieu de la version 4.6, tel que décrit dans l’[article de la base de connaissances 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="4628f-152">You should directly install .NET 4.6.1 rather than version 4.6, as described in the [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
   > 
   > 

3. <span data-ttu-id="4628f-153">Ajoutez le fichier install.cmd à chaque rôle en sélectionnant**Ajouter** > **Élément existant** dans l’**Explorateur de solutions**, tel que décrit précédemment dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="4628f-153">Add the install.cmd file to each role by using **Add** > **Existing Item** in **Solution Explorer** as described earlier in this topic.</span></span> 

    <span data-ttu-id="4628f-154">Une fois cette étape réalisée, tous les rôles doivent avoir le fichier du programme d'installation de .NET et le fichier install.cmd.</span><span class="sxs-lookup"><span data-stu-id="4628f-154">After this step is complete, all roles should have the .NET installer file and the install.cmd file.</span></span>

   ![Contenu du rôle avec tous les fichiers][2]

## <a name="configure-diagnostics-to-transfer-startup-logs-to-blob-storage"></a><span data-ttu-id="4628f-156">Configurer les diagnostics pour transférer les journaux de démarrage vers le stockage Blob</span><span class="sxs-lookup"><span data-stu-id="4628f-156">Configure Diagnostics to transfer startup logs to Blob storage</span></span>
<span data-ttu-id="4628f-157">Pour simplifier la résolution des problèmes d’installation, vous pouvez configurer Azure Diagnostics de façon à transférer tous les fichiers journaux générés par le script de démarrage ou le programme d’installation de .NET vers le stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="4628f-157">To simplify troubleshooting installation issues, you can configure Azure Diagnostics to transfer any log files generated by the startup script or the .NET installer to Azure Blob storage.</span></span> <span data-ttu-id="4628f-158">Grâce à cette approche, vous pouvez afficher les journaux en téléchargeant les fichiers journaux depuis le stockage Blob au lieu d’accéder au rôle par le biais du Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="4628f-158">By using this approach, you can view the logs by downloading the log files from Blob storage rather than having to remote desktop into the role.</span></span>

<span data-ttu-id="4628f-159">Pour configurer les diagnostics, ouvrez le fichier diagnostics.wadcfgx et ajoutez le contenu suivant sous le nœud **Directories** :</span><span class="sxs-lookup"><span data-stu-id="4628f-159">To configure Diagnostics, open the diagnostics.wadcfgx file and add the following content under the **Directories** node:</span></span> 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

<span data-ttu-id="4628f-160">Ce code XML configure Diagnostics de façon à transférer tous les fichiers du répertoire log de la ressource **NETFXInstall** vers le compte de stockage de Diagnostics dans le conteneur d’objets blob **netfx-install**.</span><span class="sxs-lookup"><span data-stu-id="4628f-160">This XML configures Diagnostics to transfer the files in the log directory in the **NETFXInstall** resource to the Diagnostics storage account in the **netfx-install** blob container.</span></span>

## <a name="deploy-your-cloud-service"></a><span data-ttu-id="4628f-161">Déployer votre service cloud</span><span class="sxs-lookup"><span data-stu-id="4628f-161">Deploy your cloud service</span></span>
<span data-ttu-id="4628f-162">Quand vous déployez votre service cloud, les tâches de démarrage installent .NET Framework, s’il n’est pas déjà installé.</span><span class="sxs-lookup"><span data-stu-id="4628f-162">When you deploy your cloud service, the startup tasks install the .NET Framework if it's not already installed.</span></span> <span data-ttu-id="4628f-163">Vos rôles de service cloud seront à l’état *Occupé* pendant l’installation de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="4628f-163">Your cloud service roles are in the *busy* state while the framework is being installed.</span></span> <span data-ttu-id="4628f-164">et peuvent même être redémarrés si l’installation le nécessite.</span><span class="sxs-lookup"><span data-stu-id="4628f-164">If the framework installation requires a restart, the service roles might also restart.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4628f-165">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4628f-165">Additional resources</span></span>
* <span data-ttu-id="4628f-166">[Installation du .NET Framework][Installing the .NET Framework]</span><span class="sxs-lookup"><span data-stu-id="4628f-166">[Installing the .NET Framework][Installing the .NET Framework]</span></span>
* <span data-ttu-id="4628f-167">[Identifier les versions de .NET Framework installées][How to: Determine Which .NET Framework Versions Are Installed]</span><span class="sxs-lookup"><span data-stu-id="4628f-167">[Determine which .NET Framework versions are installed][How to: Determine Which .NET Framework Versions Are Installed]</span></span>
* <span data-ttu-id="4628f-168">[Résolution des problèmes liés aux installations de .NET Framework][Troubleshooting .NET Framework Installations]</span><span class="sxs-lookup"><span data-stu-id="4628f-168">[Troubleshooting .NET Framework installations][Troubleshooting .NET Framework Installations]</span></span>

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing the .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
