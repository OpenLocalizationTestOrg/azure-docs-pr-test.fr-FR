---
title: "aaaHosting inverser les zones de recherche DNS dans le système DNS Azure | Documents Microsoft"
description: "Découvrez comment hello de toohost toouse Azure DNS inverse des zones de recherche DNS pour vos plages IP"
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
ms.openlocfilehash: 24feb8ef1c75a7d91938867f348fed1190046e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a>Hébergement de zones de recherche inversées DNS dans Azure DNS

Cet article explique comment toohost hello inverser les zones de recherche DNS pour vos plages IP affectées dans Azure DNS. plages d’adresses IP Hello représentés par la zone de recherche inversée hello doivent être assignés tooyour organisation, généralement par votre fournisseur de services Internet.

tooconfigure la recherche DNS inversée pour Azure appartenant à l’IP adresse affectée tooyour service Azure, consultez [configurer inversée hello pour les adresses IP hello allouée tooyour service Azure](dns-reverse-dns-for-azure-services.md).

Avant de lire cet article, prenez connaissance de cette [Vue d’ensemble des DNS inversés et de la prise en charge dans Azure](dns-reverse-dns-overview.md).

Cet article vous assiste hello étapes toocreate votre première zone de recherche inversée DNS et un enregistrement à l’aide de hello portail Azure, Azure PowerShell, Azure CLI 1.0 ou 2.0 de CLI d’Azure.

## <a name="create-a-reverse-lookup-dns-zone"></a>Créer une zone de recherche inversée DNS

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com)
1. Dans le menu du Hub hello, cliquez sur, puis cliquez sur **nouveau** > **mise en réseau** > puis cliquez sur **zone DNS** tooopen hello **créer Directory**panneau.

   ![Zone DNS](./media/dns-reverse-dns-hosting/figure1.png)

