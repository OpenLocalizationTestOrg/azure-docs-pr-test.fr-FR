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
# <a name="overview-of-reverse-dns-and-support-in-azure"></a><span data-ttu-id="0d8b9-103">Vue d’ensemble du DNS inversé et prise en charge dans Azure</span><span class="sxs-lookup"><span data-stu-id="0d8b9-103">Overview of reverse DNS and support in Azure</span></span>

<span data-ttu-id="0d8b9-104">Cet article donne un aperçu de comment inversée DNS fonctionne et hello des scénarios DNS inverses pris en charge dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-104">This article gives an overview of how reverse DNS works, and hello reverse DNS scenarios supported in Azure.</span></span>

## <a name="what-is-reverse-dns"></a><span data-ttu-id="0d8b9-105">Qu’est-ce que le DNS inversé ?</span><span class="sxs-lookup"><span data-stu-id="0d8b9-105">What is reverse DNS?</span></span>

<span data-ttu-id="0d8b9-106">Les enregistrements DNS conventionnelles activer un mappage à partir de l’adresse IP DNS tooan nom (par exemple, « www.contoso.com ») (par exemple, 64.4.6.100).</span><span class="sxs-lookup"><span data-stu-id="0d8b9-106">Conventional DNS records enable a mapping from a DNS name (such as 'www.contoso.com') tooan IP address (such as 64.4.6.100).</span></span>  <span data-ttu-id="0d8b9-107">DNS inversée permet la traduction hello d’un nom de tooa précédent (64.4.6.100) d’adresse IP (« www.contoso.com »).</span><span class="sxs-lookup"><span data-stu-id="0d8b9-107">Reverse DNS enables hello translation of an IP address (64.4.6.100) back tooa name ('www.contoso.com').</span></span>

<span data-ttu-id="0d8b9-108">Les enregistrements DNS inversés sont utilisés dans de nombreuses situations.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-108">Reverse DNS records are used in a variety of situations.</span></span> <span data-ttu-id="0d8b9-109">Par exemple, les enregistrements DNS inverses sont couramment utilisées dans la lutte contre le courrier non sollicité en vérifiant l’expéditeur hello d’un message électronique.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-109">For example, reverse DNS records are widely used in combating e-mail spam by verifying hello sender of an e-mail message.</span></span>  <span data-ttu-id="0d8b9-110">Hello extrait du serveur mail réception hello enregistrement DNS inversé de hello envoyer l’adresse IP du serveur et vérifie si qui hébergent messagerie toosend autorisés de hello provenant domaine.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-110">hello receiving mail server retrieves hello reverse DNS record of hello sending server's IP address, and verifies if that host is authorized toosend e-mail from hello originating domain.</span></span> 

## <a name="how-reverse-dns-works"></a><span data-ttu-id="0d8b9-111">Fonctionnement du DNS inversé</span><span class="sxs-lookup"><span data-stu-id="0d8b9-111">How reverse DNS works</span></span>

<span data-ttu-id="0d8b9-112">Les enregistrements DNS inversés sont hébergés dans des zones DNS spéciales, appelées zones « ARPA ».</span><span class="sxs-lookup"><span data-stu-id="0d8b9-112">Reverse DNS records are hosted in special DNS zones, known as 'ARPA' zones.</span></span>  <span data-ttu-id="0d8b9-113">Ces zones forment une hiérarchie DNS distincte en parallèle avec une hiérarchie normale de hello hébergeant des domaines tels que « contoso.com ».</span><span class="sxs-lookup"><span data-stu-id="0d8b9-113">These zones form a separate DNS hierarchy in parallel with hello normal hierarchy hosting domains such as 'contoso.com'.</span></span>

