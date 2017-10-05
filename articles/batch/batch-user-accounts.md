---
title: "Exécuter des tâches sous des comptes d’utilisateur dans Azure Batch | Microsoft Docs"
description: "Configurer des comptes d’utilisateur pour exécuter des tâches dans Azure Batch"
services: batch
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.openlocfilehash: d408c0565c0ed81fc97cc2b3976a4fc233e31302
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="run-tasks-under-user-accounts-in-batch"></a><span data-ttu-id="f5a25-103">Exécuter des tâches sous des comptes d’utilisateur dans Azure Batch</span><span class="sxs-lookup"><span data-stu-id="f5a25-103">Run tasks under user accounts in Batch</span></span>

<span data-ttu-id="f5a25-104">Dans Azure Batch, une tâche s’exécute toujours sous un compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f5a25-104">A task in Azure Batch always runs under a user account.</span></span> <span data-ttu-id="f5a25-105">Par défaut, les tâches s’exécutent sous des comptes d’utilisateur standard qui ne possèdent pas de droits d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f5a25-105">By default, tasks run under standard user accounts, without administrator permissions.</span></span> <span data-ttu-id="f5a25-106">Ces paramètres de compte d’utilisateur par défaut sont généralement suffisants.</span><span class="sxs-lookup"><span data-stu-id="f5a25-106">These default user account settings are typically sufficient.</span></span> <span data-ttu-id="f5a25-107">Toutefois, pour certains scénarios, il est utile de pouvoir configurer le compte d’utilisateur sous lequel vous voulez exécuter une tâche.</span><span class="sxs-lookup"><span data-stu-id="f5a25-107">For certain scenarios, however, it's useful to be able to configure the user account under which you want a task to run.</span></span> <span data-ttu-id="f5a25-108">Cet article décrit les types de comptes d’utilisateur et la manière dont vous pouvez les configurer pour votre scénario.</span><span class="sxs-lookup"><span data-stu-id="f5a25-108">This article discusses the types of user accounts and how you can configure them for your scenario.</span></span>

## <a name="types-of-user-accounts"></a><span data-ttu-id="f5a25-109">Types de comptes d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="f5a25-109">Types of user accounts</span></span>

<span data-ttu-id="f5a25-110">Azure Batch offre deux types comptes d’utilisateur pour l’exécution des tâches :</span><span class="sxs-lookup"><span data-stu-id="f5a25-110">Azure Batch provides two types of user accounts for running tasks:</span></span>

- <span data-ttu-id="f5a25-111">**Comptes d’utilisateur automatique.**</span><span class="sxs-lookup"><span data-stu-id="f5a25-111">**Auto-user accounts.**</span></span> <span data-ttu-id="f5a25-112">Les comptes d’utilisateur automatique sont des comptes d’utilisateurs intégrés, créés automatiquement par le service Batch.</span><span class="sxs-lookup"><span data-stu-id="f5a25-112">Auto-user accounts are built-in user accounts that are created automatically by the Batch service.</span></span> <span data-ttu-id="f5a25-113">Par défaut, les tâches sont exécutées sous un compte d’utilisateur automatique.</span><span class="sxs-lookup"><span data-stu-id="f5a25-113">By default, tasks run under an auto-user account.</span></span> <span data-ttu-id="f5a25-114">Vous pouvez configurer la spécification d’utilisateur automatique pour une tâche afin d’indiquer le compte d’utilisateur automatique sous lequel la tâche doit être exécutée.</span><span class="sxs-lookup"><span data-stu-id="f5a25-114">You can configure the auto-user specification for a task to indicate under which auto-user account a task should run.</span></span> <span data-ttu-id="f5a25-115">La spécification d’utilisateur automatique vous permet de spécifier le niveau d’élévation et l’étendue du compte d’utilisateur automatique qui exécutera la tâche.</span><span class="sxs-lookup"><span data-stu-id="f5a25-115">The auto-user specification allows you to specify the elevation level and scope of the auto-user account that will run the task.</span></span> 

