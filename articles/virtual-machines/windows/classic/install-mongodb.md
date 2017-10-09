---
title: aaaInstall MongoDB sur un ordinateur virtuel Windows Azure | Documents Microsoft
description: "Découvrez comment tooinstall MongoDB sur une machine virtuelle Azure est créé avec le modèle de déploiement classique hello exécutant Windows Server."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4095df41-bb69-4bbe-9c1c-70923b0d84ba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: iainfou
ms.openlocfilehash: aafd86b4c49c6a97ae8a1a2191ae375b6c47483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="13a7f-103">Installation de MongoDB sur une machine virtuelle Windows dans Azure</span><span class="sxs-lookup"><span data-stu-id="13a7f-103">Install MongoDB on a Windows VM in Azure</span></span>
> [!IMPORTANT]
> <span data-ttu-id="13a7f-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="13a7f-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="13a7f-105">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="13a7f-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="13a7f-106">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="13a7f-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="13a7f-107">tooinstall et configurer MongoDB à l’aide du modèle de déploiement du Gestionnaire de ressources hello, consultez [cet article](../install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="13a7f-107">tooinstall and configure MongoDB using hello Resource Manager deployment model, see [this article](../install-mongodb.md).</span></span>

<span data-ttu-id="13a7f-108">[MongoDB][MongoDB] est une base de données NoSQL open-source qui offre des performances élevées.</span><span class="sxs-lookup"><span data-stu-id="13a7f-108">[MongoDB][MongoDB] is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="13a7f-109">Cet article vous guide à travers de la création d’un serveur de Windows de machine virtuelle (VM) à l’aide de hello [portail Azure][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="13a7f-109">This article guides you through creating a Windows Server virtual machine (VM) using hello [Azure portal][AzurePortal].</span></span> <span data-ttu-id="13a7f-110">Ensuite, créer et attacher un toohello de disque de données machine virtuelle avant d’installer et de configuration MongoDB.</span><span class="sxs-lookup"><span data-stu-id="13a7f-110">You then create and attach a data disk toohello VM before installing and configuring MongoDB.</span></span> <span data-ttu-id="13a7f-111">Si vous avez une machine virtuelle existante dans Azure que vous aimeriez toouse, vous pouvez passer directement trop[installation et configuration MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="13a7f-111">If you have an existing VM in Azure that you would like toouse, you can jump straight too[installing and configuring MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span></span>

## <a name="create-a-virtual-machine-running-windows-server"></a><span data-ttu-id="13a7f-112">Création d’une machine virtuelle exécutant Windows Server</span><span class="sxs-lookup"><span data-stu-id="13a7f-112">Create a virtual machine running Windows Server</span></span>
<span data-ttu-id="13a7f-113">Suivez ces instructions de toocreate une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="13a7f-113">Follow these instructions toocreate a virtual machine.</span></span>

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> <span data-ttu-id="13a7f-114">Vous pouvez ajouter un point de terminaison pour MongoDB lors de la création d’ordinateur virtuel de hello et le configurer comme suit : en tant que nom **Mongo**, utilisez **TCP** comme protocole de hello et définissez les deux ports publics et privés hello trop**27017**.</span><span class="sxs-lookup"><span data-stu-id="13a7f-114">You can add an endpoint for MongoDB while creating hello virtual machine, and configure it as follows: name it as **Mongo**, use **TCP** as hello protocol, and set both hello public and private ports too**27017**.</span></span>
>
>

## <a name="attach-a-data-disk"></a><span data-ttu-id="13a7f-115">Association d’un disque de données</span><span class="sxs-lookup"><span data-stu-id="13a7f-115">Attach a data disk</span></span>
<span data-ttu-id="13a7f-116">stockage tooprovide pour l’ordinateur virtuel de hello, attacher un disque de données et l’initialiser pour que Windows puisse l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="13a7f-116">tooprovide storage for hello virtual machine, attach a data disk and then initialize it so that Windows can use it.</span></span> <span data-ttu-id="13a7f-117">Si vous disposez déjà d’un disque de données, vous pouvez attacher ce disque existant. Sinon, vous pouvez attacher un disque vide.</span><span class="sxs-lookup"><span data-stu-id="13a7f-117">If you already have a data disk, you can attach that existing disk, or you can attach an empty disk.</span></span>

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

<span data-ttu-id="13a7f-118">Pour obtenir des instructions sur l’initialisation de disque de hello, consultez « Comment : initialiser un nouveau disque de données dans Windows Server » dans [tooattach données de l’ordinateur virtuel Windows tooa disque](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="13a7f-118">For instructions on initializing hello disk, see "How to: Initialize a new data disk in Windows Server" in [How tooattach a data disk tooa Windows virtual machine](attach-disk.md).</span></span>

## <a name="install-and-run-mongodb-on-hello-virtual-machine"></a><span data-ttu-id="13a7f-119">Installer et exécuter MongoDB sur l’ordinateur virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="13a7f-119">Install and run MongoDB on hello virtual machine</span></span>
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a><span data-ttu-id="13a7f-120">Résumé</span><span class="sxs-lookup"><span data-stu-id="13a7f-120">Summary</span></span>
<span data-ttu-id="13a7f-121">Dans ce didacticiel, vous avez appris comment toocreate une machine virtuelle exécutant Windows Server, à distance connecter tooit et attacher un disque de données.</span><span class="sxs-lookup"><span data-stu-id="13a7f-121">In this tutorial, you learned how toocreate a virtual machine running Windows Server, remotely connect tooit, and attach a data disk.</span></span>  <span data-ttu-id="13a7f-122">Vous avez également appris tooinstall et configurer MongoDB sur l’ordinateur virtuel de basés sur Windows hello.</span><span class="sxs-lookup"><span data-stu-id="13a7f-122">You also learned how tooinstall and configure MongoDB on hello Windows-based virtual machine.</span></span> <span data-ttu-id="13a7f-123">Vous pouvez désormais accéder aux MongoDB sur l’ordinateur virtuel basé sur Windows hello, par suite hello rubriques Bonjour avancées [documentation MongoDB][MongoDocs].</span><span class="sxs-lookup"><span data-stu-id="13a7f-123">You can now access MongoDB on hello Windows-based virtual machine, by following hello advanced topics in hello [MongoDB documentation][MongoDocs].</span></span>

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/

