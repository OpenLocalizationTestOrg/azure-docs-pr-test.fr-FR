---
title: "aaaManage le Cache Redis Azure à l’aide d’Azure CLI | Documents Microsoft"
description: "Découvrez comment tooinstall hello CLI d’Azure sur n’importe quelle plateforme, comment toouse il tooconnect tooyour compte Azure et comment toocreate et gérer un cache Redis à partir de hello CLI d’Azure."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 964ff245-859d-4bc1-bccf-62e4b3c1169f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: e8ee30090133e6b4edea93dcd13fd171e75989bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-azure-redis-cache-using-hello-azure-command-line-interface-azure-cli"></a>Comment toocreate et gérer le Cache Redis Azure à l’aide de hello Azure Interface de ligne (Azure)
> [!div class="op_single_selector"]
> * [PowerShell](cache-howto-manage-redis-cache-powershell.md)
> * [Interface de ligne de commande Azure](cache-manage-cli.md)
>
>

Hello CLI d’Azure est un excellent moyen toomanage votre infrastructure Azure à partir de n’importe quelle plateforme. Cet article vous montre comment toocreate et gérer vos instances de Cache Redis Azure à l’aide de hello CLI d’Azure.

> [!NOTE]
> Cet article s’applique tooa la version précédente de CLI d’Azure. Pour les scripts d’exemple hello dernière Azure CLI 2.0, consultez [exemples de cache Azure Redis de CLI](cli-samples.md).
> 
> 

## <a name="prerequisites"></a>Composants requis
toocreate et gérer des instances de Cache Redis Azure à l’aide de CLI d’Azure, vous devez effectuer des hello comme suit.

* Vous devez disposer d’un compte Azure. Si vous n’en avez pas, vous pouvez créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/) en quelques minutes.
* [Installer hello CLI d’Azure](../cli-install-nodejs.md).
* Se connecter à votre installation du CLI d’Azure avec un compte Azure personnel ou avec un travail ou scolaire compte Azure et connectez-vous à partir de hello CLI Azure à l’aide de hello `azure login` commande. toounderstand hello différences et choisir, consultez [connecter tooan abonnement Azure à partir de hello Azure Interface de ligne (Azure)](../xplat-cli-connect.md).
* Avant d’exécuter un des hello suivant de commandes, basculez hello CLI d’Azure en mode de gestionnaire de ressources en exécutant hello `azure config mode arm` commande. Pour plus d’informations, consultez [utiliser hello CLI d’Azure toomanage Azure ressources et groupes de ressources](../xplat-cli-azure-resource-manager.md).

## <a name="redis-cache-properties"></a>Propriétés du cache Redis
les propriétés suivantes Hello sont utilisées lors de la création et la mise à jour des instances de Cache Redis.

| Propriété | Switch | Description |
| --- | --- | --- |
| name |-n, --name |Nom de hello du Cache Redis. |
| resource group |-g, --resource-group |Nom du groupe de ressources de hello. |
| location |-l, --location |Cache d’emplacements de toocreate. |
| size |-z, --size |Taille de hello du Cache Redis. Valeurs valides : [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4] |
| sku |-x, --sku |SKU Redis. Doit être une des valeurs : [De Base, Standard, Premium] |
| enableNonSslPort |-e, --enable-non-ssl-port |Propriété EnableNonSslPort Hello du Cache Redis. Ajoutez cet indicateur si vous souhaitez que le Port tooenable hello Non SSL pour votre cache |
| Configuration de Redis |-c, --redis-configuration |Configuration de Redis. Entrez ici une chaîne au format JSON des clés et des valeurs de configuration. Format :"{"":"","":""}" |
| Configuration de Redis |-f, --redis-configuration-file |Configuration de Redis. Entrez le chemin d’accès de hello d’un fichier contenant les clés de configuration et les valeurs ici. Format d’entrée du fichier hello : { » » : « », « » : « »} |
| Nombre de partitions |-r, --shard-count |Nombre de toocreate de partitions sur un Cache de Cluster Premium avec le clustering. |
| Réseau virtuel |-v, --virtual-network |Lors de l’hébergement de votre cache dans un réseau virtuel spécifie hello exacte ID de ressource ARM Hello de toodeploy de réseau virtuel hello redis cache dans. Exemple de format : /subscriptions/{ID_abonnement}/resourceGroups/{nom_groupe_ressources}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1 |
| key type |-t, --key-type |Type de clé toorenew. Valeurs valides : [Primary, Secondary] |
| StaticIP |-p, --static-ip <static-ip> |Lorsque vous hébergez votre cache dans un réseau virtuel, spécifie une adresse IP unique dans un sous-réseau hello pour le cache de hello. Si n’est fourni, une est choisie pour vous à partir du sous-réseau de hello. |
| Sous-réseau |t, --subnet <subnet> |Lorsque vous hébergez votre cache dans un réseau virtuel, spécifie le nom hello du sous-réseau de hello dans le cache de hello toodeploy. |
| VirtualNetwork |-v, --virtual-network <virtual-network> |Lors de l’hébergement de votre cache dans un réseau virtuel spécifie hello exacte ID de ressource ARM Hello de toodeploy de réseau virtuel hello redis cache dans. Exemple de format : /subscriptions/{ID_abonnement}/resourceGroups/{nom_groupe_ressources}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1 |
| Abonnement |-s, --subscription |identificateur d’abonnement Hello. |

