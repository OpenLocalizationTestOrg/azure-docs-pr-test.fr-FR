---
title: "aaaRun des tâches de démarrage dans les Services de cloud computing Azure | Documents Microsoft"
description: "Les tâches de démarrage facilitent la préparation de votre environnement de service cloud pour votre application. Il vous apprend comment démarrage des tâches et toomake les"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 886939be-4b5b-49cc-9a6e-2172e3c133e9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 3391a5d7434164f59972b8e497e5c34e33409543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-and-run-startup-tasks-for-a-cloud-service"></a><span data-ttu-id="d1ad4-104">Des tâches de démarrage tooconfigure et exécution d’un service cloud</span><span class="sxs-lookup"><span data-stu-id="d1ad4-104">How tooconfigure and run startup tasks for a cloud service</span></span>
<span data-ttu-id="d1ad4-105">Vous pouvez utiliser les opérations de tooperform de tâches de démarrage avant le démarrage d’un rôle.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-105">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="d1ad4-106">Les opérations que vous pourriez tooperform incluent l’installation d’un composant, l’inscription des composants COM, définition de clés de Registre ou à partir d’un processus à long terme.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-106">Operations that you might want tooperform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span>

> [!NOTE]
> <span data-ttu-id="d1ad4-107">Tâches de démarrage ne sont pas applicables tooVirtual Machines, tooCloud Service Web et les rôles de travail.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-107">Startup tasks are not applicable tooVirtual Machines, only tooCloud Service Web and Worker roles.</span></span>
> 
> 

## <a name="how-startup-tasks-work"></a><span data-ttu-id="d1ad4-108">Fonctionnement des tâches de démarrage</span><span class="sxs-lookup"><span data-stu-id="d1ad4-108">How startup tasks work</span></span>
<span data-ttu-id="d1ad4-109">Tâches de démarrage sont des actions qui sont effectuées avant que vos rôles commencent et sont définis dans hello [ServiceDefinition.csdef] fichier à l’aide de hello [tâche] élément hello [démarrage]élément.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-109">Startup tasks are actions that are taken before your roles begin and are defined in hello [ServiceDefinition.csdef] file by using hello [Task] element within hello [Startup] element.</span></span> <span data-ttu-id="d1ad4-110">Souvent les tâches de démarrage sont des fichiers de commandes, mais elles peuvent également être des applications console ou des fichiers de commandes qui démarrent des scripts PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-110">Frequently startup tasks are batch files, but they can also be console applications, or batch files that start PowerShell scripts.</span></span>

<span data-ttu-id="d1ad4-111">Variables d’environnement passent des informations dans une tâche de démarrage et le stockage local peut être informations toopass utilisé en dehors d’une tâche de démarrage.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-111">Environment variables pass information into a startup task, and local storage can be used toopass information out of a startup task.</span></span> <span data-ttu-id="d1ad4-112">Par exemple, une variable d’environnement peut spécifier programme de tooa hello chemin d’accès souhaité tooinstall et les fichiers peuvent être écrites de stockage toolocal qui peut être lu ultérieurement par vos rôles.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-112">For example, an environment variable can specify hello path tooa program you want tooinstall, and files can be written toolocal storage that can then be read later by your roles.</span></span>

<span data-ttu-id="d1ad4-113">Votre tâche de démarrage peut enregistrer des informations et répertoire de toohello d’erreurs spécifié par hello **TEMP** variable d’environnement.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-113">Your startup task can log information and errors toohello directory specified by hello **TEMP** environment variable.</span></span> <span data-ttu-id="d1ad4-114">Au cours de la tâche de démarrage hello, hello **TEMP** variable d’environnement résout toohello *C:\\ressources\\temp\\[guid]. [ rolename]\\RoleTemp* active lors de l’exécution sur le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-114">During hello startup task, hello **TEMP** environment variable resolves toohello *C:\\Resources\\temp\\[guid].[rolename]\\RoleTemp* directory when running on hello cloud.</span></span>

