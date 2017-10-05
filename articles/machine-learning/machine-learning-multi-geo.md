---
title: "Documentation d'aide de zones géographiques multiples | Microsoft Docs"
description: "Apprenez à créer un espace de travail et à publier un service web dans une région Azure autre que South Central United States (SCUS)."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: rmca14
tags: 
ms.assetid: ed0ca8a8-fa53-4e56-b824-2d7e44641967
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/6/2017
ms.author: tedway; neerajkh
ms.openlocfilehash: 32f80863308c00c32b1496bb92d39a7ae7d0cc6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="multi-geo-help-documentation"></a><span data-ttu-id="808ed-103">Documentation d'aide de zones géographiques multiples</span><span class="sxs-lookup"><span data-stu-id="808ed-103">Multi-Geo Help documentation</span></span>
<span data-ttu-id="808ed-104">Cet article explique comment vous pouvez créer un espace de travail et publier un service web dans différentes régions Azure.</span><span class="sxs-lookup"><span data-stu-id="808ed-104">This article describes how you can create a workspace and publish a web service in different Azure regions.</span></span>  <span data-ttu-id="808ed-105">La page [Produits Azure par région](https://azure.microsoft.com/en-us/regions/services/) répertorie les régions dans lesquelles Azure Machine Learning est disponible.</span><span class="sxs-lookup"><span data-stu-id="808ed-105">The [Azure Products by Region page](https://azure.microsoft.com/en-us/regions/services/) lists regions where Azure Machine Learning is available.</span></span>

## <a name="create-a-workspace"></a><span data-ttu-id="808ed-106">Créer un espace de travail</span><span class="sxs-lookup"><span data-stu-id="808ed-106">Create a workspace</span></span>
1. <span data-ttu-id="808ed-107">Connectez-vous au portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="808ed-107">Sign in to the Azure Classic Portal.</span></span>
2. <span data-ttu-id="808ed-108">Cliquez sur **+NOUVEAU** > **SERVICES DE DONNÉES** > **MACHINE LEARNING** > **CRÉATION RAPIDE**.</span><span class="sxs-lookup"><span data-stu-id="808ed-108">Click **+NEW** > **DATA SERVICES** > **MACHINE LEARNING** > **QUICK CREATE**.</span></span>  <span data-ttu-id="808ed-109">Sous **EMPLACEMENT**, sélectionner une autre région, par exemple, l'**Asie du Sud-est**.</span><span class="sxs-lookup"><span data-stu-id="808ed-109">Under **LOCATION** select another region, such as **Southeast Asia**.</span></span>
   <span data-ttu-id="808ed-110">![Aide zone géographique multiple image 1][1]</span><span class="sxs-lookup"><span data-stu-id="808ed-110">![Multi-Geo Help image 1][1]</span></span>
3. <span data-ttu-id="808ed-111">Sélectionnez l'espace de travail, puis cliquez sur **Se connecter à ML Studio**.</span><span class="sxs-lookup"><span data-stu-id="808ed-111">Select the workspace, and then click **Sign-in to ML Studio**.</span></span>
   <span data-ttu-id="808ed-112">![Aide zone géographique multiple image 2][2]</span><span class="sxs-lookup"><span data-stu-id="808ed-112">![Multi-Geo Help image 2][2]</span></span>
4. <span data-ttu-id="808ed-113">Vous disposez désormais d'un espace de travail dans une autre région que vous pouvez utiliser comme tout autre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="808ed-113">You now have a workspace in another region that you may use just like any other workspace.</span></span> <span data-ttu-id="808ed-114">Pour basculer d'un espace de travail à l'autre, recherchez le coin supérieur droit de votre écran.</span><span class="sxs-lookup"><span data-stu-id="808ed-114">To switch among your workspaces, look to the upper right of your screen.</span></span> <span data-ttu-id="808ed-115">Cliquez sur la liste déroulante, sélectionnez la région, puis sélectionnez l'espace de travail.</span><span class="sxs-lookup"><span data-stu-id="808ed-115">Click the dropdown, select the region, and then select the workspace.</span></span> <span data-ttu-id="808ed-116">Tout est lié à la région dans laquelle l’espace de travail se trouve.</span><span class="sxs-lookup"><span data-stu-id="808ed-116">Everything is local to the workspace region.</span></span>  <span data-ttu-id="808ed-117">Par exemple, tous les services web créés à partir d’un espace de travail seront dans la même région que l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="808ed-117">For example, all of your web services created from a workspace will be in the same region the workspace is located in.</span></span>
   <span data-ttu-id="808ed-118">![Aide zone géographique multiple image 3][3]</span><span class="sxs-lookup"><span data-stu-id="808ed-118">![Multi-Geo Help image 3][3]</span></span>

## <a name="open-an-experiment-from-gallery"></a><span data-ttu-id="808ed-119">Ouvrir une expérience à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="808ed-119">Open an experiment from Gallery</span></span>
<span data-ttu-id="808ed-120">Si vous ouvrez une expérience à partir de la galerie, vous pouvez également sélectionner la région dans laquelle vous souhaitez copier l'expérience.</span><span class="sxs-lookup"><span data-stu-id="808ed-120">If you open an experiment from Gallery, you can also select which region you want to copy the experiment to.</span></span>

![Aide zone géographique multiple image 4][4a]

## <a name="web-service-management"></a><span data-ttu-id="808ed-122">Gestion des services web</span><span class="sxs-lookup"><span data-stu-id="808ed-122">Web service management</span></span>
<span data-ttu-id="808ed-123">Pour gérer par programmation les services web, par exemple pour la reformation, utilisez l’adresse propre à la région :</span><span class="sxs-lookup"><span data-stu-id="808ed-123">To programmatically manage web services, such as for retraining, use the region-specific address:</span></span>

* <span data-ttu-id="808ed-124">https://asiasoutheast.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="808ed-124">https://asiasoutheast.management.azureml.net</span></span>
* <span data-ttu-id="808ed-125">https://europewest.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="808ed-125">https://europewest.management.azureml.net</span></span>

### <a name="things-to-note"></a><span data-ttu-id="808ed-126">Points à noter</span><span class="sxs-lookup"><span data-stu-id="808ed-126">Things to note</span></span>
1. <span data-ttu-id="808ed-127">Vous pouvez uniquement copier des expériences entre espaces de travail appartenant à la même région de cette façon.</span><span class="sxs-lookup"><span data-stu-id="808ed-127">You can only copy experiments between workspaces that belong to the same region this way.</span></span> <span data-ttu-id="808ed-128">Si vous devez copier l’expérience des espaces de travail dans différentes régions, vous pouvez utiliser l’applet de commande [PowerShell](http://aka.ms/amlps) [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) pour le faire.</span><span class="sxs-lookup"><span data-stu-id="808ed-128">If you need to copy experiment across workspaces in different regions, you can use the [PowerShell](http://aka.ms/amlps) commandlet [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) to accomplish that.</span></span> <span data-ttu-id="808ed-129">Une autre solution de contournement consiste à publier l’expérience dans la galerie en mode non répertorié, puis à l’ouvrir dans l’espace de travail à partir de l’autre région.</span><span class="sxs-lookup"><span data-stu-id="808ed-129">Another workaround is to publish the experiment into Gallery in unlisted mode, then open it in the workspace from the other region.</span></span>
2. <span data-ttu-id="808ed-130">Le sélecteur de région affiche uniquement les espaces de travail d'une seule région à la fois.</span><span class="sxs-lookup"><span data-stu-id="808ed-130">The region selector will only show workspaces for one region at a time.</span></span>  
3. <span data-ttu-id="808ed-131">Un accès à espace libre ou invité (anonyme) est créé et hébergé dans la région South Central U.S.</span><span class="sxs-lookup"><span data-stu-id="808ed-131">A free workspace or Guest Access (anonymous) workspace will be created and hosted in South Central U.S.</span></span>  
4. <span data-ttu-id="808ed-132">Les services web déployés à partir d'un espace de travail en Asie du Sud-est sont également  hébergés en Asie du Sud-est.</span><span class="sxs-lookup"><span data-stu-id="808ed-132">Web services deployed from a workspace in Southeast Asia will also be hosted in Southeast Asia.</span></span>  

## <a name="more-information"></a><span data-ttu-id="808ed-133">Plus d’informations</span><span class="sxs-lookup"><span data-stu-id="808ed-133">More information</span></span>
<span data-ttu-id="808ed-134">Poser une question sur le [forum Azure Machine Learning](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span><span class="sxs-lookup"><span data-stu-id="808ed-134">Ask a question on the [Azure Machine Learning forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span></span>

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
