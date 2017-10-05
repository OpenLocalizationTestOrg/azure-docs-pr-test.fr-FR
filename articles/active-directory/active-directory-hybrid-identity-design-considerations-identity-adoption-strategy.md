---
title: "Considérations relatives à la conception d’identités hybrides Azure Active Directory : Définir une stratégie d’adoption des identités hybrides | Microsoft Docs"
description: "Avec le contrôle d’accès conditionnel, Azure Active Directory vérifie les conditions spécifiques que vous choisissez lors de l’authentification de l’utilisateur et avant d’autoriser l’accès à l’application. Une fois que ces conditions sont remplies, l’utilisateur est authentifié et autorisé à accéder à l’application."
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
ms.openlocfilehash: 2c57b394beb6382807a4c8c83de975a0ae68d726
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="define-a-hybrid-identity-adoption-strategy"></a>Définir une stratégie d’adoption des identités hybrides
Dans cette tâche, vous allez définir la stratégie d’adoption des identités hybrides pour que votre solution d’identités hybrides réponde aux exigences de l’entreprise évoquées dans :

* [Déterminer les besoins métier](active-directory-hybrid-identity-design-considerations-business-needs.md)
* [Déterminer les exigences de synchronisation de répertoire](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)
* [Déterminer les exigences d’authentification multifacteur](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="define-business-needs-strategy"></a>Définir une stratégie de besoins métier
La première tâche concerne la détermination des besoins métier de l’entreprise.  Cette opération peut être très étendue et vous risquez de vous éloigner des objectifs si vous n’êtes pas prudent.  Au début, faites simple, mais n’oubliez pas de prévoir une conception qui prend en charge et facilite les modifications ultérieures.  Qu’il s’agisse d’une conception simple ou très complexe, Azure Active Directory est la plateforme Microsoft Identity qui prend en charge Office 365, Microsoft Online Services et les applications cloud.

## <a name="define-an-integration-strategy"></a>Définir une stratégie d’intégration
Microsoft possède trois scénarios principaux d’intégration : identités cloud, identités synchronisées et identités fédérées.  Vous devez prévoir d’adopter l’une de ces stratégies d’intégration.  La stratégie que vous choisissez peut varier et les éléments à considérer à l’heure d’en choisir une peuvent inclure le type d’expérience utilisateur que vous souhaitez proposer, le fait de disposer de l’infrastructure existante déjà en place et la rentabilité.  

![](./media/hybrid-id-design-considerations/integration-scenarios.png)

Les scénarios définis dans la figure ci-dessus sont les suivants :

* **Identités cloud**: ce sont des identités qui existent uniquement dans le cloud.  Dans le cas d’Azure AD, elles résideraient en particulier dans votre répertoire Azure AD.
* **Synchronisée**: ce sont des identités qui existent en local et dans le cloud.  À l’aide d’Azure AD Connect, ces utilisateurs sont créés ou joints avec des comptes Azure AD existants.  Le hachage du mot de passe de l’utilisateur est synchronisé à partir de l’environnement local vers le cloud dans ce que l’on appelle un hachage du mot de passe.  Lorsque vous utilisez l’option Synchronisée, l’inconvénient est que si un utilisateur est désactivé dans l’environnement local, l’affichage de l’état du compte dans Azure AD peut prendre jusqu’à 3 heures.  Cela est dû à l’intervalle de synchronisation.
* **Fédérée**: ces identités existent à la fois en local et dans le cloud.  À l’aide d’Azure AD Connect, ces utilisateurs sont créés ou joints avec des comptes Azure AD existants.  

> [!NOTE]
> Pour plus d’informations sur les options de synchronisation, consultez la rubrique [Intégration de vos identités locales à Azure Active Directory](connect/active-directory-aadconnect.md).
> 
> 

Le tableau suivant vous aidera à déterminer les avantages et inconvénients de chacune des stratégies suivantes :

| Stratégie | Avantages | Inconvénients |
| --- | --- | --- |
| **Identités cloud** |Plus faciles à gérer pour les petites entreprises. <br> Rien à installer localement - Aucun matériel supplémentaire requis<br>Faciles à désactiver si l’utilisateur quitte l’entreprise |Les utilisateurs devront se connecter lorsqu’ils accèdent aux charges de travail dans le cloud  <br> Les mots de passe peuvent être les mêmes ou non pour les identités cloud et locales |
| **Synchronisée** |Le mot de passe local permettra l’authentification sur les répertoires locaux et cloud  <br>Plus faciles à gérer pour les petites, moyennes et grandes entreprises <br>Les utilisateurs peuvent disposer de l’authentification unique (SSO) pour certaines ressources <br> Méthode Microsoft préférée pour la synchronisation <br> Plus faciles à gérer |Certains clients peuvent rechigner à synchroniser leurs répertoires avec le cloud en raison de la stratégie spécifique de l’entreprise |
| **Adresses IP fédérées** |Les utilisateurs peuvent disposer de l’authentification unique (SSO)  <br>Si un utilisateur termine une mission ou quitte l’entreprise, le compte peut immédiatement être désactivé et l’accès révoqué,<br> Prise en charge des scénarios avancés qui ne peuvent pas être effectués avec l’option Synchronisée |Étapes supplémentaires pour installer et configurer <br> Maintenance plus élevée <br> Peut requérir du matériel supplémentaire pour l’infrastructure STS <br> Peut requérir du matériel supplémentaire pour installer le serveur de fédération. Un logiciel supplémentaire est requis si vous utilisez AD FS <br> Requiert une installation complète pour l’authentification unique <br> Point de défaillance critique : si le serveur de fédération est arrêté, les utilisateurs ne sont pas en mesure de s’authentifier |

### <a name="client-experience"></a>Expérience client
La stratégie que vous utilisez détermine l’expérience de connexion utilisateur.  Les tableaux suivants vous fournissent des informations sur ce que les utilisateurs peuvent attendre de leur expérience de connexion.  Notez que tous les fournisseurs d’identité fédérée ne prennent pas en charge l’authentification unique dans tous les scénarios.

**Applications réseau jointes à un domaine et privées**:

|  | Identité synchronisée | Identité fédérée |
| --- | --- | --- |
| Navigateurs web |Authentification basée sur les formulaires |Authentification unique, parfois requise pour fournir l’ID d’organisation |
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

Si vous avez déterminé lors de la tâche 1 que vous avez un IdP tiers ou que vous allez en utiliser un pour fournir une fédération avec Azure AD, vous devez connaître les fonctionnalités prises en charge suivantes :

* N’importe quel fournisseur SAML 2.0 compatible avec le profil SP-Lite peut prendre en charge l’authentification auprès d’Azure AD et des applications associées
* Prend en charge l’authentification passive, qui facilite l’authentification OWA, SPO, etc.
* Les clients Exchange Online peuvent être pris en charge avec le profil client amélioré (ECP) SAML 2.0

Vous devez également avoir conscience des fonctionnalités qui ne seront pas disponibles :

* Sans prise en charge de WS-Trust/WS-Federation, tous les autres clients actifs s’interrompent.
  * Cela signifie aucun client Lync, client OneDrive, abonnement Office ou Office Mobile antérieur à Office 2016.
* La transition d’Office à l’authentification passive permettra la prise en charge de fournisseurs d’identité SAML 2.0 purs, mais cette prise en charge s’effectuera toujours client par client.

> [!NOTE]
> Pour consulter la liste la plus à jour, lisez l’article http://aka.ms/ssoproviders.
> 
> 

## <a name="define-synchronization-strategy"></a>Définir la stratégie de synchronisation
Dans cette tâche, vous allez définir les outils qui seront utilisés pour synchroniser les données locales de l’organisation sur le cloud et la topologie à utiliser.  Étant donné que la plupart des organisations utilisent Active Directory, les informations sur l’utilisation d’Azure AD Connect concernant les questions ci-dessus sont très détaillées.  Pour les environnements qui ne disposent pas d’Active Directory, des informations sur l’utilisation de FIM 2010 R2 ou MIM 2016 sont disponibles pour aider à planifier cette stratégie.  Toutefois, les versions futures d’Azure AD Connect prendront en charge les répertoires LDAP. Par conséquent, selon votre chronologie, ces informations sont susceptibles de vous aider.

### <a name="synchronization-tools"></a>Outils de synchronisation
Au fil des années, plusieurs outils de synchronisation ont existé et ont été utilisés pour différents scénarios.  Actuellement, Azure AD Connect est l’outil de prédilection pour tous les scénarios pris en charge.  AAD Sync et DirSync sont également toujours disponibles et peuvent même être présents dans votre environnement actuel. 

> [!NOTE]
> Pour les dernières informations concernant les fonctionnalités prises en charge de chaque outil, consultez l’article [Comparaison des outils d’intégration de répertoire](active-directory-hybrid-identity-design-considerations-tools-comparison.md) .  
> 
> 

### <a name="supported-topologies"></a>Topologies prises en charge
Lorsque vous définissez une stratégie de synchronisation, la topologie qui est utilisée doit être déterminée. Selon les informations qui ont été déterminées à l’étape 2, vous pouvez déterminer la topologie adaptée à utiliser. La forêt unique, topologie Azure AD unique, est la plus courante et se compose d’une forêt Active Directory unique et d’une seule instance d’Azure AD.  Ces éléments seront utilisés dans la majorité des scénarios et constituent la topologie attendue lors de l’utilisation de l’installation Express Azure AD Connect comme indiqué dans la figure ci-dessous.

![](./media/hybrid-id-design-considerations/single-forest.png) Scénario de forêt unique Il est très courant pour les grandes et même pour les petites entreprises de posséder plusieurs forêts, comme illustré à la Figure 5.

> [!NOTE]
> Pour plus d’informations sur les différentes topologies locales et Azure AD avec la synchronisation Azure AD Connect, consultez l’article [Topologies pour Azure AD Connect](connect/active-directory-aadconnect-topologies.md).
> 
> 

![](./media/hybrid-id-design-considerations/multi-forest.png) 

Scénario de forêts multiples

La topologie Azure AD unique de forêts multiples doit être prise en considération si les éléments suivants sont vrais :

* Les utilisateurs ont 1 identité uniquement dans toutes les forêts ; la section relative à l’identification unique des utilisateurs ci-dessous décrit cela plus en détail.
* L’utilisateur s’authentifie à la forêt dans laquelle se trouve son identité.
* Le nom UPN et l’ancre source (ID immuable) proviendront de cette forêt.
* Toutes les forêts sont accessibles par Azure AD Connect : cela signifie qu’elles ne doivent pas obligatoirement être jointes à un domaine et qu’elles peuvent être placées dans une zone DMZ si cela facilite ce processus.
* Les utilisateurs n’ont qu’une seule boîte aux lettres.
* La forêt qui héberge la boîte aux lettres d’un utilisateur a la meilleure qualité de données pour les attributs visibles dans la liste d’adresses globale (LAG) Exchange.
* Si aucune boîte aux lettres n’est associée à l’utilisateur, n’importe quelle forêt peut être utilisée pour fournir ces valeurs.
* Si vous avez une boîte aux lettres liée, il existe également un autre compte dans une forêt différente de celle utilisée pour la connexion.

> [!NOTE]
> Les objets qui existent à la fois en local et dans le cloud sont « connectés » via un identificateur unique. Dans le contexte de synchronisation de répertoire, cet identificateur unique est appelé SourceAnchor. Dans le contexte de l’authentification unique, il est appelé ImmutableId. [Principes de conception pour Azure AD Connect](connect/active-directory-aadconnect-design-concepts.md#sourceanchor) pour plus d’informations concernant l’utilisation de SourceAnchor.
> 
> 

Si la partie ci-dessus n’est pas vraie et que vous avez plus d’un compte actif ou plusieurs boîtes aux lettres, Azure AD Connect choisira un élément et ignorera les autres.  Si vous avez lié des boîtes aux lettres, mais aucun autre compte, ces comptes ne seront pas exportés vers Azure AD et cet utilisateur ne sera membre d’aucun groupe.  La situation a évolué avec DirSync et l’intention est de mieux prendre en charge ces scénarios de forêts multiples. Un scénario de forêts multiples est illustré dans la figure ci-dessous.

![](./media/hybrid-id-design-considerations/multiforest-multipleAzureAD.png) 

**Scénario Azure AD de plusieurs forêts multiples**

Il est recommandé de disposer seulement d’un répertoire unique dans Azure AD pour une organisation, mais une relation 1 à 1 reste possible entre un serveur de synchronisation Azure AD Connect et un répertoire Azure AD.  Pour chaque instance d’Azure AD, vous aurez besoin d’une installation d’Azure AD Connect.  En outre, par conception, Azure AD est isolé et les utilisateurs dans une instance d’Azure AD ne seront pas en mesure de voir les utilisateurs dans une autre instance.

Il est possible et pris en charge de connecter une instance locale d’Active Directory à plusieurs répertoires Azure AD, comme illustré dans la figure ci-dessous :

![](./media/hybrid-id-design-considerations/single-forest-flitering.png) 

**Scénario de filtrage d’une forêt unique**

Pour ce faire, les éléments suivants doivent se vérifier :

* Les serveurs de synchronisation Azure AD Connect doivent être configurés pour le filtrage et ils ont donc chacun un ensemble d’objets mutuellement exclusifs.  Cela est possible, par exemple, en délimitant l’étendue de chaque serveur à un domaine ou à une unité d’organisation spécifique.
* Un domaine DNS ne peut être inscrit que dans un seul répertoire Azure AD. Les UPN des utilisateurs d’Active Directory local doivent utiliser des espaces de noms distincts.
* Les utilisateurs dans une instance d’Azure AD seront uniquement en mesure de voir les utilisateurs à partir de leur instance.  Ils ne pourront pas voir les utilisateurs dans les autres instances.
* Seul un des répertoires Azure AD peut activer Exchange hybride avec AD local.
* L’exclusivité mutuelle s’applique également à l’écriture différée.  Ainsi, certaines fonctionnalités d’écriture différée ne sont pas prises en charge avec cette topologie, car elles supposent une configuration locale unique.  notamment :
  * Écriture différée des groupes avec la configuration par défaut
  * Écriture différée des appareils

Sachez que les éléments suivants ne sont pas pris en charge et ne doivent pas être choisis comme une implémentation :

* La connexion de plusieurs serveurs de synchronisation Azure AD Connect au même répertoire Azure AD n’est pas prise en charge, même s’ils sont configurés pour synchroniser un ensemble d’objets mutuellement exclusifs.
* La synchronisation d’un même utilisateur vers plusieurs annuaires Azure AD n’est pas prise en charge. 
* La modification d’une configuration pour faire en sorte que les utilisateurs dans un annuaire Azure AD apparaissent comme contacts dans un autre annuaire Azure AD n’est pas prise en charge. 
* La modification d’Azure AD Connect Sync pour qu’il se connecte à plusieurs annuaires Azure AD n’est pas non plus prise en charge.
* Les annuaires Azure AD sont isolés par conception. La modification de la configuration d’Azure AD Connect Sync pour lire des données à partir d’un autre annuaire Azure AD pour générer une liste d’adresses globale commune et unifiée entre les annuaires n’est pas prise en charge. L’exportation d’utilisateurs comme contacts vers un autre annuaire Active Directory local avec Azure AD Connect Sync n’est pas prise en charge.

> [!NOTE]
> Si votre organisation limite la connexion des ordinateurs de votre réseau à Internet, cet article répertorie les points de terminaison (noms de domaine complets, plages d’adresses IPv4 et IPv6) que vous devez inclure dans vos listes d’autorisation sortante et dans votre zone Sites de confiance Internet Explorer d’ordinateurs clients pour garantir que vos ordinateurs peuvent utiliser Office 365. Pour plus d’informations, consultez [URL et plages d’adresses IP Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US).
> 
> 

## <a name="define-multi-factor-authentication-strategy"></a>Définir la stratégie d’authentification multifacteur
Dans cette tâche, vous allez définir la stratégie d’authentification multifacteur à utiliser.  Azure Multi-Factor Authentication existe en deux versions différentes.  L’une est basée sur le cloud, et l’autre est locale et utilise le serveur MFA Azure.  En vous appuyant sur l’évaluation effectuée précédemment, vous pouvez déterminer quelle solution est correcte pour votre stratégie.  Utilisez le tableau ci-dessous pour déterminer l’option de conception répondant le mieux aux exigences de sécurité de votre entreprise :

Options de conception multifacteur :

| Élément multimédia à sécuriser | MFA dans le cloud | MFA en local |
| --- | --- | --- |
| Applications Microsoft |yes |yes |
| Applications SaaS dans la galerie d’applications |yes |yes |
| Applications IIS publiées via le proxy d'application Azure AD |yes |yes |
| Applications IIS non publiées via le proxy Azure AD App  |no |yes |
| Accès à distance en tant que VPN, passerelle Bureau à distance (RDG) |no |yes |

Même si vous avez opté pour une solution pour votre stratégie, vous devez toujours utiliser l’évaluation ci-dessus sur l’emplacement où se trouvent vos utilisateurs.  Cela peut entraîner la modification de la solution.  Utilisez le tableau ci-dessous pour vous aider à déterminer les éléments suivants :

| Emplacement de l’utilisateur | Option de conception préférée |
| --- | --- |
| Azure Active Directory |Multi-Factor Authentication dans le cloud |
| Azure AD et AD local à l'aide de la fédération avec AD FS |Les deux |
| Azure AD et AD local utilisant Azure AD Connect : aucune synchronisation de mot de passe |Les deux |
| Azure AD et local utilisant Azure AD Connect avec synchronisation de mot de passe |Les deux |
| AD local |Serveur Multi-Factor Authentication |

> [!NOTE]
> Vous devez également vous assurer que l’option de conception de l’authentification multifacteur sélectionnée prend en charge les fonctionnalités requises pour votre conception.  Pour plus d’informations, consultez la rubrique [Choix de la solution de sécurité multifacteur la mieux adaptée](../multi-factor-authentication/multi-factor-authentication-get-started.md#what-am-i-trying-to-secure).
> 
> 

## <a name="multi-factor-auth-provider"></a>Fournisseur d’authentification multi facteurs
Multi-Factor Authentication est disponible par défaut pour les administrateurs généraux ayant un locataire Azure Active Directory. Toutefois, si vous souhaitez étendre l’authentification multifacteur à tous vos utilisateurs et/ou souhaitez que vos administrateurs généraux puissent tirer pleinement parti de certaines fonctionnalités telles que le portail de gestion, les messages de bienvenue personnalisés et les rapports, vous devez acheter et configurer un fournisseur Multi-Factor Authentication.

> [!NOTE]
> Vous devez également vous assurer que l’option de conception de l’authentification multifacteur sélectionnée prend en charge les fonctionnalités requises pour votre conception. 
> 
> 

## <a name="next-steps"></a>Étapes suivantes
[Déterminer les exigences de protection des données](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md)

## <a name="see-also"></a>Voir aussi
[Présentation des considérations relatives à la conception](active-directory-hybrid-identity-design-considerations-overview.md)

