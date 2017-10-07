---
title: "connecteurs de Proxy d’Application aaaUnderstand Azure AD | Documents Microsoft"
description: "Traite des principes de base hello des connecteurs de Proxy d’Application Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 294cb26803ef7cf8be9f3af0678d6d2e64f6cc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-ad-application-proxy-connectors"></a>Présentation des connecteurs de proxy d’application Azure AD

Les connecteurs rendent possible le proxy d’application Azure AD. Ils sont simple, facile toodeploy et mettre à jour et super puissant. Cet article explique les connecteurs sont, leur fonctionnement et certaines des suggestions pour toooptimize votre déploiement. 

## <a name="what-is-an-application-proxy-connector"></a>Qu’est-ce qu’un connecteur de proxy d’application ?

Les connecteurs sont des agents légers qui se trouvent sur site et facilitent le service de Proxy d’Application toohello hello connexion sortante. Connecteurs doivent être installés sur un serveur Windows qui a accès le toohello application principale. Vous pouvez organiser des connecteurs dans les groupes de connecteurs à chaque groupe de gestion des applications de toospecific du trafic. Connecteurs équilibrer automatiquement et peut aider à toooptimize structure de votre réseau. 

## <a name="requirements-and-deployment"></a>Exigences et déploiement

toodeploy Proxy d’Application avec succès, vous devez au moins un connecteur, mais nous vous recommandons de deux ou plusieurs pour assurer la résilience supérieure. Installer le connecteur de hello sur un ordinateur Windows Server 2012 R2 ou machine 2016. connecteur de Hello doit toocommunicate en mesure de toobe avec le service de Proxy d’Application hello, ainsi que des applications locales hello que vous publiez. 

Pour plus d’informations sur la configuration requise pour le serveur de connecteur hello hello, consultez [prise en main le Proxy d’Application et l’installation d’un connecteur](active-directory-application-proxy-enable.md).

## <a name="maintenance"></a>Maintenance 
Hello connecteurs et service de hello prenez soin de toutes les tâches de haute disponibilité hello. Vous pouvez les ajouter ou supprimer de manière dynamique. Chaque fois qu’une nouvelle demande arrive, il est routé tooone des connecteurs de hello qui est actuellement disponible. Si un connecteur n’est pas disponible temporairement, il ne répond pas le trafic de toothis.

les connecteurs Hello sont sans état et n’ont aucune donnée de configuration sur l’ordinateur de hello. Hello uniquement les données qu’ils contiennent sont hello paramètres pour la connexion de service de hello et son certificat d’authentification. Lorsqu’ils connectent toohello service, ils extraient toutes les données de configuration hello requis et actualiser toutes les deux minutes.

Connecteurs interrogent également toofind de serveur hello s’il existe une version plus récente du connecteur de hello. S’il existe, les connecteurs hello se mettent à jour.

Vous pouvez surveiller vos connecteurs à partir de l’ordinateur hello qu’ils sont en cours d’exécution, à l’aide du journal des événements hello et compteurs de performance. Ou vous pouvez afficher leur état à partir de la page de Proxy d’Application hello Hello portail Azure :

 ![Connecteurs de proxy d’application Azure AD](./media/application-proxy-understand-connectors/app-proxy-connectors.png)

Vous n’avez pas toomanually supprimer les liens qui ne sont pas utilisés. Lorsqu’un connecteur est en cours d’exécution, il reste actif comme il connecte toohello service. Les connecteurs inutilisés sont marqués comme _inactifs_ et sont supprimés après 10 jours d’inactivité. Si vous voulez toouninstall un connecteur, cependant, désinstallez les services de connecteur hello et hello Updater hello serveur. Redémarrez votre ordinateur toofully supprimer hello service.

## <a name="automatic-updates"></a>Mises à jour automatiques

