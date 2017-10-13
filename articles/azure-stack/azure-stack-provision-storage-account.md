---
title: Comptes de stockage dans Azure Stack | Microsoft Docs
description: "Découvrez comment créer un compte de stockage Azure Stack."
services: azure-stack
documentationcenter: 
author: vhorne
manager: byronr
editor: 
ms.assetid: e1152110-b756-4c1a-9fa2-73fe3ab0ad8e
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 3/1/2017
ms.author: victorh
ms.openlocfilehash: 41c9ee37c43d4ad41c51ea2ed023d3b47d460dd1
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2017
---
# <a name="storage-accounts-in-azure-stack"></a><span data-ttu-id="0e28c-103">Comptes de stockage dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="0e28c-103">Storage accounts in Azure Stack</span></span>
<span data-ttu-id="0e28c-104">Les comptes de stockage incluent les services d’objets Blob et de Table, ainsi que l’espace de noms unique pour vos objets de données de stockage.</span><span class="sxs-lookup"><span data-stu-id="0e28c-104">Storage accounts include Blob and Table services, and the unique namespace for your storage data objects.</span></span> <span data-ttu-id="0e28c-105">Par défaut, les données de votre compte sont uniquement accessibles par vous, le propriétaire du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="0e28c-105">By default, the data in your account is available only to you, the storage account owner.</span></span>

1. <span data-ttu-id="0e28c-106">Sur l’ordinateur Azure Stack POC, connectez-vous à `https://adminportal.local.azurestack.external` en tant qu’[administrateur](azure-stack-connect-azure-stack.md), puis cliquez sur **Nouveau** > **Données + stockage** > **Compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="0e28c-106">On the Azure Stack POC computer, log in to `https://adminportal.local.azurestack.external` as [an admin](azure-stack-connect-azure-stack.md), and then click **New** > **Data + Storage** > **Storage account**.</span></span>

   ![](media/azure-stack-provision-storage-account/image01.png)
2. <span data-ttu-id="0e28c-107">Dans le panneau **Créer un compte de stockage**, tapez un nom pour votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="0e28c-107">In the **Create storage account** blade, type a name for your storage account.</span></span> <span data-ttu-id="0e28c-108">Créer un **Groupe de ressources** ou sélectionnez un groupe existant, puis cliquez sur **Créer** pour créer le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="0e28c-108">Create a new **Resource Group**, or select an existing one, then click **Create** to create the storage account.</span></span>

   ![](media/azure-stack-provision-storage-account/image02.png)
3. <span data-ttu-id="0e28c-109">Pour voir votre nouveau compte de stockage, cliquez sur **Toutes les ressources**, puis recherchez le compte de stockage et cliquez sur son nom.</span><span class="sxs-lookup"><span data-stu-id="0e28c-109">To see your new storage account, click **All resources**, then search for the storage account and click its name.</span></span>

    ![](media/azure-stack-provision-storage-account/image03.png)

### <a name="next-steps"></a><span data-ttu-id="0e28c-110">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0e28c-110">Next steps</span></span>
[<span data-ttu-id="0e28c-111">Utiliser les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0e28c-111">Use Azure Resource Manager templates</span></span>](user/azure-stack-arm-templates.md)

[<span data-ttu-id="0e28c-112">Découvrir les comptes de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="0e28c-112">Learn about Azure storage accounts</span></span>](../storage/common/storage-create-storage-account.md)

[<span data-ttu-id="0e28c-113">Télécharger le guide de validation du stockage ACS (Azure-Consistent Storage) d’Azure Stack</span><span class="sxs-lookup"><span data-stu-id="0e28c-113">Download the Azure Stack Azure-consistent Storage Validation Guide</span></span>](http://aka.ms/azurestacktp1doc)
