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
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a>Installation de MongoDB sur une machine virtuelle Windows dans Azure
> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).  Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. tooinstall et configurer MongoDB à l’aide du modèle de déploiement du Gestionnaire de ressources hello, consultez [cet article](../install-mongodb.md).

[MongoDB][MongoDB] est une base de données NoSQL open-source qui offre des performances élevées. Cet article vous guide à travers de la création d’un serveur de Windows de machine virtuelle (VM) à l’aide de hello [portail Azure][AzurePortal]. Ensuite, créer et attacher un toohello de disque de données machine virtuelle avant d’installer et de configuration MongoDB. Si vous avez une machine virtuelle existante dans Azure que vous aimeriez toouse, vous pouvez passer directement trop[installation et configuration MongoDB](#install-and-run-mongodb-on-the-virtual-machine).

## <a name="create-a-virtual-machine-running-windows-server"></a>Création d’une machine virtuelle exécutant Windows Server
Suivez ces instructions de toocreate une machine virtuelle.

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> Vous pouvez ajouter un point de terminaison pour MongoDB lors de la création d’ordinateur virtuel de hello et le configurer comme suit : en tant que nom **Mongo**, utilisez **TCP** comme protocole de hello et définissez les deux ports publics et privés hello trop**27017**.
>
>

## <a name="attach-a-data-disk"></a>Association d’un disque de données
stockage tooprovide pour l’ordinateur virtuel de hello, attacher un disque de données et l’initialiser pour que Windows puisse l’utiliser. Si vous disposez déjà d’un disque de données, vous pouvez attacher ce disque existant. Sinon, vous pouvez attacher un disque vide.

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

Pour obtenir des instructions sur l’initialisation de disque de hello, consultez « Comment : initialiser un nouveau disque de données dans Windows Server » dans [tooattach données de l’ordinateur virtuel Windows tooa disque](attach-disk.md).

## <a name="install-and-run-mongodb-on-hello-virtual-machine"></a>Installer et exécuter MongoDB sur l’ordinateur virtuel de hello
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a>Résumé
Dans ce didacticiel, vous avez appris comment toocreate une machine virtuelle exécutant Windows Server, à distance connecter tooit et attacher un disque de données.  Vous avez également appris tooinstall et configurer MongoDB sur l’ordinateur virtuel de basés sur Windows hello. Vous pouvez désormais accéder aux MongoDB sur l’ordinateur virtuel basé sur Windows hello, par suite hello rubriques Bonjour avancées [documentation MongoDB][MongoDocs].

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/

