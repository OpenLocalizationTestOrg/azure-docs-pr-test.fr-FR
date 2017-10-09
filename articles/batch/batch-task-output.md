---
title: "aaaPersist résultats ou les journaux à partir de terminée des données tooa tâches store - Azure Batch | Documents Microsoft"
description: "Découvrez les différentes possibilités pour conserver les données de sortie des tâches et des travaux Batch. Vous pouvez conserver les données tooAzure stockage ou tooanother stocker."
services: batch
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0b11e387f1694e1ce3e9573db7f6013f0154cad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-output"></a>Conserver les résultats des tâches et des travaux

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

Voici quelques exemples courants de sortie de tâche :

- Fichiers créés lorsque le processus de tâche hello les données d’entrée.
- Fichiers journaux associés à l’exécution des tâches. 

Cet article décrit les différentes options de persistance scénarios de sortie et hello tâche pour laquelle chaque option est la plus appropriée.   

## <a name="about-hello-batch-file-conventions-standard"></a>À propos des standard de hello Conventions pour les fichiers par lots

Batch définit un ensemble facultatif de conventions pour nommer les fichiers de sortie de tâche dans le Stockage Azure. Hello [standard de Conventions pour les fichiers Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) décrit ces conventions. norme de Conventions pour les fichiers Hello détermine les noms de hello de hello conteneur et l’objet blob de chemin de destination dans le stockage Azure pour un fichier de sortie donnée en fonction du nom hello de hello projet et la tâche.

C’est tooyou si vous décidez de toouse hello Conventions standard pour vos fichiers de données de sortie d’affectation de noms pour les fichiers. Vous pouvez également nommer les objets blob et le conteneur de destination hello toutefois vous souhaitez. Si vous utilisez hello Conventions standard pour les fichiers de nommer les fichiers de sortie, vos fichiers de sortie sont disponibles pour l’affichage dans hello [portail Azure][portal].

Il existe différentes manières que vous pouvez utiliser la norme de Conventions pour les fichiers hello :

- Si vous utilisez des fichiers de sortie du service API toopersist hello lot, vous pouvez choisir les conteneurs de destination tooname et les objets BLOB en fonction de toohello Conventions standard pour les fichiers. Hello API de service de traitement par lots vous permet de toopersist les fichiers de sortie à partir du code client, sans modifier votre application de la tâche.
- Si vous développez avec .NET, vous pouvez utiliser hello [bibliothèque Conventions pour les fichiers par lots Azure pour .NET][nuget_package]. L’avantage de l’utilisation de cette bibliothèque est prise en charge l’interrogation de vos fichiers de sortie en fonction de tootheir ID ou l’objectif. fonctionnalités de requête intégrées Hello rendent tooaccess facilement des fichiers de sortie à partir d’une application cliente ou d’autres tâches. Toutefois, votre application de la tâche doit être bibliothèque de Conventions pour les fichiers modifiés toocall. Pour plus d’informations, consultez référence hello pour hello [bibliothèque Conventions pour les fichiers pour .NET](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.aspx).
- Si vous développez avec une langue autre que .NET, vous pouvez implémenter hello Conventions de fichier standard dans votre application.

## <a name="design-considerations-for-persisting-output"></a>Considérations de conception pour la conservation des sorties 

Lorsque vous concevez votre solution de traitement par lots, envisagez de toojob connexe des facteurs suivants de hello et résultats de tâches.

* **Durée de vie de nœud de calcul**: les nœuds de calcul sont souvent temporaires, notamment dans les pools à mise à l’échelle automatique. Sortie à partir d’une tâche qui s’exécute sur un nœud est disponible que lorsque le nœud hello existe, et uniquement au sein de la période de rétention du fichier hello que vous avez défini pour la tâche hello. Si une tâche génère la sortie qui peut-être être requises une fois la tâche hello est terminée, tâche hello doit télécharger son magasin durable tooa sortie fichiers tels que le stockage Azure.

* **Stockage de sortie** : le Stockage Azure est recommandé comme magasin de données pour la sortie des tâches, mais vous pouvez utiliser n’importe quel stockage durable. L’écriture de tâches sortie tooAzure stockage est intégré hello API de service de traitement par lots. Si vous utilisez une autre forme d’un stockage durable, vous devez sortie de la tâche toowrite hello application logique toopersist vous-même.   

* **Récupération de sortie**: vous pouvez récupérer sortie de la tâche directement à partir des nœuds de calcul hello dans votre pool d’ou de stockage Azure ou une autre banque de données si vous avez conservé la sortie de la tâche. tooretrieve une tâche de sortie directement à partir d’un nœud de calcul, vous devez le nom de fichier hello et son emplacement de sortie sur le nœud de hello. Si vous rendez persistante tooAzure de sortie de tâche stockage, vous devez fichier de toohello hello chemin d’accès complet dans les fichiers de sortie Azure Storage toodownload hello avec hello SDK Azure Storage.

