---
title: "Bibliothèques clientes requises pour la connexion à Azure Analysis Services | Microsoft Docs"
description: "Décrit les bibliothèques clientes requises pour que les applications clientes et les outils se connectent à Azure Analysis Services"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: a96e7fe671dc051da35168fa7b49ecba53b4c4a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="client-libraries-for-connecting-to-azure-analysis-services"></a><span data-ttu-id="12223-103">Bibliothèques clientes pour la connexion à Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="12223-103">Client libraries for connecting to Azure Analysis Services</span></span>

<span data-ttu-id="12223-104">Les bibliothèques clientes sont nécessaires pour que les applications clientes et les outils se connectent aux serveurs Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="12223-104">Client libraries are necessary for client applications and tools to connect to Analysis Services servers.</span></span> 

<span data-ttu-id="12223-105">Analysis Services utilise trois bibliothèques clientes.</span><span class="sxs-lookup"><span data-stu-id="12223-105">Analysis Services utilize three client libraries.</span></span> <span data-ttu-id="12223-106">ADOMD.NET et Analysis Services Management Objects (AMO) sont des bibliothèques clientes managées.</span><span class="sxs-lookup"><span data-stu-id="12223-106">ADOMD.NET and Analysis Services Management Objects (AMO), are managed client libraries.</span></span> <span data-ttu-id="12223-107">Le fournisseur OLE DB Analysis Services (MSOLAP DLL) est une bibliothèque cliente native.</span><span class="sxs-lookup"><span data-stu-id="12223-107">The Analysis Services OLE DB provider (MSOLAP DLL) is a native client library.</span></span> <span data-ttu-id="12223-108">En général, les trois bibliothèques sont installées en même temps.</span><span class="sxs-lookup"><span data-stu-id="12223-108">Typically, all three are installed at the same time.</span></span> <span data-ttu-id="12223-109">Azure Analysis Services nécessite les dernières versions.</span><span class="sxs-lookup"><span data-stu-id="12223-109">Azure Analysis Services requires the latest versions.</span></span> 

<span data-ttu-id="12223-110">Les applications clientes Microsoft telles que Power BI Desktop et Excel installent les trois bibliothèques clientes.</span><span class="sxs-lookup"><span data-stu-id="12223-110">Microsoft client applications such as Power BI Desktop and Excel install all three client libraries.</span></span> <span data-ttu-id="12223-111">Toutefois, selon la version ou la fréquence des mises à jour, les bibliothèques clientes peuvent ne pas être les dernières versions requises par Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="12223-111">However, depending on the version or frequency of updates, client libraries may not be the latest versions required by Azure Analysis Services.</span></span> <span data-ttu-id="12223-112">Il en va de même pour les applications personnalisées ou d’autres interfaces telles que AsCmd, TOM, ADOMD.NET.</span><span class="sxs-lookup"><span data-stu-id="12223-112">The same applies to custom applications or other interfaces such as AsCmd, TOM, ADOMD.NET.</span></span> <span data-ttu-id="12223-113">Ces applications nécessitent l’installation manuelle des bibliothèques.</span><span class="sxs-lookup"><span data-stu-id="12223-113">These applications require manually installing the libraries.</span></span> <span data-ttu-id="12223-114">Les bibliothèques clientes pour l’installation manuelle sont incluses dans les packs de fonctionnalités SQL Server sous forme de packages distribuables.</span><span class="sxs-lookup"><span data-stu-id="12223-114">The client libraries for manual installation are included in SQL Server feature packs as distributable packages.</span></span> <span data-ttu-id="12223-115">Toutefois, elles sont liées à la version de SQL Server et il se peut qu’elles ne soient pas à jour.</span><span class="sxs-lookup"><span data-stu-id="12223-115">However, these client libraries are tied to the SQL Server version and may not be the latest.</span></span>  

<span data-ttu-id="12223-116">Les bibliothèques clientes pour les connexions clientes sont différentes des fournisseurs de données requis pour connecter un serveur Azure Analysis Services à une source de données.</span><span class="sxs-lookup"><span data-stu-id="12223-116">Client libraries for client connections are different from data providers required to connect from an Azure Analysis Services server to a data source.</span></span> <span data-ttu-id="12223-117">Pour plus d’informations sur les connexions aux sources de données, consultez [Connexions de source de données](analysis-services-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="12223-117">To learn more about datasource connections, see [Datasource connections](analysis-services-datasource.md).</span></span>

## <a name="download-the-latest-client-libraries"></a><span data-ttu-id="12223-118">Télécharger les dernières bibliothèques clientes</span><span class="sxs-lookup"><span data-stu-id="12223-118">Download the latest client libraries</span></span>  
<span data-ttu-id="12223-119">Utilisez les bibliothèques clientes suivantes si vous êtes dans un environnement de production et avez besoin de versions entièrement publiées et prises en charge.</span><span class="sxs-lookup"><span data-stu-id="12223-119">Use the following client libraries if you are in a production environment and require fully released and supported versions.</span></span>

[<span data-ttu-id="12223-120">MSOLAP (amd64)</span><span class="sxs-lookup"><span data-stu-id="12223-120">MSOLAP (amd64)</span></span>](https://go.microsoft.com/fwlink/?linkid=829576)</br><span data-ttu-id="12223-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span><span class="sxs-lookup"><span data-stu-id="12223-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span></span></br><span data-ttu-id="12223-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span><span class="sxs-lookup"><span data-stu-id="12223-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span></span></br><span data-ttu-id="12223-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span><span class="sxs-lookup"><span data-stu-id="12223-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="12223-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="12223-124">Next steps</span></span>
<span data-ttu-id="12223-125">[Connexion avec Excel](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="12223-125">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
[<span data-ttu-id="12223-126">Connexion avec Power BI</span><span class="sxs-lookup"><span data-stu-id="12223-126">Connect with Power BI</span></span>](analysis-services-connect-pbi.md)
