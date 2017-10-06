---
title: aaaConnect tooAzure Analysis Services avec Power BI | Documents Microsoft
description: "Découvrez comment tooconnect tooan Azure Analysis Services server à l’aide de Power BI."
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
ms.openlocfilehash: f6c4cdec6edb92900ad2e552e23a4d9172ba9b84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-power-bi"></a><span data-ttu-id="8f732-103">Se connecter avec Power BI</span><span class="sxs-lookup"><span data-stu-id="8f732-103">Connect with Power BI</span></span>

<span data-ttu-id="8f732-104">Une fois que vous avez créé un serveur dans Azure et déployé un modèle tabulaire de tooit, les utilisateurs de votre organisation sont tooconnect prêt et commencent à Explorer les données.</span><span class="sxs-lookup"><span data-stu-id="8f732-104">Once you've created a server in Azure, and deployed a tabular model tooit, users in your organization are ready tooconnect and begin exploring data.</span></span> 

> [!TIP]
> <span data-ttu-id="8f732-105">Être vraiment toouse hello version la plus récente de [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="8f732-105">Be sure toouse hello latest version of [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span></span>
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a><span data-ttu-id="8f732-106">Se connecter à Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="8f732-106">Connect in Power BI Desktop</span></span>

1. <span data-ttu-id="8f732-107">Dans Power BI Desktop, cliquez sur **Obtenir les données** > **Azure** > **Base de données Azure Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="8f732-107">In Power BI Desktop, click **Get Data** > **Azure** > **Azure Analysis Services database**.</span></span>

2. <span data-ttu-id="8f732-108">Dans **serveur**, entrez le nom du serveur hello.</span><span class="sxs-lookup"><span data-stu-id="8f732-108">In **Server**, enter hello server name.</span></span> 
    
    <span data-ttu-id="8f732-109">Être une URL complète que tooinclude hello.</span><span class="sxs-lookup"><span data-stu-id="8f732-109">Be sure tooinclude hello full URL.</span></span> <span data-ttu-id="8f732-110">Par exemple, asazure://westcentralus.asazure.windows.net/advworks.</span><span class="sxs-lookup"><span data-stu-id="8f732-110">For example, asazure://westcentralus.asazure.windows.net/advworks.</span></span>

3. <span data-ttu-id="8f732-111">Dans **base de données**, si vous connaissez le nom hello de base de données de modèle tabulaire hello ou perspective que vous souhaitez tooconnect à coller ici.</span><span class="sxs-lookup"><span data-stu-id="8f732-111">In **Database**, if you know hello name of hello tabular model database or perspective you want tooconnect to, paste it here.</span></span> <span data-ttu-id="8f732-112">Sinon, vous pouvez laisser ce champ vide et sélectionner une base de données ou une perspective ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="8f732-112">Otherwise, you can leave this field blank and select a database or perspective later.</span></span>

4. <span data-ttu-id="8f732-113">Laissez la valeur par défaut hello **connexion live** option, puis appuyez sur **Connect**.</span><span class="sxs-lookup"><span data-stu-id="8f732-113">Leave hello default **Connect live** option, then press **Connect**.</span></span> 

5. <span data-ttu-id="8f732-114">Entrez vos informations d’identification si elles vous sont demandées.</span><span class="sxs-lookup"><span data-stu-id="8f732-114">If prompted, enter your login credentials.</span></span> 

6. <span data-ttu-id="8f732-115">Dans **Navigator**, développez hello serveur, puis sélectionnez le modèle de hello ou une perspective vous souhaitez tooconnect, puis à cliquer sur **connexion**.</span><span class="sxs-lookup"><span data-stu-id="8f732-115">In **Navigator**, expand hello server, then select hello model or perspective you want tooconnect to, then click **Connect**.</span></span> <span data-ttu-id="8f732-116">Cliquez sur un tooshow de modèle ou de perspective de tous les objets hello pour cette vue.</span><span class="sxs-lookup"><span data-stu-id="8f732-116">Click  a model or perspective tooshow all hello objects for that view.</span></span>

    <span data-ttu-id="8f732-117">modèle de Hello s’ouvre dans Power BI Desktop avec un rapport vierge en mode rapport.</span><span class="sxs-lookup"><span data-stu-id="8f732-117">hello model opens in Power BI Desktop with a blank report in Report view.</span></span> <span data-ttu-id="8f732-118">liste de champs Hello affiche tous les objets de modèle de non masqués.</span><span class="sxs-lookup"><span data-stu-id="8f732-118">hello Fields list displays all non-hidden model objects.</span></span> <span data-ttu-id="8f732-119">État de la connexion s’affiche dans le coin inférieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="8f732-119">Connection status is displayed in hello lower-right corner.</span></span>

## <a name="connect-in-power-bi-service"></a><span data-ttu-id="8f732-120">Se connecter à Power BI Desktop (service)</span><span class="sxs-lookup"><span data-stu-id="8f732-120">Connect in Power BI (service)</span></span>

1. <span data-ttu-id="8f732-121">Créez un fichier Power BI Desktop qui dispose d’un modèle de tooyour de connexion active sur votre serveur.</span><span class="sxs-lookup"><span data-stu-id="8f732-121">Create a Power BI Desktop file that has a live connection tooyour model on your server.</span></span>
2. <span data-ttu-id="8f732-122">Dans [Power BI](https://powerbi.microsoft.com), cliquez sur **Obtenir les données** > **Fichiers**.</span><span class="sxs-lookup"><span data-stu-id="8f732-122">In [Power BI](https://powerbi.microsoft.com), click **Get Data** > **Files**.</span></span> <span data-ttu-id="8f732-123">Recherchez et sélectionnez votre fichier.</span><span class="sxs-lookup"><span data-stu-id="8f732-123">Locate and select your file.</span></span>



## <a name="see-also"></a><span data-ttu-id="8f732-124">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="8f732-124">See also</span></span>
<span data-ttu-id="8f732-125">[Se connecter tooAzure Analysis Services](analysis-services-connect.md) </span><span class="sxs-lookup"><span data-stu-id="8f732-125">[Connect tooAzure Analysis Services](analysis-services-connect.md) </span></span>  
[<span data-ttu-id="8f732-126">Fournisseurs de données pour la connexion à Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="8f732-126">Client libraries</span></span>](analysis-services-data-providers.md)