Azure AD fournit les mises à jour automatiques pour tous les connecteurs hello que vous déployez. Tant que hello service de mise à jour du connecteur Application Proxy est en cours d’exécution, vos connecteurs de mettre à jour automatiquement. Si vous ne voyez pas hello du service de mise à jour du connecteur sur votre serveur, vous devez trop[réinstaller votre connecteur](active-directory-application-proxy-enable.md) tooget les mises à jour. 

Si vous ne souhaitez pas toowait d’un connecteur de tooyour toocome mise à jour automatique, vous pouvez effectuer une mise à niveau manuelle. Accédez toohello [page de téléchargement du connecteur](https://download.msappproxy.net/subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/connector/download) sur serveur hello où votre connecteur est localisé et sélectionnez **télécharger**. Ce processus démarre, une mise à niveau pour le connecteur local de hello. 

Pour les clients avec plusieurs connecteurs, les mises à jour automatiques hello ciblent un connecteur à la fois dans chaque groupe tooprevent temps morts dans votre environnement. 

Vous pouvez rencontrer des temps d’arrêt lors de la mise à jour de votre connecteur si :  
- Vous n’avez qu’un seul connecteur. tooavoid ce temps mort et améliorer la disponibilité, nous vous recommandons d’installer un second connecteur et [créer un groupe de connecteurs](active-directory-application-proxy-connectors-azure-portal.md).  
- Un connecteur a été milieu hello d’une transaction au début de la mise à jour hello. Bien que la transaction d’origine hello est perdue, votre navigateur doit automatiquement retenter hello ou vous pouvez actualiser votre page. Lors de la demande de hello renvoyée, le trafic de hello est routé tooa connecteur de sauvegarde.

## <a name="creating-connector-groups"></a>Créer des groupe de connecteurs

Groupes de connecteurs activer des applications spécifiques tooassign des connecteurs spécifiques tooserve. Vous pouvez regrouper un nombre de connecteurs et puis affecter à chaque groupe de tooa d’application. 

Groupes de connecteurs rendent plus facile toomanage des déploiements. Ils améliorent également latence pour les clients qui ont des applications hébergées dans des régions différentes, car vous pouvez créer des groupes de basée sur l’emplacement des connecteurs tooserve des applications locales uniquement. 

toolearn savoir plus sur les groupes de connecteurs, consultez [publier des applications sur des réseaux distincts et les emplacements à l’aide de groupes de connecteurs](active-directory-application-proxy-connectors-azure-portal.md).

## <a name="security-and-networking"></a>Sécurité et mise en réseau

Connecteurs peuvent être installés n’importe où sur le réseau hello qui leur permet de service de Proxy d’Application toohello toosend demandes. L’essentiel est qu’ordinateur hello exécutant le connecteur de hello également a accès tooyour applications. Vous pouvez installer les connecteurs à l’intérieur de votre réseau d’entreprise ou sur un ordinateur virtuel qui s’exécute dans le cloud de hello. Les connecteurs peuvent s’exécuter dans une zone démilitarisée (DMZ), mais ce n’est pas nécessaire car tout le trafic est sortant afin sécuriser votre réseau.

Les connecteurs envoient uniquement des demandes sortantes. le trafic sortant de Hello est envoyé à service de Proxy d’Application toohello et toohello applications publiées. Vous n’avez pas tooopen ports d’entrée, car le trafic acheminé les deux sens, une fois qu’une session est établie. Vous n’avez tooset d’équilibrage de charge entre les connecteurs hello ou configurer l’accès entrant à travers votre pare-feu. 

Pour plus d’informations sur la configuration des règles sortantes de pare-feu, consultez [Travailler avec des serveurs proxy locaux existants](application-proxy-working-with-proxy-servers.md).

Hello d’utilisation [Azure AD Application Proxy Connector Ports Test outil](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify que votre connecteur pouvez contacter le service de Proxy d’Application hello. Au minimum, assurez-vous que toutes les coches vertes la région du centre des États-Unis hello et tooyou le plus proche de la région de hello. En outre, un nombre plus élevé de coches vertes signifie une résilience accrue. 

## <a name="performance-and-scalability"></a>Performances et évolutivité

Échelle pour hello service Proxy d’Application est transparent, mais l’échelle est un facteur de connecteurs. Vous devez toohave suffisamment connecteurs toohandle pic de trafic. Toutefois, vous n’avez pas besoin tooconfigure équilibrage de charge, car tous les connecteurs dans un groupe de connecteurs automatiquement équilibrer la charge.

Étant donné que les connecteurs sont sans état, ils ne sont pas affectés par un nombre d’utilisateurs ou des sessions hello. Au lieu de cela, ils répondent nombre toohello de demandes et de leur taille de charge utile. Avec le trafic web standard, une machine moyenne peut gérer quelques milliers de requêtes par seconde. capacité Hello dépend des caractéristiques de l’ordinateur exact hello. 

performances du connecteur Hello est lié par processeur et de mise en réseau. Performances de l’UC est nécessaire pour le chiffrement SSL et le déchiffrement, tandis que la mise en réseau est important tooget connectivité rapide toohello et applications hello en ligne dans Azure.

En revanche, la mémoire est moins problématique pour les connecteurs. service en ligne de Hello effectue une grande partie du traitement de hello et tout le trafic non authentifié. Tout ce qui peut être effectué dans le cloud de hello est effectué dans le cloud de hello. 

Un autre facteur affectant les performances est qualité hello de mise en réseau hello entre connecteurs hello, y compris : 

* **Hello service en ligne**: connexions lentes ou à latence élevée toohello service de Proxy d’Application dans les performances du connecteur Azure influence hello. Pour de meilleures performances de hello, rejoignez Express Route tooAzure de votre organisation. Sinon, demandez à votre équipe de mise en réseau de vous assurer que tooAzure connexions sont gérées aussi efficacement que possible. 
* **Hello applications principales**: dans certains cas, il existe des proxys supplémentaires entre les connecteur hello et les applications principales hello qui peuvent ralentir ou empêcher les connexions. tootroubleshoot ce scénario, ouvrez un navigateur à partir du serveur de connecteur hello et essayer tooaccess hello application. Si vous exécutez les connecteurs hello dans Azure, mais les applications hello sont locaux, expérience de hello peut-être pas ce que vos utilisateurs attendent.
* **contrôleurs de domaine de Hello**: si les connecteurs hello effectuer l’authentification unique à l’aide de la délégation contrainte Kerberos, ils contacter les contrôleurs de domaine de hello avant l’envoi de hello demande toohello principal. les connecteurs Hello ont un cache des tickets Kerberos, mais dans un environnement occupé réactivité hello hello des contrôleurs de domaine peut affecter les performances. Ce problème est plus courant pour les connecteurs qui s’exécutent dans Azure mais qui communiques avec les contrôleurs de domaine locaux. 

Pour plus d’informations sur l’optimisation de votre réseau, consultez [Considérations sur la topologie du réseau lors de l’utilisation du proxy d’application Azure Active Directory](application-proxy-network-topology-considerations.md).

## <a name="domain-joining"></a>Jonction de domaine

Les connecteurs peuvent s’exécuter sur une machine qui n’est pas jointe à un domaine. Toutefois, si vous souhaitez que seul sign-on (SSO) tooapplications qui utilisent l’authentification Windows (intégrée), vous devez un ordinateur joint au domaine. Dans ce cas, les ordinateurs de connecteur hello doivent être tooa joint à un domaine qui peut effectuer [Kerberos](https://web.mit.edu/kerberos) la délégation contrainte pour le compte utilisateurs hello pourquoi les applications publiées.

Les connecteurs peuvent également être jointes toodomains ou les forêts qui disposent d’une confiance partielle ou contrôleurs de domaine tooread uniquement.

## <a name="connector-deployments-on-hardened-environments"></a>Déploiements des connecteurs sur les environnements de sécurité renforcés

Généralement, le déploiement de connecteurs est simple et ne nécessite aucune configuration spéciale. Mais certaines conditions uniques doivent être prises en compte :

* Les organisations qui limitent le trafic sortant de hello doivent [ouvrir les ports requis](active-directory-application-proxy-enable.md#open-your-ports).
* Les ordinateurs compatibles FIPS peuvent être requis toochange leur tooallow configuration hello connecteur processus toogenerate et stocker un certificat.
* Les organisations qui verrouiller leur environnement en fonction des processus de hello que hello problème réseau des demandes ont toomake assurer que les deux services de connecteur sont les ports activé tooaccess tous requis et les adresses IP.
* Dans certains cas, les proxys de transfert sortants peuvent interrompre l’authentification de certificat bidirectionnelle hello et provoquer hello communication toofail.

## <a name="connector-authentication"></a>Authentification du connecteur

tooprovide un service sécurisé, les connecteurs ont tooauthenticate vers le service de hello, et service de hello tooauthenticate vers le connecteur de hello. Cette authentification est effectuée à l’aide de certificats client et serveur lorsque les connecteurs hello initier la connexion de hello. Nom d’utilisateur et mot de passe de l’administrateur hello de cette façon ne sont pas stockées sur l’ordinateur de connecteur hello.

les certificats de Hello utilisés sont service de Proxy d’Application toohello spécifique. Ils sont créés au cours de l’inscription initiale de hello et sont automatiquement renouvelés par les connecteurs de hello quelques mois. 

Si un connecteur n’est pas connecté service toohello depuis plusieurs mois, ses certificats peut-être être obsolète. Dans ce cas, désinstallez et réinstallez l’inscription de hello connecteur tootrigger. Vous pouvez exécuter hello suivant de commandes PowerShell :

```
Import-module AppProxyPSModule
Register-AppProxyConnector
```

## <a name="under-hello-hood"></a>Dans les coulisses de hello

Connecteurs sont basées sur le Proxy d’Application Web Windows Server, afin qu’ils puissent la plupart des hello mêmes outils de gestion, y compris les journaux des événements Windows

 ![Gérer les journaux des événements hello Observateur d’événements](./media/application-proxy-understand-connectors/event-view-window.png)

et les compteurs de performances Windows. 

 ![Ajouter le connecteur toohello de compteurs par hello Analyseur de performances](./media/application-proxy-understand-connectors/performance-monitor.png)

les connecteurs Hello ont admin et session journaux. les journaux d’administration Hello incluent leurs erreurs et les événements de touche. journaux de session de Hello incluent toutes les transactions hello ainsi que leurs informations de traitement. 

journaux de hello toosee, accédez à toohello Observateur d’événements, ouvrez hello **vue** menu et activer **afficher d’analyse et les journaux de débogage**. Ensuite, activez les toostart collecte d’événements. Ces journaux n’apparaissent pas dans le Proxy d’Application Web dans Windows Server 2012 R2, comme les connecteurs hello sont basées sur une version plus récente.

Vous pouvez examiner l’état de hello du service hello dans la fenêtre Services hello. connecteur de Hello comprend deux Services Windows : connecteur réel de hello et hello updater. Les deux doivent exécuter hello tout le temps.

 ![AzureAD Services Local](./media/application-proxy-understand-connectors/aad-connector-services.png)

## <a name="next-steps"></a>Étapes suivantes


* [Publier des applications sur des réseaux et emplacements distincts à l’aide de groupes de connecteurs](active-directory-application-proxy-connectors-azure-portal.md)
* [Travailler avec des serveurs proxy locaux existants](application-proxy-working-with-proxy-servers.md)
* [Résoudre les erreurs du proxy d’application et du connecteur](active-directory-application-proxy-troubleshoot.md)
* [Comment toosilently installer hello connecteur Proxy d’Application Azure AD](active-directory-application-proxy-silent-installation.md)

