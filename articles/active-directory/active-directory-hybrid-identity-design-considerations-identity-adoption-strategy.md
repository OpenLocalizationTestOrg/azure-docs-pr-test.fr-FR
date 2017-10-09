---
title: "Considérations de conception pour les identités hybrides aaaAzure Active Directory - définir une stratégie d’adoption identité hybride | Documents Microsoft"
description: "Avec le contrôle d’accès conditionnel, Azure Active Directory vérifie les conditions spécifiques hello que vous choisissez lors de l’authentification utilisateur de hello et avant d’autoriser l’accès toohello application. Lorsque ces conditions sont réunies, hello utilisateur authentifié et autorisé accès toohello application."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: b92fa5a9-c04c-4692-b495-ff64d023792c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 9ffca675d0c714392adfcbbc4dcfad12fccbac78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="define-a-hybrid-identity-adoption-strategy"></a>Définir une stratégie d’adoption des identités hybrides
Dans cette tâche, vous allez définir la stratégie d’adoption identité hello hybride pour hybride identité solution toomeet hello besoins de votre entreprise qui ont été présentés dans :

* [Déterminer les besoins métier](active-directory-hybrid-identity-design-considerations-business-needs.md)
* [Déterminer les exigences de synchronisation de répertoire](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)
* [Déterminer les exigences d’authentification multifacteur](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="define-business-needs-strategy"></a>Définir une stratégie de besoins métier
tâche première Hello déterminant hello organisations à leurs besoins.  Cette opération peut être très étendue et vous risquez de vous éloigner des objectifs si vous n’êtes pas prudent.  Début de hello plus de simplicité, mais n’oubliez pas toujours des tooplan pour une conception à prendre en compte et faciliter la modification de hello futures.  Qu’il s’agisse d’une conception simple ou un pourcentage extrêmement complexe, Azure Active Directory est la plateforme Microsoft Identity hello qui prend en charge Office 365, Microsoft Online Services et applications prenant en charge de cloud.

## <a name="define-an-integration-strategy"></a>Définir une stratégie d’intégration
Microsoft possède trois scénarios principaux d’intégration : identités cloud, identités synchronisées et identités fédérées.  Vous devez prévoir d’adopter l’une de ces stratégies d’intégration.  Hello stratégie que vous choisissez peut varier et inclure les décisions de hello en choisissant une, le type de l’expérience utilisateur vous souhaitez tooprovide, avez-vous des infrastructures hello déjà en place et nouveautés hello plus économique.  

![](./media/hybrid-id-design-considerations/integration-scenarios.png)

scénarios de Hello définis dans hello ci-dessus figure sont :

* **Identités de cloud computing**: il s’agit des identités qui existent uniquement dans le cloud de hello.  Dans les cas de hello d’Azure AD, ils résident en particulier dans votre annuaire Azure AD.
* **Synchronisation**: il s’agit des identités qui existent localement et dans le cloud de hello.  À l’aide d’Azure AD Connect, ces utilisateurs sont créés ou joints avec des comptes Azure AD existants.  Hello hachage de mot de passe de l’utilisateur est synchronisé à partir de cloud de toohello environnement hello local dans ce que l'on appelle un hachage de mot de passe.  Lors de la synchronisation de l’aide hello l’inconvénient est que si un utilisateur est désactivé dans l’environnement local de hello, il peut occuper les heures too3 pour ce tooshow d’état de compte dans Azure AD.  Il s’agit en raison de l’intervalle de temps de synchronisation toohello.
* **Fédéré**: ces identités existent à la fois localement et dans le cloud de hello.  À l’aide d’Azure AD Connect, ces utilisateurs sont créés ou joints avec des comptes Azure AD existants.  

> [!NOTE]
> Pour plus d’informations sur les options de synchronisation hello lire [intégrer vos identités locales avec Azure Active Directory](connect/active-directory-aadconnect.md).
> 
> 

Hello tableau suivant vous aide à déterminer les avantages de hello et les inconvénients de chacune des hello suivant des stratégies :

| Stratégie | Avantages | Inconvénients |
| --- | --- | --- |
| **Identités cloud** |Toomanage plus facile de petite entreprise. <br> Rien n’est nécessaire de matériel supplémentaire de tooinstall non local<br>Aisément la désactiver si l’utilisateur de hello quitte la société de hello |Les utilisateurs doivent toosign dans lorsqu’ils accèdent à des charges de travail dans le cloud de hello <br> Les mots de passe peuvent ou peut ne pas être la même hello pour les identités de cloud et locales |
| **Synchronisée** |Le mot de passe local permettra l’authentification sur les répertoires locaux et cloud  <br>Toomanage plus facile pour les organisations de petite, moyennes ou grandes <br>Les utilisateurs peuvent disposer de l’authentification unique (SSO) pour certaines ressources <br> Méthode Microsoft préférée pour la synchronisation <br> Toomanage plus facile |Certains clients ne puissent pas envie toosynchronize leurs répertoires avec hello cloud en raison de la police de la société spécifique |
| **Adresses IP fédérées** |Les utilisateurs peuvent disposer de l’authentification unique (SSO)  <br>Si un utilisateur s’arrête ou quitte, hello compte possible être immédiatement désactivé et l’accès est révoqué,<br> Prise en charge des scénarios avancés qui ne peuvent pas être effectués avec l’option Synchronisée |Les étapes plus toosetup et configurer <br> Maintenance plus élevée <br> Peut nécessiter du matériel supplémentaire pour l’infrastructure STS hello <br> Serveur de fédération de matériel supplémentaire tooinstall hello nécessiter. Logiciels supplémentaires sont nécessaires si AD FS est utilisé. <br> Requiert une installation complète pour l’authentification unique <br> Point critique de l’échec si le serveur de fédération hello est arrêté, les utilisateurs ne pourront tooauthenticate |

### <a name="client-experience"></a>Expérience client
stratégie Hello que vous utilisez détermine l’expérience d’authentification de l’utilisateur du hello.  Hello tableaux suivants fournissent des informations sur ce que les utilisateurs hello doivent attendre leurs connectez-vous expérience toobe.  Notez que tous les fournisseurs d’identité fédérée ne prennent pas en charge l’authentification unique dans tous les scénarios.

**Applications réseau jointes à un domaine et privées**:

|  | Identité synchronisée | Identité fédérée |
| --- | --- | --- |
| Navigateurs web |Authentification basée sur les formulaires |l’authentification unique, parfois requis toosupply ID d’organisation |
| Outlook |Demander les informations d’identification |Demander les informations d’identification |
| Skype Entreprise (Lync) |Demander les informations d’identification |Authentification unique pour Lync, informations d’identification demandées pour Exchange |
| OneDrive Entreprise |Demander les informations d’identification |Authentification unique |
| Abonnement Office Professionnel Plus |Demander les informations d’identification |Authentification unique |

**Sources externes ou non fiables** :

|  | Identité synchronisée | Identité fédérée |
| --- | --- | --- |
| Navigateurs web |Authentification basée sur les formulaires |Authentification basée sur les formulaires |
| Outlook, Skype Entreprise (Lync), OneDrive Entreprise, abonnement Office |Demander les informations d’identification |Demander les informations d’identification |
| Exchange ActiveSync |Demander les informations d’identification |Authentification unique pour Lync, informations d’identification demandées pour Exchange |
| Applications mobiles |Demander les informations d’identification |Demander les informations d’identification |

Si vous avez déterminé à partir de la tâche 1 que vous avez un 3e partie toouse de cours IdP ou sont une fédération tooprovide avec Azure AD, vous avez besoin de fonctionnalités de toobe prenant en charge de hello suivant pris en charge :

* N’importe quel fournisseur SAML 2.0 qui est conforme pour hello profil SP-Lite peut prendre en charge l’authentification tooAzure AD et les applications associées
* Authentification passive prend en charge, ce qui facilite la tooOWA d’authentification, simulé, etc..
* Les clients Exchange Online peuvent être pris en charge via hello SAML 2.0 améliorée Client profil (ECP)

Vous devez également avoir conscience des fonctionnalités qui ne seront pas disponibles :

* Sans prise en charge de WS-Trust/WS-Federation, tous les autres clients actifs s’interrompent.
  * Cela signifie aucun client Lync, le client OneDrive, abonnement Office, Office Mobile, tooOffice préalable 2016
* Transition de l’authentification d’Office toopassive lui permettront de toosupport IdPs de 2.0 SAML pur, mais prise en charge seront toujours sur une base de client par client

> [!NOTE]
> Pour hello plus mises à jour de liste de lecture hello article http://aka.ms/ssoproviders.
> 
> 

## <a name="define-synchronization-strategy"></a>Définir la stratégie de synchronisation
Dans cette tâche, vous allez définir outils hello qui seront locale données toohello dans le cloud utilisé toosynchronize hello organisation et ce que vous devez utiliser de topologie.  Car la plupart des organisations utilisent Active Directory, les informations sur l’utilisation de questions de hello Azure AD Connect tooaddress ci-dessus sont fournies en détail.  Pour les environnements qui n’ont pas d’Active Directory, il existe des informations sur l’utilisation de FIM 2010 R2 ou MIM 2016 toohelp planifier cette stratégie.  Toutefois, les versions futures d’Azure AD Connect prend en charge les annuaires LDAP, par conséquent, en fonction de votre scénario, ces informations peuvent être en mesure de tooassist.

### <a name="synchronization-tools"></a>Outils de synchronisation
Années de hello, plusieurs outils de synchronisation ont existé et utilisés pour différents scénarios.  Actuellement, Azure AD Connect est hello tootool accédez de choix pour tous les scénarios pris en charge.  AAD Sync et DirSync sont également toujours disponibles et peuvent même être présents dans votre environnement actuel. 

> [!NOTE]
> Pour hello dernières informations concernant les fonctions hello pris en charge de chaque outil, consultez [comparaison des outils d’intégration d’annuaire](active-directory-hybrid-identity-design-considerations-tools-comparison.md) l’article.  
> 
> 

### <a name="supported-topologies"></a>Topologies prises en charge
Lorsque vous définissez une stratégie de synchronisation, topologie hello utilisé doit être déterminée. Selon hello informations a été déterminées à l’étape 2, vous pouvez déterminer quelle topologie sont toouse d’un bon hello. forêt unique d’Hello, seule topologie Active Directory de Azure est hello courants et se compose d’une seule forêt Active Directory et une seule instance d’Azure AD.  Il est en train de toobe utilisé dans la majorité des scénarios de hello et topologie de hello attendu lors de l’utilisation de l’installation de Azure AD connecter Express comme indiqué dans la figure ci-dessous hello.

![](./media/hybrid-id-design-considerations/single-forest.png)Scénario de forêt unique il est très courant pour un même les petites et grandes entreprises toohave plusieurs forêts, comme indiqué dans la Figure 5.

> [!NOTE]
> Pour plus d’informations sur hello différents locaux et topologies de Azure AD avec synchronisation Azure AD Connect lire l’article de hello [Topologies pour Azure AD Connect](connect/active-directory-aadconnect-topologies.md).
> 
> 

![](./media/hybrid-id-design-considerations/multi-forest.png) 

Scénario de forêts multiples

Si ce cas hello hello puis multi-forest-seule topologie AD Azure doit être considérée si hello éléments suivantes sont remplies :

* Les utilisateurs ont une identité uniquement 1 dans toutes les forêts : hello identifiant de section utilisateurs ci-dessous décrit plus en détail.
* utilisateur de Hello authentifie forêt toohello dans lequel se trouve leur identité
* Le nom UPN et l’ancre source (ID immuable) proviendront de cette forêt.
* Toutes les forêts sont accessibles par Azure AD Connect : cela signifie qu’il n’a pas besoin toobe joint au domaine et que vous peut être placé dans un réseau de périmètre si cela facilite ce.
* Les utilisateurs n’ont qu’une seule boîte aux lettres.
* forêt Hello qui héberge les boîtes aux lettres d’un utilisateur a la meilleure qualité de données hello pour les attributs visibles dans la liste d’adresses globale (LAG) Exchange de hello
* S’il n’existe aucune boîte aux lettres utilisateur de hello, puis n’importe quelle forêt peut être toocontribute utilisé ces valeurs.
* Si vous avez une boîte aux lettres liée, puis il existe également un autre compte dans un toosign forêt différente de celle utilisée dans.

> [!NOTE]
> Objets qui existent dans à la fois localement et dans le cloud de hello sont « connectés » via un identificateur unique. Dans le contexte de hello de synchronisation d’annuaires, cet identificateur unique est désignée tooas hello SourceAnchor. Dans le contexte de hello de Single Sign-On, il s’agit de tooas visé hello ImmutableId. [Concepts de conception pour Azure AD Connect](connect/active-directory-aadconnect-design-concepts.md#sourceanchor) pour plus d’informations concernant l’utilisation de hello de SourceAnchor.
> 
> 

Si hello ci-dessus ne sont pas remplies et que vous avez plusieurs comptes actifs ou plusieurs boîtes aux lettres, Azure AD Connect sera choisir l’une et ignorer hello autres.  Si vous avez lié des boîtes aux lettres, mais aucun autre compte, ces comptes ne seront pas exportée tooAzure AD et que l’utilisateur ne sera pas membre des groupes.  Cette valeur diffère de la façon dont il se trouvait hello au-delà avec DirSync et est prise en charge toobetter intentionnelle ces scénarios à plusieurs forêts. Un scénario de forêts multiples est indiqué dans la figure ci-dessous hello.

![](./media/hybrid-id-design-considerations/multiforest-multipleAzureAD.png) 

**Scénario Azure AD de plusieurs forêts multiples**

Il est recommandé de toohave que simplement un répertoire unique dans Azure AD pour une organisation, mais elle est prise en charge qu’il qu'est conservée une relation 1:1 entre un serveur de synchronisation Azure AD Connect et un annuaire Azure AD.  Pour chaque instance d’Azure AD, vous aurez besoin d’une installation d’Azure AD Connect.  En outre, Azure AD, par sa conception est isolé et les utilisateurs dans une instance d’Azure AD ne sera pas en mesure de toosee des utilisateurs dans une autre instance.

Il est possible et tooconnect pris en charge une instance de répertoires d’Azure AD de toomultiple d’Active Directory comme indiqué dans la figure ci-dessous hello sur site :

![](./media/hybrid-id-design-considerations/single-forest-flitering.png) 

**Scénario de filtrage d’une forêt unique**

Dans l’ordre toodo suivante hello doit être remplie :

* Les serveurs de synchronisation Azure AD Connect doivent être configurés pour le filtrage et ils ont donc chacun un ensemble d’objets mutuellement exclusifs.  Cela fait, par exemple, par la portée de chaque unité d’organisation ou un domaine particulier du serveur tooa.
* Un serveur DNS ne peut être inscrit dans un seul annuaire Azure AD pour hello UPN des utilisateurs hello Bonjour locale Active Directory doit utiliser des espaces de noms distincts
* Les utilisateurs dans une instance d’Azure AD seront en mesure de toosee des utilisateurs à partir de leur instance.  Ils ne seront pas être des autres instances d’utilisateurs en mesure de toosee hello
* Seul un des répertoires de hello Azure AD peut activer Exchange hybride avec hello AD local
* Exclusivité mutuelle s’applique également à toowrite différée.  Ainsi, certaines fonctionnalités d’écriture différée ne sont pas prises en charge avec cette topologie, car elles supposent une configuration locale unique.  notamment :
  * Écriture différée des groupes avec la configuration par défaut
  * Écriture différée des appareils

Sachez que hello suivante n’est pas pris en charge et ne doit pas être choisie en tant qu’implémentation :

* Il n’est pas toohave pris en charge plusieurs serveurs de synchronisation Azure AD Connect connexion toohello même instance Azure AD directory même s’ils sont configuré toosynchronize mutuellement définis d’objet
* Il est non pris en charge toosync hello répertoires de toomultiple AD Azure même utilisateur. 
* Il est également toomake non pris en charge une modification de configuration des utilisateurs de toomake dans un tooappear d’Azure AD en tant que contacts dans un autre annuaire Azure AD. 
* Il est également des répertoires de toomodify non pris en charge Azure AD Connect synchronisation tooconnect toomultiple Azure AD.
* Les annuaires Azure AD sont isolés par conception. Il s’agit de configuration de hello toochange non pris en charge Azure AD Connect tooread de données de synchronisation à partir d’un autre annuaire Azure AD dans un toobuild tentative d’une liste d’adresses globale commune et unifiée entre les annuaires hello. Il est également tooexport non pris en charge par les utilisateurs comme contacts tooanother local AD à l’aide de la synchronisation Azure AD Connect.

> [!NOTE]
> Si votre organisation limite les ordinateurs de votre réseau de se connecter toohello Internet, cet article répertorie les points de terminaison hello (noms de domaine complets, IPv4 et IPv6 de plages d’adresses) que vous devez inclure dans votre sortie autorise des listes et la Zone des Sites de confiance Internet Explorer de tooensure des ordinateurs client vos ordinateurs utiliser Office 365. Pour plus d’informations, consultez [URL et plages d’adresses IP Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US).
> 
> 

## <a name="define-multi-factor-authentication-strategy"></a>Définir la stratégie d’authentification multifacteur
Dans cette tâche, vous allez définir hello toouse de stratégie de l’authentification multifacteur.  Azure Multi-Factor Authentication existe en deux versions différentes.  Un est un nuage et hello autres est local à l’aide de hello serveur Azure MFA.  Basé sur l’évaluation hello que vous ci-dessus, vous pouvez déterminer quelle solution est hello un approprié pour votre stratégie.  Tableau hello ci-dessous toodetermine la conception option mieux répondre aux exigences de sécurité de votre entreprise :

Options de conception multifacteur :

| Asset toosecure | Authentification Multifacteur dans le cloud de hello | MFA en local |
| --- | --- | --- |
| Applications Microsoft |yes |yes |
| Applications SaaS dans la galerie d’applications hello |yes |yes |
| Applications IIS publiées via le proxy d'application Azure AD |yes |yes |
| Applications IIS ne pas publiées via hello Proxy d’application Azure AD |no |yes |
| Accès à distance en tant que VPN, passerelle Bureau à distance (RDG) |no |yes |

Bien que vous pouvez avoir réglé sur une solution pour votre stratégie, vous devez toujours toouse hello évaluation ci-dessus dans lequel se trouvent vos utilisateurs.  Cela peut entraîner des toochange de solution hello.  Utilisez table hello ci-dessous tooassist vous cette classification :

| Emplacement de l’utilisateur | Option de conception préférée |
| --- | --- |
| Azure Active Directory |Multi-Factor Authentication dans le cloud de hello |
| Azure AD et AD local à l'aide de la fédération avec AD FS |Les deux |
| Azure AD et AD local utilisant Azure AD Connect : aucune synchronisation de mot de passe |Les deux |
| Azure AD et local utilisant Azure AD Connect avec synchronisation de mot de passe |Les deux |
| AD local |Serveur Multi-Factor Authentication |

> [!NOTE]
> Vous devez également vous assurer qu’option de conception de l’authentification multifacteur hello que vous avez sélectionné prend en charge les fonctionnalités de hello qui sont requises pour votre conception.  Pour plus d’informations consultez [choisir des solutions de sécurité de multi-Factor hello pour vous](../multi-factor-authentication/multi-factor-authentication-get-started.md#what-am-i-trying-to-secure).
> 
> 

## <a name="multi-factor-auth-provider"></a>Fournisseur d’authentification multi facteurs
Multi-Factor Authentication est disponible par défaut pour les administrateurs généraux ayant un locataire Azure Active Directory. Toutefois, si vous souhaitez tooall de l’authentification multifacteur tooextend de vos utilisateurs et/ou souhaitez tooyour administrateurs globaux toobe tootake en mesure de parti de certaines fonctionnalités telles que le portail de gestion hello, messages de bienvenue personnalisés et des rapports, puis vous devez acheter et configurer Fournisseur d’authentification multifacteur.

> [!NOTE]
> Vous devez également vous assurer qu’option de conception de l’authentification multifacteur hello que vous avez sélectionné prend en charge les fonctionnalités de hello qui sont requises pour votre conception. 
> 
> 

## <a name="next-steps"></a>Étapes suivantes
[Déterminer les exigences de protection des données](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md)

## <a name="see-also"></a>Voir aussi
[Présentation des considérations relatives à la conception](active-directory-hybrid-identity-design-considerations-overview.md)

