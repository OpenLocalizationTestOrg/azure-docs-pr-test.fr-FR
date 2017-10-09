---
title: aaaDelegate votre tooAzure de domaine DNS | Documents Microsoft
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
ms.openlocfilehash: f780bdaa416150e5e3afe6c6845dc75ba54b6203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-a-domain-tooazure-dns"></a>Déléguer un tooAzure de domaine DNS

DNS Azure vous permet de toohost une zone DNS et gérer les enregistrements DNS de hello pour un domaine dans Azure. Dans l’ordre pour les requêtes DNS pour un tooreach de domaine DNS d’Azure, domaine de hello a toobe déléguée tooAzure DNS dans le domaine parent hello. N’oubliez pas d’Azure DNS n’est pas de domaines hello. Cet article explique comment toodelegate votre tooAzure de domaine DNS.

Pour les domaines achetés à partir d’un bureau d’enregistrement, votre bureau d’enregistrement offre tooset d’option hello ces enregistrements NS. Il est inutile tooown un toocreate domaine une zone DNS avec ce nom de domaine dans le système DNS Azure. Toutefois, vous n’avez pas besoin de tooown hello domaine tooset des hello tooAzure de délégation DNS avec le bureau d’enregistrement hello.

Par exemple, supposons que vous achetez le domaine hello 'contoso.net' et créez une zone avec le nom hello 'contoso.net' dans le système DNS Azure. En tant que propriétaire hello du domaine de hello, votre bureau d’enregistrement offre que Hello d’adresses de serveur de noms option tooconfigure hello (autrement dit, les enregistrements hello NS) pour votre domaine. bureau d’enregistrement Hello stocke ces enregistrements NS dans le domaine parent hello, dans ce cas, « .net ». Les clients monde hello peuvent ensuite être domaine tooyour suggérés dans la zone DNS de Azure lors de la tentative d’enregistrements DNS tooresolve 'contoso.net'.

## <a name="create-a-dns-zone"></a>Création d’une zone DNS

1. Se connecter toohello portail Azure
1. Dans le menu du Hub hello, cliquez sur, puis cliquez sur **Nouveau > mise en réseau >** puis cliquez sur **zone DNS** Panneau de zone DNS de créer tooopen hello.

    ![Zone DNS](./media/dns-domain-delegation/dns.png)

1. Sur hello **zone DNS de créer** panneau hello valeurs suivantes, puis entrez **créer**:

   | **Paramètre** | **Valeur** | **Détails** |
   |---|---|---|
   |**Name**|contoso.net|nom Hello de zone DNS de hello|
   |**Abonnement**|[Votre abonnement]|Sélectionnez une passerelle d’application abonnement toocreate hello dans.|
   |**Groupe de ressources**|**Créer :** contosoRG|Créez un groupe de ressources. nom de groupe de ressources Hello doit être unique au sein de l’abonnement hello sélectionné. toolearn plus d’informations sur les groupes de ressources, lire hello [le Gestionnaire de ressources](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) l’article de vue d’ensemble.|
   |**Emplacement**|Ouest des États-Unis||

> [!NOTE]
> groupe de ressources Hello fait référence emplacement toohello hello du groupe de ressources et n’a aucun impact sur la zone DNS de hello. emplacement des zones DNS Hello est toujours « globaux » et n’est pas affiché.

## <a name="retrieve-name-servers"></a>Récupérer les serveurs de noms

Vous pouvez déléguer votre tooAzure de zone DNS DNS, vous devez tout d’abord tooknow hello server nom de votre zone. Azure DNS alloue des serveurs de noms à partir d’un pool chaque fois qu’une zone est créée.

1. Avec zone DNS de hello créé, Bonjour Azure portal **favoris** volet, cliquez sur **toutes les ressources**. Cliquez sur hello **contoso.net** zone DNS Bonjour **toutes les ressources** panneau. Si l’abonnement hello déjà sélectionné comporte plusieurs ressources, vous pouvez entrer **contoso.net** Bonjour filtre par nom... passerelle d’application hello boîte tooeasily accès. 

1. Récupérer des serveurs de noms hello à partir du Panneau de zone DNS hello. Dans cet exemple, la zone de hello 'contoso.net' a été affectée à des serveurs de nom ' ns1-01.azure-dns.com', 'ns2-01.azure-dns .net', ' ns3-01.azure-dns.org », et « ns4-01.azure-dns.info':

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

