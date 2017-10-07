---
title: "aaaGet main DNS Azure à l’aide de hello portail Azure | Documents Microsoft"
description: "Découvrez comment toocreate DNS zone et cet enregistrement dans le système DNS Azure. Ceci est un toocreate guide pas à pas et que vous gérez votre première zone DNS et un enregistrement à l’aide de hello portail Azure."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 5cea01d840d794001cccac64defed8b329d948db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-hello-azure-portal"></a>Prise en main Azure DNS à l’aide de hello portail Azure

> [!div class="op_single_selector"]
> * [Portail Azure](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Azure CLI 1.0](dns-getstarted-cli-nodejs.md)
> * [Azure CLI 2.0](dns-getstarted-cli.md)

Cet article vous assiste hello étapes toocreate votre première zone DNS et un enregistrement à l’aide de hello portail Azure. Vous pouvez également effectuer ces étapes à l’aide d’Azure PowerShell ou hello CLI d’Azure inter-plateformes.

Une zone DNS est toohost utilisé hello les enregistrements DNS pour un domaine particulier. toostart hébergeant votre domaine dans le système DNS Azure, vous devez toocreate une zone DNS pour ce nom de domaine. Chaque enregistrement DNS pour votre domaine est ensuite créé à l’intérieur de cette zone DNS. Enfin, toopublish votre serveur DNS de la zone toohello Internet, vous avez besoin de serveurs de noms tooconfigure hello pour le domaine de hello. Chacune de ces étapes est décrite dans hello comme suit.

## <a name="create-a-dns-zone"></a>Création d’une zone DNS

1. Se connecter toohello portail Azure
2. Dans le menu du Hub hello, cliquez sur, puis cliquez sur **Nouveau > mise en réseau >** puis cliquez sur **zone DNS** Panneau de zone DNS de créer tooopen hello.

    ![Zone DNS](./media/dns-getstarted-portal/openzone650.png)

4. Sur hello **zone DNS de créer** panneau hello valeurs suivantes, puis entrez **créer**:


   | **Paramètre** | **Valeur** | **Détails** |
   |---|---|---|
   |**Name**|contoso.com|nom Hello de zone DNS de hello|
   |**Abonnement**|[Votre abonnement]|Sélectionnez une zone DNS d’abonnement toocreate hello dans.|
   |**Groupe de ressources**|**Créer :** contosoDNSRG|Créez un groupe de ressources. nom de groupe de ressources Hello doit être unique au sein de l’abonnement hello sélectionné. toolearn plus d’informations sur les groupes de ressources, lire hello [le Gestionnaire de ressources](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) l’article de vue d’ensemble.|
   |**Emplacement**|Ouest des États-Unis||

> [!NOTE]
> groupe de ressources Hello fait référence emplacement toohello hello du groupe de ressources et n’a aucun impact sur la zone DNS de hello. emplacement des zones DNS Hello est toujours « globaux » et n’est pas affiché.

## <a name="create-a-dns-record"></a>Créer un enregistrement DNS

Hello exemple suivant vous guide hello processus de création de nouveaux enregistrement de « A ». Pour d’autres types d’enregistrements et les enregistrements existants de toomodify, consultez [enregistrements DNS de gérer et jeux d’enregistrements à l’aide de portail Azure hello](dns-operations-recordsets-portal.md). 

1. Créé par hello Zone DNS Bonjour Azure portal **favoris** volet, cliquez sur **toutes les ressources**. Cliquez sur hello **contoso.com** de zone DNS Bonjour toutes les lames de ressources. Si l’abonnement hello déjà sélectionné comporte plusieurs ressources, vous pouvez entrer **contoso.com** Bonjour **filtrer par nom...** zone tooeasily accéder à la Zone DNS de hello.

1. En haut de hello Hello **zone DNS** panneau, sélectionnez **+ enregistrer ensemble** tooopen hello **ajouter le jeu d’enregistrements** panneau.

