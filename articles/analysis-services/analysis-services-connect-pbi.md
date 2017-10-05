---
title: "Se connecter à Azure Analysis Services avec Power BI | Microsoft Docs"
description: "Découvrez comment vous connecter à un serveur Azure Analysis Services à l’aide de Power BI."
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
ms.openlocfilehash: 3a2af043feddb4a1d6d63f50e838c8a39035449f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-with-power-bi"></a><span data-ttu-id="eda9a-103">Se connecter avec Power BI</span><span class="sxs-lookup"><span data-stu-id="eda9a-103">Connect with Power BI</span></span>

<span data-ttu-id="eda9a-104">Une fois que vous avez créé un serveur dans Azure avant d’y déployer un modèle tabulaire, les utilisateurs de votre entreprise sont prêts à s’y connecter et à explorer les données.</span><span class="sxs-lookup"><span data-stu-id="eda9a-104">Once you've created a server in Azure, and deployed a tabular model to it, users in your organization are ready to connect and begin exploring data.</span></span> 

> [!TIP]
> <span data-ttu-id="eda9a-105">Assurez-vous d’utiliser la dernière version de [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="eda9a-105">Be sure to use the latest version of [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span></span>
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a><span data-ttu-id="eda9a-106">Se connecter à Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="eda9a-106">Connect in Power BI Desktop</span></span>

1. <span data-ttu-id="eda9a-107">Dans Power BI Desktop, cliquez sur **Obtenir les données** > **Azure** > **Base de données Azure Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="eda9a-107">In Power BI Desktop, click **Get Data** > **Azure** > **Azure Analysis Services database**.</span></span>

2. <span data-ttu-id="eda9a-108">Dans **Serveur**, entrez le nom du serveur.</span><span class="sxs-lookup"><span data-stu-id="eda9a-108">In **Server**, enter the server name.</span></span> 
    
    <span data-ttu-id="eda9a-109">Veillez à inclure l’URL complète.</span><span class="sxs-lookup"><span data-stu-id="eda9a-109">Be sure to include the full URL.</span></span> <span data-ttu-id="eda9a-110">Par exemple, asazure://westcentralus.asazure.windows.net/advworks.</span><span class="sxs-lookup"><span data-stu-id="eda9a-110">For example, asazure://westcentralus.asazure.windows.net/advworks.</span></span>

3. <span data-ttu-id="eda9a-111">Dans **Base de données**, si vous connaissez le nom de la base de données de modèle tabulaire ou de la perspective à laquelle vous souhaitez vous connecter, collez-le ici.</span><span class="sxs-lookup"><span data-stu-id="eda9a-111">In **Database**, if you know the name of the tabular model database or perspective you want to connect to, paste it here.</span></span> <span data-ttu-id="eda9a-112">Sinon, vous pouvez laisser ce champ vide et sélectionner une base de données ou une perspective ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="eda9a-112">Otherwise, you can leave this field blank and select a database or perspective later.</span></span>

4. <span data-ttu-id="eda9a-113">Laissez l’option par défaut **Connexion active** sélectionnée, puis appuyez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="eda9a-113">Leave the default **Connect live** option, then press **Connect**.</span></span> 

5. <span data-ttu-id="eda9a-114">Entrez vos informations d’identification si elles vous sont demandées.</span><span class="sxs-lookup"><span data-stu-id="eda9a-114">If prompted, enter your login credentials.</span></span> 

6. <span data-ttu-id="eda9a-115">Dans le **Navigateur**, développez le serveur, puis sélectionnez le modèle ou la perspective auquel vous souhaitez vous connecter, puis cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="eda9a-115">In **Navigator**, expand the server, then select the model or perspective you want to connect to, then click **Connect**.</span></span> <span data-ttu-id="eda9a-116">Cliquez sur un modèle ou une perspective pour afficher tous les objets de cette vue.</span><span class="sxs-lookup"><span data-stu-id="eda9a-116">Click  a model or perspective to show all the objects for that view.</span></span>

    <span data-ttu-id="eda9a-117">Le modèle s’ouvre dans Power BI Desktop avec un rapport vierge dans l’affichage Rapport.</span><span class="sxs-lookup"><span data-stu-id="eda9a-117">The model opens in Power BI Desktop with a blank report in Report view.</span></span> <span data-ttu-id="eda9a-118">La liste Champs affiche tous les objets du modèle qui ne sont pas cachés.</span><span class="sxs-lookup"><span data-stu-id="eda9a-118">The Fields list displays all non-hidden model objects.</span></span> <span data-ttu-id="eda9a-119">L’état de la connexion se trouve dans le coin inférieur droit.</span><span class="sxs-lookup"><span data-stu-id="eda9a-119">Connection status is displayed in the lower-right corner.</span></span>

## <a name="connect-in-power-bi-service"></a><span data-ttu-id="eda9a-120">Se connecter à Power BI Desktop (service)</span><span class="sxs-lookup"><span data-stu-id="eda9a-120">Connect in Power BI (service)</span></span>

1. <span data-ttu-id="eda9a-121">Créez un fichier Power BI Desktop qui inclut une connexion active à votre modèle sur votre serveur.</span><span class="sxs-lookup"><span data-stu-id="eda9a-121">Create a Power BI Desktop file that has a live connection to your model on your server.</span></span>
2. <span data-ttu-id="eda9a-122">Dans [Power BI](https://powerbi.microsoft.com), cliquez sur **Obtenir les données** > **Fichiers**.</span><span class="sxs-lookup"><span data-stu-id="eda9a-122">In [Power BI](https://powerbi.microsoft.com), click **Get Data** > **Files**.</span></span> <span data-ttu-id="eda9a-123">Recherchez et sélectionnez votre fichier.</span><span class="sxs-lookup"><span data-stu-id="eda9a-123">Locate and select your file.</span></span>



## <a name="see-also"></a><span data-ttu-id="eda9a-124">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="eda9a-124">See also</span></span>
<span data-ttu-id="eda9a-125">[Connect to an Azure Analysis Services server](analysis-services-connect.md)  (Se connecter à un serveur Azure Analysis Services)</span><span class="sxs-lookup"><span data-stu-id="eda9a-125">[Connect to Azure Analysis Services](analysis-services-connect.md) </span></span>  
[<span data-ttu-id="eda9a-126">Fournisseurs de données pour la connexion à Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="eda9a-126">Client libraries</span></span>](analysis-services-data-providers.md)

