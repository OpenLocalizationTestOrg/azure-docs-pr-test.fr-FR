---
title: "Procéder à un déploiement sur Azure Analysis Services à l’aide de SSDT | Microsoft Docs"
description: "Découvrez comment déployer un modèle tabulaire sur un serveur Azure Analysis Services à l’aide de SSDT."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 5f1f0ae7-11de-4923-a3da-888b13a3638c
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: e9a3aedfb6e55696e1525e226fada1062fd5eda8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-model-from-ssdt"></a><span data-ttu-id="67ace-103">Déployer un modèle à partir de SSDT</span><span class="sxs-lookup"><span data-stu-id="67ace-103">Deploy a model from SSDT</span></span>
<span data-ttu-id="67ace-104">Une fois que vous avez créé un serveur dans votre abonnement Azure, vous êtes prêt à déployer une base de données de modèle tabulaire sur celui-ci.</span><span class="sxs-lookup"><span data-stu-id="67ace-104">Once you've created a server in your Azure subscription, you're ready to deploy a tabular model database to it.</span></span> <span data-ttu-id="67ace-105">Vous pouvez utiliser SQL Server Data Tools (SSDT) pour créer et déployer un projet de modèle tabulaire sur lequel vous travaillez.</span><span class="sxs-lookup"><span data-stu-id="67ace-105">You can use SQL Server Data Tools (SSDT) to build and deploy a tabular model project you're working on.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="67ace-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="67ace-106">Prerequisites</span></span>
<span data-ttu-id="67ace-107">Pour commencer, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="67ace-107">To get started, you need:</span></span>

