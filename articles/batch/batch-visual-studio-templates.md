---
title: "aaaStart création de solutions de lot avec les modèles de projet Visual Studio - Azure | Documents Microsoft"
description: "Découvrez comment des modèles de projet Visual Studio peuvent vous aider à implémenter et à exécuter vos charges de travail nécessitant beaucoup de ressources sur Azure Batch."
services: batch
documentationcenter: .net
author: fayora
manager: timlt
editor: 
ms.assetid: 5e041ae2-25af-4882-a79e-3aa63c4bfb20
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a61c480ddc4dffd66c01220a137a3e852e39c338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-project-templates-toojump-start-batch-solutions"></a>Utiliser des solutions de lot de Visual Studio projet modèles toojump-Démarrer

Hello **Gestionnaire de travaux** et **modèles Visual Studio de tâche processeur** pour le traitement par lots fournissent le code toohelp vous tooimplement et exécuter vos charges de travail de calcul intensif sur le traitement par lots avec hello moins quantité de travail. Ce document décrit ces modèles et fournit des conseils sur la façon de toouse les.

> [!IMPORTANT]
> Cet article traite uniquement les modèles applicables toothese deux informations et part du principe que vous êtes familiarisé avec le service de traitement par lots hello et tooit connexes des concepts clés : calcul de pools, nœuds, travaux et tâches, le Gestionnaire des tâches, les variables d’environnement et autres informations pertinentes. Vous trouverez plus d’informations dans [principes de base d’Azure Batch](batch-technical-overview.md), [vue d’ensemble de lot pour les développeurs](batch-api-basics.md), et [démarrer avec la bibliothèque de traitement par lots Azure hello pour .NET](batch-dotnet-get-started.md).
> 
> 

## <a name="high-level-overview"></a>Vue d’ensemble globale
modèles de gestionnaire de travaux et tâches processeur Hello peuvent être toocreate utilisés de deux composants utiles :

* Une tâche du gestionnaire de travaux qui permet de fractionner un travail afin de le découper en plusieurs tâches pouvant être exécutées indépendamment, en parallèle.
* Un processeur de tâches qui peut être pré-traitement tooperform utilisés et post-traitement autour d’une ligne de commande d’application.

Par exemple, dans un scénario de rendu vidéo, fractionnées de travail hello activer un travail de séquence unique dans des centaines, voire des milliers de tâches distinctes qui seraient traitent des frames individuels séparément. En conséquence, processeur de tâches hello serait appeler hello rendu application et tous les processus dépendants qui sont nécessaire toorender chaque frame, ainsi qu’exécuter toute action supplémentaire (par exemple, copie hello rendu frame tooa emplacement de stockage).

> [!NOTE]
> modèles de gestionnaire de travaux et tâches processeur Hello sont indépendantes des autres, vous pouvez donc choisir toouse à la fois, ou uniquement un d’eux selon les spécifications de hello de votre travail de calcul et de vos préférences.
> 
> 

Comme indiqué dans le schéma hello ci-dessous, un travail de calcul qui utilise ces modèles passe par trois étapes :

1. le code Hello client (par exemple, application, service web, etc.) soumet un toohello de la tâche service de traitement par lots sur Azure, en spécifiant en tant que son programme Gestionnaire de travail manager tâche hello travail.
2. service de traitement par lots Hello exécute la tâche du gestionnaire hello sur un nœud de calcul et hello travail fractionnées lance hello spécifiée nombre de tâches du processeur de tâches, si plusieurs nœuds de calcul en fonction des besoins, selon les paramètres de hello et les spécifications dans le code de fractionnement de tâche hello.
3. Hello tâche processeur tâches s’exécutent indépendamment, en parallèle, tooprocess les données d’entrée hello et génèrent des données de sortie hello.

![Diagramme montrant comment le code client interagit avec hello service Batch][diagram01]

## <a name="prerequisites"></a>Composants requis
modèles de lot toouse hello, vous devrez suivant de hello :

* Un ordinateur où Visual Studio 2015 est installé. Les modèles Batch sont actuellement pris en charge seulement pour Visual Studio 2015.
* modèles de lot Hello, qui sont disponibles à partir de hello [galerie Visual Studio] [ vs_gallery] en tant qu’extensions de Visual Studio. Il existe deux façons de modèles de hello tooget :
  
  * Installer les modèles hello à l’aide de hello **Extensions et mises à jour** boîte de dialogue dans Visual Studio (pour plus d’informations, consultez [recherche et utilisation des Extensions Visual Studio][vs_find_use_ext]). Bonjour **Extensions et mises à jour** boîte de dialogue, la recherche et le téléchargement hello suivant deux extensions :
    
    * Le gestionnaire de travaux Azure Batch avec l’outil de fractionnement du travail
    * Le processeur de tâches Azure Batch
  * Télécharger des modèles de hello à partir de la galerie en ligne de hello pour Visual Studio : [modèles de projet Microsoft Azure Batch][vs_gallery_templates]