* **Affichage de la sortie**: lorsque vous accédez tooa tâche hello Azure portail et sélectionnez **fichiers sur le nœud**ne Hello pas seulement les fichiers de sortie que vous êtes intéressé, vous sont présentées avec tous les fichiers associés de tâche hello. Là encore, les fichiers sur les nœuds de calcul sont disponibles que lorsque le nœud hello existe et uniquement dans la période de rétention hello que vous avez défini pour la tâche hello. sortie de la tâche de tooview que vous avez conservées tooAzure stockage, vous pouvez utiliser des hello portail Azure ou une application cliente de stockage Azure telles que hello [Azure Storage Explorer][storage_explorer]. tooview sortie des données dans le stockage Azure avec le portail de hello ou un autre outil, vous devez connaître l’emplacement du fichier hello et accédez tooit directement.

## <a name="options-for-persisting-output"></a>Options de conservation de sortie

Selon votre scénario, il existe quelques approches différentes, vous pouvez effectuer la sortie de la tâche toopersist :

- Utiliser les API de service de traitement par lots hello.  
- Utilisez la bibliothèque de Conventions pour les fichiers Batch hello pour .NET.  
- Implémenter hello Conventions pour les fichiers par lots standard dans votre application.
- Implémenter une solution de déplacement de fichiers personnalisée.

Hello les sections suivantes décrire chaque méthode plus en détail.

### <a name="use-hello-batch-service-api"></a>Utiliser l’API de service de traitement par lots hello