DNS Azure crée automatiquement les enregistrements NS faisant autoritées dans votre zone contenant hello affecté des serveurs de noms.  noms de serveur de noms toosee hello via Azure PowerShell ou CLI d’Azure, vous devez simplement tooretrieve ces enregistrements.

Hello exemples suivants fournissent également des étapes de hello serveurs de noms tooretrieve hello pour une zone DNS Azure avec PowerShell et CLI d’Azure.

### <a name="powershell"></a>PowerShell

```powershell
# hello record name "@" is used toorefer toorecords at hello top of hello zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

Hello, l’exemple suivant est la réponse de hello.

```
Name              : @
ZoneName          : contoso.net
ResourceGroupName : contosorg
Ttl               : 172800
Etag              : 03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5
RecordType        : NS
Records           : {ns1-07.azure-dns.com., ns2-07.azure-dns.net., ns3-07.azure-dns.org.,
                    ns4-07.azure-dns.info.}
Metadata          :
```

### <a name="azure-cli"></a>Interface de ligne de commande Azure

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

Hello, l’exemple suivant est la réponse de hello.

```json
{
  "etag": "03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosoRG/providers/Microsoft.Network/dnszones/contoso.net/NS/@",
  "metadata": null,
  "name": "@",
  "nsRecords": [
    {
      "nsdname": "ns1-07.azure-dns.com."
    },
    {
      "nsdname": "ns2-07.azure-dns.net."
    },
    {
      "nsdname": "ns3-07.azure-dns.org."
    },
    {
      "nsdname": "ns4-07.azure-dns.info."
    }
  ],
  "resourceGroup": "contosoRG",
  "ttl": 172800,
  "type": "Microsoft.Network/dnszones/NS"
}
```

## <a name="delegate-hello-domain"></a>Domaine de hello délégué

Maintenant que la zone DNS de hello est créé et que les serveurs de noms hello, le domaine parent hello doit toobe mis à jour avec les serveurs DNS de Azure hello. Chaque bureau d’enregistrement a leurs propres enregistrements DNS management tools toochange hello name server pour un domaine. Dans la page de gestion hello du bureau d’enregistrement DNS, modifier les enregistrements NS hello et remplacer les enregistrements NS hello hello ceux créé par le système DNS Azure.

Lors de la délégation un tooAzure de domaine DNS, vous devez utiliser des noms de serveur de nom de hello fournies par le système DNS Azure. Il est recommandé de toouse toutes les quatre noms des noms de serveur, quel que soit le nom hello de votre domaine. Délégation de domaine ne nécessite pas de toouse de nom de serveur de nom hello hello du même domaine de niveau supérieur que votre domaine.

Vous ne devez pas utiliser « enregistrements glue » toopoint toohello Azure DNS nom adresses IP de serveur, étant donné que ces adresses IP peuvent changer dans les futures. Les délégations utilisant les noms de serveurs de noms dans votre propre zone (parfois appelés « serveurs de noms de redirection vers un microsite ») ne sont actuellement pas prises en charge dans Azure DNS.

## <a name="verify-name-resolution-is-working"></a>Vérifier le fonctionnement de la résolution de noms

Après avoir effectué la délégation de hello, vous pouvez vérifier que la résolution de noms fonctionne à l’aide d’un outil tel que « nslookup » tooquery hello enregistrement SOA de votre zone (qui est créé automatiquement lors de la création de la zone de hello).

Vous n’avez pas de serveurs de noms DNS Azure toospecify hello, si la délégation contrainte hello a été configurée correctement, hello DNS résolution processus normal détecte automatiquement les serveurs de noms hello.

```
nslookup -type=SOA contoso.com
```

Hello Voici un exemple de réponse à partir de hello précédant la commande :

```
Server: ns1-04.azure-dns.com
Address: 208.76.47.4

