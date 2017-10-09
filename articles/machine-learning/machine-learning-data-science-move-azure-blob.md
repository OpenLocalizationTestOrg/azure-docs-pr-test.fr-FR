---
title: "tooand de données aaaMove à partir du stockage d’objets Blob Azure | Documents Microsoft"
description: "Déplacer les données tooand à partir du stockage d’objets Blob Azure"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d6681e30-ab45-45ea-a9fb-ac8acefe544d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;sachouks
ms.openlocfilehash: e12b8c157955195e826f8b108075afaf25ca7bd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage"></a>Déplacer les données tooand à partir du stockage d’objets Blob Azure
[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this tooseparate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

La méthode la mieux adaptée à vos besoins dépend de votre scénario. Hello [scénarios d’analytique avancée dans Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) article vous aide à déterminer les ressources hello nécessaires pour une variété de workflows de science des données utilisées dans hello avancé du processus de l’analytique.

> [!NOTE]
> Pour un stockage d’objets blob tooAzure présentation complète, consultez trop[principes de base Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) et trop[Service d’objets Blob Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

Comme alternative, vous pouvez utiliser [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) pour : 

* créer et planifier un pipeline qui télécharge les données à partir du stockage d’objets blob Azure, 
* Passez-le tooa publié le service web Azure Machine Learning 
* obtenir des résultats analytique prédictive hello et 
* Téléchargez hello résultats toostorage. 

Pour plus d’informations, consultez la page [Créer des pipelines prédictifs à l’aide d’Azure Data Factory et Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).

## <a name="prerequisites"></a>Composants requis
Ce document suppose que vous disposez d’un abonnement Azure, un compte de stockage et la clé de stockage correspondante hello pour ce compte. Avant de charger ou télécharger des données, vous devez connaître le nom et la clé de votre compte Azure Storage.

* tooset d’un abonnement Azure, consultez [version d’évaluation d’un mois gratuite](https://azure.microsoft.com/pricing/free-trial/).
* Pour obtenir des instructions sur la création d’un compte de stockage, ainsi que des informations sur le compte et la clé, consultez [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md).

