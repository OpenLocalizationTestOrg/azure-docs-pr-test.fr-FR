---
title: "aaaAzure lot exécute les solutions informatiques parallèles à grande échelle dans le cloud de hello | Documents Microsoft"
description: "En savoir plus sur l’utilisation du service de traitement par lots Azure hello pour parallèles à grande échelle et les charges de travail HPC"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 93e37d44-7585-495e-8491-312ed584ab79
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: acc52e46330c465f81951441d9067371098cf63a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-intrinsically-parallel-workloads-with-batch"></a>Exécuter des charges de travail intrinsèquement parallèles avec Batch

Traitement par lots Azure est un service de plateforme pour l’exécution des applications à grande échelle parallèle et haute-performance computing (HPC) efficacement dans le cloud de hello. Traitement par lots Azure planifie toorun de travail de calcul intensif sur une collection gérée de machines virtuelles, et peut automatiquement montée en puissance de calcul ressources toomeet hello aux besoins de vos tâches.

Avec Azure Batch, vous pouvez facilement définir tooexecute des ressources de calcul Azure vos applications en parallèle et à grande échelle. Il n’existe aucun toomanually besoin de créer, configurer et gérer un cluster HPC, les machines virtuelles, les réseaux virtuels ou une tâche complexe et infrastructure de planification de tâches. Azure Batch automatise ou simplifie ces tâches.

## <a name="use-cases-for-batch"></a>Exemples d’utilisation du service Batch
Batch est un service Azure géré qui est utilisé pour le *traitement par lots* ou *Batch Computing*, et qui exécute un grand nombre de tâches similaires afin d’obtenir les résultats souhaités. Le traitement par lots est couramment utilisé dans les entreprises qui sont régulièrement amenées à traiter, transformer et analyser d’importants volumes de données.

Le service Batch fonctionne parfaitement avec les applications et charges de travail intrinsèquement parallèles (ou « massivement parallèles »). Les charges de travail intrinsèquement parallèles peuvent être facilement fractionnées en plusieurs tâches exécutées simultanément sur plusieurs ordinateurs.

![Tâches parallèles][1]<br/>

Voici quelques exemples de charges de travail communément traitées à l’aide de cette technique :

* Modélisation de risques financiers
* Analyse des données hydrologiques et météorologiques
* Rendu, analyse et traitement d’images
* Encodage et transcodage multimédia
* Analyse de séquence génétique
* Analyse des contraintes en ingénierie
* Test de logiciels

Lot peut également effectuer des calculs parallèles avec une étape de la réduire à la fin de hello et exécuter des charges de travail HPC plus complexes telles que [Interface MPI (Message Passing)](batch-mpi.md) applications.

Pour obtenir une comparaison entre Batch et d’autres solutions HPC utilisées dans Azure, consultez la page [Solutions Batch et HPC](batch-hpc-solutions.md).

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="scenario-scale-out-a-parallel-workload"></a>Scénario : Montée en charge d’une charge de travail parallèle
Une solution commune qui utilise des hello API de lot toointeract avec hello service Batch implique la montée en charge de travail intrinsèquement parallèle telles que le rendu hello des images pour des scènes 3D--sur un pool de nœuds de calcul. Ce pool de nœuds de calcul peut être « votre batterie de rendu » qui fournit des dizaines, centaines ou voire des milliers de travail de rendu tooyour cœurs, par exemple.

Hello diagramme suivant montre un flux de travail de lot courant, avec une application cliente ou un service hébergé à l’aide de lot toorun une charge de travail parallèle.

![Flux de travail de la solution Batch][2]

Dans ce scénario courant, votre application ou service traite une charge de travail de calcul dans Azure Batch en effectuant hello comme suit :

