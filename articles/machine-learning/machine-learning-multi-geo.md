---
title: "documentation d’aide géo-aaaMulti | Documents Microsoft"
description: "Découvrez comment toocreate un espace de travail et publier un service web dans une région Azure différente de hello South centrale United States (SCUS) région Azure."
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
ms.openlocfilehash: 77b055950ebfe329131b40e5f0a2f6be1e33c51e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="multi-geo-help-documentation"></a><span data-ttu-id="39964-103">Documentation d'aide de zones géographiques multiples</span><span class="sxs-lookup"><span data-stu-id="39964-103">Multi-Geo Help documentation</span></span>
<span data-ttu-id="39964-104">Cet article explique comment vous pouvez créer un espace de travail et publier un service web dans différentes régions Azure.</span><span class="sxs-lookup"><span data-stu-id="39964-104">This article describes how you can create a workspace and publish a web service in different Azure regions.</span></span>  <span data-ttu-id="39964-105">Hello [produits Azure par page région](https://azure.microsoft.com/en-us/regions/services/) répertorie les zones où Azure Machine Learning n’est disponible.</span><span class="sxs-lookup"><span data-stu-id="39964-105">hello [Azure Products by Region page](https://azure.microsoft.com/en-us/regions/services/) lists regions where Azure Machine Learning is available.</span></span>

## <a name="create-a-workspace"></a><span data-ttu-id="39964-106">Créer un espace de travail</span><span class="sxs-lookup"><span data-stu-id="39964-106">Create a workspace</span></span>
1. <span data-ttu-id="39964-107">Connectez-vous toohello portail classique Azure.</span><span class="sxs-lookup"><span data-stu-id="39964-107">Sign in toohello Azure Classic Portal.</span></span>
2. <span data-ttu-id="39964-108">Cliquez sur **+NOUVEAU** > **SERVICES DE DONNÉES** > **MACHINE LEARNING** > **CRÉATION RAPIDE**.</span><span class="sxs-lookup"><span data-stu-id="39964-108">Click **+NEW** > **DATA SERVICES** > **MACHINE LEARNING** > **QUICK CREATE**.</span></span>  <span data-ttu-id="39964-109">Sous **EMPLACEMENT**, sélectionner une autre région, par exemple, l'**Asie du Sud-est**.</span><span class="sxs-lookup"><span data-stu-id="39964-109">Under **LOCATION** select another region, such as **Southeast Asia**.</span></span>
   <span data-ttu-id="39964-110">![Aide zone géographique multiple image 1][1]</span><span class="sxs-lookup"><span data-stu-id="39964-110">![Multi-Geo Help image 1][1]</span></span>
3. <span data-ttu-id="39964-111">Sélectionnez l’espace de travail hello, puis cliquez sur **connexion tooML Studio**.</span><span class="sxs-lookup"><span data-stu-id="39964-111">Select hello workspace, and then click **Sign-in tooML Studio**.</span></span>
   <span data-ttu-id="39964-112">![Aide zone géographique multiple image 2][2]</span><span class="sxs-lookup"><span data-stu-id="39964-112">![Multi-Geo Help image 2][2]</span></span>
4. <span data-ttu-id="39964-113">Vous disposez désormais d'un espace de travail dans une autre région que vous pouvez utiliser comme tout autre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="39964-113">You now have a workspace in another region that you may use just like any other workspace.</span></span> <span data-ttu-id="39964-114">tooswitch entre vos espaces de travail, consultez toohello coin supérieur droit votre écran.</span><span class="sxs-lookup"><span data-stu-id="39964-114">tooswitch among your workspaces, look toohello upper right of your screen.</span></span> <span data-ttu-id="39964-115">Cliquez sur hello déroulante, sélectionnez hello région et espace de travail puis sélectionnez hello.</span><span class="sxs-lookup"><span data-stu-id="39964-115">Click hello dropdown, select hello region, and then select hello workspace.</span></span> <span data-ttu-id="39964-116">Tout est la région d’espace de travail local toohello.</span><span class="sxs-lookup"><span data-stu-id="39964-116">Everything is local toohello workspace region.</span></span>  <span data-ttu-id="39964-117">Par exemple, de tous vos services web créés à partir d’un espace de travail sera Bonjour même espace de travail région hello se trouve dans.</span><span class="sxs-lookup"><span data-stu-id="39964-117">For example, all of your web services created from a workspace will be in hello same region hello workspace is located in.</span></span>
   <span data-ttu-id="39964-118">![Aide zone géographique multiple image 3][3]</span><span class="sxs-lookup"><span data-stu-id="39964-118">![Multi-Geo Help image 3][3]</span></span>

## <a name="open-an-experiment-from-gallery"></a><span data-ttu-id="39964-119">Ouvrir une expérience à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="39964-119">Open an experiment from Gallery</span></span>
<span data-ttu-id="39964-120">Si vous ouvrez une expérience à partir de la galerie, vous pouvez également sélectionner la région que vous souhaitez toocopy hello expérimentation.</span><span class="sxs-lookup"><span data-stu-id="39964-120">If you open an experiment from Gallery, you can also select which region you want toocopy hello experiment to.</span></span>

![Aide zone géographique multiple image 4][4a]

## <a name="web-service-management"></a><span data-ttu-id="39964-122">Gestion des services web</span><span class="sxs-lookup"><span data-stu-id="39964-122">Web service management</span></span>
<span data-ttu-id="39964-123">tooprogrammatically gérer les services web, tels qu’à instruire de nouveau, utiliser une adresse spécifique à la région hello :</span><span class="sxs-lookup"><span data-stu-id="39964-123">tooprogrammatically manage web services, such as for retraining, use hello region-specific address:</span></span>

* <span data-ttu-id="39964-124">https://asiasoutheast.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="39964-124">https://asiasoutheast.management.azureml.net</span></span>
* <span data-ttu-id="39964-125">https://europewest.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="39964-125">https://europewest.management.azureml.net</span></span>

### <a name="things-toonote"></a><span data-ttu-id="39964-126">Éléments toonote</span><span class="sxs-lookup"><span data-stu-id="39964-126">Things toonote</span></span>
1. <span data-ttu-id="39964-127">Vous pouvez copier uniquement les expériences entre les espaces de travail qui appartiennent toohello ainsi la même région.</span><span class="sxs-lookup"><span data-stu-id="39964-127">You can only copy experiments between workspaces that belong toohello same region this way.</span></span> <span data-ttu-id="39964-128">Si vous avez besoin d’expérience de toocopy entre les espaces de travail dans des régions différentes, vous pouvez utiliser hello [PowerShell](http://aka.ms/amlps) applet de commande [ *copie-AmlExperiment* ](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish qui.</span><span class="sxs-lookup"><span data-stu-id="39964-128">If you need toocopy experiment across workspaces in different regions, you can use hello [PowerShell](http://aka.ms/amlps) commandlet [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish that.</span></span> <span data-ttu-id="39964-129">Une autre solution de contournement est expérience de hello toopublish dans la bibliothèque en mode non listé, ouvrez-le dans l’espace de travail hello de hello autre région.</span><span class="sxs-lookup"><span data-stu-id="39964-129">Another workaround is toopublish hello experiment into Gallery in unlisted mode, then open it in hello workspace from hello other region.</span></span>
2. <span data-ttu-id="39964-130">Sélecteur de région de Hello affichera uniquement les espaces de travail pour une région à la fois.</span><span class="sxs-lookup"><span data-stu-id="39964-130">hello region selector will only show workspaces for one region at a time.</span></span>  
3. <span data-ttu-id="39964-131">Un accès à espace libre ou invité (anonyme) est créé et hébergé dans la région South Central U.S.</span><span class="sxs-lookup"><span data-stu-id="39964-131">A free workspace or Guest Access (anonymous) workspace will be created and hosted in South Central U.S.</span></span>  
4. <span data-ttu-id="39964-132">Les services web déployés à partir d'un espace de travail en Asie du Sud-est sont également  hébergés en Asie du Sud-est.</span><span class="sxs-lookup"><span data-stu-id="39964-132">Web services deployed from a workspace in Southeast Asia will also be hosted in Southeast Asia.</span></span>  

## <a name="more-information"></a><span data-ttu-id="39964-133">Plus d’informations</span><span class="sxs-lookup"><span data-stu-id="39964-133">More information</span></span>
<span data-ttu-id="39964-134">Posez une question sur hello [forum d’Azure Machine Learning](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span><span class="sxs-lookup"><span data-stu-id="39964-134">Ask a question on hello [Azure Machine Learning forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span></span>

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
