---
title: "aaaDNS Zones et enregistrements présentation - DNS Azure | Documents Microsoft"
description: "Vue d’ensemble de la prise en charge de l’hébergement d’enregistrements et zones DNS dans le DNS Microsoft Azure."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: be4580d7-aa1b-4b6b-89a3-0991c0cda897
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: jonatul
ms.openlocfilehash: f214c3e2e810a80a000281820acd35f0aaf5a7e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-dns-zones-and-records"></a>Vue d’ensemble des enregistrements et des zones DNS

Cette page décrit les concepts clés de hello de domaines, les zones DNS, les enregistrements DNS et jeux d’enregistrements et comment elles sont prises en charge dans le système DNS Azure.

## <a name="domain-names"></a>Noms de domaine

Hello Domain Name System est une hiérarchie de domaines. hiérarchie de Hello démarre à partir du domaine de « root » hello, dont le nom est simplement «**.**'.  Puis viennent les domaines de niveau supérieur, tels que « com », « net », « org », « uk » ou « jp ».  Vous trouvez ensuite les domaines de second niveau, comme « org.uk » ou « co.jp ». domaines Hello dans la hiérarchie de hello DNS sont distribuées globalement, hébergé par les serveurs de noms DNS monde hello.

Un enregistrement de domaines est une organisation qui vous permet de toopurchase un nom de domaine, par exemple, « contoso.com ».  Achat d’un domaine donne nom hello de droite toocontrol hello hiérarchie DNS sous ce nom, par exemple vous autorisez le site web entreprise toodirect hello nom « www.contoso.com » tooyour. bureau d’enregistrement Hello peut héberger le domaine hello dans ses propres serveurs de noms à votre place, ou vous toospecify les serveurs d’autre nom.

DNS Azure fournit une infrastructure de serveur nom distribuée globalement, haute disponibilité, que vous pouvez utiliser toohost votre domaine. En hébergeant vos domaines dans Azure DNS, vous pouvez gérer vos enregistrements DNS avec hello même informations d’identification, API, outils, la facturation et la prise en charge en tant que vos autres services Azure.

Azure DNS ne prend actuellement pas en charge l'achat de noms de domaine. Si vous voulez toopurchase un nom de domaine, vous devez toouse un bureau d’enregistrement du nom de domaine de l’application tierce. bureau d’enregistrement Hello généralement des frais une petite annuel. les domaines Hello peuvent ensuite être hébergés dans Azure DNS pour la gestion des enregistrements DNS. Consultez [déléguer un tooAzure de domaine DNS](dns-domain-delegation.md) pour plus d’informations.

## <a name="dns-zones"></a>Zones DNS

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="dns-records"></a>Enregistrements DNS

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

### <a name="time-to-live"></a>Durée de vie

heure de Hello toolive ou durée de vie, spécifie la durée pendant laquelle chaque enregistrement est mis en cache par les clients avant interrogé de nouveau. Bonjour exemple ci-dessus, hello durée de vie est 3 600 secondes ou 1 heure.

Dans le système DNS Azure, hello durée de vie est spécifiée pour le jeu d’enregistrements hello, pas pour chaque enregistrement, par conséquent, hello même valeur est utilisée pour tous les enregistrements au sein de cet enregistrement défini.  Vous pouvez spécifier une valeur de durée de vie quelconque comprise entre 1 et 2 147 483 647 secondes.

### <a name="wildcard-records"></a>Enregistrements génériques

