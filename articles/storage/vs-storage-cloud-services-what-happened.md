---
title: "Qu’est-il arrivé à mon projet service cloud ? | Microsoft Docs"
description: "Décrit ce qui se produit dans un projet services cloud une fois que vous vous connectez à un compte de stockage Azure à l’aide des services connectés de Visual Studio"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: ca0ea68d-f417-4ce8-9413-40d76f69cdea
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 4e0d4864c2fad624fbde39080146dc62ebebff09
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="what-happened-to-my-cloud-services-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="f8a33-104">Qu’est-il arrivé à mon projet services cloud (service connecté Azure Storage de Visual Studio) ?</span><span class="sxs-lookup"><span data-stu-id="f8a33-104">What happened to my cloud services project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="f8a33-105">Références ajoutées</span><span class="sxs-lookup"><span data-stu-id="f8a33-105">References added</span></span>
<span data-ttu-id="f8a33-106">Le package NuGet Azure Storage a été ajouté à votre projet Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f8a33-106">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="f8a33-107">Ce package ajoute les références .NET suivantes :</span><span class="sxs-lookup"><span data-stu-id="f8a33-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="f8a33-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="f8a33-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="f8a33-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="f8a33-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="f8a33-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="f8a33-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="f8a33-111">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="f8a33-111">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="f8a33-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="f8a33-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="f8a33-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="f8a33-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="f8a33-114">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="f8a33-114">**System.Data**</span></span>
* <span data-ttu-id="f8a33-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="f8a33-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="f8a33-116">Chaîne de connexion pour Azure Storage ajoutée</span><span class="sxs-lookup"><span data-stu-id="f8a33-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="f8a33-117">Les éléments ont été créés avec la clé et la chaîne de connexion du compte de stockage sélectionné.</span><span class="sxs-lookup"><span data-stu-id="f8a33-117">Elements were created with the selected storage account's connection string and key.</span></span> <span data-ttu-id="f8a33-118">Des modifications ont été apportées aux fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="f8a33-118">Modifications were made to the following files:</span></span>

* <span data-ttu-id="f8a33-119">**ServiceDefinition.csdef**</span><span class="sxs-lookup"><span data-stu-id="f8a33-119">**ServiceDefinition.csdef**</span></span>
* <span data-ttu-id="f8a33-120">**ServiceConfiguration.Cloud.cscfg**</span><span class="sxs-lookup"><span data-stu-id="f8a33-120">**ServiceConfiguration.Cloud.cscfg**</span></span>
* <span data-ttu-id="f8a33-121">**ServiceConfiguration.Local.cscfg**</span><span class="sxs-lookup"><span data-stu-id="f8a33-121">**ServiceConfiguration.Local.cscfg**</span></span>

