---
title: aaaGet route de Python et des Services de cloud computing Azure | Documents Microsoft
description: "Vue d’ensemble de l’utilisation des outils Python pour Visual Studio toocreate Azure cloud services, y compris les rôles web et worker."
services: cloud-services
documentationcenter: python
author: thraka
manager: timlt
editor: 
ms.assetid: 5489405d-6fa9-4b11-a161-609103cbdc18
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: f5fd85e754839f146abe912351c59dc4a148c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="python-web-and-worker-roles-with-python-tools-for-visual-studio"></a>Rôles Web et rôles de travail Python avec Python Tools pour Visual Studio

Cet article fournit une vue d’ensemble de l’utilisation des rôles Web et de travail Python avec [Python Tools pour Visual Studio][Python Tools for Visual Studio]. Découvrez comment toouse Visual Studio toocreate et déployer un Service Cloud de base qui utilise les Python.

## <a name="prerequisites"></a>Composants requis
* [Visual Studio 2013, 2015 ou 2017](https://www.visualstudio.com/)
* [Python Tools pour Visual Studio][Python Tools for Visual Studio] (PTVS)
* [Outils du Kit de développement logiciel (SDK) Azure pour Visual Studio 2013][Azure SDK Tools for VS 2013] ou  
[Outils du Kit de développement logiciel (SDK) Azure pour Visual Studio 2015][Azure SDK Tools for VS 2015] ou  
[Outils du Kit de développement logiciel (SDK) Azure pour Visual Studio 2017][Azure SDK Tools for VS 2017]
* [Python 2.7 32 bits][Python 2.7 32-bit] ou [Python 3.5 32 bits][Python 3.5 32-bit]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-are-python-web-and-worker-roles"></a>Présentation des rôles web et de travail Python
Azure propose trois modèles de calcul pour l’exécution d’applications : [fonctionnalité Web Apps dans Azure App Service][execution model-web sites], [Machines Virtuelles Azure][execution model-vms] et [Azure Cloud Services][execution model-cloud services]. Ils prennent tous les trois en charge Python. Azure Cloud Services, qui inclut les rôles Web et de travail, fournit la fonctionnalité *PaaS (Platform as a Service)*. Dans un service cloud, un rôle web fournit une dédié du frontal web Internet Information Services (IIS) web server toohost applications, lors d’un rôle de travail peut exécuter des tâches asynchrones, longues ou perpétuelles indépendantes de l’intervention de l’utilisateur ou entrée.

Pour en savoir plus, voir [Présentation d’un service Cloud].

> [!NOTE]
> *Recherchez toobuild un site Web simple ?*
> Si votre scénario implique simplement un simple site Web frontal, envisagez d’utiliser la fonctionnalité d’applications Web légère hello dans Azure App Service. Vous pouvez facilement mettre à niveau tooa Service Cloud croissance de votre site Web et à vos besoins. Consultez hello <a href="/develop/python/">centre de développement Python</a> pour les articles qui couvrent le développement de la fonctionnalité d’applications Web hello dans Azure App Service.
> <br />
> 
> 

## <a name="project-creation"></a>Création du projet
Dans Visual Studio, vous pouvez sélectionner **Azure Cloud Service** Bonjour **nouveau projet** boîte de dialogue **Python**.

![Boîte de dialogue Nouveau projet](./media/cloud-services-python-ptvs/new-project-cloud-service.png)

Dans l’Assistant d’Azure Cloud Service hello, vous pouvez créer un site web et les rôles de travail.

![Azure Cloud Service Dialog](./media/cloud-services-python-ptvs/new-service-wizard.png)

modèle de rôle de travail Hello est fourni avec le code réutilisable code tooconnect tooan compte de stockage Azure ou Azure Service Bus.

![Cloud Service Solution](./media/cloud-services-python-ptvs/worker.png)

Vous pouvez ajouter le web ou travail rôles tooan service cloud existant à tout moment.  Vous pouvez choisir de tooadd des projets existants dans votre solution, ou créer de nouveaux.

![Add Role Command](./media/cloud-services-python-ptvs/add-new-or-existing-role.png)

Votre service cloud peut contenir des rôles dans différents langages.  Par exemple, vous pouvez avoir un rôle web Python implémenté à l'aide de Django, avec des rôles de travail Python ou C#.  Vous pouvez assurer la communication entre les rôles grâce aux files d'attente Service Bus ou aux files d'attente de stockage.

## <a name="install-python-on-hello-cloud-service"></a>Installer Python sur le service de cloud computing hello
> [!WARNING]
> les scripts de configuration Hello qui sont installés avec Visual Studio (au moment de hello que dernière mise à jour de cet article) ne fonctionnent pas. Cette section décrit comment contourner le problème.
> 
> 

Hello principal problème avec les scripts de configuration hello est qu’ils n’installent pas les python. Tout d’abord définir deux [tâches de démarrage](cloud-services-startup-tasks.md) Bonjour [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) fichier. tâche première Hello (**PrepPython.ps1**) télécharge et installe le runtime de Python hello. tâche deuxième Hello (**PipInstaller.ps1**) s’exécute pip tooinstall toutes les dépendances que vous avez peut-être.

Hello scripts suivants ont été écrits ciblage Python 3.5. Si vous voulez toouse hello version 2.x de python, jeu hello **PYTHON2** variable trop de fichiers**sur** pour les tâches de démarrage hello deux et la tâche d’exécution hello : `<Variable name="PYTHON2" value="<mark>on</mark>" />`.

```xml
<Startup>

  <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PrepPython.ps1">
    <Environment>
      <Variable name="EMULATED">
        <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
      </Variable>
      <Variable name="PYTHON2" value="off" />
    </Environment>
  </Task>

  <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PipInstaller.ps1">
    <Environment>
      <Variable name="EMULATED">
        <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
      </Variable>
      <Variable name="PYTHON2" value="off" />
    </Environment>

  </Task>

</Startup>
```

Hello **PYTHON2** et **PYPATH** variables doivent être ajoutés en tâche de démarrage du processus de travail toohello. Hello **PYPATH** variable est utilisée uniquement si hello **PYTHON2** sa valeur est trop**sur**.

```xml
<Runtime>
  <Environment>
    <Variable name="EMULATED">
      <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
    </Variable>
    <Variable name="PYTHON2" value="off" />
    <Variable name="PYPATH" value="%SystemDrive%\Python27" />
  </Environment>
  <EntryPoint>
    <ProgramEntryPoint commandLine="bin\ps.cmd LaunchWorker.ps1" setReadyOnProcessStart="true" />
  </EntryPoint>
</Runtime>
```

#### <a name="sample-servicedefinitioncsdef"></a>Exemple de fichier ServiceDefinition.csdef
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="AzureCloudServicePython" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2015-04.2.6">
  <WorkerRole name="WorkerRole1" vmsize="Small">
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" />
      <Setting name="Python2" />
    </ConfigurationSettings>
    <Startup>
      <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PrepPython.ps1">
        <Environment>
          <Variable name="EMULATED">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
          <Variable name="PYTHON2" value="off" />
        </Environment>
      </Task>
      <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PipInstaller.ps1">
        <Environment>
          <Variable name="EMULATED">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
          <Variable name="PYTHON2" value="off" />
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="EMULATED">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
        </Variable>
        <Variable name="PYTHON2" value="off" />
        <Variable name="PYPATH" value="%SystemDrive%\Python27" />
      </Environment>
      <EntryPoint>
        <ProgramEntryPoint commandLine="bin\ps.cmd LaunchWorker.ps1" setReadyOnProcessStart="true" />
      </EntryPoint>
    </Runtime>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
  </WorkerRole>
</ServiceDefinition>
```



Ensuite, créez hello **PrepPython.ps1** et **PipInstaller.ps1** fichiers Bonjour **. / bin** dossier de votre rôle.

#### <a name="preppythonps1"></a>PrepPython.ps1
Ce script installe Python. Si hello **PYTHON2** variable d’environnement est définie trop**sur**, puis Python 2.7 est installée, sinon les Python 3.5 est installé.

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated){
    Write-Output "Checking if python is installed...$nl"
    if ($is_python2) {
        & "${env:SystemDrive}\Python27\python.exe"  -V | Out-Null
    }
    else {
        py -V | Out-Null
    }

    if (-not $?) {

        $url = "https://www.python.org/ftp/python/3.5.2/python-3.5.2-amd64.exe"
        $outFile = "${env:TEMP}\python-3.5.2-amd64.exe"

        if ($is_python2) {
            $url = "https://www.python.org/ftp/python/2.7.12/python-2.7.12.amd64.msi"
            $outFile = "${env:TEMP}\python-2.7.12.amd64.msi"
        }

        Write-Output "Not found, downloading $url too$outFile$nl"
        Invoke-WebRequest $url -OutFile $outFile
        Write-Output "Installing$nl"

        if ($is_python2) {
            Start-Process msiexec.exe -ArgumentList "/q", "/i", "$outFile", "ALLUSERS=1" -Wait
        }
        else {
            Start-Process "$outFile" -ArgumentList "/quiet", "InstallAllUsers=1" -Wait
        }

        Write-Output "Done$nl"
    }
    else {
        Write-Output "Already installed"
    }
}
```

#### <a name="pipinstallerps1"></a>PipInstaller.ps1
Ce script appelle pip et installe toutes les dépendances de hello Bonjour **requirements.txt** fichier. Si hello **PYTHON2** variable d’environnement est définie trop**sur**, puis Python 2.7 est utilisé, sinon les Python 3.5 est utilisée.

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated){
    Write-Output "Checking if requirements.txt exists$nl"
    if (Test-Path ..\requirements.txt) {
        Write-Output "Found. Processing pip$nl"

        if ($is_python2) {
            & "${env:SystemDrive}\Python27\python.exe" -m pip install -r ..\requirements.txt
        }
        else {
            py -m pip install -r ..\requirements.txt
        }

        Write-Output "Done$nl"
    }
    else {
        Write-Output "Not found$nl"
    }
}
```

#### <a name="modify-launchworkerps1"></a>Modifier LaunchWorker.ps1
> [!NOTE]
> Dans les cas de hello d’un **rôle** projet, **LauncherWorker.ps1** fichier est requis tooexecute hello démarrage du fichier. Dans un **rôle web** projet d’équipe, hello fichier de démarrage est à la place définie dans les propriétés du projet hello.
> 
> 

Hello **bin\LaunchWorker.ps1** toodo une grande quantité de travail, mais il ne fonctionne pas réellement créé. Remplacez le contenu hello dans ce fichier avec hello script suivant.

Ce script appelle hello **worker.py** fichier à partir de votre projet de python. Si hello **PYTHON2** variable d’environnement est définie trop**sur**, puis Python 2.7 est utilisé, sinon les Python 3.5 est utilisée.

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated)
{
    Write-Output "Running worker.py$nl"

    if ($is_python2) {
        cd..
        iex "$env:PYPATH\python.exe worker.py"
    }
    else {
        cd..
        iex "py worker.py"
    }
}
else
{
    Write-Output "Running (EMULATED) worker.py$nl"

    # Customize tooyour local dev environment

    if ($is_python2) {
        cd..
        iex "$env:PYPATH\python.exe worker.py"
    }
    else {
        cd..
        iex "py worker.py"
    }
}
```

