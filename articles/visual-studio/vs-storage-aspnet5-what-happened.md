---
title: "Qu’est-il arrivé à mon projet ASP.NET 5 (services connectés de Visual Studio) ? | Microsoft Docs"
description: "Décrit ce qui se produit une fois que vous vous connectez à un compte de stockage Azure dans un projet Visual Studio ASP.NET 5 à l’aide des services connectés de Visual Studio"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: e7caa9fa-c780-45eb-a546-299fc1c68455
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 2a25c24fd7625374d269622a805f386fcd52bb5f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-aspnet-5-project-visual-studio-azure-storage-connected-services"></a><span data-ttu-id="1e9bb-103">Qu’est-il arrivé à mon projet ASP.NET 5 (services connectés Azure Storage de Visual Studio) ?</span><span class="sxs-lookup"><span data-stu-id="1e9bb-103">What happened to my ASP.NET 5 project (Visual Studio Azure Storage connected services)?</span></span>
## <a name="references-added"></a><span data-ttu-id="1e9bb-104">Références ajoutées</span><span class="sxs-lookup"><span data-stu-id="1e9bb-104">References added</span></span>
<span data-ttu-id="1e9bb-105">Le package NuGet Azure Storage a été ajouté à votre projet Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1e9bb-105">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="1e9bb-106">Ce package ajoute les références .NET suivantes :</span><span class="sxs-lookup"><span data-stu-id="1e9bb-106">This package adds the following .NET references:</span></span>

* <span data-ttu-id="1e9bb-107">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="1e9bb-107">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="1e9bb-108">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="1e9bb-108">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="1e9bb-109">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="1e9bb-109">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="1e9bb-110">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="1e9bb-110">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="1e9bb-111">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="1e9bb-111">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="1e9bb-112">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="1e9bb-112">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="1e9bb-113">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="1e9bb-113">**System.Data**</span></span>
* <span data-ttu-id="1e9bb-114">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="1e9bb-114">**System.Spatial**</span></span>

<span data-ttu-id="1e9bb-115">De plus, le package NuGet nommé **Microsoft.Framework.Configuration.Json** a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="1e9bb-115">Also, the NuGet package **Microsoft.Framework.Configuration.Json** was added.</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="1e9bb-116">Chaîne de connexion pour Azure Storage ajoutée</span><span class="sxs-lookup"><span data-stu-id="1e9bb-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="1e9bb-117">Dans le fichier config.json de votre projet, un élément a été créé avec la clé et la chaîne de connexion du compte de stockage sélectionné.</span><span class="sxs-lookup"><span data-stu-id="1e9bb-117">In the config.json file of your project, an element was created with the selected storage account's connection string and key.</span></span>

<span data-ttu-id="1e9bb-118">Pour plus d’informations, consultez [ASP.NET 5](http://www.asp.net/vnext).</span><span class="sxs-lookup"><span data-stu-id="1e9bb-118">For more information, see [ASP.NET 5](http://www.asp.net/vnext).</span></span>

