---
title: "Présentation de délégation DNS aaaAzure | Documents Microsoft"
description: "Comprendre comment délégation de domaine toochange et Azure DNS d’utiliser le nom de serveurs tooprovide domaine héberge."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: eaf2d2e345004b4d631e8d81d548b8ca23277d05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="delegation-of-dns-zones-with-azure-dns"></a>Délégation de zones DNS dans Azure DNS

DNS Azure vous permet de toohost une zone DNS et gérer les enregistrements DNS de hello pour un domaine dans Azure. Dans l’ordre pour les requêtes DNS pour un tooreach de domaine DNS d’Azure, domaine de hello a toobe déléguée tooAzure DNS dans le domaine parent hello. N’oubliez pas d’Azure DNS n’est pas de domaines hello. Cet article explique comment la délégation de domaine fonctionne et comment toodelegate tooAzure de domaines DNS.

## <a name="how-dns-delegation-works"></a>Fonctionnement de la délégation DNS

### <a name="domains-and-zones"></a>Zones et domaines

Hello Domain Name System est une hiérarchie de domaines. hiérarchie de Hello démarre à partir du domaine de « root » hello, dont le nom est simplement «**.**'.  Puis viennent les domaines de niveau supérieur, tels que « com », « net », « org », « uk » ou « jp ».  Vous trouvez ensuite les domaines de second niveau, comme « org.uk » ou « co.jp ».  Et ainsi de suite. domaines Hello Bonjour hiérarchie DNS sont hébergés à l’aide des zones DNS distinctes. Ces zones sont distribuées globalement, hébergé par les serveurs de noms DNS monde hello.

**Zone DNS** -un domaine est un nom unique dans hello Domain Name System, par exemple, « contoso.com ». Une zone DNS est toohost utilisé hello les enregistrements DNS pour un domaine particulier. Par exemple, le domaine hello « contoso.com » peut contenir plusieurs enregistrements DNS tels que « mail.contoso.com » (pour un serveur de messagerie) et « www.contoso.com » (pour un site Web).

Un **bureau d’enregistrement de domaines** est une société qui fournit des noms de domaine Internet. Il vérifie le domaine Internet de hello toouse est disponible et vous permettre de toopurchase il. Une fois que le nom de domaine hello est inscrit, vous êtes propriétaire de juridique de hello pour le nom de domaine hello. Si vous disposez déjà d’un domaine Internet, vous allez utiliser hello actuel domaine bureau d’enregistrement toodelegate tooAzure DNS.

toofind plus d’informations sur le propriétaire d’un nom de domaine donné, ou pour plus d’informations sur la façon de toobuy un domaine, consultez [gestion de domaine Internet dans Azure AD](https://msdn.microsoft.com/library/azure/hh969248.aspx).

### <a name="resolution-and-delegation"></a>Résolution et délégation

Deux types de serveur DNS sont disponibles :

* Un serveur DNS *faisant autorité* héberge les zones DNS. Il répond aux requêtes DNS pour les enregistrements de ces zones uniquement.
* Un serveur DNS *récursif* n’héberge pas de zones DNS. Il répond à toutes les requêtes DNS en appelant des données du hello toogather de serveurs DNS faisant autorité dont il a besoin.

Azure DNS fournit un service DNS faisant autorité.  Il ne fournit pas un service DNS récursif. Services de cloud computing et machines virtuelles dans Azure sont configuré automatiquement toouse un service DNS récursive qui est fourni séparément dans le cadre de l’infrastructure Azure. Pour plus d’informations sur comment toochange ces paramètres DNS, consultez [résolution de noms dans Azure](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

Clients DNS dans les ordinateurs ou appareils mobiles appellent généralement toutes les requêtes DNS hello les applications clientes doivent un tooperform de serveur DNS récursif.

Lorsqu’un serveur DNS récursif reçoit une requête pour un enregistrement DNS, tel que « www.contoso.com », il doit d’abord toofind hello nom serveur hébergement hello zone pour le domaine « contoso.com » de hello. serveur de noms toofind hello, il commence à des serveurs de noms racine hello et à partir de là, recherche les serveurs de noms hello hébergeant hello 'com' zone. Il interroge ensuite hello 'com' nom toofind hello nom serveurs hébergeant hello « contoso.com » zone.  Enfin, il est en mesure de tooquery ces serveurs de noms pour « www.contoso.com ».

Cette procédure est appelée la résolution du nom DNS de hello. Parler, la résolution DNS inclut des étapes supplémentaires, telles que les enregistrements CNAME suivantes, mais qui n’est pas important toounderstanding le fonctionnement de la délégation DNS.

Comment une zone parente 'point' toohello des serveurs de noms pour une zone enfant ? Elle utilise pour cela un type spécial d’enregistrement DNS appelé enregistrement NS (pour « serveur de noms »). Par exemple, zone racine de hello contient les enregistrements NS pour « com » et affiche les serveurs de noms hello pour la zone de « com » hello. À son tour, la zone de « com » hello contient des enregistrements NS pour « contoso.com », qui affiche les serveurs de noms hello pour la zone de « contoso.com » hello. Configurer les enregistrements NS hello pour une zone enfant dans une zone parente est appelé domaine de hello délégation.

Hello suivant image montre un exemple de requête DNS. partners.contoso.NET et hello contoso.net sont des zones DNS de Azure.

![Dns-nameserver](./media/dns-domain-delegation/image1.png)

1. Hello les demandes des clients `www.partners.contoso.net` à partir de leur serveur DNS local.
1. serveur DNS local de Hello n’a pas d’enregistrement de hello, il est un serveur de noms racine demande tootheir.
1. serveur de noms racine Hello n’a pas d’enregistrement de hello, mais il connaît l’adresse hello Hello `.net` le serveur, il fournit ce serveur DNS de toohello adresse
1. Hello DNS envoie hello demande toohello `.net` serveur de noms, il n’a pas hello enregistrement mais ne savez adresse hello hello contoso.net du serveur de noms. Dans ce cas, il s’agit d’une zone DNS hébergée dans Azure DNS.
1. zone de Hello `contoso.net` n’a pas d’enregistrement de hello mais connaît le nom du serveur hello de `partners.contoso.net` et répond avec qui. Dans ce cas, il s’agit d’une zone DNS hébergée dans Azure DNS.
1. demandes de serveur DNS de Hello en adresse IP hello `partners.contoso.net` de hello `partners.contoso.net` zone. Il contient l’enregistrement A de hello et répond avec l’adresse IP de hello.
1. serveur DNS de Hello fournit hello IP adresse toohello
1. Hello se connecte du site Web toohello `www.partners.contoso.net`.

Chaque délégation a en fait deux copies d’enregistrements NS de hello. l’une dans la zone parente de hello pointant toohello enfant et l’autre dans la zone enfant de hello lui-même. zone de 'contoso.net' Hello contient des enregistrements hello NS 'contoso.net' (dans les enregistrements NS du toohello ajout dans « net »). Ces enregistrements sont appelés des enregistrements NS faisant autoritées, et ils se trouvent au sommet de hello de zone enfant de hello.

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment trop[déléguer votre tooAzure de domaine DNS](dns-delegate-domain-azure-dns.md)