#### <a name="pscmd"></a>ps.cmd
modèles de Visual Studio Hello doivent avoir créé un **ps.cmd** fichier Bonjour **. / bin** dossier. Ce script de shell appelle hello PowerShell scripts wrapper ci-dessus et fournit la journalisation basée sur nom hello hello PowerShell wrapper est appelée. Si ce fichier n’a pas été créé, voici ce qu’il doit contenir. 

```bat
@echo off

cd /D %~dp0

if not exist "%DiagnosticStore%\LogFiles" mkdir "%DiagnosticStore%\LogFiles"
%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Unrestricted -File %* >> "%DiagnosticStore%\LogFiles\%~n1.txt" 2>> "%DiagnosticStore%\LogFiles\%~n1.err.txt"
```



## <a name="run-locally"></a>Exécution locale
Si vous définissez votre projet de service cloud comme projet de démarrage hello et appuyez sur F5, le service cloud hello s’exécute dans l’émulateur de Azure local hello.

PTVS prend en charge du lancement dans l’émulateur hello, débogage (par exemple, points d’arrêt) ne fonctionne pas.

toodebug vos rôles web et de travail, vous pouvez définir le projet de rôle hello en tant que projet de démarrage hello et que, au lieu de débogage.  Vous pouvez aussi définir plusieurs projets de démarrage.  Solution de hello d’avec le bouton droit, puis sélectionnez **définir les projets de démarrage**.

