---
title: "aaaConnect tooAzure Data Lake Store à partir de réseaux virtuels | Documents Microsoft"
description: "Se connecter tooAzure Data Lake Store à partir de réseaux virtuels Azure"
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 683fcfdc-cf93-46c3-b2d2-5cb79f5e9ea5
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: c695dcf49fe4e1a87a90729cf085a938f3b51fe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="access-azure-data-lake-store-from-vms-within-an-azure-vnet"></a>Accéder à Azure Data Lake Store à partir de machines virtuelles au sein d’un réseau virtuel Azure
Azure Data Lake Store est un service PaaS qui s’exécute sur des adresses IP Internet publiques. N’importe quel serveur qui peut se connecter peut Internet public de toohello généralement se connecter tooAzure Data Lake Store points de terminaison. Par défaut, toutes les machines virtuelles qui se trouvent dans des réseaux virtuels Azure peuvent accéder à Internet de hello et peuvent donc accéder à Azure Data Lake Store. Toutefois, il est de machines virtuelles de tooconfigure possibles dans un toonot de réseau virtuel ont accès toohello Internet. Pour ces ordinateurs virtuels, accès tooAzure Data Lake Store est restreint. Bloquer l’accès Internet public pour les machines virtuelles dans des réseaux virtuels Azure peut être effectuée à l’aide de l’approche de hello.

* En configurant des groupes de sécurité réseau (NSG)
* En configurant des itinéraires définis par l’utilisateur
* En échangeant des routes via BGP (industrie standard protocole de routage dynamique) lorsque ExpressRoute est utilisé à ce bloc accéder toohello Internet

Dans cet article, vous allez apprendre comment tooenable accéder toohello Azure Data Lake Store à partir de machines virtuelles Azure qui ont été restreints tooaccess ressources à l’aide d’une des trois méthodes de hello répertoriés ci-dessus.

## <a name="enabling-connectivity-tooazure-data-lake-store-from-vms-with-restricted-connectivity"></a>L’activation de la connectivité tooAzure Data Lake Store à partir d’ordinateurs virtuels avec une connectivité limitée
Magasin de Azure Data Lake tooaccess à partir de ces ordinateurs virtuels, vous devez les configurer une adresse IP de tooaccess hello où hello compte Azure Data Lake Store est disponible. Vous pouvez identifier les adresses IP de hello pour vos comptes Data Lake Store par la résolution de noms DNS de hello de vos comptes (`<account>.azuredatalakestore.net`). Pour ce faire, vous pouvez utiliser des outils tels que **nslookup**. Ouvrez une invite de commandes sur votre ordinateur et exécutez hello commande suivante.

    nslookup mydatastore.azuredatalakestore.net

sortie de Hello ressemble au suivant de hello. Hello valeur contre **adresse** propriété est l’adresse IP de hello associé à votre compte Data Lake Store.

    Non-authoritative answer:
    Name:    1434ceb1-3a4b-4bc0-9c69-a0823fd69bba-mydatastore.projectcabostore.net
    Address:  104.44.88.112
    Aliases:  mydatastore.azuredatalakestore.net


### <a name="enabling-connectivity-from-vms-restricted-by-using-nsg"></a>Activation de la connectivité à partir de machines virtuelles restreintes à l’aide d’un groupe de sécurité réseau
Lorsqu’une règle de groupe de sécurité réseau est utilisée tooblock accéder toohello Internet, vous pouvez ensuite créer un autre groupe de sécurité réseau qui permet l’accès toohello adresse IP du magasin lac de données. Pour plus d’informations sur les règles de groupe de sécurité réseau, consultez [What is a Network Security Group?](../virtual-network/virtual-networks-nsg.md) (Qu’est-ce qu’un groupe de sécurité réseau ?). Pour obtenir des instructions sur les groupes de sécurité réseau toocreate voir [comment toomanage groupes de sécurité réseau à l’aide de hello Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).

### <a name="enabling-connectivity-from-vms-restricted-by-using-udr-or-expressroute"></a>Activation de la connectivité à partir de machines virtuelles restreintes à l’aide d’un itinéraire défini par l’utilisateur ou d’ExpressRoute
Lorsque les itinéraires, soit UDRs ou des itinéraires BGP-échangés, sont utilisés tooblock accès toohello Internet, un itinéraire spéciale doit toobe configuré de sorte que les machines virtuelles dans ces sous-réseaux peuvent accéder à des points de terminaison Data Lake Store. Pour plus d’informations, consultez [Présentation des itinéraires définis par l’utilisateur](../virtual-network/virtual-networks-udr-overview.md). Pour obtenir des instructions sur la création d’itinéraires définis par l’utilisateur, consultez [Création d’itinéraires définis par l’utilisateur (UDR) dans Resource Manager](../virtual-network/virtual-network-create-udr-arm-ps.md).

### <a name="enabling-connectivity-from-vms-restricted-by-using-expressroute"></a>Activation de la connectivité à partir de machines virtuelles restreintes à l’aide d’ExpressRoute
Lorsqu’un circuit ExpressRoute est configuré, hello sur des serveurs locaux peuvent accéder à Data Lake Store via l’homologation publique. Pour plus d’informations sur la configuration d’ExpressRoute pour l’appairage public, consultez [Forum Aux Questions ExpressRoute](../expressroute/expressroute-faqs.md).

## <a name="see-also"></a>Voir aussi
* [Présentation d'Azure Data Lake Store](data-lake-store-overview.md)
* [Sécurisation des données stockées dans Azure Data Lake Store](data-lake-store-security-overview.md)

