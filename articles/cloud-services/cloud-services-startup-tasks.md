---
title: "Exécuter des tâches de démarrage dans Azure Cloud Services | Microsoft Docs"
description: "Les tâches de démarrage facilitent la préparation de votre environnement de service cloud pour votre application. Cette documentation vous apprend comment fonctionnent les tâches de démarrage et comment les créer."
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
ms.openlocfilehash: 1c1b3aa86dc8211de0c07c9fb68da5685c86f551
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-and-run-startup-tasks-for-a-cloud-service"></a><span data-ttu-id="d07b3-104">Comment configurer et exécuter des tâches de démarrage pour un service cloud</span><span class="sxs-lookup"><span data-stu-id="d07b3-104">How to configure and run startup tasks for a cloud service</span></span>
<span data-ttu-id="d07b3-105">Vous pouvez utiliser des tâches de démarrage pour exécuter des opérations avant le démarrage d’un rôle.</span><span class="sxs-lookup"><span data-stu-id="d07b3-105">You can use startup tasks to perform operations before a role starts.</span></span> <span data-ttu-id="d07b3-106">Parmi les opérations que vous pouvez effectuer figurent l’installation d’un composant, l’enregistrement de composants COM, la définition des clés du Registre ou le démarrage d’un processus de longue durée.</span><span class="sxs-lookup"><span data-stu-id="d07b3-106">Operations that you might want to perform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span>

> [!NOTE]
> <span data-ttu-id="d07b3-107">Les tâches de démarrage ne s’appliquent pas aux rôles de machine virtuelle ; elles ne concernent que les rôles web de service cloud et de travail.</span><span class="sxs-lookup"><span data-stu-id="d07b3-107">Startup tasks are not applicable to Virtual Machines, only to Cloud Service Web and Worker roles.</span></span>
> 
> 

## <a name="how-startup-tasks-work"></a><span data-ttu-id="d07b3-108">Fonctionnement des tâches de démarrage</span><span class="sxs-lookup"><span data-stu-id="d07b3-108">How startup tasks work</span></span>
<span data-ttu-id="d07b3-109">Les tâches de démarrage sont des actions qui sont effectuées avant le début de vos rôles, et sont définies dans le fichier [ServiceDefinition.csdef] à l’aide de l’élément [Task] dans l’élément [Startup].</span><span class="sxs-lookup"><span data-stu-id="d07b3-109">Startup tasks are actions that are taken before your roles begin and are defined in the [ServiceDefinition.csdef] file by using the [Task] element within the [Startup] element.</span></span> <span data-ttu-id="d07b3-110">Souvent les tâches de démarrage sont des fichiers de commandes, mais elles peuvent également être des applications console ou des fichiers de commandes qui démarrent des scripts PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d07b3-110">Frequently startup tasks are batch files, but they can also be console applications, or batch files that start PowerShell scripts.</span></span>

<span data-ttu-id="d07b3-111">Les variables d’environnement passent des informations dans une tâche de démarrage et le stockage local peut être utilisé pour transmettre des informations hors d’une tâche de démarrage.</span><span class="sxs-lookup"><span data-stu-id="d07b3-111">Environment variables pass information into a startup task, and local storage can be used to pass information out of a startup task.</span></span> <span data-ttu-id="d07b3-112">Par exemple, une variable d’environnement peut spécifier le chemin d’accès à un programme que vous voulez installer, et des fichiers peuvent être écrits dans le stockage local qui peuvent être lus ultérieurement par vos rôles.</span><span class="sxs-lookup"><span data-stu-id="d07b3-112">For example, an environment variable can specify the path to a program you want to install, and files can be written to local storage that can then be read later by your roles.</span></span>

