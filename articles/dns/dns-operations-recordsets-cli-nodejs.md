---
title: "aaaManage les enregistrements DNS à l’aide d’Azure DNS hello Azure CLI 1.0 | Documents Microsoft"
description: "Gestion des jeux d'enregistrements DNS et des enregistrements dans Azure DNS lorsque votre domaine est hébergé dans Azure DNS. Toutes les commandes CLI 1.0 destinées aux opérations sur les jeux d’enregistrements et les enregistrements."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/20/2016
ms.author: jonatul
ms.openlocfilehash: 1f01450b0839f712cb1d96be318766bac581fea1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-in-azure-dns-using-hello-azure-cli-10"></a>Gérer les enregistrements DNS dans le système DNS d’Azure à l’aide de hello Azure CLI 1.0

> [!div class="op_single_selector"]
> * [portail Azure](dns-operations-recordsets-portal.md)
> * [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

Cet article vous explique comment toomanage les enregistrements DNS pour votre zone DNS à l’aide de hello multiplateforme Azure interface de ligne de commande (CLI), qui est disponible pour Windows, Mac et Linux. Vous pouvez également gérer vos enregistrements DNS à l’aide de [Azure PowerShell](dns-operations-recordsets.md) ou hello [portail Azure](dns-operations-recordsets-portal.md).

## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete

Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

* [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) -notre CLI pour les modèles de déploiement gestion classique et les ressources des hello.
* [Azure CLI 2.0](dns-operations-recordsets-cli.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello.

exemples Hello dans cet article supposent que vous avez déjà [installé hello Azure CLI 1.0, signé et créé une zone DNS](dns-operations-dnszones-cli-nodejs.md).

## <a name="introduction"></a>Introduction

Avant de créer des enregistrements DNS dans le système DNS d’Azure, vous devez d’abord toounderstand comment Azure DNS organise les enregistrements DNS dans les jeux d’enregistrements DNS.

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

Pour plus d’informations sur les enregistrements DNS dans Azure DNS, voir [Enregistrements et zones DNS](dns-zones-records.md).

## <a name="create-a-dns-record"></a>Créer un enregistrement DNS

toocreate un enregistrement DNS, utilisez hello `azure network dns record-set add-record` commande. Pour obtenir de l’aide, consultez l’article `azure network dns record-set add-record -h`.

Lorsque vous créez un enregistrement, vous devez le nom du groupe ressource toospecify hello, nom de la zone, jeu d’enregistrements nom, type d’enregistrement hello et détails hello d’enregistrement hello en cours de création. Hello nom de jeu d’enregistrements donné doit être un *relatif* nom, qui signifie qu’il doit exclure le nom de la zone hello.

Si le jeu d’enregistrements hello n’existe pas déjà, cette commande crée pour vous. Si le jeu d’enregistrements hello existe déjà, nommez-la de cette commande hello enregistrement que vous spécifiez le jeu d’enregistrements existant toohello.

Si un jeu d’enregistrements est créé, une durée de vie (TTL) de 3600 est utilisée par défaut. Pour obtenir des instructions sur toouse TTLs différents, voir [créer un jeu d’enregistrements DNS](#create-a-dns-record-set).

Hello exemple suivant crée un enregistrement A appelé *www* dans la zone de hello *contoso.com* dans le groupe de ressources hello *MyResourceGroup*. Hello d’adresse IP de hello un enregistrement est *1.2.3.4*.

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

toocreate un enregistrement dans apex hello de zone de hello (dans ce cas, « contoso.com »), utilisez le nom de l’enregistrement hello « @ », y compris les guillemets hello :

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" A -a 1.2.3.4
```

## <a name="create-a-dns-record-set"></a>Créer un jeu d’enregistrements DNS

Bonjour exemples ci-dessus, un enregistrement DNS hello a été soit ajouté tooan existante du jeu d’enregistrements ou de création de jeu d’enregistrements hello *implicitement*. Vous pouvez également créer le jeu d’enregistrements hello *explicitement* avant l’ajout d’enregistrements tooit. DNS Azure prend en charge les jeux d’enregistrements 'empty', qui peut agir comme un espace réservé tooreserve un nom DNS avant de créer des enregistrements DNS. Jeux d’enregistrements vides est visibles dans hello Azure DNS plan de contrôle, mais n’apparaissent pas sur les serveurs DNS de Azure hello.

Jeux d’enregistrements est créés à l’aide de hello `azure network dns record-set create` commande. Pour obtenir de l’aide, consultez l’article `azure network dns record-set create -h`.

Création d’enregistrement hello définie explicitement vous permet de propriétés du jeu d’enregistrements toospecify tels que hello [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) et les métadonnées. [Métadonnées du jeu d’enregistrements](dns-zones-records.md#tags-and-metadata) peuvent être des données spécifiques à l’application tooassociate utilisées avec chaque jeu d’enregistrements, en tant que paires clé-valeur.

Hello exemple suivant crée un enregistrement vide est définie avec une durée de vie de 60 secondes, à l’aide de hello `--ttl` paramètre (forme abrégée : `-l`) :

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --ttl 60
```

Hello exemple suivant crée un jeu enregistrements avec deux entrées de métadonnées, « dept = finance » et « environnement = production », à l’aide de hello `--metadata` paramètre (forme abrégée : `-m`) :

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

Après avoir créé un jeu d’enregistrements vide, les enregistrements peuvent être ajoutés à l’aide de `azure network dns record-set add-record`, comme décrit dans [Création d’un enregistrement DNS](#create-a-dns-record).

## <a name="create-records-of-other-types"></a>Créer des enregistrements d’autres types

Après avoir vu en détail comment toocreate 'A' enregistre, hello suivant exemples montrent comment enregistrement toocreate d’autres types d’enregistrements pris en charge par le système DNS Azure.

les paramètres de Hello utilisés enregistrement de hello toospecify données varient en fonction de type hello d’enregistrement de hello. Par exemple, pour un enregistrement de type « A », vous spécifiez l’adresse de hello IPv4 avec le paramètre hello `-a <IPv4 address>`. Hello des paramètres pour chaque type d’enregistrement peut être à l’aide de `azure network dns record-set add-record -h`.

Dans chaque cas, nous montrons comment toocreate un enregistrement unique. enregistrement de Hello est ajouté toohello existante du jeu d’enregistrements, ou un jeu d’enregistrements créé implicitement. Pour plus d’informations sur la création de jeux d’enregistrements et la définition explicite des paramètres de jeu d’enregistrements, consultez [Création d’un jeu d’enregistrements DNS](#create-a-dns-record-set).

Nous ne donnent pas une toocreate exemple un jeu d’enregistrements SOA, étant donné que SOA est créées et supprimées avec chaque zone DNS et ne peut pas être créée ou supprimée séparément. Toutefois, [hello SOA peut être modifiée, comme indiqué dans un exemple plus loin](#to-modify-an-SOA-record).

### <a name="create-an-aaaa-record"></a>Créer un enregistrement AAAA

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-aaaa AAAA --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a>Créer un enregistrement CNAME

> [!NOTE]
> les normes DNS Hello n’autorisent pas les enregistrements CNAME au sommet de hello d’une zone (`-Name "@"`), ni font qu’ils autorisent les jeux d’enregistrements contenant plusieurs enregistrements.
> 
> Pour plus d’informations, voir [Enregistrements CNAME](dns-zones-records.md#cname-records).

```azurecli
azure network dns record-set add-record  MyResourceGroup contoso.com  test-cname CNAME --cname www.contoso.com
```

### <a name="create-an-mx-record"></a>Créer un enregistrement MX

Dans cet exemple, nous utilisons le nom du jeu d’enregistrements hello « @ » toocreate hello enregistrement MX au sommet de zone hello (dans ce cas, « contoso.com »).

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "@" MX --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a>Créer un enregistrement NS

```azurecli
azure network dns record-set add-record MyResourceGroup  contoso.com  test-ns NS --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a>Création d’un enregistrement PTR

Dans ce cas, « my-arpa-zone.com' représente hello zone ARPA représentant votre plage IP. Chaque enregistrement PTR dans cette zone correspond à adresse IP de tooan au sein de cette plage d’adresses IP.  nom de l’enregistrement Hello « 10 » est le dernier octet de hello d’adresse IP de hello dans cette plage IP représentée par cet enregistrement.

```azurecli
azure network dns record-set add-record MyResourceGroup my-arpa-zone.com "10" PTR --ptrdname "myservice.contoso.com"
```

### <a name="create-an-srv-record"></a>Création d’un enregistrement SRV

Lorsque vous créez un [jeu d’enregistrements SRV](dns-zones-records.md#srv-records), spécifiez hello  *\_service* et  *\_protocole* Bonjour nom du jeu d’enregistrements. Il n’existe aucun besoin tooinclude « @ » Bonjour jeu d’enregistrements nom lors de la création d’un enregistrement SRV définie au sommet de zone hello.

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "_sip._tls" SRV --priority 10 --weight 5 --port 8080 --target "sip.contoso.com"
```

### <a name="create-a-txt-record"></a>Création d’un enregistrement TXT

Hello suivant montre comment enregistrer des toocreate un TXT. Pour plus d’informations sur la longueur maximale de la chaîne hello pris en charge dans les enregistrements TXT, consultez [enregistrements TXT](dns-zones-records.md#txt-records).

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-txt TXT --text "This is a TXT record"
```

## <a name="get-a-record-set"></a>Obtention d’un jeu d'enregistrements

tooretrieve un jeu d’enregistrements existant, utilisez `azure network dns record-set show`. Pour obtenir de l’aide, consultez l’article `azure network dns record-set show -h`.

Lorsque vous créez un enregistrement ou un jeu d’enregistrements, enregistrement de hello SET nom donné doit être un *relatif* nom, qui signifie qu’il doit exclure le nom de la zone hello. Vous devez également le type d’enregistrement toospecify hello, zone hello contenant hello enregistrement défini et hello contenant hello zone de groupe de ressources.

Hello exemple suivant récupère les enregistrement hello *www* d’un type de zone *contoso.com* dans le groupe de ressources *MyResourceGroup*:

```azurecli
azure network dns record-set show MyResourceGroup contoso.com www A
```

## <a name="list-record-sets"></a>Liste des jeux d'enregistrements

Vous pouvez répertorier tous les enregistrements dans une zone DNS à l’aide de hello `azure network dns record-set list` commande. Pour obtenir de l’aide, consultez l’article `azure network dns record-set list -h`.

Cet exemple retourne tous les enregistrements définit dans la zone de hello *contoso.com*, dans le groupe de ressources *MyResourceGroup*, quel que soit le nom ou le type d’enregistrement :

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```

Cet exemple retourne tous les jeux d’enregistrements qui correspondent aux hello donné du type d’enregistrement (dans ce cas, les enregistrements de 'A') :

```azurecli
azure network dns record-set list MyResourceGroup contoso.com --type A
```

## <a name="add-a-record-tooan-existing-record-set"></a>Ajouter un enregistrement tooan existante du jeu d’enregistrements

Vous pouvez utiliser `azure network dns record-set add-record` les deux toocreate un enregistrement dans un nouvel enregistrement défini ou tooadd un enregistrement existant tooan enregistrement.

Pour plus d’informations, consultez [Création d’un enregistrement DNS](#create-a-dns-record) et [Création d’enregistrements d’autres types](#create-records-of-other-types) ci-dessus.

## <a name="remove-a-record-from-an-existing-record-set"></a>Suppression d’un enregistrement d’un jeu d'enregistrements existant.

tooremove DNS enregistrer à partir d’un jeu d’enregistrements existant, utilisez `azure network dns record-set delete-record`. Pour obtenir de l’aide, consultez l’article `azure network dns record-set delete-record -h`.

Cette commande supprime un enregistrement DNS d’un jeu d’enregistrements. Si le dernier enregistrement dans un jeu d’enregistrements de hello est supprimé, hello jeu d’enregistrements lui-même est **pas** supprimé. Un jeu d’enregistrements vide est laissé à la place. enregistrement de hello toodelete défini à la place, consultez [supprimer un jeu d’enregistrements](#delete-a-record-set).

Vous devez toospecify hello enregistrement toobe est supprimé et zone hello qui doit être supprimée à partir, à l’aide de hello les mêmes paramètres que lors de la création d’un enregistrement à l’aide `azure network dns record-set add-record`. Ces paramètres sont décrits dans [Création d’un enregistrement DNS](#create-a-dns-record) et [Création d’enregistrements d’autres types](#create-records-of-other-types) ci-dessus.

Cette commande vous demande de confirmer l’opération. Ce message peut être supprimé à l’aide de hello `--quiet` basculer (forme abrégée : `-q`).

Hello suivant supprime de l’exemple hello un enregistrement avec la valeur « 1.2.3.4 » à partir de l’enregistrement de hello définir nommée *www* dans la zone de hello *contoso.com*, dans le groupe de ressources hello *MyResourceGroup*. invite de confirmation Hello est supprimée.

```azurecli
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4 --quiet
```

## <a name="modify-an-existing-record-set"></a>Modifier un jeu d’enregistrements

Chaque jeu d’enregistrements contient une [durée de vie (TTL)](dns-zones-records.md#time-to-live), des [métadonnées](dns-zones-records.md#tags-and-metadata) et des enregistrements DNS. Hello sections suivantes expliquent comment toomodify de ces propriétés.

### <a name="toomodify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a>toomodify un enregistrement A, AAAA, MX, NS, PTR, SRV ou TXT

toomodify un enregistrement existant de type A, AAAA, MX, NS, PTR, SRV ou TXT, vous devez tout d’abord ajouter un nouvel enregistrement, puis hello un enregistrement existant. Pour obtenir des instructions détaillées sur la façon de toodelete et ajouter des enregistrements, consultez hello les premières sections de cet article.

Hello, l’exemple suivant montre comment la corriger toomodify un enregistrement de « A », à partir de l’IP adresse 1.2.3.4 tooIP 5.6.7.8 :

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 5.6.7.8
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

### <a name="toomodify-a-cname-record"></a>toomodify un enregistrement CNAME

toomodify un enregistrement CNAME, utilisez `azure network dns record-set add-record` tooadd hello nouvelle valeur d’enregistrement. Contrairement aux autres types d’enregistrements, un jeu d’enregistrements CNAME ne peut contenir qu’un seul enregistrement. Par conséquent, les enregistrements existants hello sont *remplacé* lorsque hello nouvel enregistrement est ajouté et n’a pas besoin toobe supprimée séparément.  Vous est demandée tooaccept ce remplacement.

exemple Hello modifie jeu d’enregistrements CNAME hello *www* dans la zone de hello *contoso.com*, dans le groupe de ressources *MyResourceGroup*, toopoint trop 'www.fabrikam.net' à la place de son valeur existante :

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www CNAME --cname www.fabrikam.net
``` 

### <a name="toomodify-an-soa-record"></a>toomodify un enregistrement SOA

Utilisez `azure network dns record-set set-soa-record` toomodify hello SOA pour une zone DNS. Pour obtenir de l’aide, consultez l’article `azure network dns record-set set-soa-record -h`.

Hello suivant montre comment enregistrer des propriété tooset hello « email » de hello SOA de zone de hello *contoso.com* dans le groupe de ressources hello *MyResourceGroup*:

```azurecli
azure network dns record-set set-soa-record rg1 contoso.com --email admin.contoso.com
```


### <a name="toomodify-ns-records-at-hello-zone-apex"></a>enregistrements toomodify NS au sommet de zone hello

jeu au sommet de zone hello d’enregistrements NS Hello sont automatiquement créé avec chaque zone DNS. Il contient les noms de hello de zone de hello Azure DNS nom serveurs toohello attribué.

Vous pouvez ajouter des noms supplémentaires serveurs toothis NS jeu d’enregistrements, toosupport domaines l’hébergement avec le fournisseur DNS. Vous pouvez également modifier la durée de vie de hello et les métadonnées pour ce jeu d’enregistrements. Toutefois, vous ne peut pas supprimer ou modifier les serveurs de noms DNS Azure hello préremplies.

Notez que cela s’applique uniquement toohello NS jeu d’enregistrements au sommet de zone hello. Autres jeux d’enregistrements NS dans votre zone (comme les zones enfant toodelegate utilisé) peut être modifié sans contrainte.

Bonjour à l’exemple suivant montre comment tooadd un enregistrement de noms supplémentaires server toohello NS définie les au sommet de zone hello :

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="toomodify-hello-ttl-of-an-existing-record-set"></a>définie des toomodify hello durée de vie d’un enregistrement existant

définie des toomodify hello durée de vie d’un enregistrement existant, utilisez `azure network dns record-set set`. Pour obtenir de l’aide, consultez l’article `azure network dns record-set set -h`.

Bonjour à l’exemple suivant montre comment toomodify un jeu d’enregistrements durée de vie, dans ce cas too60 secondes :

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --ttl 60
```

### <a name="toomodify-hello-metadata-of-an-existing-record-set"></a>définir des métadonnées de hello toomodify d’un enregistrement existant

[Métadonnées du jeu d’enregistrements](dns-zones-records.md#tags-and-metadata) peuvent être des données spécifiques à l’application tooassociate utilisées avec chaque jeu d’enregistrements, en tant que paires clé-valeur. définir des métadonnées de hello toomodify d’un enregistrement existant, utilisez `azure network dns record-set set`. Pour obtenir de l’aide, consultez l’article `azure network dns record-set set -h`.

Hello suivant montre comment toomodify un jeu d’enregistrements avec deux entrées de métadonnées, « dept = finance » et « environnement = production », à l’aide de hello `--metadata` paramètre (forme abrégée : `-m`). Notez que toutes les métadonnées existantes sont *remplacé* par les valeurs hello donnés.

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

## <a name="delete-a-record-set"></a>Supprimer un jeu d’enregistrements

Jeux d’enregistrements peut être supprimés à l’aide de hello `azure network dns record-set delete` commande. Pour obtenir de l’aide, consultez l’article `azure network dns record-set delete -h`. Suppression d’un jeu d’enregistrements supprime également tous les enregistrements dans le jeu d’enregistrements hello.

> [!NOTE]
> Vous ne pouvez pas supprimer hello SOA et NS jeux d’enregistrements au sommet de zone hello (`-Name "@"`).  Ceux-ci sont créés automatiquement lorsque hello zone a été créé et sont automatiquement supprimés lorsque la zone de hello est supprimée.

exemple Hello supprime hello jeu d’enregistrements nommé *www* d’un type de zone de hello *contoso.com* dans le groupe de ressources *MyResourceGroup*:

```azurecli
azure network dns record-set delete MyResourceGroup contoso.com www A
```

Vous êtes opération de suppression demandées tooconfirm hello. toosuppress ce invite de commandes, utilisez hello `--quiet` basculer (forme abrégée : `-q`).

## <a name="next-steps"></a>Étapes suivantes

Apprenez-en davantage sur les [zones et enregistrements dans Azure DNS](dns-zones-records.md).
<br>
Découvrez comment trop[protéger les zones et les enregistrements](dns-protect-zones-recordsets.md) lors de l’utilisation d’Azure DNS.