Avec la version 2017-05-01, hello service Batch ajoute la prise en charge pour la spécification des fichiers de sortie dans le stockage Azure pour les données de tâche lorsque vous [ajouter une tâche de tooa](https://docs.microsoft.com/rest/api/batchservice/add-a-task-to-a-job) ou [ajouter une collection de travaux de tooa tâches](https://docs.microsoft.com/rest/api/batchservice/add-a-collection-of-tasks-to-a-job).

Hello API de service de traitement par lots prend en charge la persistance tooan de données de tâche compte de stockage Azure à partir des pools créés avec la configuration d’ordinateur virtuel hello. Avec hello API de service de traitement par lots, vous pouvez conserver les données de la tâche sans modifier l’application hello par votre tâche. Vous pouvez respecter éventuellement toohello [standard de Conventions pour les fichiers par lots](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) de nommer les fichiers de hello qui vous rendre persistante tooAzure stockage. 

Utiliser la sortie lors de la tâche de toopersist hello API de service de traitement par lots :

- Vous souhaitez que les données de toopersist de tâches par lot et le gestionnaire tâches dans des pools créés avec la configuration d’ordinateur virtuel hello.
- Vous souhaitez que le conteneur de stockage Azure tooan toopersist données avec un nom quelconque.
- Vous souhaitez que le conteneur de stockage Azure toopersist données tooan nommé toohello conformément [standard de Conventions pour les fichiers Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). 

> [!NOTE]
> Hello API de service de traitement par lots ne prend pas en charge la persistance des données à partir de tâches qui s’exécutent dans des pools créés avec la configuration du service cloud hello. Pour plus d’informations sur la sortie à partir de pools de configuration des services cloud hello en cours d’exécution de tâche persistante, consultez [conserver les travaux et des tâches données tooAzure stockage avec bibliothèque de Conventions pour les fichiers Batch hello pour .NET toopersist](batch-task-output-file-conventions.md)
> 
> 

Pour plus d’informations sur la sortie de la tâche persistantes avec hello API de service de traitement par lots, consultez [conserver des tâches données tooAzure stockage avec hello API de lot](batch-task-output-files.md). Consultez également hello [PersistOutputs] [github_persistoutputs] exemple de projet sur GitHub, qui illustre comment toouse bibliothèque cliente de lot hello pour les tâches de toopersist .NET sortie toodurable stockage.

### <a name="use-hello-batch-file-conventions-library-for-net"></a>Utilisez la bibliothèque de Conventions pour les fichiers par lots de hello pour .NET

Les développeurs de la création de solutions de traitement par lots avec c# et .NET peuvent utiliser hello [bibliothèque Conventions pour les fichiers pour .NET] [ nuget_package] tooan de données de tâche toopersist compte de stockage Azure, en fonction de toohello [fichier de commandes Conventions standards](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). bibliothèque de Conventions pour les fichiers Hello gère mobile tooAzure de fichiers de sortie stockage et d’affectation de noms conteneurs de destination et les objets BLOB d’une façon bien connue.

Hello Conventions pour les fichiers bibliothèque prend en charge l’interrogation des fichiers de sortie par ID ou de fin, sans avoir besoin de hello rend facile toolocate terminer URI de fichier. 

Utiliser la bibliothèque hello Conventions pour les fichiers par lots pour les tâches de toopersist .NET lorsque la sortie :

- Vous souhaitez toostream données tooAzure stockage alors que la tâche hello est en cours d’exécution.
- Vous souhaitez que les données de toopersist à partir des pools créés avec la configuration du service cloud hello ou de configuration d’ordinateur virtuel hello.
- Votre application cliente ou autres tâches dans hello toolocate des besoins de la tâche et téléchargement les fichiers de sortie de tâche par ID ou de leur rôle. 
- Vous souhaitez tooperform un téléchargement pointant vers la vérification ou anticipée de résultats initiales.
- Vous souhaitez obtenir une sortie tâche tooview hello portail Azure.

Pour plus d’informations sur la sortie de la tâche persistantes avec la bibliothèque de Conventions pour les fichiers hello pour .NET, consultez [conserver les travaux et des tâches données tooAzure stockage avec bibliothèque de Conventions pour les fichiers Batch hello pour .NET toopersist ](batch-task-output-file-conventions.md). Consultez également hello [PersistOutputs] [github_persistoutputs] exemple de projet sur GitHub, qui illustre la manière dont la bibliothèque de Conventions pour les fichiers toouse hello pour les tâches de toopersist .NET sortie toodurable stockage.

Hello [PersistOutputs] [github_persistoutputs] exemple de projet sur GitHub montre comment toouse bibliothèque cliente de lot hello pour les tâches de toopersist .NET sortie toodurable stockage.

### <a name="implement-hello-batch-file-conventions-standard"></a>Implémenter hello Conventions pour les fichiers Batch standard

Si vous utilisez une langue autre que .NET, vous pouvez implémenter hello [standard de Conventions pour les fichiers Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) dans votre application. 

Vous souhaiterez tooimplement hello standard d’affectation de noms de fichier Conventions vous-même un schéma d’affectation de noms ayant fait leurs preuves, ou lorsque vous souhaitez que le résultat de la tâche tooview Bonjour portail Azure.

### <a name="implement-a-custom-file-movement-solution"></a>Implémenter une solution de déplacement de fichiers personnalisée

Vous pouvez aussi implémenter votre propre solution de déplacement de fichiers complète. Suivez cette approche dans les cas suivants :

- Vous souhaitez que le magasin de données tooa toopersist tâches données autre que le stockage Azure. tooupload fichiers tooa magasin de données SQL Azure ou Azure DataLake, vous pouvez créer un script personnalisé ou un emplacement de toothat tooupload exécutable. Vous pouvez ensuite l’appeler sur la ligne de commande hello après l’exécution de votre fichier exécutable principal. Par exemple, sur un nœud Windows, vous pouvez appeler ces deux commandes : `doMyWork.exe && uploadMyFilesToSql.exe`
- Vous souhaitez tooperform un téléchargement pointant vers la vérification ou anticipée de résultats initiales.
- Vous voulez toomaintain un contrôle granulaire sur la gestion des erreurs. Par exemple, vous souhaiterez peut-être tooimplement votre propre solution si vous souhaitez toouse tâche dépendance actions tootake certaines télécharger des actions en fonction des codes de sortie de tâche spécifique. Pour plus d’informations sur les actions de dépendance de tâche, consultez [toorun les tâches qui dépendent d’autres tâches de créer des interdépendances](batch-task-dependencies.md). 

## <a name="next-steps"></a>Étapes suivantes

- Explorez à l’aide des nouvelles fonctionnalités de hello dans les données de tâche toopersist hello API de service de traitement par lots dans [conserver des tâches données tooAzure stockage avec hello API de lot](batch-task-output-files.md).
- En savoir plus sur l’utilisation de la bibliothèque de Conventions pour les fichiers Batch hello pour .NET dans [conserver les travaux et des tâches données tooAzure stockage avec bibliothèque de Conventions pour les fichiers Batch hello pour .NET toopersist ](batch-task-output-file-conventions.md).
- Consultez hello [PersistOutputs] [github_persistoutputs] exemple de projet sur GitHub, qui illustre comment toouse les deux hello bibliothèque cliente de lot pour .NET et bibliothèque de Conventions pour les fichiers hello pour les tâches de toopersist .NET toodurable stockage de sortie.

[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/