<span data-ttu-id="0d8b9-114">Par exemple, hello l’enregistrement DNS « www.contoso.com » est implémentée à l’aide d’un enregistrement DNS 'A' avec le nom hello « www » dans la zone de hello « contoso.com ».</span><span class="sxs-lookup"><span data-stu-id="0d8b9-114">For example, hello DNS record 'www.contoso.com' is implemented using a DNS 'A' record with hello name 'www' in hello zone 'contoso.com'.</span></span>  <span data-ttu-id="0d8b9-115">Cet enregistrement A pointe toohello adresse IP, dans ce cas 64.4.6.100.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-115">This A record points toohello corresponding IP address, in this case 64.4.6.100.</span></span>  <span data-ttu-id="0d8b9-116">la recherche inversée Hello est implémentée séparément, à l’aide d’un enregistrement « PTR » nommé « 100 » dans la zone de hello '6.4.64.in-addr.arpa' (Notez que les adresses IP sont inversés dans les zones ARPA).  Cet enregistrement PTR, s’il a été configuré correctement, pointe toohello nom « www.contoso.com ».</span><span class="sxs-lookup"><span data-stu-id="0d8b9-116">hello reverse lookup is implemented separately, using a 'PTR' record named '100' in hello zone '6.4.64.in-addr.arpa' (note that IP addresses are reversed in ARPA zones.)  This PTR record, if it has been configured correctly, points toohello name 'www.contoso.com'.</span></span>

<span data-ttu-id="0d8b9-117">Lorsqu’une organisation est assignée à un bloc d’adresses IP, ils acquièrent également hello toomanage droite hello correspondant arpa parent.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-117">When an organization is assigned an IP address block, they also acquire hello right toomanage hello corresponding ARPA zone.</span></span> <span data-ttu-id="0d8b9-118">Bonjour zones ARPA correspondant toohello adresse blocs utilisés par Azure sont hébergés et gérés par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-118">hello ARPA zones corresponding toohello IP address blocks used by Azure are hosted and managed by Microsoft.</span></span> <span data-ttu-id="0d8b9-119">Votre fournisseur de services Internet peut héberger arpa parent hello pour vos propres adresses IP pour vous, ou peut autoriser tooyou hôte arpa parent hello dans un service DNS de votre choix, par exemple, Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-119">Your ISP may host hello ARPA zone for your own IP addresses for you, or may allow tooyou host hello ARPA zone in a DNS service of your choice, such as Azure DNS.</span></span>

> [!NOTE]
> <span data-ttu-id="0d8b9-120">Les recherches DNS directes et inversées sont implémentées dans des hiérarchies DNS distinctes, en parallèle.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-120">Forward DNS lookups and reverse DNS lookups are implemented in separate, parallel DNS hierarchies.</span></span> <span data-ttu-id="0d8b9-121">la recherche inversée Hello pour « www.contoso.com » est **pas** hébergé dans la zone de hello « contoso.com », au lieu de cela, il est hébergé dans arpa parent hello pour le bloc d’adresses IP correspondante hello.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-121">hello reverse lookup for 'www.contoso.com' is **not** hosted in hello zone 'contoso.com', rather it is hosted in hello ARPA zone for hello corresponding IP address block.</span></span> <span data-ttu-id="0d8b9-122">Plusieurs zones distinctes sont utilisées pour les blocs d’adresses IPv4 et IPv6.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-122">Separate zones are used for IPv4 and IPv6 address blocks.</span></span>

### <a name="ipv4"></a><span data-ttu-id="0d8b9-123">IPv4</span><span class="sxs-lookup"><span data-stu-id="0d8b9-123">IPv4</span></span>

<span data-ttu-id="0d8b9-124">nom de Hello d’une zone de recherche inversée IPv4 doit être hello suivant le format : `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-124">hello name of an IPv4 reverse lookup zone should be in hello following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span>

<span data-ttu-id="0d8b9-125">Par exemple, lorsque vous créez une zone de recherche inversée toohost enregistrements pour les hôtes avec des adresses IP qui se trouvent dans le préfixe de 192.0.2.0/24 hello, nom de la zone hello serait créé en isolant le préfixe réseau hello l’adresse hello (192.0.2) puis en inversant l’ordre hello (2.0.192) et ajout de hello suffixe `.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-125">For example, when creating a reverse zone toohost records for hosts with IPs that are in hello 192.0.2.0/24 prefix, hello zone name would be created by isolating hello network prefix of hello address (192.0.2) and then reversing hello order (2.0.192) and adding hello suffix `.in-addr.arpa`.</span></span>

