---
title: "Injecter des données dans des machines virtuelles Windows sur Azure | Microsoft Docs"
description: "Cette rubrique explique comment injecter des données personnalisées dans une machine virtuelle Azure lors de la création de l’instance, et comment localiser les données personnalisées dans Windows ou Linux."
services: virtual-machines-windows
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 48759f76-eaa0-4202-ada0-706d3f9a9467
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: 7836577f16940b618a2912012ba8a8e7160980e8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="injecting-custom-data-into-an-azure-virtual-machine"></a><span data-ttu-id="7a293-103">Injection de données personnalisées dans une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="7a293-103">Injecting custom data into an Azure virtual machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="7a293-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7a293-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7a293-105">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="7a293-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="7a293-106">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7a293-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="7a293-107">Pour plus d’informations sur l’utilisation de l’extension de script personnalisé avec le modèle Resource Manager, suivez [ce lien](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7a293-107">For information about using the Custom Script Extension with the Resource Manager model, see [here](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-inject-custom-data](../../../../includes/virtual-machines-common-classic-inject-custom-data.md)]