<span data-ttu-id="d1ad4-115">Les tâches de démarrage peuvent également être exécutées plusieurs fois entre des redémarrages.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-115">Startup tasks can also be executed several times between reboots.</span></span> <span data-ttu-id="d1ad4-116">Par exemple, tâche de démarrage hello s’exécutera chaque fois hello rôle est recyclé, et les recyclages de rôle n’incluent pas toujours un redémarrage.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-116">For example, hello startup task will be run each time hello role recycles, and role recycles may not always include a reboot.</span></span> <span data-ttu-id="d1ad4-117">Tâches de démarrage doivent être écrites d’une manière qui leur permet de toorun plusieurs fois sans problème.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-117">Startup tasks should be written in a way that allows them toorun several times without problems.</span></span>

<span data-ttu-id="d1ad4-118">Tâches de démarrage doivent se terminer par un **errorlevel** (ou code de sortie) de zéro pour toocomplete de processus de démarrage hello.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-118">Startup tasks must end with an **errorlevel** (or exit code) of zero for hello startup process toocomplete.</span></span> <span data-ttu-id="d1ad4-119">Si une tâche de démarrage se termine par un zéro **errorlevel**, rôle de hello ne démarrera pas.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-119">If a startup task ends with a non-zero **errorlevel**, hello role will not start.</span></span>

## <a name="role-startup-order"></a><span data-ttu-id="d1ad4-120">Ordre de démarrage des rôles</span><span class="sxs-lookup"><span data-stu-id="d1ad4-120">Role startup order</span></span>
<span data-ttu-id="d1ad4-121">Hello suivant la procédure de démarrage de rôle listes hello dans Azure :</span><span class="sxs-lookup"><span data-stu-id="d1ad4-121">hello following lists hello role startup procedure in Azure:</span></span>

1. <span data-ttu-id="d1ad4-122">Hello instance est marquée comme **départ** et ne reçoit pas de trafic.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-122">hello instance is marked as **Starting** and does not receive traffic.</span></span>
2. <span data-ttu-id="d1ad4-123">Toutes les tâches de démarrage sont exécutées selon tootheir **taskType** attribut.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-123">All startup tasks are executed according tootheir **taskType** attribute.</span></span>
   
   * <span data-ttu-id="d1ad4-124">Hello **simple** les tâches sont exécutées de façon synchrone, une à la fois.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-124">hello **simple** tasks are executed synchronously, one at a time.</span></span>
   * <span data-ttu-id="d1ad4-125">Hello **arrière-plan** et **premier plan** tâches sont des tâches de démarrage toohello démarré de façon asynchrone et parallèle.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-125">hello **background** and **foreground** tasks are started asynchronously, parallel toohello startup task.</span></span>  
     
     > [!WARNING]
     > <span data-ttu-id="d1ad4-126">IIS peut être pas complètement configuré pendant l’étape de tâche de démarrage hello dans le processus de démarrage hello, les données spécifiques à un rôle peut ne pas être disponibles.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-126">IIS may not be fully configured during hello startup task stage in hello startup process, so role-specific data may not be available.</span></span> <span data-ttu-id="d1ad4-127">Les tâches de démarrage qui ont besoin de données spécifiques au rôle doivent utiliser [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span><span class="sxs-lookup"><span data-stu-id="d1ad4-127">Startup tasks that require role-specific data should use [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span></span>
     > 
     > 
3. <span data-ttu-id="d1ad4-128">processus hôte de rôle Hello est démarré et le site de hello est créé dans IIS.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-128">hello role host process is started and hello site is created in IIS.</span></span>
4. <span data-ttu-id="d1ad4-129">Hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) méthode est appelée.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-129">hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method is called.</span></span>
5. <span data-ttu-id="d1ad4-130">Hello instance est marquée comme **prêt** et le trafic est routé toohello instance.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-130">hello instance is marked as **Ready** and traffic is routed toohello instance.</span></span>
6. <span data-ttu-id="d1ad4-131">Hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) méthode est appelée.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-131">hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method is called.</span></span>

