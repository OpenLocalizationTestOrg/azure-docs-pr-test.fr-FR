---
title: "aaaUse outils et API de traitement par lots Azure toodevelop à grande échelle le traitement parallèle solutions | Documents Microsoft"
description: "Découvrez hello API et les outils disponibles pour développer des solutions avec le service de traitement par lots Azure hello."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: tamram
ms.openlocfilehash: ca75a1a63b3e7e6b0805e79a63685bc49aaaca8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-batch-apis-and-tools"></a>Vue d’ensemble des outils et API Batch

Le traitement des charges de travail parallèles dans Azure Batch est généralement effectué par programme en utilisant l’une des hello [API de lot](#batch-development-apis). Votre application cliente ou le service peut utiliser des hello API de lot toocommunicate avec hello service Batch. Avec hello API de lot, vous pouvez créer et gérer les pools de nœuds de calcul, machines virtuelles ou services de cloud computing. Vous pouvez ensuite planifier des travaux et des tâches toorun sur ces nœuds. 

Vous pouvez efficacement traiter les charges de travail à grande échelle pour votre organisation, ou fournir un serveur frontal service tooyour clients afin qu’ils peuvent exécutés travaux et des tâches, à la demande ou selon une planification--sur un, des centaines ou milliers de nœuds. Vous pouvez également utiliser Azure Batch dans le cadre d’un plus grand workflow géré par des outils comme [Azure Data Factory](../data-factory/data-factory-data-processing-using-batch.md?toc=%2fazure%2fbatch%2ftoc.json).

> [!TIP]
> Lorsque vous êtes prêt toodig dans toohello API de lot pour une compréhension plus approfondie de hello fonctionnalités qu’il fournit, consultez hello [vue d’ensemble de lot pour les développeurs](batch-api-basics.md).
> 
> 

## <a name="azure-accounts-for-batch-development"></a>Comptes Azure pour le développement de Batch
Lorsque vous développez des solutions de lot, vous allez utiliser hello suivant des comptes dans Microsoft Azure.

* **Compte et abonnement Azure** : si vous ne possédez pas encore d’abonnement Azure, vous pouvez activer les [avantages de votre abonnement MSDN][msdn_benefits] ou vous inscrire pour obtenir un [compte Azure gratuit][free_account]. Lorsque vous créez un compte, un abonnement par défaut est automatiquement créé.
* **Compte Batch** : les ressources Azure Batch, notamment les pools, les nœuds de calcul, les travaux et les tâches, sont associées à un compte Azure Batch. Lorsque votre application effectue une demande de hello service Batch, il authentifie la demande hello à l’aide du nom du compte Azure Batch hello, l’URL de hello du compte de hello et une clé d’accès. Vous pouvez [création du compte Batch](batch-account-create-portal.md) Bonjour portail Azure.
* **Compte de stockage** : Batch inclut la prise en charge intégrée de l’utilisation des fichiers dans [Azure Storage][azure_storage]. Presque tous les scénarios de traitement par lots utilise le stockage Blob Azure pour la mise en lots programmes hello qui exécutent des tâches et qu’ils traitent les données de salutation et pour le stockage de données de sortie qu’ils génèrent hello. toocreate un compte de stockage, consultez [comptes de stockage sur Azure](../storage/common/storage-create-storage-account.md).

## <a name="batch-service-apis"></a>API du service Batch

Vos applications et services peuvent émettre des appels d’API REST directs ou utiliser une ou plusieurs des hello suivant toorun de bibliothèques de client et de gérer vos charges de travail de traitement par lots Azure.

| API | Informations de référence sur l'API | Télécharger | Didacticiel | Exemples de code | En savoir plus |
| --- | --- | --- | --- | --- | --- |
| **Batch REST** |[MSDN][batch_rest] |N/A |- |- | [Versions prises en charge](https://docs.microsoft.com/rest/api/batchservice/batch-service-rest-api-versioning) |
| **Batch .NET** |[docs.microsoft.com][api_net] |[NuGet ][api_net_nuget] |[Didacticiel](batch-dotnet-get-started.md) |[GitHub][api_sample_net] | [Notes de publication](http://aka.ms/batch-net-dataplane-changelog) |
| **Python Batch** |[readthedocs.io][api_python] |[PyPI][api_python_pypi] |[Didacticiel](batch-python-tutorial.md)|[GitHub][api_sample_python] | [Lisez-moi](https://github.com/Azure/azure-sdk-for-python/blob/master/doc/batch.rst) |
| **Batch Node.js** |[github.io][api_nodejs] |[npm][api_nodejs_npm] |- |- | [Lisez-moi](https://github.com/Azure/azure-sdk-for-node/tree/master/lib/services/batch) |
| **Java Batch** |[github.io][api_java] |[Maven][api_java_jar] |- |[Lisez-moi][api_sample_java] | [Lisez-moi](https://github.com/Azure/azure-batch-sdk-for-java)|

## <a name="batch-management-apis"></a>API de Batch Management

Hello API du Gestionnaire de ressources Azure pour le traitement par lots fournissent un accès par programmation tooBatch comptes. À l’aide de ces API, vous pouvez gérer par programme les comptes Batch, les quotas et les packages d’applications.  

| API | Informations de référence sur l'API | Télécharger | Didacticiel | Exemples de code |
| --- | --- | --- | --- | --- |
| **REST Batch Resource Manager** |[docs.microsoft.com][api_rest_mgmt] |N/A |- |[GitHub](https://github.com/Azure-Samples/batch-dotnet-manage-batch-accounts) |
| **.NET Batch Resource Manager** |[docs.microsoft.com][api_net_mgmt] |[NuGet ][api_net_mgmt_nuget] | [Didacticiel](batch-management-dotnet.md) |[GitHub][api_sample_net] |

## <a name="batch-command-line-tools"></a>Outils en ligne de commande Batch

Ces outils de ligne de commande fournissent hello même fonctionnalité que hello service Batch et API de gestion de lot : 

* [Applets de commande PowerShell du lot][batch_ps]: hello applets de commande de traitement par lots Azure Bonjour [Azure PowerShell](/powershell/azure/overview) module vous activer toomanage des ressources de traitement par lots avec PowerShell.
* [CLI Azure](/cli/azure/overview): hello Azure Interface de ligne (Azure) est un ensemble d’outils multiplateformes qui fournit des commandes shell pour interagir avec plusieurs services Azure, y compris le service de traitement par lots hello et le service de gestion par lots. Consultez [des ressources de traitement par lots de gérer avec CLI d’Azure](batch-cli-get-started.md) pour plus d’informations sur l’utilisation de hello CLI d’Azure avec le lot.

## <a name="other-tools-for-application-development"></a>Autres outils pour le développement d’applications

Voici quelques outils supplémentaires qui peuvent être utiles pour générer et déboguer vos applications et services Batch :

* [Portail Azure][portal]: vous pouvez créer, surveiller et supprimer les pools par lots, les travaux et les tâches Bonjour Azure panneaux de lot du portail. Vous pouvez afficher des informations d’état hello pour celles-ci et d’autres ressources pendant que vous exécutez vos tâches et même Téléchargez des fichiers à partir des nœuds de calcul hello dans les pools. Par exemple, vous pouvez télécharger une tâche ayant échoué `stderr.txt` lors de la résolution des problèmes. Vous pouvez également télécharger les fichiers Bureau à distance (RDP) que vous pouvez utiliser toolog dans toocompute nœuds.
* [L’Explorateur de traitement par lots Azure][batch_explorer]: Explorateur de lot offre une fonctionnalité d’administration de ressource lot similaire hello portail Azure, mais dans une application cliente de Windows Presentation Foundation (WPF) autonome. Une des applications d’exemple hello Batch .NET disponibles sur [GitHub][github_samples], vous pouvez créer avec Visual Studio 2015 ou version ultérieure et toobrowse l’utiliser et gérer les ressources de hello dans votre compte de traitement par lots lors du développement et déboguer vos solutions de traitement par lots. Afficher le travail, le pool et détails de la tâche, téléchargent des fichiers à partir des nœuds de calcul et vous connecter toonodes à distance à l’aide de fichiers RDP (Remote Desktop) que vous pouvez télécharger avec l’Explorateur de lot.
* [Microsoft Azure Storage Explorer][storage_explorer]: lors pas strictement d’un outil de traitement par lots Azure, hello Explorateur de stockage est un autre outil précieux toohave pendant que vous développez et débogage de solutions de votre lot.

## <a name="additional-resources"></a>Ressources supplémentaires

- toolearn sur les événements de journalisation à partir de votre application de traitement par lots, consultez [journaliser les événements de diagnostic d’évaluation et la surveillance des solutions de lot](batch-diagnostics.md). Pour des informations sur les événements déclenchés par hello service Batch, consultez [lot Analytique](batch-analytics.md).
- Pour plus d’informations sur les variables d’environnement des nœuds de calcul, consultez [Variables d’environnement de nœud de calcul Azure Batch](batch-compute-node-environment-variables.md).

## <a name="next-steps"></a>Étapes suivantes

* Hello de lecture [vue d’ensemble de lot pour les développeurs](batch-api-basics.md), des informations essentielles pour toute personne préparation toouse lot. Hello contient des informations détaillées sur les ressources du service de traitement par lots comme pools, nœuds, travaux, tâches et des hello nombreuses fonctionnalités de l’API que vous pouvez utiliser lors de la génération de votre application de traitement par lots.
* [Démarrer avec la bibliothèque de traitement par lots Azure hello pour .NET](batch-dotnet-get-started.md) toolearn comment toouse c# et hello Batch .NET bibliothèque tooexecute une charge de travail simple à l’aide d’un flux de travail courant de lot. Cet article doit être votre première arrête lorsque vous apprenez comment toouse hello service Batch. Il existe également un [version Python](batch-python-tutorial.md) du didacticiel de hello.
* Télécharger hello [code des exemples sur GitHub] [ github_samples] toosee comment c# et Python pouvant communiquer avec le lot tooschedule et processus exemple les charges de travail.
* Extraire hello [lot cursus] [ learning_path] tooget une idée de tooyou disponible de ressources hello en tant que vous découvrez toowork traitement par lots.


[azure_storage]: https://azure.microsoft.com/services/storage/
[api_java]: http://azure.github.io/azure-sdk-for-java/
[api_java_jar]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-batch%22
[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_nuget]: https://www.nuget.org/packages/Azure.Batch/
[api_rest_mgmt]: https://docs.microsoft.com/\rest/api/batchmanagement/
[api_net_mgmt]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[api_net_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[api_nodejs]: http://azure.github.io/azure-sdk-for-node/azure-batch/latest/
[api_nodejs_npm]: https://www.npmjs.com/package/azure-batch
[api_python]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html
[api_python_pypi]: https://pypi.python.org/pypi/azure-batch
[api_sample_net]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp
[api_sample_python]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch
[api_sample_java]: https://github.com/Azure/azure-batch-samples/tree/master/Java/
[batch_ps]: /powershell/resourcemanager/azurerm.batch/v2.7.0/azurerm.batch
[batch_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx
[free_account]: https://azure.microsoft.com/free/
[github_samples]: https://github.com/Azure/azure-batch-samples
[learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[msdn_benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[storage_explorer]: http://storageexplorer.com/
[portal]: https://portal.azure.com
