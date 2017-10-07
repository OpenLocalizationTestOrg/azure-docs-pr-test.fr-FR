---
title: aaaCreate une machine virtuelle avec une adresse IP publique statique - portail Azure | Documents Microsoft
description: "Découvrez comment toocreate une machine virtuelle avec un statique publique adresse IP via hello portail Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e9546bcc-f300-428f-b94a-056c5bd29035
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f74d2132785f06148757409ee0a44b98d1e4b98e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-portal"></a><span data-ttu-id="70157-103">Créer une machine virtuelle avec une adresse IP publique statique à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="70157-103">Create a VM with a static public IP address using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="70157-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="70157-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="70157-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="70157-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="70157-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="70157-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="70157-107">Modèle</span><span class="sxs-lookup"><span data-stu-id="70157-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="70157-108">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="70157-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="70157-109">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="70157-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="70157-110">Cet article décrit à l’aide du modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="70157-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a><span data-ttu-id="70157-111">Créer une machine virtuelle avec une adresse IP publique statique</span><span class="sxs-lookup"><span data-stu-id="70157-111">Create a VM with a static public IP</span></span>

<span data-ttu-id="70157-112">toocreate une machine virtuelle avec une adresse IP publique statique d’adresses Bonjour portail Azure, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="70157-112">toocreate a VM with a static public IP address in hello Azure portal, complete hello following steps:</span></span>

1. <span data-ttu-id="70157-113">À partir d’un navigateur, accédez à toohello [portail Azure](https://portal.azure.com) et, si nécessaire, connectez-vous à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="70157-113">From a browser, navigate toohello [Azure portal](https://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="70157-114">Dans hello coin supérieur gauche du portail de hello, cliquez sur **nouveau**>>**de calcul**>**Windows Server 2012 R2 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="70157-114">On hello top left hand corner of hello portal, click **New**>>**Compute**>**Windows Server 2012 R2 Datacenter**.</span></span>
3. <span data-ttu-id="70157-115">Bonjour **sélectionner un modèle de déploiement** , sélectionnez **le Gestionnaire de ressources** et cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="70157-115">In hello **Select a deployment model** list, select **Resource Manager** and click **Create**.</span></span>
4. <span data-ttu-id="70157-116">Bonjour **notions de base** panneau, entrez les informations sur les ordinateurs virtuels hello comme indiqué ci-dessous, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="70157-116">In hello **Basics** blade, enter hello VM information as shown below, and then click **OK**.</span></span>
   
    ![Portail Azure - De base](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. <span data-ttu-id="70157-118">Bonjour **choisir une taille** panneau, cliquez sur **A1 Standard** comme indiqué ci-dessous, puis cliquez sur **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="70157-118">In hello **Choose a size** blade, click **A1 Standard** as shown below, and then click **Select**.</span></span>
   
    ![Portail Azure - Choisir une taille](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. <span data-ttu-id="70157-120">Bonjour **paramètres** panneau, cliquez sur **adresse IP publique**, puis Bonjour **créer une adresse IP publique** panneau, sous **affectation**, cliquez sur **Statique** comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="70157-120">In hello **Settings** blade, click **Public IP address**, then in hello **Create public IP address** blade, under **Assignment**, click **Static** as shown below.</span></span> <span data-ttu-id="70157-121">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="70157-121">And then click **OK**.</span></span>
   
    ![Portail Azure - Créer une adresse IP publique](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. <span data-ttu-id="70157-123">Bonjour **paramètres** panneau, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="70157-123">In hello **Settings** blade, click **OK**.</span></span>
8. <span data-ttu-id="70157-124">Hello de révision **Résumé** panneau, comme illustré ci-dessous, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="70157-124">Review hello **Summary** blade, as shown below, and then click **OK**.</span></span>
   
    ![Portail Azure - Créer une adresse IP publique](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. <span data-ttu-id="70157-126">Notez la nouvelle vignette de hello dans votre tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="70157-126">Notice hello new tile in your dashboard.</span></span>
   
    ![Portail Azure - Créer une adresse IP publique](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. <span data-ttu-id="70157-128">Une fois créé, hello VM hello **paramètres** panneau s’affichera comme indiqué ci-dessous</span><span class="sxs-lookup"><span data-stu-id="70157-128">Once hello VM is created, hello **Settings** blade will be displayed as shown below</span></span>
    
    ![Portail Azure - Créer une adresse IP publique](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)