## <a name="example-of-a-startup-task"></a><span data-ttu-id="d1ad4-132">Exemple d’une tâche de démarrage</span><span class="sxs-lookup"><span data-stu-id="d1ad4-132">Example of a startup task</span></span>
<span data-ttu-id="d1ad4-133">Tâches de démarrage sont définies dans hello [ServiceDefinition.csdef] fichier, Bonjour **tâche** élément.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-133">Startup tasks are defined in hello [ServiceDefinition.csdef] file, in hello **Task** element.</span></span> <span data-ttu-id="d1ad4-134">Hello **commandLine** attribut spécifie le nom de hello et paramètres des commandes de démarrage hello de fichiers ou de la console de commande, hello **executionContext** attribut spécifie le niveau de privilège hello du démarrage de hello tâche et hello **taskType** attribut spécifie comment hello tâche sera exécutée.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-134">hello **commandLine** attribute specifies hello name and parameters of hello startup batch file or console command, hello **executionContext** attribute specifies hello privilege level of hello startup task, and hello **taskType** attribute specifies how hello task will be executed.</span></span>

<span data-ttu-id="d1ad4-135">Dans cet exemple, une variable d’environnement **MyVersionNumber**, est créé pour la tâche de démarrage hello et toohello la valeur «**1.0.0.0**».</span><span class="sxs-lookup"><span data-stu-id="d1ad4-135">In this example, an environment variable, **MyVersionNumber**, is created for hello startup task and set toohello value "**1.0.0.0**".</span></span>

<span data-ttu-id="d1ad4-136">**ServiceDefinition.csdef**:</span><span class="sxs-lookup"><span data-stu-id="d1ad4-136">**ServiceDefinition.csdef**:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

<span data-ttu-id="d1ad4-137">Dans l’exemple suivant de hello, hello **Startup.cmd** fichier de commandes écrit, « la version actuelle de hello est 1.0.0.0 » de fichier de StartupLog.txt toohello, ligne de hello dans le répertoire hello spécifié par la variable d’environnement TEMP hello.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-137">In hello following example, hello **Startup.cmd** batch file writes hello line "hello current version is 1.0.0.0" toohello StartupLog.txt file in hello directory specified by hello TEMP environment variable.</span></span> <span data-ttu-id="d1ad4-138">Hello `EXIT /B 0` ligne garantit que cette tâche de démarrage hello se termine par un **errorlevel** égale à zéro.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-138">hello `EXIT /B 0` line ensures that hello startup task ends with an **errorlevel** of zero.</span></span>

