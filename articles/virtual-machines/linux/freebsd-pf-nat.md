---
title: toocreate de filtre de paquets de FreeBSD aaaUse un pare-feu dans Azure | Documents Microsoft
description: "Découvrez comment toodeploy un NAT de pare-feu à l’aide de FreeBSD PF dans Azure."
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/20/2017
ms.author: kyliel
ms.openlocfilehash: 3d3a5dde2ca03ba6fc384581c786f5eb746e6d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-freebsds-packet-filter-toocreate-a-secure-firewall-in-azure"></a>Comment toocreate de filtre de paquets de FreeBSD toouse pare-feu sécurisé dans Azure
Cet article présente comment toodeploy un pare-feu NAT à l’aide du filtre de programme de compression de FreeBSD via le modèle Azure Resource Manager pour le scénario de serveur web courant.

## <a name="what-is-pf"></a>Qu’est-ce que PF ?
PF (filtre de paquets, également écrit pf) est un filtre de paquets avec état sous licence BSD, un élément central des logiciels de pare-feu. PF a évolué rapidement et offre désormais plusieurs avantages par rapport aux autres pare-feu disponibles. Traduction d’adresses réseau (NAT) est PF depuis le premier jour, puis le Planificateur de paquets et la gestion de la file d’attente active ont été intégrées à PF, en intégrant des hello ALTQ et ce qui peut être configuré via une configuration de dossiers publics. Les fonctionnalités telles que pfsync et du protocole CARP pour le basculement et la redondance, authpf d’authentification de la session et de proxy ftp tooease il hello difficile protocole FTP, ont également étendu PF. En bref, PF est un pare-feu puissant et riche en fonctionnalités. 

## <a name="get-started"></a>Prise en main
Si vous souhaitez configurer un pare-feu sécurisé dans le cloud hello pour vos serveurs web, puis nous pouvons commencer. Vous pouvez également appliquer des scripts de hello utilisés dans cette tooset de modèle Azure Resource Manager votre topologie de réseau.
modèle de gestionnaire de ressources Azure Hello configurer un ordinateur virtuel de FreeBSD qui effectue /redirection NAT à l’aide de dossiers publics deux machines virtuelles et FreeBSD avec serveur de web Nginx hello installé et configuré. En outre tooperforming NAT pour deux serveurs web de hello sortie le trafic, ordinateur virtuel de la redirection des NAT/hello intercepte les requêtes HTTP et les redirige toohello deux serveurs web dans tourniquet. Hello réseau virtuel utilise hello privée non routable IP adresse espace 10.0.0.2/24 et vous pouvez modifier les paramètres du modèle de hello hello. modèle de gestionnaire de ressources Azure Hello définit également une table de routage pour hello réseau virtuel entier, ce qui est une collection d’itinéraires individuelles utilisées toooverride des itinéraires par défaut Azure basés sur l’adresse IP de destination hello. 

![pf_topology](./media/freebsd-pf-nat/pf_topology.jpg)
    
### <a name="deploy-through-azure-cli"></a>Déploiement avec l’interface de ligne de commande Azure
Vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login). Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create). Hello exemple suivant crée un nom de groupe de ressources `myResourceGroup` Bonjour `West US` emplacement.

```azurecli
az group create --name myResourceGroup --location westus
```

Ensuite, déployez le modèle de hello [pf-freebsd-setup](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup) avec [créer de déploiement de groupe az](/cli/azure/group/deployment#create). Télécharger [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/pf-freebsd-setup/azuredeploy.parameters.json) sous hello même chemin d’accès et définir vos propres valeurs de ressource, telles que `adminPassword`, `networkPrefix`, et `domainNamePrefix`. 

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeploymentName \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/pf-freebsd-setup/azuredeploy.json \
    --parameters '@azuredeploy.parameters.json' --verbose
```

Après environ cinq minutes, vous obtenez des informations hello de `"provisioningState": "Succeeded"`. Ensuite, vous pouvez ssh toohello frontal VM (NAT) ou d’accéder au serveur de web Nginx dans un navigateur à l’aide de l’adresse IP hello ou nom de domaine complet d’un serveur frontal de hello VM (NAT). Hello exemple suivant répertorie les nom de domaine complet et l’adresse IP publique affectée toohello frontal VM (NAT) Bonjour `myResourceGroup` groupe de ressources. 

```azurecli
az network public-ip list --resource-group myResourceGroup
```
    
## <a name="next-steps"></a>Étapes suivantes
Voulez-vous tooset des vôtre NAT dans Azure ? L’Open Source, gratuit mais puissant ? Alors PF est un bon choix. À l’aide du modèle de hello [pf-freebsd-setup](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup), vous devez uniquement tooset de cinq minutes d’un pare-feu NAT avec tourniquet d’équilibrage à l’aide de FreeBSD PF dans Azure pour le scénario de serveur web courant. 

Si vous souhaitez offre hello toolearn FreeBSD dans Azure, reportez-vous trop[tooFreeBSD introduction sur Azure](freebsd-intro-on-azure.md).

Si vous souhaitez tooknow plus d’informations sur les dossiers publics, reportez-vous trop[FreeBSD manuel](https://www.freebsd.org/doc/handbook/firewalls-pf.html) ou [PF-Guide de](https://www.freebsd.org/doc/handbook/firewalls-pf.html).
