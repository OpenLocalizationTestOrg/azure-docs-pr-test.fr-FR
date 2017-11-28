---
title: "Qu’est-il arrivé à mon projet de tâche web (service connecté Azure Storage de Visual Studio) ? | Microsoft Docs"
description: "Décrit ce qui s’est produit dans un projet de tâche web une fois que vous vous connectez à un compte de stockage à l’aide des services connectés de Visual Studio"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 36ae7ff7-c22c-47eb-b220-049d61618c74
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 8891685a99c5ba366b74af0a21396d4a5e499835
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-webjob-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="78f4c-104">Qu’est-il arrivé à mon projet de tâche web (service connecté Azure Storage de Visual Studio) ?</span><span class="sxs-lookup"><span data-stu-id="78f4c-104">What happened to my WebJob project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="78f4c-105">Références ajoutées</span><span class="sxs-lookup"><span data-stu-id="78f4c-105">References Added</span></span>
<span data-ttu-id="78f4c-106">Le package NuGet Azure Storage a été ajouté ou mis à jour dans votre projet Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="78f4c-106">The Azure Storage NuGet package was added to or updated in your Visual Studio project.</span></span>  
<span data-ttu-id="78f4c-107">Ce package ajoute les références .NET suivantes :</span><span class="sxs-lookup"><span data-stu-id="78f4c-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="78f4c-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="78f4c-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="78f4c-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="78f4c-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="78f4c-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="78f4c-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="78f4c-111">**Microsoft.WindowsAzure.ConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="78f4c-111">**Microsoft.WindowsAzure.ConfigurationManager**</span></span>
* <span data-ttu-id="78f4c-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="78f4c-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="78f4c-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="78f4c-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="78f4c-114">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="78f4c-114">**System.Data**</span></span>
* <span data-ttu-id="78f4c-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="78f4c-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="78f4c-116">Chaîne de connexion pour Azure Storage ajoutée</span><span class="sxs-lookup"><span data-stu-id="78f4c-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="78f4c-117">Dans le fichier App.config de votre projet, les entrées **AzureWebJobsStorage** et **AzureWebJobsDashboard** ont été mises à jour avec la chaîne de connexion et la clé du compte de stockage sélectionné.</span><span class="sxs-lookup"><span data-stu-id="78f4c-117">In the App.config file of your project, the **AzureWebJobsStorage** and **AzureWebJobsDashboard** entries were updated with the selected storage account's connection string and key.</span></span>

<span data-ttu-id="78f4c-118">Pour plus d’informations, consultez [Ressources de documentation relatives à Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="78f4c-118">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

