---
title: "aaaGet main DNS Azure à l’aide de PowerShell | Documents Microsoft"
description: "Découvrez comment toocreate DNS zone et cet enregistrement dans le système DNS Azure. Ceci est un toocreate guide pas à pas et gérer votre première zone DNS et enregistrer à l’aide de PowerShell."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 0f9dead1e4b44fcc74c84a024c41cdfaeb02b5d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-powershell"></a>Prise en main d’Azure DNS à l’aide de PowerShell

> [!div class="op_single_selector"]
> * [Portail Azure](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Azure CLI 1.0](dns-getstarted-cli-nodejs.md)
> * [Azure CLI 2.0](dns-getstarted-cli.md)

Cet article vous assiste hello étapes toocreate votre première zone DNS et un enregistrement à l’aide d’Azure PowerShell. Vous pouvez également effectuer ces étapes à l’aide de hello portail Azure ou hello CLI d’Azure inter-plateformes.

Une zone DNS est toohost utilisé hello les enregistrements DNS pour un domaine particulier. toostart hébergeant votre domaine dans le système DNS Azure, vous devez toocreate une zone DNS pour ce nom de domaine. Chaque enregistrement DNS pour votre domaine est ensuite créé à l’intérieur de cette zone DNS. Enfin, toopublish votre serveur DNS de la zone toohello Internet, vous avez besoin de serveurs de noms tooconfigure hello pour le domaine de hello. Chacune de ces étapes est décrite ci-dessous.

Ces instructions supposent que vous avez déjà installé et connecté tooAzure PowerShell. Pour plus d’aide, consultez [fonctionnement des zones toomanage DNS à l’aide de PowerShell](dns-operations-dnszones.md).

## <a name="create-hello-resource-group"></a>Créer le groupe de ressources hello

Avant de créer la zone DNS de hello, un groupe de ressources est créé de Zone DNS de hello toocontain. Hello Voici commande hello.

```powershell
New-AzureRMResourceGroup -name MyResourceGroup -location "westus"
```

## <a name="create-a-dns-zone"></a>Création d’une zone DNS

Une zone DNS est créée à l’aide de hello `New-AzureRmDnsZone` applet de commande. Hello exemple suivant crée une zone DNS appelée *contoso.com* dans le groupe de ressources hello appelé *MyResourceGroup*. Utilisez hello exemple toocreate une zone DNS, en spécifiant les valeurs hello pour votre propre.

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a>Créer un enregistrement DNS

Vous créez des jeux d’enregistrements à l’aide de hello `New-AzureRmDnsRecordSet` applet de commande. Hello exemple suivant crée un enregistrement avec le nom relatif de hello « www » Bonjour Zone du DNS « contoso.com », dans le groupe de ressources « MyResourceGroup ». nom qualifié complet de Hello du jeu d’enregistrements hello est « www.contoso.com ». type d’enregistrement Hello est « A », avec l’adresse IP « 1.2.3.4 » et hello durée de vie est 3 600 secondes.

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

Pour les autres types d’enregistrements, pour des jeux d’enregistrements avec plusieurs enregistrements et les enregistrements existants toomodify, consultez [enregistrements DNS de gérer et jeux d’enregistrements à l’aide d’Azure PowerShell](dns-operations-recordsets.md). 


## <a name="view-records"></a>Affichage des enregistrements

les enregistrements DNS toolist hello dans votre fuseau, utilisez :

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a>Mettre à jour les serveurs de noms

Une fois que vous êtes satisfait que votre zone DNS et les enregistrements ont été configurées correctement, vous devez tooconfigure votre nom de domaine toouse serveurs DNS de Azure hello. Cela permet à d’autres utilisateurs sur hello Internet toofind vos enregistrements DNS.

serveurs de noms Hello pour votre zone sont fournies par hello `Get-AzureRmDnsZone` applet de commande :

```powershell
Get-AzureRmDnsZone -ZoneName contoso.com -ResourceGroupName MyResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-b40d-0996b97ed101
Tags                  : {}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org., ns4-01.azure-dns.info.}
NumberOfRecordSets    : 3
MaxNumberOfRecordSets : 5000
```

Ces serveurs de noms doivent être configurés avec le Registre des noms de domaine hello (où vous avez acheté nom de domaine hello). Tooset d’option hello des serveurs de noms hello pour le domaine de hello propose de votre bureau d’enregistrement. Pour plus d’informations, consultez [déléguer votre tooAzure de domaine DNS](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Supprimer toutes les ressources

toodelete toutes les ressources créées dans cet article, hello take suivant l’étape :

```powershell
Remove-AzureRMResourceGroup -Name MyResourceGroup
```

## <a name="next-steps"></a>Étapes suivantes

toolearn en savoir plus sur Azure DNS, consultez [vue d’ensemble de DNS Azure](dns-overview.md).

toolearn savoir plus sur la gestion des zones DNS dans le système DNS Azure, consultez [zones DNS de gestion dans DNS Azure à l’aide de PowerShell](dns-operations-dnszones.md).

toolearn savoir plus sur la gestion des enregistrements DNS dans le système DNS Azure, consultez [des enregistrements DNS de gérer et enregistrement définit dans le système DNS d’Azure à l’aide de PowerShell](dns-operations-recordsets.md).

