---
title: "aaaDeploy tooAzure Analysis Services à l’aide de SSDT | Documents Microsoft"
description: "Découvrez comment toodeploy un tooan de modèle tabulaire Azure Analysis Services server à l’aide de SSDT."
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
ms.openlocfilehash: e3f3771fe32a37b9e0173c274080c647152edd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-model-from-ssdt"></a><span data-ttu-id="a5e58-103">Déployer un modèle à partir de SSDT</span><span class="sxs-lookup"><span data-stu-id="a5e58-103">Deploy a model from SSDT</span></span>
<span data-ttu-id="a5e58-104">Une fois que vous avez créé un serveur dans votre abonnement Azure, vous êtes prêt toodeploy un tooit de base de données de modèle tabulaire.</span><span class="sxs-lookup"><span data-stu-id="a5e58-104">Once you've created a server in your Azure subscription, you're ready toodeploy a tabular model database tooit.</span></span> <span data-ttu-id="a5e58-105">Vous pouvez utiliser SQL Server Data Tools (SSDT) toobuild et déployer un projet de modèle tabulaire sur lequel vous travaillez.</span><span class="sxs-lookup"><span data-stu-id="a5e58-105">You can use SQL Server Data Tools (SSDT) toobuild and deploy a tabular model project you're working on.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a5e58-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a5e58-106">Prerequisites</span></span>
<span data-ttu-id="a5e58-107">tooget démarré, vous devez :</span><span class="sxs-lookup"><span data-stu-id="a5e58-107">tooget started, you need:</span></span>

