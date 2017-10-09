---
title: "packages d’applications aaaInstall sur les nœuds de calcul - Azure Batch | Documents Microsoft"
description: "Utiliser la fonctionnalité packages application hello de traitement par lots Azure tooeasily gérer plusieurs applications et les nœuds de calcul des versions pour l’installation sur le lot."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 3b6044b7-5f65-4a27-9d43-71e1863d16cf
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 683be7b7f1bd5db7835332016f6dccb72f45c3b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-applications-toocompute-nodes-with-batch-application-packages"></a>Déployer des nœuds de toocompute d’applications avec les packages d’applications de traitement par lots

fonctionnalité Hello de packages d’application de traitement par lots Azure fournit une gestion plus simple des applications de la tâche et leur toohello déploiement nœuds de calcul dans le pool. Avec les packages d’application, vous pouvez télécharger et gérer plusieurs versions d’applications hello que vos tâches de s’exécuter, y compris leurs fichiers de support. Vous pouvez ensuite automatiquement déployer une ou plusieurs de ces applications toohello nœuds de calcul dans le pool.

Dans cet article, vous allez apprendre comment tooupload et gérer des packages d’application Bonjour portail Azure. Vous apprendrez ensuite comment tooinstall sur d’un pool nœuds de calcul avec hello [Batch .NET] [ api_net] bibliothèque.

> [!NOTE]
> 
> Les packages d’applications sont pris en charge sur tous les pools Batch créés après le 5 juillet 2017. Elles sont prises en charge sur les pools de traitement par lots créés entre 10 mars 2016 et 5 juillet 2017 uniquement si le pool de hello a été créé à l’aide d’une configuration de Service Cloud. Les pools de lot créés too10 préalable mars 2016 ne gèrent pas les packages d’applications.
>
> API pour créer et gérer des packages d’application Hello font partie de hello [Batch Management .NET] [[api_net_mgmt]] bibliothèque. API pour l’installation des packages d’application sur un nœud de calcul Hello font partie de hello [Batch .NET] [ api_net] bibliothèque.  
>
> fonctionnalité de packages d’application Hello décrite ici remplace la fonctionnalité des applications Batch hello disponible dans les versions précédentes du service de hello.
> 
> 

## <a name="application-package-requirements"></a>Configuration requise des packages d’application
toouse des packages d’applications, vous devez trop[lier un compte de stockage Azure](#link-a-storage-account) tooyour compte Batch.

Cette fonctionnalité a été introduite dans [API REST de traitement par lots] [ api_rest] version 2015-12-01.2.2). et hello correspondant [Batch .NET] [ api_net] version de la bibliothèque 3.1.0. Nous vous recommandons de toujours utiliser version plus récente de l’API hello lorsque vous travaillez avec un lot.

> [!NOTE]
> Les packages d’applications sont pris en charge sur tous les pools Batch créés après le 5 juillet 2017. Elles sont prises en charge sur les pools de traitement par lots créés entre 10 mars 2016 et 5 juillet 2017 uniquement si le pool de hello a été créé à l’aide d’une configuration de Service Cloud. Les pools de lot créés too10 préalable mars 2016 ne gèrent pas les packages d’applications.
>
>

## <a name="about-applications-and-application-packages"></a>Concernant les applications et les packages d’applications
Dans le traitement par lots Azure, un *application* fait référence à set tooa des fichiers binaires avec version qui peuvent être des nœuds de calcul toohello automatiquement téléchargé dans votre pool de. Un *package d’application* fait référence tooa *ensemble spécifique* des fichiers binaires et représente une donnée *version* de l’application hello.

![Diagramme détaillé sur les applications et les packages d’applications][1]

### <a name="applications"></a>Applications
Une application dans le lot contient une ou plusieurs applications, packages et spécifie les options de configuration de l’application hello. Par exemple, une application peut spécifier hello par défaut application package version tooinstall sur les nœuds de calcul et si ses packages peuvent être mis à jour ou supprimées.

