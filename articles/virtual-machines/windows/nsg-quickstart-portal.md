---
title: "à l’aide d’aaaOpen ports tooa VM hello portail Azure | Documents Microsoft"
description: "Découvrez comment tooopen un port / créer un point de terminaison de tooyour machine virtuelle Windows à l’aide du modèle de déploiement du Gestionnaire de ressources hello Bonjour portail Azure"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: f7cf0319-5ee7-435e-8f94-c484bf5ee6f1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: aba789c65254651899aa688f256fe616c3d0126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-tooa-virtual-machine-with-hello-azure-portal"></a>Comment tooopen ports virtuels tooa avec hello portail Azure
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a>Commandes rapides
Vous pouvez également [effectuer ces étapes à l’aide d’Azure PowerShell](nsg-quickstart-powershell.md).

Créez d’abord votre Groupe de sécurité réseau. Sélectionnez un groupe de ressources dans le portail de hello, choisissez **ajouter**, puis recherchez et sélectionnez **groupe de sécurité réseau**:

![Ajouter un groupe de sécurité réseau](./media/nsg-quickstart-portal/add-nsg.png)

Entrez un nom pour votre groupe de sécurité réseau, sélectionnez ou créez un groupe de ressources, et sélectionnez un emplacement. Sélectionnez **Créer** quand vous avez terminé :

![Création d'un groupe de sécurité réseau](./media/nsg-quickstart-portal/create-nsg.png)

Sélectionnez un nouveau groupe de sécurité réseau. Sélectionnez « Entrant des règles de sécurité », puis hello **ajouter** bouton toocreate une règle :

![Ajouter une règle de trafic entrant](./media/nsg-quickstart-portal/add-inbound-rule.png)

Choisissez un commun **Service** à partir du menu déroulant de hello, tel que *HTTP*. Vous pouvez également sélectionner *personnalisé* tooprovide un toouse de port spécifique. Si vous le souhaitez, modifier la priorité de hello ou nom. ordre de hello dans lequel les règles sont appliquées - une valeur numérique hello inférieure hello affecte Hello priorité, hello antérieures hello règle est appliquée. Vous pouvez également sélectionner **avancé** haut hello cette tooenter écran spécifique à une source IP bloc ou plage de ports, par exemple. Lorsque vous êtes prêt, sélectionnez **OK** règle de hello toocreate :

![Créer une règle de trafic entrant](./media/nsg-quickstart-portal/create-inbound-rule.png)

L’étape finale consiste tooassociate groupe de sécurité de votre réseau avec un sous-réseau ou une interface réseau spécifique. Nous allons associer hello groupe de sécurité réseau à un sous-réseau. Sélectionnez **Sous-réseaux**, puis choisissez **Associer** :

![Associer un groupe de sécurité réseau à un sous-réseau](./media/nsg-quickstart-portal/associate-subnet.png)

Sélectionnez votre réseau virtuel, puis sous-réseau approprié de hello :

![Association d’un groupe de sécurité réseau à un réseau virtuel](./media/nsg-quickstart-portal/select-vnet-subnet.png)

Vous avez maintenant créé un groupe de sécurité réseau, créé une règle de trafic entrant qui autorise le trafic sur le port 80 et l’avez associé à un sous-réseau. Les machines virtuelles que vous vous connectez toothat sous-réseau sont accessibles sur le port 80.

## <a name="more-information-on-network-security-groups"></a>En savoir plus sur les groupes de sécurité réseau
Hello rapide commandes vous permettent de tooget haut et en cours d’exécution avec tooyour de flux de trafic VM. Groupes de sécurité réseau fournissent de nombreuses fonctionnalités et granularité pour contrôler les ressources tooyour accès. Découvrez plus d’informations sur la [création d’un groupe de sécurité réseau et de règles de liste de contrôle d’accès ici](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).

Pour les applications Web hautement disponibles, vous devez placer vos machines virtuelles derrière un équilibreur de charge Azure. équilibrage de charge Hello distribue tooVMs le trafic, avec un groupe de sécurité réseau qui fournit un filtrage du trafic. Pour plus d’informations, consultez [comment le solde tooload Linux virtual machines dans Azure toocreate une application hautement disponible](tutorial-load-balancer.md).

## <a name="next-steps"></a>Étapes suivantes
Dans cet exemple, vous avez créé un trafic de tooallow HTTP règle simple. Vous trouverez des informations sur la création d’environnements plus Bonjour suivant des articles :

* [Présentation d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [Présentation du groupe de sécurité réseau](../../virtual-network/virtual-networks-nsg.md)