contoso.com
primary name server = ns1-04.azure-dns.com
responsible mail addr = msnhst.microsoft.com
serial = 1
refresh = 900 (15 mins)
retry = 300 (5 mins)
expire = 604800 (7 days)
default TTL = 300 (5 mins)
```

## <a name="delegate-sub-domains-in-azure-dns"></a>Déléguer les sous-domaines dans Azure DNS

Si vous souhaitez tooset d’une zone enfant distincte, vous pouvez déléguer un sous-domaine dans Azure DNS. Par exemple, avoir défini et délégués 'contoso.net' dans le système DNS Azure, supposons que vous aimeriez tooset d’une zone enfant distincte, 'partners.contoso.net'.

1. Créer hello enfant zone 'partners.contoso.net' dans le système DNS Azure.
2. Recherchez les enregistrements NS faisant autoritées hello dans hello enfant zone tooobtain hello serveurs de noms hébergeant la zone enfant de hello dans Azure DNS.
3. Déléguer hello enfant en configurant les enregistrements NS dans la zone parente de hello pointant vers la zone enfant de toohello.

### <a name="create-a-dns-zone"></a>Création d’une zone DNS

1. Se connecter toohello portail Azure
1. Dans le menu du Hub hello, cliquez sur, puis cliquez sur **Nouveau > mise en réseau >** puis cliquez sur **zone DNS** Panneau de zone DNS de créer tooopen hello.

    ![Zone DNS](./media/dns-domain-delegation/dns.png)

1. Sur hello **zone DNS de créer** panneau hello valeurs suivantes, puis entrez **créer**:

   | **Paramètre** | **Valeur** | **Détails** |
   |---|---|---|
   |**Name**|partners.contoso.net|nom Hello de zone DNS de hello|
   |**Abonnement**|[Votre abonnement]|Sélectionnez une passerelle d’application abonnement toocreate hello dans.|
   |**Groupe de ressources**|**Use Existing :** (Utiliser existant) contosoRG|Créez un groupe de ressources. nom de groupe de ressources Hello doit être unique au sein de l’abonnement hello sélectionné. toolearn plus d’informations sur les groupes de ressources, lire hello [le Gestionnaire de ressources](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) l’article de vue d’ensemble.|
   |**Emplacement**|Ouest des États-Unis||

> [!NOTE]
> groupe de ressources Hello fait référence emplacement toohello hello du groupe de ressources et n’a aucun impact sur la zone DNS de hello. emplacement des zones DNS Hello est toujours « globaux » et n’est pas affiché.

### <a name="retrieve-name-servers"></a>Récupérer les serveurs de noms

1. Avec zone DNS de hello créé, Bonjour Azure portal **favoris** volet, cliquez sur **toutes les ressources**. Cliquez sur hello **partners.contoso.net** zone DNS Bonjour **toutes les ressources** panneau. Si l’abonnement hello déjà sélectionné comporte plusieurs ressources, vous pouvez entrer **partners.contoso.net** Bonjour filtre par nom... zone DNS zone tooeasily accès hello.

1. Récupérer des serveurs de noms hello à partir du Panneau de zone DNS hello. Dans cet exemple, la zone de hello 'contoso.net' a été affectée à des serveurs de nom ' ns1-01.azure-dns.com', 'ns2-01.azure-dns .net', ' ns3-01.azure-dns.org », et « ns4-01.azure-dns.info':

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

DNS Azure crée automatiquement les enregistrements NS faisant autoritées dans votre zone contenant hello affecté des serveurs de noms.  noms de serveur de noms toosee hello via Azure PowerShell ou CLI d’Azure, vous devez simplement tooretrieve ces enregistrements.

### <a name="create-name-server-record-in-parent-zone"></a>Créer un enregistrement de serveur de noms dans la zone parente

1. Accédez toohello **contoso.net** zone DNS Bonjour portail Azure.
1. Cliquez sur **+ Jeu d’enregistrements**.
1. Sur hello **ajouter le jeu d’enregistrements** panneau, entrez hello valeurs suivantes, puis cliquez sur **OK**:

   | **Paramètre** | **Valeur** | **Détails** |
   |---|---|---|
   |**Name**|partenaires|nom de Hello de zone DNS d’enfant hello|
   |**Type**|NS|Utilisez NS pour les enregistrements de serveur de noms.|
   |**TTL**|1|Heure toolive.|
   |**Unité de durée de vie**|Heures|définit les toohours toolive unité de temps|
   |**SERVEUR DE NOMS**|{serveurs de noms à partir de la zone partners.contoso.net}|Entrez les 4 hello de serveurs de noms à partir de la zone de partners.contoso.net. |

   ![Dns-nameserver](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a>Déléguer des sous-domaines dans Azure DNS avec d’autres outils

Hello suivants fournit des exemples des étapes de hello toodelegate des sous-domaines dans DNS Azure avec PowerShell et l’interface CLI :

#### <a name="powershell"></a>PowerShell

Hello PowerShell l’exemple suivant montre comment cela fonctionne. Hello mêmes étapes peuvent être exécutées via hello portail Azure ou via hello CLI d’Azure inter-plateformes.

```powershell
# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
$parent = New-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
$child = New-AzureRmDnsZone -Name partners.contoso.net -ResourceGroupName contosoRG

