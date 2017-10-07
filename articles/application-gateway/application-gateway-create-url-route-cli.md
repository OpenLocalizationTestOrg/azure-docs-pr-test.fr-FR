---
title: "aaaCreate une passerelle d’application à l’aide de routage d’URL règles - Azure CLI 2.0 | Documents Microsoft"
description: "Cette page fournit des instructions toocreate, configurez une passerelle d’application Windows Azure à l’aide des règles de routage d’URL"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: 335b52be258945e1172eb0252b732e0e6ecb2ef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing-with-azure-cli-20"></a>Créer une passerelle d’application à l’aide du routage basé sur le chemin avec Azure CLI 2.0

> [!div class="op_single_selector"]
> * [Portail Azure](application-gateway-create-url-route-portal.md)
> * [Commandes PowerShell pour Azure Resource Manager](application-gateway-create-url-route-arm-ps.md)
> * [Azure CLI 2.0](application-gateway-create-url-route-cli.md)

Le routage basé sur le chemin d’accès URL permet d’itinéraires tooassociate vous selon le chemin d’URL de hello d’une requête Http. Il vérifie s’il existe un pool de back-end tooa itinéraire configuré pour hello les URL présentée dans hello passerelle d’Application et envoie toohello de trafic réseau hello défini par pool de back-end. Une utilisation courante pour le routage basé sur l’URL est équilibrer les demandes de tooload pour les pools de serveur principal toodifferent différents types de contenu.

Le routage basé sur des URL introduit une nouvelle passerelle de tooapplication de type de règle. La passerelle Application Gateway comporte deux types de règles : une règle de base et PathBasedRouting. Type de règle de base fournit des service tourniquet pour les principaux hello pools lors PathBasedRouting en outre distribution Round robin de tooround, prend également le modèle de chemin d’accès de l’URL de demande hello en compte tout en appuyant sur le pool principal d’hello.

## <a name="scenario"></a>Scénario

Dans l’exemple suivant de hello, passerelle d’Application sert le trafic pour contoso.com avec deux pools de serveur principal : un pool de serveurs par défaut et un pool de serveurs d’image.

Demandes de http://contoso.com/image * sont routés de pool de serveurs tooimage (imagesBackendPool), si hello modèle du chemin d’accès ne correspond pas, un pool de serveurs par défaut (appGatewayBackendPool) est sélectionné.

![itinéraire d’URL](./media/application-gateway-create-url-route-cli/scenario.png)

## <a name="log-in-tooazure"></a>Connectez-vous à tooAzure

Ouvrez hello **invite de commandes Microsoft Azure**et les journaux. 

```azurecli
az login -u "username"
```

> [!NOTE]
> Vous pouvez également utiliser `az login` sans commutateur hello pour la connexion de périphérique qui requiert la saisie d’un code à aka.ms/devicelogin.

Une fois que vous tapez hello précédent exemple, un code est fourni. Accédez toohttps://aka.ms/devicelogin dans un processus de connexion de navigateur toocontinue hello.

![Invite de commande affichant le code de l’appareil][1]

Dans le navigateur de hello, entrez le code hello que vous avez reçu. Vous êtes redirigé tooa-page de connexion.

![code de tooenter du navigateur][2]

Une fois que le code de hello a été entré. vous êtes connecté, fermer hello navigateur toocontinue avec le scénario hello.

![Connexion réussie][3]

## <a name="add-a-path-based-rule-tooan-existing-application-gateway"></a>Ajouter une passerelle d’application existant du tooan une règle basée sur le chemin d’accès

Créer une passerelle d’application avec une règle de chemin personnalisée

### <a name="create-a-new-back-end-pool"></a>Créer un pool principal

Configurer le paramètre de passerelle d’application **imagesBackendPool** hello équilibrés en charge le trafic réseau dans le pool principal d’hello. Dans cet exemple, vous configurez les paramètres de pool principal différent pour le nouveau pool de back-end hello. Chaque pool principal peut avoir son propre paramètre de pool principal.  Paramètres HTTP du serveur principal sont utilisées par les règles tooroute trafic toohello les membres du pool principal approprié. Ce paramètre détermine le protocole de hello et port qui est utilisé lors de l’envoi de trafic toohello les membres du pool principal. Sessions basées sur un cookie sont également déterminées par les paramètres HTTP hello principal.  S’il est activé, l’affinité de basé sur cookie de session envoie le trafic toohello même principal en tant que requêtes précédentes pour chaque paquet.

