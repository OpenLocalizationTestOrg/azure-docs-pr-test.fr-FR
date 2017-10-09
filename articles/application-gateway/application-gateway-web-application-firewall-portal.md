---
title: "aaaCreate ou mettre à jour une passerelle d’Application Azure avec pare-feu d’applications web | Documents Microsoft"
description: "Découvrez comment toocreate une passerelle d’Application avec le pare-feu d’applications web à l’aide de hello portail"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b561a210-ed99-4ab4-be06-b49215e3255a
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: 68d140fef14499da654ea251d1208e6a800f55a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-web-application-firewall-by-using-hello-portal"></a>Créer une passerelle d’application avec le pare-feu d’applications web à l’aide du portail de hello

> [!div class="op_single_selector"]
> * [Portail Azure](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Interface de ligne de commande Azure](application-gateway-web-application-firewall-cli.md)

Découvrez comment toocreate un pare-feu d’applications web activé la passerelle d’application.

pare-feu d’applications Hello web (WAF) dans la passerelle d’Application Azure protège les applications web à partir des attaques courantes basée sur le web telles que l’injection SQL, les attaques de script entre sites et des détournements de session. Application Web protège contre un grand nombre des hello OWASP avoir top 10 web vulnérabilités courantes.

## <a name="scenarios"></a>Scénarios

Dans cet article, il existe deux scénarios :

