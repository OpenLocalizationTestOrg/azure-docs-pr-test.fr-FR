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
# <a name="run-tasks-under-user-accounts-in-batch"></a>Exécuter des tâches sous des comptes d’utilisateur dans Azure Batch

Dans Azure Batch, une tâche s’exécute toujours sous un compte d’utilisateur. Par défaut, les tâches s’exécutent sous des comptes d’utilisateur standard qui ne possèdent pas de droits d’administrateur. Ces paramètres de compte d’utilisateur par défaut sont généralement suffisants. Toutefois, pour certains scénarios, il est utile toobe tooconfigure en mesure de hello compte d’utilisateur sous lequel un toorun de tâche. Cet article décrit les types de comptes d’utilisateur et comment vous pouvez les configurer pour votre scénario hello.

## <a name="types-of-user-accounts"></a>Types de comptes d’utilisateur

Azure Batch offre deux types comptes d’utilisateur pour l’exécution des tâches :

- **Comptes d’utilisateur automatique.** Comptes d’utilisateur d’automatique sont des comptes d’utilisateurs intégrés sont créés automatiquement par hello service Batch. Par défaut, les tâches sont exécutées sous un compte d’utilisateur automatique. Vous pouvez configurer la spécification d’auto-utilisateur hello pour un tooindicate tâche sous auto-utilisateur compte une tâche doit s’exécuter. spécification d’auto-utilisateur Hello vous permet de niveau d’élévation toospecify hello et étendue hello auto-du compte d’utilisateur qui exécutera la tâche hello. 

- **Un compte d’utilisateur nommé.** Vous pouvez spécifier un ou plusieurs comptes d’utilisateur nommé pour un pool lorsque vous créez le pool de hello. Chaque compte d’utilisateur est créé sur chaque nœud du pool de hello. En outre toohello nom du compte, vous spécifiez hello mot de passe utilisateur, élévation, ainsi que, pour les pools de Linux, la clé privée SSH hello. Lorsque vous ajoutez une tâche, vous pouvez spécifier hello appelé compte d’utilisateur sous lequel cette tâche doit s’exécuter.