```azurecli-interactive
az network application-gateway address-pool create \
--gateway-name AdatumAppGateway \
--name imagesBackendPool  \
--resource-group myresourcegroup \
--servers 10.0.0.6 10.0.0.7
```

### <a name="create-a-new-front-end-port"></a>Créer un port frontal

Configurer le port frontal de hello pour une passerelle d’application. objet de configuration du port frontal Hello est utilisé par un toodefine écoute le port d’écoute de passerelle d’Application hello pour le trafic sur le port d’écoute hello.

```azurecli-interactive
az network application-gateway frontend-port create --port 82 --gateway-name AdatumAppGateway --resource-group myresourcegroup --name port82
```

### <a name="create-a-new-listener"></a>Créer un écouteur

Configurer un écouteur de hello. Cette étape configure l’écouteur hello pour l’adresse IP publique de hello et le port utilisé tooreceive du trafic réseau entrant. Hello, l’exemple suivant prend une configuration IP frontale de hello précédemment configuré, la configuration de port frontal et un protocole (http ou https) et configure l’écouteur de hello. Dans cet exemple, port d’écoute hello écoute tooHTTP du trafic sur le port 82 hello adresse IP publique qui a été créé précédemment.

```azurecli-interactive
az network application-gateway http-listener create --name imageListener --frontend-ip appGatewayFrontendIP  --frontend-port port82 --resource-group myresourcegroup --gateway-name AdatumAppGateway
```

### <a name="create-hello-url-path-map"></a>Créer le mappage de chemin d’accès d’Url hello

Configurer les chemins d’accès de la règle URL pour les pools principaux hello. Cette étape configure le chemin d’accès relatif hello utilisé par la passerelle toodefine hello mappage entre le chemin d’accès de l’URL et le pool principal reçoit le trafic entrant de toohandle hello.

> [!IMPORTANT]
> Chaque chemin d’accès doit commencer par / et hello uniquement une «\*» est autorisé, à la fin de hello. /xyz, /xyz* ou /xyz/* sont des exemples valides. Hello chaîne fed détecteur de chemin d’accès toohello n’inclut pas de texte après hello tout d’abord « ? » ou « # » et ces caractères ne sont pas autorisés. 

Hello exemple suivant crée une règle pour « / images / * « chemin d’accès de routage du trafic tooback-end « imagesBackendPool ». Cette règle garantit que le trafic pour chaque jeu d’URL est routé toohello principal. Par exemple, http://adatum.com/images/figure1.jpg devient trop « imagesBackendPool ». Si le chemin d’accès hello ne correspond pas à une des règles de chemin d’accès prédéterminé hello, configuration de mappage de chemin d’accès de règle hello configure également un pool d’adresses principal par défaut. Par exemple, http://adatum.com/shoppingcart/test.html devient toopool1 telle qu’elle est définie en tant que pool par défaut de hello pour le trafic non apparié.

```azurecli-interactive
az network application-gateway url-path-map create \
--gateway-name AdatumAppGateway \
--name imagespathmap \
--paths /images/* \
--resource-group myresourcegroup2 \
--address-pool imagesBackendPool \
--default-address-pool appGatewayBackendPool \
--default-http-settings appGatewayBackendHttpSettings \
--http-settings appGatewayBackendHttpSettings \
--rule-name images
```

## <a name="next-steps"></a>Étapes suivantes

Si vous souhaitez toolearn sur le déchargement de Secure Sockets Layer (SSL), consultez [configurer une passerelle d’application pour le déchargement SSL](application-gateway-ssl-cli.md).


[scenario]: ./media/application-gateway-create-url-route-cli/scenario.png
[1]: ./media/application-gateway-create-url-route-cli/figure1.png
[2]: ./media/application-gateway-create-url-route-cli/figure2.png
[3]: ./media/application-gateway-create-url-route-cli/figure3.png