Dans le premier scénario de hello, vous découvrez trop[créer une passerelle d’application avec le pare-feu d’applications web](#create-an-application-gateway-with-web-application-firewall)

Dans le second scénario de hello, vous découvrez trop[ajouter web application pare-feu tooan existant passerelle d’application](#add-web-application-firewall-to-an-existing-application-gateway).

![Exemple de scénario][scenario]

> [!NOTE]
> Les tests de configuration supplémentaires de la passerelle d’application hello, y compris l’intégrité personnalisée, les adresses du pool principal et des règles supplémentaires sont configurés après la configuration de la passerelle d’application hello et non pendant le déploiement initial.

## <a name="before-you-begin"></a>Avant de commencer

La passerelle Application Gateway Azure requiert son propre sous-réseau. Lorsque vous créez un réseau virtuel, assurez-vous que vous laissez suffisamment toohave d’espace adresse plusieurs sous-réseaux. Une fois que vous déployez un tooa de sous-réseau de la passerelle d’application, passerelles d’application supplémentaires seulement sont en mesure de toobe ajouté toohello sous-réseau.

##<a name="add-web-application-firewall-to-an-existing-application-gateway"></a>Ajouter web application pare-feu tooan existant passerelle d’application

Cet exemple met à jour un application passerelle toosupport web application de pare-feu existant en mode de prévention.

1. Bonjour Azure portal **favoris** volet, cliquez sur **toutes les ressources**. Cliquez sur hello passerelle d’Application existante dans hello **toutes les ressources** panneau. Si l’abonnement hello déjà sélectionné comporte plusieurs ressources, vous pouvez entrer le nom de hello Bonjour **filtrer par nom...** zone DNS zone tooeasily accès hello.

   ![Création d’une passerelle Application Gateway][1]

1. Cliquez sur **pare-feu d’applications Web** et mettre à jour les paramètres de passerelle d’application hello. Lorsque vous avez terminé, cliquez sur **Enregistrer**

    paramètres de Hello tooupdate un pare-feu d’applications web existantes application passerelle toosupport sont les suivantes :

   | **Paramètre** | **Valeur** | **Détails**
   |---|---|---|
   |**Mise à niveau tooWAF couche**| Activé | Cela définit le niveau hello de hello passerelle toohello WAF applicative.|
   |**État du pare-feu**| Activé | Ce paramètre active le pare-feu sur hello WAF hello.|
   |**Mode du pare-feu** | Prévention | Ce paramètre spécifique comment le pare-feu d’application web traite le trafic malveillant. **Détection** mode consigne uniquement les événements de hello, où **prévention** mode journalise les événements de hello et s’arrête hello du trafic malveillant.|
   |**Ensemble de règles**|3.0|Ce paramètre détermine hello [ensemble de règles de base](application-gateway-web-application-firewall-overview.md#core-rule-sets) qui est utilisé tooprotect hello principaux membres du pool.|
   |**Configurer des règles désactivées**|varie|tooprevent possible de faux positifs, ce paramètre vous permet de toodisable certains [et groupes de règles](application-gateway-crs-rulegroups-rules.md).|

    >[!NOTE]
    > Lors de la mise à niveau un existant toohello de passerelle d’application WAF référence (SKU), hello référence (SKU) de taille modifications trop**support**. Cela peut être reconfiguré une fois la configuration terminée.

    ![panneau montrant les paramètres de base][2-1]

    > [!NOTE]
    > journaux du pare-feu tooview web application, diagnostics doivent être activés et ApplicationGatewayFirewallLog sélectionné. Vous pouvez choisir un nombre d’instances de 1 à des fins de test. Il est important que n’importe quelle instance compte dans les deux instances de tooknow n’est pas couverte par un contrat SLA de hello et ne sont donc pas recommandée. Les petites passerelles ne sont pas disponibles lorsque vous utilisez des pare-feu d’applications web.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>créer une passerelle d’application avec le pare-feu d’applications web

Ce scénario va :

* créer une passerelle Application Gateway moyenne avec deux instances ;
* créer un réseau virtuel nommé AdatumAppGatewayVNET avec un bloc CIDR réservé de 10.0.0.0/16 ;
* créer un sous-réseau appelé Appgatewaysubnet qui utilise 10.0.0.0/28 comme bloc CIDR ;
* configurer un certificat pour le déchargement SSL.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com). Si vous ne possédez pas encore de compte, vous pouvez [vous inscrire pour bénéficier d’un essai gratuit d’un mois](https://azure.microsoft.com/free).
1. Dans le volet de favoris hello du portail de hello, cliquez sur **nouveau**
1. Bonjour **nouveau** panneau, cliquez sur **réseau**. Bonjour **réseau** panneau, cliquez sur **Application Gateway**, comme indiqué dans hello suivant image :
1. Accédez toohello portail Azure, cliquez sur **nouveau** > **réseau** > **Application Gateway**

    ![Création d’une passerelle Application Gateway][1]

1. Bonjour **notions de base** panneau qui s’affiche, entrez hello valeurs suivantes, puis cliquez sur **OK**:

   | **Paramètre** | **Valeur** | **Détails**
   |---|---|---|
   |**Nom**|AdatumAppGateway|nom de Hello de passerelle d’application hello|
   |**Niveau**|WAF|Les valeurs disponibles sont Standard et WAF. Visitez [pare-feu d’applications web](application-gateway-web-application-firewall-overview.md) toolearn plus WAF.|
   |**Taille de la référence (SKU)**|Moyenne|Si vous sélectionnez le niveau Standard, vous avez le choix entre Petite, Moyenne et Grande. Si vous choisissez le niveau WAF, les options sont limitées à Moyenne et Grande.|
   |**Nombre d’instances**|2|Nombre d’instances de la passerelle d’application hello pour la haute disponibilité. Un nombre d’instances de 1 doit être utilisé uniquement à des fins de test.|
   |**Abonnement**|[Votre abonnement]|Sélectionnez une passerelle d’application abonnement toocreate hello dans.|
   |**Groupe de ressources**|**Créer un nouveau :** AdatumAppGatewayRG|Créez un groupe de ressources. nom de groupe de ressources Hello doit être unique au sein de l’abonnement hello sélectionné. toolearn plus d’informations sur les groupes de ressources, lire hello [le Gestionnaire de ressources](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) l’article de vue d’ensemble.|
   |**Emplacement**|Ouest des États-Unis||

   ![panneau montrant les paramètres de base][2-2]

1. Bonjour **paramètres** panneau s’affiche sous **réseau virtuel**, cliquez sur **choisir un réseau virtuel**. Cette étape s’ouvre entrez hello **réseau virtuel de choisir** panneau.  Cliquez sur **nouvel** tooopen hello **créer un réseau virtuel** panneau.

   ![choisir un réseau virtuel][2]

1. Sur hello **Panneau de réseau virtuel créer** , puis entrez les valeurs suivantes de hello **OK**. Cette étape ferme hello **créer un réseau virtuel** et **réseau virtuel de choisir** lames. Cette opération remplit hello **sous-réseau** champ hello **paramètres** panneau avec sous-réseau hello choisi.

   |**Paramètre** | **Valeur** | **Détails** |
   |---|---|---|
   |**Nom**|AdatumAppGatewayVNET|Nom de la passerelle d’application hello|
   |**Espace d’adressage**|10.0.0.0/16| Cette valeur est l’espace d’adressage hello pour le réseau virtuel de hello|
   |**Nom du sous-réseau**|AppGatewaySubnet|Nom du sous-réseau de hello pour la passerelle d’application hello|
   |**Plage d’adresses de sous-réseau**|10.0.0.0/28 | Ce sous-réseau permet à d’autres sous-réseaux supplémentaires dans le réseau virtuel de hello pour les membres du pool principal|

1. Sur hello **paramètres** panneau sous **configuration Frontend IP**, choisissez **Public** comme hello **type d’adresse IP**

1. Sur hello **paramètres** panneau sous **adresse IP publique**, cliquez sur **choisir une adresse IP publique**, cette étape permet d’ouvrir hello **choisir une adresse IP publique**panneau, cliquez sur **nouvel**.

   ![choisir une adresse ip publique][3]

1. Sur hello **créer une adresse IP publique** panneau, acceptez la valeur par défaut de hello, puis cliquez sur **OK**. Cette étape ferme hello **choisir une adresse IP publique** panneau, hello **créer une adresse IP publique** panneau et le remplir **adresse IP publique** avec l’adresse IP publique hello choisi.

1. Sur hello **paramètres** panneau sous **configuration de l’écouteur**, cliquez sur **HTTP** sous **protocole**. toouse **https**, un certificat est requis. clé privée de Hello du certificat de hello est nécessaire pour une exportation .pfx du certificat de hello doit toobe fourni et hello de mot de passe pour le fichier de hello.

1. Configurer hello **WAF** des paramètres spécifiques.

   |**Paramètre** | **Valeur** | **Détails** |
   |---|---|---|
   |**État du pare-feu**| Activé| Ce paramètre active ou désactive WAF.|
   |**Mode du pare-feu** | Prévention| Ce paramètre détermine les actions hello que WAF prend le trafic malveillant. Si le mode de **détection** est choisi, le trafic est uniquement consigné.  Si le mode de **prévention** est choisi, le trafic est consigné et bloqué avec une réponse d’erreur d’autorisation 403.|


1. Passez en revue la page Résumé de hello et cliquez sur **OK**.  Maintenant la passerelle d’application hello est la file d’attente et créé.

1. Une fois que la passerelle d’application hello a été créé, accédez à tooit dans la configuration du portail toocontinue hello de passerelle d’application hello.

    ![Vue des ressources de la passerelle Application Gateway][10]

Les étapes suivantes créent une passerelle d’application de base avec les paramètres par défaut pour l’écouteur de hello, pool principal, paramètres http du serveur principal et les règles. Vous pouvez modifier ces paramètres toosuit votre déploiement une fois l’approvisionnement de hello réussie

> [!NOTE]
> Passerelles d’application créés avec la configuration du pare-feu application hello web de base sont configurés avec CRS 3.0 pour les protections.

## <a name="next-steps"></a>Étapes suivantes

Ensuite, vous pouvez apprendre comment tooconfigure un alias de domaine personnalisé pour hello [adresse IP publique](../dns/dns-custom-domain.md#public-ip-address) à l’aide d’Azure DNS ou un autre fournisseur DNS.

Découvrez comment tooconfigure journalisation des diagnostics, événements de hello toolog détectés ou prévenir pare-feu d’applications web en vous rendant sur [Diagnostics de passerelle d’Application](application-gateway-diagnostics.md)

Découvrez comment des sondes toocreate d’état personnalisé en vous rendant sur [créer une sonde d’intégrité personnalisé](application-gateway-create-probe-portal.md)

Découvrez comment tooconfigure déchargement SSL et le déchiffrement SSL coûteux take hello désactivé vos serveurs web en vous rendant sur [configurer le déchargement SSL](application-gateway-ssl-portal.md)

<!--Image references-->
[1]: ./media/application-gateway-web-application-firewall-portal/figure1.png
[2]: ./media/application-gateway-web-application-firewall-portal/figure2.png
[2-1]: ./media/application-gateway-web-application-firewall-portal/figure2-1.png
[2-2]: ./media/application-gateway-web-application-firewall-portal/figure2-2.png
[3]: ./media/application-gateway-web-application-firewall-portal/figure3.png
[10]: ./media/application-gateway-web-application-firewall-portal/figure10.png
[scenario]: ./media/application-gateway-web-application-firewall-portal/scenario.png