1. Sur hello **zone DNS de créer** panneau, nommez votre zone DNS. nom Hello de zone de hello est spécialement conçu différemment pour les préfixes IPv4 et IPv6. Utilisez deux instructions hello pour [IPV4](#ipv4) ou [IPv6](#ipv6) tooname votre zone. Lorsque vous avez terminé cliquez **créer** zone de hello toocreate.

### <a name="ipv4"></a>IPv4

nom de Hello d’une zone de recherche inversée IPv4 est basé sur une plage d’adresses IP hello qu’il représente. Devrait être hello suivant le format : `<IPv4 network prefix in reverse order>.in-addr.arpa`. Pour obtenir des exemples, consultez [vue d’ensemble des DNS inversés et prise en charge dans Azure](dns-reverse-dns-overview.md#ipv4).

> [!NOTE]
> Lors de la création de routage interdomaine sans classe zones de recherche DNS inversées dans DNS de Azure, vous devez utiliser un trait d’union (`-`) au lieu d’une barre oblique (« / ») dans le nom de la zone hello.
>
> Par exemple, pour hello IP plage 192.0.2.128/26, vous devez utiliser `128-26.2.0.192.in-addr.arpa` en tant que nom de la zone hello au lieu de `128/26.2.0.192.in-addr.arpa`.
>
> C’est pourquoi, tandis que les deux sont pris en charge par les normes DNS hello, de noms contenant la barre oblique hello zone DNS (`/`) caractères ne sont pas pris en charge dans le système DNS Azure.

Hello suivant montre comment toocreate une classe C inverser la zone DNS nommé `2.0.192.in-addr.arpa` dans le système DNS Azure via hello portail Azure :

 ![créer une zone DNS](./media/dns-reverse-dns-hosting/figure2.png)

Bonjour 'Emplacement de groupe de ressources' définit l’emplacement de hello pour le groupe de ressources hello et n’a aucun impact sur la zone DNS de hello. emplacement des zones DNS Hello est toujours 'global' et n’est pas affiché.

Hello exemples suivants montrent comment toocomplete cette tâche, avec Azure PowerShell et hello CLI d’Azure :

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a>IPv6

nom Hello d’une zone de recherche inversée IPv6 doit être Bonjour suivant du formulaire : `<IPv6 network prefix in reverse order>.ip6.arpa`.  Pour obtenir des exemples, consultez [vue d’ensemble des DNS inversés et prise en charge dans Azure](dns-reverse-dns-overview.md#ipv6).


Hello suivant montre comment toocreate une zone de recherche DNS inversée IPv6 nommé `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` dans le système DNS Azure via hello portail Azure :

 ![créer une zone DNS](./media/dns-reverse-dns-hosting/figure3.png)

Bonjour 'Emplacement de groupe de ressources' définit l’emplacement de hello pour le groupe de ressources hello et n’a aucun impact sur la zone DNS de hello. emplacement des zones DNS Hello est toujours 'global' et n’est pas affiché.

Hello exemples suivants montrent comment toocomplete cette tâche, avec Azure PowerShell et hello CLI d’Azure :

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a>Azure CLI 1.0

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a>Azure CLI 2.0

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a>Déléguer une zone de recherche inversée DNS

Après avoir créé votre zone de recherche DNS inversée, vous devez vous assurer que zone hello est déléguée à partir de la zone parente de hello. La délégation DNS Active hello résolution processus toofind hello nom serveurs DNS qui héberge la zone de recherche DNS inversée. Ainsi, ces serveurs tooanswer DNS inverses requêtes de noms pour les adresses IP de hello dans votre plage d’adresses.

Pour les zones de recherche directe, processus hello de délégation de zone DNS est décrite dans [déléguer votre tooAzure de domaine DNS](dns-delegate-domain-azure-dns.md). Fonctionnement de la délégation pour les zones de recherche inversée hello identique. Hello seule différence est que vous avez besoin de serveurs de noms hello tooconfigure avec hello fournisseur de services Internet qui vous a fourni votre plage IP, plutôt que sur votre bureau d’enregistrement du nom de domaine.

## <a name="create-a-dns-ptr-record"></a>Créer un enregistrement PTR DNS

### <a name="ipv4"></a>IPv4

Hello exemple suivant vous guide hello processus de création d’un enregistrement PTR dans une zone de recherche inversée DNS dans le système DNS Azure. Pour d’autres types d’enregistrements et les enregistrements existants de toomodify, consultez [enregistrements DNS de gérer et jeux d’enregistrements à l’aide de portail Azure hello](dns-operations-recordsets-portal.md).

1.  En haut de hello Hello **zone DNS** panneau, sélectionnez **+ enregistrer ensemble** tooopen hello **ajouter le jeu d’enregistrements** panneau.

 ![Zone DNS](./media/dns-reverse-dns-hosting/figure4.png)

1. Sur hello **ajouter le jeu d’enregistrements** panneau. 
1. Sélectionnez **PTR** à partir de l’enregistrement de hello »**Type**« menu.  
1. Hello nom du jeu d’enregistrements hello pour un enregistrement PTR doit reste hello toobe hello adresse IPv4 dans l’ordre inverse. Dans cet exemple, hello trois premiers octets sont déjà remplies en tant que partie du nom de la zone hello (.2.0.192). Par conséquent, seuls hello dernier octet est fournie dans le champ de nom hello. Vous pouvez par exemple nommer votre jeu d’enregistrements «**15**» pour une ressource dont l’adresse IP est 192.0.2.15.  
1. Bonjour »**nom de domaine**», entrez le nom de domaine complet (FQDN) hello de ressource hello à l’aide de hello IP.
1. Sélectionnez **OK** bas l’enregistrement DNS de hello panneau toocreate hello hello.

 ![ajouter un jeu d’enregistrements](./media/dns-reverse-dns-hosting/figure5.png)

Hello Voici des exemples sur la façon de toocomplete cette tâche avec PowerShell et hello AzureCLI :

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a>Azure CLI 1.0

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a>Azure CLI 2.0

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a>IPv6

Bonjour à l’exemple suivant vous guide tout au long des processus de hello de création d’enregistrement « PTR ». Pour d’autres types d’enregistrements et les enregistrements existants de toomodify, consultez [enregistrements DNS de gérer et jeux d’enregistrements à l’aide de portail Azure hello](dns-operations-recordsets-portal.md).

1. En haut de hello Hello **Panneau de zone DNS**, sélectionnez **+ enregistrer ensemble** tooopen hello **ajouter le jeu d’enregistrements** panneau.

  ![panneau zone DNS](./media/dns-reverse-dns-hosting/figure6.png)

2. Sur hello **ajouter le jeu d’enregistrements** panneau. 
3. Sélectionnez **PTR** à partir de l’enregistrement de hello »**Type**« menu.  
4. Hello nom du jeu d’enregistrements hello pour un enregistrement PTR doit reste hello toobe hello adresse IPv6 dans l’ordre inverse. Il ne doit inclure aucune compression des zéros. Dans cet exemple, hello 64 premiers bits de hello IPv6 figurent déjà dans le cadre du nom de la zone hello (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa). Par conséquent, seuls hello 64 derniers bits sont fournis dans le champ de nom hello. Hello dernière 64 bits de l’adresse IP de hello sont entrés dans l’ordre inverse, en utilisant un point comme séparateur hello entre chaque nombre hexadécimal. Par exemple, vous pouvez nommer votre jeu d’enregistrements «**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**» pour une ressource dont l’adresse IP est 2001:0db8:abdc:0000:f524:10bc:1af9:405e.  
5. Bonjour »**nom de domaine**», entrez le nom de domaine complet (FQDN) hello de ressource hello à l’aide de hello IP.
6. Sélectionnez **OK** bas l’enregistrement DNS de hello panneau toocreate hello hello.

![ajouter un panneau du jeu d’enregistrements](./media/dns-reverse-dns-hosting/figure7.png)

Hello Voici des exemples sur la façon de toocomplete cette tâche avec PowerShell et hello AzureCLI :

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a>Azure CLI 1.0

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a>Azure CLI 2.0

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a>Afficher des Enregistrements

les enregistrements de hello tooview vous avez créé, accédez à zone DNS de tooyour Bonjour portail Azure. Bonjour partie basse de hello **zone DNS** panneau, vous pouvez voir des enregistrements hello pour la zone DNS de hello. Vous devez voir hello par défaut enregistrements NS et SOA, qui sont créées dans chaque zone, ainsi que les nouveaux enregistrements que vous avez créé.

### <a name="ipv4"></a>IPv4

Panneau zone DNS, affichant les enregistrements PTR de IPv4 :

![panneau zone DNS](./media/dns-reverse-dns-hosting/figure8.png)

Hello exemples suivants montrent comment tooview hello PTR enregistre à l’aide de PowerShell ou hello CLI d’Azure :

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a>IPv6

Panneau zone DNS, affichant les enregistrements PTR de IPv6 :

![panneau zone DNS](./media/dns-reverse-dns-hosting/figure9.png)

Hello Voici des exemples sur la modification des enregistrements tooview hello avec PowerShell et hello AzureCLI :

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a>Forum Aux Questions

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a>Puis-je héberger des zones de recherche inversée DNS pour les blocs IP attribués par mon fournisseur de services Internet sur Azure DNS ?

Oui. Hébergeant des zones de recherche inversée (ARPA) hello pour vos propres plages IP dans le système DNS Azure est entièrement pris en charge.

Créer une zone de recherche inversée hello dans le système DNS Azure comme expliqué dans cet article, puis de travailler avec votre fournisseur de services Internet trop[délégué hello zone](dns-domain-delegation.md).  Vous pouvez ensuite gérer les enregistrements PTR hello pour chaque recherche inversée Bonjour même façon que d’autres types d’enregistrements.

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a>Combien coûte l’hébergement de ma zone de recherche DNS inversée ?

Zone de recherche DNS inversée hello d’hébergement pour votre bloc IP affectée par le fournisseur de services Internet dans DNS Azure est facturée au [taux Azure DNS standard](https://azure.microsoft.com/pricing/details/dns/).

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a>Puis-je héberger des zones de recherche inversée DNS pour les adresses IPv4 et IPv6 dans Azure DNS ?

Oui. Cet article explique comment toocreate à la fois IPv4 et IPv6 de zones de recherche DNS dans Azure DNS inversée.

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a>Puis-je importer une zone de recherche DNS inversée existante ?

Oui. Vous pouvez utiliser des zones DNS existantes de hello CLI d’Azure tooimport dans le système DNS Azure. Cela fonctionne pour les zones de recherche directe et des zones de recherche inversée.

Pour plus d’informations, consultez [importer et exporter un fichier de zone DNS à l’aide de CLI d’Azure hello](dns-import-export.md).

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur le DNS inversé, consultez [Recherche DNS inversée sur Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).
<br>
Découvrez comment trop[gère les enregistrements DNS inverses pour vos services Azure](dns-reverse-dns-for-azure-services.md).
