---
title: "aaaManage DNS des enregistrements dans DNS Azure à l’aide d’Azure PowerShell | Documents Microsoft"
description: "Gestion des jeux d'enregistrements DNS et des enregistrements dans Azure DNS lorsque votre domaine est hébergé dans Azure DNS. Toutes les commandes PowerShell pour les opérations sur les jeux d'enregistrements et les enregistrements."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 7136a373-0682-471c-9c28-9e00d2add9c2
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: bfdf116e174d06db0514abdc0ec3f4fc4ee0a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a>Gérer les enregistrements et jeux d’enregistrements DNS dans Azure DNS à l’aide d’Azure PowerShell

> [!div class="op_single_selector"]
> * [Portail Azure](dns-operations-recordsets-portal.md)
> * [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

Cet article explique la modification des enregistrements par toomanage DNS pour votre zone DNS à l’aide d’Azure PowerShell. Enregistrements DNS peuvent également être gérés à l’aide de hello inter-plateformes [CLI d’Azure](dns-operations-recordsets-cli.md) ou hello [portail Azure](dns-operations-recordsets-portal.md).

exemples Hello dans cet article supposent que vous avez déjà [installé Azure PowerShell, signé et la création d’une zone DNS](dns-operations-dnszones.md).

## <a name="introduction"></a>Introduction

Avant de créer des enregistrements DNS dans le système DNS d’Azure, vous devez d’abord toounderstand comment Azure DNS organise les enregistrements DNS dans les jeux d’enregistrements DNS.

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

Pour plus d’informations sur les enregistrements DNS dans Azure DNS, voir [Enregistrements et zones DNS](dns-zones-records.md).


## <a name="create-a-new-dns-record"></a>Créer un enregistrement DNS

Si votre nouvel enregistrement hello même nom et le type en tant qu’un enregistrement existant, vous devez trop[ajouter le jeu d’enregistrements existant toohello](#add-a-record-to-an-existing-record-set). Si votre nouvel enregistrement a un tooall de nom et type de différents enregistrements existants, vous devez toocreate un nouveau jeu d’enregistrements. 

### <a name="create-a-records-in-a-new-record-set"></a>Créer des enregistrements « A » dans un nouveau jeu d’enregistrements

Vous créez des jeux d’enregistrements à l’aide de hello `New-AzureRmDnsRecordSet` applet de commande. Lorsque vous créez un jeu d’enregistrements, vous avez besoin de nom de jeu d’enregistrements toospecify hello, zone de hello, hello création toolive (TTL), type d’enregistrement hello et hello enregistrements toobe.

paramètres de Hello pour ajouter le jeu d’enregistrements enregistrements tooa varient en fonction de type hello du jeu d’enregistrements hello. Par exemple, lorsque vous utilisez un jeu d’enregistrements de type « A », vous avez besoin d’adresse IP de toospecify hello à l’aide du paramètre hello `-IPv4Address`. D’autres paramètres sont utilisés pour d’autres types d’enregistrements. Pour plus d’informations, voir les [autres exemples de types d’enregistrements](#additional-record-type-examples).

Hello exemple suivant crée un enregistrement avec le nom relatif de hello « www » Bonjour Zone du DNS « contoso.com ». nom qualifié complet de Hello du jeu d’enregistrements hello est « www.contoso.com ». type d’enregistrement Hello est « A » et hello durée de vie est 3 600 secondes. jeu d’enregistrements Hello contient un enregistrement unique, avec l’adresse IP « 1.2.3.4 ».

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

toocreate un jeu d’enregistrements à hello 'apex » d’une zone (dans ce cas, « contoso.com »), utilisez le nom de jeu d’enregistrements hello ' @' (sans guillemets) :

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

Si vous avez besoin d’un jeu d’enregistrements contenant plusieurs enregistrements de toocreate, tout d’abord créer un tableau local et ajouter des enregistrements de hello, puis passer le tableau de hello trop`New-AzureRmDnsRecordSet` comme suit :

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

[Métadonnées du jeu d’enregistrements](dns-zones-records.md#tags-and-metadata) peuvent être des données spécifiques à l’application tooassociate utilisées avec chaque jeu d’enregistrements, en tant que paires clé-valeur. Hello suivant montre comment toocreate un jeu d’enregistrements avec deux entrées de métadonnées, « dept = finance' et ' environnement = production ».

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

DNS Azure prend également en charge les jeux d’enregistrements 'empty', qui peut agir comme un espace réservé tooreserve un nom DNS avant de créer des enregistrements DNS. Jeux d’enregistrements vides est visibles dans le plan de contrôle hello Azure DNS, mais s’affichent sur les serveurs DNS de Azure hello. Bonjour à l’exemple suivant crée un jeu d’enregistrements vide :

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a>Créer des enregistrements d’autres types

Après avoir vu en détail comment toocreate 'A' enregistre, hello suivant exemples montrent comment toocreate les enregistrements d’autres types pris en charge par le système DNS Azure d’enregistrements.

Dans chaque cas, nous montrons comment toocreate un enregistrement défini contenant un seul enregistrement. Hello les exemples précédents pour les enregistrements 'A' peuvent être adapté toocreate jeux d’enregistrements d’autres types contenant plusieurs enregistrements avec des métadonnées, ou des jeux d’enregistrements de vide toocreate.

Nous ne donnent pas une toocreate exemple un jeu d’enregistrements SOA, étant donné que SOA est créées et supprimées avec chaque zone DNS et ne peut pas être créée ou supprimée séparément. Toutefois, [hello SOA peut être modifiée, comme indiqué dans un exemple plus loin](#to-modify-an-SOA-record).

### <a name="create-an-aaaa-record-set-with-a-single-record"></a>Créer un jeu d’enregistrements AAAA avec un seul enregistrement

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a>Créer un jeu d’enregistrements CNAME avec un seul enregistrement

> [!NOTE]
> les normes DNS Hello n’autorisent pas les enregistrements CNAME au sommet de hello d’une zone (`-Name '@'`), ni font qu’ils autorisent les jeux d’enregistrements contenant plusieurs enregistrements.
> 
> Pour plus d’informations, voir [Enregistrements CNAME](dns-zones-records.md#cname-records).


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a>Créer un jeu d’enregistrements MX avec un seul enregistrement

Dans cet exemple, nous utilisons le nom du jeu d’enregistrements hello ' @' enregistrement toocreate un MX au sommet de zone hello (dans ce cas, « contoso.com »).


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a>Créer un jeu d’enregistrements NS avec un seul enregistrement

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a>Créer un jeu d’enregistrements PTR avec un seul enregistrement

Dans ce cas, « my-arpa-zone.com' représente hello zone de recherche inversée ARPA représentant votre plage IP. Chaque enregistrement PTR dans cette zone correspond à adresse IP de tooan au sein de cette plage d’adresses IP. nom de l’enregistrement Hello « 10 » est le dernier octet de hello d’adresse IP de hello dans cette plage IP représentée par cet enregistrement.

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a>Créer un jeu d’enregistrements SRV avec un seul enregistrement

Lorsque vous créez un [jeu d’enregistrements SRV](dns-zones-records.md#srv-records), spécifiez hello  *\_service* et  *\_protocole* Bonjour nom du jeu d’enregistrements. Il n’existe aucun besoin tooinclude ' @' Bonjour jeu d’enregistrements nom lors de la création d’un enregistrement SRV définie au sommet de zone hello.

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a>Créer un jeu d’enregistrements TXT avec un seul enregistrement

Hello suivant montre comment enregistrer des toocreate un TXT. Pour plus d’informations sur la longueur maximale de la chaîne hello pris en charge dans les enregistrements TXT, consultez [enregistrements TXT](dns-zones-records.md#txt-records).

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a>Obtention d’un jeu d'enregistrements

tooretrieve un jeu d’enregistrements existant, utilisez `Get-AzureRmDnsRecordSet`. Cette applet de commande retourne un objet local représentant hello jeu d’enregistrements dans DNS Azure.

Comme avec `New-AzureRmDnsRecordSet`, nom du jeu d’enregistrements hello donné doit être un *relatif* nom, qui signifie qu’il doit exclure le nom de la zone hello. Vous devez également le type d’enregistrement toospecify hello et zone hello contenant le jeu d’enregistrements hello.

Hello suivant montre comment tooretrieve un jeu d’enregistrements. Dans cet exemple, les zones de hello est spécifié à l’aide de hello `-ZoneName` et `-ResourceGroupName` paramètres.

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

Vous pouvez également spécifier également zone hello à l’aide d’un objet de fuseau, passé à l’aide de hello `-Zone` paramètre.

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a>Liste des jeux d'enregistrements

Vous pouvez également utiliser `Get-AzureRmDnsZone` des jeux d’enregistrements de toolist dans une zone, en omettant hello `-Name` et/ou `-RecordType` paramètres.

Hello exemple suivant retourne tous les enregistrements définit dans la zone de hello :

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

Hello suivant montre comment tous les jeux d’un type donné d’enregistrements peuvent être récupérées en spécifiant le type d’enregistrement hello pendant enregistrement de hello l'omission de définie le nom :

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

tooretrieve définit de tous les enregistrements avec un nom donné, entre les types d’enregistrement, vous devez tooretrieve tous les jeux d’enregistrements, puis filtre hello résultats :

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

Bonjour tous les exemples ci-dessus, zone de hello peut être spécifié à l’aide de hello `-ZoneName` et `-ResourceGroupName`paramètres (comme indiqué), ou en spécifiant un objet de la zone :

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-tooan-existing-record-set"></a>Ajouter un enregistrement tooan existante du jeu d’enregistrements

tooadd un enregistrement existant tooan enregistrement défini, procédez comme hello trois comme suit :

1. Obtenir le jeu d’enregistrements existant hello

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. Ajoutez hello nouvel enregistrement toohello local ensemble d’enregistrements. Cette opération se fait hors connexion.

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. Valider hello modification toohello arrière service DNS Azure. 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

À l’aide de `Set-AzureRmDnsRecordSet` *remplace* hello enregistrement existant, défini dans le système DNS Azure (et tous les enregistrements qu’il contient) avec le jeu d’enregistrements hello spécifié. [Vérification ETag](dns-zones-records.md#etags) servent tooensure des modifications simultanées ne sont pas remplacées. Vous pouvez utiliser hello facultatif `-Overwrite` commutateur toosuppress ces vérifications.

Séquence d’opérations peut également être *dirigés*, ce qui signifie que vous passez un objet de jeu d’enregistrements hello par une barre verticale hello plutôt que d’en lui passant comme paramètre :

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

exemples de Hello ci-dessus montrent comment définie des tooadd un 'A' enregistrement existant tooan enregistrements de type « A ». Une séquence d’opérations similaire est utilisé tooadd enregistrements toorecord définit d’autres types, en remplaçant hello `-Ipv4Address` paramètre de `Add-AzureRmDnsRecordConfig` avec un autre type d’enregistrement Paramètres tooeach spécifique. Hello paramètres pour chaque type d’enregistrement sont hello même que pour hello `New-AzureRmDnsRecordConfig` applet de commande, comme indiqué dans [exemples du type d’enregistrement supplémentaires](#additional-record-type-examples) ci-dessus.

Les jeux d’enregistrements de type « CNAME » ou « SOA » ne peuvent pas contenir plusieurs enregistrements. Cette contrainte se produit à partir des normes DNS hello. Il ne s’agit pas d’une limitation d’Azure DNS.

## <a name="remove-a-record-from-an-existing-record-set"></a>Suppression d’un enregistrement d’un jeu d'enregistrements existant

Bonjour processus tooremove un enregistrement à partir d’un jeu d’enregistrements est similaire tooadd de processus toohello un enregistrement tooan existant enregistrer ensemble :

1. Obtenir le jeu d’enregistrements existant hello

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. Supprimer l’enregistrement de hello à partir de l’objet de jeu d’enregistrements local hello. Cette opération se fait hors connexion. enregistrement Hello est en cours de suppression doit être une correspondance exacte avec un enregistrement existant entre tous les paramètres.

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. Valider hello modification toohello arrière service DNS Azure. Hello utilisation facultative `-Overwrite` commutateur toosuppress [Etag vérifie](dns-zones-records.md#etags) de modifications simultanées.

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

À l’aide de hello ci-dessus séquence tooremove hello dernier à partir d’un jeu d’enregistrements ne supprime pas le jeu d’enregistrements hello, au lieu de cela, elle laisse un jeu d’enregistrements vide. tooremove un jeu d’enregistrements, consultez [supprimer un jeu d’enregistrements](#delete-a-record-set).

De même tooadding enregistrements tooa jeu d’enregistrements, séquence hello de tooremove opérations un jeu d’enregistrements peut également être transmis :

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

Différents types d’enregistrements sont pris en charge en passant les paramètres spécifiques au type approprié hello trop`Remove-AzureRmDnsRecordSet`. Hello paramètres pour chaque type d’enregistrement sont hello même que pour hello `New-AzureRmDnsRecordConfig` applet de commande, comme indiqué dans [exemples du type d’enregistrement supplémentaires](#additional-record-type-examples) ci-dessus.


## <a name="modify-an-existing-record-set"></a>Modifier un jeu d’enregistrements

Hello étapes permettant de modifier un jeu d’enregistrements existant sont similaires toohello que vous prenez lors de l’ajout ou la suppression des enregistrements à partir d’un jeu d’enregistrements :

1. Récupérer hello existant jeu d’enregistrements à l’aide de `Get-AzureRmDnsRecordSet`.
2. Modifier un objet de jeu d’enregistrements local hello par :
    * ajout ou suppression d’enregistrements ;
    * Modification des paramètres de hello des enregistrements existants
    * La modification d’enregistrement de hello définie toolive TTL (time) et les métadonnées
3. Valider les modifications apportées à l’aide de hello `Set-AzureRmDnsRecordSet` applet de commande. Cela *remplace* hello enregistrement existant défini dans Azure DNS avec le jeu d’enregistrements hello spécifié.

Lorsque vous utilisez `Set-AzureRmDnsRecordSet`, [Etag vérifie](dns-zones-records.md#etags) servent tooensure des modifications simultanées ne sont pas remplacées. Vous pouvez utiliser hello facultatif `-Overwrite` commutateur toosuppress ces vérifications.

### <a name="tooupdate-a-record-in-an-existing-record-set"></a>définie des tooupdate un enregistrement d’un enregistrement existant

Dans cet exemple, nous changeons hello adresseIP de 'A' enregistrement existant :

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-an-soa-record"></a>toomodify un enregistrement SOA

Impossible d’ajouter ou supprimer des enregistrements de hello créé automatiquement SOA jeu d’enregistrements au sommet de zone hello (`-Name "@"`, y compris les guillemets). Toutefois, vous pouvez modifier les paramètres de hello dans hello enregistrement SOA (à l’exception de « hôte ») et enregistrement de hello définie la durée de vie.

Hello suivant montre l’exemple de comment toochange hello *messagerie* propriété Hello enregistrement SOA :

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a>enregistrements toomodify NS au sommet de zone hello

jeu au sommet de zone hello d’enregistrements NS Hello sont automatiquement créé avec chaque zone DNS. Il contient les noms de hello de zone de hello Azure DNS nom serveurs toohello attribué.

Vous pouvez ajouter des noms supplémentaires serveurs toothis NS jeu d’enregistrements, toosupport domaines l’hébergement avec le fournisseur DNS. Vous pouvez également modifier la durée de vie de hello et les métadonnées pour ce jeu d’enregistrements. Toutefois, vous ne peut pas supprimer ou modifier les serveurs de noms DNS Azure hello préremplies.

Notez que cela s’applique uniquement toohello NS jeu d’enregistrements au sommet de zone hello. Autres jeux d’enregistrements NS dans votre zone (comme les zones enfant toodelegate utilisé) peut être modifié sans contrainte.

Bonjour à l’exemple suivant montre comment tooadd un enregistrement de noms supplémentaires server toohello NS définie les au sommet de zone hello :

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-record-set-metadata"></a>métadonnées du jeu d’enregistrement de toomodify

[Métadonnées du jeu d’enregistrements](dns-zones-records.md#tags-and-metadata) peuvent être des données spécifiques à l’application tooassociate utilisées avec chaque jeu d’enregistrements, en tant que paires clé-valeur.

Hello suivant montre comment définir les métadonnées de hello toomodify d’un enregistrement existant :

```powershell
# Get hello record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a>Supprimer un jeu d’enregistrements

Jeux d’enregistrements peut être supprimés à l’aide de hello `Remove-AzureRmDnsRecordSet` applet de commande. Suppression d’un jeu d’enregistrements supprime également tous les enregistrements dans le jeu d’enregistrements hello.

> [!NOTE]
> Vous ne pouvez pas supprimer hello SOA et NS jeux d’enregistrements au sommet de zone hello (`-Name '@'`).  DNS Azure ces créés automatiquement lors de la zone de hello a été créé et supprime automatiquement lors de la zone de hello est supprimée.

Hello suivant montre comment toodelete un jeu d’enregistrements. Dans cet exemple, nom du jeu d’enregistrements hello, type de jeu d’enregistrements, nom de la zone et groupe de ressources sont chacun spécifiés explicitement.

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

Sinon, jeu d’enregistrements hello peut être spécifié par le nom et le type et hello spécifié à l’aide d’un objet de la zone :

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

Comme une troisième option, hello jeu d’enregistrements lui-même peuvent être spécifié à l’aide d’un objet de jeu d’enregistrements :

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

Lorsque vous spécifiez l’enregistrement de hello défini toobe supprimée à l’aide d’un objet de jeu d’enregistrements, [Etag vérifie](dns-zones-records.md#etags) servent tooensure des modifications simultanées ne sont pas supprimées. Vous pouvez utiliser hello facultatif `-Overwrite` commutateur toosuppress ces vérifications.

objet de jeu d’enregistrements Hello peut également être transmis au lieu de passé en tant que paramètre :

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a>Invites de confirmation

Hello `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, et `Remove-AzureRmDnsRecordSet` prend en charge les applets de commande toutes les invites de confirmation.

Chaque applet de commande vous demande de confirmer si hello `$ConfirmPreference` a la valeur de variable de préférence PowerShell `Medium` ou inférieure. Depuis la valeur par défaut de hello `$ConfirmPreference` est `High`, ces messages ne sont pas affectés lors de l’utilisation de paramètres de PowerShell hello par défaut.

Vous pouvez remplacer hello actuel `$ConfirmPreference` paramètre à l’aide de hello `-Confirm` paramètre. Si vous spécifiez `-Confirm` ou `-Confirm:$True` , hello applet de commande vous demande confirmation avant qu’il s’exécute. Si vous spécifiez `-Confirm:$False` , applet de commande hello ne vous demande pas de confirmation. 

Pour plus d’informations sur les paramètres `-Confirm` et `$ConfirmPreference`, voir [À propos des variables de préférence](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).

## <a name="next-steps"></a>Étapes suivantes

Apprenez-en davantage sur les [zones et enregistrements dans Azure DNS](dns-zones-records.md).
<br>
Découvrez comment trop[protéger les zones et les enregistrements](dns-protect-zones-recordsets.md) lors de l’utilisation d’Azure DNS.
<br>
Hello de révision [documentation de référence PowerShell pour Azure DNS](/powershell/module/azurerm.dns).
