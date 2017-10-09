---
title: "Considérations relatives à l’aaaSecurity pour le Proxy d’Application Azure AD | Documents Microsoft"
description: "Couvre les considérations de sécurité lors de l’utilisation du proxy d’application Azure AD"
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
ms.openlocfilehash: ebd14b9d1fc8f4629c5916e5a910595727d935d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="security-considerations-for-accessing-apps-remotely-with-azure-ad-application-proxy"></a>Considérations de sécurité pour l’accès aux applications à distance avec le proxy d’application Azure AD

Cet article explique comment le proxy d’application Azure Active Directory fournit un service sécurisé pour la publication et l’accès à distance de vos applications.

Hello ci-dessous diagramme illustre comment Azure AD permet de sécuriser l’accès à distance tooyour des applications locales.

 ![Diagramme illustrant l’accès sécurisé à distance via le proxy d’application Azure AD](./media/application-proxy-security-considerations/secure-remote-access.png)

## <a name="security-benefits"></a>Avantages en matière de sécurité

Proxy d’Application Azure AD offre hello avantages de sécurité suivants :

### <a name="authenticated-access"></a>Accès authentifié 

Si vous choisissez toouse Azure Active Directory la pré-authentification, uniquement les connexions authentifiées peuvent accéder à votre réseau.

Proxy d’Application Azure AD s’appuie sur hello AD Azure service jeton de sécurité (STS) pour toutes les authentifications.  La pré-authentification, par sa nature, bloque un nombre important d’attaques anonymes, uniquement les identités authentifiées pouvant accéder à l’application principale de hello.

Si vous choisissez Passthrough comme méthode de préauthentification, vous ne bénéficiez pas de cet avantage. 

### <a name="conditional-access"></a>Accès conditionnel

Appliquer des contrôles de stratégie plus riches avant tooyour réseau sont établies les connexions.

Avec [accès conditionnel](active-directory-conditional-access-azuread-connected-apps.md), vous pouvez définir des restrictions sur le trafic est autorisé à tooaccess vos applications principales. Vous pouvez créer des stratégies qui limitent les connexions en fonction de l’emplacement, de la force de l’authentification et du profil de risque de l’utilisateur.

Vous pouvez également utiliser les stratégies d’authentification multifacteur tooconfigure accès conditionnel en ajoutant une autre couche d’authentification de sécurité tooyour utilisateur. 

### <a name="traffic-termination"></a>Arrêt du trafic

Tout le trafic est arrêté dans le cloud de hello.

Étant donné que le Proxy d’Application Azure AD est un proxy inverse, toutes les applications de tooback-end du trafic se termine au niveau de service de hello. Hello session peut obtenir rétablie uniquement avec le serveur principal de hello, ce qui signifie que vos serveurs principaux ne sont pas exposées toodirect HTTP du trafic. Cette configuration signifie que vous êtes mieux protégé contre les attaques ciblées.

### <a name="all-access-is-outbound"></a>Tous les accès sont sortants 

Vous n’avez pas besoin réseau de l’entreprise toohello tooopen les connexions entrantes.

Connecteur de Proxy d’application utilisent uniquement le service de Proxy d’Application les connexions sortantes toohello Azure AD, ce qui signifie qu’il est inutile tooopen des ports de pare-feu pour les connexions entrantes. Proxys traditionnels requis d’un réseau de périmètre (également appelé *DMZ*, *zone démilitarisée*, ou *sous-réseau filtré*) et autorisés l’accès toounauthenticated connexions en périphérie du réseau hello. Ce scénario requis nombreux investissement supplémentaire dans l’application web le trafic tooanalyze de produits de pare-feu et offre addition protections toohello environnement. Avec le proxy d’application, vous pouvez même vous passer de réseau de périmètre, car toutes les connexions sont sortantes et sur un canal sécurisé.

Pour plus d’informations sur les connecteurs, consultez [Présentation des connecteurs de proxy d’application Azure AD](application-proxy-understand-connectors.md).

### <a name="cloud-scale-analytics-and-machine-learning"></a>Analyse à l’échelle du cloud et apprentissage automatique 

Bénéficiez d’une protection de sécurité de pointe.

Car il fait partie d’Azure Active Directory, le Proxy d’Application peut tirer parti de [Azure AD Identity Protection](active-directory-identityprotection.md), avec intelligence contrôlée par l’apprentissage automatique d’ordinateur et les données à partir de Microsoft Security Response Center de hello et Digital Crimes Unit. Ensemble, nous identifions de façon proactive les comptes compromis et offrons une protection en temps réel contre les connexions à haut risque. Nous prenons en compte divers facteurs, dont l’accès à partir d’appareils infectés et à travers des réseaux anonymes, ainsi qu’à partir d’emplacements atypiques et peu probables.