* Si vous envisagez de toouse hello [les Packages d’applications](batch-application-packages.md) Gestionnaire de travaux de fonctionnalité toodeploy hello et toohello de processeur de tâches par lots des nœuds de calcul, vous devez toolink un tooyour de compte de stockage du compte Batch.

## <a name="preparation"></a>Préparation
Nous vous recommandons de créer une solution peut contenir votre gestionnaire de travaux, ainsi que votre processeur de tâches, car cela peut rendre plus facile code tooshare entre votre gestionnaire de travaux et les programmes de traitement de tâche. toocreate cette solution, procédez comme suit :

1. Ouvrez Visual Studio et sélectionnez **Fichier** > **Nouveau** > **Projet**.
2. Sous **Modèles**, développez **Autres Types de projets**, cliquez sur **Solutions Visual Studio**, puis sélectionnez **Nouvelle Solution**.
3. Tapez un nom qui décrit votre objet application et hello de cette solution (par exemple, « LitwareBatchTaskPrograms »).
4. toocreate hello nouvelle solution, cliquez sur **OK**.

## <a name="job-manager-template"></a>Modèle du gestionnaire de travaux
modèle de gestionnaire de travaux Hello permet de vous tooimplement une tâche du gestionnaire qui peut effectuer hello suivant des actions :

* Fractionner un travail en plusieurs tâches.
* Envoyer ces toorun de tâches sur le lot.

> [!NOTE]
> Pour plus d’informations sur le gestionnaire de travaux, consultez [Présentation des fonctionnalités du service Batch pour les développeurs](batch-api-basics.md#job-manager-task).
> 
> 

### <a name="create-a-job-manager-using-hello-template"></a>Créer un gestionnaire de travaux à l’aide du modèle de hello
tooadd une solution de toohello de gestionnaire de travail que vous avez créé précédemment, procédez comme suit :

1. Ouvrez votre solution existante dans Visual Studio.
2. Dans l’Explorateur de solutions de hello avec le bouton droit, cliquez sur **ajouter** > **nouveau projet**.
3. Sous **Visual C#**, cliquez sur **Cloud**, puis sur **Azure Batch Job Manager with Job Splitter** (Gestionnaire de travaux Azure Batch avec outil de fractionnement du travail).
4. Tapez un nom qui décrit votre application, ce projet en tant que gestionnaire de travaux hello (par exemple) « GestionnaireTravauxLitware »).
5. projet de hello toocreate, cliquez sur **OK**.
6. Enfin, build hello projet tooforce Visual Studio tooload tous les référencé les packages NuGet et tooverify qui hello du projet n’est valide avant de commencer à modifier.

### <a name="job-manager-template-files-and-their-purpose"></a>Les fichiers du modèle du gestionnaire de travaux et leur objectif
Lorsque vous créez un projet à l’aide du modèle de gestionnaire de travaux hello, il génère trois groupes de fichiers de code :

* fichier de programme principal Hello (Program.cs). Il contient le point d’entrée de programme de hello et la gestion des exceptions de niveau supérieur. Vous ne devez pas normalement besoin toomodify.
* répertoire du Framework Hello. Il contient des fichiers de hello responsables hello 'standard' travailler par programme de gestionnaire de travaux hello – décompression des paramètres, ajouter des lots de tâches toohello, etc.. Vous ne devez pas normalement besoin toomodify ces fichiers.
* fichier de fractionnement de travail Hello (JobSplitter.cs). C’est là que vous allez placer la logique spécifique à votre application pour le fractionnement d’un travail en tâches.

Bien sûr vous pouvez ajouter des fichiers supplémentaires comme toosupport requis votre code de fractionnement travail, selon la complexité hello du travail hello séparation logique.

modèle de Hello génère également des fichiers de projet .NET standards comme un fichier .csproj app.config, packages.config, etc..

reste Hello de cette section décrit les différents fichiers de hello et leur structure de code et explique ce que fait chaque classe.

![Explorateur de solutions Visual Studio affichant des solutions de modèle de gestionnaire de travaux hello][solution_explorer01]

**Fichiers Framework**

* `Configuration.cs`: Encapsule chargement hello travail de données de configuration telles que les détails du compte Batch, informations d’identification du compte de stockage liés, les informations de projet et la tâche et paramètres de la tâche. Il fournit également accès aux variables d’environnement de définis par le tooBatch (voir les paramètres d’environnement pour les tâches, dans la documentation de lot hello) via la classe de Configuration.EnvironmentVariable hello.
* `IConfiguration.cs`: Résumés hello implémentation de classe de Configuration de hello, afin que vous puissiez de test unitaire votre séparateur de travail à l’aide d’un objet de configuration faux ou fictive.
* `JobManager.cs`: Orchestre des composants de programme de gestion du travail hello hello. Il est chargé de hello l’initialisation du séparateur de travail hello, appel de séparateur de travail hello, et la distribution des tâches de hello retourné par le soumissionnaire tâche toohello hello travail fractionnées.
* `JobManagerException.cs`Représente une erreur qui nécessite hello travail manager tooterminate. JobManagerException est utilisé toowrap les erreurs 'attendu' où les informations de diagnostic spécifiques peuvent être fournies dans le cadre de l’arrêt.
* `TaskSubmitter.cs`: Cette classe est retournées par lots hello projet fractionnées toohello des tâches tooadding responsable. classe de JobManager Hello agrège séquence hello de tâches dans des lots de travail de toohello plus efficace mais en temps voulu, puis appelle TaskSubmitter.SubmitTasks sur un thread d’arrière-plan pour chaque lot.

