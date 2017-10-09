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
# <a name="move-data-tooand-from-azure-blob-storage"></a><span data-ttu-id="9f4d0-103">Déplacer les données tooand à partir du stockage d’objets Blob Azure</span><span class="sxs-lookup"><span data-stu-id="9f4d0-103">Move data tooand from Azure Blob Storage</span></span>
[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this tooseparate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

<span data-ttu-id="9f4d0-104">La méthode la mieux adaptée à vos besoins dépend de votre scénario.</span><span class="sxs-lookup"><span data-stu-id="9f4d0-104">Which method is best for you depends on your scenario.</span></span> <span data-ttu-id="9f4d0-105">Hello [scénarios d’analytique avancée dans Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) article vous aide à déterminer les ressources hello nécessaires pour une variété de workflows de science des données utilisées dans hello avancé du processus de l’analytique.</span><span class="sxs-lookup"><span data-stu-id="9f4d0-105">hello [Scenarios for advanced analytics in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) article helps you determine hello resources you need for a variety of data science workflows used in hello advanced analytics process.</span></span>

> [!NOTE]
> <span data-ttu-id="9f4d0-106">Pour un stockage d’objets blob tooAzure présentation complète, consultez trop[principes de base Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) et trop[Service d’objets Blob Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="9f4d0-106">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

<span data-ttu-id="9f4d0-107">Comme alternative, vous pouvez utiliser [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) pour :</span><span class="sxs-lookup"><span data-stu-id="9f4d0-107">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to:</span></span> 

* <span data-ttu-id="9f4d0-108">créer et planifier un pipeline qui télécharge les données à partir du stockage d’objets blob Azure,</span><span class="sxs-lookup"><span data-stu-id="9f4d0-108">create and schedule a pipeline that downloads data from Azure blob storage,</span></span> 
* <span data-ttu-id="9f4d0-109">Passez-le tooa publié le service web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9f4d0-109">pass it tooa published Azure Machine Learning web service,</span></span> 
* <span data-ttu-id="9f4d0-110">obtenir des résultats analytique prédictive hello et</span><span class="sxs-lookup"><span data-stu-id="9f4d0-110">receive hello predictive analytics results, and</span></span> 
* <span data-ttu-id="9f4d0-111">Téléchargez hello résultats toostorage.</span><span class="sxs-lookup"><span data-stu-id="9f4d0-111">upload hello results toostorage.</span></span> 

<span data-ttu-id="9f4d0-112">Pour plus d’informations, consultez la page [Créer des pipelines prédictifs à l’aide d’Azure Data Factory et Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="9f4d0-112">For more information, see [Create predictive pipelines using Azure Data Factory and Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f4d0-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9f4d0-113">Prerequisites</span></span>
<span data-ttu-id="9f4d0-114">Ce document suppose que vous disposez d’un abonnement Azure, un compte de stockage et la clé de stockage correspondante hello pour ce compte.</span><span class="sxs-lookup"><span data-stu-id="9f4d0-114">This document assumes that you have an Azure subscription, a storage account, and hello corresponding storage key for that account.</span></span> <span data-ttu-id="9f4d0-115">Avant de charger ou télécharger des données, vous devez connaître le nom et la clé de votre compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="9f4d0-115">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="9f4d0-116">tooset d’un abonnement Azure, consultez [version d’évaluation d’un mois gratuite](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9f4d0-116">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="9f4d0-117">Pour obtenir des instructions sur la création d’un compte de stockage, ainsi que des informations sur le compte et la clé, consultez [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="9f4d0-117">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