Nombre de ces rapports et événements sont déjà disponibles via une API pour l’intégration avec vos systèmes de gestion des événements et des informations de sécurité.

### <a name="remote-access-as-a-service"></a>Accès à distance en tant que service

Vous n’avez pas tooworry sur la gestion et la mise à jour corrective sur des serveurs locaux.

Les logiciels sans correctifs sont toujours responsables d’un grand nombre d’attaques. Proxy d’Application Azure AD est un service de l’échelle de l’Internet détenues par Microsoft, afin de toujours obtenir les derniers correctifs de sécurité hello et les mises à niveau.

sécurité de hello tooimprove des applications publiées par le Proxy d’Application Azure AD, nous bloquons robots de robot web à partir de l’indexation et l’archivage de vos applications. Chaque fois qu’un robot web tente de récupérer les paramètres de robots d’une application publiée, le proxy d’application répond avec un fichier robots.txt qui inclut `User-agent: * Disallow: /`.

## <a name="under-hello-hood"></a>Dans les coulisses de hello

Le proxy d’application Azure Active Directory se compose de deux parties :

* services de cloud computing de Hello : ce service s’exécute dans Azure et est l’endroit de connexions de client / l’utilisateur externe hello.
* [Hello connecteur local](application-proxy-understand-connectors.md): un composant de local, le connecteur de hello écoute les demandes de service de Proxy d’Application hello Azure AD et gère les applications internes toohello de connexions. 

Un flux de connecteur de hello et le service de Proxy d’Application hello est établi lorsque :

* connecteur de Hello est tout d’abord configurer.
* connecteur de Hello extrait les informations de configuration de hello service Proxy d’Application.
* Un utilisateur accède à une application publiée.

>[!NOTE]
>Toutes les communications se produisent sur le protocole SSL, et ils proviennent toujours hello connecteur toohello service Proxy d’Application. service de Hello est sortant uniquement.

connecteur de Hello utilise un toohello tooauthenticate du certificat client service de Proxy d’Application pour presque tous les appels. Hello uniquement exception toothis processus est étape de la configuration initiale de hello, où le certificat de client hello est établie.

### <a name="installing-hello-connector"></a>L’installation du connecteur de hello

Lorsque le connecteur de hello est définissez tout d’abord, hello après le transfert d’événements ont lieu :

1. service de toohello Hello connecteur d’enregistrement se produit dans le cadre de l’installation de hello du connecteur de hello. Les utilisateurs est invités à tooenter leurs informations d’identification administrateur de Azure AD. Le jeton obtenu à partir de cette authentification est ensuite présenté service de Proxy d’Application Azure AD toohello.
2. Hello service Proxy d’Application évalue le jeton de hello. Elle garantit que l’utilisateur hello est un administrateur d’entreprise au sein de client de hello hello jeton a été émis pour. Si l’utilisateur de hello n’est pas un administrateur, le processus de hello est arrêtée.
3. connecteur de Hello génère une demande de certificat client et le passe, ainsi que de toohello de jeton, hello service Proxy d’Application. service de Hello à son tour vérifie le jeton de hello et signe la demande de certificat de client hello.
4. connecteur de Hello utilise un certificat de client hello pour les communications futures avec hello service Proxy d’Application.
5. connecteur de Hello effectue une extraction initiale des données de configuration du système hello service hello à l’aide de son certificat de client, et il est maintenant prêt tootake demandes.

### <a name="updating-hello-configuration-settings"></a>Mise à jour des paramètres de configuration hello

Chaque fois que hello service Proxy d’Application des mises à jour les paramètres de configuration hello, hello après le transfert d’événements ont lieu :

1. connecteur de Hello connecte de point de terminaison de configuration toohello dans hello service Proxy d’Application à l’aide de son certificat de client.
2. Après la validation de certificat de client hello, hello service Proxy d’Application retourne le connecteur de toohello de données de configuration (par exemple, groupe de connecteur hello hello connecteur doit être partie).
3. Si le certificat actuel hello est plus de 180 jours, le connecteur de hello génère une demande de certificat, laquelle efficacement met à jour les certificats de client hello tous les 180 jours.

### <a name="accessing-published-applications"></a>Accès aux applications publiées

Lorsque les utilisateurs accèdent à une application publiée, hello événements suivants se produisent entre le service de Proxy d’Application hello et le connecteur de Proxy d’Application hello :