## <a name="see-all-redis-cache-commands"></a>Voir toutes les commandes de cache Redis
toosee toutes les commandes de Cache Redis et leurs paramètres, utilisez hello `azure rediscache -h` commande.

    C:\>azure rediscache -h
    help:    Commands toomanage your Azure Redis Cache(s)
    help:
    help:    Create a Redis Cache
    help:      rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Delete an existing Redis Cache
    help:      rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    List all Redis Caches within your Subscription or Resource Group
    help:      rediscache list [options]
    help:
    help:    Show properties of an existing Redis Cache
    help:      rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Change settings of an existing Redis Cache
    help:      rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Renew hello authentication key for an existing Redis Cache
    help:      rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:      rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help  output usage information
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="create-a-redis-cache"></a>Création d’un cache Redis
toocreate un Cache Redis, utilisez hello de commande suivante :

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

Pour plus d’informations sur cette commande, exécutez hello `azure rediscache create -h` commande.

    C:\>azure rediscache create -h
    help:    Create a Redis Cache
    help:
    help:    Usage: rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -l, --location <location>                                Location toocreate cache.
    help:      -z, --size <size>                                        Size of hello Redis Cache. Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]
    help:      -x, --sku <sku>                                          Redis SKU. Should be one of : [Basic, Standard, Premium]
    help:      -e, --enable-non-ssl-port                                EnableNonSslPort property of hello Redis Cache. Add this flag if you want tooenable hello Non SSL Port for your cache
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here. Format:"{"<key1>":"<value1>","<key2>":"<value2>"}"
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here. Format for hello file entry: {"<key1>":"<value1>","<key2>":"<value2>"}
    help:      -r, --shard-count <shard-count>                          Number of Shards toocreate on a Premium Cluster Cache
    help:      -v, --virtual-network <virtual-network>                  hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1
    help:      -t, --subnet <subnet>                                    Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -p, --static-ip <static-ip>                              Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -s, --subscription <id>                                  hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="delete-an-existing-redis-cache"></a>Suppression d’un cache Redis
toodelete un Cache Redis, utilisez hello de commande suivante :

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

Pour plus d’informations sur cette commande, exécutez hello `azure rediscache delete -h` commande.

    C:\>azure rediscache delete -h
    help:    Delete an existing Redis Cache
    help:
    help:    Usage: rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which hello cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a>Liste de tous les caches Redis dans votre abonnement ou groupe de ressources
utilisation de tous les Caches Redis au sein de votre abonnement ou le groupe de ressources, toolist hello la commande suivante :

    azure rediscache list [options]

Pour plus d’informations sur cette commande, exécutez hello `azure rediscache list -h` commande.

    C:\>azure rediscache list -h
    help:    List all Redis Caches within your Subscription or Resource Group
    help:
    help:    Usage: rediscache list [options]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="show-properties-of-an-existing-redis-cache"></a>Affichage des propriétés d’un cache Redis existant
tooshow des propriétés d’un Cache Redis existant, utilisez hello de commande suivante :

    azure rediscache show [--name <name> --resource-group <resource-group>]

Pour plus d’informations sur cette commande, exécutez hello `azure rediscache show -h` commande.

    C:\>azure rediscache show -h
    help:    Show properties of an existing Redis Cache
    help:
    help:    Usage: rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

<a name="scale"></a>

## <a name="change-settings-of-an-existing-redis-cache"></a>Modification des paramètres d’un cache Redis
paramètres toochange d’un Cache Redis existant, utilisez hello de commande suivante :

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

Pour plus d’informations sur cette commande, exécutez hello `azure rediscache set -h` commande.

    C:\>azure rediscache set -h
    help:    Change settings of an existing Redis Cache
    help:
    help:    Usage: rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here.
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here.
    help:      -s, --subscription <subscription>                        hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="renew-hello-authentication-key-for-an-existing-redis-cache"></a>Renouveler la clé d’authentification hello pour un Cache Redis existant
clé d’authentification toorenew hello pour un Redis Cache existant, hello utilisez commande suivante :

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

Spécifiez `Primary` ou `Secondary` pour `key-type`.

Pour plus d’informations sur cette commande, exécutez hello `azure rediscache renew-key -h` commande.

    C:\>azure rediscache renew-key -h
    help:    Renew hello authentication key for an existing Redis Cache
    help:
    help:    Usage: rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which cache exists
    help:      -t, --key-type <key-type>              type of key toorenew. Valid values are: 'Primary', 'Secondary'.
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a>Liste des clés primaire et secondaire d’un cache Redis
clés primaires et secondaires de toolist d’un Cache Redis existant, utilisez hello de commande suivante :

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

Pour plus d’informations sur cette commande, exécutez hello `azure rediscache list-keys -h` commande.

    C:\>azure rediscache list-keys -h
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:
    help:    Usage: rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which Cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)