# Retrieve hello authoritative NS records from hello child zone as shown in hello next example. This contains hello name servers assigned toohello child zone.
$child_ns_recordset = Get-AzureRmDnsRecordSet -Zone $child -Name "@" -RecordType NS

# Create hello corresponding NS record set in hello parent zone toocomplete hello delegation. hello record set name in hello parent zone matches hello child zone name, in this case "partners".
$parent_ns_recordset = New-AzureRmDnsRecordSet -Zone $parent -Name "partners" -RecordType NS -Ttl 3600
$parent_ns_recordset.Records = $child_ns_recordset.Records
Set-AzureRmDnsRecordSet -RecordSet $parent_ns_recordset
```

Utilisez `nslookup` tooverify que tout est configuré correctement en recherchant hello enregistrement SOA de zone enfant de hello.

```
nslookup -type=SOA partners.contoso.com
```

```
Server: ns1-08.azure-dns.com
Address: 208.76.47.8

partners.contoso.com
    primary name server = ns1-08.azure-dns.com
    responsible mail addr = msnhst.microsoft.com
    serial = 1
    refresh = 900 (15 mins)
    retry = 300 (5 mins)
    expire = 604800 (7 days)
    default TTL = 300 (5 mins)
```

#### <a name="azure-cli"></a>Interface de ligne de commande Azure

```azurecli
#!/bin/bash

# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

Récupérer les serveurs nom hello hello `partners.contoso.net` zone à partir de la sortie de hello.

```
{
  "etag": "00000003-0000-0000-418f-250de2b2d201",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosorg/providers/Microsoft.Network/dnszones/partners.contoso.net",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "partners.contoso.net",
  "nameServers": [
    "ns1-09.azure-dns.com.",
    "ns2-09.azure-dns.net.",
    "ns3-09.azure-dns.org.",
    "ns4-09.azure-dns.info."
  ],
  "numberOfRecordSets": 2,
  "resourceGroup": "contosorg",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

Créer le jeu d’enregistrements hello et les enregistrements NS pour chaque serveur de noms.

```azurecli
#!/bin/bash

# Create hello record set
az network dns record-set ns create --resource-group contosorg --zone-name contoso.net --name partners

# Create a ns record for each name server.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns1-09.azure-dns.com.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns2-09.azure-dns.net.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns3-09.azure-dns.org.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns4-09.azure-dns.info.
```

## <a name="delete-all-resources"></a>Supprimer toutes les ressources

toodelete toutes les ressources créées dans cet article, hello complète comme suit :

1. Bonjour Azure portal **favoris** volet, cliquez sur **toutes les ressources**. Cliquez sur hello **contosorg** groupe de ressources Bonjour toutes les lames de ressources. Si l’abonnement hello déjà sélectionné comporte plusieurs ressources, vous pouvez entrer **contosorg** Bonjour **filtrer par nom...** groupe de ressources boîte tooeasily accès hello.
1. Bonjour **contosorg** panneau, cliquez sur hello **supprimer** bouton.
1. Hello portail requiert vous tootype hello nom du tooconfirm de groupe de ressources hello que vous souhaitez toodelete il. Type *contosorg* pour le nom du groupe de ressources de hello, puis cliquez sur **supprimer**. La suppression d’un groupe de ressources supprime toutes les ressources dans le groupe de ressources hello, toujours que tooconfirm contenu hello d’un groupe de ressources avant de le supprimer. portail de Hello supprime toutes les ressources contenues dans le groupe de ressources hello, puis supprime le groupe de ressources hello lui-même. Cette opération prend plusieurs minutes.

## <a name="next-steps"></a>Étapes suivantes

[Gestion des zones DNS](dns-operations-dnszones.md)

[Gestion des enregistrements DNS](dns-operations-recordsets.md)