* <span data-ttu-id="a5e58-108">**Serveur Analysis Services** dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e58-108">**Analysis Services server** in Azure.</span></span> <span data-ttu-id="a5e58-109">toolearn, voir [créer un serveur Azure Analysis Services](analysis-services-create-server.md).</span><span class="sxs-lookup"><span data-stu-id="a5e58-109">toolearn more, see [Create an Azure Analysis Services server](analysis-services-create-server.md).</span></span>
* <span data-ttu-id="a5e58-110">**Projet de modèle tabulaire** dans SSDT ou un modèle tabulaire existant hello 1200 au niveau de compatibilité supérieur.</span><span class="sxs-lookup"><span data-stu-id="a5e58-110">**Tabular model project** in SSDT or an existing tabular model at hello 1200 or higher compatibility level.</span></span> <span data-ttu-id="a5e58-111">Vous ne l’avez jamais fait ?</span><span class="sxs-lookup"><span data-stu-id="a5e58-111">Never created one?</span></span> <span data-ttu-id="a5e58-112">Essayez de hello [didacticiel de modélisation tabulaire vente Adventure Works Internet](https://msdn.microsoft.com/library/hh231691.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5e58-112">Try hello [Adventure Works Internet sales tabular modeling tutorial](https://msdn.microsoft.com/library/hh231691.aspx).</span></span>
* <span data-ttu-id="a5e58-113">**Passerelle locale** -si une ou plusieurs sources de données sont localement dans le réseau de votre organisation, vous devez tooinstall une [passerelle de données locale](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="a5e58-113">**On-premises gateway** - If one or more data sources are on-premises in your organization's network, you need tooinstall an [On-premises data gateway](analysis-services-gateway.md).</span></span> <span data-ttu-id="a5e58-114">passerelle de Hello est nécessaire pour la connexion à votre serveur dans le cloud de hello tooyour des données sources tooprocess et l’actualisation des données locales dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="a5e58-114">hello gateway is necessary for your server in hello cloud connect tooyour on-premises data sources tooprocess and refresh data in hello model.</span></span>

> [!TIP]
> <span data-ttu-id="a5e58-115">Avant de déployer, assurez-vous que vous pouvez traiter les données de salutation dans vos tables.</span><span class="sxs-lookup"><span data-stu-id="a5e58-115">Before you deploy, make sure you can process hello data in your tables.</span></span> <span data-ttu-id="a5e58-116">Dans SSDT, cliquez sur **Modèle** > **Traiter** > **Traiter tout**.</span><span class="sxs-lookup"><span data-stu-id="a5e58-116">In SSDT, click **Model** > **Process** > **Process All**.</span></span> <span data-ttu-id="a5e58-117">Si le traitement échoue, vous ne pourrez pas procéder au déploiement.</span><span class="sxs-lookup"><span data-stu-id="a5e58-117">If processing fails, you cannot successfully deploy.</span></span>
> 
> 

## <a name="toodeploy-a-tabular-model-from-ssdt"></a><span data-ttu-id="a5e58-118">toodeploy un modèle tabulaire à partir de SSDT</span><span class="sxs-lookup"><span data-stu-id="a5e58-118">toodeploy a tabular model from SSDT</span></span>

1. <span data-ttu-id="a5e58-119">Avant de déployer, vous devez le nom du serveur tooget hello.</span><span class="sxs-lookup"><span data-stu-id="a5e58-119">Before you deploy, you need tooget hello server name.</span></span> <span data-ttu-id="a5e58-120">Dans **portail Azure** > serveur > **vue d’ensemble** > **nom du serveur**, copier le nom de serveur hello.</span><span class="sxs-lookup"><span data-stu-id="a5e58-120">In **Azure portal** > server > **Overview** > **Server name**, copy hello server name.</span></span>
   
    ![Obtenir le nom du serveur dans Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="a5e58-122">Dans SSDT > **l’Explorateur de solutions**, projet de hello avec le bouton droit > **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="a5e58-122">In SSDT > **Solution Explorer**, right-click hello project > **Properties**.</span></span> <span data-ttu-id="a5e58-123">Ensuite, dans **déploiement** > **Server** collez le nom du serveur hello.</span><span class="sxs-lookup"><span data-stu-id="a5e58-123">Then in **Deployment** > **Server** paste hello server name.</span></span>   
   
    ![Coller le nom du serveur dans la propriété du serveur de déploiement](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. <span data-ttu-id="a5e58-125">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur **Propriétés**, puis cliquez sur **Déployer**.</span><span class="sxs-lookup"><span data-stu-id="a5e58-125">In **Solution Explorer**, right-click **Properties**, then click **Deploy**.</span></span> <span data-ttu-id="a5e58-126">Vous pouvez être invité à toosign dans tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a5e58-126">You may be prompted toosign in tooAzure.</span></span>
   
    ![Déployer tooserver](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    <span data-ttu-id="a5e58-128">État du déploiement s’affiche dans les deux fenêtres de sortie hello et déployer.</span><span class="sxs-lookup"><span data-stu-id="a5e58-128">Deployment status appears in both hello Output window and in Deploy.</span></span>
   
    ![état du déploiement](./media/analysis-services-deploy/aas-deploy-status.png)

<span data-ttu-id="a5e58-130">C’est tout est tooit !</span><span class="sxs-lookup"><span data-stu-id="a5e58-130">That's all there is tooit!</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="a5e58-131">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="a5e58-131">Troubleshooting</span></span>
<span data-ttu-id="a5e58-132">Si le déploiement échoue lors du déploiement des métadonnées, il est probable, car SSDT n’a pas pu se connecter à tooyour server.</span><span class="sxs-lookup"><span data-stu-id="a5e58-132">If deployment fails when deploying metadata, it's likely because SSDT couldn't connect tooyour server.</span></span> <span data-ttu-id="a5e58-133">Assurez-vous que vous pouvez vous connecter serveur tooyour à l’aide de SSMS.</span><span class="sxs-lookup"><span data-stu-id="a5e58-133">Make sure you can connect tooyour server using SSMS.</span></span> <span data-ttu-id="a5e58-134">Vérifiez que hello propriété du serveur de déploiement pour le projet de hello est correct.</span><span class="sxs-lookup"><span data-stu-id="a5e58-134">Then make sure hello Deployment Server property for hello project is correct.</span></span>

<span data-ttu-id="a5e58-135">Si le déploiement échoue sur une table, il est probable, car votre serveur n’a pas pu se connecter de source de données tooa.</span><span class="sxs-lookup"><span data-stu-id="a5e58-135">If deployment fails on a table, it's likely because your server couldn't connect tooa data source.</span></span> <span data-ttu-id="a5e58-136">Si votre source de données est locale dans le réseau de votre organisation, être tooinstall vraiment une [passerelle de données locale](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="a5e58-136">If your data source is on-premises in your organization's network, be sure tooinstall an [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5e58-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a5e58-137">Next steps</span></span>
<span data-ttu-id="a5e58-138">Maintenant que vous avez votre serveur déployé tooyour de modèle tabulaire, vous êtes prêt tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="a5e58-138">Now that you have your tabular model deployed tooyour server, you're ready tooconnect tooit.</span></span> <span data-ttu-id="a5e58-139">Vous pouvez [connecter tooit avec SSMS](analysis-services-manage.md) toomanage il.</span><span class="sxs-lookup"><span data-stu-id="a5e58-139">You can [connect tooit with SSMS](analysis-services-manage.md) toomanage it.</span></span> <span data-ttu-id="a5e58-140">Et vous pouvez [se connecter à l’aide d’un outil client de tooit](analysis-services-connect.md) comme Power BI, Power BI Desktop, ou Excel et la création de rapports de début.</span><span class="sxs-lookup"><span data-stu-id="a5e58-140">And, you can [connect tooit using a client tool](analysis-services-connect.md) like Power BI, Power BI Desktop, or Excel, and start creating reports.</span></span>

