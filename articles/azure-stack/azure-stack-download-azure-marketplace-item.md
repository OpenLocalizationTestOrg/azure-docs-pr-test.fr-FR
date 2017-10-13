---
title: "Télécharger des éléments de la Place de marché à partir d’Azure | Microsoft Docs"
description: "Je peux télécharger des éléments de la Place de marché à partir d’Azure dans mon déploiement Azure Stack."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: erikje
ms.openlocfilehash: 4d7c335a3c68cc9bb8cb0c823883716a3dd6620a
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2017
---
# <a name="download-marketplace-items-from-azure-to-azure-stack"></a><span data-ttu-id="be577-103">Télécharger des éléments de la Place de marché à partir d’Azure dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="be577-103">Download marketplace items from Azure to Azure Stack</span></span>

<span data-ttu-id="be577-104">*S’applique à : systèmes intégrés Azure Stack et Kit de développement Azure Stack*</span><span class="sxs-lookup"><span data-stu-id="be577-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="be577-105">Quand vous décidez du contenu à inclure dans votre Place de marché Azure Stack, il est recommandé de prendre en compte le contenu disponible auprès de la Place de marché Azure.</span><span class="sxs-lookup"><span data-stu-id="be577-105">As you decide what content to include in your Azure Stack marketplace, you should consider the content available from the Azure marketplace.</span></span> <span data-ttu-id="be577-106">Vous pouvez télécharger à partir d’une liste organisée d’éléments de la Place de marché Azure, qui ont été préalablement testés pour s’exécuter sur Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="be577-106">You can download from a curated list of Azure marketplace items that have been pre-tested to run on Azure Stack.</span></span> <span data-ttu-id="be577-107">De nouveaux éléments sont fréquemment ajoutés à cette liste : consultez-la donc régulièrement pour voir ce qu’elle contient de nouveau.</span><span class="sxs-lookup"><span data-stu-id="be577-107">New items are frequently added to this list, so make sure check back for new content.</span></span>

<span data-ttu-id="be577-108">Pour télécharger des éléments de la Place de marché, vous devez d’abord [inscrire Azure Stack auprès d’Azure](azure-stack-register.md).</span><span class="sxs-lookup"><span data-stu-id="be577-108">To download marketplace items, you must first [register Azure Stack with Azure](azure-stack-register.md).</span></span> 

## <a name="download"></a><span data-ttu-id="be577-109">Télécharger</span><span class="sxs-lookup"><span data-stu-id="be577-109">Download</span></span>
1. <span data-ttu-id="be577-110">Connectez-vous au portail d’administration d’Azure Stack (https://portal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="be577-110">Sign in to the Azure Stack administrator portal (https://portal.local.azurestack.external).</span></span>
2. <span data-ttu-id="be577-111">Certains éléments de la Place de marché peuvent être très volumineux.</span><span class="sxs-lookup"><span data-stu-id="be577-111">Some marketplace items can be very large.</span></span>  <span data-ttu-id="be577-112">Vérifiez que vous avez suffisamment d’espace sur votre système en cliquant sur **Fournisseurs de ressources** > **Stockage**.</span><span class="sxs-lookup"><span data-stu-id="be577-112">Check to make sure you have enough space on your system by clicking **Resource Providers** > **Storage**.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image01.png)

3. <span data-ttu-id="be577-113">Cliquez sur **Autres services** > **Gestion de la Place de marché**.</span><span class="sxs-lookup"><span data-stu-id="be577-113">Click **More Services** > **Marketplace Management**.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image02.png)

4. <span data-ttu-id="be577-114">Cliquez sur **Ajouter à partir d’Azure** pour afficher la liste des éléments disponibles au téléchargement.</span><span class="sxs-lookup"><span data-stu-id="be577-114">Click **Add from Azure** to see a list of items available for download.</span></span> <span data-ttu-id="be577-115">Vous pouvez cliquer sur chaque élément de la liste pour afficher sa description et la taille du téléchargement.</span><span class="sxs-lookup"><span data-stu-id="be577-115">You can click on each item in the list to view its description and download size.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image03.png)

5. <span data-ttu-id="be577-116">Sélectionnez l’élément que vous voulez dans la liste, puis cliquez sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="be577-116">Select the item you want in the list and then click **Download**.</span></span> <span data-ttu-id="be577-117">Ceci démarre le téléchargement de l’image de machine virtuelle pour l’élément sélectionné.</span><span class="sxs-lookup"><span data-stu-id="be577-117">This starts downloading the VM image for the item you selected.</span></span> <span data-ttu-id="be577-118">Le temps de téléchargement varie.</span><span class="sxs-lookup"><span data-stu-id="be577-118">Download times vary.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image04.png)

6. <span data-ttu-id="be577-119">Une fois le téléchargement terminé, vous pouvez déployer votre nouvel élément de Place de marché en tant qu’opérateur ou utilisateur Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="be577-119">After the download completes, you can deploy your new marketplace item as either an Azure Stack operator or user.</span></span> <span data-ttu-id="be577-120">Cliquez sur **+ Nouveau**, recherchez le nouvel élément de Place de marché parmi les catégories, puis sélectionnez l’élément.</span><span class="sxs-lookup"><span data-stu-id="be577-120">Click **+New**, search among the categories for the new marketplace item, and then select the item.</span></span>
7. <span data-ttu-id="be577-121">Cliquez sur **Créer** pour ouvrir l’expérience de création de l’élément qui vient d’être téléchargé.</span><span class="sxs-lookup"><span data-stu-id="be577-121">Click **Create** to open up the creation experience for the newly downloaded item.</span></span> <span data-ttu-id="be577-122">Suivez les instructions pas à pas pour déployer votre élément.</span><span class="sxs-lookup"><span data-stu-id="be577-122">Follow the step-by-step instructions to deploy your item.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be577-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="be577-123">Next steps</span></span>

[<span data-ttu-id="be577-124">Créer et publier un article de la Place de marché</span><span class="sxs-lookup"><span data-stu-id="be577-124">Create and publish a Marketplace item</span></span>](azure-stack-create-and-publish-marketplace-item.md)
