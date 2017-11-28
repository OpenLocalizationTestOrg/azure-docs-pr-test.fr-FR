---
title: "tâches aaaRun sous des comptes d’utilisateur dans Azure Batch | Documents Microsoft"
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
ms.openlocfilehash: 13d7d76451d89a3cca090c4ef24ed0ed781bbf09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-under-user-accounts-in-batch"></a><span data-ttu-id="ad22b-103">Exécuter des tâches sous des comptes d’utilisateur dans Azure Batch</span><span class="sxs-lookup"><span data-stu-id="ad22b-103">Run tasks under user accounts in Batch</span></span>

<span data-ttu-id="ad22b-104">Dans Azure Batch, une tâche s’exécute toujours sous un compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ad22b-104">A task in Azure Batch always runs under a user account.</span></span> <span data-ttu-id="ad22b-105">Par défaut, les tâches s’exécutent sous des comptes d’utilisateur standard qui ne possèdent pas de droits d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ad22b-105">By default, tasks run under standard user accounts, without administrator permissions.</span></span> <span data-ttu-id="ad22b-106">Ces paramètres de compte d’utilisateur par défaut sont généralement suffisants.</span><span class="sxs-lookup"><span data-stu-id="ad22b-106">These default user account settings are typically sufficient.</span></span> <span data-ttu-id="ad22b-107">Toutefois, pour certains scénarios, il est utile toobe tooconfigure en mesure de hello compte d’utilisateur sous lequel un toorun de tâche.</span><span class="sxs-lookup"><span data-stu-id="ad22b-107">For certain scenarios, however, it's useful toobe able tooconfigure hello user account under which you want a task toorun.</span></span> <span data-ttu-id="ad22b-108">Cet article décrit les types de comptes d’utilisateur et comment vous pouvez les configurer pour votre scénario hello.</span><span class="sxs-lookup"><span data-stu-id="ad22b-108">This article discusses hello types of user accounts and how you can configure them for your scenario.</span></span>

## <a name="types-of-user-accounts"></a><span data-ttu-id="ad22b-109">Types de comptes d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="ad22b-109">Types of user accounts</span></span>

<span data-ttu-id="ad22b-110">Azure Batch offre deux types comptes d’utilisateur pour l’exécution des tâches :</span><span class="sxs-lookup"><span data-stu-id="ad22b-110">Azure Batch provides two types of user accounts for running tasks:</span></span>

- <span data-ttu-id="ad22b-111">**Comptes d’utilisateur automatique.**</span><span class="sxs-lookup"><span data-stu-id="ad22b-111">**Auto-user accounts.**</span></span> <span data-ttu-id="ad22b-112">Comptes d’utilisateur d’automatique sont des comptes d’utilisateurs intégrés sont créés automatiquement par hello service Batch.</span><span class="sxs-lookup"><span data-stu-id="ad22b-112">Auto-user accounts are built-in user accounts that are created automatically by hello Batch service.</span></span> <span data-ttu-id="ad22b-113">Par défaut, les tâches sont exécutées sous un compte d’utilisateur automatique.</span><span class="sxs-lookup"><span data-stu-id="ad22b-113">By default, tasks run under an auto-user account.</span></span> <span data-ttu-id="ad22b-114">Vous pouvez configurer la spécification d’auto-utilisateur hello pour un tooindicate tâche sous auto-utilisateur compte une tâche doit s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="ad22b-114">You can configure hello auto-user specification for a task tooindicate under which auto-user account a task should run.</span></span> <span data-ttu-id="ad22b-115">spécification d’auto-utilisateur Hello vous permet de niveau d’élévation toospecify hello et étendue hello auto-du compte d’utilisateur qui exécutera la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="ad22b-115">hello auto-user specification allows you toospecify hello elevation level and scope of hello auto-user account that will run hello task.</span></span> 

