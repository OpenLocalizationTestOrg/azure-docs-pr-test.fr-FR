---
title: aaaInstall MySQL sur un VM OpenSUSE | Documents Microsoft
description: En savoir plus tooinstall MySQL sur un ordinateur VMirtual de Linux OpenSUSE dans Azure.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1594e10e-c314-455a-9efb-a89441de364b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/19/2016
ms.author: cynthn
ms.openlocfilehash: 8f96d29f29cb9c466dd7fdaf92b378783fdaacd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-mysql-on-a-virtual-machine-running-opensuse-linux-in-azure"></a><span data-ttu-id="1ec70-103">Installation de MySQL sur une machine virtuelle exécutant OpenSUSE Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="1ec70-103">Install MySQL on a virtual machine running OpenSUSE Linux in Azure</span></span>
<span data-ttu-id="1ec70-104">[MySQL][MySQL] est une base de données SQL open source connue.</span><span class="sxs-lookup"><span data-stu-id="1ec70-104">[MySQL][MySQL] is a popular, open-source SQL database.</span></span> <span data-ttu-id="1ec70-105">Ce didacticiel vous montre comment toocreate une machine virtuelle exécutant OpenSUSE Linux installez ensuite MySQL.</span><span class="sxs-lookup"><span data-stu-id="1ec70-105">This tutorial shows you how toocreate a virtual machine running OpenSUSE Linux, then install MySQL.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="1ec70-106">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="1ec70-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1ec70-107">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="1ec70-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="1ec70-108">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="1ec70-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<br>

## <a name="create-a-virtual-machine-running-opensuse-linux"></a><span data-ttu-id="1ec70-109">Création d'une machine virtuelle exécutant OpenSUSE Linux</span><span class="sxs-lookup"><span data-stu-id="1ec70-109">Create a virtual machine running OpenSUSE Linux</span></span>
[!INCLUDE [create-and-configure-opensuse-vm-in-portal](../../../../includes/create-and-configure-opensuse-vm-in-portal.md)]

## <a name="install-and-run-mysql-on-hello-virtual-machine"></a><span data-ttu-id="1ec70-110">Installer et exécuter MySQL sur l’ordinateur virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="1ec70-110">Install and run MySQL on hello virtual machine</span></span>
[!INCLUDE [install-and-run-mysql-on-opensuse-vm](../../../../includes/install-and-run-mysql-on-opensuse-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="1ec70-111">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1ec70-111">Next steps</span></span>
<span data-ttu-id="1ec70-112">Pour plus d’informations sur MySQL, consultez hello [Documentation MySQL][MySQLDocs].</span><span class="sxs-lookup"><span data-stu-id="1ec70-112">For details about MySQL, see hello [MySQL Documentation][MySQLDocs].</span></span>

[MySQLDocs]:http://dev.mysql.com/doc/index-topic.html
[MySQL]:http://www.mysql.com

