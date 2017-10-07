---
title: zones DNS de Azure - Azure CLI 1.0 aaaManage DNS | Documents Microsoft
description: "Vous pouvez gérer des zones DNS à l’aide d’Azure CLI 1.0. Cet article explique comment tooupdate, supprimer et créer des zones DNS sur le système DNS Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: cb9790cc46626ef7f38a43edb57511104fe6057e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-10"></a>Comment toomanage les Zones DNS à l’aide d’Azure DNS hello Azure CLI 1.0

> [!div class="op_single_selector"]
> * [Portail](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)

Ce guide montre comment toomanage votre DNS zones à l’aide de hello inter-plateformes CLI Azure 1.0, qui est disponible pour Windows, Mac et Linux. Vous pouvez également gérer vos zones DNS à l’aide de [Azure PowerShell](dns-operations-dnszones.md) ou de bienvenue du portail Azure.

## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete

Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

* [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -notre CLI pour les modèles de déploiement gestion classique et les ressources des hello.
* [Azure CLI 2.0](dns-operations-dnszones-cli.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello.

## <a name="introduction"></a>Introduction

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a>Obtenir de l’aide

Toutes les commandes CLI 1.0 relatives tooAzure DNS commence par `azure network dns`. Aide est disponible pour chaque commande à l’aide de hello `--help` option (forme abrégée : `-h`).  Par exemple :

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a>Création d’une zone DNS

Une zone DNS est créée à l’aide de hello `azure network dns zone create` commande. Pour obtenir de l’aide, consultez l’article `azure network dns zone create -h`.

Hello exemple suivant crée une zone DNS appelée *contoso.com* dans le groupe de ressources hello appelé *MyResourceGroup*:

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a>toocreate une zone DNS avec balises

Hello suivant montre comment la zone avec deux toocreate DNS [Azure Resource Manager balises](dns-zones-records.md#tags), *projet = demo* et *env = test*, à l’aide de hello `--tags` paramètre (forme abrégée : `-t`) :

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a>Obtention d’une zone DNS

tooretrieve une zone DNS, utilisez `azure network dns zone show`. Pour obtenir de l’aide, consultez l’article `azure network dns zone show -h`.

exemple Hello retourne zone DNS de hello *contoso.com* et ses données associées du groupe de ressources *MyResourceGroup*. 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

Hello, l’exemple suivant est la réponse de hello.

```
info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
data:    Id                              : /subscriptions/.../contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 2
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            : project=demo;env=test
info:    network dns zone show command OK
```

Notez que les enregistrements DNS ne sont pas retournés par `azure network dns zone show`. utiliser des enregistrements DNS de toolist, `azure network dns record-set list`.


## <a name="list-dns-zones"></a>Création de la liste des zones DNS

utiliser des zones DNS tooenumerate `azure network dns zone list`. Pour obtenir de l’aide, consultez l’article `azure network dns zone list -h`.

Groupe de ressources en spécifiant hello répertorie uniquement les zones dans le groupe de ressources hello :

```azurecli
azure network dns zone list MyResourceGroup
```

L’omission de groupe de ressources hello répertorie toutes les zones d’abonnement de hello :

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a>Mise à jour d’une zone DNS

Tooa modifications ressource de zone DNS peut être établie en utilisant `azure network dns zone set`. Pour obtenir de l’aide, consultez l’article `azure network dns zone set -h`.

Cette commande ne met pas à jour des jeux d’enregistrements DNS hello dans la zone de hello (consultez [comment les enregistrements DNS tooManage](dns-operations-recordsets-cli-nodejs.md)). Il est tooupdate utilisé uniquement les propriétés de ressource de zone hello lui-même. Ces propriétés sont actuellement limitée toohello [Azure Resource Manager « balises »](dns-zones-records.md#tags) pour les ressources de la zone hello.

Hello suivant montre comment les balises tooupdate hello sur une zone DNS. les balises existantes Hello sont remplacés par la valeur hello spécifiée.

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a>Suppression d’une zone DNS

Les zones DNS peuvent être supprimées en utilisant `azure network dns zone delete`. Pour obtenir de l’aide, consultez l’article `azure network dns zone delete -h`.

> [!NOTE]
> Suppression d’une zone DNS supprime également tous les enregistrements DNS dans la zone de hello. Il est impossible d’annuler cette opération. Si la zone DNS de hello est en cours d’utilisation, les services à l’aide de la zone de hello échoue lors de la zone de hello est supprimée.
>
>tooprotect contre la suppression accidentelle de zone, consultez [comment tooprotect DNS zones et enregistrements](dns-protect-zones-recordsets.md).

Cette commande vous demande de confirmer l’opération. Hello facultatif `--quiet` basculer (forme abrégée : `-q`) supprime cette invite.

Hello suivant montre comment toodelete hello zone *contoso.com* du groupe de ressources *MyResourceGroup*.

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment trop[gérer les jeux d’enregistrements et les enregistrements](dns-getstarted-create-recordset-cli-nodejs.md) dans votre zone DNS.

Découvrez comment trop[déléguer votre tooAzure de domaine DNS](dns-domain-delegation.md).

