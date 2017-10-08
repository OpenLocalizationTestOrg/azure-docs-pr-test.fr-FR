---
title: "Installation personnalisée d’Azure AD Connect | Microsoft Docs"
description: "Ce document décrit en détail les options d’installation personnalisée hello pour Azure AD Connect. Utilisez ces instructions de tooinstall Active Directory via Azure AD Connect."
services: active-directory
keywords: "Qu’est-ce que Azure AD Connect, Installation d’Active Directory, Composants requis pour Azure AD"
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 6d42fb79-d9cf-48da-8445-f482c4c536af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: c49724fab78c5a1688662043f69506fff6f82104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-installation-of-azure-ad-connect"></a>Installation personnalisée d’Azure AD Connect
Azure AD Connect **paramètres personnalisés** est utilisée lorsque vous souhaitez davantage d’options pour l’installation de hello. Il est utilisé si vous avez plusieurs forêts, ou si vous souhaitez que les fonctionnalités facultatives tooconfigure non traitées dans l’installation rapide de hello. Il est utilisé dans tous les cas où hello [ **installation express** ](active-directory-aadconnect-get-started-express.md) option ne répond pas à votre déploiement ou la topologie.

Avant de commencer l’installation d’Azure AD Connect, assurez-vous que trop[Téléchargez Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) préalable hello terminé les étapes [Azure AD Connect : conditions matérielles et](active-directory-aadconnect-prerequisites.md). Assurez-vous également de disposer des comptes comme décrit dans [Autorisations et comptes Azure AD Connect](active-directory-aadconnect-accounts-permissions.md).

