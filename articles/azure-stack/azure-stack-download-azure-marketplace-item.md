---
title: "éléments du marketplace aaaDownload à partir de Azure | Documents Microsoft"
description: "Je peux télécharger les éléments du marketplace à partir d’Azure toomy de déploiement de la pile de Azure."
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
ms.openlocfilehash: 734470fbacc09617908a2f6db9107ffa9c39e51d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="download-marketplace-items-from-azure-tooazure-stack"></a><span data-ttu-id="fc32f-103">Télécharger des éléments du marketplace à partir de la pile de tooAzure Azure</span><span class="sxs-lookup"><span data-stu-id="fc32f-103">Download marketplace items from Azure tooAzure Stack</span></span>

<span data-ttu-id="fc32f-104">Lorsque vous décidez quelles tooinclude contenu dans le marketplace de pile d’Azure, vous devez envisager de contenu hello disponible à partir de hello Azure marketplace.</span><span class="sxs-lookup"><span data-stu-id="fc32f-104">As you decide what content tooinclude in your Azure Stack marketplace, you should consider hello content available from hello Azure marketplace.</span></span> <span data-ttu-id="fc32f-105">Vous pouvez le télécharger dans la liste d’éléments d’Azure marketplace qui ont été préalablement testé toorun sur Azure pile organisée.</span><span class="sxs-lookup"><span data-stu-id="fc32f-105">You can download from a curated list of Azure marketplace items that have been pre-tested toorun on Azure Stack.</span></span> <span data-ttu-id="fc32f-106">Nouveaux éléments sont ajoutés fréquemment toothis liste, vous devez donc vous consultez renvoyé par le nouveau contenu.</span><span class="sxs-lookup"><span data-stu-id="fc32f-106">New items are frequently added toothis list, so make sure check back for new content.</span></span>

<span data-ttu-id="fc32f-107">éléments du marketplace toodownload, vous devez d’abord [inscrire la pile d’Azure avec Azure](azure-stack-register.md).</span><span class="sxs-lookup"><span data-stu-id="fc32f-107">toodownload marketplace items, you must first [register Azure Stack with Azure](azure-stack-register.md).</span></span> 

## <a name="download"></a><span data-ttu-id="fc32f-108">Télécharger</span><span class="sxs-lookup"><span data-stu-id="fc32f-108">Download</span></span>
1. <span data-ttu-id="fc32f-109">Se connecter toohello portail d’administration Azure pile (https://portal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="fc32f-109">Sign in toohello Azure Stack administrator portal (https://portal.local.azurestack.external).</span></span>
2. <span data-ttu-id="fc32f-110">Certains éléments de la Place de marché peuvent être très volumineux.</span><span class="sxs-lookup"><span data-stu-id="fc32f-110">Some marketplace items can be very large.</span></span>  <span data-ttu-id="fc32f-111">Vérifiez toomake sûr d’avoir suffisamment d’espace sur votre système en cliquant sur **fournisseurs de ressources** > **stockage**.</span><span class="sxs-lookup"><span data-stu-id="fc32f-111">Check toomake sure you have enough space on your system by clicking **Resource Providers** > **Storage**.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image01.png)

3. <span data-ttu-id="fc32f-112">Cliquez sur **Autres services** > **Gestion de la Place de marché**.</span><span class="sxs-lookup"><span data-stu-id="fc32f-112">Click **More Services** > **Marketplace Management**.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image02.png)

4. <span data-ttu-id="fc32f-113">Cliquez sur **ajouter à partir d’Azure** toosee une liste d’éléments disponibles en téléchargement.</span><span class="sxs-lookup"><span data-stu-id="fc32f-113">Click **Add from Azure** toosee a list of items available for download.</span></span> <span data-ttu-id="fc32f-114">Vous pouvez cliquez sur chaque élément dans hello liste tooview sa description et la taille de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="fc32f-114">You can click on each item in hello list tooview its description and download size.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image03.png)

5. <span data-ttu-id="fc32f-115">Sélectionnez hello élément souhaité dans la liste de hello puis cliquez sur **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="fc32f-115">Select hello item you want in hello list and then click **Download**.</span></span> <span data-ttu-id="fc32f-116">Cela démarre le téléchargement de l’image de machine virtuelle hello pour hello que vous avez sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="fc32f-116">This starts downloading hello VM image for hello item you selected.</span></span> <span data-ttu-id="fc32f-117">Le temps de téléchargement varie.</span><span class="sxs-lookup"><span data-stu-id="fc32f-117">Download times vary.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image04.png)

6. <span data-ttu-id="fc32f-118">Une fois le téléchargement de hello terminé, vous pouvez déployer votre nouvel élément de marketplace comme un opérateur cloud ou un utilisateur du client.</span><span class="sxs-lookup"><span data-stu-id="fc32f-118">After hello download completes, you can deploy your new marketplace item as either a cloud operator or tenant user.</span></span> <span data-ttu-id="fc32f-119">Cliquez sur **+ nouveau**, rechercher parmi les catégories de hello pour le nouvel élément de marketplace hello, puis sélectionnez un élément hello.</span><span class="sxs-lookup"><span data-stu-id="fc32f-119">Click **+New**, search among hello categories for hello new marketplace item, and then select hello item.</span></span>
7. <span data-ttu-id="fc32f-120">Cliquez sur **créer** tooopen expérience de création de hello pour hello nouvellement téléchargé élément.</span><span class="sxs-lookup"><span data-stu-id="fc32f-120">Click **Create** tooopen up hello creation experience for hello newly downloaded item.</span></span> <span data-ttu-id="fc32f-121">Suivez toodeploy des instructions pas à pas hello votre élément.</span><span class="sxs-lookup"><span data-stu-id="fc32f-121">Follow hello step-by-step instructions toodeploy your item.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc32f-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fc32f-122">Next steps</span></span>

[<span data-ttu-id="fc32f-123">Créer et publier un article de la Place de marché</span><span class="sxs-lookup"><span data-stu-id="fc32f-123">Create and publish a Marketplace item</span></span>](azure-stack-create-and-publish-marketplace-item.md)
