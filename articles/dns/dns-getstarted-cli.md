---
title: "aaaGet main DNS Azure à l’aide d’Azure CLI 2.0 | Documents Microsoft"
description: "Découvrez comment toocreate DNS zone et cet enregistrement dans le système DNS Azure. Ceci est un toocreate guide pas à pas et que vous gérez votre première zone DNS et un enregistrement à l’aide de hello Azure CLI 2.0."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 8a894941e9910d5cc35394a1be9dbca9792613f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-20"></a>Prise en main d’Azure DNS à l’aide d’Azure CLI 2.0

> [!div class="op_single_selector"]
> * [portail Azure](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Azure CLI 1.0](dns-getstarted-cli-nodejs.md)
> * [Azure CLI 2.0](dns-getstarted-cli.md)

Cet article vous guide tout hello étapes toocreate votre première zone DNS et à l’aide de l’enregistrement hello à multiplateforme Azure CLI 2.0, qui est disponible pour Windows, Mac et Linux. Vous pouvez également effectuer ces étapes à l’aide de hello portail Azure ou Azure PowerShell.

Une zone DNS est toohost utilisé hello les enregistrements DNS pour un domaine particulier. toostart hébergeant votre domaine dans le système DNS Azure, vous devez toocreate une zone DNS pour ce nom de domaine. Chaque enregistrement DNS pour votre domaine est ensuite créé à l’intérieur de cette zone DNS. Enfin, toopublish votre serveur DNS de la zone toohello Internet, vous avez besoin de serveurs de noms tooconfigure hello pour le domaine de hello. Chacune de ces étapes est décrite ci-dessous.

Ces instructions supposent que vous avez déjà installé et connecté tooAzure CLI 2.0. Pour plus d’aide, consultez [fonctionnement des zones toomanage DNS à l’aide d’Azure CLI 2.0](dns-operations-dnszones-cli.md).

## <a name="create-hello-resource-group"></a>Créer le groupe de ressources hello

Avant de créer la zone DNS de hello, un groupe de ressources est créé de Zone DNS de hello toocontain. Hello Voici commande hello.

```azurecli
az group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a>Création d’une zone DNS

Une zone DNS est créée à l’aide de hello `az network dns zone create` commande. aide toosee de cette commande, tapez `az network dns zone create -h`.

Hello exemple suivant crée une zone DNS appelée *contoso.com* dans le groupe de ressources hello *MyResourceGroup*. Utilisez hello exemple toocreate une zone DNS, en spécifiant les valeurs hello pour votre propre.

```azurecli
az network dns zone create -g MyResourceGroup -n contoso.com
```


## <a name="create-a-dns-record"></a>Créer un enregistrement DNS

toocreate un enregistrement DNS, utilisez hello `az network dns record-set [record type] add-record` commande. Pour obtenir de l’aide, concernant les enregistrements A par exemple, consultez `azure network dns record-set A add-record -h`.

Hello exemple suivant crée un enregistrement avec le nom relatif de hello « www » Bonjour Zone du DNS « contoso.com », dans le groupe de ressources « MyResourceGroup ». nom qualifié complet de Hello du jeu d’enregistrements hello est « www.contoso.com ». type d’enregistrement Hello est « A », avec l’adresse IP « 1.2.3.4 », et une durée de vie de 3 600 secondes (1 heure) de la valeur par défaut est utilisée.

```azurecli
az network dns record-set a add-record -g MyResourceGroup -z contoso.com -n www -a 1.2.3.4
```

Pour les autres types d’enregistrements, pour des jeux d’enregistrements avec plusieurs enregistrements, pour les autres valeurs de durée de vie et toomodify les enregistrements existants, consultez [enregistrements DNS de gérer et jeux d’enregistrements à l’aide de Azure CLI 2.0 hello](dns-operations-recordsets-cli.md).


## <a name="view-records"></a>Affichage des enregistrements

les enregistrements DNS toolist hello dans votre fuseau, utilisez :

```azurecli
az network dns record-set list -g MyResourceGroup -z contoso.com
```


## <a name="update-name-servers"></a>Mettre à jour les serveurs de noms

Une fois que vous êtes satisfait que votre zone DNS et les enregistrements ont été configurées correctement, vous devez tooconfigure votre nom de domaine toouse serveurs DNS de Azure hello. Cela permet à d’autres utilisateurs sur hello Internet toofind vos enregistrements DNS.

serveurs de noms Hello pour votre zone sont fournies par hello `az network dns zone show` commande. noms de serveur nom toosee hello, utilisez JSON de sortie, comme indiqué dans hello l’exemple suivant.

```azurecli
az network dns zone show -g MyResourceGroup -n contoso.com -o json

{
  "etag": "00000003-0000-0000-b40d-0996b97ed101",
  "id": "/subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-01.azure-dns.com.",
    "ns2-01.azure-dns.net.",
    "ns3-01.azure-dns.org.",
    "ns4-01.azure-dns.info."
  ],
  "numberOfRecordSets": 3,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

Ces serveurs de noms doivent être configurés avec le Registre des noms de domaine hello (où vous avez acheté nom de domaine hello). Tooset d’option hello des serveurs de noms hello pour le domaine de hello propose de votre bureau d’enregistrement. Pour plus d’informations, consultez [déléguer votre tooAzure de domaine DNS](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Supprimer toutes les ressources
 
toodelete toutes les ressources créées dans cet article, hello take suivant l’étape :

```azurecli
az group delete --name MyResourceGroup
```

## <a name="next-steps"></a>Étapes suivantes

toolearn en savoir plus sur Azure DNS, consultez [vue d’ensemble de DNS Azure](dns-overview.md).

toolearn savoir plus sur la gestion des zones DNS dans le système DNS Azure, consultez [zones DNS de gestion dans DNS Azure à l’aide d’Azure CLI 2.0](dns-operations-dnszones-cli.md).

toolearn savoir plus sur la gestion des enregistrements DNS dans le système DNS Azure, consultez [des enregistrements DNS de gérer et enregistrement définit dans le système DNS d’Azure à l’aide d’Azure CLI 2.0](dns-operations-recordsets-cli.md).
