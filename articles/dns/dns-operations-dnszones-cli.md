---
title: zones DNS de Azure - Azure CLI 2.0 aaaManage DNS | Documents Microsoft
description: "Vous pouvez gérer des zones DNS à l’aide d’Azure CLI 2.0. Cet article explique comment tooupdate, supprimer et créer des zones DNS sur le système DNS Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: gwallace
ms.openlocfilehash: 3945a558b2db3490e50678d8395a47e55a85c8fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-20"></a>Comment toomanage les Zones DNS à l’aide d’Azure DNS hello Azure CLI 2.0

> [!div class="op_single_selector"]
> * [Portail](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)


Ce guide montre comment toomanage votre DNS zones à l’aide de hello inter-plateformes CLI d’Azure, qui est disponible pour Windows, Mac et Linux. Vous pouvez également gérer vos zones DNS à l’aide de [Azure PowerShell](dns-operations-dnszones.md) ou de bienvenue du portail Azure.

## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete

Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

* [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -notre CLI pour les modèles de déploiement gestion classique et les ressources des hello.
* [Azure CLI 2.0](dns-operations-dnszones-cli.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello.

## <a name="introduction"></a>Introduction

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a>Configuration d’Azure CLI 2.0 pour Azure DNS

### <a name="before-you-begin"></a>Avant de commencer

Vérifiez que vous disposez des éléments suivants avant de commencer votre configuration de hello.

* Un abonnement Azure. Si vous ne disposez pas déjà d’un abonnement Azure, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/).

* Installez hello dernière version de hello Azure CLI 2.0, disponible pour Windows, Linux ou Mac. Plus d’informations est disponible à l’adresse [installation Bonjour Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

### <a name="sign-in-tooyour-azure-account"></a>Se connecter tooyour compte Azure

Ouvrez une fenêtre de console et procédez à l’authentification à l’aide de vos informations d’identification. Pour plus d’informations, consultez le journal dans tooAzure de hello CLI d’Azure

```
az login
```

### <a name="select-hello-subscription"></a>Sélectionnez l’abonnement de hello

Vérifiez les abonnements hello pour le compte de hello.

```
az account list
```

Choisissez parmi vos toouse abonnements Azure.

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a>Créer un groupe de ressources

Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement. Cela est utilisé comme emplacement par défaut de hello pour les ressources dans ce groupe de ressources. Toutefois, étant donné que toutes les ressources DNS sont globales, pas régional, choix hello de l’emplacement du groupe de ressources n’a aucun impact sur le système DNS Azure.

Ignorez cette étape si vous utilisez un groupe de ressources existant.

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a>Obtenir de l’aide

Toutes les commandes CLI 2.0 relatives tooAzure DNS commence par `az network dns`. Aide est disponible pour chaque commande à l’aide de hello `--help` option (forme abrégée : `-h`).  Par exemple :

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a>Création d’une zone DNS

Une zone DNS est créée à l’aide de hello `az network dns zone create` commande. Pour obtenir de l’aide, consultez l’article `az network dns zone create -h`.

Hello exemple suivant crée une zone DNS appelée *contoso.com* dans le groupe de ressources hello appelé *MyResourceGroup*:

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a>toocreate une zone DNS avec balises

Hello suivant montre comment la zone avec deux toocreate DNS [Azure Resource Manager balises](dns-zones-records.md#tags), *projet = demo* et *env = test*, à l’aide de hello `--tags` paramètre (forme abrégée : `-t`) :

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a>Obtention d’une zone DNS

tooretrieve une zone DNS, utilisez `az network dns zone show`. Pour obtenir de l’aide, consultez l’article `az network dns zone show --help`.

exemple Hello retourne zone DNS de hello *contoso.com* et ses données associées du groupe de ressources *MyResourceGroup*. 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

Hello, l’exemple suivant est la réponse de hello.

```json
{
  "etag": "00000002-0000-0000-3d4d-64aa3689d201",
  "id": "/subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-04.azure-dns.com.",
    "ns2-04.azure-dns.net.",
    "ns3-04.azure-dns.org.",
    "ns4-04.azure-dns.info."
  ],
  "numberOfRecordSets": 4,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

Notez que les enregistrements DNS ne sont pas retournés par `az network dns zone show`. utiliser des enregistrements DNS de toolist, `az network dns record-set list`.


## <a name="list-dns-zones"></a>Création de la liste des zones DNS

utiliser des zones DNS tooenumerate `az network dns zone list`. Pour obtenir de l’aide, consultez l’article `az network dns zone list --help`.

Groupe de ressources en spécifiant hello répertorie uniquement les zones dans le groupe de ressources hello :

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

L’omission de groupe de ressources hello répertorie toutes les zones d’abonnement de hello :

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a>Mise à jour d’une zone DNS

Tooa modifications ressource de zone DNS peut être établie en utilisant `az network dns zone update`. Pour obtenir de l’aide, consultez l’article `az network dns zone update --help`.

Cette commande ne met pas à jour des jeux d’enregistrements DNS hello dans la zone de hello (consultez [comment les enregistrements DNS tooManage](dns-operations-recordsets-cli.md)). Il est tooupdate utilisé uniquement les propriétés de ressource de zone hello lui-même. Ces propriétés sont actuellement limitée toohello [Azure Resource Manager « balises »](dns-zones-records.md#tags) pour les ressources de la zone hello.

Hello suivant montre comment les balises tooupdate hello sur une zone DNS. les balises existantes Hello sont remplacés par la valeur hello spécifiée.

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a>Suppression d’une zone DNS

Les zones DNS peuvent être supprimées en utilisant `az network dns zone delete`. Pour obtenir de l’aide, consultez l’article `az network dns zone delete --help`.

> [!NOTE]
> Suppression d’une zone DNS supprime également tous les enregistrements DNS dans la zone de hello. Il est impossible d’annuler cette opération. Si la zone DNS de hello est en cours d’utilisation, les services à l’aide de la zone de hello échoue lors de la zone de hello est supprimée.
>
>tooprotect contre la suppression accidentelle de zone, consultez [comment tooprotect DNS zones et enregistrements](dns-protect-zones-recordsets.md).

Cette commande vous demande de confirmer l’opération. Hello facultatif `--yes` commutateur supprime cette invite.

Hello suivant montre comment toodelete hello zone *contoso.com* du groupe de ressources *MyResourceGroup*.

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment trop[gérer les jeux d’enregistrements et les enregistrements](dns-getstarted-create-recordset-cli.md) dans votre zone DNS.

Découvrez comment trop[déléguer votre tooAzure de domaine DNS](dns-domain-delegation.md).