![Solution Startup Project Properties](./media/cloud-services-python-ptvs/startup.png)

## <a name="publish-tooazure"></a>Publication tooAzure
toopublish, cliquez sur le projet de service cloud hello dans la solution de hello, puis sélectionnez **publier**.

![Microsoft Azure Publish Sign In](./media/cloud-services-python-ptvs/publish-sign-in.png)

Suivez l’Assistant de hello. En cas de besoin, activez le Bureau à distance. Bureau à distance est utile lorsque vous devez toodebug quelque chose.

Une fois que vous avez terminé la configuration des paramètres, cliquez sur **Publier**.

Certains progression s’affiche dans la fenêtre de sortie hello, puis vous verrez la fenêtre du journal des activités Microsoft Azure hello.

![Microsoft Azure Activity Log Window](./media/cloud-services-python-ptvs/publish-activity-log.png)

Déploiement prend plusieurs minutes toocomplete, puis sur votre site web et/ou les rôles de travail s’exécutent sur Azure !

### <a name="investigate-logs"></a>Examiner les journaux
Une fois que l’ordinateur virtuel du service de cloud hello démarre et installe les Python, vous pouvez examiner hello journaux toofind messages d’échec. Ces journaux sont situés dans hello **C:\Resources\Directory\\{rôle} \LogFiles** dossier. **PrepPython.err.txt** comporte au moins une erreur à partir de lorsque le script de hello tente toodetect si Python est installé et **PipInstaller.err.txt** peuvent se plaindre une version obsolète du pip.

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des informations plus détaillées sur l’utilisation des rôles web et de travail dans les outils Python pour Visual Studio, consultez la documentation de PTVS hello :

