---
title: "aaaInstall .NET sur les rôles des Services de cloud computing Azure | Documents Microsoft"
description: "Cet article décrit comment toomanually installer hello .NET Framework sur vos rôles web et de travail du service cloud"
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
ms.openlocfilehash: 45f0f30221292f98c591511b091b02ebe1c1272c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-net-on-azure-cloud-services-roles"></a><span data-ttu-id="28b7c-103">Installer .NET sur des rôles d’Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="28b7c-103">Install .NET on Azure Cloud Services roles</span></span>
<span data-ttu-id="28b7c-104">Cet article décrit comment tooinstall les versions du .NET Framework qui ne comportent pas de hello du système d’exploitation invité de Azure.</span><span class="sxs-lookup"><span data-stu-id="28b7c-104">This article describes how tooinstall versions of .NET Framework that don't come with hello Azure Guest OS.</span></span> <span data-ttu-id="28b7c-105">Vous pouvez utiliser .NET sur tooconfigure de système d’exploitation invité hello vos rôles web et de travail du service cloud.</span><span class="sxs-lookup"><span data-stu-id="28b7c-105">You can use .NET on hello Guest OS tooconfigure your cloud service web and worker roles.</span></span>

<span data-ttu-id="28b7c-106">Par exemple, vous pouvez installer le .NET 4.6.1 sur hello famille de système d’exploitation invité 4, ce qui n’est fourni avec une version de .NET 4.6.</span><span class="sxs-lookup"><span data-stu-id="28b7c-106">For example, you can install .NET 4.6.1 on hello Guest OS family 4, which doesn't come with any release of .NET 4.6.</span></span> <span data-ttu-id="28b7c-107">(hello famille de système d’exploitation invité 5 n’est fourni avec .NET 4.6.) Pour plus d’informations plus récentes hello sur hello mises à jour de système d’exploitation invité de Azure, consultez hello [informations de version du système d’exploitation invité de Azure](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="28b7c-107">(hello Guest OS family 5 does come with .NET 4.6.) For hello latest information on hello Azure Guest OS releases, see hello [Azure Guest OS release news](cloud-services-guestos-update-matrix.md).</span></span> 