**Outil de fractionnement du travail**

`JobSplitter.cs`: Cette classe contient la logique pour fractionner le travail de hello en tâches spécifiques à l’application. Hello framework appelle hello JobSplitter.Split méthode tooobtain une séquence de tâches, qu’elle ajoute travail toohello en tant que méthode hello les retourne. Il s’agit d’hello classe où vous serez injecter la logique de hello de votre travail. Implémenter hello fractionnement méthode tooreturn une séquence d’instances CloudTask représentant les tâches hello dans lequel vous souhaitez le travail de hello toopartition.

**Fichiers de projet de ligne de commande .NET standard**

* `App.config`: Fichier de configuration d’application .NET standard.
* `Packages.config`: Fichier de dépendance de package NuGet standard.
* `Program.cs`: Contient le point d’entrée de programme de hello et la gestion des exceptions de niveau supérieur.

### <a name="implementing-hello-job-splitter"></a>Implémentation de fractionnement de tâche hello
Lorsque vous ouvrez le projet de modèle de gestionnaire de travaux hello, hello projet possède fichier JobSplitter.cs de hello ouverte par défaut. Vous pouvez implémenter hello fractionner logique pour les tâches de hello dans votre charge de travail à l’aide d’afficher de méthode hello Split() ci-dessous :

```csharp
/// <summary>
/// Gets hello tasks into which toosplit hello job. This is where you inject
/// your application-specific logic for decomposing hello job into tasks.
///
/// hello job manager framework invokes hello Split method for you; you need
/// only tooimplement it, not toocall it yourself. Typically, your
/// implementation should return tasks lazily, for example using a C#
/// iterator and hello "yield return" statement; this allows tasks toobe added
/// and toostart running while splitting is still in progress.
/// </summary>
/// <returns>hello tasks toobe added toohello job. Tasks are added automatically
/// by hello job manager framework as they are returned by this method.</returns>
public IEnumerable<CloudTask> Split()
{
    // Your code for hello split logic goes here.
    int startFrame = Convert.ToInt32(_parameters["StartFrame"]);
    int endFrame = Convert.ToInt32(_parameters["EndFrame"]);

    for (int i = startFrame; i <= endFrame; i++)
    {
        yield return new CloudTask("myTask" + i, "cmd /c dir");
    }
}
```

> [!NOTE]
> Hello annoté section Bonjour `Split()` méthode est section uniquement hello hello code de modèle de gestionnaire de travaux qui est destiné à vous toomodify en ajoutant hello logique toosplit vos travaux de différentes tâches. Si vous souhaitez toomodify une autre section du modèle de hello, vérifiez que vous sont être familiarisé avec le fonctionne de lot et essayer de quelques exemples de hello [traiter par lot des exemples de code][github_samples].
> 
> 

Votre implémentation Split() a accès :

* Hello paramètres du travail, via hello `_parameters` champ.
* Hello CloudJob de l’objet travail représentant hello via hello `_job` champ.
* Hello CloudTask de l’objet représentant hello tâche du gestionnaire, via hello `_jobManagerTask` champ.

Votre `Split()` implémentation n’a pas besoin travail de toohello tooadd tâches directement. Au lieu de cela, votre code doit retourner une séquence d’objets de CloudTask, et ils seront ajoutés toohello travail automatiquement par les classes de framework hello qui appellent le séparateur de travail hello. Il est commun toouse C# itérateur (`yield return`) tooimplement les séparateurs de travail de fonctionnalité car cela permet de hello toostart de tâches en cours d’exécution dès que possible, plutôt que d’attendre que toutes les tâches toobe calculés.

**Échec du fractionnement du travail**

Si votre outil de fractionnement du travail rencontre une erreur, il doit soit :

* Mettre fin à la séquence de hello à l’aide de hello c# `yield break` instruction, dans lequel le Gestionnaire de travaux hello cas est considéré comme réussi ; ou
* Une exception, dans laquelle le Gestionnaire de travaux hello cas est considéré comme ayant échoué et peut être retentée selon la client de hello a la configuration).

Dans les deux cas, toutes les tâches déjà retourné par le séparateur de travail hello et toohello ajouté par lots seront toorun éligible. Si vous ne souhaitez pas cette toohappen, vous pouvez :

