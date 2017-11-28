---
title: "Déployer des modèles avec le portail dans Azure Stack | Microsoft Docs"
description: "Apprenez à utiliser le portail Azure Stack pour déployer des modèles."
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: eafa60f2-16c9-4ef1-b724-47709e9ea29e
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: eb6e67dc4707b2b999efcceec1c55dc950c5996e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-templates-using-the-azure-stack-portal"></a><span data-ttu-id="85f9d-103">Déployer des modèles à l’aide du portail Azure Stack</span><span class="sxs-lookup"><span data-stu-id="85f9d-103">Deploy templates using the Azure Stack portal</span></span>
<span data-ttu-id="85f9d-104">Utilisez le portail pour déployer des modèles Azure Resource Manager dans le kit de développement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="85f9d-104">Use the portal to deploy Azure Resource Manager templates to the Azure Stack development kit.</span></span>

<span data-ttu-id="85f9d-105">Les modèles Resource Manager déploient et approvisionnent toutes les ressources de l’application en une seule opération coordonnée.</span><span class="sxs-lookup"><span data-stu-id="85f9d-105">Resource Manager templates deploy and provision all the resources for your application in a single, coordinated operation.</span></span>

1. <span data-ttu-id="85f9d-106">Connectez-vous au portail, cliquez sur **Nouveau**, **Personnalisé**, puis **Déploiement du modèle**.</span><span class="sxs-lookup"><span data-stu-id="85f9d-106">Log in to the portal, click **New**, click **Custom**, and then click **Template deployment**.</span></span>
2. <span data-ttu-id="85f9d-107">Cliquez sur **Modifier un modèle**, puis collez le code de votre modèle JSON sur le panneau et cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="85f9d-107">Click **Edit template**, then paste your JSON template code into the blade, and then click **Save**.</span></span>
3. <span data-ttu-id="85f9d-108">Cliquez sur **Modifier les paramètres**, tapez des valeurs pour les paramètres listés, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="85f9d-108">Click **Edit parameters**, type values for the parameters listed, and then click **OK**.</span></span>
4. <span data-ttu-id="85f9d-109">Cliquez sur **Abonnement**, choisissez l’abonnement que vous souhaitez utiliser, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="85f9d-109">Click **Subscription**, choose the subscription you want to use, and then click **OK**.</span></span>
5. <span data-ttu-id="85f9d-110">Cliquez sur **Groupe de ressources**, choisissez un groupe de ressources existant ou créez-en un, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="85f9d-110">Click **Resource group**, choose an existing resource group or create a new one, and then click **OK**.</span></span>
6. <span data-ttu-id="85f9d-111">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="85f9d-111">Click **Create**.</span></span> <span data-ttu-id="85f9d-112">Le tableau de bord contient maintenant une nouvelle vignette qui suit la progression du déploiement de votre modèle.</span><span class="sxs-lookup"><span data-stu-id="85f9d-112">A new tile on the dashboard tracks the progress of your template deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85f9d-113">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="85f9d-113">Next steps</span></span>
[<span data-ttu-id="85f9d-114">Déployer des modèles avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="85f9d-114">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)

