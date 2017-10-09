---
title: "bibliothèques aaaClient requis pour la connexion tooAzure Analysis Services | Documents Microsoft"
description: "Décrit les bibliothèques clientes requises pour le client tooconnect outils et applications Azure Analysis Services"
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
ms.openlocfilehash: 74ba5c05ba76c6587c5aed38f200a1ba469aa4f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="client-libraries-for-connecting-tooazure-analysis-services"></a><span data-ttu-id="19e99-103">Bibliothèques clientes pour connecter tooAzure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="19e99-103">Client libraries for connecting tooAzure Analysis Services</span></span>

<span data-ttu-id="19e99-104">Les bibliothèques clientes sont nécessaires pour les applications clientes et les serveurs de Services outils tooconnect tooAnalysis.</span><span class="sxs-lookup"><span data-stu-id="19e99-104">Client libraries are necessary for client applications and tools tooconnect tooAnalysis Services servers.</span></span> 

<span data-ttu-id="19e99-105">Analysis Services utilise trois bibliothèques clientes.</span><span class="sxs-lookup"><span data-stu-id="19e99-105">Analysis Services utilize three client libraries.</span></span> <span data-ttu-id="19e99-106">ADOMD.NET et Analysis Services Management Objects (AMO) sont des bibliothèques clientes managées.</span><span class="sxs-lookup"><span data-stu-id="19e99-106">ADOMD.NET and Analysis Services Management Objects (AMO), are managed client libraries.</span></span> <span data-ttu-id="19e99-107">fournisseur OLE DB pour Analysis Services de Hello (DLL MSOLAP) est une bibliothèque cliente native.</span><span class="sxs-lookup"><span data-stu-id="19e99-107">hello Analysis Services OLE DB provider (MSOLAP DLL) is a native client library.</span></span> <span data-ttu-id="19e99-108">En règle générale, les trois sont installés à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="19e99-108">Typically, all three are installed at hello same time.</span></span> <span data-ttu-id="19e99-109">Azure Analysis Services nécessite les versions les plus récentes hello.</span><span class="sxs-lookup"><span data-stu-id="19e99-109">Azure Analysis Services requires hello latest versions.</span></span> 

<span data-ttu-id="19e99-110">Les applications clientes Microsoft telles que Power BI Desktop et Excel installent les trois bibliothèques clientes.</span><span class="sxs-lookup"><span data-stu-id="19e99-110">Microsoft client applications such as Power BI Desktop and Excel install all three client libraries.</span></span> <span data-ttu-id="19e99-111">Toutefois, selon la version de hello ou la fréquence des mises à jour, les bibliothèques clientes peut-être pas hello dernières versions requises par Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="19e99-111">However, depending on hello version or frequency of updates, client libraries may not be hello latest versions required by Azure Analysis Services.</span></span> <span data-ttu-id="19e99-112">Hello va de même toocustom applications ou autres interfaces telles que AsCmd, TOM, ADOMD.NET.</span><span class="sxs-lookup"><span data-stu-id="19e99-112">hello same applies toocustom applications or other interfaces such as AsCmd, TOM, ADOMD.NET.</span></span> <span data-ttu-id="19e99-113">Ces applications nécessitent l’installation manuelle des bibliothèques de hello.</span><span class="sxs-lookup"><span data-stu-id="19e99-113">These applications require manually installing hello libraries.</span></span> <span data-ttu-id="19e99-114">les bibliothèques clientes Hello pour l’installation manuelle sont inclus dans les packs de fonctionnalités de SQL Server en tant que packages distribuables.</span><span class="sxs-lookup"><span data-stu-id="19e99-114">hello client libraries for manual installation are included in SQL Server feature packs as distributable packages.</span></span> <span data-ttu-id="19e99-115">Toutefois, ces bibliothèques clientes sont la version de SQL Server liée toohello et ne peuvent pas être hello plus récentes.</span><span class="sxs-lookup"><span data-stu-id="19e99-115">However, these client libraries are tied toohello SQL Server version and may not be hello latest.</span></span>  

<span data-ttu-id="19e99-116">Les bibliothèques clientes pour les connexions client sont différentes des données fournisseurs tooconnect requis à partir d’une source de données Azure Analysis Services server tooa.</span><span class="sxs-lookup"><span data-stu-id="19e99-116">Client libraries for client connections are different from data providers required tooconnect from an Azure Analysis Services server tooa data source.</span></span> <span data-ttu-id="19e99-117">toolearn en savoir plus sur les connexions de source de données, consultez [des connexions de source de données](analysis-services-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="19e99-117">toolearn more about datasource connections, see [Datasource connections](analysis-services-datasource.md).</span></span>

## <a name="download-hello-latest-client-libraries"></a><span data-ttu-id="19e99-118">Télécharger les bibliothèques clientes plus récentes hello</span><span class="sxs-lookup"><span data-stu-id="19e99-118">Download hello latest client libraries</span></span>  
<span data-ttu-id="19e99-119">Utilisez hello suivant des bibliothèques clientes si vous êtes dans un environnement de production et que vous requièrent des versions entièrement publiées et pris en charge.</span><span class="sxs-lookup"><span data-stu-id="19e99-119">Use hello following client libraries if you are in a production environment and require fully released and supported versions.</span></span>

[<span data-ttu-id="19e99-120">MSOLAP (amd64)</span><span class="sxs-lookup"><span data-stu-id="19e99-120">MSOLAP (amd64)</span></span>](https://go.microsoft.com/fwlink/?linkid=829576)</br><span data-ttu-id="19e99-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span><span class="sxs-lookup"><span data-stu-id="19e99-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span></span></br><span data-ttu-id="19e99-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span><span class="sxs-lookup"><span data-stu-id="19e99-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span></span></br><span data-ttu-id="19e99-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span><span class="sxs-lookup"><span data-stu-id="19e99-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="19e99-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="19e99-124">Next steps</span></span>
<span data-ttu-id="19e99-125">[Connexion avec Excel](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="19e99-125">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
[<span data-ttu-id="19e99-126">Connexion avec Power BI</span><span class="sxs-lookup"><span data-stu-id="19e99-126">Connect with Power BI</span></span>](analysis-services-connect-pbi.md)
