---
title: "toouse de réseau virtuel Azure hello aaaValidate avec Azure RemoteApp | Documents Microsoft"
description: "Découvrez comment toomake que votre réseau virtuel Azure est prêt toouse avec Azure RemoteApp"
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
ms.openlocfilehash: 5587556c264356e6ab6039b983a38cb2b95ed268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-hello-azure-vnet-toouse-with-azure-remoteapp"></a><span data-ttu-id="8f8f4-103">Valider toouse de réseau virtuel Azure hello avec Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="8f8f4-103">Validate hello Azure VNET toouse with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8f8f4-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="8f8f4-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="8f8f4-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="8f8f4-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="8f8f4-106">Avant d’utiliser un réseau virtuel Azure avec Azure RemoteApp, vous pourriez toovalidate hello réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="8f8f4-106">Before you use an Azure VNET with Azure RemoteApp, you might want toovalidate hello VNET.</span></span> <span data-ttu-id="8f8f4-107">Cette action permet d'éviter les problèmes de connectivité.</span><span class="sxs-lookup"><span data-stu-id="8f8f4-107">This helps prevent issues with connectivity.</span></span>

<span data-ttu-id="8f8f4-108">toovalidate votre réseau virtuel Azure, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="8f8f4-108">toovalidate your Azure VNET, do hello following:</span></span>

1. <span data-ttu-id="8f8f4-109">Créer une machine virtuelle Azure à l’intérieur du sous-réseau hello Hello réseau virtuel de Azure vous souhaitez toouse avec Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8f8f4-109">Create an Azure virtual machine inside hello subnet of hello Azure VNET you want toouse with Azure RemoteApp.</span></span>
2. <span data-ttu-id="8f8f4-110">Se connecter toothat machine virtuelle à l’aide de hello **Connect** option hello portail de gestion.</span><span class="sxs-lookup"><span data-stu-id="8f8f4-110">Connect toothat VM by using hello **Connect** option in hello management portal.</span></span>
3. <span data-ttu-id="8f8f4-111">Jointure toohello de machine virtuelle hello même domaine que vous souhaitez toouse avec Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8f8f4-111">Join hello virtual machine toohello same domain that you want toouse with Azure RemoteApp.</span></span> <span data-ttu-id="8f8f4-112">Si vous créez une collection hybride qui connecte le réseau local de tooyour, joignez hello machine virtuelle tooyour dans le domaine local.</span><span class="sxs-lookup"><span data-stu-id="8f8f4-112">If you are creating a hybrid collection that connects tooyour on-premises network, join hello virtual machine tooyour local domain.</span></span>

<span data-ttu-id="8f8f4-113">Si l’opération réussit, hello réseau virtuel Azure est prêt toouse avec RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8f8f4-113">If this is successful, hello Azure VNET is ready toouse with RemoteApp.</span></span>

<span data-ttu-id="8f8f4-114">Pour plus d’informations sur les flux de travail de collection hello hybride de bout en bout, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="8f8f4-114">For more information about hello end-to-end hybrid collection workflow, see hello following articles:</span></span>

* [<span data-ttu-id="8f8f4-115">Comment tooplan votre réseau virtuel pour Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="8f8f4-115">How tooplan your virtual network for Azure RemoteApp</span></span>](remoteapp-planvnet.md)
* [<span data-ttu-id="8f8f4-116">Création d'une collection hybride</span><span class="sxs-lookup"><span data-stu-id="8f8f4-116">Create a hybrid collection</span></span>](remoteapp-create-hybrid-deployment.md)
* [<span data-ttu-id="8f8f4-117">Déployer Azure RemoteApp collection tooyour réseau virtuel Azure (avec prise en charge pour ExpressRoute)</span><span class="sxs-lookup"><span data-stu-id="8f8f4-117">Deploy Azure RemoteApp collection tooyour Azure Virtual Network (with support for ExpressRoute)</span></span>](http://blogs.msdn.com/b/rds/archive/2015/04/23/deploy-azure-remoteapp-collection-to-your-azure-virtual-network-with-support-for-expressroute.aspx)