* <span data-ttu-id="67ace-108">**Serveur Analysis Services** dans Azure.</span><span class="sxs-lookup"><span data-stu-id="67ace-108">**Analysis Services server** in Azure.</span></span> <span data-ttu-id="67ace-109">Pour plus d’informations, consultez l’article [Création d’un serveur Azure Analysis Services dans le portail Azure](analysis-services-create-server.md).</span><span class="sxs-lookup"><span data-stu-id="67ace-109">To learn more, see [Create an Azure Analysis Services server](analysis-services-create-server.md).</span></span>
* <span data-ttu-id="67ace-110">**Projet de modèle tabulaire** dans SSDT ou modèle tabulaire existant au niveau de compatibilité 1200 ou supérieur.</span><span class="sxs-lookup"><span data-stu-id="67ace-110">**Tabular model project** in SSDT or an existing tabular model at the 1200 or higher compatibility level.</span></span> <span data-ttu-id="67ace-111">Vous ne l’avez jamais fait ?</span><span class="sxs-lookup"><span data-stu-id="67ace-111">Never created one?</span></span> <span data-ttu-id="67ace-112">Essayez le [Didacticiel de modélisation tabulaire des ventes Internet Adventure Works](https://msdn.microsoft.com/library/hh231691.aspx).</span><span class="sxs-lookup"><span data-stu-id="67ace-112">Try the [Adventure Works Internet sales tabular modeling tutorial](https://msdn.microsoft.com/library/hh231691.aspx).</span></span>
* <span data-ttu-id="67ace-113">**Passerelle locale** : si une ou plusieurs sources de données sont locales dans le réseau de votre entreprise, vous devez installer une [Passerelle de données locale](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="67ace-113">**On-premises gateway** - If one or more data sources are on-premises in your organization's network, you need to install an [On-premises data gateway](analysis-services-gateway.md).</span></span> <span data-ttu-id="67ace-114">La passerelle est nécessaire pour que votre serveur se connecte dans le cloud à vos sources de données locales pour traiter et actualiser les données du modèle.</span><span class="sxs-lookup"><span data-stu-id="67ace-114">The gateway is necessary for your server in the cloud connect to your on-premises data sources to process and refresh data in the model.</span></span>

> [!TIP]
> <span data-ttu-id="67ace-115">Avant de déployer, assurez-vous que vous pouvez traiter les données de vos tables.</span><span class="sxs-lookup"><span data-stu-id="67ace-115">Before you deploy, make sure you can process the data in your tables.</span></span> <span data-ttu-id="67ace-116">Dans SSDT, cliquez sur **Modèle** > **Traiter** > **Traiter tout**.</span><span class="sxs-lookup"><span data-stu-id="67ace-116">In SSDT, click **Model** > **Process** > **Process All**.</span></span> <span data-ttu-id="67ace-117">Si le traitement échoue, vous ne pourrez pas procéder au déploiement.</span><span class="sxs-lookup"><span data-stu-id="67ace-117">If processing fails, you cannot successfully deploy.</span></span>
> 
> 

## <a name="to-deploy-a-tabular-model-from-ssdt"></a><span data-ttu-id="67ace-118">Pour déployer un modèle tabulaire à partir de SSDT</span><span class="sxs-lookup"><span data-stu-id="67ace-118">To deploy a tabular model from SSDT</span></span>

1. <span data-ttu-id="67ace-119">Avant de déployer, vous devez obtenir le nom du serveur.</span><span class="sxs-lookup"><span data-stu-id="67ace-119">Before you deploy, you need to get the server name.</span></span> <span data-ttu-id="67ace-120">Dans **Portail Azure** > Serveur > **Présentation** > **Nom du serveur**, copiez le nom du serveur.</span><span class="sxs-lookup"><span data-stu-id="67ace-120">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span></span>
   
    ![Obtenir le nom du serveur dans Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="67ace-122">Dans SSDT > **Explorateur de solutions**, cliquez avec le bouton droit sur le projet > **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="67ace-122">In SSDT > **Solution Explorer**, right-click the project > **Properties**.</span></span> <span data-ttu-id="67ace-123">Ensuite, dans **Déploiement** > **Serveur**, collez le nom du serveur.</span><span class="sxs-lookup"><span data-stu-id="67ace-123">Then in **Deployment** > **Server** paste the server name.</span></span>   
   
    ![Coller le nom du serveur dans la propriété du serveur de déploiement](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. <span data-ttu-id="67ace-125">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur **Propriétés**, puis cliquez sur **Déployer**.</span><span class="sxs-lookup"><span data-stu-id="67ace-125">In **Solution Explorer**, right-click **Properties**, then click **Deploy**.</span></span> <span data-ttu-id="67ace-126">Vous serez peut-être invité à vous connecter à Azure.</span><span class="sxs-lookup"><span data-stu-id="67ace-126">You may be prompted to sign in to Azure.</span></span>
   
    ![Déployer sur un serveur](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    <span data-ttu-id="67ace-128">L’état du déploiement s’affiche dans la fenêtre Sortie et dans Déployer.</span><span class="sxs-lookup"><span data-stu-id="67ace-128">Deployment status appears in both the Output window and in Deploy.</span></span>
   
    ![état du déploiement](./media/analysis-services-deploy/aas-deploy-status.png)

<span data-ttu-id="67ace-130">C’est tout !</span><span class="sxs-lookup"><span data-stu-id="67ace-130">That's all there is to it!</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="67ace-131">Résolution de problèmes</span><span class="sxs-lookup"><span data-stu-id="67ace-131">Troubleshooting</span></span>
<span data-ttu-id="67ace-132">Si le déploiement échoue lors du déploiement de métadonnées, il est probable que SSDT n’ait pas pu se connecter à votre serveur.</span><span class="sxs-lookup"><span data-stu-id="67ace-132">If deployment fails when deploying metadata, it's likely because SSDT couldn't connect to your server.</span></span> <span data-ttu-id="67ace-133">Vérifiez que vous pouvez vous connecter à votre serveur à l’aide de SSMS.</span><span class="sxs-lookup"><span data-stu-id="67ace-133">Make sure you can connect to your server using SSMS.</span></span> <span data-ttu-id="67ace-134">Vérifiez ensuite que la propriété Serveur de déploiement du projet est correcte.</span><span class="sxs-lookup"><span data-stu-id="67ace-134">Then make sure the Deployment Server property for the project is correct.</span></span>

<span data-ttu-id="67ace-135">Si le déploiement échoue sur une table, il est probable que votre serveur n’ait pas pu se connecter à une source de données.</span><span class="sxs-lookup"><span data-stu-id="67ace-135">If deployment fails on a table, it's likely because your server couldn't connect to a data source.</span></span> <span data-ttu-id="67ace-136">Si votre source de données est locale dans le réseau de votre entreprise, veillez à installer une [Passerelle de données locale](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="67ace-136">If your data source is on-premises in your organization's network, be sure to install an [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="67ace-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="67ace-137">Next steps</span></span>
<span data-ttu-id="67ace-138">Maintenant que votre modèle tabulaire est déployé sur votre serveur, vous êtes prêt à vous connecter à celui-ci.</span><span class="sxs-lookup"><span data-stu-id="67ace-138">Now that you have your tabular model deployed to your server, you're ready to connect to it.</span></span> <span data-ttu-id="67ace-139">Vous pouvez vous [connecter à celui-ci avec SSMS](analysis-services-manage.md) pour le gérer.</span><span class="sxs-lookup"><span data-stu-id="67ace-139">You can [connect to it with SSMS](analysis-services-manage.md) to manage it.</span></span> <span data-ttu-id="67ace-140">Vous pouvez également vous [connecter à celui-ci à l’aide d’un outil client](analysis-services-connect.md) tel que Power BI, Power BI Desktop ou Excel, et commencer à créer des rapports.</span><span class="sxs-lookup"><span data-stu-id="67ace-140">And, you can [connect to it using a client tool](analysis-services-connect.md) like Power BI, Power BI Desktop, or Excel, and start creating reports.</span></span>