|<span data-ttu-id="0d8b9-126">Classe de sous-réseau</span><span class="sxs-lookup"><span data-stu-id="0d8b9-126">Subnet class</span></span>|<span data-ttu-id="0d8b9-127">Préfixe réseau</span><span class="sxs-lookup"><span data-stu-id="0d8b9-127">Network prefix</span></span>  |<span data-ttu-id="0d8b9-128">Préfixe réseau inversé</span><span class="sxs-lookup"><span data-stu-id="0d8b9-128">Reversed network prefix</span></span>  |<span data-ttu-id="0d8b9-129">Suffixe standard</span><span class="sxs-lookup"><span data-stu-id="0d8b9-129">Standard suffix</span></span>  |<span data-ttu-id="0d8b9-130">Nom de zone inversé</span><span class="sxs-lookup"><span data-stu-id="0d8b9-130">Reverse zone name</span></span> |
|-------|----------------|------------|-----------------|---------------------------|
|<span data-ttu-id="0d8b9-131">Classe A</span><span class="sxs-lookup"><span data-stu-id="0d8b9-131">Class A</span></span>|<span data-ttu-id="0d8b9-132">203.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="0d8b9-132">203.0.0.0/8</span></span>     | <span data-ttu-id="0d8b9-133">203</span><span class="sxs-lookup"><span data-stu-id="0d8b9-133">203</span></span>        | <span data-ttu-id="0d8b9-134">.in-addr.arpa</span><span class="sxs-lookup"><span data-stu-id="0d8b9-134">.in-addr.arpa</span></span>   | `203.in-addr.arpa`        |
|<span data-ttu-id="0d8b9-135">Classe B</span><span class="sxs-lookup"><span data-stu-id="0d8b9-135">Class B</span></span>|<span data-ttu-id="0d8b9-136">198.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="0d8b9-136">198.51.0.0/16</span></span>   | <span data-ttu-id="0d8b9-137">51.198</span><span class="sxs-lookup"><span data-stu-id="0d8b9-137">51.198</span></span>     | <span data-ttu-id="0d8b9-138">.in-addr.arpa</span><span class="sxs-lookup"><span data-stu-id="0d8b9-138">.in-addr.arpa</span></span>   | `51.198.in-addr.arpa`     |
|<span data-ttu-id="0d8b9-139">Classe C</span><span class="sxs-lookup"><span data-stu-id="0d8b9-139">Class C</span></span>|<span data-ttu-id="0d8b9-140">192.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="0d8b9-140">192.0.2.0/24</span></span>    | <span data-ttu-id="0d8b9-141">2.0.192</span><span class="sxs-lookup"><span data-stu-id="0d8b9-141">2.0.192</span></span>    | <span data-ttu-id="0d8b9-142">.in-addr.arpa</span><span class="sxs-lookup"><span data-stu-id="0d8b9-142">.in-addr.arpa</span></span>   | `2.0.192.in-addr.arpa`    |

### <a name="classless-ipv4-delegation"></a><span data-ttu-id="0d8b9-143">Délégation de IPv4 sans classe</span><span class="sxs-lookup"><span data-stu-id="0d8b9-143">Classless IPv4 delegation</span></span>

<span data-ttu-id="0d8b9-144">Dans certains cas, la plage d’adresses IP hello allouée tooan organisation est inférieure à une classe C (/ 24) plage.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-144">In some cases, hello IP range allocated tooan organization is smaller than a Class C (/24) range.</span></span> <span data-ttu-id="0d8b9-145">Dans ce cas, plage d’adresses IP hello n’est pas comprise dans une limite de la zone dans hello `.in-addr.arpa` hiérarchie de zone et par conséquent, ne peut pas être délégué en tant qu’une zone enfant.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-145">In this case, hello IP range does not fall on a zone boundary within hello `.in-addr.arpa` zone hierarchy, and hence cannot be delegated as a child zone.</span></span>