- <span data-ttu-id="f5a25-116">**Un compte d’utilisateur nommé.**</span><span class="sxs-lookup"><span data-stu-id="f5a25-116">**A named user account.**</span></span> <span data-ttu-id="f5a25-117">Vous pouvez spécifier un ou plusieurs comptes d’utilisateur nommé pour un pool au moment de sa création.</span><span class="sxs-lookup"><span data-stu-id="f5a25-117">You can specify one or more named user accounts for a pool when you create the pool.</span></span> <span data-ttu-id="f5a25-118">Chaque compte d’utilisateur est créé sur chaque nœud du pool.</span><span class="sxs-lookup"><span data-stu-id="f5a25-118">Each user account is created on each node of the pool.</span></span> <span data-ttu-id="f5a25-119">En plus du nom de compte, vous pouvez spécifier le mot de passe utilisateur, le niveau d’élévation, ainsi que, pour les pools Linux, la clé privée SSH.</span><span class="sxs-lookup"><span data-stu-id="f5a25-119">In addition to the account name, you specify the user account password, elevation level, and, for Linux pools, the SSH private key.</span></span> <span data-ttu-id="f5a25-120">Lorsque vous ajoutez une tâche, vous pouvez spécifier le compte d’utilisateur nommé sous lequel la tâche doit s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="f5a25-120">When you add a task, you can specify the named user account under which that task should run.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="f5a25-121">La version du service Batch 2017-01-01.4.0 introduit une modification qui vous oblige à mettre à jour votre code pour appeler cette version.</span><span class="sxs-lookup"><span data-stu-id="f5a25-121">The Batch service version 2017-01-01.4.0 introduces a breaking change that requires that you update your code to call that version.</span></span> <span data-ttu-id="f5a25-122">Si vous migrez du code à partir d’une version antérieure de Batch, notez que la propriété **runElevated** n’est plus prise en charge dans les bibliothèques d’API REST ou du client Batch.</span><span class="sxs-lookup"><span data-stu-id="f5a25-122">If you are migrating code from an older version of Batch, note that the **runElevated** property is no longer supported in the REST API or Batch client libraries.</span></span> <span data-ttu-id="f5a25-123">Utilisez la nouvelle propriété **userIdentity** d’une tâche pour spécifier le niveau d’élévation.</span><span class="sxs-lookup"><span data-stu-id="f5a25-123">Use the new **userIdentity** property of a task to specify elevation level.</span></span> <span data-ttu-id="f5a25-124">Consultez la section intitulée [Mettre à jour votre code vers la dernière bibliothèque du client Batch](#update-your-code-to-the-latest-batch-client-library) pour savoir comment mettre à jour votre code Batch si vous utilisez l’une des bibliothèques clientes.</span><span class="sxs-lookup"><span data-stu-id="f5a25-124">See the section titled [Update your code to the latest Batch client library](#update-your-code-to-the-latest-batch-client-library) for quick guidelines for updating your Batch code if you are using one of the client libraries.</span></span>
>
>

> [!NOTE] 
> <span data-ttu-id="f5a25-125">Pour des raisons de sécurité, les comptes d’utilisateur décrits dans cet article ne prennent en charge ni le protocole RDP (Remote Desktop), ni le protocole SSH (Secure Shell).</span><span class="sxs-lookup"><span data-stu-id="f5a25-125">The user accounts discussed in this article do not support Remote Desktop Protocol (RDP) or Secure Shell (SSH), for security reasons.</span></span> 
>
> <span data-ttu-id="f5a25-126">Pour vous connecter à un nœud qui exécute une configuration de machine virtuelle Linux via le protocole SSH, consultez [Installer et configurer le Bureau à distance pour effectuer une connexion à une machine virtuelle Linux dans Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="f5a25-126">To connect to a node running the Linux virtual machine configuration via SSH, see [Use Remote Desktop to a Linux VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span></span> <span data-ttu-id="f5a25-127">Pour vous connecter à des nœuds exécutant Windows via RDP, consultez [Connexion à une machine virtuelle Azure exécutant Windows](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="f5a25-127">To connect to nodes running Windows via RDP, see [Connect to a Windows Server VM](../virtual-machines/windows/connect-logon.md).</span></span><br /><br />
> <span data-ttu-id="f5a25-128">Pour vous connecter à un nœud qui exécute la configuration du service cloud via RDP, consultez [Activer une connexion Bureau à distance pour un rôle dans Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f5a25-128">To connect to a node running the cloud service configuration via RDP, see [Enable Remote Desktop Connection for a Role in Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span></span>
>
>

## <a name="user-account-access-to-files-and-directories"></a><span data-ttu-id="f5a25-129">Accès du compte d’utilisateur aux fichiers et répertoires</span><span class="sxs-lookup"><span data-stu-id="f5a25-129">User account access to files and directories</span></span>

<span data-ttu-id="f5a25-130">Les comptes d’utilisateur automatique et nommé disposent tous deux d’un accès en lecture/écriture au répertoire de travail de la tâche, au répertoire partagé et au répertoire de tâches de plusieurs instances.</span><span class="sxs-lookup"><span data-stu-id="f5a25-130">Both an auto-user account and a named user account have read/write access to the task’s working directory, shared directory, and multi-instance tasks directory.</span></span> <span data-ttu-id="f5a25-131">Les deux types de comptes ont accès en lecture aux répertoires des tâches de démarrage et préparation d’un travail.</span><span class="sxs-lookup"><span data-stu-id="f5a25-131">Both types of accounts have read access to the startup and job preparation directories.</span></span>

<span data-ttu-id="f5a25-132">Si une tâche s’exécute sous le même compte que celui utilisé pour exécuter une tâche de démarrage, la tâche dispose d’un accès en lecture-écriture au répertoire de la tâche de démarrage.</span><span class="sxs-lookup"><span data-stu-id="f5a25-132">If a task runs under the same account that was used for running a start task, the task has read-write access to the start task directory.</span></span> <span data-ttu-id="f5a25-133">De la même manière, si une tâche s’exécute sous le même compte que celui utilisé pour exécuter une tâche de préparation d’un travail, la tâche dispose d’un accès en lecture-écriture au répertoire de la tâche de préparation.</span><span class="sxs-lookup"><span data-stu-id="f5a25-133">Similarly, if a task runs under the same account that was used for running a job preparation task, the task has read-write access to the job preparation task directory.</span></span> <span data-ttu-id="f5a25-134">Si une tâche s’exécute sous un compte différent de celui utilisé pour la tâche de démarrage ou la tâche de préparation, la tâche dispose uniquement d’un accès en lecture au répertoire correspondant.</span><span class="sxs-lookup"><span data-stu-id="f5a25-134">If a task runs under a different account than the start task or job preparation task, then the task has only read access to the respective directory.</span></span>

<span data-ttu-id="f5a25-135">Pour plus d’informations sur l’accès aux fichiers et répertoires à partir d’une tâche, consultez [Développer des solutions de calcul parallèles à grande échelle avec Batch](batch-api-basics.md#files-and-directories).</span><span class="sxs-lookup"><span data-stu-id="f5a25-135">For more information on accessing files and directories from a task, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#files-and-directories).</span></span>

## <a name="elevated-access-for-tasks"></a><span data-ttu-id="f5a25-136">Accès aux tâches avec élévation de privilèges</span><span class="sxs-lookup"><span data-stu-id="f5a25-136">Elevated access for tasks</span></span> 

<span data-ttu-id="f5a25-137">Le niveau d’élévation du compte d’utilisateur indique si une tâche s’exécute dans le cadre d’un accès avec élévation de privilèges.</span><span class="sxs-lookup"><span data-stu-id="f5a25-137">The user account's elevation level indicates whether a task runs with elevated access.</span></span> <span data-ttu-id="f5a25-138">Les comptes d’utilisateur automatique et nommé peuvent s’exécuter dans le cadre d’un accès avec élévation de privilèges.</span><span class="sxs-lookup"><span data-stu-id="f5a25-138">Both an auto-user account and a named user account can run with elevated access.</span></span> <span data-ttu-id="f5a25-139">Il existe deux options de niveau d’élévation :</span><span class="sxs-lookup"><span data-stu-id="f5a25-139">The two options for elevation level are:</span></span>

- <span data-ttu-id="f5a25-140">**NonAdmin :** la tâche s’exécute en tant qu’utilisateur standard sans accès avec élévation de privilèges.</span><span class="sxs-lookup"><span data-stu-id="f5a25-140">**NonAdmin:** The task runs as a standard user without elevated access.</span></span> <span data-ttu-id="f5a25-141">Le niveau d’élévation par défaut pour un compte d’utilisateur Batch est toujours **NonAdmin**.</span><span class="sxs-lookup"><span data-stu-id="f5a25-141">The default elevation level for a Batch user account is always **NonAdmin**.</span></span>
- <span data-ttu-id="f5a25-142">**Admin :** la tâche s’exécute en tant qu’utilisateur disposant d’un accès avec élévation de privilèges et fonctionne avec des autorisations d’administrateur complètes.</span><span class="sxs-lookup"><span data-stu-id="f5a25-142">**Admin:** The task runs as a user with elevated access and operates with full Administrator permissions.</span></span> 

## <a name="auto-user-accounts"></a><span data-ttu-id="f5a25-143">Comptes d’utilisateur automatique</span><span class="sxs-lookup"><span data-stu-id="f5a25-143">Auto-user accounts</span></span>

<span data-ttu-id="f5a25-144">Par défaut, les tâches s’exécutent dans Batch sous un compte d’utilisateur automatique, en tant qu’utilisateur standard qui ne dispose pas d’un accès avec élévation de privilèges, et avec une étendue de tâche bien définie.</span><span class="sxs-lookup"><span data-stu-id="f5a25-144">By default, tasks run in Batch under an auto-user account, as a standard user without elevated access, and with task scope.</span></span> <span data-ttu-id="f5a25-145">Lorsque la spécification d’utilisateur automatique est configurée pour l’étendue de la tâche, le service Batch crée un compte d’utilisateur automatique pour cette tâche uniquement.</span><span class="sxs-lookup"><span data-stu-id="f5a25-145">When the auto-user specification is configured for task scope, the Batch service creates an auto-user account for that task only.</span></span>

<span data-ttu-id="f5a25-146">L’étendue de la tâche peut être remplacée par une étendue de pool.</span><span class="sxs-lookup"><span data-stu-id="f5a25-146">The alternative to task scope is pool scope.</span></span> <span data-ttu-id="f5a25-147">Lorsque la spécification d’utilisateur automatique d’une tâche est configurée pour l’étendue du pool, la tâche s’exécute sous un compte d’utilisateur automatique disponible pour n’importe quelle tâche dans le pool.</span><span class="sxs-lookup"><span data-stu-id="f5a25-147">When the auto-user specification for a task is configured for pool scope, the task runs under an auto-user account that is available to any task in the pool.</span></span> <span data-ttu-id="f5a25-148">Pour plus d’informations sur l’étendue du pool, consultez la section intitulée [Exécution d’une tâche en tant qu’utilisateur automatique avec une étendue de pool](#run-a-task-as-the-autouser-with-pool-scope).</span><span class="sxs-lookup"><span data-stu-id="f5a25-148">For more information about pool scope, see the section titled [Run a task as the auto-user with pool scope](#run-a-task-as-the-autouser-with-pool-scope).</span></span>   

<span data-ttu-id="f5a25-149">L’étendue par défaut est différente sur les nœuds Windows et Linux :</span><span class="sxs-lookup"><span data-stu-id="f5a25-149">The default scope is different on Windows and Linux nodes:</span></span>

- <span data-ttu-id="f5a25-150">Sur les nœuds Windows, les tâches s’exécutent sous l’étendue de la tâche par défaut.</span><span class="sxs-lookup"><span data-stu-id="f5a25-150">On Windows nodes, tasks run under task scope by default.</span></span>
- <span data-ttu-id="f5a25-151">Les nœuds Linux s’exécutent toujours sous l’étendue du pool.</span><span class="sxs-lookup"><span data-stu-id="f5a25-151">Linux nodes always run under pool scope.</span></span>

<span data-ttu-id="f5a25-152">Il existe quatre configurations possibles pour la spécification d’utilisateur automatique, chacune correspondant à un compte d’utilisateur automatique unique :</span><span class="sxs-lookup"><span data-stu-id="f5a25-152">There are four possible configurations for the auto-user specification, each of which corresponds to a unique auto-user account:</span></span>

- <span data-ttu-id="f5a25-153">Accès non-admin avec étendue de la tâche (la spécification d’utilisateur automatique par défaut)</span><span class="sxs-lookup"><span data-stu-id="f5a25-153">Non-admin access with task scope (the default auto-user specification)</span></span>
- <span data-ttu-id="f5a25-154">Accès admin (avec élévation de privilèges) avec étendue de la tâche</span><span class="sxs-lookup"><span data-stu-id="f5a25-154">Admin (elevated) access with task scope</span></span>
- <span data-ttu-id="f5a25-155">Accès non-admin avec étendue de pool</span><span class="sxs-lookup"><span data-stu-id="f5a25-155">Non-admin access with pool scope</span></span>
- <span data-ttu-id="f5a25-156">Accès admin avec étendue de pool</span><span class="sxs-lookup"><span data-stu-id="f5a25-156">Admin access with pool scope</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="f5a25-157">Les tâches en cours d’exécution sous l’étendue de la tâche ne peuvent pas accéder aux tâches sur un nœud.</span><span class="sxs-lookup"><span data-stu-id="f5a25-157">Tasks running under task scope do not have de facto access to other tasks on a node.</span></span> <span data-ttu-id="f5a25-158">Toutefois, un utilisateur malveillant ayant accès au compte pourrait contourner cette restriction en soumettant une tâche qui s’exécute avec des privilèges d’administrateur et qui accède à d’autres répertoires de la tâche.</span><span class="sxs-lookup"><span data-stu-id="f5a25-158">However, a malicious user with access to the account could work around this restriction by submitting a task that runs with administrator privileges and accesses other task directories.</span></span> <span data-ttu-id="f5a25-159">Un utilisateur malveillant pourrait également utiliser le protocole RDP ou SSH pour se connecter à un nœud.</span><span class="sxs-lookup"><span data-stu-id="f5a25-159">A malicious user could also use RDP or SSH to connect to a node.</span></span> <span data-ttu-id="f5a25-160">Il est important de protéger l’accès aux clés de votre compte Batch afin d’éviter un tel scénario.</span><span class="sxs-lookup"><span data-stu-id="f5a25-160">It's important to protect access to your Batch account keys to prevent such a scenario.</span></span> <span data-ttu-id="f5a25-161">Si vous pensez que votre compte a peut-être été compromis, veillez à régénérer vos clés.</span><span class="sxs-lookup"><span data-stu-id="f5a25-161">If you suspect your account may have been compromised, be sure to regenerate your keys.</span></span>
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a><span data-ttu-id="f5a25-162">Exécution d’une tâche en tant qu’utilisateur automatique disposant d’un accès avec élévation de privilèges</span><span class="sxs-lookup"><span data-stu-id="f5a25-162">Run a task as an auto-user with elevated access</span></span>

<span data-ttu-id="f5a25-163">Vous pouvez configurer la spécification d’utilisateur automatique pour des privilèges d’administrateur lorsque vous avez besoin d’exécuter une tâche avec un accès avec élévation de privilèges.</span><span class="sxs-lookup"><span data-stu-id="f5a25-163">You can configure the auto-user specification for administrator privileges when you need to run a task with elevated access.</span></span> <span data-ttu-id="f5a25-164">Par exemple, une tâche de démarrage peut avoir besoin d’un accès avec élévation de privilèges pour pouvoir installer un logiciel sur le nœud.</span><span class="sxs-lookup"><span data-stu-id="f5a25-164">For example, a start task may need elevated access to install software on the node.</span></span>

> [!NOTE] 
> <span data-ttu-id="f5a25-165">En général, il est préférable d’utiliser l’accès avec élévation de privilèges uniquement lorsque cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f5a25-165">In general, it's best to use elevated access only when necessary.</span></span> <span data-ttu-id="f5a25-166">Les meilleures pratiques recommandent d’accorder le privilège minimal nécessaire pour atteindre le résultat souhaité.</span><span class="sxs-lookup"><span data-stu-id="f5a25-166">Best practices recommend granting the minimum privilege necessary to achieve the desired outcome.</span></span> <span data-ttu-id="f5a25-167">Par exemple, si une tâche de démarrage installe le logiciel pour l’utilisateur actuel, et non pour l’ensemble des utilisateurs, vous pouvez sans doute éviter d’accorder aux tâches un accès avec élévation de privilèges.</span><span class="sxs-lookup"><span data-stu-id="f5a25-167">For example, if a start task installs software for the current user, instead of for all users, you may be able to avoid granting elevated access to tasks.</span></span> <span data-ttu-id="f5a25-168">Vous pouvez configurer la spécification d’utilisateur automatique d’étendue du pool et d’accès non-admin pour toutes les tâches qui doivent s’exécuter sous le même compte, y compris la tâche de démarrage.</span><span class="sxs-lookup"><span data-stu-id="f5a25-168">You can configure the auto-user specification for pool scope and non-admin access for all tasks that need to run under the same account, including the start task.</span></span> 
>
>

<span data-ttu-id="f5a25-169">Les extraits de code suivants montrent comment configurer la spécification d’utilisateur automatique.</span><span class="sxs-lookup"><span data-stu-id="f5a25-169">The following code snippets show how to configure the auto-user specification.</span></span> <span data-ttu-id="f5a25-170">Les exemples définissent le niveau d’élévation sur `Admin` et l’étendue sur `Task`.</span><span class="sxs-lookup"><span data-stu-id="f5a25-170">The examples set the elevation level to `Admin` and the scope to `Task`.</span></span> <span data-ttu-id="f5a25-171">L’étendue de la tâche est le paramètre par défaut, mais elle est incluse ici à titre d’exemple.</span><span class="sxs-lookup"><span data-stu-id="f5a25-171">Task scope is the default setting, but is included here for the sake of example.</span></span>

#### <a name="batch-net"></a><span data-ttu-id="f5a25-172">.NET Batch</span><span class="sxs-lookup"><span data-stu-id="f5a25-172">Batch .NET</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a><span data-ttu-id="f5a25-173">Java Batch</span><span class="sxs-lookup"><span data-stu-id="f5a25-173">Batch Java</span></span>

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a><span data-ttu-id="f5a25-174">Python Batch</span><span class="sxs-lookup"><span data-stu-id="f5a25-174">Batch Python</span></span>

```python
user = batchmodels.UserIdentity(
    auto_user=batchmodels.AutoUserSpecification(
        elevation_level=batchmodels.ElevationLevel.admin,
        scope=batchmodels.AutoUserScope.task))
task = batchmodels.TaskAddParameter(
    id='task_1',
    command_line='cmd /c "echo hello world"',
    user_identity=user)
batch_client.task.add(job_id=jobid, task=task)
```

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a><span data-ttu-id="f5a25-175">Exécution d’une tâche en tant qu’utilisateur automatique avec une étendue de pool</span><span class="sxs-lookup"><span data-stu-id="f5a25-175">Run a task as an auto-user with pool scope</span></span>

<span data-ttu-id="f5a25-176">Lorsqu’un nœud est approvisionné, deux comptes d’utilisateur automatique au niveau du pool sont créés sur chaque nœud du pool, l’un disposant d’un accès avec élévation de privilèges, l’autre non.</span><span class="sxs-lookup"><span data-stu-id="f5a25-176">When a node is provisioned, two pool-wide auto-user accounts are created on each node in the pool, one with elevated access, and one without elevated access.</span></span> <span data-ttu-id="f5a25-177">En définissant l’étendue du compte d’utilisateur automatique sur l’étendue du pool pour une tâche donnée, la tâche s’exécute sous l’un de ces deux comptes d’utilisateur automatique au niveau du pool.</span><span class="sxs-lookup"><span data-stu-id="f5a25-177">Setting the auto-user's scope to pool scope for a given task runs the task under one of these two pool-wide auto-user accounts.</span></span> 

<span data-ttu-id="f5a25-178">Lorsque vous spécifiez l’étendue du pool pour l’utilisateur automatique, toutes les tâches qui s’exécutent avec un accès administrateur s’exécutent sous le même compte d’utilisateur automatique au niveau du pool.</span><span class="sxs-lookup"><span data-stu-id="f5a25-178">When you specify pool scope for the auto-user, all tasks that run with administrator access run under the same pool-wide auto-user account.</span></span> <span data-ttu-id="f5a25-179">De même, les tâches qui s’exécutent sans autorisations d’administrateur s’exécutent également sous un seul compte d’utilisateur automatique au niveau du pool.</span><span class="sxs-lookup"><span data-stu-id="f5a25-179">Similarly, tasks that run without administrator permissions also run under a single pool-wide auto-user account.</span></span> 

> [!NOTE] 
> <span data-ttu-id="f5a25-180">Les deux comptes d’utilisateur automatique au niveau du pool sont des comptes distincts.</span><span class="sxs-lookup"><span data-stu-id="f5a25-180">The two pool-wide auto-user accounts are separate accounts.</span></span> <span data-ttu-id="f5a25-181">Le tâches qui s’exécutent sous le compte d’administrateur au niveau du pool ne peuvent pas partager des données avec les tâches qui s’exécutent sous le compte d’utilisateur standard, et inversement.</span><span class="sxs-lookup"><span data-stu-id="f5a25-181">Tasks running under the pool-wide administrative account cannot share data with tasks running under the standard account, and vice versa.</span></span> 
>
>

<span data-ttu-id="f5a25-182">L’avantage d’exécuter une tâche sous le même compte d’utilisateur automatique est que les tâches sont en mesure de partager des données avec d’autres tâches en cours d’exécution sur le même nœud.</span><span class="sxs-lookup"><span data-stu-id="f5a25-182">The advantage to running under the same auto-user account is that tasks are able to share data with other tasks running on the same node.</span></span>

<span data-ttu-id="f5a25-183">L’exécution de tâches sous l’un des deux comptes d’utilisateur automatique au niveau du pool est utile, par exemple, pour le partage de clés secrètes.</span><span class="sxs-lookup"><span data-stu-id="f5a25-183">Sharing secrets between tasks is one scenario where running tasks under one of the two pool-wide auto-user accounts is useful.</span></span> <span data-ttu-id="f5a25-184">Par exemple, supposons qu’une tâche de démarrage doive configurer une clé secrète dans un nœud utilisé par d’autres tâches.</span><span class="sxs-lookup"><span data-stu-id="f5a25-184">For example, suppose a start task needs to provision a secret onto the node that other tasks can use.</span></span> <span data-ttu-id="f5a25-185">Vous pouvez utiliser l’API Windows Data Protection (DPAPI), mais elle requiert des privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f5a25-185">You could use the Windows Data Protection API (DPAPI), but it requires administrator privileges.</span></span> <span data-ttu-id="f5a25-186">Au lieu de cela, vous pouvez protéger la clé secrète au niveau de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f5a25-186">Instead, you can protect the secret at the user level.</span></span> <span data-ttu-id="f5a25-187">Les tâches qui s’exécutent sous le même compte d’utilisateur peuvent accéder à la clé secrète sans accès avec élévation de privilèges.</span><span class="sxs-lookup"><span data-stu-id="f5a25-187">Tasks running under the same user account can access the secret without elevated access.</span></span>

<span data-ttu-id="f5a25-188">Il peut être également intéressant d’exécuter des tâches sous un compte d’utilisateur automatique avec une étendue de pool dans le cas d’un partage de fichiers MPI (Message Passing Interface).</span><span class="sxs-lookup"><span data-stu-id="f5a25-188">Another scenario where you may want to run tasks under an auto-user account with pool scope is a Message Passing Interface (MPI) file share.</span></span> <span data-ttu-id="f5a25-189">Un partage de fichiers MPI est utile lorsque les nœuds de la tâche MPI doivent travailler sur les mêmes données de fichier.</span><span class="sxs-lookup"><span data-stu-id="f5a25-189">An MPI file share is useful when the nodes in the MPI task need to work on the same file data.</span></span> <span data-ttu-id="f5a25-190">Le nœud principal crée un partage de fichiers auquel les nœuds enfants peuvent accéder s’ils s’exécutent sous le même compte d’utilisateur automatique.</span><span class="sxs-lookup"><span data-stu-id="f5a25-190">The head node creates a file share that the child nodes can access if they are running under the same auto-user account.</span></span> 

<span data-ttu-id="f5a25-191">L’extrait de code suivant définit l’étendue de l’utilisateur automatique sur l’étendue du pool pour une tâche dans Batch .NET.</span><span class="sxs-lookup"><span data-stu-id="f5a25-191">The following code snippet sets the auto-user's scope to pool scope for a task in Batch .NET.</span></span> <span data-ttu-id="f5a25-192">Le niveau d’élévation est omis, afin que la tâche s’exécute sous le compte standard d’utilisateur automatique au niveau du pool.</span><span class="sxs-lookup"><span data-stu-id="f5a25-192">The elevation level is omitted, so the task runs under the standard pool-wide auto-user account.</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a><span data-ttu-id="f5a25-193">Comptes d’utilisateur nommé</span><span class="sxs-lookup"><span data-stu-id="f5a25-193">Named user accounts</span></span>

<span data-ttu-id="f5a25-194">Vous pouvez définir des comptes d’utilisateur nommé lorsque vous créez un pool.</span><span class="sxs-lookup"><span data-stu-id="f5a25-194">You can define named user accounts when you create a pool.</span></span> <span data-ttu-id="f5a25-195">Un compte d’utilisateur nommé possède un nom et un mot de passe que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="f5a25-195">A named user account has a name and password that you provide.</span></span> <span data-ttu-id="f5a25-196">Vous pouvez spécifier le niveau d’élévation pour un compte d’utilisateur nommé.</span><span class="sxs-lookup"><span data-stu-id="f5a25-196">You can specify the elevation level for a named user account.</span></span> <span data-ttu-id="f5a25-197">Pour les nœuds Linux, vous pouvez également fournir une clé privée SSH.</span><span class="sxs-lookup"><span data-stu-id="f5a25-197">For Linux nodes, you can also provide an SSH private key.</span></span>

<span data-ttu-id="f5a25-198">Il existe un compte d’utilisateur nommé sur tous les nœuds du pool et ce compte est disponible sur toutes les tâches en cours d’exécution sur ces nœuds.</span><span class="sxs-lookup"><span data-stu-id="f5a25-198">A named user account exists on all nodes in the pool and is available to all tasks running on those nodes.</span></span> <span data-ttu-id="f5a25-199">Vous pouvez définir n’importe quel nombre d’utilisateurs nommés pour un pool.</span><span class="sxs-lookup"><span data-stu-id="f5a25-199">You may define any number of named users for a pool.</span></span> <span data-ttu-id="f5a25-200">Lorsque vous ajoutez une tâche ou une collection de tâches, vous pouvez indiquer que la tâche s’exécute sous l’un des comptes d’utilisateur nommé définis dans le pool.</span><span class="sxs-lookup"><span data-stu-id="f5a25-200">When you add a task or task collection, you can specify that the task runs under one of the named user accounts defined on the pool.</span></span>

<span data-ttu-id="f5a25-201">Un compte d’utilisateur nommé est utile lorsque vous souhaitez exécuter toutes les tâches d’un travail sous le même compte d’utilisateur, mais que vous voulez les isoler des tâches qui s’exécutent simultanément dans d’autres travaux.</span><span class="sxs-lookup"><span data-stu-id="f5a25-201">A named user account is useful when you want to run all tasks in a job under the same user account, but isolate them from tasks running in other jobs at the same time.</span></span> <span data-ttu-id="f5a25-202">Par exemple, vous pouvez créer un utilisateur nommé pour chaque travail, et exécuter les tâches de chaque travail sous ce compte d’utilisateur nommé.</span><span class="sxs-lookup"><span data-stu-id="f5a25-202">For example, you can create a named user for each job, and run each job's tasks under that named user account.</span></span> <span data-ttu-id="f5a25-203">Chaque travail peut ensuite partager une clé secrète avec ses propres tâches, mais pas avec les tâches qui s’exécutent dans d’autres travaux.</span><span class="sxs-lookup"><span data-stu-id="f5a25-203">Each job can then share a secret with its own tasks, but not with tasks running in other jobs.</span></span>

<span data-ttu-id="f5a25-204">Vous pouvez également utiliser un compte d’utilisateur nommé pour exécuter une tâche qui définit des autorisations sur des ressources externes, telles que des partages de fichiers.</span><span class="sxs-lookup"><span data-stu-id="f5a25-204">You can also use a named user account to run a task that sets permissions on external resources such as file shares.</span></span> <span data-ttu-id="f5a25-205">Avec un compte d’utilisateur nommé, vous pouvez contrôler l’identité de l’utilisateur et utiliser cette identité pour définir des autorisations.</span><span class="sxs-lookup"><span data-stu-id="f5a25-205">With a named user account, you control the user identity and can use that user identity to set permissions.</span></span>  

<span data-ttu-id="f5a25-206">Les comptes d’utilisateur nommé activent le protocole SSH sans mot de passe entre les nœuds Linux.</span><span class="sxs-lookup"><span data-stu-id="f5a25-206">Named user accounts enable password-less SSH between Linux nodes.</span></span> <span data-ttu-id="f5a25-207">Vous pouvez utiliser un compte d’utilisateur nommé avec des nœuds Linux qui doivent exécuter des tâches de plusieurs instances.</span><span class="sxs-lookup"><span data-stu-id="f5a25-207">You can use a named user account with Linux nodes that need to run multi-instance tasks.</span></span> <span data-ttu-id="f5a25-208">Chaque nœud du pool peut exécuter des tâches sous un compte d’utilisateur défini sur le pool entier.</span><span class="sxs-lookup"><span data-stu-id="f5a25-208">Each node in the pool can run tasks under a user account defined on the whole pool.</span></span> <span data-ttu-id="f5a25-209">Pour plus d’informations sur les tâches multi-instances, consultez [Utiliser les tâches multi\-instances pour exécuter des applications MPI (Message Passing Interface) dans Batch](batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="f5a25-209">For more information about multi-instance tasks, see [Use multi\-instance tasks to run MPI applications](batch-mpi.md).</span></span>

### <a name="create-named-user-accounts"></a><span data-ttu-id="f5a25-210">Créer des comptes d’utilisateur nommé</span><span class="sxs-lookup"><span data-stu-id="f5a25-210">Create named user accounts</span></span>

<span data-ttu-id="f5a25-211">Pour créer des comptes d’utilisateur nommé dans Batch, ajoutez une collection de comptes d’utilisateur au pool.</span><span class="sxs-lookup"><span data-stu-id="f5a25-211">To create named user accounts in Batch, add a collection of user accounts to the pool.</span></span> <span data-ttu-id="f5a25-212">Les extraits de code suivants montrent comment créer des comptes d’utilisateur nommé dans .NET, Java et Python.</span><span class="sxs-lookup"><span data-stu-id="f5a25-212">The following code snippets show how to create named user accounts in .NET, Java, and Python.</span></span> <span data-ttu-id="f5a25-213">Ces extraits de code montrent comment créer des comptes nommés admin et non-admin sur un pool.</span><span class="sxs-lookup"><span data-stu-id="f5a25-213">These code snippets show how to create both admin and non-admin named accounts on a pool.</span></span> <span data-ttu-id="f5a25-214">Les exemples montrent comment créer des pools à l’aide de la configuration du service cloud, mais en utilisant la même approche que lors de la création d’un pool Windows ou Linux à l’aide de la configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f5a25-214">The examples create pools using the cloud service configuration, but you use the same approach when creating a Windows or Linux pool using the virtual machine configuration.</span></span>

#### <a name="batch-net-example-windows"></a><span data-ttu-id="f5a25-215">Exemple .NET Batch (Windows)</span><span class="sxs-lookup"><span data-stu-id="f5a25-215">Batch .NET example (Windows)</span></span>

```csharp
CloudPool pool = null;
Console.WriteLine("Creating pool [{0}]...", poolId);

// Create a pool using the cloud service configuration.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                                         
    virtualMachineSize: "small",                                                
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));   

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount("adminUser", "xyz123", ElevationLevel.Admin),
    new UserAccount("nonAdminUser", "123xyz", ElevationLevel.NonAdmin),
};

// Commit the pool.
await pool.CommitAsync();
```

#### <a name="batch-net-example-linux"></a><span data-ttu-id="f5a25-216">Exemple .NET Batch (Linux)</span><span class="sxs-lookup"><span data-stu-id="f5a25-216">Batch .NET example (Linux)</span></span>

```csharp
CloudPool pool = null;

// Obtain a collection of all available node agent SKUs.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of the VM image to use.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain the first node agent SKU in the collection that matches
// Ubuntu Server 14.04. 
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create the virtual machine configuration to use to create the pool.
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

Console.WriteLine("Creating pool [{0}]...", poolId);

// Create the unbound pool.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                             
    virtualMachineSize: "Standard_A1",                                      
    virtualMachineConfiguration: virtualMachineConfiguration);                  

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount(
        name: "adminUser",
        password: "xyz123",
        elevationLevel: ElevationLevel.Admin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 12345,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
    new UserAccount(
        name: "nonAdminUser",
        password: "123xyz",
        elevationLevel: ElevationLevel.NonAdmin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 45678,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
};

// Commit the pool.
await pool.CommitAsync();
```


#### <a name="batch-java-example"></a><span data-ttu-id="f5a25-217">Exemple Java Batch</span><span class="sxs-lookup"><span data-stu-id="f5a25-217">Batch Java example</span></span>

```java
List<UserAccount> userList = new ArrayList<>();
userList.add(new UserAccount().withName(adminUserAccountName).withPassword(adminPassword).withElevationLevel(ElevationLevel.ADMIN));
userList.add(new UserAccount().withName(nonAdminUserAccountName).withPassword(nonAdminPassword).withElevationLevel(ElevationLevel.NONADMIN));
PoolAddParameter addParameter = new PoolAddParameter()
        .withId(poolId)
        .withTargetDedicatedNodes(POOL_VM_COUNT)
        .withVmSize(POOL_VM_SIZE)
        .withCloudServiceConfiguration(configuration)
        .withUserAccounts(userList);
batchClient.poolOperations().createPool(addParameter);
```

#### <a name="batch-python-example"></a><span data-ttu-id="f5a25-218">Exemple Python Batch</span><span class="sxs-lookup"><span data-stu-id="f5a25-218">Batch Python example</span></span>

```python
users = [
    batchmodels.UserAccount(
        name='pool-admin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.admin)
    batchmodels.UserAccount(
        name='pool-nonadmin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.nonadmin)
]
pool = batchmodels.PoolAddParameter(
    id=pool_id,
    user_accounts=users,
    virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
        image_reference=image_ref_to_use,
        node_agent_sku_id=sku_to_use),
    vm_size=vm_size,
    target_dedicated=vm_count)
batch_client.pool.add(pool)
```

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a><span data-ttu-id="f5a25-219">Exécution d’une tâche sous un compte d’utilisateur nommé disposant d’un accès avec élévation de privilèges</span><span class="sxs-lookup"><span data-stu-id="f5a25-219">Run a task under a named user account with elevated access</span></span>

<span data-ttu-id="f5a25-220">Pour exécuter une tâche en tant qu’un utilisateur avec élévation de privilèges, définissez la propriété **UserIdentity** de la tâche sur un compte d’utilisateur nommé dont la propriété **ElevationLevel** a été définie sur `Admin`.</span><span class="sxs-lookup"><span data-stu-id="f5a25-220">To run a task as an elevated user, set the task's **UserIdentity** property to a named user account that was created with its **ElevationLevel** property set to `Admin`.</span></span>

<span data-ttu-id="f5a25-221">Cet extrait de code spécifie que la tâche doit s’exécuter sous un compte d’utilisateur nommé.</span><span class="sxs-lookup"><span data-stu-id="f5a25-221">This code snippet specifies that the task should run under a named user account.</span></span> <span data-ttu-id="f5a25-222">Ce compte d’utilisateur nommé a été défini sur le pool au moment de la création du pool.</span><span class="sxs-lookup"><span data-stu-id="f5a25-222">This named user account was defined on the pool when the pool was created.</span></span> <span data-ttu-id="f5a25-223">Dans ce cas, le compte d’utilisateur nommé a été créé avec des autorisations d’administrateur :</span><span class="sxs-lookup"><span data-stu-id="f5a25-223">In this case, the named user account was created with admin permissions:</span></span>

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-to-the-latest-batch-client-library"></a><span data-ttu-id="f5a25-224">Mettre à jour votre code vers la dernière bibliothèque du client Batch</span><span class="sxs-lookup"><span data-stu-id="f5a25-224">Update your code to the latest Batch client library</span></span>

<span data-ttu-id="f5a25-225">La version du service Batch 2017-01-01.4.0 introduit une modification qui remplace la propriété **runElevated** disponible dans les versions précédentes par la propriété **userIdentity**.</span><span class="sxs-lookup"><span data-stu-id="f5a25-225">The Batch service version 2017-01-01.4.0 introduces a breaking change, replacing the **runElevated** property available in earlier versions with the **userIdentity** property.</span></span> <span data-ttu-id="f5a25-226">Les tableaux suivants fournissent un mappage simple que vous pouvez utiliser pour mettre à jour votre code à partir de versions antérieures des bibliothèques clientes.</span><span class="sxs-lookup"><span data-stu-id="f5a25-226">The following tables provide a simple mapping that you can use to update your code from earlier versions of the client libraries.</span></span>

### <a name="batch-net"></a><span data-ttu-id="f5a25-227">.NET Batch</span><span class="sxs-lookup"><span data-stu-id="f5a25-227">Batch .NET</span></span>

| <span data-ttu-id="f5a25-228">Si votre code utilise...</span><span class="sxs-lookup"><span data-stu-id="f5a25-228">If your code uses...</span></span>                  | <span data-ttu-id="f5a25-229">Mettez-le à jour vers...</span><span class="sxs-lookup"><span data-stu-id="f5a25-229">Update it to....</span></span>                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| <span data-ttu-id="f5a25-230">`CloudTask.RunElevated` non spécifié</span><span class="sxs-lookup"><span data-stu-id="f5a25-230">`CloudTask.RunElevated` not specified</span></span> | <span data-ttu-id="f5a25-231">Aucune mise à jour requise</span><span class="sxs-lookup"><span data-stu-id="f5a25-231">No update required</span></span>                                                                                               |

### <a name="batch-java"></a><span data-ttu-id="f5a25-232">Java Batch</span><span class="sxs-lookup"><span data-stu-id="f5a25-232">Batch Java</span></span>

| <span data-ttu-id="f5a25-233">Si votre code utilise...</span><span class="sxs-lookup"><span data-stu-id="f5a25-233">If your code uses...</span></span>                      | <span data-ttu-id="f5a25-234">Mettez-le à jour vers...</span><span class="sxs-lookup"><span data-stu-id="f5a25-234">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| <span data-ttu-id="f5a25-235">`CloudTask.withRunElevated` non spécifié</span><span class="sxs-lookup"><span data-stu-id="f5a25-235">`CloudTask.withRunElevated` not specified</span></span> | <span data-ttu-id="f5a25-236">Aucune mise à jour requise</span><span class="sxs-lookup"><span data-stu-id="f5a25-236">No update required</span></span>                                                                                                                     |

### <a name="batch-python"></a><span data-ttu-id="f5a25-237">Python Batch</span><span class="sxs-lookup"><span data-stu-id="f5a25-237">Batch Python</span></span>

| <span data-ttu-id="f5a25-238">Si votre code utilise...</span><span class="sxs-lookup"><span data-stu-id="f5a25-238">If your code uses...</span></span>                      | <span data-ttu-id="f5a25-239">Mettez-le à jour vers...</span><span class="sxs-lookup"><span data-stu-id="f5a25-239">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | <span data-ttu-id="f5a25-240">`user_identity=user`, où</span><span class="sxs-lookup"><span data-stu-id="f5a25-240">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | <span data-ttu-id="f5a25-241">`user_identity=user`, où</span><span class="sxs-lookup"><span data-stu-id="f5a25-241">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| <span data-ttu-id="f5a25-242">`run_elevated` non spécifié</span><span class="sxs-lookup"><span data-stu-id="f5a25-242">`run_elevated` not specified</span></span> | <span data-ttu-id="f5a25-243">Aucune mise à jour requise</span><span class="sxs-lookup"><span data-stu-id="f5a25-243">No update required</span></span>                                                                                                                                  |


## <a name="next-steps"></a><span data-ttu-id="f5a25-244">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f5a25-244">Next steps</span></span>

### <a name="batch-forum"></a><span data-ttu-id="f5a25-245">Forum Azure Batch</span><span class="sxs-lookup"><span data-stu-id="f5a25-245">Batch Forum</span></span>

<span data-ttu-id="f5a25-246">Le [Forum Azure Batch](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) sur MSDN est l’endroit idéal pour discuter de Batch et poser des questions sur le service.</span><span class="sxs-lookup"><span data-stu-id="f5a25-246">The [Azure Batch Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="f5a25-247">Consultez le forum pour obtenir des publications utiles et publiez les questions que vous vous posez pendant la création de vos solutions Batch.</span><span class="sxs-lookup"><span data-stu-id="f5a25-247">Head on over for helpful pinned posts, and post your questions as they arise while you build your Batch solutions.</span></span>