---
title: "aaaOverview de DNS inversée dans Azure | Documents Microsoft"
description: "Découvrez comment fonctionne le DNS inversé et quel usage peut en être fait dans Azure"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 687663fb83469ab8e696bb714649d0856915bad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reverse-dns-and-support-in-azure"></a>Vue d’ensemble du DNS inversé et prise en charge dans Azure

Cet article donne un aperçu de comment inversée DNS fonctionne et hello des scénarios DNS inverses pris en charge dans Azure.

## <a name="what-is-reverse-dns"></a>Qu’est-ce que le DNS inversé ?

Les enregistrements DNS conventionnelles activer un mappage à partir de l’adresse IP DNS tooan nom (par exemple, « www.contoso.com ») (par exemple, 64.4.6.100).  DNS inversée permet la traduction hello d’un nom de tooa précédent (64.4.6.100) d’adresse IP (« www.contoso.com »).

Les enregistrements DNS inversés sont utilisés dans de nombreuses situations. Par exemple, les enregistrements DNS inverses sont couramment utilisées dans la lutte contre le courrier non sollicité en vérifiant l’expéditeur hello d’un message électronique.  Hello extrait du serveur mail réception hello enregistrement DNS inversé de hello envoyer l’adresse IP du serveur et vérifie si qui hébergent messagerie toosend autorisés de hello provenant domaine. 

## <a name="how-reverse-dns-works"></a>Fonctionnement du DNS inversé

Les enregistrements DNS inversés sont hébergés dans des zones DNS spéciales, appelées zones « ARPA ».  Ces zones forment une hiérarchie DNS distincte en parallèle avec une hiérarchie normale de hello hébergeant des domaines tels que « contoso.com ».

Par exemple, hello l’enregistrement DNS « www.contoso.com » est implémentée à l’aide d’un enregistrement DNS 'A' avec le nom hello « www » dans la zone de hello « contoso.com ».  Cet enregistrement A pointe toohello adresse IP, dans ce cas 64.4.6.100.  la recherche inversée Hello est implémentée séparément, à l’aide d’un enregistrement « PTR » nommé « 100 » dans la zone de hello '6.4.64.in-addr.arpa' (Notez que les adresses IP sont inversés dans les zones ARPA).  Cet enregistrement PTR, s’il a été configuré correctement, pointe toohello nom « www.contoso.com ».

Lorsqu’une organisation est assignée à un bloc d’adresses IP, ils acquièrent également hello toomanage droite hello correspondant arpa parent. Bonjour zones ARPA correspondant toohello adresse blocs utilisés par Azure sont hébergés et gérés par Microsoft. Votre fournisseur de services Internet peut héberger arpa parent hello pour vos propres adresses IP pour vous, ou peut autoriser tooyou hôte arpa parent hello dans un service DNS de votre choix, par exemple, Azure DNS.

> [!NOTE]
> Les recherches DNS directes et inversées sont implémentées dans des hiérarchies DNS distinctes, en parallèle. la recherche inversée Hello pour « www.contoso.com » est **pas** hébergé dans la zone de hello « contoso.com », au lieu de cela, il est hébergé dans arpa parent hello pour le bloc d’adresses IP correspondante hello. Plusieurs zones distinctes sont utilisées pour les blocs d’adresses IPv4 et IPv6.

### <a name="ipv4"></a>IPv4

nom de Hello d’une zone de recherche inversée IPv4 doit être hello suivant le format : `<IPv4 network prefix in reverse order>.in-addr.arpa`.

Par exemple, lorsque vous créez une zone de recherche inversée toohost enregistrements pour les hôtes avec des adresses IP qui se trouvent dans le préfixe de 192.0.2.0/24 hello, nom de la zone hello serait créé en isolant le préfixe réseau hello l’adresse hello (192.0.2) puis en inversant l’ordre hello (2.0.192) et ajout de hello suffixe `.in-addr.arpa`.

|Classe de sous-réseau|Préfixe réseau  |Préfixe réseau inversé  |Suffixe standard  |Nom de zone inversé |
|-------|----------------|------------|-----------------|---------------------------|
|Classe A|203.0.0.0/8     | 203        | .in-addr.arpa   | `203.in-addr.arpa`        |
|Classe B|198.51.0.0/16   | 51.198     | .in-addr.arpa   | `51.198.in-addr.arpa`     |
|Classe C|192.0.2.0/24    | 2.0.192    | .in-addr.arpa   | `2.0.192.in-addr.arpa`    |

### <a name="classless-ipv4-delegation"></a>Délégation de IPv4 sans classe

Dans certains cas, la plage d’adresses IP hello allouée tooan organisation est inférieure à une classe C (/ 24) plage. Dans ce cas, plage d’adresses IP hello n’est pas comprise dans une limite de la zone dans hello `.in-addr.arpa` hiérarchie de zone et par conséquent, ne peut pas être délégué en tant qu’une zone enfant.

Un mécanisme différent est utilisé à la place, zone DNS tooa dédié des enregistrements de contrôle de tootransfer d’individuelle inversée (PTR). Ce mécanisme délègue à une zone enfant pour chaque plage IP, puis mappe chaque adresse IP Bonjour plage individuellement zone enfant de toothat à l’aide d’enregistrements CNAME.

