---
title: aaaUsing Azure AD Connect Health avec AD FS | Documents Microsoft
description: Voici hello Azure AD Connect Health page Comment toomonitor votre site infrastructure AD FS.
services: active-directory
documentationcenter: 
author: karavar
manager: femila
editor: curtand
ms.assetid: dc0e53d8-403e-462a-9543-164eaa7dd8b3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0cd26e8762be65e09d22e1f113e5165c4f131715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-ad-fs-using-azure-ad-connect-health"></a>Surveiller AD FS avec Azure AD Connect Health
Hello suite la documentation est toomonitoring spécifique de votre infrastructure AD FS avec Azure AD Connect Health. Pour plus d’informations sur la surveillance de la synchronisation Azure AD Connect avec Azure AD Connect Health, consultez [Utilisation d’Azure AD Connect Health pour la synchronisation](active-directory-aadconnect-health-sync.md). En outre, pour plus d’informations sur la surveillance des services de domaine Active Directory avec Azure AD Connect Health, consultez [Utilisation d’Azure AD Connect Health avec AD DS](active-directory-aadconnect-health-adds.md).

## <a name="alerts-for-ad-fs"></a>Alertes pour AD FS
Hello section d’alertes Azure AD Connect d’intégrité fournit que Hello de la liste des alertes actives. Chaque alerte inclut des informations pertinentes, les étapes de résolution et la documentation de toorelated de liens.

Vous pouvez double-cliquer sur une tooopen alerte, actif ou résolu un nouveau panneau avec des informations supplémentaires, procédez comme suit tooresolve hello alerte et la documentation de toorelevant des liens. Vous pouvez également afficher les données d’historique des alertes qui ont été résolus dans hello passée.

![portail Azure AD Connect Health](./media/active-directory-aadconnect-health/alert2.png)

## <a name="usage-analytics-for-ad-fs"></a>Analyse de l’utilisation pour AD FS
Azure AD se connecter d’intégrité d’utilisation Analytique analyse le trafic d’authentification hello de vos serveurs de fédération. Vous pouvez double-cliquer sur boîte analytique de l’utilisation hello, tooopen hello analytique Panneau de l’utilisation, qui vous montre plusieurs mesures et les regroupements.