1. Télécharger hello **les fichiers d’entrée** et hello **application** qui traitera ces tooyour fichiers compte de stockage Azure. les fichiers d’entrée Hello peuvent être des données de votre application va traiter, comme les données de modélisation financière ou des fichiers vidéo toobe transcodé. fichiers de l’application Hello peuvent être n’importe quelle application qui est utilisée pour le traitement des données hello, tel qu’une application de rendu 3D ou d’un TRANSCODEUR de support.
2. Créez un lot **pool** de nœuds de calcul dans votre compte Batch--ces nœuds sont des machines virtuelles hello qui exécutera vos tâches. Vous spécifiez des propriétés telles que hello [taille du nœud](../cloud-services/cloud-services-sizes-specs.md), leur système d’exploitation et l’emplacement de hello dans le stockage Azure de hello application tooinstall lorsque les nœuds hello rejoindre le pool de hello (application hello que vous avez téléchargé à l’étape #1). Vous pouvez également configurer le pool de hello trop[mettre automatiquement à l’échelle](batch-automatic-scaling.md) dans la réponse toohello la charge de travail qui génèrent de vos tâches. Montée en puissance automatique dynamiquement ajuste nombre hello de nœuds de calcul dans le pool de hello.
3. Créez un lot **travail** la charge de travail hello toorun sur pool hello de nœuds de calcul. Lorsque vous créez un travail, vous devez l’associer à un pool Batch.
4. Ajouter **tâches** toohello travail. Lorsque vous ajoutez la tâche tooa de tâches, hello service Batch planifie automatiquement les tâches de hello d’exécution sur les nœuds de calcul hello dans le pool de hello. Chaque tâche utilise l’application hello que vous avez téléchargé les fichiers d’entrée de tooprocess hello.
   
   * 4a. Avant l’exécution d’une tâche, il peut télécharger les données de salutation (fichiers d’entrée de hello) qu’il est le nœud de calcul toohello tooprocess qu'auquel elle est assignée. Si application hello n’a pas déjà été installée sur le nœud de hello (voir étape #2), il peut être téléchargé ici à la place. Lorsque les téléchargements hello sont terminées, les tâches de hello s’exécutent sur leurs nœuds attribués.
5. Comme hello tâches s’exécutent, vous pouvez interroger la progression de hello toomonitor lot de travail de hello et ses tâches. Votre application cliente ou le service communique avec hello service Batch via HTTPS. Étant donné que vous avez peut analyser des milliers de tâches qui s’exécutent sur des milliers de nœuds de calcul, veillez trop[interroger le service de traitement par lots hello efficacement](batch-efficient-list-queries.md).
6. Comme hello tâches terminées, ils peuvent télécharger leur tooAzure de données de résultat stockage. Vous pouvez également récupérer des fichiers directement à partir de système de fichiers hello sur un nœud de calcul.
7. Votre analyse détecte que les tâches de hello dans votre travail terminées, votre application cliente ou un service peut télécharger des données de sortie hello pour un traitement supplémentaire ou d’évaluation.

Gardez à l’esprit, c’est une façon toouse lot et ce scénario décrit quelques-uns de ses fonctionnalités disponibles. Par exemple, vous pouvez exécuter [plusieurs tâches en parallèle](batch-parallel-node-tasks.md) sur chaque nœud de calcul, et vous pouvez utiliser [les tâches de préparation et l’achèvement de la tâche](batch-job-prep-release.md) tooprepare hello nœuds pour vos tâches, puis nettoyer par la suite.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez une vue d’ensemble de hello service Batch, il est toolearn plu de temps toodig comment vous pouvez l’utiliser tooprocess vos charges de travail parallèles de calcul intensif.

* Hello de lecture [vue d’ensemble de lot pour les développeurs](batch-api-basics.md), des informations essentielles pour toute personne préparation toouse lot. Hello contient des informations détaillées sur les ressources du service de traitement par lots comme pools, nœuds, travaux, tâches et des hello nombreuses fonctionnalités de l’API que vous pouvez utiliser lors de la génération de votre application de traitement par lots.
* En savoir plus sur hello [outils et API de lot](batch-apis-tools.md) disponibles pour la création de solutions de traitement par lots.
* [Démarrer avec la bibliothèque de traitement par lots Azure hello pour .NET](batch-dotnet-get-started.md) toolearn comment toouse c# et hello Batch .NET bibliothèque tooexecute une charge de travail simple à l’aide d’un flux de travail courant de lot. Cet article doit être votre première arrête lorsque vous apprenez comment toouse hello service Batch. Il existe également un [version Python](batch-python-tutorial.md) du didacticiel de hello.
* Télécharger hello [code des exemples sur GitHub] [ github_samples] toosee comment c# et Python pouvant communiquer avec le lot tooschedule et processus exemple les charges de travail.
* Extraire hello [lot cursus] [ learning_path] tooget une idée de tooyou disponible de ressources hello en tant que vous découvrez toowork traitement par lots.


[github_samples]: https://github.com/Azure/azure-batch-samples
[learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/

[1]: ./media/batch-technical-overview/tech_overview_01.png
[2]: ./media/batch-technical-overview/tech_overview_02.png