<span data-ttu-id="0d8b9-146">Un mécanisme différent est utilisé à la place, zone DNS tooa dédié des enregistrements de contrôle de tootransfer d’individuelle inversée (PTR).</span><span class="sxs-lookup"><span data-stu-id="0d8b9-146">Instead, a different mechanism is used tootransfer control of individual reverse lookup (PTR) records tooa dedicated DNS zone.</span></span> <span data-ttu-id="0d8b9-147">Ce mécanisme délègue à une zone enfant pour chaque plage IP, puis mappe chaque adresse IP Bonjour plage individuellement zone enfant de toothat à l’aide d’enregistrements CNAME.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-147">This mechanism delegates a child zone for each IP range, then maps each IP address in hello range individually toothat child zone using CNAME records.</span></span>

<span data-ttu-id="0d8b9-148">Par exemple, qu'une organisation bénéficie hello IP plage 192.0.2.128/26 par son fournisseur de services Internet.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-148">For example, suppose an organization is granted hello IP range 192.0.2.128/26 by its ISP.</span></span> <span data-ttu-id="0d8b9-149">Cela représente 64 adresses IP, de 192.0.2.128 too192.0.2.191.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-149">This represents 64 IP addresses, from 192.0.2.128 too192.0.2.191.</span></span> <span data-ttu-id="0d8b9-150">Le DNS inversé de cette plage est mis en œuvre comme suit :</span><span class="sxs-lookup"><span data-stu-id="0d8b9-150">Reverse DNS for this range is implemented as follows:</span></span>
- <span data-ttu-id="0d8b9-151">organisation de Hello crée une zone de recherche inversée appelée 128-26.2.0.192.in-addr.arpa.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-151">hello organization creates a reverse lookup zone called 128-26.2.0.192.in-addr.arpa.</span></span> <span data-ttu-id="0d8b9-152">préfixe Hello ' 128-26' représente hello réseau segment affecté toohello organisation au sein de hello classe C (/ 24) plage.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-152">hello prefix '128-26' represents hello network segment assigned toohello organization within hello Class C (/24) range.</span></span>
- <span data-ttu-id="0d8b9-153">Hello ISP crée tooset d’enregistrements NS des hello délégation DNS pour hello au-dessus de zone à partir de la zone parente de classe C hello.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-153">hello ISP creates NS records tooset up hello DNS delegation for hello above zone from hello Class C parent zone.</span></span> <span data-ttu-id="0d8b9-154">Il crée également les enregistrements CNAME dans la zone de recherche inversée hello parent (classe C), le mappage de chaque adresse IP de hello IP plage toohello zone créée par l’organisation de hello :</span><span class="sxs-lookup"><span data-stu-id="0d8b9-154">It also creates CNAME records in hello parent (Class C) reverse lookup zone, mapping each IP address in hello IP range toohello new zone created by hello organization:</span></span>

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
- <span data-ttu-id="0d8b9-155">organisation Hello puis gère les enregistrements PTR individuels hello dans leur zone enfant.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-155">hello organization then manages hello individual PTR records within their child zone.</span></span>

```
$ORIGIN 128-26.2.0.192.in-addr.arpa
; PTR records for each UIP address. Names match CNAME targets in parent zone
129      PTR    www.contoso.com
130      PTR    mail.contoso.com
131      PTR    partners.contoso.com
; etc
```
<span data-ttu-id="0d8b9-156">Une recherche inversée pour les requêtes de l’adresse '192.0.2.129' hello IP pour un enregistrement PTR nommé '129.2.0.192.in-addr.arpa'.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-156">A reverse lookup for hello IP address '192.0.2.129' queries for a PTR record named '129.2.0.192.in-addr.arpa'.</span></span> <span data-ttu-id="0d8b9-157">Cette requête résout via hello CNAME dans hello zone toohello PTR parente dans la zone enfant de hello.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-157">This query resolves via hello CNAME in hello parent zone toohello PTR record in hello child zone.</span></span>

### <a name="ipv6"></a><span data-ttu-id="0d8b9-158">IPv6</span><span class="sxs-lookup"><span data-stu-id="0d8b9-158">IPv6</span></span>