> [!NOTE]
> toouse Analytique d’utilisation avec AD FS, vous devez vous assurer que l’audit AD FS est activée. Pour plus d’informations, consultez [Activer l’audit pour AD FS](active-directory-aadconnect-health-agent-install.md#enable-auditing-for-ad-fs).
>
>

![portail Azure AD Connect Health](./media/active-directory-aadconnect-health/report1.png)

tooselect des métriques supplémentaires, spécifier un intervalle de temps ou un regroupement de hello toochange, avec le bouton droit sur le graphique de l’utilisation d’analytique hello et sélectionnez Modifier le graphique. Vous pouvez ensuite spécifier la plage de temps hello, sélectionner une autre mesure et modifier hello regroupement. Vous pouvez afficher la distribution hello hello du trafic d’authentification basée sur les différentes « mesures » et regrouper chaque mesure à l’aide de paramètres de « regrouper par » pertinents décrits dans hello suivant la section :

**Métrique : Nombre total de demandes** : nombre total de demandes traitées par les serveurs AD FS.

|Regroupement | Ce que signifie regroupement de hello et pourquoi il est utile ? |
| --- | --- |
| Tout | Affiche le nombre hello du nombre total de demandes traitées par tous les serveurs AD FS.|
| Application | Groupes hello nombre total de demandes en fonction de partie de confiance hello ciblé. Ce regroupement est utile toounderstand quelle application reçoit le pourcentage du total du trafic hello. |
|  Serveur |Groupes hello nombre total de demandes en fonction de serveur hello qui a traité hello demande. Ce regroupement est la distribution de la charge utile toounderstand hello du trafic total de hello.
| Jonction d’espace de travail |Groupes hello nombre total de demandes selon si elles proviennent des périphériques rattachés (connu). Ce regroupement est utile toounderstand si vos ressources sont accessibles à l’aide d’appareils qui sont l’infrastructure d’identité toohello inconnu. |
|  Méthode d'authentification | Groupes hello nombre total de demandes en fonction de la méthode d’authentification hello utilisé pour l’authentification. Ce regroupement est utile toounderstand hello méthode d’authentification commune utilisée pour l’authentification. Voici les méthodes d’authentification possibles de hello <ol> <li>Authentification Windows intégrée (Windows)</li> <li>Authentification basée sur les formulaires (Formulaires)</li> <li>SSO (Authentification unique)</li> <li>Authentification par certificat X509 (Certificat)</li> <br>Si les serveurs de fédération hello réception demande hello avec un Cookie d’authentification unique, cette demande est comptabilisée comme authentification (authentification unique). Dans ce cas, si le cookie de hello est valide, utilisateur de hello n’est pas invité tooprovide d’informations d’identification et obtient un accès transparent toohello application. Ce comportement est courant si vous avez plusieurs parties de confiance protégées par les serveurs de fédération hello. |
| Emplacement réseau | Groupes hello nombre total de demandes basé sur l’emplacement de réseau hello d’utilisateur de hello. Il peut s’agir d’un réseau intranet ou extranet. Ce regroupement est utile tooknow quel pourcentage du trafic de hello provient d’intranet hello ou extranet. |


**Métrique : Total échecs de requête** -nombre total de hello demandes ayant échoué traitées par le service de fédération hello. (Cette métrique est disponible uniquement sur AD FS pour Windows Server 2012 R2)

|Regroupement | Ce que signifie regroupement de hello et pourquoi il est utile ? |
| --- | --- |
| Type d’erreur | Montre le nombre hello d’erreurs selon les types d’erreur prédéfinies. Ce regroupement est utile toounderstand hello courants d’erreurs. <ul><li>Incorrect nom d’utilisateur ou mot de passe : erreurs en raison de mot de passe ou nom d’utilisateur tooincorrect.</li> <li>« Le verrouillage extranet » : échecs en raison de demandes toohello reçus d’un utilisateur qui a été verrouillé depuis l’extranet </li><li> « Le mot de passe expiré » : échecs en raison de la journalisation toousers avec un mot de passe a expiré.</li><li>« Disabled compte » : échecs en raison de la journalisation de toousers avec un compte désactivé.</li><li>« Authentification de l’appareil » : échecs d’échéance tooauthenticate toousers défectueux à l’aide de l’authentification des appareils.</li><li>« Authentification de certificat utilisateur » : échecs d’échéance tooauthenticate toousers défectueux en raison d’un certificat non valide.</li><li>« L’authentification Multifacteur » : échecs d’échéance tooauthenticate toouser défectueux à l’aide de l’authentification multifacteur.</li><li>« Autres informations d’identification » : « Autorisation d’émission » : échecs en raison d’échecs de tooauthorization.</li><li>« Délégation d’émission » : échecs en raison d’erreurs de délégation tooissuance.</li><li>« Acceptation de jeton » : échecs en raison du rejet de tooADFS hello jeton à partir d’un fournisseur d’identité tiers.</li><li>« Protocol » : échec en raison d’erreurs de tooprotocol.</li><li>« Inconnu » : intercepte tout. Toutes les autres erreurs qui ne tiennent pas dans hello défini par catégories.</li> |
| Serveur | Groupes hello erreurs basés sur le serveur de hello. Ce regroupement est la distribution d’erreur toounderstand utile hello entre serveurs. Une distribution inégale peut indiquer qu’un serveur présente un état défectueux. |
| Emplacement réseau | Groupes hello erreurs basés sur l’emplacement de réseau hello de demandes de hello (intranet et extranet). Ce regroupement est de type hello de toounderstand utile de demandes qui ont échoué. |
|  Application | Groupes hello échecs en fonction de l’application hello ciblé (partie de confiance). Ce regroupement est utile toounderstand quelle application ciblée voit au nombre d’erreurs. |

**Métrique : Nombre d’utilisateurs** : nombre moyen d’utilisateurs uniques qui utilisent activement l’authentification AD FS

|Regroupement | Ce que signifie regroupement de hello et pourquoi il est utile ? |
| --- | --- |
|Tout |Cette mesure indique le nombre du nombre moyen d’utilisateurs à l’aide du service de fédération hello dans la tranche de temps sélectionnée hello. les utilisateurs de Hello ne sont pas regroupées. <br>moyenne de Hello dépend de la tranche de temps hello sélectionnée. |
| Application |Nombre moyen de hello groupes d’utilisateurs en fonction de hello cible application (partie de confiance). Ce regroupement est utile toounderstand combien d’utilisateurs est à l’aide de l’application. |

## <a name="performance-monitoring-for-ad-fs"></a>Surveillance des performances pour AD FS
L’analyse des performances Azure AD Connect Health fournit des informations d’analyse sur les mesures. Sélection de zone de surveillance hello, s’ouvre un nouveau panneau avec des informations détaillées sur les métriques hello.

![portail Azure AD Connect Health](./media/active-directory-aadconnect-health/perf1.png)

En sélectionnant l’option de filtre hello haut hello du Panneau de hello, vous pouvez filtrer par serveur toosee les métriques d’un serveur individuel. métrique de toochange, avec le bouton droit sur le graphique sous hello panneau d’analyse de surveillance de hello et sélectionnez Modifier le graphique (ou bouton Modifier le graphique de hello select). À partir de hello nouveau panneau qui s’ouvre, vous pouvez sélectionner des mesures supplémentaires dans hello de liste déroulante et spécifier une plage de temps pour l’affichage des données de performances hello.

## <a name="reports-for-ad-fs"></a>Rapports pour AD FS
Azure AD Connect Health fournit des rapports sur l’activité et les performances des services AD FS. Ces rapports aident les administrateurs à obtenir des informations sur les activités sur leurs serveurs AD FS.

### <a name="top-50-users-with-failed-usernamepassword-logins"></a>Les 50 utilisateurs dont la combinaison nom d’utilisateur/mot de passe échoue le plus souvent.
Une des raisons courantes de hello pour une demande d’authentification a échoué sur un serveur AD FS est une demande avec les informations d’identification non valides, autrement dit, un nom d’utilisateur incorrect ou le mot de passe. Se produit généralement toousers en raison des fautes de frappe, les mots de passe oubliés ou toocomplex des mots de passe.

Mais il existe d’autres raisons pouvant entraîner un nombre inattendu de demandes traitées par vos serveurs AD FS, telles que : une application qui les informations d’identification utilisateur de caches et les informations d’identification hello expirent ou un utilisateur malveillant qui toosign à un compte avec une série de mots de passe connus. Ces deux exemples sont des raisons valables qui pourrait provoquer tooa brusque dans les demandes.

Azure AD Connect Health pour AD FS fournit un rapport sur les utilisateurs de 50 premiers avec des tentatives de connexion ayant échoué en raison de mot de passe ou nom d’utilisateur tooinvalid. Ce rapport est obtenu par le traitement des événements d’audit hello générés par tous les serveurs hello AD FS dans les batteries de hello

![portail Azure AD Connect Health](./media/active-directory-aadconnect-health-adfs/report1a.png)

Dans ce rapport, vous avez toohello un accès facile suivant d’éléments d’information :

* Nombre total d’échecs de demandes avec le nom d’utilisateur/mot de passe incorrect Bonjour 30 derniers jours
* Nombre moyen d’utilisateurs dont la connexion a échoué en raison d’un nom d’utilisateur/mot de passe incorrect par jour.

En cliquant sur cette partie prend de panneau rapport principal toohello qui fournit des détails supplémentaires. Ce panneau comprend un graphique avec toohelp établir une ligne de base sur les requêtes avec un nom d’utilisateur incorrect ou le mot de passe des informations d’analyse de tendances. En outre, il fournit liste hello de 50 utilisateurs avec numéro hello de tentatives ayant échoué.

graphique de Hello fournit hello informations suivantes :

* Bonjour nombre total d’échecs de connexion en raison de tooa nom d’utilisateur/mot de passe incorrect sur une base par jour.
* Bonjour nombre total d’utilisateurs uniques qui les échecs de connexion sur une base par jour.
* Adresse IP du client pour la dernière demande

![portail Azure AD Connect Health](./media/active-directory-aadconnect-health-adfs/report3a.png)

rapport de Hello fournit hello informations suivantes :

| Élément de rapport | Description |
| --- | --- |
| ID d'utilisateur |Affiche l’ID hello qui a été utilisée. Cette valeur est le hello utilisateur typée, qui, dans certains cas, est hello ID d’utilisateur incorrect utilisé. |
| Tentatives ayant échoué |Affiche hello nombre total d’échecs de tentative pour cet ID d’utilisateur spécifique. tableau de Hello est trié par hello plus nombre de tentatives ayant échoué dans l’ordre décroissant. |
| Dernier échec |Affiche l’horodatage hello lors du dernier échec d’hello. |
| IP du dernier échec |Affiche l’adresse IP du Client de hello à partir de la demande incorrecte de hello plus récente. |

> [!NOTE]
> Ce rapport est mis automatiquement à jour une fois que toutes les deux heures par hello nouvelles informations collectées pendant ce délai. Par conséquent, tentatives de connexion dans les deux dernières heures de hello peuvent ne pas figurer dans le rapport de hello.
>
>

## <a name="related-links"></a>Liens connexes
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Installation de l'agent Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Opérations Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Utilisation d'Azure AD Connect Health pour la synchronisation (en Anglais)](active-directory-aadconnect-health-sync.md)
* [Utilisation d’Azure AD Connect Health avec AD DS](active-directory-aadconnect-health-adds.md)
* [Forum Aux Questions (FAQ) Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Historique de publication des versions d’Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)