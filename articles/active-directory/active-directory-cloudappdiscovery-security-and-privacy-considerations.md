---
title: "aaaCloud sécurité découverte et les problèmes de confidentialité | Documents Microsoft"
description: "Cette rubrique décrit la sécurité de hello et tooCloud connexes de considérations relatives à la confidentialité App Discovery."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 2fce5c82-d3de-4097-808f-40214768df9e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 33659e85bd2cf4294e443512e69a85401f7c53f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-security-and-privacy-considerations"></a>Considérations relatives à la confidentialité et à la sécurité de Cloud App Discovery
Microsoft est validée tooprotecting votre confidentialité et sécuriser vos données, tout en proposant des logiciels et services qui vous aider à gérer la sécurité hello de votre organisation.  
Nous reconnaissons que lorsque vous confiez vos tooothers de données, cette confiance exige des investissements d’ingénierie une sécurité rigoureuse et expertise tooback il.
Microsoft respecte les instructions de sécurité et de conformité de toostrict à partir de logiciels sécurisés développement du cycle de vie pratiques toooperating un service.  
La sécurisation et la protection des données constituent une priorité de premier plan pour Microsoft.

Cette rubrique explique comment les données sont recueillies, traitées et sécurisées dans Azure Active Directory Cloud App Discovery.

## <a name="overview"></a>Vue d'ensemble
Cloud App Discovery est une fonctionnalité d’Azure AD hébergée dans Microsoft Azure.  
agent de point de terminaison de Cloud App Discovery Hello est toocollect utilisé des données de découverte d’application à partir d’ordinateurs gérés.  
Hello données collectées sont envoyées en toute sécurité via un canal chiffré de toohello service Azure AD Cloud App Discovery.  
Hello, données de découverte d’application Cloud d’une organisation est ensuite visible dans hello portail Azure. 

![Fonctionnement de Cloud App Discovery](./media/active-directory-cloudappdiscovery-security-and-privacy-considerations/cad01.png) 

Bonjour sections suivantes suivent hello des flux d’informations et décrivent comment il est sécurisé lors de leur déplacement à partir de votre service de Cloud App Discovery toohello organisation et finalement portail Cloud App Discovery de toohello.

## <a name="collecting-data-from-your-organization"></a>Collecte de données de votre organisation
Dans le Cloud App discovery fonctionnalité tooget informations d’ordre toouse Azure Active Directory sur hello applications utilisées par les employés de votre organisation, vous devez toofirst déployer hello Azure AD Cloud App Discovery endpoint agent toomachines dans votre organisation.

Administrateurs du locataire d’Azure Active Directory hello (ou leur délégué) peuvent télécharger le package d’installation de l’agent de hello de hello portail Azure. l’agent de Hello peut être manuellement installé ou installé sur plusieurs ordinateurs dans l’organisation de hello à l’aide de SCCM ou la stratégie de groupe.

Pour plus d’informations sur les options de déploiement, consultez le [Guide de déploiement de Cloud App Discovery avec la stratégie de groupe](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx).