Azure DNS prend en charge les [enregistrements génériques](https://en.wikipedia.org/wiki/Wildcard_DNS_record). Les enregistrements de caractères génériques sont retournés dans la requête tooany de réponse avec un nom correspondant (à moins qu’une correspondance plus proche à partir d’un jeu d’enregistrements non génériques). Azure DNS prend en charge des jeux d'enregistrements génériques pour tous les types d'enregistrements, hormis NS et SOA.

toocreate un enregistrement générique défini, utilisez le nom de jeu d’enregistrements hello '\*'. Vous pouvez également utiliser un nom avec « \* » comme étiquette à gauche, par exemple, « \*.foo ».

### <a name="cname-records"></a>Enregistrements CNAME

Jeux d’enregistrements CNAME ne peut pas coexister avec d’autres jeux d’enregistrements avec hello même nom. Par exemple, vous ne peut pas créer un enregistrement CNAME avec le nom relatif de hello « www » et un un enregistrement avec le nom relatif hello « www » à hello même temps.

Étant donné qu’apex de zone hello (nom = ' @') contient toujours les enregistrements NS et SOA hello jeux qui ont été créés lors de la création de la zone de hello, Impossible de créer un enregistrement CNAME définie au sommet de zone hello.

Ces contraintes sont dues aux normes DNS hello et ne sont pas des limitations d’Azure DNS.

### <a name="ns-records"></a>Enregistrements NS

jeu d’enregistrements de Hello NS au sommet de zone hello (nom « @ ») est créée automatiquement avec chaque zone DNS et est automatiquement supprimée lorsque la zone de hello est supprimé (il ne peut pas être supprimée séparément).

Ce jeu d’enregistrements contient les noms de hello de zone de hello Azure DNS nom serveurs toohello attribué. Vous pouvez ajouter des noms supplémentaires serveurs toothis NS jeu d’enregistrements, toosupport domaines l’hébergement avec le fournisseur DNS. Vous pouvez également modifier la durée de vie de hello et les métadonnées pour ce jeu d’enregistrements. Toutefois, vous ne peut pas supprimer ou modifier les serveurs de noms DNS Azure hello préremplies. 

Notez que cela s’applique uniquement toohello NS jeu d’enregistrements au sommet de zone hello. Autres jeux d’enregistrements NS dans votre zone (comme les zones enfant utilisé toodelegate) peut être créés, modifiés et supprimés sans contrainte.

### <a name="soa-records"></a>Enregistrements SOA

Un jeu d’enregistrements SOA est créé automatiquement au sommet de hello de chaque zone (nom = ' @') et est automatiquement supprimée lorsque la zone de hello est supprimée.  Il n’est pas possible de créer ou supprimer séparément des enregistrements SOA.

Vous pouvez modifier toutes les propriétés de l’enregistrement SOA de hello, à l’exception de propriété 'host' hello, qui est préconfigurée de manière toorefer toohello principal nom du serveur fournie par le système DNS Azure.

### <a name="spf-records"></a>Enregistrements SPF

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="srv-records"></a>Enregistrements SRV

[Les enregistrements SRV](https://en.wikipedia.org/wiki/SRV_record) sont utilisés par les différents emplacements de serveur services toospecify. Lorsque vous spécifiez un enregistrement SRV dans le DNS Azure :

* Hello *service* et *protocole* doit être spécifié en tant que partie du nom du jeu d’enregistrements hello, le préfixe avec des traits de soulignement.  Par exemple, « \_sip.\_TCP.Name ».  Pour un enregistrement au sommet de zone hello, il n’existe aucun besoin toospecify ' @' dans le nom de l’enregistrement hello, utilisez simplement hello service et le protocole, par exemple «\_sip.\_ TCP'.
* Hello *priorité*, *poids*, *port*, et *cible* sont spécifiés comme paramètres de chaque enregistrement dans le jeu d’enregistrements hello.

### <a name="txt-records"></a>Enregistrements TXT

Enregistrements TXT sont des chaînes de texte utilisées toomap domaine noms tooarbitrary. Ils sont utilisés dans plusieurs applications, configuration tooemail connexes en particulier, par exemple hello [Framework SPF (Sender Policy)](https://en.wikipedia.org/wiki/Sender_Policy_Framework) et [DomainKeys identifié DKIM (Mail)](https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail).

les normes DNS Hello autorisent un toocontain enregistrement TXT unique plusieurs chaînes, chacune d’elles peut être des caractères too254. Lorsque plusieurs chaînes sont utilisées, elles sont concaténées par des clients et traitées comme une chaîne unique.

Quand vous appelez hello API REST de Azure DNS, vous devez toospecify chaque chaîne TXT séparément.  Lorsque vous utilisez hello portail Azure, PowerShell ou CLI interfaces vous devez spécifier une chaîne unique par enregistrement, qui est automatiquement divisée en segments de 254 caractères si nécessaire.

Hello plusieurs chaînes dans un enregistrement DNS ne doivent pas être confondus avec hello plusieurs enregistrements TXT dans un jeu d’enregistrements TXT.  Un jeu d’enregistrements TXT peut contenir plusieurs enregistrements, *chacun d'entre eux* pouvant contenir plusieurs chaînes.  DNS Azure prend en charge une longueur de chaîne total de caractères en too1024 dans chaque enregistrement TXT (sur tous les enregistrements combinés).

## <a name="tags-and-metadata"></a>Balises et métadonnées

### <a name="tags"></a>Tags

Les balises sont une liste de paires nom-valeur et sont utilisés par les ressources toolabel Azure Resource Manager.  Azure Resource Manager utilise des vues tooenable filtré de balises de votre facture Azure et vous permet également de tooset une stratégie sur les balises sont requis. Pour plus d’informations sur les balises, consultez [à l’aide des balises tooorganize vos ressources Azure](../azure-resource-manager/resource-group-using-tags.md).

Le DNS Azure prend en charge l’utilisation de balises Azure Resource Manager sur des ressources de zone DNS.  Il ne prend pas en charge les balises sur les jeux d’enregistrements DNS, bien que l’alternative « métadonnées » soit prise en charge sur les jeux d’enregistrements DNS comme expliqué ci-dessous.

### <a name="metadata"></a>Metadata

Comme une alternative toorecord définie des balises, Azure DNS prend en charge annoter les jeux d’enregistrements à l’aide de 'metadata'.  Tootags similaire, métadonnées permet de vous tooassociate paires nom-valeur avec chaque jeu d’enregistrements.  Cela peut être utile, par exemple l’objet du hello toorecord de chaque enregistrement défini.  Contrairement aux balises, les métadonnées ne peut pas être utilisé tooprovide une vue filtrée de votre facture Azure et ne peut pas être spécifiée dans une stratégie Azure Resource Manager.

## <a name="etags"></a>Etags

Supposons que deux personnes ou les deux processus essaient toomodify DNS de l’enregistrement par hello même temps. Lequel gagne ? Et le gagnant hello sait que leur avez remplacée modifications créées par quelqu'un d’autre ?

DNS Azure utilise Etags toohandle modifications simultanées toohello même ressource en toute sécurité. Les Etags sont différents des [« Balises » Azure Resource Manager](#tags). Chaque ressource DNS (zone ou jeu d’enregistrements) est associée à un Etag. Chaque fois qu’une ressource est récupérée, son Etag l’est également. Lors de la mise à jour d’une ressource, vous pouvez choisir toopass précédent hello Etag qui Azure DNS permet de vérifier que hello Etag correspond à serveur hello. Car chaque ressource tooa de mise à jour entraîne hello Etag à chaque fois, une non-correspondance d’Etag indique une modification simultanée s’est produite. ETag peut également être utilisé lors de la création d’un nouveau tooensure de ressources que les ressources hello n’existent pas déjà.

Par défaut, Azure DNS PowerShell utilise les Etags tooblock modifications simultanées toozones et jeux d’enregistrements. Hello facultatif *-remplacer* commutateur peut être utilisé toosuppress vérification Etag, auquel cas tout simultanées les modifications qui se sont produites sont remplacées.

Au niveau de hello Hello API REST de Azure DNS, les Etags sont spécifiés à l’aide d’en-têtes HTTP.  Leur comportement est donné dans hello tableau suivant :

| En-tête | Comportement |
| --- | --- |
| Aucun |PUT réussit toujours (aucune vérification Etag) |
| If-match <etag> |PUT ne réussit que si la ressource existe et que l’Etag correspond |
| If-match * |PUT réussit seulement si la ressource existe |
| If-none-match * |PUT réussit seulement si la ressource n’existe pas |


## <a name="limits"></a>limites

Hello suivant les limites par défaut s’appliquent lors de l’utilisation d’Azure DNS :

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

## <a name="next-steps"></a>Étapes suivantes

* toostart à l’aide de DNS Azure, découvrez comment trop[créer une zone DNS](dns-getstarted-create-dnszone-portal.md) et [créer des enregistrements DNS](dns-getstarted-create-recordset-portal.md).
* toomigrate une zone DNS existante, découvrez comment trop[importer et exporter un fichier de zone DNS](dns-import-export.md).