Par exemple, qu'une organisation bénéficie hello IP plage 192.0.2.128/26 par son fournisseur de services Internet. Cela représente 64 adresses IP, de 192.0.2.128 too192.0.2.191. Le DNS inversé de cette plage est mis en œuvre comme suit :
- organisation de Hello crée une zone de recherche inversée appelée 128-26.2.0.192.in-addr.arpa. préfixe Hello ' 128-26' représente hello réseau segment affecté toohello organisation au sein de hello classe C (/ 24) plage.
- Hello ISP crée tooset d’enregistrements NS des hello délégation DNS pour hello au-dessus de zone à partir de la zone parente de classe C hello. Il crée également les enregistrements CNAME dans la zone de recherche inversée hello parent (classe C), le mappage de chaque adresse IP de hello IP plage toohello zone créée par l’organisation de hello :

```
$ORIGIN 2.0.192.in-addr.arpa
; Delegate child zone
128-26    NS       <name server 1 for 128-26.2.0.192.in-addr.arpa>
128-26    NS       <name server 2 for 128-26.2.0.192.in-addr.arpa>
; CNAME records for each IP address
129       CNAME    129.128-26.2.0.192.in-addr.arpa
130       CNAME    130.128-26.2.0.192.in-addr.arpa
131       CNAME    131.128-26.2.0.192.in-addr.arpa
; etc
```
- organisation Hello puis gère les enregistrements PTR individuels hello dans leur zone enfant.

```
$ORIGIN 128-26.2.0.192.in-addr.arpa
; PTR records for each UIP address. Names match CNAME targets in parent zone
129      PTR    www.contoso.com
130      PTR    mail.contoso.com
131      PTR    partners.contoso.com
; etc
```
Une recherche inversée pour les requêtes de l’adresse '192.0.2.129' hello IP pour un enregistrement PTR nommé '129.2.0.192.in-addr.arpa'. Cette requête résout via hello CNAME dans hello zone toohello PTR parente dans la zone enfant de hello.

### <a name="ipv6"></a>IPv6

nom Hello d’une zone de recherche inversée IPv6 doit être hello suivant du formulaire :`<IPv6 network prefix in reverse order>.ip6.arpa`

Par exemple, Lorsque vous créez une zone de recherche inversée toohost enregistrements pour les hôtes avec des adresses IP qui se trouvent dans hello 2001:db8:1000:abdc :: / 64 préfixe, nom de la zone hello serait créé en isolant le préfixe de réseau hello d’adresse de hello (2001:db8:abdc ::). Développez ensuite les tooremove de préfixe réseau IPv6 de hello [zéro compression](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx), s’il s’agissait de préfixe d’adresse utilisé tooshorten hello IPv6 (2001:0db8:abdc:0000 ::). Inverse l’ordre de hello, en utilisant un point comme hello séparateur entre chaque nombre hexadécimal de préfixe de hello, toobuild hello inversée préfixe réseau (`0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2`) et ajouter un suffixe de hello `.ip6.arpa`.


|Préfixe réseau  |Préfixe réseau développé et inversé |Suffixe standard |Nom de zone inversé  |
|---------|---------|---------|---------|
|2001:db8:ABDC::/64    | 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2        | .ip6.arpa        | `0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa`       |
|2001:db8:1000:9102::/64    | 2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2        | .ip6.arpa        | `2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2.ip6.arpa`        |


## <a name="azure-support-for-reverse-dns"></a>Prise en charge Azure pour le DNS inversé

Azure prend en charge deux scénarios distincts concernant tooreverse DNS :

**Hébergement hello inversée zone correspondante tooyour bloc d’adresses IP.**
DNS Azure peut être utilisé trop[héberger vos zones de recherche inversée et de gérer les enregistrements PTR hello pour chaque recherche DNS inversée](dns-reverse-dns-hosting.md), à la fois IPv4 et IPv6.  Hello du processus de création de zone de recherche inversée (ARPA) hello, configurer la délégation contrainte hello, et configuration PTR enregistrements est hello même que pour les zones DNS standards.  Hello uniquement les différences sont que la délégation de hello doit être configurée via votre fournisseur de services Internet au lieu de votre bureau d’enregistrement DNS, et uniquement hello type d’enregistrement PTR doit être utilisé.

**Configurer hello inverse enregistrement DNS pour hello adresse IP tooyour service Azure.** Azure vous permet de trop[configurer inversée hello pour les adresses IP hello allouée tooyour service Azure](dns-reverse-dns-for-azure-services.md).  Cette recherche inversée est configurée par Azure comme un enregistrement PTR dans les zones ARPA correspondant hello.  Ces zones ARPA, correspondant de plages d’IP tooall hello sont utilisées par Azure, sont hébergés par Microsoft

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur le DNS inversé, consultez [Recherche DNS inversée sur Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).
<br>
Découvrez comment trop[zone de recherche inversée hello hôte pour votre plage IP affectée par le fournisseur de services Internet dans Azure DNS](dns-reverse-dns-for-azure-services.md).
<br>
Découvrez comment trop[gère les enregistrements DNS inverses pour vos services Azure](dns-reverse-dns-for-azure-services.md).