```cmd
ECHO hello current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> <span data-ttu-id="d1ad4-139">Dans Visual Studio, hello **copier tooOutput active** propriété pour votre fichier de commandes de démarrage doit être définie trop**toujours copier** toobe assurer que votre fichier de commandes de démarrage est correctement déployé le projet tooyour sur Azure (**approot\\bin** pour les rôles Web, et **approot** pour les rôles de travail).</span><span class="sxs-lookup"><span data-stu-id="d1ad4-139">In Visual Studio, hello **Copy tooOutput Directory** property for your startup batch file should be set too**Copy Always** toobe sure that your startup batch file is properly deployed tooyour project on Azure (**approot\\bin** for Web roles, and **approot** for worker roles).</span></span>
> 
> 

## <a name="description-of-task-attributes"></a><span data-ttu-id="d1ad4-140">Description des attributs de tâche</span><span class="sxs-lookup"><span data-stu-id="d1ad4-140">Description of task attributes</span></span>
<span data-ttu-id="d1ad4-141">Hello suivante décrit les attributs hello Hello **tâche** élément Bonjour [ServiceDefinition.csdef] fichier :</span><span class="sxs-lookup"><span data-stu-id="d1ad4-141">hello following describes hello attributes of hello **Task** element in hello [ServiceDefinition.csdef] file:</span></span>

<span data-ttu-id="d1ad4-142">**ligne de commande** -spécifie la ligne de commande hello pour la tâche de démarrage hello :</span><span class="sxs-lookup"><span data-stu-id="d1ad4-142">**commandLine** - Specifies hello command line for hello startup task:</span></span>

* <span data-ttu-id="d1ad4-143">Hello commande avec des paramètres de ligne de commande facultatifs, qui commence la tâche de démarrage hello.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-143">hello command, with optional command line parameters, which begins hello startup task.</span></span>
* <span data-ttu-id="d1ad4-144">Il s’agit souvent hello de nom de fichier d’un fichier de commandes .cmd ou .bat.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-144">Frequently this is hello filename of a .cmd or .bat batch file.</span></span>
* <span data-ttu-id="d1ad4-145">tâche Hello est relatif toohello AppRoot\\dossier Bin pour le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-145">hello task is relative toohello AppRoot\\Bin folder for hello deployment.</span></span> <span data-ttu-id="d1ad4-146">Variables d’environnement ne sont pas développées dans la détermination hello chemin d’accès et de la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-146">Environment variables are not expanded in determining hello path and file of hello task.</span></span> <span data-ttu-id="d1ad4-147">Si ce développement est nécessaire, vous pouvez créer un petit script .cmd qui appelle votre tâche de démarrage.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-147">If environment expansion is required, you can create a small .cmd script that calls your startup task.</span></span>
* <span data-ttu-id="d1ad4-148">Il peut s’agir d’une application console ou d’un fichier de commande qui démarre un [script PowerShell](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span><span class="sxs-lookup"><span data-stu-id="d1ad4-148">Can be a console application or a batch file that starts a [PowerShell script](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span></span>

<span data-ttu-id="d1ad4-149">**executionContext** -Spécifie le niveau de privilège hello pour la tâche de démarrage hello.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-149">**executionContext** - Specifies hello privilege level for hello startup task.</span></span> <span data-ttu-id="d1ad4-150">niveau de privilège Hello peut être limité ou élevé :</span><span class="sxs-lookup"><span data-stu-id="d1ad4-150">hello privilege level can be limited or elevated:</span></span>

* <span data-ttu-id="d1ad4-151">**limited**</span><span class="sxs-lookup"><span data-stu-id="d1ad4-151">**limited**</span></span>  
  <span data-ttu-id="d1ad4-152">tâche de démarrage Hello s’exécute avec hello mêmes privilèges en tant que rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-152">hello startup task runs with hello same privileges as hello role.</span></span> <span data-ttu-id="d1ad4-153">Hello lorsque **executionContext** attribut pour hello [Runtime] élément est également **limité**, puis les privilèges utilisateur sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-153">When hello **executionContext** attribute for hello [Runtime] element is also **limited**, then user privileges are used.</span></span>
* <span data-ttu-id="d1ad4-154">**elevated**</span><span class="sxs-lookup"><span data-stu-id="d1ad4-154">**elevated**</span></span>  
  <span data-ttu-id="d1ad4-155">tâche de démarrage Hello s’exécute avec des privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-155">hello startup task runs with administrator privileges.</span></span> <span data-ttu-id="d1ad4-156">Ainsi, les tâches de démarrage tooinstall programmes, apporter des modifications de configuration IIS, effectuer des modifications du Registre et autres tâches d’administration, sans augmenter le niveau de privilège hello du rôle hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-156">This allows startup tasks tooinstall programs, make IIS configuration changes, perform registry changes, and other administrator level tasks, without increasing hello privilege level of hello role itself.</span></span>  

> [!NOTE]
> <span data-ttu-id="d1ad4-157">Hello niveau de privilège d’une tâche de démarrage n’a pas besoin toobe même hello en tant que rôle hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-157">hello privilege level of a startup task does not need toobe hello same as hello role itself.</span></span>
> 
> 

<span data-ttu-id="d1ad4-158">**taskType** -spécifie hello façon une tâche de démarrage est exécutée.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-158">**taskType** - Specifies hello way a startup task is executed.</span></span>

* <span data-ttu-id="d1ad4-159">**simple**</span><span class="sxs-lookup"><span data-stu-id="d1ad4-159">**simple**</span></span>  
  <span data-ttu-id="d1ad4-160">Les tâches sont exécutées de façon synchrone, une à la fois, dans l’ordre de hello spécifié dans hello [ServiceDefinition.csdef] fichier.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-160">Tasks are executed synchronously, one at a time, in hello order specified in hello [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="d1ad4-161">Lorsqu’un **simple** tâche de démarrage se termine par un **errorlevel** de zéro, hello ensuite **simple** tâche de démarrage est exécutée.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-161">When one **simple** startup task ends with an **errorlevel** of zero, hello next **simple** startup task is executed.</span></span> <span data-ttu-id="d1ad4-162">S’il n’y a plus aucun **simple** tooexecute, les tâches de démarrage puis démarrera rôle hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-162">If there are no more **simple** startup tasks tooexecute, then hello role itself will be started.</span></span>   
  
  > [!NOTE]
  > <span data-ttu-id="d1ad4-163">Si hello **simple** tâche se termine par un zéro **errorlevel**, hello instance sera bloquée.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-163">If hello **simple** task ends with a non-zero **errorlevel**, hello instance will be blocked.</span></span> <span data-ttu-id="d1ad4-164">Ultérieures **simple** tâches de démarrage et rôle hello lui-même, ne démarrent pas.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-164">Subsequent **simple** startup tasks, and hello role itself, will not start.</span></span>
  > 
  > 
  
    <span data-ttu-id="d1ad4-165">tooensure votre fichier de commandes se termine par un **errorlevel** égal à zéro, exécutez la commande hello `EXIT /B 0` à fin hello de votre processus de fichier de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-165">tooensure that your batch file ends with an **errorlevel** of zero, execute hello command `EXIT /B 0` at hello end of your batch file process.</span></span>
* <span data-ttu-id="d1ad4-166">**background**</span><span class="sxs-lookup"><span data-stu-id="d1ad4-166">**background**</span></span>  
  <span data-ttu-id="d1ad4-167">Tâches sont exécutées de façon asynchrone, en parallèle avec démarrage hello du rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-167">Tasks are executed asynchronously, in parallel with hello startup of hello role.</span></span>
* <span data-ttu-id="d1ad4-168">**foreground**</span><span class="sxs-lookup"><span data-stu-id="d1ad4-168">**foreground**</span></span>  
  <span data-ttu-id="d1ad4-169">Tâches sont exécutées de façon asynchrone, en parallèle avec démarrage hello du rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-169">Tasks are executed asynchronously, in parallel with hello startup of hello role.</span></span> <span data-ttu-id="d1ad4-170">Hello la principale différence entre un **premier plan** et un **arrière-plan** est que la tâche un **premier plan** tâche empêche le rôle hello de recyclage ou l’arrêt jusqu'à ce que la tâche hello a s’est terminée.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-170">hello key difference between a **foreground** and a **background** task is that a **foreground** task prevents hello role from recycling or shutting down until hello task has ended.</span></span> <span data-ttu-id="d1ad4-171">Hello **arrière-plan** tâches ne disposent pas de cette restriction.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-171">hello **background** tasks do not have this restriction.</span></span>

## <a name="environment-variables"></a><span data-ttu-id="d1ad4-172">Variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="d1ad4-172">Environment variables</span></span>
<span data-ttu-id="d1ad4-173">Variables d’environnement sont une tâche de démarrage de façon toopass informations tooa.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-173">Environment variables are a way toopass information tooa startup task.</span></span> <span data-ttu-id="d1ad4-174">Par exemple, vous pouvez placer hello chemin d’accès tooa blob qui contient un programme tooinstall, ou les numéros de port qui utilise votre rôle ou toocontrol les fonctionnalités des paramètres de votre tâche de démarrage.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-174">For example, you can put hello path tooa blob that contains a program tooinstall, or port numbers that your role will use, or settings toocontrol features of your startup task.</span></span>

<span data-ttu-id="d1ad4-175">Il existe deux types de variables d’environnement pour les tâches de démarrage ; variables d’environnement statiques et les variables d’environnement basée sur les membres de hello [ RoleEnvironment] classe.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-175">There are two kinds of environment variables for startup tasks; static environment variables and environment variables based on members of hello [RoleEnvironment] class.</span></span> <span data-ttu-id="d1ad4-176">Les deux sont Bonjour [environnement] section Hello [ServiceDefinition.csdef] de fichiers et les deux hello utilisation [ Variable] élément et **nom** attribut.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-176">Both are in hello [Environment] section of hello [ServiceDefinition.csdef] file, and both use hello [Variable] element and **name** attribute.</span></span>

<span data-ttu-id="d1ad4-177">Hello d’utilise les variables statiques environnement **valeur** attribut Hello [ Variable] élément.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-177">Static environment variables uses hello **value** attribute of hello [Variable] element.</span></span> <span data-ttu-id="d1ad4-178">exemple Hello ci-dessus crée la variable d’environnement hello **MyVersionNumber** avec une valeur statique de «**1.0.0.0**».</span><span class="sxs-lookup"><span data-stu-id="d1ad4-178">hello example above creates hello environment variable **MyVersionNumber** which has a static value of "**1.0.0.0**".</span></span> <span data-ttu-id="d1ad4-179">Un autre exemple consisterait à toocreate un **StagingOrProduction** variable d’environnement que vous pouvez définir manuellement toovalues de «**intermédiaire**« ou »**production**» tooperform les actions de démarrage différentes en fonction de la valeur hello hello **StagingOrProduction** variable d’environnement.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-179">Another example would be toocreate a **StagingOrProduction** environment variable which you can manually set toovalues of "**staging**" or "**production**" tooperform different startup actions based on hello value of hello **StagingOrProduction** environment variable.</span></span>

<span data-ttu-id="d1ad4-180">Variables d’environnement basées sur les membres de hello classe RoleEnvironment n’utilisent pas hello **valeur** attribut Hello [ Variable] élément.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-180">Environment variables based on members of hello RoleEnvironment class do not use hello **value** attribute of hello [Variable] element.</span></span> <span data-ttu-id="d1ad4-181">Au lieu de cela, hello [RoleInstanceValue] élément enfant, avec hello approprié **XPath** valeur d’attribut, est toocreate utilisé une variable d’environnement basée sur un membre spécifique de hello [ RoleEnvironment] classe.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-181">Instead, hello [RoleInstanceValue] child element, with hello appropriate **XPath** attribute value, are used toocreate an environment variable based on a specific member of hello [RoleEnvironment] class.</span></span> <span data-ttu-id="d1ad4-182">Valeurs pour hello **XPath** tooaccess d’attributs différentes [ RoleEnvironment] les valeurs se trouvent [ici](cloud-services-role-config-xpath.md).</span><span class="sxs-lookup"><span data-stu-id="d1ad4-182">Values for hello **XPath** attribute tooaccess various [RoleEnvironment] values can be found [here](cloud-services-role-config-xpath.md).</span></span>

<span data-ttu-id="d1ad4-183">Par exemple, toocreate une variable d’environnement qui est «**true**» lors de l’instance de hello est en cours d’exécution dans l’émulateur de calcul hello, et «**false**» lors de l’exécution dans le cloud de hello, utilisez des éléments suivants de hello [ Variable] et [RoleInstanceValue] éléments :</span><span class="sxs-lookup"><span data-stu-id="d1ad4-183">For example, toocreate an environment variable that is "**true**" when hello instance is running in hello compute emulator, and "**false**" when running in hello cloud, use hello following [Variable] and [RoleInstanceValue] elements:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create hello environment variable that informs hello startup task whether it is running
                in hello Compute Emulator or in hello cloud. "%ComputeEmulatorRunning%"=="true" when
                running in hello Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in hello cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a><span data-ttu-id="d1ad4-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d1ad4-184">Next steps</span></span>
<span data-ttu-id="d1ad4-185">Découvrez comment tooperform certains [tâches courantes de démarrage](cloud-services-startup-tasks-common.md) avec votre Service Cloud.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-185">Learn how tooperform some [common startup tasks](cloud-services-startup-tasks-common.md) with your Cloud Service.</span></span>

<span data-ttu-id="d1ad4-186">[Créez un package](cloud-services-model-and-package.md) de votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="d1ad4-186">[Package](cloud-services-model-and-package.md) your Cloud Service.</span></span>  

[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef
[tâche]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[démarrage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[environnement]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[ Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[ RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
