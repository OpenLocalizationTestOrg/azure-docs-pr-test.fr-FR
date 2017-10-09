---
title: "aaaCreate une passerelle d’Application Azure - Azure CLI 1.0 | Documents Microsoft"
description: "Découvrez comment toocreate une passerelle d’Application à l’aide de hello Azure CLI 1.0 dans le Gestionnaire de ressources"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3c0d2d96b6be404d0372d00f0deb2a32959ca419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli"></a>Créer une passerelle d’application à l’aide de hello CLI d’Azure

> [!div class="op_single_selector"]
> * [Portail Azure](application-gateway-create-gateway-portal.md)
> * [Commandes PowerShell pour Azure Resource Manager](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Modèle Azure Resource Manager](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI 1.0](application-gateway-create-gateway-cli.md)
> * [Azure CLI 2.0](application-gateway-create-gateway-cli.md)
> 
> 

La passerelle Azure Application Gateway est un équilibreur de charge de couche 7. Il fournit un basculement, routage des performances des requêtes HTTP entre différents serveurs, qu’ils soient sur le cloud de hello ou localement. Passerelle d’application a hello suivant les fonctionnalités de remise d’applications : charger des sondes de l’intégrité personnalisée équilibrage de charge, l’affinité de basé sur cookie de session et déchargement de Secure Sockets Layer (SSL), HTTP et prise en charge de plusieurs sites.

## <a name="prerequisite-install-hello-azure-cli"></a>Condition préalable : Installez hello CLI d’Azure

les étapes tooperform hello dans cet article, vous devez trop[installer hello Interface de ligne de commande Azure pour Mac, Linux et Windows (Azure CLI)](../xplat-cli-install.md) et que vous devez trop[session tooAzure](../xplat-cli-connect.md). 

> [!NOTE]
> Si vous n’avez pas de compte Azure, vous devez vous en procurer un. Inscrivez-vous à un [essai gratuit ici](../active-directory/sign-up-organization.md).

## <a name="scenario"></a>Scénario

Dans ce scénario, vous découvrez comment une passerelle d’application à l’aide de toocreate hello portail Azure.

Ce scénario va :

* Créer une passerelle Application Gateway moyenne avec deux instances.
* Créer un réseau virtuel nommé ContosoVNET avec un bloc CIDR réservé de 10.0.0.0/16.
* Créer un sous-réseau appelé subnet01 qui utilise 10.0.0.0/28 comme bloc CIDR.

> [!NOTE]
> Les tests de configuration supplémentaires de la passerelle d’application hello, y compris l’intégrité personnalisée, les adresses du pool principal et des règles supplémentaires sont configurés après la configuration de la passerelle d’application hello et non pendant le déploiement initial.

## <a name="before-you-begin"></a>Avant de commencer

La passerelle Application Gateway Azure requiert son propre sous-réseau. Lorsque vous créez un réseau virtuel, assurez-vous que vous laissez suffisamment toohave d’espace adresse plusieurs sous-réseaux. Une fois que vous déployez un tooa de sous-réseau de la passerelle d’application, passerelles d’application supplémentaires seulement sont en mesure de toobe ajouté toohello sous-réseau.

## <a name="log-in-tooazure"></a>Connectez-vous à tooAzure

Ouvrez hello **invite de commandes Microsoft Azure**et les journaux. 

```azurecli-interactive
azure login
```

Une fois que vous tapez hello précédent exemple, un code est fourni. Accédez toohttps://aka.ms/devicelogin dans un processus de connexion de navigateur toocontinue hello.

![Invite de commande affichant le code de l’appareil][1]

Dans le navigateur de hello, entrez le code hello que vous avez reçu. Vous êtes redirigé tooa-page de connexion.

![code de tooenter du navigateur][2]

Une fois que le code de hello a été entré. vous êtes connecté, fermer hello navigateur toocontinue avec le scénario hello.

![Connexion réussie][3]

## <a name="switch-tooresource-manager-mode"></a>Commutateur tooResource Manager Mode

```azurecli-interactive
azure config mode arm
```

## <a name="create-hello-resource-group"></a>Créer le groupe de ressources hello

Avant de créer la passerelle d’application hello, un groupe de ressources est créé de passerelle d’application toocontain hello. Hello Voici commande hello.

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a>Créez un réseau virtuel

Une fois le groupe de ressources hello est créé, un réseau virtuel est créé pour la passerelle d’application hello.  Bonjour l’exemple suivant, l’espace d’adressage hello a été en tant que 10.0.0.0/16 tel que défini dans hello précédant les notes de scénario.

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a>Créer un sous-réseau

Après la création du réseau virtuel hello, un sous-réseau est ajouté pour la passerelle d’application hello.  Si vous envisagez de passerelle d’application toouse avec une application web hébergée Bonjour même virtuel réseau en tant que passerelle d’application hello, tooleave que suffisamment de place pour un autre sous-réseau.

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-hello-application-gateway"></a>Créer une passerelle d’application hello

Une fois que le sous-réseau et le réseau virtuel de hello sont créés, les conditions préalables pour la passerelle d’application hello hello sont terminées. En outre un fichier .pfx exporté précédemment hello et certificat de mot de passe hello certificat sont requis pour hello suivant l’étape : hello IP adresses utilisées pour hello principal sont hello pour votre serveur principal. Ces valeurs peuvent être des deux adresses IP privées dans le réseau virtuel de hello, des adresses IP publiques ou des noms de domaine complet pour vos serveurs principaux.

```azurecli-interactive
azure network application-gateway create \
--name AdatumAppGateway \
--location eastus \
--resource-group ContosoRG \
--vnet-name ContosoVNET \
--subnet-name subnet01 \
--servers 134.170.185.46,134.170.188.221,134.170.185.50 \
--capacity 2 \
--sku-tier Standard \
--routing-rule-type Basic \
--frontend-port 80 \
--http-settings-cookie-based-affinity Enabled \
--http-settings-port 80 \
--http-settings-protocol http \
--frontend-port http \
--sku-name Standard_Medium
```

> [!NOTE]
> Pour obtenir la liste de paramètres qui peuvent être fournies lors de la création de l’exécuter hello de commande suivante : **créer de la passerelle d’application réseau azure--aide**.

Cet exemple crée une passerelle d’application de base avec les paramètres par défaut pour l’écouteur de hello, pool principal, paramètres http du serveur principal et les règles. Vous pouvez modifier ces paramètres toosuit votre déploiement une fois l’approvisionnement de hello réussie.
Si vous avez déjà votre application web définie avec le pool principal d’hello Bonjour précédentes étapes, une fois créés, l’équilibrage de charge démarre.

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment des sondes toocreate d’état personnalisé en vous rendant sur [créer une sonde d’intégrité personnalisé](application-gateway-create-probe-portal.md)

Découvrez comment tooconfigure déchargement SSL et le déchiffrement SSL coûteux take hello désactivé vos serveurs web en vous rendant sur [configurer le déchargement SSL](application-gateway-ssl-arm.md)

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