<span data-ttu-id="d07b3-113">Votre tâche de démarrage peut enregistrer des informations et des erreurs dans un répertoire spécifié par la variable d’environnement **TEMP** .</span><span class="sxs-lookup"><span data-stu-id="d07b3-113">Your startup task can log information and errors to the directory specified by the **TEMP** environment variable.</span></span> <span data-ttu-id="d07b3-114">Pendant la tâche de démarrage, la variable d’environnement **TEMP** est résolue dans le répertoire *C:\\Resources\\temp\\[guid].[nom_rôle]\\RoleTemp* au moment de l’exécution sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="d07b3-114">During the startup task, the **TEMP** environment variable resolves to the *C:\\Resources\\temp\\[guid].[rolename]\\RoleTemp* directory when running on the cloud.</span></span>

<span data-ttu-id="d07b3-115">Les tâches de démarrage peuvent également être exécutées plusieurs fois entre des redémarrages.</span><span class="sxs-lookup"><span data-stu-id="d07b3-115">Startup tasks can also be executed several times between reboots.</span></span> <span data-ttu-id="d07b3-116">Par exemple, la tâche de démarrage est exécutée chaque fois que le rôle est recyclé, et les recyclages de rôle n’incluent pas toujours un redémarrage.</span><span class="sxs-lookup"><span data-stu-id="d07b3-116">For example, the startup task will be run each time the role recycles, and role recycles may not always include a reboot.</span></span> <span data-ttu-id="d07b3-117">Les tâches de démarrage doivent être écrites de façon à pouvoir s’exécuter de façon répétée sans problèmes.</span><span class="sxs-lookup"><span data-stu-id="d07b3-117">Startup tasks should be written in a way that allows them to run several times without problems.</span></span>

<span data-ttu-id="d07b3-118">Les tâches de démarrage doivent s’arrêter avec un **errorlevel** (ou code de sortie) égal à zéro pour que le processus de démarrage soit terminé.</span><span class="sxs-lookup"><span data-stu-id="d07b3-118">Startup tasks must end with an **errorlevel** (or exit code) of zero for the startup process to complete.</span></span> <span data-ttu-id="d07b3-119">Si une tâche de démarrage se termine par un **errorlevel**différent de zéro, le rôle ne démarre pas.</span><span class="sxs-lookup"><span data-stu-id="d07b3-119">If a startup task ends with a non-zero **errorlevel**, the role will not start.</span></span>

## <a name="role-startup-order"></a><span data-ttu-id="d07b3-120">Ordre de démarrage des rôles</span><span class="sxs-lookup"><span data-stu-id="d07b3-120">Role startup order</span></span>
<span data-ttu-id="d07b3-121">Les informations suivantes indiquent la procédure de démarrage de rôle dans Azure :</span><span class="sxs-lookup"><span data-stu-id="d07b3-121">The following lists the role startup procedure in Azure:</span></span>