<span data-ttu-id="0d8b9-159">nom Hello d’une zone de recherche inversée IPv6 doit être hello suivant du formulaire :`<IPv6 network prefix in reverse order>.ip6.arpa`</span><span class="sxs-lookup"><span data-stu-id="0d8b9-159">hello name of an IPv6 reverse lookup zone should be in hello following form: `<IPv6 network prefix in reverse order>.ip6.arpa`</span></span>

<span data-ttu-id="0d8b9-160">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="0d8b9-160">For example,.</span></span> <span data-ttu-id="0d8b9-161">Lorsque vous créez une zone de recherche inversée toohost enregistrements pour les hôtes avec des adresses IP qui se trouvent dans hello 2001:db8:1000:abdc :: / 64 préfixe, nom de la zone hello serait créé en isolant le préfixe de réseau hello d’adresse de hello (2001:db8:abdc ::).</span><span class="sxs-lookup"><span data-stu-id="0d8b9-161">When creating a reverse zone toohost records for hosts with IPs that are in hello 2001:db8:1000:abdc::/64 prefix, hello zone name would be created by isolating hello network prefix of hello address (2001:db8:abdc::).</span></span> <span data-ttu-id="0d8b9-162">Développez ensuite les tooremove de préfixe réseau IPv6 de hello [zéro compression](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx), s’il s’agissait de préfixe d’adresse utilisé tooshorten hello IPv6 (2001:0db8:abdc:0000 ::).</span><span class="sxs-lookup"><span data-stu-id="0d8b9-162">Next expand hello IPv6 network prefix tooremove [zero compression](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx), if it was used tooshorten hello IPv6 address prefix (2001:0db8:abdc:0000::).</span></span> <span data-ttu-id="0d8b9-163">Inverse l’ordre de hello, en utilisant un point comme hello séparateur entre chaque nombre hexadécimal de préfixe de hello, toobuild hello inversée préfixe réseau (`0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2`) et ajouter un suffixe de hello `.ip6.arpa`.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-163">Reverse hello order, using a period as hello delimiter between each hexadecimal number in hello prefix, toobuild hello reversed network prefix (`0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2`) and add hello suffix `.ip6.arpa`.</span></span>


|<span data-ttu-id="0d8b9-164">Préfixe réseau</span><span class="sxs-lookup"><span data-stu-id="0d8b9-164">Network prefix</span></span>  |<span data-ttu-id="0d8b9-165">Préfixe réseau développé et inversé</span><span class="sxs-lookup"><span data-stu-id="0d8b9-165">Expanded and reversed network prefix</span></span> |<span data-ttu-id="0d8b9-166">Suffixe standard</span><span class="sxs-lookup"><span data-stu-id="0d8b9-166">Standard suffix</span></span> |<span data-ttu-id="0d8b9-167">Nom de zone inversé</span><span class="sxs-lookup"><span data-stu-id="0d8b9-167">Reverse zone name</span></span>  |
|---------|---------|---------|---------|
|<span data-ttu-id="0d8b9-168">2001:db8:ABDC::/64</span><span class="sxs-lookup"><span data-stu-id="0d8b9-168">2001:db8:abdc::/64</span></span>    | <span data-ttu-id="0d8b9-169">0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2</span><span class="sxs-lookup"><span data-stu-id="0d8b9-169">0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2</span></span>        | <span data-ttu-id="0d8b9-170">.ip6.arpa</span><span class="sxs-lookup"><span data-stu-id="0d8b9-170">.ip6.arpa</span></span>        | `0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa`       |
|<span data-ttu-id="0d8b9-171">2001:db8:1000:9102::/64</span><span class="sxs-lookup"><span data-stu-id="0d8b9-171">2001:db8:1000:9102::/64</span></span>    | <span data-ttu-id="0d8b9-172">2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2</span><span class="sxs-lookup"><span data-stu-id="0d8b9-172">2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2</span></span>        | <span data-ttu-id="0d8b9-173">.ip6.arpa</span><span class="sxs-lookup"><span data-stu-id="0d8b9-173">.ip6.arpa</span></span>        | `2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2.ip6.arpa`        |


