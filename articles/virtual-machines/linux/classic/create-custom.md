---
title: "un classique de machine virtuelle Linux à l’aide d’aaaCreate hello Azure CLI 1.0 | Documents Microsoft"
description: "Découvrez comment toocreate une machine virtuelle Linux à l’aide de hello Azure CLI 1.0 hello modèle de déploiement classique"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: f8071a2e-ed91-4f77-87d9-519a37e5364f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 5c3c54e5d1444a79e8e609c76d04a3a621c8d03f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-classic-linux-vm-with-hello-azure-cli-10"></a><span data-ttu-id="a2888-103">Comment tooCreate un classique de machine virtuelle Linux avec hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a2888-103">How tooCreate a Classic Linux VM with hello Azure CLI 1.0</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="a2888-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a2888-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a2888-105">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="a2888-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="a2888-106">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="a2888-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="a2888-107">Pour la version du Gestionnaire de ressources hello, consultez [ici](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a2888-107">For hello Resource Manager version, see [here](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="a2888-108">Cette rubrique décrit comment toocreate une machine virtuelle de Linux (VM) à l’aide de hello Azure CLI 1.0 hello modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="a2888-108">This topic describes how toocreate a Linux virtual machine (VM) with hello Azure CLI 1.0 using hello Classic deployment model.</span></span> <span data-ttu-id="a2888-109">Nous utilisons une image Linux à partir de hello disponible **IMAGES** sur Azure.</span><span class="sxs-lookup"><span data-stu-id="a2888-109">We use a Linux image from hello available **IMAGES** on Azure.</span></span> <span data-ttu-id="a2888-110">commandes Hello Azure CLI 1.0 donnent hello suivant les choix de configuration, entre autres :</span><span class="sxs-lookup"><span data-stu-id="a2888-110">hello Azure CLI 1.0 commands give hello following configuration choices, among others:</span></span>

* <span data-ttu-id="a2888-111">Connexion hello tooa virtuel réseau d’ordinateurs virtuels</span><span class="sxs-lookup"><span data-stu-id="a2888-111">Connecting hello VM tooa virtual network</span></span>
* <span data-ttu-id="a2888-112">Ajout de service cloud existant de hello VM tooan</span><span class="sxs-lookup"><span data-stu-id="a2888-112">Adding hello VM tooan existing cloud service</span></span>
* <span data-ttu-id="a2888-113">Ajouter le compte de stockage existant hello VM tooan</span><span class="sxs-lookup"><span data-stu-id="a2888-113">Adding hello VM tooan existing storage account</span></span>
* <span data-ttu-id="a2888-114">Ajout de machine virtuelle hello tooan à haute disponibilité ou l’emplacement</span><span class="sxs-lookup"><span data-stu-id="a2888-114">Adding hello VM tooan availability set or location</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a2888-115">Si vous souhaitez que votre toouse de machine virtuelle un réseau virtuel pour pouvoir vous connecter tooit directement par nom d’hôte ou configurer des connexions entre différents locaux, assurez-vous que vous spécifiez le réseau virtuel de hello lorsque vous créez hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a2888-115">If you want your VM toouse a virtual network so you can connect tooit directly by hostname or set up cross-premises connections, make sure you specify hello virtual network when you create hello VM.</span></span> <span data-ttu-id="a2888-116">Une machine virtuelle peut être configurée toojoin un réseau virtuel uniquement lorsque vous créez hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a2888-116">A VM can be configured toojoin a virtual network only when you create hello VM.</span></span> <span data-ttu-id="a2888-117">Pour plus d’informations sur les réseaux virtuels, consultez la page [Présentation du réseau virtuel Azure](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span><span class="sxs-lookup"><span data-stu-id="a2888-117">For details on virtual networks, see [Azure Virtual Network Overview](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span></span>
> 
> 

## <a name="how-toocreate-a-linux-vm-using-hello-classic-deployment-model"></a><span data-ttu-id="a2888-118">Comment toocreate un VM Linux à l’aide de hello modèle de déploiement classique</span><span class="sxs-lookup"><span data-stu-id="a2888-118">How toocreate a Linux VM using hello Classic deployment model</span></span>
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