### <a name="application-packages"></a>packages d’application
Un package d’application est un fichier .zip qui contient les fichiers binaires d’application hello et les fichiers de prise en charge qui sont requises pour votre application de hello toorun tâches. Chaque package d’application représente une version spécifique de l’application hello.

Vous pouvez spécifier les packages d’applications au niveau hello pool et des tâches. Lorsque vous créez un pool ou une tâche, vous pouvez spécifier un ou plusieurs de ces packages et, le cas échéant, une version.

* **Les packages d’applications du pool** sont déployés trop*chaque* nœud dans le pool de hello. Les applications sont déployées lorsqu’un nœud rejoint un pool, et lorsqu’il est redémarré ou réinitialisé.
  
    Les packages d’application de pool sont appropriés lorsque tous les nœuds dans un pool exécutent les tâches d’un travail. Vous pouvez spécifier un ou plusieurs packages d’application lorsque vous créez un pool, et vous pouvez ajouter ou mettre à jour les packages d’un pool existant. Si vous mettez à jour les packages d’applications d’un pool existant, vous devez redémarrer ses nœuds tooinstall hello nouveau package.
* **Les packages d’applications de tâches** sont déployées uniquement le nœud de calcul tooa planifiée toorun une tâche, juste avant d’exécuter la ligne de commande de la tâche hello. Si hello spécifié version et le package d’application est déjà sur le nœud de hello, il n’est pas redéployé et hello les package existant est utilisé.
  
    Packages d’applications de tâche sont utiles dans les environnements de pool partagé, où différentes tâches sont exécutées sur un pool et pool de hello n’est pas supprimé lorsqu’un travail est terminé. Si votre travail comporte moins de tâches que les nœuds dans le pool de hello, packages d’applications de tâche peuvent réduire le transfert de données depuis votre application est déployée toohello uniquement les nœuds qui exécutent des tâches.
  
    Les autres scénarios pouvant tirer parti des packages d’application de tâche sont les travaux qui exécutent une application lourde, mais uniquement pour un petit nombre de tâches. Par exemple, une étape de prétraitement ou une tâche de fusion, où les application de pré-traitement ou de fusion hello est lourd, peut-être bénéficier à l’aide de packages d’applications Office.

> [!IMPORTANT]
> Il existe des restrictions de nombre de hello des applications et des packages d’applications au sein d’un compte de traitement par lots et de la taille du package maximale application hello. Consultez [Quotas et limites pour hello service Azure Batch](batch-quota-limit.md) pour plus d’informations sur ces limites.
> 
> 

### <a name="benefits-of-application-packages"></a>Avantages des packages d’applications
Les packages d’applications peuvent simplifier le code hello dans votre solution de traitement par lots et des inférieur hello généraux toomanage requis hello applications vos tâches.

