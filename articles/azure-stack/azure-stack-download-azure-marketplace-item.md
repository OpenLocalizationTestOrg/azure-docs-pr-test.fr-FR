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
ms.openlocfilehash: 4baa1b675d2930cd111b5b8368ac081dc2b77841
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="download-marketplace-items-from-azure-to-azure-stack"></a><span data-ttu-id="9900e-103">Télécharger des éléments de la Place de marché à partir d’Azure dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="9900e-103">Download marketplace items from Azure to Azure Stack</span></span>

<span data-ttu-id="9900e-104">Quand vous décidez du contenu à inclure dans votre Place de marché Azure Stack, il est recommandé de prendre en compte le contenu disponible auprès de la Place de marché Azure.</span><span class="sxs-lookup"><span data-stu-id="9900e-104">As you decide what content to include in your Azure Stack marketplace, you should consider the content available from the Azure marketplace.</span></span> <span data-ttu-id="9900e-105">Vous pouvez télécharger à partir d’une liste organisée d’éléments de la Place de marché Azure, qui ont été préalablement testés pour s’exécuter sur Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="9900e-105">You can download from a curated list of Azure marketplace items that have been pre-tested to run on Azure Stack.</span></span> <span data-ttu-id="9900e-106">De nouveaux éléments sont fréquemment ajoutés à cette liste : consultez-la donc régulièrement pour voir ce qu’elle contient de nouveau.</span><span class="sxs-lookup"><span data-stu-id="9900e-106">New items are frequently added to this list, so make sure check back for new content.</span></span>

<span data-ttu-id="9900e-107">Pour télécharger des éléments de la Place de marché, vous devez d’abord [inscrire Azure Stack auprès d’Azure](azure-stack-register.md).</span><span class="sxs-lookup"><span data-stu-id="9900e-107">To download marketplace items, you must first [register Azure Stack with Azure](azure-stack-register.md).</span></span> 

## <a name="download"></a><span data-ttu-id="9900e-108">Télécharger</span><span class="sxs-lookup"><span data-stu-id="9900e-108">Download</span></span>
1. <span data-ttu-id="9900e-109">Connectez-vous au portail d’administration d’Azure Stack (https://portal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="9900e-109">Sign in to the Azure Stack administrator portal (https://portal.local.azurestack.external).</span></span>
2. <span data-ttu-id="9900e-110">Certains éléments de la Place de marché peuvent être très volumineux.</span><span class="sxs-lookup"><span data-stu-id="9900e-110">Some marketplace items can be very large.</span></span>  <span data-ttu-id="9900e-111">Vérifiez que vous avez suffisamment d’espace sur votre système en cliquant sur **Fournisseurs de ressources** > **Stockage**.</span><span class="sxs-lookup"><span data-stu-id="9900e-111">Check to make sure you have enough space on your system by clicking **Resource Providers** > **Storage**.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image01.png)

3. <span data-ttu-id="9900e-112">Cliquez sur **Autres services** > **Gestion de la Place de marché**.</span><span class="sxs-lookup"><span data-stu-id="9900e-112">Click **More Services** > **Marketplace Management**.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image02.png)

4. <span data-ttu-id="9900e-113">Cliquez sur **Ajouter à partir d’Azure** pour afficher la liste des éléments disponibles au téléchargement.</span><span class="sxs-lookup"><span data-stu-id="9900e-113">Click **Add from Azure** to see a list of items available for download.</span></span> <span data-ttu-id="9900e-114">Vous pouvez cliquer sur chaque élément de la liste pour afficher sa description et la taille du téléchargement.</span><span class="sxs-lookup"><span data-stu-id="9900e-114">You can click on each item in the list to view its description and download size.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image03.png)

5. <span data-ttu-id="9900e-115">Sélectionnez l’élément que vous voulez dans la liste, puis cliquez sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="9900e-115">Select the item you want in the list and then click **Download**.</span></span> <span data-ttu-id="9900e-116">Ceci démarre le téléchargement de l’image de machine virtuelle pour l’élément sélectionné.</span><span class="sxs-lookup"><span data-stu-id="9900e-116">This starts downloading the VM image for the item you selected.</span></span> <span data-ttu-id="9900e-117">Le temps de téléchargement varie.</span><span class="sxs-lookup"><span data-stu-id="9900e-117">Download times vary.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image04.png)

6. <span data-ttu-id="9900e-118">Une fois le téléchargement terminé, vous pouvez déployer votre nouvel élément de Place de marché en tant qu’opérateur cloud ou utilisateur du locataire.</span><span class="sxs-lookup"><span data-stu-id="9900e-118">After the download completes, you can deploy your new marketplace item as either a cloud operator or tenant user.</span></span> <span data-ttu-id="9900e-119">Cliquez sur **+ Nouveau**, recherchez le nouvel élément de Place de marché parmi les catégories, puis sélectionnez l’élément.</span><span class="sxs-lookup"><span data-stu-id="9900e-119">Click **+New**, search among the categories for the new marketplace item, and then select the item.</span></span>
7. <span data-ttu-id="9900e-120">Cliquez sur **Créer** pour ouvrir l’expérience de création de l’élément qui vient d’être téléchargé.</span><span class="sxs-lookup"><span data-stu-id="9900e-120">Click **Create** to open up the creation experience for the newly downloaded item.</span></span> <span data-ttu-id="9900e-121">Suivez les instructions pas à pas pour déployer votre élément.</span><span class="sxs-lookup"><span data-stu-id="9900e-121">Follow the step-by-step instructions to deploy your item.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9900e-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9900e-122">Next steps</span></span>

[<span data-ttu-id="9900e-123">Créer et publier un article du Marketplace</span><span class="sxs-lookup"><span data-stu-id="9900e-123">Create and publish a Marketplace item</span></span>](azure-stack-create-and-publish-marketplace-item.md)
