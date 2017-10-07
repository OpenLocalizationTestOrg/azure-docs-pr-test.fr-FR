---
title: aaaOverview de DNS Azure | Documents Microsoft
description: "Vue d’ensemble des services d’hébergement DNS sur Microsoft Azure. Héberger votre domaine sur Microsoft Azure"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 68747a0d-b358-4b8e-b5e2-e2570745ec3f
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: gwallace
ms.openlocfilehash: a10f87c488356469e9c04aabde31129049563891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-overview"></a>Vue d’ensemble d’Azure DNS

Hello système de nom de domaine, ou DNS, est responsable de la traduction (ou la résolution de) un site Web ou un service name tooits adresse IP. Azure DNS est un service d'hébergement pour les domaines DNS et qui offre une résolution de noms à l'aide de l'infrastructure Microsoft Azure. En hébergeant vos domaines dans Azure, vous pouvez gérer votre serveur DNS les enregistrements à l’aide de hello même des informations d’identification, les API, outils et facturation en tant que vos autres services Azure.

![Vue d’ensemble de DNS](./media/dns-overview/scenario.png)

## <a name="features"></a>Caractéristiques

* **Fiabilité et performances** : les domaines DNS dans Azure DNS sont hébergés sur un réseau global de serveurs de noms DNS. Nous utilisons Anycast mise en réseau afin que chaque requête DNS est reçu par le serveur DNS le plus proche disponible hello. Cette technique offre des performances élevées et une haute disponibilité pour votre domaine.

* **Intégration transparente** -service DNS Azure de hello peut être utilisé toomanage enregistrements DNS pour vos services Azure et peut être utilisé tooprovide DNS pour vos ressources externes ainsi. Azure DNS est intégré dans hello portail Azure et utilise hello les mêmes informations d’identification, la facturation et le contrat de prise en charge en tant que vos autres services Azure.

* **Sécurité** -hello service DNS Azure est basé sur le Gestionnaire de ressources Azure. Ainsi, il tire parti de fonctionnalités de Resource Manager telles que le contrôle d’accès en fonction du rôle, les journaux d’audit et le verrouillage de ressources. Vos domaines et les enregistrements peuvent être gérés via hello portail Azure, les applets de commande PowerShell de Azure et hello CLI d’Azure inter-plateformes. Applications qui requièrent la gestion DNS automatique peuvent intégrer service hello via hello API REST et les kits de développement logiciel.

Azure DNS ne prend actuellement pas en charge l'achat de noms de domaine. Si vous souhaitez toopurchase domaines, vous devez toouse un bureau d’enregistrement du nom de domaine de l’application tierce. bureau d’enregistrement Hello généralement des frais une petite annuel. les domaines Hello peuvent ensuite être hébergés dans Azure DNS pour la gestion des enregistrements DNS. Consultez [déléguer un tooAzure de domaine DNS](dns-domain-delegation.md) pour plus d’informations.

## <a name="pricing"></a>Tarification

Facturation de DNS est basée sur le nombre de hello de zones DNS hébergées dans Azure et en nombre hello de requêtes DNS. toolearn plus d’informations sur la tarification visite [de la tarification Azure DNS](https://azure.microsoft.com/pricing/details/dns/).

## <a name="faq"></a>Forum Aux Questions

Pour les questions fréquemment posées sur le système DNS d’Azure, consultez hello [le Forum aux questions sur Azure DNS](dns-faq.md).

## <a name="next-steps"></a>Étapes suivantes

Obteniez plus d’informations sur les zones et enregistrements DNS en consultant : [Vue d’ensemble des enregistrements et zones DNS](dns-zones-records.md).

Découvrez comment trop[créer une zone DNS](./dns-getstarted-create-dnszone-portal.md) dans Azure DNS.

En savoir plus sur certaines des hello autre clé [fonctionnalités de réseau](../networking/networking-overview.md) de Azure.