### <a name="data-collected-by-hello-agent"></a>Données collectées par l’agent de hello
Hello décrites dans la liste hello ci-dessous sont recueillies par l’agent de hello lorsqu’une connexion est établie tooa application Web. Hello informations sont collectées uniquement pour les applications qu’administrateur hello a configuré pour la découverte.  
Vous pouvez modifier la liste de hello d’applications cloud hello des analyses de l’agent via le panneau de Cloud App Discovery hello Bonjour Microsoft [portail Azure](https://portal.azure.com/), sous **paramètres**->**données Collection**->**liste de la Collection d’applications**. Pour plus d’informations, consultez la page [Prise en main de Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)


**Catégorie d’informations** : informations sur l’utilisateur  
**Description** :  
nom d’utilisateur Windows Hello du processus hello qui a effectué une application Web de la cible de toohello demande (par exemple : domaine om_utilisateur), ainsi que de hello identificateur de sécurité Windows (SID) de l’utilisateur de hello.

**Catégorie d’informations** : informations sur le processus  
**Description** :  
nom de Hello du processus de hello qui a effectué l’application Web de hello demande toohello cible (par exemple : « iexplore.exe »)

**Catégorie d’informations** : informations sur la machine  
**Description** :  
nom NetBIOS d’ordinateur Hello sur quel hello agent est installé.

**Catégorie d’informations** : Informations sur le trafic d’application  
**Description** : 

Hello les informations de connexion suivantes :

* source de Hello (ordinateur local) et les adresses IP de destination et les numéros de port
* Hello d’adresse IP d’organisation hello via le hello demande transite.
* temps de Hello de demande de hello
* volume Hello du trafic envoyé et reçu
* Hello IP version (4 ou 6)
* Pour les connexions TLS uniquement : nom d’hôte hello cible à partir de l’extension d’Indication de nom de serveur hello ou de certificat de serveur hello.

Hello les informations HTTP suivantes :

* Méthode (GET, POST, etc.)
* Protocole (HTTP/1.1, etc.)
* Chaîne d’agent utilisateur
* Nom d’hôte
* URI cible (à l’exclusion de la chaîne de requête)
* Informations de type de contenu
* Informations d’URL de point d’accès (à l’exception de la chaîne de requête)

> [!NOTE]
> Hello informations HTTP ci-dessus est collecté pour toutes les connexions non chiffrées.
> Pour les connexions TLS, ces informations sont capturées uniquement les lorsque hello « Inspection approfondie » est activé dans le portail de hello. Hello est « Activé » par défaut.
> Pour plus d’informations, consultez la section ci-dessous, ainsi que la page [Prise en main de Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)
> 
> 

En outre les données toohello que l’agent hello collecte sur l’activité réseau hello, il recueille également des informations anonymes sur la configuration matérielle et logicielle de hello, des rapports d’erreurs et des informations sur l’utilisation de l’agent de hello.


### <a name="how-hello-agent-works"></a>Fonctionne de l’agent de hello
installation de l’agent Hello comprend deux composants :

* un composant en mode utilisateur ;
* un composant de pilote en mode noyau (pilote de plateforme de filtrage Windows).

Lors de la première installation de l’agent de hello il stocke un certificat de confiance spécifiques à l’ordinateur sur l’ordinateur de hello qu’il utilise ensuite tooestablish une connexion sécurisée avec le service de Cloud App Discovery hello.  
agent de Hello extrait régulièrement la configuration de la stratégie de hello service Cloud App Discovery via cette connexion sécurisée.  
stratégie de Hello inclut plus d’informations sur le toomonitor d’applications cloud et indique si la mise à jour automatique doit être activée, entre autres choses.

Comme le trafic Web est envoyé et reçu sur l’ordinateur hello à partir d’Internet Explorer et Chrome, l’agent de découverte d’application Cloud hello analyse le trafic de hello et extraits hello métadonnées pertinentes (voir hello **les données collectées par l’agent de hello** section ci-dessus).  
Chaque minute, l’agent de hello télécharge hello collectée métadonnées toohello service Cloud App Discovery sur un canal chiffré.

Hello pilote composant intercepte hello le trafic chiffré et s’insère dans le flux de données chiffré hello. Plus de détails dans hello **interception des données à partir des connexions chiffrées (inspection approfondie)** section ci-dessous.

### <a name="respecting-user-privacy"></a>Respect de la confidentialité de l’utilisateur
Notre objectif est tooprovide administrateurs hello outils tooset hello équilibrer optiques détaillées dans confidentialité utilisateur et l’utilisation d’application en fonction de leur organisation. toothat fin, nous fournissons hello suivant des boutons de la page de paramètres hello Bonjour portail :

* **Collecte de données**: les administrateurs peuvent choisir toospecify les applications ou les catégories d’applications qu’ils souhaitent tooget les données de découverte sur.
* **Une Inspection approfondie**: les administrateurs peuvent choisir toospecify si l’agent de hello recueille le trafic HTTP pour les connexions SSL/TLS (également appelé **« Inspection approfondie »**). Plus d’informations sur cette configuration dans la section suivante de hello.
* **Options de consentement**: les administrateurs peuvent utiliser toochoose de portail Cloud App Discovery hello si les utilisateurs toonotify hello de collecte de données par l’agent hello, et si l’utilisateur de toorequire accepter avant de l’agent de hello commence la collecte de données utilisateur.

agent de point de terminaison de Cloud App Discovery Hello collecte uniquement les informations de hello décrites dans hello **les données collectées par l’agent de hello** section ci-dessus.

### <a name="intercepting-data-from-encrypted-connections-deep-inspection"></a>Interception des données à partir de connexions chiffrées (inspection approfondie)
Comme mentionné précédemment, les administrateurs peuvent configurer les données toomonitor hello l’agent à partir des connexions chiffrées (« inspection approfondie »). TLS ([Transport Layer Security](https://msdn.microsoft.com/library/windows/desktop/aa380516%28v=vs.85%29.aspx)) est un des hello protocoles les plus courants en cours d’utilisation sur Internet de hello aujourd'hui. En chiffrant la communication avec le protocole TLS, un client peut établir un canal de communication de sécurité et la confidentialité avec un serveur web. TLS offre une protection essentielle pour passer des informations d’identification de l’authentification et empêcher la divulgation d’informations sensibles hello.

Alors que le canal chiffré sécurisé à bout en bout de hello fourni par TLS permet important de la sécurité et la protection des données, protocole de hello est fréquente à des fins malveillantes ou malveillant. En fait, que TLS est souvent donc beaucoup visés tooas hello « contournement de pare-feu universal protocol ». racine Hello de problème de hello est que la plupart des pare-feu sont communication TLS de tooinspect impossible, car les données de la couche de l’application hello sont chiffrées avec SSL. Sachant cela, des personnes malveillantes exploitent fréquemment certain même hello plus intelligents pare-feu applicatifs sont totalement invisible tooTLS et doivent simplement relayer les communications TLS entre les hôtes d’utilisateur de tooa du malveillants toodeliver TLS. Les utilisateurs finaux fréquemment tirer parti des contrôles d’accès TLS toobypass appliquées par leur pare-feu d’entreprise et les serveurs proxy, l’utiliser tooconnect toopublic proxys et pour le tunneling de protocoles non-TLS à travers le pare-feu hello qui risque d’être bloqué par la stratégie.

Une inspection approfondie permet hello Cloud App Discovery agent tooact comme une confiance man-in-the-middle. Lorsqu’une demande du client est effectuée tooaccess HTTPS une ressource protégée, pilote de l’Agent de point de terminaison hello intercepte les connexion hello et établit un nouveau serveur tooretrieves connexion toohello destination son certificat SSL pour le compte client de hello. l’agent de Hello vérifie ensuite que les certificats hello peuvent être approuvés (par la vérification qu’il n’a pas été révoqué et effectuer d’autres vérifications de certificats), et si ces tests, hello Agent de point de terminaison, puis copie les informations de hello du certificat de serveur hello et crée sa propre certificat de serveur--appelé un certificat de l’interception--à l’aide de ces informations. certificat de l’interception de Hello est signé à la volée par l’agent de point de terminaison hello avec un certificat racine, qui est installé dans le magasin de certificats approuvés Windows hello. Ce certificat racine auto-signé est marqué comme non exportable et ACL avait tooadministrators. C’est prévu toonever laissez hello machine sur laquelle il a été créé. Lors de l’application cliente de hello-l’utilisateur final reçoit le certificat de l’interception de hello, il sera l’approbation, car il peut valider correctement la chaîne de certificats hello tous les certificats racine de hello moyen toohello. Ce processus, qui est pour l’essentiel transparent du point de vue de l'utilisateur final, présente quelques inconvénients, comme décrit ci-dessous.

En activant une inspection approfondie, hello Cloud App Discovery Endpoint Agent peut déchiffrer et inspecter les communications TLS chiffré, ce qui permet de bruit de tooreduce service hello et fournir des informations sur l’utilisation de hello hello chiffré des applications de cloud.

#### <a name="a-word-of-caution"></a>Avertissement
Avant d’activer une inspection approfondie, il est fortement recommandé que vous communiquer vos tooyour intentions légal et les départements des ressources humaines et obtenez leur consentement. L’inspection des communications chiffrées privées de l’utilisateur final peut être un sujet sensible pour des raisons évidentes. Avant une restauration montée de production d’une inspection approfondie, assurez-vous que la sécurité de votre entreprise et les stratégies d’utilisation acceptable ont été mis à jour tooindicate qui communication chiffrée est recherchée. Notification utilisateur et exemption de sites données sensibles (par exemple, bancaires et médicales sites) peuvent également s’avérer nécessaires si vous configurez la découverte d’application Cloud toomonitor les. Comme indiqué ci-dessus, les administrateurs peuvent utiliser les toochoose de portail Cloud App Discovery hello indique si les utilisateurs toonotify hello de collecte de données par l’agent hello, et si l’utilisateur de toorequire accepter avant de l’agent de hello commence la collecte de données utilisateur.

### <a name="known-issues-and-drawbacks"></a>Problèmes connus et inconvénients
Il existe quelques cas où l’interception de TLS peut avoir un impact sur l’expérience utilisateur hello :

* Étendue certificats EV (Validation) rendu barre d’adresses hello de hello web navigateur vert tooact comme un indice visuel que vous visitez un site web de confiance. Inspection de TLS ne peut pas dupliquer EV certificat hello qu’elle émet toohello client, pour les sites web qui utilisent des certificats EV fonctionne normalement mais barre d’adresses hello n’affichera pas vert.  
* Public épinglage clés (également connu comme l’épinglage de certificat) sont conçus toohelp utilisateurs contre les attaques de man-in-the-middle et non autorisés d’autorités de certification. Lorsque le certificat racine de hello pour un site épinglé ne correspond pas à un des hello connu de l’autorité de certification bon, le navigateur de hello rejette connexion hello avec une erreur. Comme l'interception TLS est en fin de compte un intercepteur, ces connexions échouent.
* Si les utilisateurs cliquent sur l’icône de verrou de hello dans les informations de site hello barre navigateur tooinspect hello navigateur adresse, ils verront pas une chaîne se terminant par une autorité de certification hello utilisé le certificat de site Web toosign hello, mais à la place une chaîne de certificats se terminant par hello Windows magasin de certificats approuvés.

occurrences de hello tooreduce de ces problèmes, nous assurer le suivi des services de cloud computing et les applications clientes connues toouse étendues validation ou l’épinglage de clé publique et demander des tooavoid de l’Agent de point de terminaison hello interception des connexions concernées. Même dans ce cas, toutefois, vous continuerez à recevoir des rapports utilisez hello de ces applications cloud et le volume hello de données transférées, mais qui ne sont pas approfondies inspecté, pas plus d’informations sur l’utilisation des applications de hello ont été seront disponibles.

## <a name="sending-data-toocloud-app-discovery"></a>Envoi de données tooCloud App Discovery
Une fois que les métadonnées ont été collectées par l’agent de hello, il est mis en cache sur l’ordinateur hello pour les tooone minute ou jusqu'à ce que hello les données mises en cache atteignent une taille de 5 Mo. Elles sont ensuite compressées et envoyée via une connexion sécurisée de toohello service Cloud App Discovery.

Si l’agent de hello est toocommunicate impossible avec hello service Cloud App Discovery pour une raison quelconque, hello métadonnées collectées sont stockées dans un cache de fichiers local qui est accessible par les utilisateurs disposant de privilèges sur l’ordinateur hello (par exemple, le groupe d’administrateurs hello).  
l’agent de Hello automatiquement tentatives tooresend hello métadonnées mises en cache jusqu'à ce qu’il a été correctement reçu par le service de Cloud App Discovery hello.

## <a name="receiving-hello-data-at-hello-service-end"></a>Recevoir des données à la fin du service hello hello
les agents Hello authentifient toohello Cloud App Discovery service à l’aide du certificat d’authentification client spécifique hello ordinateur évoqué ci-dessus et transfère les données sur un canal chiffré.  
analytique du service de Cloud App Discovery Hello pipeline des métadonnées de processus pour chaque client séparément en les partitionnant logiquement à toutes les étapes du pipeline d’analytique hello.
Hello analysés hello de lecteurs de métadonnées différents rapports dans le portail de hello.

Hello des métadonnées non traitées et les métadonnées hello analysée sont stockées pour too180 jours. En outre, les clients peuvent choisir toocapture hello analysée métadonnées dans un compte de stockage d’objets blob Azure de leur choix.
Cela est utile pour l’analyse hors ligne des métadonnées ainsi que la conservation à longue terme des données de hello.

## <a name="accessing-hello-data-using-hello-azure-portal"></a>L’accès aux données hello à l’aide de hello portail Azure
Métadonnées de hello tookeep d’effort collectées sécurisée, par défaut seuls les administrateurs globaux du client de hello ont fonctionnalité Cloud App Discovery de toohello accès Bonjour portail Azure.  
Toutefois, les administrateurs peuvent choisir toodelegate cet accès tooother utilisateurs ou des groupes.

> [!NOTE]
> Pour plus d’informations, consultez la page [Prise en main de Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)
> 
> 


Toutes les données de hello utilisateur l’accès au portail hello doit être titulaire d’une licence Azure AD Premium.

## <a name="additional-resources"></a>Ressources supplémentaires
* [Comment puis-je détecter les applications cloud non approuvées utilisées au sein de mon organisation ?](active-directory-cloudappdiscovery-whatis.md)
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)

