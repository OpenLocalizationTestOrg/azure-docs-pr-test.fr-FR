---
title: aaaAzure Forum aux questions sur DNS | Documents Microsoft
description: Forum aux questions sur Azure DNS
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: jonatul
ms.openlocfilehash: 55006e9d8b311f1e94678eb9d35ce3448b936488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-faq"></a>FAQ Azure DNS

## <a name="about-azure-dns"></a>À propos d’Azure DNS

### <a name="what-is-azure-dns"></a>Présentation d’Azure DNS

Hello système de nom de domaine, ou DNS, est responsable de la traduction (ou la résolution de) un site Web ou un service name tooits adresse IP. Azure DNS est un service d'hébergement pour les domaines DNS et qui offre une résolution de noms à l'aide de l'infrastructure Microsoft Azure. En hébergeant vos domaines dans Azure, vous pouvez gérer votre serveur DNS les enregistrements à l’aide de hello même des informations d’identification, les API, outils et facturation en tant que vos autres services Azure.

Les domaines DNS dans Azure DNS sont hébergés sur un réseau global de serveurs de noms DNS. Nous utilisons Anycast mise en réseau afin que chaque requête DNS est reçu par le serveur DNS le plus proche disponible hello. Cette technique offre des performances élevées et une haute disponibilité pour votre domaine.

Hello service DNS Azure est basé sur le Gestionnaire de ressources Azure. Ainsi, il tire parti de fonctionnalités de Resource Manager telles que le contrôle d’accès en fonction du rôle, les journaux d’audit et le verrouillage de ressources. Vos domaines et les enregistrements peuvent être gérés via hello portail Azure, les applets de commande PowerShell de Azure et hello CLI d’Azure inter-plateformes. Applications qui requièrent la gestion DNS automatique peuvent intégrer service hello via hello API REST et les kits de développement logiciel.

### <a name="how-much-does-azure-dns-cost"></a>Combien coûte Azure DNS ?

modèle de facturation Azure DNS Hello repose sur nombre hello de zones DNS hébergées dans Azure DNS et de nombre de hello de requêtes DNS qu’ils reçoivent. Des remises sont proposées en fonction de l’utilisation.