>[!IMPORTANT]
><span data-ttu-id="28b7c-108">Bonjour Azure SDK 2.9 contient une restriction sur le déploiement de .NET 4.6 sur la famille de systèmes d’exploitation invités hello 4 ou une version antérieure.</span><span class="sxs-lookup"><span data-stu-id="28b7c-108">hello Azure SDK 2.9 contains a restriction on deploying .NET 4.6 on hello Guest OS family 4 or earlier.</span></span> <span data-ttu-id="28b7c-109">Un correctif pour la restriction de hello est disponible sur hello [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.</span><span class="sxs-lookup"><span data-stu-id="28b7c-109">A fix for hello restriction is available on hello [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.</span></span>

<span data-ttu-id="28b7c-110">tooinstall .NET sur vos rôles web et de travail, incluent le programme d’installation de web de .NET hello dans le cadre de votre projet de service cloud.</span><span class="sxs-lookup"><span data-stu-id="28b7c-110">tooinstall .NET on your web and worker roles, include hello .NET web installer as part of your cloud service project.</span></span> <span data-ttu-id="28b7c-111">Démarrer le programme d’installation de hello en tant que partie de du rôle hello tâches de démarrage.</span><span class="sxs-lookup"><span data-stu-id="28b7c-111">Start hello installer as part of hello role's startup tasks.</span></span> 

## <a name="add-hello-net-installer-tooyour-project"></a><span data-ttu-id="28b7c-112">Ajouter un projet de tooyour de programme d’installation de .NET hello</span><span class="sxs-lookup"><span data-stu-id="28b7c-112">Add hello .NET installer tooyour project</span></span>
<span data-ttu-id="28b7c-113">toodownload hello web programme d’installation pour hello .NET Framework, choisissez la version hello que vous souhaitez tooinstall :</span><span class="sxs-lookup"><span data-stu-id="28b7c-113">toodownload hello web installer for hello .NET Framework, choose hello version that you want tooinstall:</span></span>

* [<span data-ttu-id="28b7c-114">Programme d’installation web de .NET 4.7</span><span class="sxs-lookup"><span data-stu-id="28b7c-114">.NET 4.7 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=825298)
* [<span data-ttu-id="28b7c-115">Programme d’installation web de.NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="28b7c-115">.NET 4.6.1 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=671729)

<span data-ttu-id="28b7c-116">programme d’installation de tooadd hello pour un *web* rôle :</span><span class="sxs-lookup"><span data-stu-id="28b7c-116">tooadd hello installer for a *web* role:</span></span>
  1. <span data-ttu-id="28b7c-117">Dans l’**Explorateur de solutions**, dans votre projet de service cloud, sous **Rôles**, cliquez avec le bouton droit sur votre rôle *web*, puis sélectionnez **Ajouter** > **Nouveau dossier**.</span><span class="sxs-lookup"><span data-stu-id="28b7c-117">In **Solution Explorer**, under **Roles** in your cloud service project, right-click your *web* role and select **Add** > **New Folder**.</span></span> <span data-ttu-id="28b7c-118">Créez un dossier intitulé **bin**.</span><span class="sxs-lookup"><span data-stu-id="28b7c-118">Create a folder named **bin**.</span></span>
  2. <span data-ttu-id="28b7c-119">Cliquez sur le dossier bin de hello et sélectionnez **ajouter** > **élément existant**.</span><span class="sxs-lookup"><span data-stu-id="28b7c-119">Right-click hello bin folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="28b7c-120">Sélectionnez le programme d’installation de .NET hello et ajouter le dossier bin de toohello.</span><span class="sxs-lookup"><span data-stu-id="28b7c-120">Select hello .NET installer and add it toohello bin folder.</span></span>
  
<span data-ttu-id="28b7c-121">programme d’installation de tooadd hello pour un *travail* rôle :</span><span class="sxs-lookup"><span data-stu-id="28b7c-121">tooadd hello installer for a *worker* role:</span></span>
* <span data-ttu-id="28b7c-122">Cliquez avec le bouton droit sur votre rôle *de travail*, puis sélectionnez **Ajouter** > **Élément existant**.</span><span class="sxs-lookup"><span data-stu-id="28b7c-122">Right-click your *worker* role and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="28b7c-123">Sélectionnez le programme d’installation de .NET hello et ajoutez-le toohello rôle.</span><span class="sxs-lookup"><span data-stu-id="28b7c-123">Select hello .NET installer and add it toohello role.</span></span> 

<span data-ttu-id="28b7c-124">Lorsque les fichiers sont ajoutés dans ce dossier de contenu de façon toohello rôle, elles sont automatiquement ajoutées tooyour package de service cloud.</span><span class="sxs-lookup"><span data-stu-id="28b7c-124">When files are added in this way toohello role content folder, they're automatically added tooyour cloud service package.</span></span> <span data-ttu-id="28b7c-125">Hello les fichiers sont ensuite emplacement cohérent de tooa déployé sur l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="28b7c-125">hello files are then deployed tooa consistent location on hello virtual machine.</span></span> <span data-ttu-id="28b7c-126">Répétez ce processus pour chaque rôle web et de travail dans votre service cloud afin que tous les rôles de disposer d’une copie du programme d’installation hello.</span><span class="sxs-lookup"><span data-stu-id="28b7c-126">Repeat this process for each web and worker role in your cloud service so that all roles have a copy of hello installer.</span></span>

> [!NOTE]
> <span data-ttu-id="28b7c-127">Même si votre application cible .NET 4.6, nous vous conseillons d’installer .NET 4.6.1 sur votre rôle de service cloud.</span><span class="sxs-lookup"><span data-stu-id="28b7c-127">You should install .NET 4.6.1 on your cloud service role even if your application targets .NET 4.6.</span></span> <span data-ttu-id="28b7c-128">Hello du système d’exploitation invité inclut hello Base de connaissances [mettre à jour 3098779](https://support.microsoft.com/kb/3098779) et [mettre à jour 3097997](https://support.microsoft.com/kb/3097997).</span><span class="sxs-lookup"><span data-stu-id="28b7c-128">hello Guest OS includes hello Knowledge Base [update 3098779](https://support.microsoft.com/kb/3098779) and [update 3097997](https://support.microsoft.com/kb/3097997).</span></span> <span data-ttu-id="28b7c-129">Problèmes peuvent se produire lorsque vous exécutez vos applications .NET si .NET 4.6 est installé sur les mises à jour de la Base de connaissances hello.</span><span class="sxs-lookup"><span data-stu-id="28b7c-129">Issues can occur when you run your .NET applications if .NET 4.6 is installed on top of hello Knowledge Base updates.</span></span> <span data-ttu-id="28b7c-130">tooavoid ces problèmes, installez le .NET 4.6.1 plutôt que la version 4.6.</span><span class="sxs-lookup"><span data-stu-id="28b7c-130">tooavoid these issues, install .NET 4.6.1 rather than version 4.6.</span></span> <span data-ttu-id="28b7c-131">Pour plus d’informations, consultez hello [l’article de la Base de connaissances 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="28b7c-131">For more information, see hello [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
> 
> 

![Contenu du rôle avec les fichiers d'installation][1]

## <a name="define-startup-tasks-for-your-roles"></a><span data-ttu-id="28b7c-133">Définir des tâches de démarrage pour vos rôles</span><span class="sxs-lookup"><span data-stu-id="28b7c-133">Define startup tasks for your roles</span></span>
<span data-ttu-id="28b7c-134">Vous pouvez utiliser les opérations de tooperform de tâches de démarrage avant le démarrage d’un rôle.</span><span class="sxs-lookup"><span data-stu-id="28b7c-134">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="28b7c-135">L’installation hello .NET Framework comme partie de la tâche de démarrage hello garantit que framework hello est installé avant l’exécution de tout code d’application.</span><span class="sxs-lookup"><span data-stu-id="28b7c-135">Installing hello .NET Framework as part of hello startup task ensures that hello framework is installed before any application code is run.</span></span> <span data-ttu-id="28b7c-136">Pour plus d’informations sur les tâches de démarrage, consultez [Exécuter des tâches de démarrage dans Azure](cloud-services-startup-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="28b7c-136">For more information on startup tasks, see [Run startup tasks in Azure](cloud-services-startup-tasks.md).</span></span> 

1. <span data-ttu-id="28b7c-137">Ajouter hello contenu toohello le fichier ServiceDefinition.csdef sous hello suivant **WebRole** ou **WorkerRole** nœud pour tous les rôles :</span><span class="sxs-lookup"><span data-stu-id="28b7c-137">Add hello following content toohello ServiceDefinition.csdef file under hello **WebRole** or **WorkerRole** node for all roles:</span></span>
   
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
   
    <span data-ttu-id="28b7c-138">commande de console hello exécute Hello précédente configuration `install.cmd` avec tooinstall de privilèges d’administrateur hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="28b7c-138">hello preceding configuration runs hello console command `install.cmd` with administrator privileges tooinstall hello .NET Framework.</span></span> <span data-ttu-id="28b7c-139">configuration de Hello crée également un **LocalStorage** élément nommé **NETFXInstall**.</span><span class="sxs-lookup"><span data-stu-id="28b7c-139">hello configuration also creates a **LocalStorage** element named **NETFXInstall**.</span></span> <span data-ttu-id="28b7c-140">script de démarrage Hello définit hello dossier temporaire toouse cette ressource de stockage local.</span><span class="sxs-lookup"><span data-stu-id="28b7c-140">hello startup script sets hello temp folder toouse this local storage resource.</span></span> 
    
    > [!IMPORTANT]
    > <span data-ttu-id="28b7c-141">tooensure corriger l’installation de framework hello, taille hello du jeu de tooat de cette ressource moins 1 024 Mo.</span><span class="sxs-lookup"><span data-stu-id="28b7c-141">tooensure correct installation of hello framework, set hello size of this resource tooat least 1,024 MB.</span></span>
    
    <span data-ttu-id="28b7c-142">Pour plus d’informations sur les tâches de démarrage, consultez [Tâches courantes de démarrage dans Azure Cloud Services](cloud-services-startup-tasks-common.md).</span><span class="sxs-lookup"><span data-stu-id="28b7c-142">For more information about startup tasks, see [Common Azure Cloud Services startup tasks](cloud-services-startup-tasks-common.md).</span></span>

2. <span data-ttu-id="28b7c-143">Créez un fichier nommé **install.cmd** et ajoutez suivant de hello installer le fichier de script toohello.</span><span class="sxs-lookup"><span data-stu-id="28b7c-143">Create a file named **install.cmd** and add hello following install script toohello file.</span></span>

    <span data-ttu-id="28b7c-144">script de Hello vérifie si version spécifiée de hello Hello .NET Framework est déjà installée sur l’ordinateur de hello en interrogeant le Registre de hello.</span><span class="sxs-lookup"><span data-stu-id="28b7c-144">hello script checks whether hello specified version of hello .NET Framework is already installed on hello machine by querying hello registry.</span></span> <span data-ttu-id="28b7c-145">Si la version de .NET hello n’est pas installée, le programme d’installation web hello .NET est ouvert.</span><span class="sxs-lookup"><span data-stu-id="28b7c-145">If hello .NET version is not installed, then hello .NET web installer is opened.</span></span> <span data-ttu-id="28b7c-146">toohelp résoudre les problèmes, le script de hello enregistre toutes les activités toohello fichier startuptasklog-(date et heure actuelles) .txt stocké dans **InstallLogs** stockage local.</span><span class="sxs-lookup"><span data-stu-id="28b7c-146">toohelp troubleshoot any issues, hello script logs all activity toohello file startuptasklog-(current date and time).txt that is stored in **InstallLogs** local storage.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="28b7c-147">Utilisez un éditeur de texte simple comme bloc-notes Windows toocreate hello install.cmd fichier.</span><span class="sxs-lookup"><span data-stu-id="28b7c-147">Use a basic text editor like Windows Notepad toocreate hello install.cmd file.</span></span> <span data-ttu-id="28b7c-148">Si vous utilisez Visual Studio toocreate un fichier texte et que vous modifiez hello extension too.cmd, fichier de hello peut présenter une marque d’ordre UTF-8.</span><span class="sxs-lookup"><span data-stu-id="28b7c-148">If you use Visual Studio toocreate a text file and change hello extension too.cmd, hello file might still contain a UTF-8 byte order mark.</span></span> <span data-ttu-id="28b7c-149">Cette marque peut provoquer une erreur lors de l’exécution de hello première ligne du script de hello.</span><span class="sxs-lookup"><span data-stu-id="28b7c-149">This mark can cause an error when hello first line of hello script is run.</span></span> <span data-ttu-id="28b7c-150">tooavoid cette erreur, assurez-vous hello première ligne de hello une instruction REM qui peut être ignorée par le traitement des commandes hello octets de script.</span><span class="sxs-lookup"><span data-stu-id="28b7c-150">tooavoid this error, make hello first line of hello script a REM statement that can be skipped by hello byte order processing.</span></span> 
    > 
    >
   
    ```cmd
    REM Set hello value of netfx tooinstall appropriate .NET Framework. 
    REM ***** tooinstall .NET 4.5.2 set hello variable netfx too"NDP452" *****
    REM ***** tooinstall .NET 4.6 set hello variable netfx too"NDP46" *****
    REM ***** tooinstall .NET 4.6.1 set hello variable netfx too"NDP461" *****
    REM ***** tooinstall .NET 4.6.2 set hello variable netfx too"NDP462" *****
    REM ***** tooinstall .NET 4.7 set hello variable netfx too"NDP47" *****
    set netfx="NDP47"

    REM ***** Set script start timestamp *****
    set timehour=%time:~0,2%
    set timestamp=%date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2%
    set "log=install.cmd started %timestamp%."

    REM ***** Exit script if running in Emulator *****
    if %ComputeEmulatorRunning%=="true" goto exit

    REM ***** Needed toocorrectly install .NET 4.6.1, otherwise you may see an out of disk space error *****
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
    echo Restarting toocomplete .NET (%netfx%) installation >> %startuptasklog%
    EXIT /B %ERRORLEVEL%

    :installed
    echo .NET (%netfx%) is installed >> %startuptasklog%

    :end
    echo install.cmd completed: %date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2% >> %startuptasklog%

    :exit
    EXIT /B 0
    ```
   
   > [!NOTE]
   > <span data-ttu-id="28b7c-151">Le script suivant montre comment tooinstall .NET 4.5.2 ou version 4.6 pour la continuité des activités, même si .NET 4.5.2 est déjà disponible sur hello du système d’exploitation invité de Azure.</span><span class="sxs-lookup"><span data-stu-id="28b7c-151">This script shows how tooinstall .NET 4.5.2 or version 4.6 for continuity, even though .NET 4.5.2 is already available on hello Azure Guest OS.</span></span> <span data-ttu-id="28b7c-152">Vous devez installer directement .NET 4.6.1 plutôt que la version 4.6, comme décrit dans hello [l’article de la Base de connaissances 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="28b7c-152">You should directly install .NET 4.6.1 rather than version 4.6, as described in hello [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
   > 
   > 

3. <span data-ttu-id="28b7c-153">Ajouter hello install.cmd fichier tooeach un rôle à l’aide de **ajouter** > **élément existant** dans **l’Explorateur de solutions** comme décrit précédemment dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="28b7c-153">Add hello install.cmd file tooeach role by using **Add** > **Existing Item** in **Solution Explorer** as described earlier in this topic.</span></span> 

    <span data-ttu-id="28b7c-154">Une fois cette étape terminée, tous les rôles doivent avoir de fichier du programme d’installation .NET hello et de fichier du fichier install.cmd hello.</span><span class="sxs-lookup"><span data-stu-id="28b7c-154">After this step is complete, all roles should have hello .NET installer file and hello install.cmd file.</span></span>

   ![Contenu du rôle avec tous les fichiers][2]

## <a name="configure-diagnostics-tootransfer-startup-logs-tooblob-storage"></a><span data-ttu-id="28b7c-156">Configurer le stockage de Diagnostics tootransfer démarrage journaux tooBlob</span><span class="sxs-lookup"><span data-stu-id="28b7c-156">Configure Diagnostics tootransfer startup logs tooBlob storage</span></span>
<span data-ttu-id="28b7c-157">toosimplify résolution des problèmes d’installation, vous pouvez configurer les Diagnostics Azure tootransfer tous les fichiers journaux générés par le démarrage de hello générer un script ou hello du stockage d’objets Blob tooAzure .NET programme d’installation.</span><span class="sxs-lookup"><span data-stu-id="28b7c-157">toosimplify troubleshooting installation issues, you can configure Azure Diagnostics tootransfer any log files generated by hello startup script or hello .NET installer tooAzure Blob storage.</span></span> <span data-ttu-id="28b7c-158">À l’aide de cette approche, vous pouvez afficher des journaux de hello en téléchargeant des fichiers journaux hello depuis le stockage Blob au lieu d’utiliser le bureau tooremote dans le rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="28b7c-158">By using this approach, you can view hello logs by downloading hello log files from Blob storage rather than having tooremote desktop into hello role.</span></span>

<span data-ttu-id="28b7c-159">tooconfigure Diagnostics, ouvrez le fichier diagnostics.wadcfgx de hello et ajouter hello suivant le contenu de hello **répertoires** nœud :</span><span class="sxs-lookup"><span data-stu-id="28b7c-159">tooconfigure Diagnostics, open hello diagnostics.wadcfgx file and add hello following content under hello **Directories** node:</span></span> 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

<span data-ttu-id="28b7c-160">Ce code XML configure les fichiers de diagnostic tootransfer hello dans le répertoire du journal hello Bonjour **NETFXInstall** ressource toohello compte de stockage de Diagnostics dans hello **installer netfx** conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="28b7c-160">This XML configures Diagnostics tootransfer hello files in hello log directory in hello **NETFXInstall** resource toohello Diagnostics storage account in hello **netfx-install** blob container.</span></span>

## <a name="deploy-your-cloud-service"></a><span data-ttu-id="28b7c-161">Déployer votre service cloud</span><span class="sxs-lookup"><span data-stu-id="28b7c-161">Deploy your cloud service</span></span>
<span data-ttu-id="28b7c-162">Lorsque vous déployez votre service cloud, les tâches de démarrage hello installer hello .NET Framework s’il n’est pas déjà installé.</span><span class="sxs-lookup"><span data-stu-id="28b7c-162">When you deploy your cloud service, hello startup tasks install hello .NET Framework if it's not already installed.</span></span> <span data-ttu-id="28b7c-163">Rôles de votre service cloud sont Bonjour *occupé* d’état pendant l’installation de framework de hello.</span><span class="sxs-lookup"><span data-stu-id="28b7c-163">Your cloud service roles are in hello *busy* state while hello framework is being installed.</span></span> <span data-ttu-id="28b7c-164">Si l’installation de framework hello nécessite un redémarrage, les rôles de service hello peuvent également redémarrer.</span><span class="sxs-lookup"><span data-stu-id="28b7c-164">If hello framework installation requires a restart, hello service roles might also restart.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="28b7c-165">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="28b7c-165">Additional resources</span></span>
* <span data-ttu-id="28b7c-166">[Hello lors de l’installation .NET Framework][Installing hello .NET Framework]</span><span class="sxs-lookup"><span data-stu-id="28b7c-166">[Installing hello .NET Framework][Installing hello .NET Framework]</span></span>
* <span data-ttu-id="28b7c-167">[Identifier les versions de .NET Framework installées][How to: Determine Which .NET Framework Versions Are Installed]</span><span class="sxs-lookup"><span data-stu-id="28b7c-167">[Determine which .NET Framework versions are installed][How to: Determine Which .NET Framework Versions Are Installed]</span></span>
* <span data-ttu-id="28b7c-168">[Résolution des problèmes liés aux installations de .NET Framework][Troubleshooting .NET Framework Installations]</span><span class="sxs-lookup"><span data-stu-id="28b7c-168">[Troubleshooting .NET Framework installations][Troubleshooting .NET Framework Installations]</span></span>

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing hello .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