* Arrêter le travail de hello avant le renvoi d’un fractionnement de tâche hello
* Collection d’ensemble de la tâche hello avant de le renvoyer de formuler (autrement dit, retourner un `ICollection<CloudTask>` ou `IList<CloudTask>` au lieu d’implémenter le séparateur de travail à l’aide d’un itérateur c#)
* Utilisez toomake de dépendances de tâche toutes les tâches dépendent de la réussite de hello du Gestionnaire de travaux hello

**Nouvelles tentatives du gestionnaire de travaux**

Si le Gestionnaire de travaux hello échoue, il peut être retentée par le service de traitement par lots hello en fonction des paramètres de nouvelle tentative hello client. En règle générale, il s’agit-safe, car lors de l’infrastructure de hello ajoute le travail de toohello de tâches, il ignore toutes les tâches qui existent déjà. Toutefois, si le calcul de tâches est coûteux, vous pouvez de pas coût de hello tooincur de recalcul des tâches qui ont déjà été ajoutés toohello travail ; à l’inverse, si vous exécutez de nouveau hello est toogenerate non garanti hello même ID de tâche, puis le comportement d’ignorer les doublons hello ne se lancera pas. Dans ce cas, vous devez concevoir votre travail fractionnées toodetect hello le travail a déjà été effectué et se répète pas, par exemple en effectuant un CloudJob.ListTasks avant de démarrer des tâches de tooyield.

### <a name="exit-codes-and-exceptions-in-hello-job-manager-template"></a>Quitter les codes et les exceptions dans le modèle de gestionnaire de travaux hello
Codes de sortie et les exceptions fournissent un résultat de hello toodetermine mécanisme d’exécution d’un programme, et elles peuvent aider à tooidentify tous les problèmes de l’exécution de hello du programme de hello. modèle de gestionnaire de travaux Hello implémente les codes de sortie hello et exceptions décrites dans cette section.

Une tâche du gestionnaire qui est implémentée avec un modèle de gestionnaire de travaux hello peut retourner trois codes de sortie possibles :

| Code | Description |
| --- | --- |
| 0 |Gestionnaire de travaux Hello s’est terminé correctement. Votre code de fractionnement du travail exécuté toocompletion et toutes les tâches ont été ajoutées toohello travail. |
| 1 |Échec de la tâche du gestionnaire Hello avec une exception dans une partie 'attendue' du programme de hello. exception de Hello a été traduit tooa JobManagerException avec des informations de diagnostic et, si possible, des suggestions de résolution hello échec. |
| 2 |Échec de la tâche du gestionnaire Hello avec une exception « inattendue ». exception Hello était connecté toostandard de sortie, mais le Gestionnaire de travaux hello tooadd Impossible de toutes les informations de diagnostic ou de mise à jour supplémentaires. |

Dans les cas de hello Échec de tâche de Gestionnaire des tâches, certaines tâches peuvent toujours ont été ajoutées toohello service avant hello erreur s’est produite. Ces tâches s’exécutent normalement. Pour plus d’informations sur ce chemin de code, consultez la rubrique « Échec du fractionnement du travail » ci-dessus.

Toutes les informations de hello retournées par les exceptions sont écrites dans les fichiers stdout.txt et stderr.txt. Pour plus d’informations, consultez la rubrique [Gestion des erreurs](batch-api-basics.md#error-handling).

### <a name="client-considerations"></a>Considérations du client
Cette section présente certaines exigences d’implémentation du client lors de l’appel d’un gestionnaire de travaux basé sur ce modèle. Consultez [comment toopass paramètres et variables d’environnement à partir de hello code client](#pass-environment-settings) pour plus d’informations sur le passage des paramètres et des paramètres d’environnement.

**Informations d’identification obligatoires**

Dans l’ordre tooadd tâches toohello Azure par lots, tâche hello du gestionnaire requiert votre URL de compte Azure Batch et la clé. Vous devez les transmettre en tant que variables d’environnement appelées YOUR_BATCH_URL et YOUR_BATCH_KEY. Vous pouvez définir dans le Gestionnaire de travaux de hello paramètres d’environnement de tâche. Par exemple, dans un client C# :

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    new EnvironmentSetting("YOUR_BATCH_URL", "https://account.region.batch.azure.com"),
    new EnvironmentSetting("YOUR_BATCH_KEY", "{your_base64_encoded_account_key}"),
};
```
**Informations d’identification de stockage**

En règle générale, hello client n’a pas besoin tooprovide hello stockage compte informations d’identification toohello tâche du gestionnaire, car (a) la plupart des responsables de projet n’est pas nécessaire de compte de stockage tooexplicitly accès hello lié et (b) hello compte de stockage lié est souvent fournie tâches tooall comme un paramètre d’environnement courant pour le travail de hello. Si vous ne fournissez pas hello lié compte de stockage via les paramètres d’environnement commun hello, le Gestionnaire de travaux hello nécessite un accès toolinked stockage, puis vous devez fournir des informations d’identification du stockage hello lié comme suit :

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    /* other environment settings */
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

**Paramètres de tâche du gestionnaire de travaux**

client de Hello doit définir le Gestionnaire de travaux hello *killJobOnCompletion* indicateur trop**false**.

Il est plus sûr pour hello client tooset *runExclusive* trop**false**.

Hello client doit utiliser un hello *resourceFiles* ou *applicationPackageReferences* collection toohave hello le Gestionnaire de travaux exécutable (et ses DLL requises) déployé toohello de nœud de calcul.

Par défaut, le Gestionnaire de travaux hello ne sera pas relancée en cas d’échec. Selon votre logique du Gestionnaire de travail, les clients hello souhaitant tentatives tooenable via *contraintes*/*maxTaskRetryCount*.

**Paramètres du travail**

Si le séparateur de travail hello émet des tâches avec des dépendances, client de hello doit définir des tootrue usesTaskDependencies de la tâche hello.

Dans le modèle de séparateur de travail hello, il est rare pour les clients toowish tooadd tâches toojobs au-delà le fractionnement de la tâche hello crée. client de Hello doit par conséquent normalement définie de la tâche hello *onAllTasksComplete* trop**terminatejob**.

## <a name="task-processor-template"></a>Modèle du processeur de tâches
Un modèle de tâche vous permet de tooimplement un processeur de tâches que peut effectuer hello suit les actions suivantes :

* Définir les informations de hello requises par chaque toorun de tâche de traitement par lots.
* Exécuter toutes les actions requises par chaque tâche Batch.
* Enregistrez les sorties de tâche toopersistent stockage.

Bien que le processeur de tâches n’est pas requis toorun des tâches sur le lot, hello principal avantage de l’utilisation du processeur de tâches est qu’il fournit un wrapper tooimplement toutes les actions de l’exécution de tâches dans un seul emplacement. Par exemple, si vous devez toorun plusieurs applications dans le contexte de hello de chaque tâche, ou si vous avez besoin de toocopy toopersistent stockage après la fin de chaque tâche.

les actions Hello effectuées par le processeur de tâche hello peuvent être simple ou complexe et autant ou aussi peu, comme requis par votre charge de travail. En outre, en mettant en œuvre toutes les actions de tâches dans un processeur de tâches, vous pouvez facilement mettre à jour ou ajouter des actions en fonction des exigences de tooapplications ou de la charge de travail des modifications. Toutefois, dans certains cas un processeur de tâches peut-être pas idéal de hello pour votre implémentation comme il peut ajouter une complexité inutile, par exemple lors de l’exécution de travaux peut être démarré rapidement à partir d’une ligne de commande simple.

### <a name="create-a-task-processor-using-hello-template"></a>Créer un processeur de tâches à l’aide du modèle de hello
tooadd une solution de toohello de processeur de tâches que vous avez créé précédemment, procédez comme suit :

1. Ouvrez votre solution existante dans Visual Studio.
2. Dans l’Explorateur de solutions de hello avec le bouton droit, cliquez sur **ajouter**, puis cliquez sur **nouveau projet**.
3. Sous **Visual C#**, cliquez sur **Cloud**, puis sur **Azure Batch Task Processor** (Processeur de tâches Azure Batch).
4. Tapez un nom qui décrit votre application et identifie ce projet comme hello processeur de tâches (par exemple) « ProcesseurLitwareTask »).
5. projet de hello toocreate, cliquez sur **OK**.
6. Enfin, build hello projet tooforce Visual Studio tooload tous les référencé les packages NuGet et tooverify qui hello du projet n’est valide avant de commencer à modifier.

### <a name="task-processor-template-files-and-their-purpose"></a>Les fichiers du modèle du processeur de tâches et leur objectif
Lorsque vous créez un projet à l’aide du modèle de traitement de tâche hello, il génère trois groupes de fichiers de code :

* fichier de programme principal Hello (Program.cs). Il contient le point d’entrée de programme de hello et la gestion des exceptions de niveau supérieur. Vous ne devez pas normalement besoin toomodify.
* répertoire du Framework Hello. Il contient des fichiers de hello responsables hello 'standard' travailler par programme de gestionnaire de travaux hello – décompression des paramètres, ajouter des lots de tâches toohello, etc.. Vous ne devez pas normalement besoin toomodify ces fichiers.
* fichier du processeur tâche Hello (TaskProcessor.cs). Il s’agit dans lequel vous placerez votre logique spécifique à l’application pour l’exécution d’une tâche (en général en appelant exécutable existant de tooan). C’est aussi là que se trouve le code de pré et de post-traitement, tel que le téléchargement de données supplémentaires ou de fichiers de résultats.

Bien sûr vous pouvez ajouter des fichiers supplémentaires comme toosupport requis votre code de processeur tâche, en fonction de la complexité hello du travail hello séparation logique.

modèle de Hello génère également des fichiers de projet .NET standards comme un fichier .csproj app.config, packages.config, etc..

reste Hello de cette section décrit les différents fichiers de hello et leur structure de code et explique ce que fait chaque classe.

![Explorateur de solutions Visual Studio affichant des solutions de modèle de processeur de la tâche hello][solution_explorer02]

**Fichiers Framework**

* `Configuration.cs`: Encapsule chargement hello travail de données de configuration telles que les détails du compte Batch, informations d’identification du compte de stockage liés, les informations de projet et la tâche et paramètres de la tâche. Il fournit également accès aux variables d’environnement de définis par le tooBatch (voir les paramètres d’environnement pour les tâches, dans la documentation de lot hello) via la classe de Configuration.EnvironmentVariable hello.
* `IConfiguration.cs`: Résumés hello implémentation de classe de Configuration de hello, afin que vous puissiez de test unitaire votre séparateur de travail à l’aide d’un objet de configuration faux ou fictive.
* `TaskProcessorException.cs`Représente une erreur qui nécessite hello travail manager tooterminate. TaskProcessorException est utilisé toowrap les erreurs 'attendu' où les informations de diagnostic spécifiques peuvent être fournies dans le cadre de l’arrêt.

**Processeur de tâches**

* `TaskProcessor.cs`: Exécute la tâche hello. framework de Hello appelle la méthode TaskProcessor.Run de hello. Il s’agit d’hello classe où vous serez injecter la logique de spécifiques à l’application de hello de votre tâche. Implémentez la méthode Run hello :
  * Analyser et valider les paramètres de n’importe quelle tâche
  * Composer la ligne de commande hello pour n’importe quel programme externe, vous souhaitez tooinvoke
  * Enregistrer des informations de diagnostic qui peuvent vous être utiles pour le débogage
  * Démarrer un processus à l’aide de cette ligne de commande
  * Attendez que hello processus tooexit
  * Capturer le code de sortie hello hello processus toodetermine si elle a réussi ou a échoué
  * Enregistrer tous les fichiers de sortie que vous souhaitez tookeep toopersistent stockage

**Fichiers de projet de ligne de commande .NET standard**

* `App.config`: Fichier de configuration d’application .NET standard.
* `Packages.config`: Fichier de dépendance de package NuGet standard.
* `Program.cs`: Contient le point d’entrée de programme de hello et la gestion des exceptions de niveau supérieur.

## <a name="implementing-hello-task-processor"></a>Implémentation du processeur de tâches hello
Lorsque vous ouvrez le projet de modèle de processeur de tâches hello, hello projet possède fichier TaskProcessor.cs de hello ouverte par défaut. Vous pouvez implémenter la logique hello exécuter des tâches de hello dans votre charge de travail à l’aide de méthode de Run() hello indiqué ci-dessous :

```csharp
/// <summary>
/// Runs hello task processing logic. This is where you inject
/// your application-specific logic for decomposing hello job into tasks.
///
/// hello task processor framework invokes hello Run method for you; you need
/// only tooimplement it, not toocall it yourself. Typically, your
/// implementation will execute an external program (from resource files or
/// an application package), check hello exit code of that program and
/// save output files toopersistent storage.
/// </summary>
public async Task<int> Run()

{
    try
    {
        //Your code for hello task processor goes here.
        var command = $"compare {_parameters["Frame1"]} {_parameters["Frame2"]} compare.gif";
        using (var process = Process.Start($"cmd /c {command}"))
        {
            process.WaitForExit();
            var taskOutputStorage = new TaskOutputStorage(
            _configuration.StorageAccount,
            _configuration.JobId,
            _configuration.TaskId
            );
            await taskOutputStorage.SaveAsync(
            TaskOutputKind.TaskOutput,
            @"..\stdout.txt",
            @"stdout.txt"
            );
            return process.ExitCode;
        }
    }
    catch (Exception ex)
    {
        throw new TaskProcessorException(
        $"{ex.GetType().Name} exception in run task processor: {ex.Message}",
        ex
        );
    }
}
```
> [!NOTE]
> Hello annotée section hello méthode Run() est section uniquement de hello hello processeur de tâches du code de modèle qui est destiné à vous toomodify en ajoutant une logique pour les tâches de hello hello exécuter dans votre charge de travail. Si vous souhaitez toomodify une autre section du modèle de hello, Veuillez tout d’abord Familiarisez-vous avec le fonctionnement de lot en consultant la documentation du lot hello et essayer de quelques exemples de code de lot hello.
> 
> 

Hello méthode Run() est chargé de lancer la ligne de commande hello, à partir d’un ou plusieurs processus, en attente pour tous les processus toocomplete, l’enregistrement des résultats de hello et enfin retour avec un code de sortie. Hello méthode Run() est où vous implémentez hello logique pour vos tâches de traitement. infrastructure de processeur Hello tâches appelle la méthode de Run() de hello pour vous. vous n’avez pas besoin de toocall il vous-même.

Votre implémentation Run() a accès :

* Hello des paramètres de la tâche via hello `_parameters` champ.
* Hello ID de projet et la tâche via hello `_jobId` et `_taskId` champs.
* configuration de la tâche Hello, via hello `_configuration` champ.

**Échec de la tâche**

En cas de défaillance, vous pouvez quitter la méthode Run() de hello en levant une exception, mais cela laisse un gestionnaire d’exceptions de niveau supérieur hello dans le contrôle de code de sortie de tâche hello. Si vous avez besoin de code de sortie hello toocontrol afin que vous pouvez distinguer les différents types d’échec, par exemple pour établir un diagnostic ou parce que certains modes d’échec doivent s’arrêter les travaux hello et autres ne doivent pas, puis vous devez quitter la méthode Run() de hello en retournant un code de sortie différent de zéro. Cela devient le code de sortie de tâche hello.

### <a name="exit-codes-and-exceptions-in-hello-task-processor-template"></a>Quitter les codes et les exceptions dans le modèle de processeur de la tâche hello
Codes de sortie et les exceptions fournissent un résultat de hello toodetermine mécanisme d’exécution d’un programme, et elles peuvent aider à identifier les problèmes avec l’exécution de hello du programme de hello. modèle de processeur de tâches Hello implémente les codes de sortie hello et exceptions décrites dans cette section.

Une tâche de processeur qui est implémentée avec un modèle de tâche hello peut retourner trois codes de sortie possibles :

| Code | Description |
| --- | --- |
| [Process.ExitCode][process_exitcode] |processeur de tâches Hello toocompletion s’est produite. Notez que cela ne signifie pas ce programme hello que l’appel a réussi : uniquement ce processeur de la tâche hello a été appelée et effectuer tout traitement sans exceptions. sens de Hello du code de sortie hello dépend de programme de hello appelé : en général, le code de sortie 0 signifie a réussi le programme de hello et tout autre code de sortie signifie que le programme hello a échoué. |
| 1 |processeur de tâches Hello a échoué avec une exception dans une partie 'attendue' du programme de hello. Hello exception a été traduit tooa `TaskProcessorException` avec des informations de diagnostic et, si possible, des suggestions de résolution hello échec. |
| 2 |processeur de tâches Hello a échoué avec une exception « inattendue ». exception Hello était connecté toostandard de sortie, mais processeur de tâches hello tooadd Impossible de toutes les informations de diagnostic ou de mise à jour supplémentaires. |

> [!NOTE]
> Si le programme hello que vous appelez utilise des modes d’échec spécifique tooindicate exit codes 1 et 2, puis à l’aide de codes de sortie 1 et 2 pour les erreurs de processeur de tâche est ambigu. Vous pouvez modifier ces codes de sortie de tâche processeur erreur codes toodistinctive en modifiant les cas d’exception hello dans le fichier Program.cs de hello.
> 
> 

Toutes les informations de hello retournées par les exceptions sont écrites dans les fichiers stdout.txt et stderr.txt. Pour plus d’informations, voir gestion d’erreurs, Bonjour documentation du lot.

### <a name="client-considerations"></a>Considérations du client
**Informations d’identification de stockage**

Si votre processeur de tâches utilise des sorties de toopersist de stockage blob Azure, par exemple à l’aide de la bibliothèque d’assistance de hello fichier conventions, puis il a besoin d’accéder trop*soit* hello des informations d’identification de compte de stockage cloud *ou* une URL de conteneur d’objets blob qui inclut une signature d’accès partagé (SAS). modèle de Hello prend en charge en fournissant des informations d’identification via des variables d’environnement courantes. Votre client peut transmettre des informations d’identification du stockage hello comme suit :

```csharp
job.CommonEnvironmentSettings = new [] {
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

compte de stockage Hello est ensuite disponible dans hello classe TaskProcessor via hello `_configuration.StorageAccount` propriété.

Si vous préférez toouse une URL de conteneur de SAP, vous pouvez également passer ce via un paramètre d’environnement courantes de travail, mais les modèle de traitement de tâche hello n’inclut pas actuellement prise en charge intégrée pour ce.

**Paramétrage du stockage**

Il est recommandé de cette tâche de gestionnaire de client ou de la tâche hello créer n’importe quel conteneur requis par les tâches avant d’ajouter le travail de toohello tâches hello. Ce champ est obligatoire que si vous utilisez une URL de conteneur de SAP, par conséquent une URL n’inclut pas autorisation toocreate hello conteneur. Il est recommandé de même si vous transmettez des informations d’identification du compte de stockage, qu’il enregistre toutes les tâches ayant toocall CloudBlobContainer.CreateIfNotExistsAsync sur le conteneur de hello.

## <a name="pass-parameters-and-environment-variables"></a>Transmettre des paramètres et des variables d’environnement
### <a name="pass-environment-settings"></a>Transmettre des paramètres d’environnement
Un client peut transmettre des informations toohello tâche du gestionnaire sous forme de hello de paramètres d’environnement. Ces informations peuvent ensuite être utilisées par la tâche du gestionnaire hello lors de la tâche de calcul de génération tâches processeur hello tâche qui seront exécute dans le cadre de hello. Exemples d’informations hello que vous pouvez passer en tant que paramètres d’environnement sont :

* Clés d’accès et nom du compte de stockage
* URL du compte Batch
* Clé du compte Batch

Hello service Batch possède une mécanisme simple toopass environnement paramètres tooa tâche du gestionnaire à l’aide de hello `EnvironmentSettings` propriété dans [Microsoft.Azure.Batch.JobManagerTask][net_jobmanagertask].

Par exemple, tooget hello `BatchClient` instance pour un compte de traitement par lots, vous pouvez passer comme variables d’environnement à partir du client de hello code hello URL et partagé des informations d’identification de clé pour le compte de traitement par lots hello. De même, compte de stockage tooaccess hello est lié toohello du compte Batch, vous pouvez passer le nom de compte de stockage hello et clé de compte de stockage hello en tant que variables d’environnement.

### <a name="pass-parameters-toohello-job-manager-template"></a>Passez le modèle de gestionnaire de travaux toohello de paramètres
Dans de nombreux cas, il est utile toopass par travail paramètres toohello tâche du gestionnaire, des travaux hello toocontrol divisant processus ou tâches hello tooconfigure hello travail. Pour cela, en téléchargeant un fichier JSON nommé parameters.json comme fichier de ressources pour la tâche du gestionnaire hello. paramètres de Hello peuvent ensuite devenir disponibles Bonjour `JobSplitter._parameters` champ dans le modèle de gestionnaire de travaux hello.

> [!NOTE]
> Gestionnaire de paramètres prédéfinis de Hello prend en charge uniquement les dictionnaires de chaîne en chaîne. Si vous souhaitez que les valeurs JSON complexes toopass comme valeurs de paramètre, serez toopass ces sous forme de chaînes et les analyser dans un fractionnement de tâche hello ou que vous modifiez du framework hello `Configuration.GetJobParameters` (méthode).
> 
> 

### <a name="pass-parameters-toohello-task-processor-template"></a>Passer des paramètres toohello tâche modèle de traitement
Vous pouvez également transmettre des paramètres tooindividual tâches implémentée à l’aide du modèle de tâche hello. Tout comme avec le modèle de gestionnaire de tâche hello, modèle de traitement de tâche hello recherche un fichier de ressources nommé

Parameters.JSON et s’il a déterminé qu’il charge en tant que dictionnaire de paramètres hello. Il existe deux options pour la toopass paramètres toohello tâches processeur de tâches :

* Réutiliser les paramètres de la tâche hello JSON. Cela fonctionne bien si seuls les paramètres hello sont ceux qui sont à l’échelle de la tâche (par exemple, un rendu hauteur et largeur). toodo, lors de la création d’un CloudTask de fractionnement de tâche hello, ajouter un objet de fichier de référence toohello parameters.json resource de ResourceFiles de hello tâche du gestionnaire (`JobSplitter._jobManagerTask.ResourceFiles`) collecte des ResourceFiles de toohello CloudTask.
* Générer et télécharger un document parameters.json de tâches spécifiques dans le cadre de l’exécution du travail fractionnées et faire référence à cet objet blob dans la collection de fichiers de ressources de la tâche hello. Cela est nécessaire si des tâches différentes ont des paramètres différents. Un exemple peut être un scénario de rendu 3D dans lequel les index de trame hello est passé toohello tâche en tant que paramètre.

> [!NOTE]
> Gestionnaire de paramètres prédéfinis de Hello prend en charge uniquement les dictionnaires de chaîne en chaîne. Si vous souhaitez que les valeurs JSON complexes toopass comme valeurs de paramètre, serez toopass ces sous forme de chaînes et les analyser dans le processeur de tâche hello ou que vous modifiez du framework hello `Configuration.GetTaskParameters` (méthode).
> 
> 

## <a name="next-steps"></a>Étapes suivantes
### <a name="persist-job-and-task-output-tooazure-storage"></a>Conserver les travaux et les tâches de sortie tooAzure stockage
Les [conventions de fichiers Azure Batch][nuget_package] sont également utiles au développement de solutions Batch. Utilisez cette bibliothèque de classes .NET (actuellement en version préliminaire) dans votre magasin de tooeasily d’applications .NET de lot et récupérer des tooand des sorties de tâche depuis le stockage Azure. [Conserver la sortie de projet et la tâche de traitement par lots Azure](batch-task-output.md) contient une description complète de la bibliothèque de hello et son utilisation.

### <a name="batch-forum"></a>Forum Azure Batch
Hello [Forum de traitement par lots Azure] [ forum] sur MSDN est une bonne placer toodiscuss lot et poser des questions sur le service de hello. Consultez le forum pour obtenir des publications « permanentes » utiles et publiez les questions que vous vous posez pendant la création de vos solutions Batch.

[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[net_jobmanagertask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobmanagertask.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[process_exitcode]: https://msdn.microsoft.com/library/system.diagnostics.process.exitcode.aspx
[vs_gallery]: https://visualstudiogallery.msdn.microsoft.com/
[vs_gallery_templates]: https://go.microsoft.com/fwlink/?linkid=820714
[vs_find_use_ext]: https://msdn.microsoft.com/library/dd293638.aspx

[diagram01]: ./media/batch-visual-studio-templates/diagram01.png
[solution_explorer01]: ./media/batch-visual-studio-templates/solution_explorer01.png
[solution_explorer02]: ./media/batch-visual-studio-templates/solution_explorer02.png
