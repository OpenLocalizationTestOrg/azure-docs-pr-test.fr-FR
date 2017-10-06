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
# <a name="install-net-on-azure-cloud-services-roles"></a>Installer .NET sur des rôles d’Azure Cloud Services
Cet article décrit comment tooinstall les versions du .NET Framework qui ne comportent pas de hello du système d’exploitation invité de Azure. Vous pouvez utiliser .NET sur tooconfigure de système d’exploitation invité hello vos rôles web et de travail du service cloud.

Par exemple, vous pouvez installer le .NET 4.6.1 sur hello famille de système d’exploitation invité 4, ce qui n’est fourni avec une version de .NET 4.6. (hello famille de système d’exploitation invité 5 n’est fourni avec .NET 4.6.) Pour plus d’informations plus récentes hello sur hello mises à jour de système d’exploitation invité de Azure, consultez hello [informations de version du système d’exploitation invité de Azure](cloud-services-guestos-update-matrix.md). 

>[!IMPORTANT]
>Bonjour Azure SDK 2.9 contient une restriction sur le déploiement de .NET 4.6 sur la famille de systèmes d’exploitation invités hello 4 ou une version antérieure. Un correctif pour la restriction de hello est disponible sur hello [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.

tooinstall .NET sur vos rôles web et de travail, incluent le programme d’installation de web de .NET hello dans le cadre de votre projet de service cloud. Démarrer le programme d’installation de hello en tant que partie de du rôle hello tâches de démarrage. 

## <a name="add-hello-net-installer-tooyour-project"></a>Ajouter un projet de tooyour de programme d’installation de .NET hello
toodownload hello web programme d’installation pour hello .NET Framework, choisissez la version hello que vous souhaitez tooinstall :

* [Programme d’installation web de .NET 4.7](http://go.microsoft.com/fwlink/?LinkId=825298)
* [Programme d’installation web de.NET 4.6.1](http://go.microsoft.com/fwlink/?LinkId=671729)

programme d’installation de tooadd hello pour un *web* rôle :
  1. Dans l’**Explorateur de solutions**, dans votre projet de service cloud, sous **Rôles**, cliquez avec le bouton droit sur votre rôle *web*, puis sélectionnez **Ajouter** > **Nouveau dossier**. Créez un dossier intitulé **bin**.
  2. Cliquez sur le dossier bin de hello et sélectionnez **ajouter** > **élément existant**. Sélectionnez le programme d’installation de .NET hello et ajouter le dossier bin de toohello.
  
programme d’installation de tooadd hello pour un *travail* rôle :
* Cliquez avec le bouton droit sur votre rôle *de travail*, puis sélectionnez **Ajouter** > **Élément existant**. Sélectionnez le programme d’installation de .NET hello et ajoutez-le toohello rôle. 

Lorsque les fichiers sont ajoutés dans ce dossier de contenu de façon toohello rôle, elles sont automatiquement ajoutées tooyour package de service cloud. Hello les fichiers sont ensuite emplacement cohérent de tooa déployé sur l’ordinateur virtuel de hello. Répétez ce processus pour chaque rôle web et de travail dans votre service cloud afin que tous les rôles de disposer d’une copie du programme d’installation hello.

> [!NOTE]
> Même si votre application cible .NET 4.6, nous vous conseillons d’installer .NET 4.6.1 sur votre rôle de service cloud. Hello du système d’exploitation invité inclut hello Base de connaissances [mettre à jour 3098779](https://support.microsoft.com/kb/3098779) et [mettre à jour 3097997](https://support.microsoft.com/kb/3097997). Problèmes peuvent se produire lorsque vous exécutez vos applications .NET si .NET 4.6 est installé sur les mises à jour de la Base de connaissances hello. tooavoid ces problèmes, installez le .NET 4.6.1 plutôt que la version 4.6. Pour plus d’informations, consultez hello [l’article de la Base de connaissances 3118750](https://support.microsoft.com/kb/3118750).
> 
> 

![Contenu du rôle avec les fichiers d'installation][1]

## <a name="define-startup-tasks-for-your-roles"></a>Définir des tâches de démarrage pour vos rôles
Vous pouvez utiliser les opérations de tooperform de tâches de démarrage avant le démarrage d’un rôle. L’installation hello .NET Framework comme partie de la tâche de démarrage hello garantit que framework hello est installé avant l’exécution de tout code d’application. Pour plus d’informations sur les tâches de démarrage, consultez [Exécuter des tâches de démarrage dans Azure](cloud-services-startup-tasks.md). 

1. Ajouter hello contenu toohello le fichier ServiceDefinition.csdef sous hello suivant **WebRole** ou **WorkerRole** nœud pour tous les rôles :
   
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
   
    commande de console hello exécute Hello précédente configuration `install.cmd` avec tooinstall de privilèges d’administrateur hello .NET Framework. configuration de Hello crée également un **LocalStorage** élément nommé **NETFXInstall**. script de démarrage Hello définit hello dossier temporaire toouse cette ressource de stockage local. 
    
    > [!IMPORTANT]
    > tooensure corriger l’installation de framework hello, taille hello du jeu de tooat de cette ressource moins 1 024 Mo.
    
    Pour plus d’informations sur les tâches de démarrage, consultez [Tâches courantes de démarrage dans Azure Cloud Services](cloud-services-startup-tasks-common.md).

2. Créez un fichier nommé **install.cmd** et ajoutez suivant de hello installer le fichier de script toohello.

    script de Hello vérifie si version spécifiée de hello Hello .NET Framework est déjà installée sur l’ordinateur de hello en interrogeant le Registre de hello. Si la version de .NET hello n’est pas installée, le programme d’installation web hello .NET est ouvert. toohelp résoudre les problèmes, le script de hello enregistre toutes les activités toohello fichier startuptasklog-(date et heure actuelles) .txt stocké dans **InstallLogs** stockage local.

    > [!IMPORTANT]
    > Utilisez un éditeur de texte simple comme bloc-notes Windows toocreate hello install.cmd fichier. Si vous utilisez Visual Studio toocreate un fichier texte et que vous modifiez hello extension too.cmd, fichier de hello peut présenter une marque d’ordre UTF-8. Cette marque peut provoquer une erreur lors de l’exécution de hello première ligne du script de hello. tooavoid cette erreur, assurez-vous hello première ligne de hello une instruction REM qui peut être ignorée par le traitement des commandes hello octets de script. 
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
   > Le script suivant montre comment tooinstall .NET 4.5.2 ou version 4.6 pour la continuité des activités, même si .NET 4.5.2 est déjà disponible sur hello du système d’exploitation invité de Azure. Vous devez installer directement .NET 4.6.1 plutôt que la version 4.6, comme décrit dans hello [l’article de la Base de connaissances 3118750](https://support.microsoft.com/kb/3118750).
   > 
   > 

3. Ajouter hello install.cmd fichier tooeach un rôle à l’aide de **ajouter** > **élément existant** dans **l’Explorateur de solutions** comme décrit précédemment dans cette rubrique. 

    Une fois cette étape terminée, tous les rôles doivent avoir de fichier du programme d’installation .NET hello et de fichier du fichier install.cmd hello.

   ![Contenu du rôle avec tous les fichiers][2]

## <a name="configure-diagnostics-tootransfer-startup-logs-tooblob-storage"></a>Configurer le stockage de Diagnostics tootransfer démarrage journaux tooBlob
toosimplify résolution des problèmes d’installation, vous pouvez configurer les Diagnostics Azure tootransfer tous les fichiers journaux générés par le démarrage de hello générer un script ou hello du stockage d’objets Blob tooAzure .NET programme d’installation. À l’aide de cette approche, vous pouvez afficher des journaux de hello en téléchargeant des fichiers journaux hello depuis le stockage Blob au lieu d’utiliser le bureau tooremote dans le rôle de hello.

tooconfigure Diagnostics, ouvrez le fichier diagnostics.wadcfgx de hello et ajouter hello suivant le contenu de hello **répertoires** nœud : 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

Ce code XML configure les fichiers de diagnostic tootransfer hello dans le répertoire du journal hello Bonjour **NETFXInstall** ressource toohello compte de stockage de Diagnostics dans hello **installer netfx** conteneur d’objets blob.

## <a name="deploy-your-cloud-service"></a>Déployer votre service cloud
Lorsque vous déployez votre service cloud, les tâches de démarrage hello installer hello .NET Framework s’il n’est pas déjà installé. Rôles de votre service cloud sont Bonjour *occupé* d’état pendant l’installation de framework de hello. Si l’installation de framework hello nécessite un redémarrage, les rôles de service hello peuvent également redémarrer. 

## <a name="additional-resources"></a>Ressources supplémentaires
* [Hello lors de l’installation .NET Framework][Installing hello .NET Framework]
* [Identifier les versions de .NET Framework installées][How to: Determine Which .NET Framework Versions Are Installed]
* [Résolution des problèmes liés aux installations de .NET Framework][Troubleshooting .NET Framework Installations]

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing hello .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