1. [service de Hello authentifie l’utilisateur hello pour une application hello](#the-service-checks-the-configuration-settings-for-the-app)
2. [service de Hello place une demande dans la file d’attente du connecteur hello](#The-service-places-a-request-in-the-connector-queue)
3. [Un connecteur traite la demande hello à partir de la file d’attente hello](#the-connector-receives-the-request-from-the-queue)
4. [connecteur de Hello attend une réponse](#the-connector-waits-for-a-response)
5. [utilisateur Hello flux données toohello](#the-service-streams-data-to-the-user)

toolearn en savoir plus sur ce qui se passe dans chacune de ces étapes, conserver la lecture.


#### <a name="1-hello-service-authenticates-hello-user-for-hello-app"></a>1. service de hello authentifie utilisateur hello pour une application hello

Si vous avez configuré hello application toouse relais en tant que sa méthode de pré-authentification, étapes hello dans cette section sont ignorés.

Si vous avez configuré hello application toopreauthenticate avec Azure AD, les utilisateurs sont redirigé toohello tooauthenticate de STS Azure AD et hello étapes suivantes ont lieu :

1. Vérification du Proxy d’application pour des exigences de stratégie d’accès conditionnel pour application hello. Cette étape garantit que toohello application a été affecté à cet utilisateur hello. Si la vérification en deux étapes est nécessaire, la séquence d’authentification hello demande utilisateur hello une deuxième méthode d’authentification.

2. Une fois que toutes les vérifications ont réussi, hello Azure AD STS émet un jeton signé pour l’application hello et redirections hello toohello arrière d’utilisateur service Proxy d’Application.

3. Le Proxy d’application vérifie que ce jeton hello a été émis application hello de toocorrect. Il effectue également les autres contrôles, tels que vous être assuré que hello jeton a été signé par Azure AD et qu’il est toujours dans la fenêtre valide hello.

4. Le Proxy d’application définit un tooindicate de cookie d’authentification chiffré qui application toohello de l’authentification s’est produite. Hello cookie inclut un horodatage d’expiration qui est basé sur le jeton hello d’Azure AD et d’autres données, comme le nom d’utilisateur hello hello d’authentification est basée sur. cookie de Hello est chiffré avec une clé privée est connue uniquement toohello service Proxy d’Application.

5. Application Proxy redirections hello utilisateur précédent toohello les URL initialement demandée.

Si une partie des étapes de la pré-authentification hello échoue, demande de l’utilisateur hello est refusé et utilisateur de hello s’affiche un message indiquant la source hello problème de hello.


#### <a name="2-hello-service-places-a-request-in-hello-connector-queue"></a>2. service de hello place une demande dans la file d’attente du connecteur hello

Connecteurs de conserver un toohello ouvrir de connexion sortante service Proxy d’Application. Lorsqu’une demande arrive, service de hello des files d’attente demande hello sur l’une des connexions ouvertes de hello pour toopick de connecteur hello haut.

demande de Hello inclut des éléments à partir de l’application hello, tels que les en-têtes de demande hello, les données à partir du cookie de hello chiffré, hello utilisateur qui demande de hello et hello ID de la demande Bien que les données à partir du cookie chiffré de hello sont envoyées avec la demande de hello, cookie d’authentification hello lui-même n’est pas.

#### <a name="3-hello-connector-processes-hello-request-from-hello-queue"></a>3. hello connecteur processus hello demande à partir de la file d’attente hello. 

En fonction de la demande de hello, le Proxy d’Application effectue l’une des hello suivant des actions :

* Si la demande de hello est une opération simple (par exemple, il n’existe aucune donnée dans le corps de hello en l’état avec un RESTful *obtenir* demande), connecteur de hello, une ressource interne de connexion toohello cible et puis attend une réponse.

* Si la demande de hello a des données associées dans le corps de hello (par exemple, un RESTful *POST* opération), connecteur de hello établit une connexion sortante à l’aide d’instance du Proxy d’Application hello client certificat toohello. Il met connexion toorequest hello et ouvrir une ressource interne toohello de connexion. Après avoir reçu la demande de hello connecteur de hello, service de Proxy d’Application hello commence à accepter le contenu à partir de l’utilisateur de hello et transmet le connecteur toohello de données. connecteur de Hello, transfère à son tour, les ressources internes du toohello données hello.

#### <a name="4-hello-connector-waits-for-a-response"></a>4. connecteur de hello attend une réponse.

Une fois la demande de hello et transmission de contenu toohello dans fin terminée, le connecteur de hello attend une réponse.

Après avoir reçu une réponse, connecteur de hello rend un service de Proxy d’Application toohello connexion sortante, tooreturn hello les détails de l’en-tête et commencer la diffusion en continu de données de retour hello.

#### <a name="5-hello-service-streams-data-toohello-user"></a>5. hello flux données toohello utilisateur. 

Une partie du traitement de l’application hello peut se produire ici. Si vous avez configuré les URL ou les en-têtes de tootranslate le Proxy d’Application dans votre application, que le traitement se produit en fonction des besoins au cours de cette étape.


## <a name="next-steps"></a>Étapes suivantes

[Considérations sur la topologie du réseau lors de l’utilisation du proxy d’application Azure AD](application-proxy-network-topology-considerations.md)

[Présentation des connecteurs de proxy d’application Azure AD](application-proxy-understand-connectors.md)
