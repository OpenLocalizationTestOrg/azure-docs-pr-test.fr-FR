---
title: "aaaHost plusieurs sites avec la passerelle d’Application Azure | Documents Microsoft"
description: "Cette page fournit des instructions tooconfigure une passerelle d’application Windows Azure existante pour l’hébergement de plusieurs applications web sur hello même passerelle avec hello portail Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 95f892f6-fa27-47ee-b980-7abf4f2c66a9
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 2172aa2c80720f6f1ab7dd91745b44654bcaee00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a>Configurer une passerelle Application Gateway existante pour l’hébergement de plusieurs applications web

> [!div class="op_single_selector"]
> * [portail Azure](application-gateway-create-multisite-portal.md)
> * [Commandes PowerShell pour Azure Resource Manager](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

Hébergement de plusieurs sites vous permet de toodeploy plus d’une application web sur hello même passerelle d’application. Il s’appuie sur la présence de l’en-tête d’hôte dans la requête HTTP entrante hello, toodetermine quels écouteur reçoit le trafic. écouteur de Hello dirige ensuite pool principal de tooappropriate trafic tel que configuré dans la définition des règles de passerelle de hello hello. Dans les applications web SSL est activé, passerelle d’application s’appuie sur hello Indication de nom de serveur (SNI) extension toochoose hello correct écouteur pour le trafic web hello. Une utilisation courante pour l’hébergement de plusieurs sites est équilibrer les demandes de tooload pour les pools de serveur principal toodifferent web différents domaines. De même, plusieurs sous-domaines de hello même domaine racine peut également être hébergé sur hello même passerelle d’application.

## <a name="scenario"></a>Scénario

Dans l’exemple suivant de hello, passerelle d’application sert le trafic pour contoso.com et fabrikam.com avec deux pools de serveur principal : contoso pool de serveurs et de pool de serveurs de fabrikam. Le programme d’installation similaire peut être sous-domaines toohost utilisés comme app.contoso.com et blog.contoso.com.

![scénario multisite][multisite]

## <a name="before-you-begin"></a>Avant de commencer

Ce scénario ajoute la prise en charge de plusieurs sites tooan une passerelle d’application existant. toocomplete tooconfigure disponible de toobe a besoin de ce scénario, une passerelle d’application existant. Visitez [créer une passerelle d’application à l’aide du portail de hello](application-gateway-create-gateway-portal.md) toolearn comment toocreate une passerelle d’application de base dans le portail de hello.

Hello Voici les étapes de hello nécessaires passerelle d’application hello tooupdate :

1. Créer toouse pools du serveur principal pour chaque site.
2. Créez un écouteur pour chaque site que la passerelle Application Gateway prend en charge.
3. Créer règles toomap chaque écouteur et hello approprié back-end.

## <a name="requirements"></a>Configuration requise

* **Pool de serveur principal :** liste hello des adresses IP des serveurs principaux de hello. adresses IP de Hello répertoriés doivent appartenir soit de sous-réseau de réseau virtuel toohello ou doivent être une adresse IP/VIP publique. Le nom de domaine complet peut également être utilisé.
* **Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies. Ces paramètres sont lié tooa pool et sont des serveurs tooall appliqué dans le pool de hello.
* **Port frontal :** ce port est le port public hello qui est ouvert sur la passerelle d’application hello. Le trafic atteint ce port et obtient redirigés tooone de hello sur les serveurs principaux.
* **Écouteur :** hello port d’écoute utilise un port frontal, un protocole (Http ou Https, ces valeurs respectent la casse) et le nom du certificat SSL hello (si le déchargement de la configuration de SSL). Pour les passerelles Application Gateway activées pour plusieurs sites, le nom d’hôte et les indicateurs SNI sont également ajoutés.
* **La règle :** règle de hello lie écouteur hello, pool de serveur principal hello et définit le trafic de hello de pool de serveur principal doit être dirigée toowhen il atteint un écouteur particulier. Les règles sont traitées dans l’ordre de hello qu’ils sont répertoriés, et le trafic est dirigé via hello première règle qui correspond, quelle que soit la spécificité. Par exemple, si vous disposez d’une règle à l’aide d’un écouteur de base et une règle à l’aide d’un écouteur de plusieurs site à la fois sur hello même règle de port, hello avec écouteur de plusieurs sites hello doit figurer avant les règle hello qu’un écouteur de base hello dans l’ordre pour toofunction de règle de plusieurs sites hello en tant que attendu. 
* **Certificats :** chaque écouteur requiert un certificat unique, dans cet exemple, 2 écouteurs sont créés pour plusieurs sites. Deux .pfx certificats et les mots de passe hello pour eux doivent toobe créé.

## <a name="create-back-end-pools-for-each-site"></a>Créer des pools principaux pour chaque site

Un pool principal pour chaque site que cette passerelle Application Gateway prend en charge est nécessaire, dans cet exemple, 2 sont créés : un pour contoso11.com et un fabrikam11.com.

### <a name="step-1"></a>Étape 1

Accédez à passerelle d’application existant tooan Bonjour portail Azure (https://portal.azure.com). Sélectionnez **Pools principaux** et cliquez sur **Ajouter**

![ajouter des pools principaux][7]

### <a name="step-2"></a>Étape 2

Renseignez les informations de hello pour le pool principal de hello **pool1**, en ajoutant des adresses ip hello ou des noms de domaine complets pour les serveurs principaux hello et cliquez sur **OK**

![paramètres du pool principal pool1][8]

### <a name="step-3"></a>Étape 3 :

Panneau de pools de principaux hello sur **ajouter** tooadd un pool principal supplémentaire **pool2**, en ajoutant des adresses ip hello ou des noms de domaine complets pour les serveurs principaux hello et cliquez sur **OK**

![paramètres du pool principal pool2][9]

## <a name="create-listeners-for-each-back-end"></a>Créer des écouteurs pour chaque serveur principal

Passerelle d’application s’appuie sur HTTP 1.1 hôte en-têtes toohost plus d’un site Web sur hello même adresse IP publique et le port. écouteur de base Hello créé dans le portail de hello ne contient pas cette propriété.

### <a name="step-1"></a>Étape 1

Cliquez sur **écouteurs** hello passerelle d’application existant et cliquez sur **multisite** premier écouteur de tooadd hello.

![panneau Vue d’ensemble des écouteurs][1]

### <a name="step-2"></a>Étape 2

Complétez les informations de hello pour le port d’écoute hello. Dans cet exemple la terminaison SSL est configurée, créez un nouveau port de serveur frontal. Téléchargez toobe de certificat .pfx hello utilisé pour la terminaison SSL. Hello sur ce panneau d’écouteur de base standard de toohello panneau par rapport diffère uniquement nom d’hôte hello.

![panneau Propriétés d’écouteur][2]

### <a name="step-3"></a>Étape 3 :

Cliquez sur **multisite** et créer un autre écouteur comme décrit dans l’étape précédente de hello pour le site de deuxième hello. Assurez-vous que toouse un certificat différent pour l’écouteur de deuxième hello. Hello sur ce panneau d’écouteur de base standard de toohello panneau par rapport diffère uniquement nom d’hôte hello. Renseignez les informations hello pour le port d’écoute hello et cliquez sur **OK**.

![panneau Propriétés d’écouteur][3]

> [!NOTE]
> La création d’écouteurs Bonjour portail Azure pour la passerelle d’application est une tâche de longue durée, peut prendre quelques hello toocreate de temps deux écouteurs dans ce scénario. Lorsque les écouteurs hello complète affichent dans le portail de hello comme Bonjour suivant image :

![vue d’ensemble de l’écouteur][4]

## <a name="create-rules-toomap-listeners-toobackend-pools"></a>Créer des pools de toobackend toomap écouteurs de règles

### <a name="step-1"></a>Étape 1

Accédez à passerelle d’application existant tooan Bonjour portail Azure (https://portal.azure.com). Sélectionnez **règles** , sélectionnez une règle par défaut existant hello **rule1** et cliquez sur **modifier**.

### <a name="step-2"></a>Étape 2

Remplir le panneau de règles hello comme Bonjour suivant l’image. Choisissez le premier écouteur de hello et premier pool et sur **enregistrer** lorsque vous avez terminé.

![modifier une règle existante][6]

### <a name="step-3"></a>Étape 3 :

Cliquez sur **de règles de base** deuxième règle de toocreate hello. Rempliront hello avec hello deuxième port d’écoute et le second pool principal et cliquez sur **OK** toosave.

![panneau ajouter une règle de base][10]

Ce scénario procède à la configuration d’une passerelle d’application existant avec prise en charge de plusieurs site via hello portail Azure.

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment tooprotect vos sites Web avec [passerelle d’Application - pare-feu d’applications Web](application-gateway-webapplicationfirewall-overview.md)

<!--Image references-->
[1]: ./media/application-gateway-create-multisite-portal/figure1.png
[2]: ./media/application-gateway-create-multisite-portal/figure2.png
[3]: ./media/application-gateway-create-multisite-portal/figure3.png
[4]: ./media/application-gateway-create-multisite-portal/figure4.png
[5]: ./media/application-gateway-create-multisite-portal/figure5.png
[6]: ./media/application-gateway-create-multisite-portal/figure6.png
[7]: ./media/application-gateway-create-multisite-portal/figure7.png
[8]: ./media/application-gateway-create-multisite-portal/figure8.png
[9]: ./media/application-gateway-create-multisite-portal/figure9.png
[10]: ./media/application-gateway-create-multisite-portal/figure10.png
[multisite]: ./media/application-gateway-create-multisite-portal/multisite.png