- <span data-ttu-id="ad22b-116">**Un compte d’utilisateur nommé.**</span><span class="sxs-lookup"><span data-stu-id="ad22b-116">**A named user account.**</span></span> <span data-ttu-id="ad22b-117">Vous pouvez spécifier un ou plusieurs comptes d’utilisateur nommé pour un pool lorsque vous créez le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="ad22b-117">You can specify one or more named user accounts for a pool when you create hello pool.</span></span> <span data-ttu-id="ad22b-118">Chaque compte d’utilisateur est créé sur chaque nœud du pool de hello.</span><span class="sxs-lookup"><span data-stu-id="ad22b-118">Each user account is created on each node of hello pool.</span></span> <span data-ttu-id="ad22b-119">En outre toohello nom du compte, vous spécifiez hello mot de passe utilisateur, élévation, ainsi que, pour les pools de Linux, la clé privée SSH hello.</span><span class="sxs-lookup"><span data-stu-id="ad22b-119">In addition toohello account name, you specify hello user account password, elevation level, and, for Linux pools, hello SSH private key.</span></span> <span data-ttu-id="ad22b-120">Lorsque vous ajoutez une tâche, vous pouvez spécifier hello appelé compte d’utilisateur sous lequel cette tâche doit s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="ad22b-120">When you add a task, you can specify hello named user account under which that task should run.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="ad22b-121">version du service de traitement par lots Hello 2017-01-01.4.0 introduit une modification avec rupture qui requiert que vous mettez à jour votre code toocall cette version.</span><span class="sxs-lookup"><span data-stu-id="ad22b-121">hello Batch service version 2017-01-01.4.0 introduces a breaking change that requires that you update your code toocall that version.</span></span> <span data-ttu-id="ad22b-122">Si vous êtes la migration du code à partir d’une version antérieure du lot, notez que hello **runElevated** propriété n’est plus pris en charge dans des bibliothèques du client hello API REST ou le lot.</span><span class="sxs-lookup"><span data-stu-id="ad22b-122">If you are migrating code from an older version of Batch, note that hello **runElevated** property is no longer supported in hello REST API or Batch client libraries.</span></span> <span data-ttu-id="ad22b-123">Hello utilisez nouveau **userIdentity** propriété d’un niveau de l’élévation toospecify tâche.</span><span class="sxs-lookup"><span data-stu-id="ad22b-123">Use hello new **userIdentity** property of a task toospecify elevation level.</span></span> <span data-ttu-id="ad22b-124">Consultez la section hello intitulée [mettre à jour votre bibliothèque de client de lot dernier code toohello](#update-your-code-to-the-latest-batch-client-library) pour connaître les instructions de mise à jour de votre code de lot si vous utilisez une des bibliothèques de client hello rapides.</span><span class="sxs-lookup"><span data-stu-id="ad22b-124">See hello section titled [Update your code toohello latest Batch client library](#update-your-code-to-the-latest-batch-client-library) for quick guidelines for updating your Batch code if you are using one of hello client libraries.</span></span>
>
>

> [!NOTE] 
> <span data-ttu-id="ad22b-125">comptes d’utilisateur Hello abordés dans cet article ne prennent pas en charge protocole RDP (Remote Desktop) ou Secure Shell (SSH), pour des raisons de sécurité.</span><span class="sxs-lookup"><span data-stu-id="ad22b-125">hello user accounts discussed in this article do not support Remote Desktop Protocol (RDP) or Secure Shell (SSH), for security reasons.</span></span> 
>
> <span data-ttu-id="ad22b-126">tooconnect tooa nœud en cours d’exécution hello Linux configuration d’ordinateur virtuel via SSH, consultez [tooa de bureau à distance d’utilisation VM Linux dans Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="ad22b-126">tooconnect tooa node running hello Linux virtual machine configuration via SSH, see [Use Remote Desktop tooa Linux VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span></span> <span data-ttu-id="ad22b-127">toonodes tooconnect Windows en cours d’exécution via le protocole RDP, consultez [connecter tooa machine virtuelle Windows Server](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="ad22b-127">tooconnect toonodes running Windows via RDP, see [Connect tooa Windows Server VM](../virtual-machines/windows/connect-logon.md).</span></span><br /><br />
> <span data-ttu-id="ad22b-128">tooconnect tooa nœud en cours d’exécution hello configuration du service cloud via le protocole RDP, consultez [activer de connexion Bureau à distance pour un rôle dans Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ad22b-128">tooconnect tooa node running hello cloud service configuration via RDP, see [Enable Remote Desktop Connection for a Role in Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span></span>
>
>

## <a name="user-account-access-toofiles-and-directories"></a><span data-ttu-id="ad22b-129">Répertoires et toofiles de l’accès de compte utilisateur</span><span class="sxs-lookup"><span data-stu-id="ad22b-129">User account access toofiles and directories</span></span>

<span data-ttu-id="ad22b-130">Un compte d’utilisateur d’automatique et un compte d’utilisateur nommé ont le répertoire de travail en lecture/écriture toohello la tâche d’accès répertoire partagé et active des tâches à instances multiples.</span><span class="sxs-lookup"><span data-stu-id="ad22b-130">Both an auto-user account and a named user account have read/write access toohello task’s working directory, shared directory, and multi-instance tasks directory.</span></span> <span data-ttu-id="ad22b-131">Les deux types de comptes d’ont des accès en lecture toohello démarrage et la tâche de préparation répertoires.</span><span class="sxs-lookup"><span data-stu-id="ad22b-131">Both types of accounts have read access toohello startup and job preparation directories.</span></span>

<span data-ttu-id="ad22b-132">Si une tâche s’exécute sous hello même compte qui a été utilisé pour l’exécution d’une tâche de démarrage, la tâche hello a répertoire de tâche de démarrage de toohello accès en lecture-écriture.</span><span class="sxs-lookup"><span data-stu-id="ad22b-132">If a task runs under hello same account that was used for running a start task, hello task has read-write access toohello start task directory.</span></span> <span data-ttu-id="ad22b-133">De même, si une tâche s’exécute sous hello même compte qui a été utilisé pour l’exécution d’une tâche de préparation, la tâche hello a répertoire de tâche de l’accès en lecture / écriture toohello tâche préparation.</span><span class="sxs-lookup"><span data-stu-id="ad22b-133">Similarly, if a task runs under hello same account that was used for running a job preparation task, hello task has read-write access toohello job preparation task directory.</span></span> <span data-ttu-id="ad22b-134">Si une tâche s’exécute sous un compte différent de la tâche de démarrage hello ou de la tâche de préparation, tâche hello a uniquement un accès en lecture toohello répertoire correspondant.</span><span class="sxs-lookup"><span data-stu-id="ad22b-134">If a task runs under a different account than hello start task or job preparation task, then hello task has only read access toohello respective directory.</span></span>

<span data-ttu-id="ad22b-135">Pour plus d’informations sur l’accès aux fichiers et répertoires à partir d’une tâche, consultez [Développer des solutions de calcul parallèles à grande échelle avec Batch](batch-api-basics.md#files-and-directories).</span><span class="sxs-lookup"><span data-stu-id="ad22b-135">For more information on accessing files and directories from a task, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#files-and-directories).</span></span>

## <a name="elevated-access-for-tasks"></a><span data-ttu-id="ad22b-136">Accès aux tâches avec élévation de privilèges</span><span class="sxs-lookup"><span data-stu-id="ad22b-136">Elevated access for tasks</span></span> 

<span data-ttu-id="ad22b-137">niveau d’élévation du compte d’utilisateur Hello indique si une tâche s’exécute avec un accès avec élévation de privilèges.</span><span class="sxs-lookup"><span data-stu-id="ad22b-137">hello user account's elevation level indicates whether a task runs with elevated access.</span></span> <span data-ttu-id="ad22b-138">Les comptes d’utilisateur automatique et nommé peuvent s’exécuter dans le cadre d’un accès avec élévation de privilèges.</span><span class="sxs-lookup"><span data-stu-id="ad22b-138">Both an auto-user account and a named user account can run with elevated access.</span></span> <span data-ttu-id="ad22b-139">Hello deux options pour le niveau d’élévation sont :</span><span class="sxs-lookup"><span data-stu-id="ad22b-139">hello two options for elevation level are:</span></span>

- <span data-ttu-id="ad22b-140">**NonAdmin :** tâche hello s’exécute en tant qu’utilisateur standard sans accès avec élévation de privilèges.</span><span class="sxs-lookup"><span data-stu-id="ad22b-140">**NonAdmin:** hello task runs as a standard user without elevated access.</span></span> <span data-ttu-id="ad22b-141">niveau d’élévation Hello par défaut pour un compte d’utilisateur de lot est toujours **NonAdmin**.</span><span class="sxs-lookup"><span data-stu-id="ad22b-141">hello default elevation level for a Batch user account is always **NonAdmin**.</span></span>
- <span data-ttu-id="ad22b-142">**Administrateur :** tâche hello s’exécute en tant qu’utilisateur avec un accès avec élévation de privilèges et qu’il fonctionne avec des autorisations d’administrateur complètes.</span><span class="sxs-lookup"><span data-stu-id="ad22b-142">**Admin:** hello task runs as a user with elevated access and operates with full Administrator permissions.</span></span> 

## <a name="auto-user-accounts"></a><span data-ttu-id="ad22b-143">Comptes d’utilisateur automatique</span><span class="sxs-lookup"><span data-stu-id="ad22b-143">Auto-user accounts</span></span>

<span data-ttu-id="ad22b-144">Par défaut, les tâches s’exécutent dans Batch sous un compte d’utilisateur automatique, en tant qu’utilisateur standard qui ne dispose pas d’un accès avec élévation de privilèges, et avec une étendue de tâche bien définie.</span><span class="sxs-lookup"><span data-stu-id="ad22b-144">By default, tasks run in Batch under an auto-user account, as a standard user without elevated access, and with task scope.</span></span> <span data-ttu-id="ad22b-145">Lors de la spécification d’auto-utilisateur hello est configurée pour l’étendue de la tâche, service de traitement par lots hello crée un compte d’utilisateur automatiquement pour cette tâche uniquement.</span><span class="sxs-lookup"><span data-stu-id="ad22b-145">When hello auto-user specification is configured for task scope, hello Batch service creates an auto-user account for that task only.</span></span>

<span data-ttu-id="ad22b-146">étendue de remplacement tootask Hello est étendue du pool.</span><span class="sxs-lookup"><span data-stu-id="ad22b-146">hello alternative tootask scope is pool scope.</span></span> <span data-ttu-id="ad22b-147">Lors de la spécification d’auto-utilisateur hello pour une tâche est configurée pour l’étendue du pool, la tâche hello s’exécute sous un compte d’utilisateur automatique qui est la tâche tooany disponibles dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="ad22b-147">When hello auto-user specification for a task is configured for pool scope, hello task runs under an auto-user account that is available tooany task in hello pool.</span></span> <span data-ttu-id="ad22b-148">Pour plus d’informations sur l’étendue du pool, consultez la section hello intitulée [exécuter une tâche comme hello auto-utilisateur avec une étendue pool](#run-a-task-as-the-autouser-with-pool-scope).</span><span class="sxs-lookup"><span data-stu-id="ad22b-148">For more information about pool scope, see hello section titled [Run a task as hello auto-user with pool scope](#run-a-task-as-the-autouser-with-pool-scope).</span></span>   

<span data-ttu-id="ad22b-149">étendue par défaut de Hello est différent sur les nœuds Windows et Linux :</span><span class="sxs-lookup"><span data-stu-id="ad22b-149">hello default scope is different on Windows and Linux nodes:</span></span>

- <span data-ttu-id="ad22b-150">Sur les nœuds Windows, les tâches s’exécutent sous l’étendue de la tâche par défaut.</span><span class="sxs-lookup"><span data-stu-id="ad22b-150">On Windows nodes, tasks run under task scope by default.</span></span>
- <span data-ttu-id="ad22b-151">Les nœuds Linux s’exécutent toujours sous l’étendue du pool.</span><span class="sxs-lookup"><span data-stu-id="ad22b-151">Linux nodes always run under pool scope.</span></span>

<span data-ttu-id="ad22b-152">Il existe quatre configurations possibles pour la spécification d’auto-utilisateur hello, chacune d’elles correspondant de compte d’utilisateur unique automatique tooa :</span><span class="sxs-lookup"><span data-stu-id="ad22b-152">There are four possible configurations for hello auto-user specification, each of which corresponds tooa unique auto-user account:</span></span>

- <span data-ttu-id="ad22b-153">Accès non-admin avec une étendue de tâche (spécification d’auto-utilisateur par défaut de hello)</span><span class="sxs-lookup"><span data-stu-id="ad22b-153">Non-admin access with task scope (hello default auto-user specification)</span></span>
- <span data-ttu-id="ad22b-154">Accès admin (avec élévation de privilèges) avec étendue de la tâche</span><span class="sxs-lookup"><span data-stu-id="ad22b-154">Admin (elevated) access with task scope</span></span>
- <span data-ttu-id="ad22b-155">Accès non-admin avec étendue de pool</span><span class="sxs-lookup"><span data-stu-id="ad22b-155">Non-admin access with pool scope</span></span>
- <span data-ttu-id="ad22b-156">Accès admin avec étendue de pool</span><span class="sxs-lookup"><span data-stu-id="ad22b-156">Admin access with pool scope</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="ad22b-157">Tâches en cours d’exécution sous l’étendue de la tâche ne disposent pas de tâches de tooother accès de fait sur un nœud.</span><span class="sxs-lookup"><span data-stu-id="ad22b-157">Tasks running under task scope do not have de facto access tooother tasks on a node.</span></span> <span data-ttu-id="ad22b-158">Toutefois, un utilisateur malveillant avec le compte d’accès toohello pourrait contourner cette restriction en soumettant une tâche qui s’exécute avec des privilèges d’administrateur et accède à d’autres répertoires de la tâche.</span><span class="sxs-lookup"><span data-stu-id="ad22b-158">However, a malicious user with access toohello account could work around this restriction by submitting a task that runs with administrator privileges and accesses other task directories.</span></span> <span data-ttu-id="ad22b-159">Un utilisateur malveillant pourrait utiliser également de nœud de tooa tooconnect RDP ou SSH.</span><span class="sxs-lookup"><span data-stu-id="ad22b-159">A malicious user could also use RDP or SSH tooconnect tooa node.</span></span> <span data-ttu-id="ad22b-160">Il est important tooprotect accès tooyour lot compte clés tooprevent un tel scénario.</span><span class="sxs-lookup"><span data-stu-id="ad22b-160">It's important tooprotect access tooyour Batch account keys tooprevent such a scenario.</span></span> <span data-ttu-id="ad22b-161">Si vous pensez que votre compte a peut-être été compromis, être tooregenerate que vos clés.</span><span class="sxs-lookup"><span data-stu-id="ad22b-161">If you suspect your account may have been compromised, be sure tooregenerate your keys.</span></span>
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a><span data-ttu-id="ad22b-162">Exécution d’une tâche en tant qu’utilisateur automatique disposant d’un accès avec élévation de privilèges</span><span class="sxs-lookup"><span data-stu-id="ad22b-162">Run a task as an auto-user with elevated access</span></span>

<span data-ttu-id="ad22b-163">Vous pouvez configurer la spécification d’auto-utilisateur hello des privilèges d’administrateur lorsque vous devez toorun une tâche avec un accès avec élévation de privilèges.</span><span class="sxs-lookup"><span data-stu-id="ad22b-163">You can configure hello auto-user specification for administrator privileges when you need toorun a task with elevated access.</span></span> <span data-ttu-id="ad22b-164">Par exemple, une tâche de démarrage peut-être besoin d’un logiciel tooinstall accès avec élévation de privilèges sur le nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="ad22b-164">For example, a start task may need elevated access tooinstall software on hello node.</span></span>

> [!NOTE] 
> <span data-ttu-id="ad22b-165">En règle générale, il est préférable toouse élevé accès uniquement lorsque cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ad22b-165">In general, it's best toouse elevated access only when necessary.</span></span> <span data-ttu-id="ad22b-166">Les meilleures pratiques recommandent l’octroi du résultat souhaité de hello avec privilèges minimums nécessaires tooachieve hello.</span><span class="sxs-lookup"><span data-stu-id="ad22b-166">Best practices recommend granting hello minimum privilege necessary tooachieve hello desired outcome.</span></span> <span data-ttu-id="ad22b-167">Par exemple, si une tâche de démarrage installe le logiciel pour l’utilisateur actuel de hello, au lieu de pour tous les utilisateurs, vous pouvez être tooavoid en mesure de l’octroi d’accès avec élévation de privilèges tootasks.</span><span class="sxs-lookup"><span data-stu-id="ad22b-167">For example, if a start task installs software for hello current user, instead of for all users, you may be able tooavoid granting elevated access tootasks.</span></span> <span data-ttu-id="ad22b-168">Vous pouvez configurer la spécification d’auto-utilisateur hello pour l’accès de portée et non-admin pool pour toutes les tâches qui doivent toorun sous le même compte, y compris les tâches de démarrage hello de hello.</span><span class="sxs-lookup"><span data-stu-id="ad22b-168">You can configure hello auto-user specification for pool scope and non-admin access for all tasks that need toorun under hello same account, including hello start task.</span></span> 
>
>

<span data-ttu-id="ad22b-169">Hello suivant des extraits de code montrent comment tooconfigure hello spécification auto-utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ad22b-169">hello following code snippets show how tooconfigure hello auto-user specification.</span></span> <span data-ttu-id="ad22b-170">les exemples Hello définissent au niveau de l’élévation hello trop`Admin` et hello étendue trop`Task`.</span><span class="sxs-lookup"><span data-stu-id="ad22b-170">hello examples set hello elevation level too`Admin` and hello scope too`Task`.</span></span> <span data-ttu-id="ad22b-171">Étendue de la tâche est le paramètre par défaut de hello, mais il est inclus ici par souci de hello d’exemple.</span><span class="sxs-lookup"><span data-stu-id="ad22b-171">Task scope is hello default setting, but is included here for hello sake of example.</span></span>

#### <a name="batch-net"></a><span data-ttu-id="ad22b-172">.NET Batch</span><span class="sxs-lookup"><span data-stu-id="ad22b-172">Batch .NET</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a><span data-ttu-id="ad22b-173">Java Batch</span><span class="sxs-lookup"><span data-stu-id="ad22b-173">Batch Java</span></span>

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a><span data-ttu-id="ad22b-174">Python Batch</span><span class="sxs-lookup"><span data-stu-id="ad22b-174">Batch Python</span></span>

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

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a><span data-ttu-id="ad22b-175">Exécution d’une tâche en tant qu’utilisateur automatique avec une étendue de pool</span><span class="sxs-lookup"><span data-stu-id="ad22b-175">Run a task as an auto-user with pool scope</span></span>

<span data-ttu-id="ad22b-176">Lorsqu’un nœud est configuré, les deux à l’échelle du pool automatique-comptes d’utilisateur est créés sur chaque nœud dans le pool de hello, avec accès avec élévation de privilèges et l’autre sans accès avec élévation de privilèges.</span><span class="sxs-lookup"><span data-stu-id="ad22b-176">When a node is provisioned, two pool-wide auto-user accounts are created on each node in hello pool, one with elevated access, and one without elevated access.</span></span> <span data-ttu-id="ad22b-177">La définition étendue de toopool étendue hello automatiquement l’utilisateur pour une tâche donnée, tâche hello sous un de ces deux pool à l’échelle automatique-comptes d’utilisateur s’exécute.</span><span class="sxs-lookup"><span data-stu-id="ad22b-177">Setting hello auto-user's scope toopool scope for a given task runs hello task under one of these two pool-wide auto-user accounts.</span></span> 

<span data-ttu-id="ad22b-178">Lorsque vous spécifiez la portée de pool pour hello auto-utilisateur, toutes les tâches qui s’exécutent en tant qu’administrateur s’exécutent sous hello même compte d’utilisateur à l’échelle du pool automatique.</span><span class="sxs-lookup"><span data-stu-id="ad22b-178">When you specify pool scope for hello auto-user, all tasks that run with administrator access run under hello same pool-wide auto-user account.</span></span> <span data-ttu-id="ad22b-179">De même, les tâches qui s’exécutent sans autorisations d’administrateur s’exécutent également sous un seul compte d’utilisateur automatique au niveau du pool.</span><span class="sxs-lookup"><span data-stu-id="ad22b-179">Similarly, tasks that run without administrator permissions also run under a single pool-wide auto-user account.</span></span> 

> [!NOTE] 
> <span data-ttu-id="ad22b-180">Hello deux pool à l’échelle automatique-comptes d’utilisateur sont des comptes distincts.</span><span class="sxs-lookup"><span data-stu-id="ad22b-180">hello two pool-wide auto-user accounts are separate accounts.</span></span> <span data-ttu-id="ad22b-181">Tâches en cours d’exécution sous un compte d’administrateur de l’ensemble du pool hello ne peuvent pas partager des données avec les tâches en cours d’exécution sous un compte d’utilisateur standard hello et vice versa.</span><span class="sxs-lookup"><span data-stu-id="ad22b-181">Tasks running under hello pool-wide administrative account cannot share data with tasks running under hello standard account, and vice versa.</span></span> 
>
>

<span data-ttu-id="ad22b-182">Hello toorunning parti sous le même compte d’utilisateur d’automatique est que les tâches sont en mesure de tooshare des données avec d’autres tâches en cours d’exécution sur hello de hello même nœud.</span><span class="sxs-lookup"><span data-stu-id="ad22b-182">hello advantage toorunning under hello same auto-user account is that tasks are able tooshare data with other tasks running on hello same node.</span></span>

<span data-ttu-id="ad22b-183">Partage des secrets entre les tâches est un scénario dans lequel il est utile de tâches sous un des comptes d’utilisateur à l’échelle du pool automatique hello deux en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="ad22b-183">Sharing secrets between tasks is one scenario where running tasks under one of hello two pool-wide auto-user accounts is useful.</span></span> <span data-ttu-id="ad22b-184">Par exemple, qu'une tâche de démarrage doit tooprovision un secret sur le nœud de hello autres tâches peuvent utiliser.</span><span class="sxs-lookup"><span data-stu-id="ad22b-184">For example, suppose a start task needs tooprovision a secret onto hello node that other tasks can use.</span></span> <span data-ttu-id="ad22b-185">Vous pouvez utiliser hello API de Protection des données (DPAPI) Windows, mais elle nécessite des privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ad22b-185">You could use hello Windows Data Protection API (DPAPI), but it requires administrator privileges.</span></span> <span data-ttu-id="ad22b-186">Au lieu de cela, vous pouvez protéger secret hello au niveau de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="ad22b-186">Instead, you can protect hello secret at hello user level.</span></span> <span data-ttu-id="ad22b-187">Tâches en cours d’exécution sous hello même compte d’utilisateur peut accéder hello secret sans accès avec élévation de privilèges.</span><span class="sxs-lookup"><span data-stu-id="ad22b-187">Tasks running under hello same user account can access hello secret without elevated access.</span></span>

<span data-ttu-id="ad22b-188">Partage d’un autre scénario que vous deviez tâches toorun sous un compte d’utilisateur automatique avec la portée du pool est un fichier de l’Interface MPI (Message Passing).</span><span class="sxs-lookup"><span data-stu-id="ad22b-188">Another scenario where you may want toorun tasks under an auto-user account with pool scope is a Message Passing Interface (MPI) file share.</span></span> <span data-ttu-id="ad22b-189">Un partage de fichiers MPI est utile lorsque les nœuds hello hello MPI tâche besoin toowork sur hello des mêmes données de fichier.</span><span class="sxs-lookup"><span data-stu-id="ad22b-189">An MPI file share is useful when hello nodes in hello MPI task need toowork on hello same file data.</span></span> <span data-ttu-id="ad22b-190">nœud principal Hello crée un partage de fichiers accessibles à des nœuds enfants hello si elles sont exécutent sous hello même compte d’utilisateur automatiquement.</span><span class="sxs-lookup"><span data-stu-id="ad22b-190">hello head node creates a file share that hello child nodes can access if they are running under hello same auto-user account.</span></span> 

<span data-ttu-id="ad22b-191">Hello suivant extrait de code définit l’étendue de toopool de portée de hello automatiquement l’utilisateur pour une tâche dans le lot .NET.</span><span class="sxs-lookup"><span data-stu-id="ad22b-191">hello following code snippet sets hello auto-user's scope toopool scope for a task in Batch .NET.</span></span> <span data-ttu-id="ad22b-192">niveau d’élévation Hello est omis, afin de la tâche hello s’exécute sous le compte de pool à l’échelle automatique-utilisateur standard hello.</span><span class="sxs-lookup"><span data-stu-id="ad22b-192">hello elevation level is omitted, so hello task runs under hello standard pool-wide auto-user account.</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a><span data-ttu-id="ad22b-193">Comptes d’utilisateur nommé</span><span class="sxs-lookup"><span data-stu-id="ad22b-193">Named user accounts</span></span>

<span data-ttu-id="ad22b-194">Vous pouvez définir des comptes d’utilisateur nommé lorsque vous créez un pool.</span><span class="sxs-lookup"><span data-stu-id="ad22b-194">You can define named user accounts when you create a pool.</span></span> <span data-ttu-id="ad22b-195">Un compte d’utilisateur nommé possède un nom et un mot de passe que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="ad22b-195">A named user account has a name and password that you provide.</span></span> <span data-ttu-id="ad22b-196">Vous pouvez spécifier le niveau d’élévation hello pour un compte d’utilisateur nommé.</span><span class="sxs-lookup"><span data-stu-id="ad22b-196">You can specify hello elevation level for a named user account.</span></span> <span data-ttu-id="ad22b-197">Pour les nœuds Linux, vous pouvez également fournir une clé privée SSH.</span><span class="sxs-lookup"><span data-stu-id="ad22b-197">For Linux nodes, you can also provide an SSH private key.</span></span>

<span data-ttu-id="ad22b-198">Un compte d’utilisateur nommé existe sur tous les nœuds dans le pool de hello et sont disponible tooall tâches en cours d’exécution sur ces nœuds.</span><span class="sxs-lookup"><span data-stu-id="ad22b-198">A named user account exists on all nodes in hello pool and is available tooall tasks running on those nodes.</span></span> <span data-ttu-id="ad22b-199">Vous pouvez définir n’importe quel nombre d’utilisateurs nommés pour un pool.</span><span class="sxs-lookup"><span data-stu-id="ad22b-199">You may define any number of named users for a pool.</span></span> <span data-ttu-id="ad22b-200">Lorsque vous ajoutez une tâche ou une collection de tâches, vous pouvez spécifier que cette tâche hello s’exécute sous un des hello nommé de comptes d’utilisateur définis sur le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="ad22b-200">When you add a task or task collection, you can specify that hello task runs under one of hello named user accounts defined on hello pool.</span></span>

<span data-ttu-id="ad22b-201">Un compte d’utilisateur nommé est utile lorsque vous souhaitez toorun toutes les tâches dans un projet sous hello du même compte d’utilisateur, mais les isoler les tâches qui s’exécutent dans d’autres tâches à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="ad22b-201">A named user account is useful when you want toorun all tasks in a job under hello same user account, but isolate them from tasks running in other jobs at hello same time.</span></span> <span data-ttu-id="ad22b-202">Par exemple, vous pouvez créer un utilisateur nommé pour chaque travail, et exécuter les tâches de chaque travail sous ce compte d’utilisateur nommé.</span><span class="sxs-lookup"><span data-stu-id="ad22b-202">For example, you can create a named user for each job, and run each job's tasks under that named user account.</span></span> <span data-ttu-id="ad22b-203">Chaque travail peut ensuite partager une clé secrète avec ses propres tâches, mais pas avec les tâches qui s’exécutent dans d’autres travaux.</span><span class="sxs-lookup"><span data-stu-id="ad22b-203">Each job can then share a secret with its own tasks, but not with tasks running in other jobs.</span></span>

<span data-ttu-id="ad22b-204">Vous pouvez également utiliser un toorun de compte d’utilisateur nommé une tâche qui définit des autorisations sur les ressources externes telles que des partages de fichiers.</span><span class="sxs-lookup"><span data-stu-id="ad22b-204">You can also use a named user account toorun a task that sets permissions on external resources such as file shares.</span></span> <span data-ttu-id="ad22b-205">Avec un compte d’utilisateur nommé, vous contrôler l’identité de l’utilisateur hello et utilisez cette identité tooset des autorisations.</span><span class="sxs-lookup"><span data-stu-id="ad22b-205">With a named user account, you control hello user identity and can use that user identity tooset permissions.</span></span>  

<span data-ttu-id="ad22b-206">Les comptes d’utilisateur nommé activent le protocole SSH sans mot de passe entre les nœuds Linux.</span><span class="sxs-lookup"><span data-stu-id="ad22b-206">Named user accounts enable password-less SSH between Linux nodes.</span></span> <span data-ttu-id="ad22b-207">Vous pouvez utiliser un compte d’utilisateur nommé avec des nœuds Linux nécessitant des tâches toorun à instances multiples.</span><span class="sxs-lookup"><span data-stu-id="ad22b-207">You can use a named user account with Linux nodes that need toorun multi-instance tasks.</span></span> <span data-ttu-id="ad22b-208">Chaque nœud dans le pool de hello peut exécuter des tâches sous un compte d’utilisateur définis sur le pool entier de hello.</span><span class="sxs-lookup"><span data-stu-id="ad22b-208">Each node in hello pool can run tasks under a user account defined on hello whole pool.</span></span> <span data-ttu-id="ad22b-209">Pour plus d’informations sur les tâches d’instances multiples, consultez [utiliser multi\-instance tâches des applications MPI toorun](batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="ad22b-209">For more information about multi-instance tasks, see [Use multi\-instance tasks toorun MPI applications](batch-mpi.md).</span></span>

### <a name="create-named-user-accounts"></a><span data-ttu-id="ad22b-210">Créer des comptes d’utilisateur nommé</span><span class="sxs-lookup"><span data-stu-id="ad22b-210">Create named user accounts</span></span>

<span data-ttu-id="ad22b-211">toocreate nommé de comptes d’utilisateur dans un lot, ajouter une collection de pool toohello de comptes d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ad22b-211">toocreate named user accounts in Batch, add a collection of user accounts toohello pool.</span></span> <span data-ttu-id="ad22b-212">Hello extraits de code suivants montrent comment toocreate nommé comptes d’utilisateur dans .NET, Java et Python.</span><span class="sxs-lookup"><span data-stu-id="ad22b-212">hello following code snippets show how toocreate named user accounts in .NET, Java, and Python.</span></span> <span data-ttu-id="ad22b-213">Ces afficher des extraits de code comment toocreate admin et non nommée sur un pool de comptes d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ad22b-213">These code snippets show how toocreate both admin and non-admin named accounts on a pool.</span></span> <span data-ttu-id="ad22b-214">les exemples Hello créent des pools à l’aide de la configuration du service cloud hello, mais que vous utilisez hello même approche lors de la création d’un pool de Windows ou Linux à l’aide de la configuration d’ordinateur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="ad22b-214">hello examples create pools using hello cloud service configuration, but you use hello same approach when creating a Windows or Linux pool using hello virtual machine configuration.</span></span>

#### <a name="batch-net-example-windows"></a><span data-ttu-id="ad22b-215">Exemple .NET Batch (Windows)</span><span class="sxs-lookup"><span data-stu-id="ad22b-215">Batch .NET example (Windows)</span></span>

```csharp
CloudPool pool = null;
Console.WriteLine("Creating pool [{0}]...", poolId);

// Create a pool using hello cloud service configuration.
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

// Commit hello pool.
await pool.CommitAsync();
```

#### <a name="batch-net-example-linux"></a><span data-ttu-id="ad22b-216">Exemple .NET Batch (Linux)</span><span class="sxs-lookup"><span data-stu-id="ad22b-216">Batch .NET example (Linux)</span></span>

```csharp
CloudPool pool = null;

// Obtain a collection of all available node agent SKUs.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of hello VM image toouse.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain hello first node agent SKU in hello collection that matches
// Ubuntu Server 14.04. 
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create hello virtual machine configuration toouse toocreate hello pool.
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

Console.WriteLine("Creating pool [{0}]...", poolId);

// Create hello unbound pool.
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

// Commit hello pool.
await pool.CommitAsync();
```


#### <a name="batch-java-example"></a><span data-ttu-id="ad22b-217">Exemple Java Batch</span><span class="sxs-lookup"><span data-stu-id="ad22b-217">Batch Java example</span></span>

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

#### <a name="batch-python-example"></a><span data-ttu-id="ad22b-218">Exemple Python Batch</span><span class="sxs-lookup"><span data-stu-id="ad22b-218">Batch Python example</span></span>

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

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a><span data-ttu-id="ad22b-219">Exécution d’une tâche sous un compte d’utilisateur nommé disposant d’un accès avec élévation de privilèges</span><span class="sxs-lookup"><span data-stu-id="ad22b-219">Run a task under a named user account with elevated access</span></span>

<span data-ttu-id="ad22b-220">toorun une tâche en tant qu’avec élévation de privilèges, hello définies pour les tâches de **UserIdentity** tooa propriété nommé le compte d’utilisateur qui a été créée avec sa **ElevationLevel** propriété trop`Admin`.</span><span class="sxs-lookup"><span data-stu-id="ad22b-220">toorun a task as an elevated user, set hello task's **UserIdentity** property tooa named user account that was created with its **ElevationLevel** property set too`Admin`.</span></span>

<span data-ttu-id="ad22b-221">Cet extrait de code spécifie que cette tâche hello doit s’exécuter sous un compte d’utilisateur nommé.</span><span class="sxs-lookup"><span data-stu-id="ad22b-221">This code snippet specifies that hello task should run under a named user account.</span></span> <span data-ttu-id="ad22b-222">Ce compte d’utilisateur nommé a été défini sur le pool de hello lorsque hello pool a été créé.</span><span class="sxs-lookup"><span data-stu-id="ad22b-222">This named user account was defined on hello pool when hello pool was created.</span></span> <span data-ttu-id="ad22b-223">Dans ce cas, hello appelé compte d’utilisateur a été créé avec des autorisations d’administrateur :</span><span class="sxs-lookup"><span data-stu-id="ad22b-223">In this case, hello named user account was created with admin permissions:</span></span>

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-toohello-latest-batch-client-library"></a><span data-ttu-id="ad22b-224">Mettre à jour votre bibliothèque de client de lot dernier code toohello</span><span class="sxs-lookup"><span data-stu-id="ad22b-224">Update your code toohello latest Batch client library</span></span>

<span data-ttu-id="ad22b-225">version du service de traitement par lots Hello 2017-01-01.4.0 introduit une modification avec rupture, en remplaçant hello **runElevated** propriété disponible dans les versions antérieures avec hello **userIdentity** propriété.</span><span class="sxs-lookup"><span data-stu-id="ad22b-225">hello Batch service version 2017-01-01.4.0 introduces a breaking change, replacing hello **runElevated** property available in earlier versions with hello **userIdentity** property.</span></span> <span data-ttu-id="ad22b-226">Hello les tableaux suivants fournit un simple mappage que vous pouvez utiliser tooupdate votre code à partir de versions antérieures des bibliothèques clientes de hello.</span><span class="sxs-lookup"><span data-stu-id="ad22b-226">hello following tables provide a simple mapping that you can use tooupdate your code from earlier versions of hello client libraries.</span></span>

### <a name="batch-net"></a><span data-ttu-id="ad22b-227">.NET Batch</span><span class="sxs-lookup"><span data-stu-id="ad22b-227">Batch .NET</span></span>

| <span data-ttu-id="ad22b-228">Si votre code utilise...</span><span class="sxs-lookup"><span data-stu-id="ad22b-228">If your code uses...</span></span>                  | <span data-ttu-id="ad22b-229">Mettez-le à jour vers...</span><span class="sxs-lookup"><span data-stu-id="ad22b-229">Update it to....</span></span>                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| <span data-ttu-id="ad22b-230">`CloudTask.RunElevated` non spécifié</span><span class="sxs-lookup"><span data-stu-id="ad22b-230">`CloudTask.RunElevated` not specified</span></span> | <span data-ttu-id="ad22b-231">Aucune mise à jour requise</span><span class="sxs-lookup"><span data-stu-id="ad22b-231">No update required</span></span>                                                                                               |

### <a name="batch-java"></a><span data-ttu-id="ad22b-232">Java Batch</span><span class="sxs-lookup"><span data-stu-id="ad22b-232">Batch Java</span></span>

| <span data-ttu-id="ad22b-233">Si votre code utilise...</span><span class="sxs-lookup"><span data-stu-id="ad22b-233">If your code uses...</span></span>                      | <span data-ttu-id="ad22b-234">Mettez-le à jour vers...</span><span class="sxs-lookup"><span data-stu-id="ad22b-234">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| <span data-ttu-id="ad22b-235">`CloudTask.withRunElevated` non spécifié</span><span class="sxs-lookup"><span data-stu-id="ad22b-235">`CloudTask.withRunElevated` not specified</span></span> | <span data-ttu-id="ad22b-236">Aucune mise à jour requise</span><span class="sxs-lookup"><span data-stu-id="ad22b-236">No update required</span></span>                                                                                                                     |

### <a name="batch-python"></a><span data-ttu-id="ad22b-237">Python Batch</span><span class="sxs-lookup"><span data-stu-id="ad22b-237">Batch Python</span></span>

| <span data-ttu-id="ad22b-238">Si votre code utilise...</span><span class="sxs-lookup"><span data-stu-id="ad22b-238">If your code uses...</span></span>                      | <span data-ttu-id="ad22b-239">Mettez-le à jour vers...</span><span class="sxs-lookup"><span data-stu-id="ad22b-239">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | <span data-ttu-id="ad22b-240">`user_identity=user`, où</span><span class="sxs-lookup"><span data-stu-id="ad22b-240">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | <span data-ttu-id="ad22b-241">`user_identity=user`, où</span><span class="sxs-lookup"><span data-stu-id="ad22b-241">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| <span data-ttu-id="ad22b-242">`run_elevated` non spécifié</span><span class="sxs-lookup"><span data-stu-id="ad22b-242">`run_elevated` not specified</span></span> | <span data-ttu-id="ad22b-243">Aucune mise à jour requise</span><span class="sxs-lookup"><span data-stu-id="ad22b-243">No update required</span></span>                                                                                                                                  |


## <a name="next-steps"></a><span data-ttu-id="ad22b-244">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ad22b-244">Next steps</span></span>

### <a name="batch-forum"></a><span data-ttu-id="ad22b-245">Forum Azure Batch</span><span class="sxs-lookup"><span data-stu-id="ad22b-245">Batch Forum</span></span>

<span data-ttu-id="ad22b-246">Hello [Forum de traitement par lots Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) sur MSDN est une bonne placer toodiscuss lot et poser des questions sur le service de hello.</span><span class="sxs-lookup"><span data-stu-id="ad22b-246">hello [Azure Batch Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="ad22b-247">Consultez le forum pour obtenir des publications utiles et publiez les questions que vous vous posez pendant la création de vos solutions Batch.</span><span class="sxs-lookup"><span data-stu-id="ad22b-247">Head on over for helpful pinned posts, and post your questions as they arise while you build your Batch solutions.</span></span>