1. Sur hello **ajouter le jeu d’enregistrements** panneau, entrez hello valeurs suivantes, puis cliquez sur **OK**. Dans cet exemple, vous créez un enregistrement A.

   |**Paramètre** | **Valeur** | **Détails** |
   |---|---|---|
   |**Name**|www|Nom de l’enregistrement de hello|
   |**Type**|A| Type de toocreate d’enregistrement DNS, les valeurs acceptables sont A, AAAA, CNAME, MX, NS, SRV, TXT et PTR.  Pour plus d’informations sur les types d’enregistrement, voir [Aperçu des zones DNS et des enregistrements](dns-zones-records.md)|
   |**TTL**|1|Durée de vie de la requête DNS hello.|
   |**Unité de durée de vie**|Heures|Mesure de temps pour la durée de vie.|
   |**Adresse IP**|ipAddressValue| Cette valeur est l’adresse IP hello correspondant à un enregistrement DNS hello.|

## <a name="view-records"></a>Affichage des enregistrements

Dans la partie inférieure de hello du Panneau de zone DNS hello, vous pouvez voir des enregistrements hello pour la zone DNS de hello. Vous devez voir hello enregistrements par défaut DNS et SOA, qui sont créées dans chaque zone, ainsi que les nouveaux enregistrements que vous avez créé.

![zone](./media/dns-getstarted-portal/viewzone500.png)


## <a name="update-name-servers"></a>Mettre à jour les serveurs de noms

Une fois que vous êtes satisfait que votre zone DNS et les enregistrements ont été configurées correctement, vous devez tooconfigure votre nom de domaine toouse serveurs DNS de Azure hello. Cela permet à d’autres utilisateurs sur hello Internet toofind vos enregistrements DNS.

serveurs de noms Hello pour votre zone figurent hello portail Azure :

![zone](./media/dns-getstarted-portal/viewzonens500.png)

Ces serveurs de noms doivent être configurés avec le Registre des noms de domaine hello (où vous avez acheté nom de domaine hello). Votre bureau d’enregistrement offre tooset d’option hello des serveurs de noms hello pour le domaine de hello. Pour plus d’informations, consultez [déléguer votre tooAzure de domaine DNS](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Supprimer toutes les ressources

toodelete toutes les ressources créées dans cet article, hello complète comme suit :

1. Bonjour Azure portal **favoris** volet, cliquez sur **toutes les ressources**. Cliquez sur hello **MyResourceGroup** groupe de ressources Bonjour toutes les lames de ressources. Si l’abonnement hello déjà sélectionné comporte plusieurs ressources, vous pouvez entrer **MyResourceGroup** Bonjour **filtrer par nom...** groupe de ressources boîte tooeasily accès hello.
1. Bonjour **MyResourceGroup** panneau, cliquez sur hello **supprimer** bouton.
1. Hello portail requiert vous tootype hello nom du tooconfirm de groupe de ressources hello que vous souhaitez toodelete il. Cliquez sur **supprimer**, Type *MyResourceGroup* pour le nom du groupe de ressources de hello, puis cliquez sur **supprimer**. La suppression d’un groupe de ressources supprime toutes les ressources dans le groupe de ressources hello, toujours que tooconfirm contenu hello d’un groupe de ressources avant de le supprimer. portail de Hello supprime toutes les ressources contenues dans le groupe de ressources hello, puis supprime le groupe de ressources hello lui-même. Cette opération prend plusieurs minutes.


## <a name="next-steps"></a>Étapes suivantes

toolearn en savoir plus sur Azure DNS, consultez [vue d’ensemble de DNS Azure](dns-overview.md).

toolearn savoir plus sur la gestion des enregistrements DNS dans le système DNS Azure, consultez [enregistrements DNS de gérer et jeux d’enregistrements à l’aide de portail Azure hello](dns-operations-recordsets-portal.md).