Avec les packages d’application, tâche de démarrage de votre pool n’est toospecify une longue liste de tooinstall des fichiers de ressources individuels sur les nœuds hello. Vous n’avez pas toomanually gérer plusieurs versions de vos fichiers d’application dans le stockage Azure, ou sur les nœuds. Et vous n’avez pas besoin de tooworry sur la génération de [URL de SAP](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide toohello accéder aux fichiers de votre compte de stockage. Fonctionne en arrière-plan hello avec les packages d’applications Azure Storage toostore du lot et les déployer toocompute nœuds.

> [!NOTE] 
> Hello taille totale d’une tâche de démarrage doit être inférieur ou égal too32768 caractères, y compris les fichiers de ressources et les variables d’environnement. Si votre tâche de démarrage dépasse cette limite, l’utilisation de packages d’application est une autre option. Vous pouvez également créer une archive ZIP qui contient vos fichiers de ressources, télécharger sous la forme d’un objet blob de tooAzure stockage, puis décompressez-le à partir de la ligne de commande hello de votre tâche de démarrage. 
>
>

## <a name="upload-and-manage-applications"></a>Téléchargement et gestion des applications
Vous pouvez utiliser hello [portail Azure] [ portal] ou hello [Batch Management .NET](batch-management-dotnet.md) packages d’application bibliothèque toomanage hello dans votre compte Batch. Dans hello ensuite des sections suivantes, nous montrer tout d’abord comment toolink un compte de stockage, puis discutez ajoutant des applications et packages et les gérer avec hello portal.

### <a name="link-a-storage-account"></a>Liaison d’un compte de stockage
toouse des packages d’applications, vous devez d’abord lier un tooyour de compte de stockage Azure du compte Batch. Si vous n’avez pas encore configuré un compte de stockage, hello portail Azure affiche un avertissement hello première fois que vous cliquez sur hello **Applications** vignette Bonjour **compte Batch** panneau.

> [!IMPORTANT]
> Prend en charge du lot actuellement *uniquement* hello **à usage général** type de compte de stockage comme décrit à l’étape 5, [créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account), dans [sur Azure comptes de stockage](../storage/common/storage-create-storage-account.md). Lorsque vous liez un tooyour de compte de stockage Azure du compte Batch, *uniquement* un **à usage général** compte de stockage.
> 
> 

![Avertissement « Aucun compte de stockage configuré » dans le portail Azure][9]

Hello lot service utilise hello associés toostore de compte de stockage vos packages d’application. Une fois que vous avez lié des deux comptes de hello, lot peut déployer automatiquement des packages de hello stockées dans les nœuds de calcul hello lié stockage compte tooyour. toolink un tooyour de compte de stockage du compte Batch, cliquez sur **les paramètres de compte de stockage** sur hello **avertissement** panneau, puis cliquez sur **compte de stockage** sur hello **Compte de stockage** panneau.

![Panneau Sélectionner un compte de stockage dans le Portail Azure][10]

Nous vous recommandons de créer un compte de stockage *spécifiquement* destiné à être utilisé avec votre compte Batch et de le sélectionner ici. Pour plus d’informations sur la façon toocreate un compte de stockage, consultez la section « Créer un compte de stockage » dans [les comptes sur le stockage Azure](../storage/common/storage-create-storage-account.md). Une fois que vous avez créé un compte de stockage, vous pouvez ensuite lier il tooyour lot compte à l’aide de hello **compte de stockage** panneau.

> [!WARNING]
> Hello service Batch utilise le stockage Azure toostore vos packages d’application en tant qu’objets BLOB de blocs. Vous êtes [facturé comme d’habitude] [ storage_pricing] pour les données blob de bloc hello. Être sûr de taille de hello tooconsider et nombre de vos packages d’application et supprimer régulièrement les coûts de toominimize déconseillées de packages.
> 
> 

### <a name="view-current-applications"></a>Affichage des applications en cours
applications de hello tooview dans votre compte de traitement par lots, cliquez sur hello **Applications** élément de menu dans le menu de gauche hello lors de l’affichage hello **compte Batch** panneau.

![Vignette Applications][2]

Cette option de menu ouvre hello **Applications** panneau :

![Liste des applications][3]

Hello **Applications** panneau affiche hello ID de chaque application dans votre compte et hello les propriétés suivantes :

* **Packages**: hello le nombre de versions associées à cette application.
* **Version par défaut**: version de l’application hello installée si vous n’indiquez pas une version lorsque vous spécifiez l’application hello pour un pool. Ce paramètre est facultatif.
* **Autoriser les mises à jour**: valeur hello qui spécifie si le package met à jour, suppressions et les ajouts sont autorisés. Si la valeur est trop**non**, mises à jour de package et les suppressions sont désactivées pour l’application hello. Seules les nouvelles versions de package d’application pourront être ajoutées. valeur par défaut Hello est **Oui**.

### <a name="view-application-details"></a>Affichage des détails de l’application
panneau hello tooopen qui inclut des détails de hello pour une application, sélectionnez hello Bonjour **Applications** panneau.

![Détails de l’application][4]

Dans le panneau des détails de l’application hello, vous pouvez configurer hello suivant les paramètres de votre application.

* **Autoriser les mises à jour** : permet de spécifier si ses packages d’application peuvent être mis à jour ou supprimés. Voir la section « Mettre à jour ou supprimer un package d’application » dans la suite de cet article.
* **Version par défaut**: spécifiez une valeur par défaut package toodeploy toocompute des nœuds d’applications.
* **Nom d’affichage**: spécifiez un nom convivial votre solution peut utiliser lorsqu’il affiche plus d’informations sur l’application hello, par exemple, Bonjour l’interface utilisateur d’un service que vous fournissez tooyour des clients via le traitement de lot.

### <a name="add-a-new-application"></a>Ajout d’une application
toocreate une nouvelle application, ajoutez un package d’application et spécifier un ID d’application des nouveaux et uniques. Hello premier package d’application que vous ajoutez à un nouvel ID d’application hello crée également la nouvelle application de hello.

Cliquez sur **ajouter** sur hello **Applications** hello tooopen de panneau **nouvelle application** panneau.

![Panneau Nouvelle application dans le Portail Azure][5]

Hello **nouvelle application** panneau fournit des paramètres de hello toospecify de votre package d’application et la nouvelle application de champs de suivant de hello.

**ID d’application**

Ce champ spécifie l’ID hello de votre nouvelle application, qui est le sujet toohello standard ID de lot Azure des règles de validation. règles de Hello pour fournir un ID d’application sont les suivantes :

* Sur les nœuds de Windows hello ID peut contenir n’importe quelle combinaison de caractères alphanumériques, des traits d’union et des traits de soulignement. Sur des nœuds Linux, seuls les caractères alphanumériques et les traits de soulignement sont autorisés.
* Ne peut pas contenir plus de 64 caractères.
* Doit être unique au sein de hello compte Batch.
* Conserve la casse et ne respecte pas la casse.

**Version**

Ce champ spécifie la version de hello du package d’application hello que vous téléchargez. Chaînes de version sont toohello sujet suivant les règles de validation :

* Sur les nœuds de Windows, chaîne de version hello peut contenir n’importe quelle combinaison de caractères alphanumériques, des traits d’union, des traits de soulignement et des points. Des nœuds Linux, la chaîne de version hello peut contenir uniquement des caractères alphanumériques et des traits de soulignement.
* Ne peut pas contenir plus de 64 caractères.
* Doit être unique au sein de l’application hello.
* Conservent la casse et ne respectent pas la casse.

**Package d’application**

Ce champ spécifie le fichier .zip hello qui contient les fichiers binaires d’application hello et fichiers de prise en charge l’application hello tooexecute requis. Cliquez sur hello **sélectionner un fichier** zone ou hello tooand de toobrowse icône de dossier sélectionner un fichier .zip qui contient les fichiers de votre application.

Une fois que vous avez sélectionné un fichier, cliquez sur **OK** toobegin hello téléchargement tooAzure stockage. Lors de l’opération de téléchargement de hello est terminée, portail de hello affiche une notification et ferme le panneau de hello. Selon la taille de hello du fichier hello que vous êtes hello et téléchargement de la vitesse de votre connexion réseau, cette opération peut prendre un certain temps.

> [!WARNING]
> Ne fermez pas hello **nouvelle application** panneau avant de l’opération de téléchargement de hello est terminée. Cela arrête les processus de téléchargement hello.
> 
> 

### <a name="add-a-new-application-package"></a>Ajout d’un package d’application
tooadd une nouvelle version de package d’application pour une application existante, sélectionnez une application Bonjour **Applications** panneau, cliquez sur **Packages**, puis cliquez sur **ajouter** tooopen Hello **un package** panneau.

![Panneau Ajouter un package d’application dans le Portail Azure][8]

Comme vous pouvez le voir, les champs hello correspondent à celles de hello **nouvelle application** panneau mais hello **id de l’Application** à cocher est désactivée. Comme vous l’avez fait pour application hello, spécifiez hello **Version** pour votre nouveau package, parcourir tooyour **package d’Application** .zip de fichier, puis cliquez sur **OK** hello de tooupload package.

### <a name="update-or-delete-an-application-package"></a>Mettre à jour ou supprimer un package d’application
tooupdate ou supprimer un package d’application, panneau de détails hello ouvert pour l’application hello, cliquez sur **Packages** tooopen hello **Packages** panneau, cliquez sur hello **sélection**dans la ligne hello hello du package d’application que vous souhaitez toomodify et sélectionnez l’action hello que vous souhaitez tooperform.

![Mettre à jour ou supprimer un package dans le Portail Azure][7]

**Mettre à jour**

Lorsque vous cliquez sur **mise à jour**, hello *package de mise à jour* panneau s’affiche. Ce panneau est similaire toohello *nouveau package d’application* panneau toutefois seul champ de sélection de package de hello est activé, ce qui vous toospecify une nouvelle tooupload de fichier ZIP.

![Panneau Mettre à jour un package dans le Portail Azure][11]

**Supprimer**

Lorsque vous cliquez sur **supprimer**, vous êtes invité à la suppression hello tooconfirm de version du package hello et lot supprime le package de hello depuis le stockage Azure. Si vous supprimez la version par défaut de hello d’une application, hello **version par défaut** paramètre est supprimé pour l’application hello.

![Supprimer l’application][12]

## <a name="install-applications-on-compute-nodes"></a>Installation d’applications sur des nœuds de calcul
Maintenant que vous avez appris comment toomanage application packages avec hello portail Azure, nous pouvons voir comment toodeploy les nœuds de toocompute et de les exécuter avec les tâches de traitement par lots.

### <a name="install-pool-application-packages"></a>Installation des packages d’application de pool
tooinstall un package d’application sur tous les nœuds de calcul dans un pool, spécifiez au moins un package d’application *références* pour le pool de hello. les packages d’applications Hello que vous spécifiez pour un pool sont installés sur chaque nœud de calcul lorsque ce nœud rejoint le pool de hello et lorsque le nœud de hello est redémarré ou la réinitialisation.

Dans Batch .NET, spécifiez une ou plusieurs propriétés [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] lorsque vous créez un pool ou pour un pool existant. Hello [ApplicationPackageReference] [ net_pkgref] classe spécifie un ID d’application et la version tooinstall sur d’un pool nœuds de calcul.

```csharp
// Create hello unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify hello application and version tooinstall on hello compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit hello pool so that it's created in hello Batch service. As hello nodes join
// hello pool, hello specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> Si un déploiement de package d’application échoue pour une raison quelconque, les marques de service de traitement par lots hello hello nœud [inutilisable][net_nodestate], et aucune tâche est planifiée pour l’exécution sur ce nœud. Dans ce cas, vous devez **redémarrer** hello de déploiement de package de nœud tooreinitiate hello. Nœud de hello redémarrage vous permet également de planification des tâches à nouveau sur le nœud de hello.
> 
> 

### <a name="install-task-application-packages"></a>Installation des packages d’application de tâche
Pool de tooa similaire, spécifiez de package d’application *références* pour une tâche. Lorsqu’une tâche est planifiée toorun sur un nœud, le package de hello est téléchargé et extrait juste avant l’exécution de la ligne de commande de la tâche hello. Si une version et le package spécifié est déjà installé sur le nœud de hello, package de hello n’est pas téléchargé et hello les package existant est utilisé.

tooinstall un package d’application Office, configurez la tâche hello [CloudTask][net_cloudtask].[ ApplicationPackageReferences] [ net_cloudtask_pkgref] propriété :

```csharp
CloudTask task =
    new CloudTask(
        "litwaretask001",
        "cmd /c %AZ_BATCH_APP_PACKAGE_LITWARE%\\litware.exe -args -here");

task.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference
    {
        ApplicationId = "litware",
        Version = "1.1001.2b"
    }
};
```

## <a name="execute-hello-installed-applications"></a>Exécuter des applications de hello installé
Hello packages que vous avez spécifié pour un pool ou une tâche sont téléchargés et extrait tooa nommé répertoire hello `AZ_BATCH_ROOT_DIR` du nœud de hello. Traitement par lots crée également une variable d’environnement qui contient toohello de chemin d’accès hello nommé active. Les lignes de commande de tâche utiliser cette variable d’environnement pour référencer l’application hello sur le nœud de hello. 

Sur les nœuds de Windows, variable de hello est Bonjour suivant le format :

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

Des nœuds Linux, le format de hello est légèrement différente. Points (.), des tirets (-) et des signes dièse (#) sont mis à plat toounderscores dans la variable d’environnement hello. Par exemple :

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

`APPLICATIONID`et `version` sont des valeurs qui correspondent toohello application et la version du package que vous avez spécifié pour le déploiement. Par exemple, si vous avez spécifié cette version 2.7 d’application *blender* doit être installé sur les nœuds de Windows, les lignes de commande de tâche utiliseriez cette tooaccess de variable d’environnement ses fichiers :

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

Des nœuds Linux, spécifiez la variable d’environnement hello dans ce format :

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

Lorsque vous téléchargez un package d’application, vous pouvez spécifier un tooyour toodeploy de version par défaut des nœuds de calcul. Si vous avez spécifié une version par défaut pour une application, vous pouvez omettre suffixe de version hello lorsque vous faites référence application hello. Vous pouvez spécifier la version de l’application par défaut hello Bonjour portail Azure, dans le panneau des Applications hello, comme indiqué dans [télécharger et gérer des applications](#upload-and-manage-applications).

Par exemple, si vous définissez « 2.7 » en tant que version par défaut de hello pour application *blender*, vos tâches référencent hello suivant la variable d’environnement, puis les nœuds de Windows seront exécute la version 2.7 :

`AZ_BATCH_APP_PACKAGE_BLENDER`

Hello extrait de code suivant montre un exemple de ligne de commande tâche qui lance la version par défaut de hello Hello *blender* application :

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> Consultez [paramètres d’environnement pour les tâches](batch-api-basics.md#environment-settings-for-tasks) Bonjour [vue d’ensemble de lot](batch-api-basics.md) pour plus d’informations sur les paramètres d’environnement de nœud de calcul.
> 
> 

## <a name="update-a-pools-application-packages"></a>Mise à jour des packages d’applications d’un pool
Si un pool existant a déjà été configuré avec un package d’application, vous pouvez spécifier un nouveau package pour le pool de hello. Si vous spécifiez une nouvelle référence de package pour un pool, suivants de hello s’appliquent :

* Hello service Batch installe package nouvellement spécifié de hello sur tous les nœuds nouveau joindre le pool de hello et sur n’importe quel nœud existant qui est redémarré ou la réinitialisation.
* Calcul des nœuds qui sont déjà dans le pool de hello lorsque vous mettez à jour les références de package hello n’installent pas automatiquement le nouveau package d’application hello. Ces nœuds doivent être redémarrés ou réinitialisé tooreceive hello nouveau package de calcul.
* Lorsqu’un nouveau package est déployé, hello créé des variables d’environnement reflètent les nouvelles références de package d’application hello.

Dans cet exemple, un pool existant hello a la version 2.7 de hello *blender* application configurée comme l’un de ses [CloudPool][net_cloudpool].[ ApplicationPackageReferences][net_cloudpool_pkgref]. nœuds du pool tooupdate hello avec la version 2.76b, spécifiez un nouveau [ApplicationPackageReference] [ net_pkgref] avec la nouvelle version de hello et validation hello modification.

```csharp
string newVersion = "2.76b";
CloudPool boundPool = await batchClient.PoolOperations.GetPoolAsync("myPool");
boundPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "blender",
        Version = newVersion }
};
await boundPool.CommitAsync();
```

Maintenant que hello nouvelle version a été configurée, hello service Batch installe la version 2.76b tooany *nouveau* nœud qui rejoint hello pool. tooinstall 2.76b sur nœuds hello *déjà* dans le pool de hello, redémarrez ou les réinitialiser. Notez que les nœuds redémarrés conservent fichiers hello à partir des déploiements de package précédents.

## <a name="list-hello-applications-in-a-batch-account"></a>Liste des applications hello dans un compte Batch
Vous pouvez répertorier les applications hello et les packages dans un compte de traitement par lots à l’aide de hello [ApplicationOperations][net_appops].[ ListApplicationSummaries] [ net_appops_listappsummaries] (méthode).

```csharp
// List hello applications and their application packages in hello Batch account.
List<ApplicationSummary> applications = await batchClient.ApplicationOperations.ListApplicationSummaries().ToListAsync();
foreach (ApplicationSummary app in applications)
{
    Console.WriteLine("ID: {0} | Display Name: {1}", app.Id, app.DisplayName);

    foreach (string version in app.Versions)
    {
        Console.WriteLine("  {0}", version);
    }
}
```

## <a name="wrap-up"></a>Conclusion
Avec les packages d’application, vous pouvez aider vos clients sélectionnez applications hello pour leurs tâches et spécifiez hello version exacte toouse lors du traitement des travaux avec votre service de traitement par lots. Vous pouvez également permettre de hello pour votre tooupload clients et effectuer le suivi de leurs propres applications dans votre service.

## <a name="next-steps"></a>Étapes suivantes
* Hello [API REST de traitement par lots] [ api_rest] fournit également la prise en charge toowork avec les packages d’applications. Par exemple, consultez hello [applicationPackageReferences] [ rest_add_pool_with_packages] élément [ajouter un compte du pool de tooan] [ rest_add_pool] pour plus d’informations sur la façon toospecify tooinstall de packages à l’aide des API REST de hello. Consultez [Applications] [ rest_applications] pour plus d’informations sur comment informations à l’aide de l’application tooobtain hello API REST de traitement par lots.
* Découvrez comment tooprogrammatically [gérer les quotas avec Batch Management .NET et des comptes Azure Batch](batch-management-dotnet.md). Hello [Batch Management .NET][api_net_mgmt] bibliothèque peut activer des fonctionnalités de création et la suppression de compte pour votre application de traitement ou d’un service.

[api_net]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/client?view=azure-dotnet
[api_net_mgmt]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/management?view=azure-dotnet
[api_rest]: https://docs.microsoft.com/en-us/rest/api/batchservice/
[batch_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[github_samples]: https://github.com/Azure/azure-batch-samples
[storage_pricing]: https://azure.microsoft.com/pricing/details/storage/
[net_appops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.aspx
[net_appops_listappsummaries]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.listapplicationsummaries.aspx
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_cloudpool_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.applicationpackagereferences.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.aspx
[net_cloudtask_pkgref]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.applicationpackagereferences.aspx
[net_nodestate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.state.aspx
[net_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationpackagereference.aspx
[portal]: https://portal.azure.com
[rest_applications]: https://msdn.microsoft.com/library/azure/mt643945.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_pool_with_packages]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_apkgreference

[1]: ./media/batch-application-packages/app_pkg_01.png "Diagramme détaillée des packages d’applications"
[2]: ./media/batch-application-packages/app_pkg_02.png "Vignette Applications dans le Portail Azure"
[3]: ./media/batch-application-packages/app_pkg_03.png "Panneau Application dans le Portail Azure"
[4]: ./media/batch-application-packages/app_pkg_04.png "Panneau Détails de l’application dans le Portail Azure"
[5]: ./media/batch-application-packages/app_pkg_05.png "Panneau Nouvelle application dans le Portail Azure"
[7]: ./media/batch-application-packages/app_pkg_07.png "Liste déroulante Mettre à jour ou supprimer des packages dans le Portail Azure"
[8]: ./media/batch-application-packages/app_pkg_08.png "Panneau Nouveau package d’application dans le Portail Azure"
[9]: ./media/batch-application-packages/app_pkg_09.png "Alerte Aucun compte de stockage lié"
[10]: ./media/batch-application-packages/app_pkg_10.png "Panneau Sélectionner un compte de stockage dans le Portail Azure"
[11]: ./media/batch-application-packages/app_pkg_11.png "Panneau Mettre à jour un package dans le Portail Azure"
[12]: ./media/batch-application-packages/app_pkg_12.png "Boîte de dialogue de confirmation de la suppression d’un package dans le Portail Azure"