1. <span data-ttu-id="d07b3-122">L’instance est marquée comme **Starting** et ne reçoit pas de trafic.</span><span class="sxs-lookup"><span data-stu-id="d07b3-122">The instance is marked as **Starting** and does not receive traffic.</span></span>
2. <span data-ttu-id="d07b3-123">Toutes les tâches de démarrage sont exécutées en fonction de leur attribut **taskType** .</span><span class="sxs-lookup"><span data-stu-id="d07b3-123">All startup tasks are executed according to their **taskType** attribute.</span></span>
   
   * <span data-ttu-id="d07b3-124">Les tâches **simple** sont exécutées de façon synchrone, une par une.</span><span class="sxs-lookup"><span data-stu-id="d07b3-124">The **simple** tasks are executed synchronously, one at a time.</span></span>
   * <span data-ttu-id="d07b3-125">Les tâches **background** et **foreground** sont démarrées de façon asynchrone, en parallèle de la tâche de démarrage.</span><span class="sxs-lookup"><span data-stu-id="d07b3-125">The **background** and **foreground** tasks are started asynchronously, parallel to the startup task.</span></span>  
     
     > [!WARNING]
     > <span data-ttu-id="d07b3-126">Il est possible qu’IIS ne soit pas configuré complètement pendant l’étape de la tâche de démarrage ; de ce fait, les données spécifiques au rôle ne sont pas forcément disponibles.</span><span class="sxs-lookup"><span data-stu-id="d07b3-126">IIS may not be fully configured during the startup task stage in the startup process, so role-specific data may not be available.</span></span> <span data-ttu-id="d07b3-127">Les tâches de démarrage qui ont besoin de données spécifiques au rôle doivent utiliser [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span><span class="sxs-lookup"><span data-stu-id="d07b3-127">Startup tasks that require role-specific data should use [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span></span>
     > 
     > 
3. <span data-ttu-id="d07b3-128">Le processus hôte de rôle est démarré, et le site est créé dans IIS.</span><span class="sxs-lookup"><span data-stu-id="d07b3-128">The role host process is started and the site is created in IIS.</span></span>
4. <span data-ttu-id="d07b3-129">La méthode [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) est appelée.</span><span class="sxs-lookup"><span data-stu-id="d07b3-129">The [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method is called.</span></span>
5. <span data-ttu-id="d07b3-130">L’instance est marquée comme **Ready** , et le trafic est acheminé vers l’instance.</span><span class="sxs-lookup"><span data-stu-id="d07b3-130">The instance is marked as **Ready** and traffic is routed to the instance.</span></span>
6. <span data-ttu-id="d07b3-131">La méthode [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) est appelée.</span><span class="sxs-lookup"><span data-stu-id="d07b3-131">The [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method is called.</span></span>

## <a name="example-of-a-startup-task"></a><span data-ttu-id="d07b3-132">Exemple d’une tâche de démarrage</span><span class="sxs-lookup"><span data-stu-id="d07b3-132">Example of a startup task</span></span>
<span data-ttu-id="d07b3-133">Les tâches de démarrage sont définies dans le fichier [ServiceDefinition.csdef] , dans l’élément **Task** .</span><span class="sxs-lookup"><span data-stu-id="d07b3-133">Startup tasks are defined in the [ServiceDefinition.csdef] file, in the **Task** element.</span></span> <span data-ttu-id="d07b3-134">L’attribut **commandLine** spécifie le nom et les paramètres du fichier de commandes de démarrage ou de la commande de la console, l’attribut **executionContext** indique le niveau de privilège de la tâche de démarrage et l’attribut **taskType** définit l’exécution de la tâche.</span><span class="sxs-lookup"><span data-stu-id="d07b3-134">The **commandLine** attribute specifies the name and parameters of the startup batch file or console command, the **executionContext** attribute specifies the privilege level of the startup task, and the **taskType** attribute specifies how the task will be executed.</span></span>

<span data-ttu-id="d07b3-135">Dans cet exemple, une variable d’environnement **MyVersionNumber**, est créée pour la tâche de démarrage et définie sur « **1.0.0.0** ».</span><span class="sxs-lookup"><span data-stu-id="d07b3-135">In this example, an environment variable, **MyVersionNumber**, is created for the startup task and set to the value "**1.0.0.0**".</span></span>

<span data-ttu-id="d07b3-136">**ServiceDefinition.csdef**:</span><span class="sxs-lookup"><span data-stu-id="d07b3-136">**ServiceDefinition.csdef**:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

<span data-ttu-id="d07b3-137">Dans l’exemple suivant, le fichier de commande **Startup.cmd** écrit la ligne « The current version is 1.0.0.0 » dans le fichier StartupLog.txt dans le répertoire spécifié par la variable d’environnement TEMP.</span><span class="sxs-lookup"><span data-stu-id="d07b3-137">In the following example, the **Startup.cmd** batch file writes the line "The current version is 1.0.0.0" to the StartupLog.txt file in the directory specified by the TEMP environment variable.</span></span> <span data-ttu-id="d07b3-138">La ligne `EXIT /B 0` garantit que la tâche de démarrage s’arrête avec un **errorlevel** égal à zéro.</span><span class="sxs-lookup"><span data-stu-id="d07b3-138">The `EXIT /B 0` line ensures that the startup task ends with an **errorlevel** of zero.</span></span>

```cmd
ECHO The current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> <span data-ttu-id="d07b3-139">Dans Visual Studio, la propriété **Copier dans le répertoire de sortie** pour votre fichier de commandes de démarrage doit être définie sur **Toujours copier** afin de vous assurer que votre fichier de commandes de démarrage est correctement déployé dans votre projet sur Azure (**approot\\bin** pour les rôles web et **approot** pour les rôles de travail).</span><span class="sxs-lookup"><span data-stu-id="d07b3-139">In Visual Studio, the **Copy to Output Directory** property for your startup batch file should be set to **Copy Always** to be sure that your startup batch file is properly deployed to your project on Azure (**approot\\bin** for Web roles, and **approot** for worker roles).</span></span>
> 
> 

## <a name="description-of-task-attributes"></a><span data-ttu-id="d07b3-140">Description des attributs de tâche</span><span class="sxs-lookup"><span data-stu-id="d07b3-140">Description of task attributes</span></span>
<span data-ttu-id="d07b3-141">Vous trouverez ci-dessous une description des attributs de l’élément **Task** du fichier [ServiceDefinition.csdef] :</span><span class="sxs-lookup"><span data-stu-id="d07b3-141">The following describes the attributes of the **Task** element in the [ServiceDefinition.csdef] file:</span></span>

<span data-ttu-id="d07b3-142">**commandLine** - spécifie la ligne de commande pour la tâche de démarrage :</span><span class="sxs-lookup"><span data-stu-id="d07b3-142">**commandLine** - Specifies the command line for the startup task:</span></span>

* <span data-ttu-id="d07b3-143">La commande avec des paramètres de ligne de commande en option, qui débute la tâche de démarrage.</span><span class="sxs-lookup"><span data-stu-id="d07b3-143">The command, with optional command line parameters, which begins the startup task.</span></span>
* <span data-ttu-id="d07b3-144">Souvent, il s’agit du nom d’un fichier de commandes .cmd ou .bat.</span><span class="sxs-lookup"><span data-stu-id="d07b3-144">Frequently this is the filename of a .cmd or .bat batch file.</span></span>
* <span data-ttu-id="d07b3-145">La tâche est relative au dossier AppRoot\\Bin pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="d07b3-145">The task is relative to the AppRoot\\Bin folder for the deployment.</span></span> <span data-ttu-id="d07b3-146">Les variables d’environnement ne sont pas développées pour déterminer le chemin d’accès et le fichier de la tâche.</span><span class="sxs-lookup"><span data-stu-id="d07b3-146">Environment variables are not expanded in determining the path and file of the task.</span></span> <span data-ttu-id="d07b3-147">Si ce développement est nécessaire, vous pouvez créer un petit script .cmd qui appelle votre tâche de démarrage.</span><span class="sxs-lookup"><span data-stu-id="d07b3-147">If environment expansion is required, you can create a small .cmd script that calls your startup task.</span></span>
* <span data-ttu-id="d07b3-148">Il peut s’agir d’une application console ou d’un fichier de commande qui démarre un [script PowerShell](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span><span class="sxs-lookup"><span data-stu-id="d07b3-148">Can be a console application or a batch file that starts a [PowerShell script](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span></span>

<span data-ttu-id="d07b3-149">**executionContext** - spécifie le niveau de privilège pour la tâche de démarrage.</span><span class="sxs-lookup"><span data-stu-id="d07b3-149">**executionContext** - Specifies the privilege level for the startup task.</span></span> <span data-ttu-id="d07b3-150">Le niveau de privilège peut être limité ou élevé :</span><span class="sxs-lookup"><span data-stu-id="d07b3-150">The privilege level can be limited or elevated:</span></span>

* <span data-ttu-id="d07b3-151">**limited**</span><span class="sxs-lookup"><span data-stu-id="d07b3-151">**limited**</span></span>  
  <span data-ttu-id="d07b3-152"> : la tâche de démarrage s’exécute avec les mêmes privilèges que le rôle.</span><span class="sxs-lookup"><span data-stu-id="d07b3-152">The startup task runs with the same privileges as the role.</span></span> <span data-ttu-id="d07b3-153">Quand l’attribut **executionContext** de l’élément [Runtime] est également **limited**, les privilèges utilisateur sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="d07b3-153">When the **executionContext** attribute for the [Runtime] element is also **limited**, then user privileges are used.</span></span>
* <span data-ttu-id="d07b3-154">**elevated**</span><span class="sxs-lookup"><span data-stu-id="d07b3-154">**elevated**</span></span>  
  <span data-ttu-id="d07b3-155"> : la tâche de démarrage s’exécute avec des privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="d07b3-155">The startup task runs with administrator privileges.</span></span> <span data-ttu-id="d07b3-156">Les tâches de démarrage peuvent ainsi installer des programmes, apporter des modifications à la configuration IIS, modifier le Registre et effectuer d’autres tâches d’administration, sans augmenter le niveau de privilège du rôle.</span><span class="sxs-lookup"><span data-stu-id="d07b3-156">This allows startup tasks to install programs, make IIS configuration changes, perform registry changes, and other administrator level tasks, without increasing the privilege level of the role itself.</span></span>  

> [!NOTE]
> <span data-ttu-id="d07b3-157">Le niveau de privilège d’une tâche de démarrage n’a pas besoin d’être le même que celui du rôle.</span><span class="sxs-lookup"><span data-stu-id="d07b3-157">The privilege level of a startup task does not need to be the same as the role itself.</span></span>
> 
> 

<span data-ttu-id="d07b3-158">**taskType** - spécifie la façon dont une tâche de démarrage est exécutée.</span><span class="sxs-lookup"><span data-stu-id="d07b3-158">**taskType** - Specifies the way a startup task is executed.</span></span>

* <span data-ttu-id="d07b3-159">**simple**</span><span class="sxs-lookup"><span data-stu-id="d07b3-159">**simple**</span></span>  
  <span data-ttu-id="d07b3-160">sont exécutées de façon synchrone, une à la fois, dans l’ordre spécifié dans le fichier [ServiceDefinition.csdef] .</span><span class="sxs-lookup"><span data-stu-id="d07b3-160">Tasks are executed synchronously, one at a time, in the order specified in the [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="d07b3-161">Quand une tâche **simple** se termine par un **errorlevel** égal à zéro, la tâche de démarrage **simple** suivante est exécutée.</span><span class="sxs-lookup"><span data-stu-id="d07b3-161">When one **simple** startup task ends with an **errorlevel** of zero, the next **simple** startup task is executed.</span></span> <span data-ttu-id="d07b3-162">Quand toutes les tâches **simple** ont été exécutées, le rôle est démarré.</span><span class="sxs-lookup"><span data-stu-id="d07b3-162">If there are no more **simple** startup tasks to execute, then the role itself will be started.</span></span>   
  
  > [!NOTE]
  > <span data-ttu-id="d07b3-163">Si la tâche **simple** se termine par un **errorlevel** différent de zéro, l’instance est bloquée.</span><span class="sxs-lookup"><span data-stu-id="d07b3-163">If the **simple** task ends with a non-zero **errorlevel**, the instance will be blocked.</span></span> <span data-ttu-id="d07b3-164">Les tâches de démarrage **simple** suivantes et le rôle ne démarrent pas.</span><span class="sxs-lookup"><span data-stu-id="d07b3-164">Subsequent **simple** startup tasks, and the role itself, will not start.</span></span>
  > 
  > 
  
    <span data-ttu-id="d07b3-165">Pour vous assurer que votre fichier de commandes se termine par un **errorlevel** égal à zéro, exécutez la commande `EXIT /B 0` à la fin du processus de votre fichier de commandes.</span><span class="sxs-lookup"><span data-stu-id="d07b3-165">To ensure that your batch file ends with an **errorlevel** of zero, execute the command `EXIT /B 0` at the end of your batch file process.</span></span>
* <span data-ttu-id="d07b3-166">**background**</span><span class="sxs-lookup"><span data-stu-id="d07b3-166">**background**</span></span>  
  <span data-ttu-id="d07b3-167">sont exécutées de façon asynchrone, en parallèle du démarrage du rôle.</span><span class="sxs-lookup"><span data-stu-id="d07b3-167">Tasks are executed asynchronously, in parallel with the startup of the role.</span></span>
* <span data-ttu-id="d07b3-168">**foreground**</span><span class="sxs-lookup"><span data-stu-id="d07b3-168">**foreground**</span></span>  
  <span data-ttu-id="d07b3-169">sont exécutées de façon asynchrone, en parallèle du démarrage du rôle.</span><span class="sxs-lookup"><span data-stu-id="d07b3-169">Tasks are executed asynchronously, in parallel with the startup of the role.</span></span> <span data-ttu-id="d07b3-170">La principale différence entre une tâche **foreground** et une tâche **background** est que la tâche **foreground** empêche le recyclage ou l’arrêt du rôle tant qu’elle n’est pas terminée.</span><span class="sxs-lookup"><span data-stu-id="d07b3-170">The key difference between a **foreground** and a **background** task is that a **foreground** task prevents the role from recycling or shutting down until the task has ended.</span></span> <span data-ttu-id="d07b3-171">Les tâches **background** n’ont pas cette restriction.</span><span class="sxs-lookup"><span data-stu-id="d07b3-171">The **background** tasks do not have this restriction.</span></span>

## <a name="environment-variables"></a><span data-ttu-id="d07b3-172">Variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="d07b3-172">Environment variables</span></span>
<span data-ttu-id="d07b3-173">Les variables d’environnement permettent de passer les informations à une tâche de démarrage.</span><span class="sxs-lookup"><span data-stu-id="d07b3-173">Environment variables are a way to pass information to a startup task.</span></span> <span data-ttu-id="d07b3-174">Par exemple, vous pouvez indiquer le chemin vers un objet blob qui contient un programme à installer ou les numéros de port que votre rôle va utiliser ou des paramètres pour contrôler les fonctionnalités de votre tâche de démarrage.</span><span class="sxs-lookup"><span data-stu-id="d07b3-174">For example, you can put the path to a blob that contains a program to install, or port numbers that your role will use, or settings to control features of your startup task.</span></span>

<span data-ttu-id="d07b3-175">Il existe deux types de variables d’environnement pour des tâches de démarrage ; des variables d’environnement statiques et des variables d’environnement basées sur les membres de la classe [RoleEnvironment] .</span><span class="sxs-lookup"><span data-stu-id="d07b3-175">There are two kinds of environment variables for startup tasks; static environment variables and environment variables based on members of the [RoleEnvironment] class.</span></span> <span data-ttu-id="d07b3-176">Elles se trouvent dans la section [Environment] du fichier [ServiceDefinition.csdef] et utilisent l’élément [Variable] et l’attribut **name**.</span><span class="sxs-lookup"><span data-stu-id="d07b3-176">Both are in the [Environment] section of the [ServiceDefinition.csdef] file, and both use the [Variable] element and **name** attribute.</span></span>

<span data-ttu-id="d07b3-177">Les variables d’environnement statiques utilisent l’attribut **value** de l’élement [Variable] .</span><span class="sxs-lookup"><span data-stu-id="d07b3-177">Static environment variables uses the **value** attribute of the [Variable] element.</span></span> <span data-ttu-id="d07b3-178">L’exemple ci-dessus crée la variable d’environnement **MyVersionNumber** avec une valeur statique de « **1.0.0.0** ».</span><span class="sxs-lookup"><span data-stu-id="d07b3-178">The example above creates the environment variable **MyVersionNumber** which has a static value of "**1.0.0.0**".</span></span> <span data-ttu-id="d07b3-179">Un autre exemple consiste à créer une variable d’environnement **StagingOrProduction** à laquelle vous pouvez manuellement attribuer les valeurs « **staging** » ou « **production** » pour exécuter des actions de démarrage différentes en fonction de la valeur de la variable d’environnement **StagingOrProduction**.</span><span class="sxs-lookup"><span data-stu-id="d07b3-179">Another example would be to create a **StagingOrProduction** environment variable which you can manually set to values of "**staging**" or "**production**" to perform different startup actions based on the value of the **StagingOrProduction** environment variable.</span></span>

<span data-ttu-id="d07b3-180">Les variables d’environnement basées sur les membres de la classe RoleEnvironment n’utilisent pas l’attribut **value** de l’élément [Variable] .</span><span class="sxs-lookup"><span data-stu-id="d07b3-180">Environment variables based on members of the RoleEnvironment class do not use the **value** attribute of the [Variable] element.</span></span> <span data-ttu-id="d07b3-181">À la place, l’élément [RoleInstanceValue] enfant, avec la valeur d’attribut **XPath** appropriée, est utilisé pour créer une variable d’environnement basée sur un membre spécifique de la classe [RoleEnvironment].</span><span class="sxs-lookup"><span data-stu-id="d07b3-181">Instead, the [RoleInstanceValue] child element, with the appropriate **XPath** attribute value, are used to create an environment variable based on a specific member of the [RoleEnvironment] class.</span></span> <span data-ttu-id="d07b3-182">Les valeurs de l’attribut **XPath** pour accéder aux différentes valeurs [RoleEnvironment] se trouvent [ici](cloud-services-role-config-xpath.md).</span><span class="sxs-lookup"><span data-stu-id="d07b3-182">Values for the **XPath** attribute to access various [RoleEnvironment] values can be found [here](cloud-services-role-config-xpath.md).</span></span>

<span data-ttu-id="d07b3-183">Par exemple, pour créer une variable d’environnement qui a la valeur « **true** » quand l’instance s’exécute dans l’émulateur de calcul et la valeur « **false** » pendant une exécution dans le cloud, utilisez les éléments [Variable] et [RoleInstanceValue] :</span><span class="sxs-lookup"><span data-stu-id="d07b3-183">For example, to create an environment variable that is "**true**" when the instance is running in the compute emulator, and "**false**" when running in the cloud, use the following [Variable] and [RoleInstanceValue] elements:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create the environment variable that informs the startup task whether it is running
                in the Compute Emulator or in the cloud. "%ComputeEmulatorRunning%"=="true" when
                running in the Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in the cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a><span data-ttu-id="d07b3-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d07b3-184">Next steps</span></span>
<span data-ttu-id="d07b3-185">Découvrez comment effectuer certaines [tâches de démarrage courantes](cloud-services-startup-tasks-common.md) avec votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="d07b3-185">Learn how to perform some [common startup tasks](cloud-services-startup-tasks-common.md) with your Cloud Service.</span></span>

<span data-ttu-id="d07b3-186">[Créez un package](cloud-services-model-and-package.md) de votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="d07b3-186">[Package](cloud-services-model-and-package.md) your Cloud Service.</span></span>  

<span data-ttu-id="d07b3-187">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span><span class="sxs-lookup"><span data-stu-id="d07b3-187">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span></span>
<span data-ttu-id="d07b3-188">[Task]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span><span class="sxs-lookup"><span data-stu-id="d07b3-188">[Task]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span></span>
<span data-ttu-id="d07b3-189">[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup</span><span class="sxs-lookup"><span data-stu-id="d07b3-189">[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup</span></span>
<span data-ttu-id="d07b3-190">[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime</span><span class="sxs-lookup"><span data-stu-id="d07b3-190">[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime</span></span>
<span data-ttu-id="d07b3-191">[Environment]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span><span class="sxs-lookup"><span data-stu-id="d07b3-191">[Environment]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span></span>
<span data-ttu-id="d07b3-192">[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span><span class="sxs-lookup"><span data-stu-id="d07b3-192">[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span></span>
<span data-ttu-id="d07b3-193">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span><span class="sxs-lookup"><span data-stu-id="d07b3-193">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span></span>
<span data-ttu-id="d07b3-194">[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx</span><span class="sxs-lookup"><span data-stu-id="d07b3-194">[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx</span></span>