Si les paramètres personnalisés ne correspond pas à votre topologie, par exemple tooupgrade DirSync, consultez [documentation connexe](#related-documentation) pour d’autres scénarios.

## <a name="custom-settings-installation-of-azure-ad-connect"></a>Installation des paramètres personnalisés d’Azure AD Connect
### <a name="express-settings"></a>Paramètres Express
Dans cette page, cliquez sur **personnaliser** toostart une installation de paramètres personnalisés.

### <a name="install-required-components"></a>Installation des composants requis
Lorsque vous installez les services de synchronisation hello, vous pouvez laisser section de configuration facultatives hello est désactivée et Azure AD Connect définit tout installer automatiquement. Il configure une instance de SQL Server 2012 Express LocalDB, créer des groupes appropriés de hello et affecter des autorisations. Si vous souhaitez les valeurs par défaut de hello toochange, vous pouvez utiliser hello suivant table toounderstand hello facultatif options de configuration qui sont disponibles.

![Composants requis](./media/active-directory-aadconnect-get-started-custom/requiredcomponents.png)

| Configuration facultative | Description |
| --- | --- |
| Utiliser un serveur SQL Server existant |Vous permet de toospecify hello nom et SQL Server nom de l’instance hello. Choisissez cette option si vous disposez déjà d’un serveur de base de données que vous aimeriez toouse. Entrez les nom d’instance hello suivi par un virgule et numéro de port dans **nom de l’Instance** si votre serveur SQL Server n’a pas de navigation activée. |
| Utiliser un compte de service existant |Par défaut, Azure AD Connect utilise un compte de service virtuel pour toouse de services de synchronisation hello. Si vous utilisez un serveur SQL distant ou que vous utilisez un proxy qui nécessite une authentification, vous devez toouse une **compte de service administré** ou utiliser un compte de service dans le domaine de hello et un mot de passe hello. Dans ce cas, entrez hello compte toouse. Assurez-vous qu’utilisateur hello exécutant hello installation est une association de sécurité dans SQL pour une connexion pour le compte de service hello peut être créée. Consultez [Autorisations et comptes Azure AD Connect](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) |
| Spécifier des groupes de synchronisation personnalisés |Par défaut Azure AD Connect crée quatre groupes locaux toohello serveur lors de l’installation des services de synchronisation hello. Ces groupes sont : groupe Administrateurs, opérateurs, Explorer le groupe et hello groupe de réinitialisation de mot de passe. Vous pouvez spécifier vos propres groupes ici. groupes de Hello doivent être locales sur le serveur de hello et ne peut pas se trouver dans le domaine de hello. |

### <a name="user-sign-in"></a>Connexion de l’utilisateur
Après avoir installé les composants requis de hello, vous êtes invité à tooselect vos utilisateurs unique méthode d’authentification. Hello tableau suivant fournit une brève description des options disponibles de hello. Pour obtenir une description complète des méthodes de connexion hello, consultez [connexion d’utilisateur](active-directory-aadconnect-user-signin.md).

![Connexion de l’utilisateur](./media/active-directory-aadconnect-get-started-custom/usersignin2.png)

| Option d’authentification unique | Description |
| --- | --- |
| Synchronisation de mot de passe |Les utilisateurs sont en mesure de toosign dans les services de cloud computing tooMicrosoft, tels qu’Office 365, à l’aide de hello même mot de passe de leur réseau local. les mots de passe utilisateurs Hello sont synchronisé tooAzure AD en tant qu’un hachage de mot de passe et l’authentification se produit dans le cloud de hello. Pour plus d’informations, consultez [Synchronisation de mot de passe](active-directory-aadconnectsync-implement-password-synchronization.md) . |
|Authentification directe (version préliminaire)|Les utilisateurs sont en mesure de toosign dans les services de cloud computing tooMicrosoft, tels qu’Office 365, à l’aide de hello même mot de passe de leur réseau local.  mot de passe utilisateurs Hello est passé via toohello locale Active Directory contrôleur toobe validé.
| Fédération avec AD FS |Les utilisateurs sont en mesure de toosign dans les services de cloud computing tooMicrosoft, tels qu’Office 365, à l’aide de hello même mot de passe de leur réseau local.  les utilisateurs de Hello sont redirigés tootheir toosign d’instance AD FS dans sur site et de l’authentification produit localement. |
| Ne pas configurer |Aucune fonctionnalité n’est installée ni configurée. Choisissez cette option si vous disposez déjà d’un serveur de fédération tiers ou d’une autre solution. |
|Activer l'authentification unique|Cette option est disponible avec la synchronisation de mot de passe et l’authentification directe et fournit une authentification unique sur l’expérience pour les utilisateurs sur le réseau d’entreprise de hello.  Pour plus d’informations, consultez [Authentification unique](active-directory-aadconnect-sso.md). </br>Remarque pour les clients d’AD FS cette option n’est pas disponible, car les services AD FS déjà offres hello même niveau de l’authentification unique.</br>(si PTA n’est pas libéré à hello simultanément)
|Option d’authentification|Cette option est disponible pour les clients de synchronisation de mot de passe et fournit une authentification unique sur l’expérience pour les utilisateurs sur le réseau d’entreprise de hello.  </br>Pour plus d’informations, consultez [Authentification unique](active-directory-aadconnect-sso.md). </br>Remarque pour les clients d’AD FS cette option n’est pas disponible, car les services AD FS déjà offres hello même niveau de l’authentification unique.


### <a name="connect-tooazure-ad"></a>Se connecter tooAzure AD
Sur l’écran tooAzure AD de se connecter hello, entrez un compte d’administrateur général et un mot de passe. Si vous avez sélectionné **fédération avec AD FS** sur la page précédente de hello, ne vous connectez pas avec un compte dans un domaine, vous prévoyez tooenable pour la fédération. Il est recommandé de toouse un compte dans la valeur par défaut hello **onmicrosoft.com** domaine, qui est fourni avec votre annuaire Azure AD.

Ce compte est uniquement utilisé toocreate un compte de service dans Azure AD et n’est pas utilisé après la fin de l’Assistant de hello.  
![Connexion de l’utilisateur](./media/active-directory-aadconnect-get-started-custom/connectaad.png)

Si votre compte d’administrateur général a l’authentification Multifacteur activée, vous devez tooprovide hello mot de passe à nouveau hello connexion contextuelle et complète hello stimulation d’authentification Multifacteur. demande d’accès Hello peut être un fournissant un code de vérification ou un appel téléphonique.  
![Connexion de l’utilisateur dans MFA](./media/active-directory-aadconnect-get-started-custom/connectaadmfa.png)

compte d’administrateur général Hello peut également avoir [Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md) activé.

Si vous recevez une erreur et que vous avez des problèmes de connectivité, consultez [Résoudre les problèmes de connectivité liés à Azure AD Connect](active-directory-aadconnect-troubleshoot-connectivity.md).

## <a name="pages-under-hello-section-sync"></a>Pages de section hello synchronisation

### <a name="connect-your-directories"></a>Connexion de vos annuaires
tooconnect tooyour des services de domaine Active Directory, Azure AD Connect a besoin de nom de la forêt hello et les informations d’identification d’un compte disposant d’autorisations suffisantes.

![Répertoire Connect](./media/active-directory-aadconnect-get-started-custom/connectdir01.png)

Après la saisie du nom de la forêt hello et en cliquant sur **ajouter un répertoire**, une boîte de dialogue contextuelle s’affiche et vous demande de hello options suivantes :

| Option | Description |
| --- | --- |
| Utiliser un compte existant | Sélectionnez cette option si vous souhaitez que le compte tooprovide une existante AD DS toobe utilisé Azure AD Connect pour la connexion toohello AD forêt au cours de la synchronisation d’annuaires. Vous pouvez entrer une partie du domaine hello au format NetBios ou nom de domaine complet, autrement dit, FABRIKAM\syncuser ou fabrikam.com\syncuser. Ce compte peut être un compte d’utilisateur ordinaire, car elle doit uniquement des autorisations de lecture par défaut hello. Toutefois, selon votre scénario, vous pouvez avoir besoin d’autorisations supplémentaires. Pour en savoir plus, voir [Autorisations et comptes Azure AD Connect](active-directory-aadconnect-accounts-permissions.md#create-the-ad-ds-account). |
| Créer un compte | Sélectionnez cette option si vous voulez Azure AD Connect Assistant toocreate hello AD DS compte requis par Azure AD Connect pour la connexion toohello AD forêt au cours de la synchronisation d’annuaires. Lorsque cette option est sélectionnée, entrez les nom d’utilisateur hello et le mot de passe pour un compte administrateur d’entreprise. Hello compte administrateur d’entreprise fourni sera utilisé par Azure AD Connect hello de toocreate Assistant requis compte AD DS. Vous pouvez entrer une partie du domaine hello au format NetBios ou nom de domaine complet, c'est-à-dire que FABRIKAM\administrator ou fabrikam.com\administrator. |

![Répertoire Connect](./media/active-directory-aadconnect-get-started-custom/connectdir02.png)


### <a name="azure-ad-sign-in-configuration"></a>Configuration de connexion AD Azure
Cette page vous permet de tooreview hello UPN de domaines existants sur site AD DS et qui ont été vérifié dans Azure AD. Cette page vous permet également tooconfigure hello attribut toouse pour hello userPrincipalName.

![Domaines non vérifiés](./media/active-directory-aadconnect-get-started-custom/aadsigninconfig.png)  
Passez en revue chaque domaine marqué **Non ajouté** et **Non vérifié**. Assurez-vous que les domaines que vous utilisez ont été vérifiés dans Azure AD. Lorsque vous avez vérifié vos domaines, cliquez sur symboles d’actualisation hello. Pour plus d’informations, consultez [ajouter et vérifier le domaine de hello](../active-directory-add-domain.md)

**UserPrincipalName** -hello attribut userPrincipalName est utilisateurs d’attribut hello utilisent lorsqu’ils se connectent dans tooAzure AD et Office 365. les domaines Hello utilisé, également appelé hello suffixe UPN, doivent être vérifiées dans Azure AD avant que les utilisateurs de hello sont synchronisés. Microsoft vous recommande de tookeep hello par défaut attribut userPrincipalName. Si cet attribut n’est pas routable et ne peut pas être vérifié, il est possible tooselect un autre attribut. Vous pouvez par exemple sélectionner par courrier électronique en tant qu’attribut hello maintenant hello nom de connexion. Tout attribut utilisé à la place de l’élément userPrincipalName est qualifié d’ **ID secondaire**. valeur d’attribut d’un autre ID de Hello doit suivre hello RFC822 standard. Un ID secondaire peut être utilisé avec la fédération et la synchronisation de mots de passe.

>[!NOTE]
> Lorsque vous activez l’authentification directe, vous devez disposer au moins un domaine vérifié dans toocontinue ordre via l’Assistant de hello.

> [!WARNING]
> L’utilisation d’un ID secondaire n’est pas compatible avec toutes les charges de travail Office 365. Pour plus d’informations, consultez trop[configuration d’un autre ID de connexion](https://technet.microsoft.com/library/dn659436.aspx).
>
>

### <a name="domain-and-ou-filtering"></a>Filtrage domaine et unité organisationnelle
Par défaut, tous les domaines et unités d’organisation sont synchronisés. S’il existe des domaines ou des unités d’organisation que vous ne souhaitez pas toosynchronize tooAzure AD, vous pouvez désélectionner ces domaines et les unités d’organisation.  
![Filtrage par domaine/unité d’organisation](./media/active-directory-aadconnect-get-started-custom/domainoufiltering.png)  
Cette page dans l’Assistant de hello est configuration du filtrage de domaine et unité d’organisation. Si vous envisagez toomake modifications, puis consultez [filtrage basé sur le domaine](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) et [filtrage basé sur une unité d’organisation](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) avant d’apporter ces modifications. Des unités d’organisation sont essentielles pour la fonctionnalité de hello et ne doivent pas être désélectionnées.

Si vous utilisez le filtrage basé sur l’unité d’organisation avec une version d’Azure AD Connect antérieure à la version 1.1.524.0, les nouvelles unités d’organisation ajoutées par la suite sont synchronisées par défaut. Si vous souhaitez que le comportement de hello que les unités d’organisation ne doivent pas être synchronisées, puis vous pouvez le configurer après hello l’Assistant a terminé avec [filtrage basé sur une unité d’organisation](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering). Pour Azure AD Connect version 1.1.524.0 ou après, vous pouvez indiquer si vous souhaitez que les nouvelles unités d’organisation toobe ou non synchronisé.

Si vous envisagez de toouse [filtrage basé sur le groupe](#sync-filtering-based-on-groups), puis vérifiez que hello unité d’organisation avec un groupe de hello est inclus et non filtré avec filtrage d’unité d’organisation. Le filtrage basé sur l’unité d’organisation est évalué avant le filtrage basé sur le groupe.

Il est également possible que certains domaines ne sont pas accessibles en raison de restrictions de toofirewall. Ces domaines sont désélectionnés par défaut et présentent un avertissement.  
![Domaines inaccessibles](./media/active-directory-aadconnect-get-started-custom/unreachable.png)  
Si vous voyez cet avertissement, assurez-vous que ces domaines sont en effet inaccessibles et hello avertissement est normal.

### <a name="uniquely-identifying-your-users"></a>Identification unique de vos utilisateurs

#### <a name="select-how-users-should-be-identified-in-your-on-premises-directories"></a>Sélectionnez la façon dont les utilisateurs doivent être identifiés dans vos répertoires locaux
Bonjour la correspondance entre les forêts fonctionnalité vous permet de toodefine comment les utilisateurs à partir de vos forêts AD DS sont représentés dans Azure AD. Il est possible de représenter seulement une fois chaque utilisateur entre toutes les forêts, ou de présenter une combinaison des comptes activés et désactivés. Hello utilisateur peut également être représenté en tant que contact dans des forêts.

![Unique](./media/active-directory-aadconnect-get-started-custom/unique.png)

| Paramètre | Description |
| --- | --- |
| [Les utilisateurs ne sont représentés qu’une seule fois à travers toutes les forêts](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Tous les utilisateurs sont créés en tant qu’objets individuels dans Azure AD. les objets Hello ne sont pas jointes hello métaverse. |
| [Attribut de messagerie](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Cette option joint les utilisateurs et contacts si l’attribut de messagerie hello a hello même valeur dans des forêts différentes. Utilisez cette option si vos contacts ont été créés avec GALSync. Si cette option est sélectionnée, les objets utilisateur dont l’attribut de messagerie ne sont pas remplies ne seront pas synchronisé tooAzure AD. |
| [ObjectSID et msExchangeMasterAccountSID/ msRTCSIP-OriginatorSid](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Cette option associe un utilisateur activé dans une forêt de comptes à un utilisateur désactivé dans une forêt de ressources. Dans Exchange, cette configuration est connue en tant que « boîte aux lettres liée ». Cette option peut également être utilisée si vous utilisez uniquement Lync et Exchange n’est pas présent dans la forêt de ressources hello. |
| sAMAccountName et MailNickName |Cette option joint les attributs où il est attendu hello connectez-vous ID des utilisateurs de hello se trouvent. |
| Un attribut spécifique |Cette option vous permet de tooselect votre propre attribut. Si cette option est sélectionnée, les objets utilisateur dont l’attribut (sélectionné) ne sont pas remplies ne seront pas synchronisé tooAzure AD. **Limitation :** rendre toopick assurer un attribut déjà se trouvant dans le métaverse de hello. Si vous choisissez un attribut personnalisé (pas dans le métaverse de hello), hello ne peut pas l’Assistant. |

#### <a name="select-how-users-should-be-identified-with-azure-ad---source-anchor"></a>Sélectionnez la façon dont les utilisateurs doivent être identifiés avec Azure AD - ancre Source
Hello attribut sourceAnchor est un attribut qui est immuable pendant la durée de vie hello d’un objet utilisateur. Il est la clé primaire de hello liaison utilisateur local de hello disposant de hello dans Azure AD.

| Paramètre | Description |
| --- | --- |
| Laisser Azure gérer ancre source de hello pour moi | Sélectionnez cette option si vous souhaitez que les attributs de hello toopick Azure AD pour vous. Si vous sélectionnez cette option, Assistant Azure AD Connect s’applique la logique de sélection attribut sourceAnchor hello décrite dans la section de l’article [Azure AD Connect : concepts : à l’aide de msDS-ConsistencyGuid comme sourceAnchor de conception](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor). Assistant de Hello vous informe de l’attribut a été sélectionnée en tant qu’attribut d’ancre Source hello issue de l’installation personnalisée. |
| Un attribut spécifique | Sélectionnez cette option si vous le souhaitez toospecify un attribut Active Directory existant en tant qu’attribut de sourceAnchor hello. |

Étant donné que l’attribut de hello ne peut pas être modifié, vous devez prévoir un toouse bon attribut. Pour cela, nous vous recommandons objectGUID. Cet attribut n’est pas modifié, sauf si le compte d’utilisateur hello est déplacé entre des forêts/domaines. Dans un environnement à forêts multiples où vous déplacez des comptes entre les forêts, un autre attribut doit être utilisé, par exemple un attribut avec hello employeeID. Évitez les attributs susceptibles de changer si une personne se marie ou si son affectation est modifiée. Vous ne pouvez pas utiliser d’attributs avec @-sign, donc les adresses de messagerie et userPrincipalName ne peuvent pas être utilisés. attribut de Hello respecte la casse lorsque vous déplacez un objet entre les forêts, assurez-vous que toopreserve hello majuscules/minuscules. Les attributs binaires sont codés en base 64, mais les autres types d’attributs restent à l’état non codé. Dans les scénarios de fédération et dans certaines interfaces Azure AD, cet attribut est également appelé « immutableID ». Vous trouverez plus d’informations sur le point d’ancrage de hello source Bonjour [concepts de conception](active-directory-aadconnect-design-concepts.md#sourceanchor).

### <a name="sync-filtering-based-on-groups"></a>Filtrage de synchronisation basé sur les groupes
Hello filtrant sur la fonctionnalité des groupes vous permet de toosync uniquement un petit sous-ensemble des objets pour un projet pilote. toouse cette fonctionnalité, créer un groupe à cet effet dans votre annuaire Active Directory local. Ajoutez ensuite les utilisateurs et groupes qui doivent être synchronisé tooAzure AD en tant que membres directs. Plus tard, vous pouvez ajouter et supprimer les utilisateurs toothis groupe toomaintain hello liste d’objets qui doivent être présents dans Azure AD. Tous les objets que vous souhaitez toosynchronize doivent être membre du groupe de hello direct. Les utilisateurs, les groupes, les contacts et les ordinateurs/appareils doivent tous être des membres directs. L’appartenance à un groupe imbriqué n’est pas résolue. Lorsque vous ajoutez un groupe comme un membre, le seul groupe hello lui-même est ajouté et pas ses membres.

![Filtrage de la synchronisation](./media/active-directory-aadconnect-get-started-custom/filter2.png)

> [!WARNING]
> Cette fonctionnalité est uniquement prévue toosupport un déploiement pilote. Ne l’utilisez pas dans un environnement de production complet.
>
>

Dans un déploiement de production complet, il va toomaintain de disque dur toobe un seul groupe avec tous les objets toosynchronize. Au lieu de cela, vous devez utiliser une des méthodes hello dans [configurer le filtrage](active-directory-aadconnectsync-configure-filtering.md).

### <a name="optional-features"></a>Fonctionnalités facultatives
Cet écran vous permet de fonctionnalités facultatives de tooselect hello pour des scénarios spécifiques.

![Fonctionnalités facultatives](./media/active-directory-aadconnect-get-started-custom/optional.png)

> [!WARNING]
> Si vous avez actuellement DirSync ou Azure AD Sync active, n’activez pas une des fonctionnalités de l’écriture différée hello dans Azure AD Connect.
>
>

| Fonctionnalités facultatives | Description |
| --- | --- |
| Déploiement Exchange hybride |Hello déploiement Exchange hybride fonctionnalité permet la coexistence de hello boîtes aux lettres Exchange à la fois localement et dans Office 365. Azure AD Connect synchronise un ensemble spécifique d’[attributs](active-directory-aadconnectsync-attributes-synchronized.md#exchange-hybrid-writeback) d’Azure AD dans votre annuaire local. |
| Dossiers publics de messagerie Exchange | fonctionnalité de dossiers publics de messagerie Exchange Hello vous permet de toosynchronize objets de dossier Public à extension messagerie à partir de votre tooAzure d’Active Directory sur site Active Directory. |
| Application Azure AD et filtrage des attributs |En activant l’application Azure AD et filtrage des attributs, hello ensemble d’attributs synchronisés peut être adapté. Cette option ajoute deux plus Assistant configuration des pages toohello. Pour en savoir plus, voir [Application Azure AD et filtrage des attributs](#azure-ad-app-and-attribute-filtering). |
| Synchronisation de mot de passe |Si vous avez sélectionné la fédération comme solution de connexion hello, vous pouvez activer cette option. La synchronisation de mot de passe peut ensuite servir d’option de sauvegarde. Pour en savoir plus, voir [Synchronisation de mot de passe](active-directory-aadconnectsync-implement-password-synchronization.md). </br></br>Si vous avez sélectionné l’authentification directe, cette option est activée par défaut de la prise en charge de tooensure pour les clients hérités et comme option de sauvegarde. Pour en savoir plus, voir [Synchronisation de mot de passe](active-directory-aadconnectsync-implement-password-synchronization.md).|
| Réécriture du mot de passe |En activant l’écriture différée de mot de passe, les modifications de mot de passe qui proviennent de Azure AD sont réécrites tooyour locale active. Pour en savoir plus, voir [Prise en main de la gestion de mot de passe](../active-directory-passwords-getting-started.md). |
| Écriture différée de groupe |Si vous utilisez hello **les groupes Office 365** fonctionnalité, vous pouvez avoir ces groupes représentés dans votre annuaire Active Directory local. Cette option n’est disponible que si Exchange est présent dans votre annuaire Active Directory local. Pour en savoir plus, voir [Écriture différée de groupe](active-directory-aadconnect-feature-preview.md#group-writeback). |
| Écriture différée des appareils |Permet aux objets d’appareil toowriteback dans Azure AD tooyour locale Active Directory pour les scénarios d’accès conditionnel. Pour en savoir plus, voir [Azure AD Connect : Activation de l’écriture différée des appareils](active-directory-aadconnect-feature-device-writeback.md). |
| Synchronisation des attributs des extensions d’annuaire |En activant la synchronisation Active extensions d’attribut, les attributs spécifiés sont synchronisé tooAzure AD. Pour en savoir plus, voir [Extensions d’annuaire](active-directory-aadconnectsync-feature-directory-extensions.md). |

### <a name="azure-ad-app-and-attribute-filtering"></a>Application Azure AD et filtrage des attributs
Si vous souhaitez toolimit le tooAzure de toosynchronize d’attributs Active Directory, commencez par sélectionner les services que vous utilisez. Si vous apportez des modifications de configuration sur cette page, un nouveau service a toobe explicitement sélectionnée en réexécutant l’Assistant installation hello.

![Fonctionnalités facultatives - Applications](./media/active-directory-aadconnect-get-started-custom/azureadapps2.png)

Selon les services hello sélectionnés à l’étape précédente de hello, cette page affiche tous les attributs qui sont synchronisés. Cette liste est une combinaison de tous les types d’objet en cours de synchronisation. S’il existe des attributs particuliers que vous avez besoin de toonot synchroniser, vous pouvez désélectionner ces attributs.

![Fonctionnalités facultatives - Attributs](./media/active-directory-aadconnect-get-started-custom/azureadattributes2.png)

> [!WARNING]
> La suppression d’attributs peut affecter la fonctionnalité. Pour consulter des recommandations et meilleures pratiques, voir [Attributs synchronisés](active-directory-aadconnectsync-attributes-synchronized.md#attributes-to-synchronize).
>
>

### <a name="directory-extension-attribute-sync"></a>Synchronisation des attributs des extensions d’annuaire
Vous pouvez étendre le schéma de hello dans Azure AD avec des attributs personnalisés ajoutés par votre organisation ou d’autres attributs dans Active Directory. toouse cette fonctionnalité, sélectionnez **synchronisation d’attribut Extension active** sur hello **fonctionnalités facultatives** page. Vous pouvez sélectionner plusieurs attributs toosync, sur cette page.

![Extensions d’annuaire](./media/active-directory-aadconnect-get-started-custom/extension2.png)

Pour en savoir plus, voir [Extensions d’annuaire](active-directory-aadconnectsync-feature-directory-extensions.md).

### <a name="enabling-single-sign-on-sso"></a>Activation de l’authentification unique (SSO)
Configuration de l’authentification unique pour une utilisation avec l’authentification de la synchronisation de mot de passe ou Pass-Through est un processus simple que vous n’avez toocomplete qu’une seule fois pour chaque forêt qui est en cours de synchronisation tooAzure AD. La configuration implique les deux étapes suivantes :

1.  Créer le compte d’ordinateur nécessaires hello dans votre annuaire Active Directory local.
2.  Configurer zone intranet de hello des ordinateurs de client hello toosupport unique de session.

#### <a name="create-hello-computer-account-in-active-directory"></a>Créer un compte d’ordinateur hello dans Active Directory
Pour chaque forêt qui a été ajoutée dans Azure AD Connect, vous devez toosupply droits d’administrateur de domaine afin que le compte d’ordinateur hello peut être créé dans chaque forêt. informations d’identification Hello sont uniquement le compte de hello toocreate utilisé et ne sont pas stockées ou utilisées pour toute autre opération. Ajoutez simplement les informations d’identification hello sur hello **activer unique connectent** page d’Assistant de connexion hello Azure AD comme indiqué :

![Activer l'authentification unique](./media/active-directory-aadconnect-get-started-custom/enablesso.png)

>[!NOTE]
>Vous pouvez ignorer une forêt particulière si vous ne souhaitez pas toouse l’authentification unique avec cette forêt.

#### <a name="configure-hello-intranet-zone-for-client-machines"></a>Configurer la Zone Intranet de hello pour les ordinateurs clients
tooensure hello client connexions automatiquement dans l’intranet de hello de zone vous devez tooensure que deux URL font partie de la zone intranet de hello. Cela garantit que cet ordinateur joint au domaine de hello envoie automatiquement un tooAzure de ticket Kerberos AD lorsqu’il est connecté toohello réseau d’entreprise.
Sur un ordinateur qui dispose d’outils de gestion de stratégie de groupe hello.

1.  Ouvrir les outils de gestion des stratégies de groupe hello
2.  Modifier la stratégie de groupe hello qui est appliqués tooall utilisateurs. Bonjour, par exemple, la stratégie de domaine par défaut.
3.  Accédez trop**Page Panel\Security de contrôle utilisateur Configuration ordinateur\Modèles d’administration\Composants Windows\Internet Explorer\Panneau** et sélectionnez **tooZone liste d’attribution de Site** par image de hello ci-dessous.
4.  Activer la stratégie hello et entrez hello deux éléments dans la boîte de dialogue hello suivants.

        Value: `https://autologon.microsoftazuread-sso.com`  
        Data: 1  
        Value: `https://aadg.windows.net.nsatc.net`  
        Data: 1

5.  Il doit se présenter comme toohello suivantes :  
![Zones intranet](./media/active-directory-aadconnect-get-started-custom/sitezone.png)

6.  Cliquez sur **OK** deux fois.

## <a name="configuring-federation-with-ad-fs"></a>Configuration de la fédération avec AD FS
La configuration d’AD FS avec Azure AD Connect s’effectue simplement en quelques clics. suivant de Hello est requis avant la configuration de hello.

* Un serveur Windows Server 2012 R2 pour le serveur de fédération hello avec la gestion à distance activé
* Un serveur Windows Server 2012 R2 pour le serveur de Proxy d’Application Web hello avec la gestion à distance activée
* Un certificat SSL pour la fédération de hello service nom que vous avez l’intention de toouse (par exemple sts.contoso.com)

### <a name="ad-fs-configuration-pre-requisites"></a>Conditions préalables à la configuration AD FS
tooconfigure AD FS à l’aide d’Azure AD Connect de batterie de serveurs, assurez-vous que WinRM est activée sur les serveurs distants hello. En outre, passent par la spécification de ports hello répertoriée dans [Table 3 - Azure AD Connect et les serveurs de fédération/WAP](active-directory-aadconnect-ports.md#table-3---azure-ad-connect-and-ad-fs-federation-serverswap).

### <a name="create-a-new-ad-fs-farm-or-use-an-existing-ad-fs-farm"></a>Création d’une batterie de serveurs AD FS ou utilisation d’une batterie de serveurs AD FS existante
Vous pouvez utiliser une batterie de serveurs AD FS existante, ou vous pouvez choisir toocreate une nouvelle batterie AD FS. Si vous choisissez toocreate un nouveau, vous êtes certificat SSL de hello tooprovide requis. Si le certificat SSL de hello est protégé par un mot de passe, vous êtes invité pour un mot de passe hello.

![Batterie de serveurs ADFS](./media/active-directory-aadconnect-get-started-custom/adfs1.png)

Si vous choisissez toouse une batterie AD FS existante, vous accédez directement toohello relation d’approbation hello entre AD FS et Azure écran de configuration.

### <a name="specify-hello-ad-fs-servers"></a>Spécifiez les serveurs hello AD FS
Entrez hello les serveurs que vous voulez tooinstall AD FS sur. Vous pouvez ajouter un ou plusieurs serveurs selon vos besoins de planification de capacité. Joignez tous les serveurs tooActive active avant d’effectuer cette configuration. Microsoft recommande d’installer un seul serveur AD FS pour les déploiements de test et pilote. Ajouter, puis déployer plusieurs serveurs toomeet à vos besoins de mise à l’échelle en exécutant Azure AD Connect à nouveau après la configuration initiale.

> [!NOTE]
> Assurez-vous que tous vos serveurs sont jointes tooan AD domaine avant de procéder à cette configuration.
>
>

![Serveurs AD FS](./media/active-directory-aadconnect-get-started-custom/adfs2.png)

### <a name="specify-hello-web-application-proxy-servers"></a>Spécifiez les serveurs Proxy d’Application Web hello
Entrez les serveurs de hello que vous souhaitez que vos serveurs de proxy d’Application Web. la serveur Hello pour le proxy d’application web est déployée dans votre réseau de périmètre (accès extranet) et prend en charge les demandes d’authentification à partir de hello extranet. Vous pouvez ajouter un ou plusieurs serveurs selon vos besoins de planification de capacité. Microsoft recommande d’installer un serveur proxy d’application web unique pour un déploiement de test ou pilote. Ajouter, puis déployer plusieurs serveurs toomeet à vos besoins de mise à l’échelle en exécutant Azure AD Connect à nouveau après la configuration initiale. Nous vous recommandons d’avoir un nombre équivalent de l’authentification toosatisfy de serveurs proxy à partir de l’intranet de hello.

> [!NOTE]
> <li> Si le compte que vous utilisez hello n’est pas un administrateur local sur les serveurs de hello AD FS, vous êtes invité pour les informations d’identification d’administrateur.</li>
> <li> Vérifiez qu’il existe connectivité HTTP/HTTPS entre serveurs de Azure AD Connect hello et hello Proxy d’Application Web avant d’exécuter cette étape.</li>
> <li> Assurez-vous qu’il existe une connectivité HTTP/HTTPS entre hello serveur d’applications Web et les demandes hello AD FS server tooallow authentification tooflow via.</li>
>

![Application web](./media/active-directory-aadconnect-get-started-custom/adfs3.png)

Vous sont des informations d’identification demandées par invite tooenter afin que hello serveur d’applications web peut établir un serveur de connexion sécurisée toohello AD FS. Ces informations d’identification doivent toobe un administrateur local sur le serveur AD FS de hello.

![Proxy](./media/active-directory-aadconnect-get-started-custom/adfs4.png)

### <a name="specify-hello-service-account-for-hello-ad-fs-service"></a>Spécifiez le compte de service hello pour hello service AD FS
service de Hello AD FS requiert un domaine de service aux utilisateurs de compte tooauthenticate et les informations utilisateur de recherche dans Active Directory. Il prend en charge 2 types de compte de service :

* **Compte de service géré de groupe** : il a été introduit dans les services de domaine Active Directory avec Windows Server 2012. Ce type de compte fournit des services, tels que AD FS, un seul compte sans avoir besoin de mot de passe de compte tooupdate hello régulièrement. Utilisez cette option si vous avez déjà des contrôleurs de domaine Windows Server 2012 dans le domaine hello appartenant à vos serveurs AD FS.
* **Compte d’utilisateur de domaine** -ce type de compte requiert vous tooprovide un mot de passe et régulièrement mises à jour un mot de passe hello lorsque le mot de passe hello change ou expire. Utilisez cette option uniquement lorsque vous n’avez pas de contrôleurs de domaine Windows Server 2012 dans le domaine hello appartenant à vos serveurs AD FS.

Si vous avez sélectionné le compte de service géré de groupe et que cette fonctionnalité n’a jamais été utilisée dans Active Directory, vous êtes invité à saisir des informations d’identification d’administrateur d’entreprise. Ces informations d’identification sont des magasins de clés utilisée tooinitiate hello et activer la fonctionnalité hello dans Active Directory.

> [!NOTE]
> Azure AD Connect effectue une vérification toodetect si le service de hello AD FS est déjà inscrit en tant qu’un SPN dans le domaine de hello.  Les services AD DS n’autorisera pas toobe du nom SPN en double inscrit à la fois.  Si un nom SPN en double est trouvé, vous ne serez pas en mesure de tooproceed plus jusqu'à ce que hello SPN est supprimé.

![Compte de service AD FS ](./media/active-directory-aadconnect-get-started-custom/adfs5.png)

### <a name="select-hello-azure-ad-domain-that-you-wish-toofederate"></a>Sélectionnez le domaine hello Azure AD que vous souhaitez toofederate
Cette configuration est la relation de fédération hello toosetup utilisé entre AD FS et Azure AD. Il configure les services AD FS tooissue sécurité jetons tooAzure AD et configure les jetons Azure AD tootrust hello à partir de cette instance d’AD FS spécifique. Cette page vous permet uniquement tooconfigure un domaine unique dans l’installation initiale de hello. Vous pouvez configurer ultérieurement des domaines supplémentaires en réexécutant Azure AD Connect.

![Domaine Azure AD](./media/active-directory-aadconnect-get-started-custom/adfs6.png)

### <a name="verify-hello-azure-ad-domain-selected-for-federation"></a>Vérifier le domaine Azure AD de hello sélectionné pour la fédération
Lorsque vous sélectionnez hello toobe de domaine fédéré, Azure AD Connect vous fournit des informations nécessaires tooverify un domaine non vérifié. Consultez [ajouter et vérifier le domaine de hello](../active-directory-add-domain.md) procédure toouse ces informations.

![Domaine Azure AD](./media/active-directory-aadconnect-get-started-custom/verifyfeddomain.png)

> [!NOTE]
> Configuration de domaine Active Directory Connect tentatives tooverify hello pendant hello étape. Si vous continuez tooconfigure sans ajouter les enregistrements DNS nécessaires hello, Assistant de hello est pas en mesure de toocomplete hello.
>
>

## <a name="configure-and-verify-pages"></a>Pages de configuration et de vérification
configuration de Hello se produit sur cette page.

> [!NOTE]
> Avant de poursuivre l’installation, si vous avez configuré la fédération, vérifiez que vous avez défini la fonction de [résolution de noms pour les serveurs de fédération](active-directory-aadconnect-prerequisites.md#name-resolution-for-federation-servers).
>
>

![Tooconfigure prêt](./media/active-directory-aadconnect-get-started-custom/readytoconfigure2.png)

### <a name="staging-mode"></a>Mode intermédiaire
Il est possible de toosetup un nouveau serveur de synchronisation en parallèle avec le mode de mise en lots. Il est uniquement pris en charge toohave un serveur de synchronisation exportation répertoire tooone dans le cloud de hello. Mais si vous souhaitez toomove à partir d’un autre serveur, par exemple une synchronisation d’annuaire en cours d’exécution, vous pouvez activer Azure AD Connect dans le mode de mise en lots. Lorsque activé, la synchronisation hello moteur importer et synchroniser les données comme d’habitude, mais il n’exporte pas quoi que ce soit tooAzure AD ou AD. Hello fonctionnalités mot de passe mot de passe et synchronisation de l’écriture différée sont désactivées en mode de mise en lots.

![Mode intermédiaire](./media/active-directory-aadconnect-get-started-custom/stagingmode.png)

En mode de mise en lots, il est le moteur de synchronisation toohello toomake possible les modifications requises et passez en revue les nouveautés sur toobe exporté. Lors de la configuration de hello semble correcte, réexécutez l’Assistant installation de hello et désactiver le mode de mise en lots. Les données sont désormais exporté tooAzure AD à partir de ce serveur. Assurez-vous que toodisable hello autre serveur à hello même ainsi qu’un seul serveur activement consiste à exporter.

Pour en savoir plus, voir [Mode intermédiaire](active-directory-aadconnectsync-operations.md#staging-mode).

### <a name="verify-your-federation-configuration"></a>Vérification de votre configuration de fédération
Azure AD Connect vérifie les paramètres DNS de hello pour vous lorsque vous cliquez sur le bouton vérifier la hello.

**Vérifications de la connectivité intranet**

* Résoudre le nom de domaine complet de fédération : Azure AD Connect vérifie si le fédération hello nom de domaine complet peut être résolu par une connectivité tooensure DNS. Si Azure AD Connect ne peut pas résoudre le nom de domaine complet de hello, vérification de hello échoue. Vérifiez qu’un enregistrement DNS est présent pour le service de fédération de hello nom de domaine complet dans la vérification de commande toosuccessfully hello terminée.
* Enregistrement A DNS : Azure AD Connect vérifie s’il existe un enregistrement A pour votre service de fédération. En absence de hello d’un enregistrement A, la vérification de hello échoue. Créer un enregistrement et non CNAME pour votre nom de domaine complet de la fédération dans l’ordre toosuccessfully terminer la vérification de hello.

**Vérifications de la connectivité extranet**

* Résoudre le nom de domaine complet de fédération : Azure AD Connect vérifie si le fédération hello nom de domaine complet peut être résolu par une connectivité tooensure DNS.

![Complete](./media/active-directory-aadconnect-get-started-custom/completed.png)

![Vérifier](./media/active-directory-aadconnect-get-started-custom/adfs7.png)

En outre, effectuer hello vérification comme suit :

* Valider que vous pouvez vous connecter à partir d’un navigateur à partir d’un ordinateur joint à un domaine sur l’intranet hello : se connecter toohttps://myapps.microsoft.com et vérifiez hello connectez-vous avec votre compte connecté. compte d’administrateur Hello intégré AD DS n’est pas synchronisé et ne peut pas être utilisé pour la vérification.
* Vérifiez que vous pouvez vous connecter à partir d’un appareil à partir de hello extranet. Sur un ordinateur personnel ou un appareil mobile, vous connecter toohttps://myapps.microsoft.com et fournissez vos informations d’identification.
* Valider la connexion à un client complet. Se connecter toohttps://testconnectivity.microsoft.com, choisissez hello **Office 365** hello onglet, puis choisissez **Office 365 Sign-On Test unique**.

## <a name="next-steps"></a>Étapes suivantes
Après installation Bonjour, se déconnecter et se connecter à nouveau tooWindows avant d’utiliser le Gestionnaire de Service de synchronisation ou l’éditeur de règles de synchronisation.

Maintenant que vous avez Azure AD Connect installée, vous pouvez [vérifier l’installation de hello et attribuer des licences](active-directory-aadconnect-whats-next.md).

En savoir plus sur ces fonctionnalités, qui ont été activées avec l’installation de hello : [empêcher des suppressions accidentelles](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) et [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

En savoir plus sur ces sujets courants : [planificateur et comment synchroniser les tootrigger](active-directory-aadconnectsync-feature-scheduler.md).

En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).
