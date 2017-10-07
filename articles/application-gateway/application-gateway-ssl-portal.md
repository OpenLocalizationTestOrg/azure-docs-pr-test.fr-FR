---
title: "aaaConfigure SSL décharger - passerelle d’Application Azure - Azure Portal | Documents Microsoft"
description: "Cette page fournit toocreate instructions déchargement d’une passerelle d’application avec SSL à l’aide du portail de hello"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 8373379a-a26a-45d2-aa62-dd282298eff3
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: e87ac0bbe10ac45e307c18802741c7bc31764a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-portal"></a>Configurer une passerelle d’application pour le déchargement SSL à l’aide du portail de hello

> [!div class="op_single_selector"]
> * [Portail Azure](application-gateway-ssl-portal.md)
> * [Commandes PowerShell pour Azure Resource Manager](application-gateway-ssl-arm.md)
> * [Azure Classic PowerShell](application-gateway-ssl.md)
> * [Azure CLI 2.0](application-gateway-ssl-cli.md)

Passerelle d’Application Azure peut être configuré tooterminate hello Secure Sockets Layer (SSL) session à hello passerelle tooavoid coûteux SSL déchiffrement tâches toohappen au niveau de la batterie de serveurs web hello. Déchargement SSL simplifie également la configuration de serveur frontal de hello et la gestion d’application web de hello.

## <a name="scenario"></a>Scénario

Hello scénario traverse configuration SSL décharger sur une passerelle d’application existant. Hello scénario part du principe que vous avez déjà suivi les étapes de hello trop[créer une passerelle d’Application](application-gateway-create-gateway-portal.md).

## <a name="before-you-begin"></a>Avant de commencer

déchargement SSL tooconfigure avec une passerelle d’application, un certificat est requis. Ce certificat est chargé sur la passerelle d’application hello et utilisé tooencrypt et le décryptage du trafic hello envoyé via SSL. certificat de Hello doit toobe au format d’échange d’informations personnelles (pfx). Ce format de fichier permet hello privé toobe clé exporté requis par hello application passerelle tooperform hello chiffrement et de déchiffrement du trafic.

## <a name="add-an-https-listener"></a>Ajouter un écouteur HTTPS

port d’écoute HTTPS Hello recherche pour le trafic en fonction de sa configuration et vous aide au pools principaux toohello itinéraire hello du trafic.

### <a name="step-1"></a>Étape 1

Accédez toohello portail Azure et sélectionnez une passerelle d’application existant

### <a name="step-2"></a>Étape 2

Cliquez sur les écouteurs et cliquez sur tooadd de bouton hello ajouter un écouteur.

![Panneau de vue d’ensemble de passerelle d’application][1]

### <a name="step-3"></a>Étape 3 :

Remplissez les informations de hello requis pour hello écouteur et le téléchargement hello certificat .pfx, lorsque vous avez terminé cliquez sur OK.

**Nom** -cette valeur est un nom convivial de l’écouteur de hello.

**Configuration IP de Frontend** -cette valeur est la configuration IP de serveur frontal hello qui est utilisée pour le port d’écoute hello.

**Le port frontal (nom/Port)** -un nom convivial pour le port hello utilisé sur les serveurs frontaux hello de passerelle d’application hello et port réelle de hello utilisé.

**Protocole** -un toodetermine commutateur si https ou http est utilisé pour le serveur frontal hello.

**Certificat (nom/mot de passe)** - si le déchargement SSL est utilisé, un certificat .pfx est requis pour ce paramètre, et un nom convivial et un mot de passe sont requis.

![ajouter panneau d’écouteur][2]

## <a name="create-a-rule-and-associate-it-toohello-listener"></a>Créer une règle et l’associer toohello écouteur

écouteur de Hello a été créé. Il est temps toocreate un règle toohandle hello du trafic à partir de l’écouteur de hello. Les règles définissent comment le trafic est routé toohello pools de principaux en fonction de plusieurs paramètres de configuration, notamment si l’affinité de session basée sur le cookie est utilisée, protocole, port et sondes d’intégrité.

### <a name="step-1"></a>Étape 1

Cliquez sur hello **règles** de passerelle d’application hello, puis cliquez sur Ajouter.

![Panneau de règles Application Gateway][3]

### <a name="step-2"></a>Étape 2

Sur hello **ajouter une règle base** panneau, tapez Bonjour le nom convivial pour la règle de hello et choisissez écouteur hello créé à l’étape précédente de hello. Choisissez le pool principal approprié de hello et configuration de http et cliquez sur **OK**

![fenêtre de paramètres https][4]

paramètres de Hello sont à présent enregistrées toohello passerelle d’application. Hello processus pour ces paramètres d’enregistrement peut prendre un certain temps avant qu’elles soient tooview disponible via le portail de hello ou PowerShell. Passerelle d’application après avoir sauvegardé hello gère le chiffrement hello et le déchiffrement du trafic. Tout le trafic entre la passerelle d’application hello et serveurs web de principaux hello est géré via http. Client toohello chiffrée, n’importe quel client de retour toohello communication si lancé via le protocole https est retournée.

## <a name="next-steps"></a>Étapes suivantes

toolearn tooconfigure un état personnalisé sonde avec la passerelle d’Application Azure, voir [créer une sonde d’intégrité personnalisé](application-gateway-create-gateway-portal.md).

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