Pour plus d’informations, consultez hello [DNS Azure page de tarification](https://azure.microsoft.com/pricing/details/dns/).

### <a name="what-is-hello-sla-for-azure-dns"></a>Quel est le contrat SLA de hello pour Azure DNS ?

Nous garantissons que les requêtes DNS valides reçoivent une réponse à partir d’au moins un serveur de nom DNS de Azure au moins 99,99 % de temps de hello.

Pour plus d’informations, consultez hello [page Azure DNS SLA](https://azure.microsoft.com/support/legal/sla/dns).

### <a name="what-is-a-dns-zone-is-it-hello-same-as-a-dns-domain"></a>Qu’est-ce qu’une « zone DNS » ? Est elle même hello comme un domaine DNS ? 

Un domaine est un nom unique dans le système de nom de domaine hello, par exemple, « contoso.com ».

Une zone DNS est toohost utilisé hello les enregistrements DNS pour un domaine particulier. Par exemple, hello domaine « contoso.com » peut contenir plusieurs enregistrements DNS, tels que « mail.contoso.com » (pour un serveur de messagerie) et « www.contoso.com » (pour un site web). Il sont hébergés dans la zone DNS hello « contoso.com ».

Un nom de domaine est *simplement un nom*, tandis qu’une zone DNS est une ressource de données contenant les enregistrements DNS de hello pour un nom de domaine. DNS Azure vous permet de toohost une zone DNS et gérer les enregistrements DNS de hello pour un domaine dans Azure. Il fournit également des serveurs de noms DNS requêtes DNS tooanswer hello Internet.

### <a name="do-i-need-toopurchase-a-dns-domain-name-toouse-azure-dns"></a>Toopurchase un toouse de nom de domaine DNS Azure DNS ai-je besoin ? 

Pas nécessairement.

Vous n’avez pas besoin de toopurchase un toohost domaine une zone DNS dans le système DNS Azure. Vous pouvez créer une zone DNS à tout moment sans propriétaire du nom de domaine hello. Requêtes DNS pour cette zone résoudra uniquement si elles sont dirigées serveurs DNS de Azure toohello affecté toohello zone.

Vous devez le nom de domaine hello toopurchase si vous souhaitez toolink votre zone DNS dans la hiérarchie DNS global hello – Cela permet les requêtes à partir de n’importe où dans hello world toofind votre zone DNS de DNS et répondre à vos enregistrements DNS.

## <a name="azure-dns-features"></a>Fonctionnalités d’Azure DNS

### <a name="does-azure-dns-support-dns-based-traffic-routing-or-endpoint-failover"></a>Azure DNS prend-il en charge le routage du trafic DNS ou le basculement du point de terminaison ?

Le routage du trafic DNS et le basculement du point de terminaison sont fournis par Azure Traffic Manager. Il s’agit d’un service Azure distinct qui peut être utilisé avec Azure DNS. Pour plus d’informations, consultez hello [présentation de Traffic Manager](../traffic-manager/traffic-manager-overview.md).

DNS Azure prend uniquement en charge des domaines DNS 'statiques', où chaque requête DNS pour un enregistrement DNS reçoit toujours hello d’hébergement même réponse DNS.

### <a name="does-azure-dns-support-domain-name-registration"></a>Azure DNS prend-il en charge l’inscription de nom de domaine ?

Non. Azure DNS ne prend actuellement pas en charge l'achat de noms de domaine. Si vous souhaitez toopurchase domaines, vous devez toouse un bureau d’enregistrement du nom de domaine de l’application tierce. bureau d’enregistrement Hello généralement des frais une petite annuel. les domaines Hello peuvent ensuite être hébergés dans Azure DNS pour la gestion des enregistrements DNS. Consultez [déléguer un tooAzure de domaine DNS](dns-domain-delegation.md) pour plus d’informations.

Il s’agit d’une fonctionnalité que nous suivons dans notre file d’attente de travaux en souffrance. Vous pouvez utiliser notre site de commentaires trop[inscrire votre prise en charge pour cette fonctionnalité](https://feedback.azure.com/forums/217313-networking/suggestions/4996615-azure-should-be-its-own-domain-registrar).

### <a name="does-azure-dns-support-private-domains"></a>Azure DNS prend-il en charge les domaines « privés » ?

Non. Azure DNS ne prend actuellement en charge que les domaines côté Internet.

Il s’agit d’une fonctionnalité que nous suivons dans notre file d’attente de travaux en souffrance. Vous pouvez utiliser notre site de commentaires trop[inscrire votre prise en charge pour cette fonctionnalité](https://feedback.azure.com/forums/217313-networking/suggestions/10737696-enable-split-dns-for-providing-both-public-and-int).

Pour plus d’informations sur les options DNS internes dans Azure, consultez [Résolution de noms pour les machines virtuelles et les instances de rôle](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

### <a name="does-azure-dns-support-dnssec"></a>Azure DNS prend-il en charge DNSSEC ?

Non. Azure DNS ne prend actuellement pas en charge DNSSEC.

Il s’agit d’une fonctionnalité que nous suivons dans notre file d’attente de travaux en souffrance. Vous pouvez utiliser notre site de commentaires trop[inscrire votre prise en charge pour cette fonctionnalité](https://feedback.azure.com/forums/217313-networking/suggestions/13284393-azure-dns-needs-dnssec-support).

### <a name="does-azure-dns-support-zone-transfers-axfrixfr"></a>Azure DNS prend-il en charge les transferts de zone (AXFR/IXFR) ?

Non. Azure DNS ne prend actuellement pas en charge les transferts de zone. Les zones DNS peuvent être [importé dans DNS Azure à l’aide de hello CLI d’Azure](dns-import-export.md). Enregistrements DNS peuvent être gérés via hello [portail de gestion Azure DNS](dns-operations-recordsets-portal.md), notre [API REST](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [applets de commande PowerShell](dns-operations-recordsets.md), ou [ Outil d’interface CLI](dns-operations-recordsets-cli.md).

Il s’agit d’une fonctionnalité que nous suivons dans notre file d’attente de travaux en souffrance. Vous pouvez utiliser notre site de commentaires trop[inscrire votre prise en charge pour cette fonctionnalité](https://feedback.azure.com/forums/217313-networking/suggestions/12925503-extend-azure-dns-to-support-zone-transfers-so-it-c).

### <a name="does-azure-dns-support-url-redirects"></a>Azure DNS prend-il en charge les redirections d’URL ?

Non. Services de redirection d’URL ne sont pas réellement un service DNS - qu’ils fonctionnent au niveau HTTP hello, et non au niveau du DNS hello. Certaines toobundle de fournisseurs DNS un service de redirection d’URL dans le cadre de leur offre globale. Ceci n’est actuellement pas pris en charge par Azure DNS.

Cette fonctionnalité est suivie dans notre file d’attente de travaux en souffrance. Vous pouvez utiliser notre site de commentaires trop[inscrire votre prise en charge pour cette fonctionnalité](https://feedback.azure.com/forums/217313-networking/suggestions/10109736-provide-a-301-permanent-redirect-service-for-ape).

## <a name="using-azure-dns"></a>Utilisation d’Azure DNS

### <a name="can-i-co-host-a-domain-using-azure-dns-and-another-dns-provider"></a>Puis-je co-héberger un domaine utilisant Azure DNS et un autre fournisseur DNS ?

Oui. Azure DNS prend en charge le co-hébergement de domaines avec d’autres services DNS.

toodo ainsi, vous devez les enregistrements hello NS toomodify pour le domaine hello (qui contrôle les fournisseurs de réception DNS interroge pour le domaine de hello) toopoint toohello des serveurs de deux fournisseurs de noms. Ces enregistrements NS doivent toobe modifié à 3 emplacements : dans le système DNS Azure, dans hello autre fournisseur et dans la zone parente de hello (généralement configuré via le Registre des noms de domaine hello). Pour plus d’informations sur la délégation DNS, consultez [Délégation de domaine DNS](dns-domain-delegation.md).

En outre, vous devez tooensure que les enregistrements DNS de hello pour le domaine de hello sont synchronisés entre les deux fournisseurs DNS. Azure DNS ne prend actuellement pas en charge les transferts de zone DNS. Vous devez toosynchronize les enregistrements DNS à l’aide soit hello [portail de gestion Azure DNS](dns-operations-recordsets-portal.md), notre [API REST](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [applets de commande PowerShell](dns-operations-recordsets.md) , ou [outil d’interface CLI](dns-operations-recordsets-cli.md).

### <a name="do-i-have-toodelegate-my-domain-tooall-4-azure-dns-name-servers"></a>Dois-je toodelegate mes serveurs de nom de domaine tooall 4 Azure DNS ?

Oui. DNS Azure affecte 4 serveurs de noms de zone DNS tooeach, pour la détection des erreurs et de résilience accrue. tooqualify pour hello contrat SLA de Azure DNS, vous devez toodelegate de vos serveurs de noms de domaine tooall 4.

### <a name="what-are-hello-usage-limits-for-azure-dns"></a>Quelles sont les limites d’utilisation de hello pour Azure DNS ?

Hello suivant les limites par défaut s’appliquent lors de l’utilisation d’Azure DNS :

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

### <a name="can-i-move-an-azure-dns-zone-between-resource-groups-or-between-subscriptions"></a>Puis-je déplacer une zone Azure DNS entre des groupes de ressources ou entre des abonnements ?

Oui. Les zones DNS peuvent être déplacées entre des groupes de ressources ou entre des abonnements.

Le déplacement d’une zone DNS n’a aucun impact sur les requêtes DNS. serveurs de noms Hello affectés toohello zone restent hello qu'identiques et les requêtes DNS sont traités comme d’habitude dans l’ensemble.

Pour plus d’informations et obtenir des instructions sur la façon de toomove les zones DNS, consultez [déplacer des ressources tooa nouveau groupe de ressources ou d’un abonnement](../azure-resource-manager/resource-group-move-resources.md).

### <a name="how-long-does-it-take-for-dns-changes-tootake-effect"></a>Combien de temps faut-il pour effet de tootake modifications DNS ?

Des zones DNS et les enregistrements DNS sont généralement répercutées sur les serveurs DNS de Azure hello rapidement, après quelques secondes.

Changer les enregistrements DNS tooexisting peuvent prendre un peu plus de temps, mais doivent toujours être reflétées sur les serveurs DNS de Azure hello pendant 60 secondes. Dans ce cas, DNS mise en cache en dehors d’Azure DNS (par les clients DNS et des programmes de résolution DNS récursive) peut également avoir un impact sur hello durée d’un toobe de modification DNS efficace. Cette durée du cache peut être contrôlée à l’aide de la propriété Time-To-Live (TTL) de hello de chaque jeu d’enregistrements.

### <a name="how-can-i-protect-my-dns-zones-against-accidental-deletion"></a>Comment puis-je protéger mes zones DNS contre une suppression accidentelle ?

DNS Azure est géré à l’aide du Gestionnaire de ressources Azure et les avantages de hello accéder aux fonctionnalités de contrôle de ce gestionnaire de ressources Azure fournit. Contrôle d’accès basé sur un rôle peut être utilisé toocontrol les utilisateurs qui ont accès en lecture ou écriture zones de tooDNS et jeux d’enregistrements. Verrous de ressources peuvent être appliqué tooprevent modifiés ou supprimés accidentellement des zones DNS et les jeux d’enregistrements.

Pour plus d’informations, consultez [Protection des zones et enregistrements DNS](dns-protect-zones-recordsets.md).

### <a name="how-do-i-set-up-spf-records-in-azure-dns"></a>Comment configurer des enregistrements SPF dans Azure DNS ?

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="how-do-i-set-up-an-international-domain-name-idn-in-azure-dns"></a>Comment configurer un nom de domaine international (IDN) dans Azure DNS ?

Les noms de domaines internationaux (IDN) encodent chaque nom DNS à l’aide de « [punycode](https://en.wikipedia.org/wiki/Punycode) ». Les requêtes DNS utilisent ces noms codés en punycode.

Vous pouvez configurer des noms de domaines internationaux (noms de domaines internationaux) dans le système DNS Azure par le premier nom de la zone hello lors de la conversion ou toopunycode du nom du jeu d’enregistrements. Azure DNS n’intègre actuellement pas la conversion de/en punycode.

## <a name="next-steps"></a>Étapes suivantes

[En savoir plus sur Azure DNS](dns-overview.md)
<br>
[En savoir plus sur les zones et enregistrements DNS](dns-zones-records.md)
<br>
[Prise en main d’Azure DNS](dns-getstarted-portal.md)