## <a name="azure-support-for-reverse-dns"></a><span data-ttu-id="0d8b9-174">Prise en charge Azure pour le DNS inversé</span><span class="sxs-lookup"><span data-stu-id="0d8b9-174">Azure support for reverse DNS</span></span>

<span data-ttu-id="0d8b9-175">Azure prend en charge deux scénarios distincts concernant tooreverse DNS :</span><span class="sxs-lookup"><span data-stu-id="0d8b9-175">Azure supports two separate scenarios relating tooreverse DNS:</span></span>

<span data-ttu-id="0d8b9-176">**Hébergement hello inversée zone correspondante tooyour bloc d’adresses IP.**</span><span class="sxs-lookup"><span data-stu-id="0d8b9-176">**Hosting hello reverse lookup zone corresponding tooyour IP address block.**</span></span>
<span data-ttu-id="0d8b9-177">DNS Azure peut être utilisé trop[héberger vos zones de recherche inversée et de gérer les enregistrements PTR hello pour chaque recherche DNS inversée](dns-reverse-dns-hosting.md), à la fois IPv4 et IPv6.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-177">Azure DNS can be used too[host your reverse lookup zones and manage hello PTR records for each reverse DNS lookup](dns-reverse-dns-hosting.md), for both IPv4 and IPv6.</span></span>  <span data-ttu-id="0d8b9-178">Hello du processus de création de zone de recherche inversée (ARPA) hello, configurer la délégation contrainte hello, et configuration PTR enregistrements est hello même que pour les zones DNS standards.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-178">hello process of creating hello reverse lookup (ARPA) zone, setting up hello delegation, and configuring PTR records is hello same as for regular DNS zones.</span></span>  <span data-ttu-id="0d8b9-179">Hello uniquement les différences sont que la délégation de hello doit être configurée via votre fournisseur de services Internet au lieu de votre bureau d’enregistrement DNS, et uniquement hello type d’enregistrement PTR doit être utilisé.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-179">hello only differences are that hello delegation must be configured via your ISP rather than your DNS registrar, and only hello PTR record type should be used.</span></span>

<span data-ttu-id="0d8b9-180">**Configurer hello inverse enregistrement DNS pour hello adresse IP tooyour service Azure.**</span><span class="sxs-lookup"><span data-stu-id="0d8b9-180">**Configure hello reverse DNS record for hello IP address assigned tooyour Azure service.**</span></span> <span data-ttu-id="0d8b9-181">Azure vous permet de trop[configurer inversée hello pour les adresses IP hello allouée tooyour service Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="0d8b9-181">Azure enables you too[configure hello reverse lookup for hello IP addresses allocated tooyour Azure service](dns-reverse-dns-for-azure-services.md).</span></span>  <span data-ttu-id="0d8b9-182">Cette recherche inversée est configurée par Azure comme un enregistrement PTR dans les zones ARPA correspondant hello.</span><span class="sxs-lookup"><span data-stu-id="0d8b9-182">This reverse lookup is configured by Azure as a PTR record in hello corresponding ARPA zone.</span></span>  <span data-ttu-id="0d8b9-183">Ces zones ARPA, correspondant de plages d’IP tooall hello sont utilisées par Azure, sont hébergés par Microsoft</span><span class="sxs-lookup"><span data-stu-id="0d8b9-183">These ARPA zones, corresponding tooall hello IP ranges used by Azure, are hosted by Microsoft</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d8b9-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0d8b9-184">Next steps</span></span>

<span data-ttu-id="0d8b9-185">Pour plus d’informations sur le DNS inversé, consultez [Recherche DNS inversée sur Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="0d8b9-185">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="0d8b9-186">Découvrez comment trop[zone de recherche inversée hello hôte pour votre plage IP affectée par le fournisseur de services Internet dans Azure DNS](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="0d8b9-186">Learn how too[host hello reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span></span>
<br>
<span data-ttu-id="0d8b9-187">Découvrez comment trop[gère les enregistrements DNS inverses pour vos services Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="0d8b9-187">Learn how too[manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>