> [!IMPORTANT] 
> version du service de traitement par lots Hello 2017-01-01.4.0 introduit une modification avec rupture qui requiert que vous mettez à jour votre code toocall cette version. Si vous êtes la migration du code à partir d’une version antérieure du lot, notez que hello **runElevated** propriété n’est plus pris en charge dans des bibliothèques du client hello API REST ou le lot. Hello utilisez nouveau **userIdentity** propriété d’un niveau de l’élévation toospecify tâche. Consultez la section hello intitulée [mettre à jour votre bibliothèque de client de lot dernier code toohello](#update-your-code-to-the-latest-batch-client-library) pour connaître les instructions de mise à jour de votre code de lot si vous utilisez une des bibliothèques de client hello rapides.
>
>

> [!NOTE] 
> comptes d’utilisateur Hello abordés dans cet article ne prennent pas en charge protocole RDP (Remote Desktop) ou Secure Shell (SSH), pour des raisons de sécurité. 
>
> tooconnect tooa nœud en cours d’exécution hello Linux configuration d’ordinateur virtuel via SSH, consultez [tooa de bureau à distance d’utilisation VM Linux dans Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md). toonodes tooconnect Windows en cours d’exécution via le protocole RDP, consultez [connecter tooa machine virtuelle Windows Server](../virtual-machines/windows/connect-logon.md).<br /><br />
> tooconnect tooa nœud en cours d’exécution hello configuration du service cloud via le protocole RDP, consultez [activer de connexion Bureau à distance pour un rôle dans Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).
>
>

## <a name="user-account-access-toofiles-and-directories"></a>Répertoires et toofiles de l’accès de compte utilisateur

Un compte d’utilisateur d’automatique et un compte d’utilisateur nommé ont le répertoire de travail en lecture/écriture toohello la tâche d’accès répertoire partagé et active des tâches à instances multiples. Les deux types de comptes d’ont des accès en lecture toohello démarrage et la tâche de préparation répertoires.

Si une tâche s’exécute sous hello même compte qui a été utilisé pour l’exécution d’une tâche de démarrage, la tâche hello a répertoire de tâche de démarrage de toohello accès en lecture-écriture. De même, si une tâche s’exécute sous hello même compte qui a été utilisé pour l’exécution d’une tâche de préparation, la tâche hello a répertoire de tâche de l’accès en lecture / écriture toohello tâche préparation. Si une tâche s’exécute sous un compte différent de la tâche de démarrage hello ou de la tâche de préparation, tâche hello a uniquement un accès en lecture toohello répertoire correspondant.

Pour plus d’informations sur l’accès aux fichiers et répertoires à partir d’une tâche, consultez [Développer des solutions de calcul parallèles à grande échelle avec Batch](batch-api-basics.md#files-and-directories).

## <a name="elevated-access-for-tasks"></a>Accès aux tâches avec élévation de privilèges 

niveau d’élévation du compte d’utilisateur Hello indique si une tâche s’exécute avec un accès avec élévation de privilèges. Les comptes d’utilisateur automatique et nommé peuvent s’exécuter dans le cadre d’un accès avec élévation de privilèges. Hello deux options pour le niveau d’élévation sont :

- **NonAdmin :** tâche hello s’exécute en tant qu’utilisateur standard sans accès avec élévation de privilèges. niveau d’élévation Hello par défaut pour un compte d’utilisateur de lot est toujours **NonAdmin**.
- **Administrateur :** tâche hello s’exécute en tant qu’utilisateur avec un accès avec élévation de privilèges et qu’il fonctionne avec des autorisations d’administrateur complètes. 

## <a name="auto-user-accounts"></a>Comptes d’utilisateur automatique

Par défaut, les tâches s’exécutent dans Batch sous un compte d’utilisateur automatique, en tant qu’utilisateur standard qui ne dispose pas d’un accès avec élévation de privilèges, et avec une étendue de tâche bien définie. Lors de la spécification d’auto-utilisateur hello est configurée pour l’étendue de la tâche, service de traitement par lots hello crée un compte d’utilisateur automatiquement pour cette tâche uniquement.

étendue de remplacement tootask Hello est étendue du pool. Lors de la spécification d’auto-utilisateur hello pour une tâche est configurée pour l’étendue du pool, la tâche hello s’exécute sous un compte d’utilisateur automatique qui est la tâche tooany disponibles dans le pool de hello. Pour plus d’informations sur l’étendue du pool, consultez la section hello intitulée [exécuter une tâche comme hello auto-utilisateur avec une étendue pool](#run-a-task-as-the-autouser-with-pool-scope).   

étendue par défaut de Hello est différent sur les nœuds Windows et Linux :

- Sur les nœuds Windows, les tâches s’exécutent sous l’étendue de la tâche par défaut.
- Les nœuds Linux s’exécutent toujours sous l’étendue du pool.

Il existe quatre configurations possibles pour la spécification d’auto-utilisateur hello, chacune d’elles correspondant de compte d’utilisateur unique automatique tooa :

- Accès non-admin avec une étendue de tâche (spécification d’auto-utilisateur par défaut de hello)
- Accès admin (avec élévation de privilèges) avec étendue de la tâche
- Accès non-admin avec étendue de pool
- Accès admin avec étendue de pool

> [!IMPORTANT] 
> Tâches en cours d’exécution sous l’étendue de la tâche ne disposent pas de tâches de tooother accès de fait sur un nœud. Toutefois, un utilisateur malveillant avec le compte d’accès toohello pourrait contourner cette restriction en soumettant une tâche qui s’exécute avec des privilèges d’administrateur et accède à d’autres répertoires de la tâche. Un utilisateur malveillant pourrait utiliser également de nœud de tooa tooconnect RDP ou SSH. Il est important tooprotect accès tooyour lot compte clés tooprevent un tel scénario. Si vous pensez que votre compte a peut-être été compromis, être tooregenerate que vos clés.
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a>Exécution d’une tâche en tant qu’utilisateur automatique disposant d’un accès avec élévation de privilèges

Vous pouvez configurer la spécification d’auto-utilisateur hello des privilèges d’administrateur lorsque vous devez toorun une tâche avec un accès avec élévation de privilèges. Par exemple, une tâche de démarrage peut-être besoin d’un logiciel tooinstall accès avec élévation de privilèges sur le nœud de hello.

> [!NOTE] 
> En règle générale, il est préférable toouse élevé accès uniquement lorsque cela est nécessaire. Les meilleures pratiques recommandent l’octroi du résultat souhaité de hello avec privilèges minimums nécessaires tooachieve hello. Par exemple, si une tâche de démarrage installe le logiciel pour l’utilisateur actuel de hello, au lieu de pour tous les utilisateurs, vous pouvez être tooavoid en mesure de l’octroi d’accès avec élévation de privilèges tootasks. Vous pouvez configurer la spécification d’auto-utilisateur hello pour l’accès de portée et non-admin pool pour toutes les tâches qui doivent toorun sous le même compte, y compris les tâches de démarrage hello de hello. 
>
>

Hello suivant des extraits de code montrent comment tooconfigure hello spécification auto-utilisateur. les exemples Hello définissent au niveau de l’élévation hello trop`Admin` et hello étendue trop`Task`. Étendue de la tâche est le paramètre par défaut de hello, mais il est inclus ici par souci de hello d’exemple.

#### <a name="batch-net"></a>.NET Batch

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a>Java Batch

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a>Python Batch

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

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a>Exécution d’une tâche en tant qu’utilisateur automatique avec une étendue de pool

Lorsqu’un nœud est configuré, les deux à l’échelle du pool automatique-comptes d’utilisateur est créés sur chaque nœud dans le pool de hello, avec accès avec élévation de privilèges et l’autre sans accès avec élévation de privilèges. La définition étendue de toopool étendue hello automatiquement l’utilisateur pour une tâche donnée, tâche hello sous un de ces deux pool à l’échelle automatique-comptes d’utilisateur s’exécute. 

Lorsque vous spécifiez la portée de pool pour hello auto-utilisateur, toutes les tâches qui s’exécutent en tant qu’administrateur s’exécutent sous hello même compte d’utilisateur à l’échelle du pool automatique. De même, les tâches qui s’exécutent sans autorisations d’administrateur s’exécutent également sous un seul compte d’utilisateur automatique au niveau du pool. 

> [!NOTE] 
> Hello deux pool à l’échelle automatique-comptes d’utilisateur sont des comptes distincts. Tâches en cours d’exécution sous un compte d’administrateur de l’ensemble du pool hello ne peuvent pas partager des données avec les tâches en cours d’exécution sous un compte d’utilisateur standard hello et vice versa. 
>
>

Hello toorunning parti sous le même compte d’utilisateur d’automatique est que les tâches sont en mesure de tooshare des données avec d’autres tâches en cours d’exécution sur hello de hello même nœud.

Partage des secrets entre les tâches est un scénario dans lequel il est utile de tâches sous un des comptes d’utilisateur à l’échelle du pool automatique hello deux en cours d’exécution. Par exemple, qu'une tâche de démarrage doit tooprovision un secret sur le nœud de hello autres tâches peuvent utiliser. Vous pouvez utiliser hello API de Protection des données (DPAPI) Windows, mais elle nécessite des privilèges d’administrateur. Au lieu de cela, vous pouvez protéger secret hello au niveau de l’utilisateur hello. Tâches en cours d’exécution sous hello même compte d’utilisateur peut accéder hello secret sans accès avec élévation de privilèges.

Partage d’un autre scénario que vous deviez tâches toorun sous un compte d’utilisateur automatique avec la portée du pool est un fichier de l’Interface MPI (Message Passing). Un partage de fichiers MPI est utile lorsque les nœuds hello hello MPI tâche besoin toowork sur hello des mêmes données de fichier. nœud principal Hello crée un partage de fichiers accessibles à des nœuds enfants hello si elles sont exécutent sous hello même compte d’utilisateur automatiquement. 

Hello suivant extrait de code définit l’étendue de toopool de portée de hello automatiquement l’utilisateur pour une tâche dans le lot .NET. niveau d’élévation Hello est omis, afin de la tâche hello s’exécute sous le compte de pool à l’échelle automatique-utilisateur standard hello.

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a>Comptes d’utilisateur nommé

Vous pouvez définir des comptes d’utilisateur nommé lorsque vous créez un pool. Un compte d’utilisateur nommé possède un nom et un mot de passe que vous spécifiez. Vous pouvez spécifier le niveau d’élévation hello pour un compte d’utilisateur nommé. Pour les nœuds Linux, vous pouvez également fournir une clé privée SSH.

Un compte d’utilisateur nommé existe sur tous les nœuds dans le pool de hello et sont disponible tooall tâches en cours d’exécution sur ces nœuds. Vous pouvez définir n’importe quel nombre d’utilisateurs nommés pour un pool. Lorsque vous ajoutez une tâche ou une collection de tâches, vous pouvez spécifier que cette tâche hello s’exécute sous un des hello nommé de comptes d’utilisateur définis sur le pool de hello.

Un compte d’utilisateur nommé est utile lorsque vous souhaitez toorun toutes les tâches dans un projet sous hello du même compte d’utilisateur, mais les isoler les tâches qui s’exécutent dans d’autres tâches à hello même temps. Par exemple, vous pouvez créer un utilisateur nommé pour chaque travail, et exécuter les tâches de chaque travail sous ce compte d’utilisateur nommé. Chaque travail peut ensuite partager une clé secrète avec ses propres tâches, mais pas avec les tâches qui s’exécutent dans d’autres travaux.

Vous pouvez également utiliser un toorun de compte d’utilisateur nommé une tâche qui définit des autorisations sur les ressources externes telles que des partages de fichiers. Avec un compte d’utilisateur nommé, vous contrôler l’identité de l’utilisateur hello et utilisez cette identité tooset des autorisations.  

Les comptes d’utilisateur nommé activent le protocole SSH sans mot de passe entre les nœuds Linux. Vous pouvez utiliser un compte d’utilisateur nommé avec des nœuds Linux nécessitant des tâches toorun à instances multiples. Chaque nœud dans le pool de hello peut exécuter des tâches sous un compte d’utilisateur définis sur le pool entier de hello. Pour plus d’informations sur les tâches d’instances multiples, consultez [utiliser multi\-instance tâches des applications MPI toorun](batch-mpi.md).

### <a name="create-named-user-accounts"></a>Créer des comptes d’utilisateur nommé

toocreate nommé de comptes d’utilisateur dans un lot, ajouter une collection de pool toohello de comptes d’utilisateur. Hello extraits de code suivants montrent comment toocreate nommé comptes d’utilisateur dans .NET, Java et Python. Ces afficher des extraits de code comment toocreate admin et non nommée sur un pool de comptes d’administrateur. les exemples Hello créent des pools à l’aide de la configuration du service cloud hello, mais que vous utilisez hello même approche lors de la création d’un pool de Windows ou Linux à l’aide de la configuration d’ordinateur virtuel hello.

#### <a name="batch-net-example-windows"></a>Exemple .NET Batch (Windows)

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

#### <a name="batch-net-example-linux"></a>Exemple .NET Batch (Linux)

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


#### <a name="batch-java-example"></a>Exemple Java Batch

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

#### <a name="batch-python-example"></a>Exemple Python Batch

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

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a>Exécution d’une tâche sous un compte d’utilisateur nommé disposant d’un accès avec élévation de privilèges

toorun une tâche en tant qu’avec élévation de privilèges, hello définies pour les tâches de **UserIdentity** tooa propriété nommé le compte d’utilisateur qui a été créée avec sa **ElevationLevel** propriété trop`Admin`.

Cet extrait de code spécifie que cette tâche hello doit s’exécuter sous un compte d’utilisateur nommé. Ce compte d’utilisateur nommé a été défini sur le pool de hello lorsque hello pool a été créé. Dans ce cas, hello appelé compte d’utilisateur a été créé avec des autorisations d’administrateur :

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-toohello-latest-batch-client-library"></a>Mettre à jour votre bibliothèque de client de lot dernier code toohello

version du service de traitement par lots Hello 2017-01-01.4.0 introduit une modification avec rupture, en remplaçant hello **runElevated** propriété disponible dans les versions antérieures avec hello **userIdentity** propriété. Hello les tableaux suivants fournit un simple mappage que vous pouvez utiliser tooupdate votre code à partir de versions antérieures des bibliothèques clientes de hello.

### <a name="batch-net"></a>.NET Batch

| Si votre code utilise...                  | Mettez-le à jour vers...                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| `CloudTask.RunElevated` non spécifié | Aucune mise à jour requise                                                                                               |

### <a name="batch-java"></a>Java Batch

| Si votre code utilise...                      | Mettez-le à jour vers...                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| `CloudTask.withRunElevated` non spécifié | Aucune mise à jour requise                                                                                                                     |

### <a name="batch-python"></a>Python Batch

| Si votre code utilise...                      | Mettez-le à jour vers...                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | `user_identity=user`, où <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | `user_identity=user`, où <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| `run_elevated` non spécifié | Aucune mise à jour requise                                                                                                                                  |


## <a name="next-steps"></a>Étapes suivantes

### <a name="batch-forum"></a>Forum Azure Batch

Hello [Forum de traitement par lots Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) sur MSDN est une bonne placer toodiscuss lot et poser des questions sur le service de hello. Consultez le forum pour obtenir des publications utiles et publiez les questions que vous vous posez pendant la création de vos solutions Batch.
