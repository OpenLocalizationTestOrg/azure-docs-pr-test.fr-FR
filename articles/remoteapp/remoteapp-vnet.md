---
title: "Valider le réseau virtuel Azure à utiliser avec Azure RemoteApp | Microsoft Docs"
description: "Découvrez comment vous assurer que votre réseau virtuel Azure est prêt à être utilisé avec Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b573ba02-4587-4be5-9821-27bd891a73b2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 05c8a0ff04293947cec391b6467cc4adddb6a7b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="validate-the-azure-vnet-to-use-with-azure-remoteapp"></a><span data-ttu-id="cfc72-103">Validation du réseau virtuel Azure à utiliser avec Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="cfc72-103">Validate the Azure VNET to use with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cfc72-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="cfc72-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="cfc72-105">Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="cfc72-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="cfc72-106">Avant d'utiliser un réseau virtuel Azure avec Azure RemoteApp, vous pouvez valider le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="cfc72-106">Before you use an Azure VNET with Azure RemoteApp, you might want to validate the VNET.</span></span> <span data-ttu-id="cfc72-107">Cette action permet d'éviter les problèmes de connectivité.</span><span class="sxs-lookup"><span data-stu-id="cfc72-107">This helps prevent issues with connectivity.</span></span>

<span data-ttu-id="cfc72-108">Pour valider votre réseau virtuel Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="cfc72-108">To validate your Azure VNET, do the following:</span></span>

1. <span data-ttu-id="cfc72-109">Créez une machine virtuelle Azure dans le sous-réseau du réseau virtuel Azure que vous souhaitez utiliser avec Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="cfc72-109">Create an Azure virtual machine inside the subnet of the Azure VNET you want to use with Azure RemoteApp.</span></span>
2. <span data-ttu-id="cfc72-110">Connectez-vous à la machine virtuelle à l'aide de l’option **Connexion** sur le portail de gestion.</span><span class="sxs-lookup"><span data-stu-id="cfc72-110">Connect to that VM by using the **Connect** option in the management portal.</span></span>
3. <span data-ttu-id="cfc72-111">Associez la machine virtuelle au domaine que vous souhaitez utiliser avec Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="cfc72-111">Join the virtual machine to the same domain that you want to use with Azure RemoteApp.</span></span> <span data-ttu-id="cfc72-112">Si vous créez une collection hybride qui se connecte à votre réseau local, associez la machine virtuelle à votre domaine local.</span><span class="sxs-lookup"><span data-stu-id="cfc72-112">If you are creating a hybrid collection that connects to your on-premises network, join the virtual machine to your local domain.</span></span>

<span data-ttu-id="cfc72-113">Si l'opération réussit, le réseau virtuel Azure est prêt à être utilisé avec RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="cfc72-113">If this is successful, the Azure VNET is ready to use with RemoteApp.</span></span>

<span data-ttu-id="cfc72-114">Pour plus d'informations sur le flux de travail de bout en bout des collections hybrides, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="cfc72-114">For more information about the end-to-end hybrid collection workflow, see the following articles:</span></span>

* [<span data-ttu-id="cfc72-115">Comment planifier votre réseau virtuel pour Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="cfc72-115">How to plan your virtual network for Azure RemoteApp</span></span>](remoteapp-planvnet.md)
* [<span data-ttu-id="cfc72-116">Création d'une collection hybride</span><span class="sxs-lookup"><span data-stu-id="cfc72-116">Create a hybrid collection</span></span>](remoteapp-create-hybrid-deployment.md)
* [<span data-ttu-id="cfc72-117">Déployer une collection Azure RemoteApp sur votre Azure Virtual Network (avec prise en charge d’ExpressRoute)</span><span class="sxs-lookup"><span data-stu-id="cfc72-117">Deploy Azure RemoteApp collection to your Azure Virtual Network (with support for ExpressRoute)</span></span>](http://blogs.msdn.com/b/rds/archive/2015/04/23/deploy-azure-remoteapp-collection-to-your-azure-virtual-network-with-support-for-expressroute.aspx)

