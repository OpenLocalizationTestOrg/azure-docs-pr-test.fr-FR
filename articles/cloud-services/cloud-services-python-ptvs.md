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
# <a name="python-web-and-worker-roles-with-python-tools-for-visual-studio"></a><span data-ttu-id="b89a1-103">Rôles Web et rôles de travail Python avec Python Tools pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b89a1-103">Python web and worker roles with Python Tools for Visual Studio</span></span>

<span data-ttu-id="b89a1-104">Cet article fournit une vue d’ensemble de l’utilisation des rôles Web et de travail Python avec [Python Tools pour Visual Studio][Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="b89a1-104">This article provides an overview of using Python web and worker roles using [Python Tools for Visual Studio][Python Tools for Visual Studio].</span></span> <span data-ttu-id="b89a1-105">Découvrez comment toouse Visual Studio toocreate et déployer un Service Cloud de base qui utilise les Python.</span><span class="sxs-lookup"><span data-stu-id="b89a1-105">Learn how toouse Visual Studio toocreate and deploy a basic Cloud Service that uses Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b89a1-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b89a1-106">Prerequisites</span></span>
* [<span data-ttu-id="b89a1-107">Visual Studio 2013, 2015 ou 2017</span><span class="sxs-lookup"><span data-stu-id="b89a1-107">Visual Studio 2013, 2015, or 2017</span></span>](https://www.visualstudio.com/)
* <span data-ttu-id="b89a1-108">[Python Tools pour Visual Studio][Python Tools for Visual Studio] (PTVS)</span><span class="sxs-lookup"><span data-stu-id="b89a1-108">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)</span></span>
* <span data-ttu-id="b89a1-109">[Outils du Kit de développement logiciel (SDK) Azure pour Visual Studio 2013][Azure SDK Tools for VS 2013] ou</span><span class="sxs-lookup"><span data-stu-id="b89a1-109">[Azure SDK Tools for VS 2013][Azure SDK Tools for VS 2013] or</span></span>  
<span data-ttu-id="b89a1-110">[Outils du Kit de développement logiciel (SDK) Azure pour Visual Studio 2015][Azure SDK Tools for VS 2015] ou</span><span class="sxs-lookup"><span data-stu-id="b89a1-110">[Azure SDK Tools for VS 2015][Azure SDK Tools for VS 2015] or</span></span>  
<span data-ttu-id="b89a1-111">[Outils du Kit de développement logiciel (SDK) Azure pour Visual Studio 2017][Azure SDK Tools for VS 2017]</span><span class="sxs-lookup"><span data-stu-id="b89a1-111">[Azure SDK Tools for VS 2017][Azure SDK Tools for VS 2017]</span></span>
* <span data-ttu-id="b89a1-112">[Python 2.7 32 bits][Python 2.7 32-bit] ou [Python 3.5 32 bits][Python 3.5 32-bit]</span><span class="sxs-lookup"><span data-stu-id="b89a1-112">[Python 2.7 32-bit][Python 2.7 32-bit] or [Python 3.5 32-bit][Python 3.5 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-are-python-web-and-worker-roles"></a><span data-ttu-id="b89a1-113">Présentation des rôles web et de travail Python</span><span class="sxs-lookup"><span data-stu-id="b89a1-113">What are Python web and worker roles?</span></span>
<span data-ttu-id="b89a1-114">Azure propose trois modèles de calcul pour l’exécution d’applications : [fonctionnalité Web Apps dans Azure App Service][execution model-web sites], [Machines Virtuelles Azure][execution model-vms] et [Azure Cloud Services][execution model-cloud services].</span><span class="sxs-lookup"><span data-stu-id="b89a1-114">Azure provides three compute models for running applications: [Web Apps feature in Azure App Service][execution model-web sites], [Azure Virtual Machines][execution model-vms], and [Azure Cloud Services][execution model-cloud services].</span></span> <span data-ttu-id="b89a1-115">Ils prennent tous les trois en charge Python.</span><span class="sxs-lookup"><span data-stu-id="b89a1-115">All three models support Python.</span></span> <span data-ttu-id="b89a1-116">Azure Cloud Services, qui inclut les rôles Web et de travail, fournit la fonctionnalité *PaaS (Platform as a Service)*.</span><span class="sxs-lookup"><span data-stu-id="b89a1-116">Cloud Services, which include web and worker roles, provide *Platform as a Service (PaaS)*.</span></span> <span data-ttu-id="b89a1-117">Dans un service cloud, un rôle web fournit une dédié du frontal web Internet Information Services (IIS) web server toohost applications, lors d’un rôle de travail peut exécuter des tâches asynchrones, longues ou perpétuelles indépendantes de l’intervention de l’utilisateur ou entrée.</span><span class="sxs-lookup"><span data-stu-id="b89a1-117">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server toohost front end web applications, while a worker role can run asynchronous, long-running, or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="b89a1-118">Pour en savoir plus, voir [Présentation d’un service Cloud].</span><span class="sxs-lookup"><span data-stu-id="b89a1-118">For more information, see [What is a Cloud Service?].</span></span>

> [!NOTE]
> <span data-ttu-id="b89a1-119">*Recherchez toobuild un site Web simple ?*</span><span class="sxs-lookup"><span data-stu-id="b89a1-119">*Looking toobuild a simple website?*</span></span>
> <span data-ttu-id="b89a1-120">Si votre scénario implique simplement un simple site Web frontal, envisagez d’utiliser la fonctionnalité d’applications Web légère hello dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="b89a1-120">If your scenario involves just a simple website front end, consider using hello lightweight Web Apps feature in Azure App Service.</span></span> <span data-ttu-id="b89a1-121">Vous pouvez facilement mettre à niveau tooa Service Cloud croissance de votre site Web et à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="b89a1-121">You can easily upgrade tooa Cloud Service as your website grows and your requirements change.</span></span> <span data-ttu-id="b89a1-122">Consultez hello <a href="/develop/python/">centre de développement Python</a> pour les articles qui couvrent le développement de la fonctionnalité d’applications Web hello dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="b89a1-122">See hello <a href="/develop/python/">Python Developer Center</a> for articles that cover development of hello Web Apps feature in Azure App Service.</span></span>
> <br />
> 
> 

## <a name="project-creation"></a><span data-ttu-id="b89a1-123">Création du projet</span><span class="sxs-lookup"><span data-stu-id="b89a1-123">Project creation</span></span>
<span data-ttu-id="b89a1-124">Dans Visual Studio, vous pouvez sélectionner **Azure Cloud Service** Bonjour **nouveau projet** boîte de dialogue **Python**.</span><span class="sxs-lookup"><span data-stu-id="b89a1-124">In Visual Studio, you can select **Azure Cloud Service** in hello **New Project** dialog box, under **Python**.</span></span>

![Boîte de dialogue Nouveau projet](./media/cloud-services-python-ptvs/new-project-cloud-service.png)

<span data-ttu-id="b89a1-126">Dans l’Assistant d’Azure Cloud Service hello, vous pouvez créer un site web et les rôles de travail.</span><span class="sxs-lookup"><span data-stu-id="b89a1-126">In hello Azure Cloud Service wizard, you can create new web and worker roles.</span></span>

![Azure Cloud Service Dialog](./media/cloud-services-python-ptvs/new-service-wizard.png)

<span data-ttu-id="b89a1-128">modèle de rôle de travail Hello est fourni avec le code réutilisable code tooconnect tooan compte de stockage Azure ou Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="b89a1-128">hello worker role template comes with boilerplate code tooconnect tooan Azure storage account or Azure Service Bus.</span></span>

![Cloud Service Solution](./media/cloud-services-python-ptvs/worker.png)

<span data-ttu-id="b89a1-130">Vous pouvez ajouter le web ou travail rôles tooan service cloud existant à tout moment.</span><span class="sxs-lookup"><span data-stu-id="b89a1-130">You can add web or worker roles tooan existing cloud service at any time.</span></span>  <span data-ttu-id="b89a1-131">Vous pouvez choisir de tooadd des projets existants dans votre solution, ou créer de nouveaux.</span><span class="sxs-lookup"><span data-stu-id="b89a1-131">You can choose tooadd existing projects in your solution, or create new ones.</span></span>

![Add Role Command](./media/cloud-services-python-ptvs/add-new-or-existing-role.png)

<span data-ttu-id="b89a1-133">Votre service cloud peut contenir des rôles dans différents langages.</span><span class="sxs-lookup"><span data-stu-id="b89a1-133">Your cloud service can contain roles implemented in different languages.</span></span>  <span data-ttu-id="b89a1-134">Par exemple, vous pouvez avoir un rôle web Python implémenté à l'aide de Django, avec des rôles de travail Python ou C#.</span><span class="sxs-lookup"><span data-stu-id="b89a1-134">For example, you can have a Python web role implemented using Django, with Python, or with C# worker roles.</span></span>  <span data-ttu-id="b89a1-135">Vous pouvez assurer la communication entre les rôles grâce aux files d'attente Service Bus ou aux files d'attente de stockage.</span><span class="sxs-lookup"><span data-stu-id="b89a1-135">You can easily communicate between your roles using Service Bus queues or storage queues.</span></span>

## <a name="install-python-on-hello-cloud-service"></a><span data-ttu-id="b89a1-136">Installer Python sur le service de cloud computing hello</span><span class="sxs-lookup"><span data-stu-id="b89a1-136">Install Python on hello cloud service</span></span>
> [!WARNING]
> <span data-ttu-id="b89a1-137">les scripts de configuration Hello qui sont installés avec Visual Studio (au moment de hello que dernière mise à jour de cet article) ne fonctionnent pas.</span><span class="sxs-lookup"><span data-stu-id="b89a1-137">hello setup scripts that are installed with Visual Studio (at hello time this article was last updated) do not work.</span></span> <span data-ttu-id="b89a1-138">Cette section décrit comment contourner le problème.</span><span class="sxs-lookup"><span data-stu-id="b89a1-138">This section describes a workaround.</span></span>
> 
> 

<span data-ttu-id="b89a1-139">Hello principal problème avec les scripts de configuration hello est qu’ils n’installent pas les python.</span><span class="sxs-lookup"><span data-stu-id="b89a1-139">hello main problem with hello setup scripts is that they do not install python.</span></span> <span data-ttu-id="b89a1-140">Tout d’abord définir deux [tâches de démarrage](cloud-services-startup-tasks.md) Bonjour [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) fichier.</span><span class="sxs-lookup"><span data-stu-id="b89a1-140">First, define two [startup tasks](cloud-services-startup-tasks.md) in hello [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) file.</span></span> <span data-ttu-id="b89a1-141">tâche première Hello (**PrepPython.ps1**) télécharge et installe le runtime de Python hello.</span><span class="sxs-lookup"><span data-stu-id="b89a1-141">hello first task (**PrepPython.ps1**) downloads and installs hello Python runtime.</span></span> <span data-ttu-id="b89a1-142">tâche deuxième Hello (**PipInstaller.ps1**) s’exécute pip tooinstall toutes les dépendances que vous avez peut-être.</span><span class="sxs-lookup"><span data-stu-id="b89a1-142">hello second task (**PipInstaller.ps1**) runs pip tooinstall any dependencies you may have.</span></span>

<span data-ttu-id="b89a1-143">Hello scripts suivants ont été écrits ciblage Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="b89a1-143">hello following scripts were written targeting Python 3.5.</span></span> <span data-ttu-id="b89a1-144">Si vous voulez toouse hello version 2.x de python, jeu hello **PYTHON2** variable trop de fichiers**sur** pour les tâches de démarrage hello deux et la tâche d’exécution hello : `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span><span class="sxs-lookup"><span data-stu-id="b89a1-144">If you want toouse hello version 2.x of python, set hello **PYTHON2** variable file too**on** for hello two startup tasks and hello runtime task: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span></span>

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

<span data-ttu-id="b89a1-145">Hello **PYTHON2** et **PYPATH** variables doivent être ajoutés en tâche de démarrage du processus de travail toohello.</span><span class="sxs-lookup"><span data-stu-id="b89a1-145">hello **PYTHON2** and **PYPATH** variables must be added toohello worker startup task.</span></span> <span data-ttu-id="b89a1-146">Hello **PYPATH** variable est utilisée uniquement si hello **PYTHON2** sa valeur est trop**sur**.</span><span class="sxs-lookup"><span data-stu-id="b89a1-146">hello **PYPATH** variable is only used if hello **PYTHON2** variable is set too**on**.</span></span>

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

#### <a name="sample-servicedefinitioncsdef"></a><span data-ttu-id="b89a1-147">Exemple de fichier ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="b89a1-147">Sample ServiceDefinition.csdef</span></span>
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



<span data-ttu-id="b89a1-148">Ensuite, créez hello **PrepPython.ps1** et **PipInstaller.ps1** fichiers Bonjour **. / bin** dossier de votre rôle.</span><span class="sxs-lookup"><span data-stu-id="b89a1-148">Next, create hello **PrepPython.ps1** and **PipInstaller.ps1** files in hello **./bin** folder of your role.</span></span>

#### <a name="preppythonps1"></a><span data-ttu-id="b89a1-149">PrepPython.ps1</span><span class="sxs-lookup"><span data-stu-id="b89a1-149">PrepPython.ps1</span></span>
<span data-ttu-id="b89a1-150">Ce script installe Python.</span><span class="sxs-lookup"><span data-stu-id="b89a1-150">This script installs python.</span></span> <span data-ttu-id="b89a1-151">Si hello **PYTHON2** variable d’environnement est définie trop**sur**, puis Python 2.7 est installée, sinon les Python 3.5 est installé.</span><span class="sxs-lookup"><span data-stu-id="b89a1-151">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is installed, otherwise Python 3.5 is installed.</span></span>

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

#### <a name="pipinstallerps1"></a><span data-ttu-id="b89a1-152">PipInstaller.ps1</span><span class="sxs-lookup"><span data-stu-id="b89a1-152">PipInstaller.ps1</span></span>
<span data-ttu-id="b89a1-153">Ce script appelle pip et installe toutes les dépendances de hello Bonjour **requirements.txt** fichier.</span><span class="sxs-lookup"><span data-stu-id="b89a1-153">This script calls up pip and installs all of hello dependencies in hello **requirements.txt** file.</span></span> <span data-ttu-id="b89a1-154">Si hello **PYTHON2** variable d’environnement est définie trop**sur**, puis Python 2.7 est utilisé, sinon les Python 3.5 est utilisée.</span><span class="sxs-lookup"><span data-stu-id="b89a1-154">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

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

#### <a name="modify-launchworkerps1"></a><span data-ttu-id="b89a1-155">Modifier LaunchWorker.ps1</span><span class="sxs-lookup"><span data-stu-id="b89a1-155">Modify LaunchWorker.ps1</span></span>
> [!NOTE]
> <span data-ttu-id="b89a1-156">Dans les cas de hello d’un **rôle** projet, **LauncherWorker.ps1** fichier est requis tooexecute hello démarrage du fichier.</span><span class="sxs-lookup"><span data-stu-id="b89a1-156">In hello case of a **worker role** project, **LauncherWorker.ps1** file is required tooexecute hello startup file.</span></span> <span data-ttu-id="b89a1-157">Dans un **rôle web** projet d’équipe, hello fichier de démarrage est à la place définie dans les propriétés du projet hello.</span><span class="sxs-lookup"><span data-stu-id="b89a1-157">In a **web role** project, hello startup file is instead defined in hello project properties.</span></span>
> 
> 

<span data-ttu-id="b89a1-158">Hello **bin\LaunchWorker.ps1** toodo une grande quantité de travail, mais il ne fonctionne pas réellement créé.</span><span class="sxs-lookup"><span data-stu-id="b89a1-158">hello **bin\LaunchWorker.ps1** was originally created toodo a lot of prep work but it doesn't really work.</span></span> <span data-ttu-id="b89a1-159">Remplacez le contenu hello dans ce fichier avec hello script suivant.</span><span class="sxs-lookup"><span data-stu-id="b89a1-159">Replace hello contents in that file with hello following script.</span></span>

<span data-ttu-id="b89a1-160">Ce script appelle hello **worker.py** fichier à partir de votre projet de python.</span><span class="sxs-lookup"><span data-stu-id="b89a1-160">This script calls hello **worker.py** file from your python project.</span></span> <span data-ttu-id="b89a1-161">Si hello **PYTHON2** variable d’environnement est définie trop**sur**, puis Python 2.7 est utilisé, sinon les Python 3.5 est utilisée.</span><span class="sxs-lookup"><span data-stu-id="b89a1-161">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

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

#### <a name="pscmd"></a><span data-ttu-id="b89a1-162">ps.cmd</span><span class="sxs-lookup"><span data-stu-id="b89a1-162">ps.cmd</span></span>
<span data-ttu-id="b89a1-163">modèles de Visual Studio Hello doivent avoir créé un **ps.cmd** fichier Bonjour **. / bin** dossier.</span><span class="sxs-lookup"><span data-stu-id="b89a1-163">hello Visual Studio templates should have created a **ps.cmd** file in hello **./bin** folder.</span></span> <span data-ttu-id="b89a1-164">Ce script de shell appelle hello PowerShell scripts wrapper ci-dessus et fournit la journalisation basée sur nom hello hello PowerShell wrapper est appelée.</span><span class="sxs-lookup"><span data-stu-id="b89a1-164">This shell script calls out hello PowerShell wrapper scripts above and provides logging based on hello name of hello PowerShell wrapper called.</span></span> <span data-ttu-id="b89a1-165">Si ce fichier n’a pas été créé, voici ce qu’il doit contenir.</span><span class="sxs-lookup"><span data-stu-id="b89a1-165">If this file wasn't created, here is what should be in it.</span></span> 

```bat
@echo off

cd /D %~dp0

if not exist "%DiagnosticStore%\LogFiles" mkdir "%DiagnosticStore%\LogFiles"
%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Unrestricted -File %* >> "%DiagnosticStore%\LogFiles\%~n1.txt" 2>> "%DiagnosticStore%\LogFiles\%~n1.err.txt"
```



## <a name="run-locally"></a><span data-ttu-id="b89a1-166">Exécution locale</span><span class="sxs-lookup"><span data-stu-id="b89a1-166">Run locally</span></span>
<span data-ttu-id="b89a1-167">Si vous définissez votre projet de service cloud comme projet de démarrage hello et appuyez sur F5, le service cloud hello s’exécute dans l’émulateur de Azure local hello.</span><span class="sxs-lookup"><span data-stu-id="b89a1-167">If you set your cloud service project as hello startup project and press F5, hello cloud service runs in hello local Azure emulator.</span></span>

<span data-ttu-id="b89a1-168">PTVS prend en charge du lancement dans l’émulateur hello, débogage (par exemple, points d’arrêt) ne fonctionne pas.</span><span class="sxs-lookup"><span data-stu-id="b89a1-168">Although PTVS supports launching in hello emulator, debugging (for example, breakpoints) does not work.</span></span>

<span data-ttu-id="b89a1-169">toodebug vos rôles web et de travail, vous pouvez définir le projet de rôle hello en tant que projet de démarrage hello et que, au lieu de débogage.</span><span class="sxs-lookup"><span data-stu-id="b89a1-169">toodebug your web and worker roles, you can set hello role project as hello startup project and debug that instead.</span></span>  <span data-ttu-id="b89a1-170">Vous pouvez aussi définir plusieurs projets de démarrage.</span><span class="sxs-lookup"><span data-stu-id="b89a1-170">You can also set multiple startup projects.</span></span>  <span data-ttu-id="b89a1-171">Solution de hello d’avec le bouton droit, puis sélectionnez **définir les projets de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="b89a1-171">Right-click hello solution and then select **Set StartUp Projects**.</span></span>

![Solution Startup Project Properties](./media/cloud-services-python-ptvs/startup.png)

## <a name="publish-tooazure"></a><span data-ttu-id="b89a1-173">Publication tooAzure</span><span class="sxs-lookup"><span data-stu-id="b89a1-173">Publish tooAzure</span></span>
<span data-ttu-id="b89a1-174">toopublish, cliquez sur le projet de service cloud hello dans la solution de hello, puis sélectionnez **publier**.</span><span class="sxs-lookup"><span data-stu-id="b89a1-174">toopublish, right-click hello cloud service project in hello solution and then select **Publish**.</span></span>

![Microsoft Azure Publish Sign In](./media/cloud-services-python-ptvs/publish-sign-in.png)

<span data-ttu-id="b89a1-176">Suivez l’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="b89a1-176">Follow hello wizard.</span></span> <span data-ttu-id="b89a1-177">En cas de besoin, activez le Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="b89a1-177">If you need to, enable remote desktop.</span></span> <span data-ttu-id="b89a1-178">Bureau à distance est utile lorsque vous devez toodebug quelque chose.</span><span class="sxs-lookup"><span data-stu-id="b89a1-178">Remote desktop is helpful when you need toodebug something.</span></span>

<span data-ttu-id="b89a1-179">Une fois que vous avez terminé la configuration des paramètres, cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="b89a1-179">When you are done configuring settings, click **Publish**.</span></span>

<span data-ttu-id="b89a1-180">Certains progression s’affiche dans la fenêtre de sortie hello, puis vous verrez la fenêtre du journal des activités Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b89a1-180">Some progress appears in hello output window, then you'll see hello Microsoft Azure Activity Log window.</span></span>

![Microsoft Azure Activity Log Window](./media/cloud-services-python-ptvs/publish-activity-log.png)

<span data-ttu-id="b89a1-182">Déploiement prend plusieurs minutes toocomplete, puis sur votre site web et/ou les rôles de travail s’exécutent sur Azure !</span><span class="sxs-lookup"><span data-stu-id="b89a1-182">Deployment takes several minutes toocomplete, then your web and/or worker roles run on Azure!</span></span>

### <a name="investigate-logs"></a><span data-ttu-id="b89a1-183">Examiner les journaux</span><span class="sxs-lookup"><span data-stu-id="b89a1-183">Investigate logs</span></span>
<span data-ttu-id="b89a1-184">Une fois que l’ordinateur virtuel du service de cloud hello démarre et installe les Python, vous pouvez examiner hello journaux toofind messages d’échec.</span><span class="sxs-lookup"><span data-stu-id="b89a1-184">After hello cloud service virtual machine starts up and installs Python, you can look at hello logs toofind any failure messages.</span></span> <span data-ttu-id="b89a1-185">Ces journaux sont situés dans hello **C:\Resources\Directory\\{rôle} \LogFiles** dossier.</span><span class="sxs-lookup"><span data-stu-id="b89a1-185">These logs are located in hello **C:\Resources\Directory\\{role}\LogFiles** folder.</span></span> <span data-ttu-id="b89a1-186">**PrepPython.err.txt** comporte au moins une erreur à partir de lorsque le script de hello tente toodetect si Python est installé et **PipInstaller.err.txt** peuvent se plaindre une version obsolète du pip.</span><span class="sxs-lookup"><span data-stu-id="b89a1-186">**PrepPython.err.txt** has at least one error in it from when hello script tries toodetect if Python is installed and **PipInstaller.err.txt** may complain about an outdated version of pip.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b89a1-187">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b89a1-187">Next steps</span></span>
<span data-ttu-id="b89a1-188">Pour obtenir des informations plus détaillées sur l’utilisation des rôles web et de travail dans les outils Python pour Visual Studio, consultez la documentation de PTVS hello :</span><span class="sxs-lookup"><span data-stu-id="b89a1-188">For more detailed information about working with web and worker roles in Python Tools for Visual Studio, see hello PTVS documentation:</span></span>

* <span data-ttu-id="b89a1-189">[Projets de service cloud][Cloud Service Projects]</span><span class="sxs-lookup"><span data-stu-id="b89a1-189">[Cloud Service Projects][Cloud Service Projects]</span></span>

<span data-ttu-id="b89a1-190">Pour plus d’informations sur l’utilisation des services Azure à partir de vos rôles web et de travail, telles que l’utilisation d’Azure Storage ou Service Bus, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="b89a1-190">For more details about using Azure services from your web and worker roles, such as using Azure Storage or Service Bus, see hello following articles:</span></span>

* <span data-ttu-id="b89a1-191">[service BLOB][Blob Service]</span><span class="sxs-lookup"><span data-stu-id="b89a1-191">[Blob Service][Blob Service]</span></span>
* <span data-ttu-id="b89a1-192">[Service de Table][Table Service]</span><span class="sxs-lookup"><span data-stu-id="b89a1-192">[Table Service][Table Service]</span></span>
* <span data-ttu-id="b89a1-193">[Service de File d’attente][Queue Service]</span><span class="sxs-lookup"><span data-stu-id="b89a1-193">[Queue Service][Queue Service]</span></span>
* <span data-ttu-id="b89a1-194">[Files d’attente Service Bus][Service Bus Queues]</span><span class="sxs-lookup"><span data-stu-id="b89a1-194">[Service Bus Queues][Service Bus Queues]</span></span>
* <span data-ttu-id="b89a1-195">[Rubriques de Service Bus][Service Bus Topics]</span><span class="sxs-lookup"><span data-stu-id="b89a1-195">[Service Bus Topics][Service Bus Topics]</span></span>

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
