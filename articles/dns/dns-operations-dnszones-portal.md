---
title: aaaManage DNS zones DNS de Azure - portail Azure | Documents Microsoft
description: "Vous pouvez gérer des zones DNS à l’aide de hello portail Azure. Cet article décrit comment tooupdate, supprimer et créer des zones DNS sur le système DNS Azure"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/18/2017
ms.author: gwallace
ms.openlocfilehash: 0d8ce302bb7126dfe8077a6f3e33418e16fcea64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-hello-azure-portal"></a>Comment les Zones DNS toomanage hello portail Azure

> [!div class="op_single_selector"]
> * [Portail](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)

Cet article explique comment toomanage votre DNS zones à l’aide de hello portail Azure. Vous pouvez également gérer vos zones DNS à l’aide de hello inter-plateformes [CLI d’Azure](dns-operations-dnszones-cli.md) ou hello Azure [PowerShell](dns-operations-dnszones.md).

## <a name="create-a-dns-zone"></a>Création d’une zone DNS

1. Se connecter toohello portail Azure
2. Dans le menu du Hub hello, cliquez sur, puis cliquez sur **Nouveau > mise en réseau >** puis cliquez sur **zone DNS** Panneau de zone DNS de créer tooopen hello.

    ![Zone DNS](./media/dns-operations-dnszones-portal/openzone650.png)

4. Sur hello **zone DNS de créer** panneau hello valeurs suivantes, puis entrez **créer**:


   | **Paramètre** | **Valeur** | **Détails** |
   |---|---|---|
   |**Name**|contoso.com|nom Hello de zone DNS de hello|
   |**Abonnement**|[Votre abonnement]|Sélectionnez une zone DNS d’abonnement toocreate hello dans.|
   |**Groupe de ressources**|**Créer :** contosoDNSRG|Créez un groupe de ressources. nom de groupe de ressources Hello doit être unique au sein de l’abonnement hello sélectionné. toolearn plus d’informations sur les groupes de ressources, lire hello [le Gestionnaire de ressources](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) l’article de vue d’ensemble.|
   |**Emplacement**|Ouest des États-Unis||

> [!NOTE]
> groupe de ressources Hello fait référence emplacement toohello hello du groupe de ressources et n’a aucun impact sur la zone DNS de hello. emplacement des zones DNS Hello est toujours « globaux » et n’est pas affiché.

## <a name="list-dns-zones"></a>Création de la liste des zones DNS

Dans l’hello portail Azure, accédez trop**davantage de services** > **réseau** > **zones DNS**. Chaque zone DNS est indépendante. Les informations telles que le nombre de jeux d’enregistrements et les serveurs de noms peuvent être consultés depuis cet aperçu. colonne de Hello **serveurs de noms** n’est pas dans la vue par défaut de hello, tooadd il clic **colonnes**, sélectionnez **serveurs de noms** et cliquez sur **fait**.

![liste des zones DNS](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a>Suppression d’une zone DNS

Accédez de zone DNS de tooa dans le portail de hello. Sur hello **zone DNS** panneau, cliquez sur **supprimer la zone**. Vous êtes invité à tooconfirm vous sont désireux de zone DNS de hello toodelete. Suppression d’une zone DNS supprime également tous les enregistrements de hello qui figurent dans la zone de hello.

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment toowork avec votre Zone DNS et les enregistrements en vous rendant sur [prise en main Azure DNS à l’aide de hello Azure portal](dns-getstarted-portal.md).