* [Projets de service cloud][Cloud Service Projects]

Pour plus d’informations sur l’utilisation des services Azure à partir de vos rôles web et de travail, telles que l’utilisation d’Azure Storage ou Service Bus, consultez hello suivant des articles :

* [service BLOB][Blob Service]
* [Service de Table][Table Service]
* [Service de File d’attente][Queue Service]
* [Files d’attente Service Bus][Service Bus Queues]
* [Rubriques de Service Bus][Service Bus Topics]

<!--Link references-->

[Présentation d’un service Cloud]: cloud-services-choose-me.md
[execution model-web sites]: ../app-service-web/app-service-web-overview.md
[execution model-vms]:../virtual-machines/windows/overview.md
[execution model-cloud services]: cloud-services-choose-me.md
[Python Developer Center]: /develop/python/

[Blob Service]:../storage/blobs/storage-python-how-to-use-blob-storage.md
[Queue Service]: ../storage/queues/storage-python-how-to-use-queue-storage.md
[Table Service]:../cosmos-db/table-storage-how-to-use-python.md
[Service Bus Queues]: ../service-bus-messaging/service-bus-python-how-to-use-queues.md
[Service Bus Topics]: ../service-bus-messaging/service-bus-python-how-to-use-topics-subscriptions.md


<!--External Link references-->

[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs
[Cloud Service Projects]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure SDK Tools for VS 2013]: http://go.microsoft.com/fwlink/?LinkId=746482
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=746481
[Azure SDK Tools for VS 2017]: http://go.microsoft.com/fwlink/?LinkId=746483
[Python 2.7 32-bit]: https://www.python.org/downloads/
[Python 3.5 32-bit]: https://www.python.org/downloads/
