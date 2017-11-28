---
title: "Déplacer des données vers et depuis un stockage Azure Blob | Microsoft Docs"
description: "Déplacer des données vers et depuis un stockage Azure Blob"
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
ms.openlocfilehash: d9a626cccd3cdfcdc85f000bd3192aef2881e9a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-and-from-azure-blob-storage"></a><span data-ttu-id="7f538-103">Déplacer des données vers et depuis Stockage Blob Azure</span><span class="sxs-lookup"><span data-stu-id="7f538-103">Move data to and from Azure Blob Storage</span></span>
[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this to separate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

<span data-ttu-id="7f538-104">La méthode la mieux adaptée à vos besoins dépend de votre scénario.</span><span class="sxs-lookup"><span data-stu-id="7f538-104">Which method is best for you depends on your scenario.</span></span> <span data-ttu-id="7f538-105">L’article sur les [Scénarios d’analyses avancées dans Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) vous aide à déterminer les ressources dont vous avez besoin pour les différents flux de travail utilisés dans le processus d’analyse avancée.</span><span class="sxs-lookup"><span data-stu-id="7f538-105">The [Scenarios for advanced analytics in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) article helps you determine the resources you need for a variety of data science workflows used in the advanced analytics process.</span></span>

> [!NOTE]
> <span data-ttu-id="7f538-106">Pour une présentation complète du stockage d’objets blob Azure, consultez les articles [Fonctionnalités de base des objets blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) et [Service Blob Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f538-106">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

<span data-ttu-id="7f538-107">Comme alternative, vous pouvez utiliser [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) pour :</span><span class="sxs-lookup"><span data-stu-id="7f538-107">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to:</span></span> 

* <span data-ttu-id="7f538-108">créer et planifier un pipeline qui télécharge les données à partir du stockage d’objets blob Azure,</span><span class="sxs-lookup"><span data-stu-id="7f538-108">create and schedule a pipeline that downloads data from Azure blob storage,</span></span> 
* <span data-ttu-id="7f538-109">transférer ces données vers un service web Azure Machine Learning publié,</span><span class="sxs-lookup"><span data-stu-id="7f538-109">pass it to a published Azure Machine Learning web service,</span></span> 
* <span data-ttu-id="7f538-110">recevoir les résultats d’analyse prédictifs, et</span><span class="sxs-lookup"><span data-stu-id="7f538-110">receive the predictive analytics results, and</span></span> 
* <span data-ttu-id="7f538-111">télécharger les résultats dans le stockage.</span><span class="sxs-lookup"><span data-stu-id="7f538-111">upload the results to storage.</span></span> 

<span data-ttu-id="7f538-112">Pour plus d’informations, consultez la page [Créer des pipelines prédictifs à l’aide d’Azure Data Factory et Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="7f538-112">For more information, see [Create predictive pipelines using Azure Data Factory and Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f538-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7f538-113">Prerequisites</span></span>
<span data-ttu-id="7f538-114">Ce document suppose que vous disposez d’un abonnement Azure, d’un compte de stockage et de la clé de stockage correspondante pour ce compte.</span><span class="sxs-lookup"><span data-stu-id="7f538-114">This document assumes that you have an Azure subscription, a storage account, and the corresponding storage key for that account.</span></span> <span data-ttu-id="7f538-115">Avant de charger ou télécharger des données, vous devez connaître le nom et la clé de votre compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="7f538-115">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="7f538-116">Pour configurer un abonnement Azure, consultez [Essai gratuit pendant un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7f538-116">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="7f538-117">Pour obtenir des instructions sur la création d’un compte de stockage et pour obtenir des informations de compte et de clé, consultez [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="7f538-117">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

