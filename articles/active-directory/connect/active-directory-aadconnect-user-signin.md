---
title: "Azure AD Connect : Connexion utilisateur | Microsoft Docs"
description: "Connexion utilisateur Azure AD Connect pour une configuration personnalisée."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 547b118e-7282-4c7f-be87-c035561001df
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 7848b419f3855b25cfa074a46779d258bd534bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-user-sign-in-options"></a>Options de connexion de l’utilisateur via Azure AD Connect
Azure Connect d’Active Directory (Azure AD) permet à votre toosign les utilisateurs dans le cloud de tooboth et des ressources locales à l’aide de hello mêmes mots de passe. Cet article décrit des concepts clés pour chaque toohelp de modèle d’identité que vous choisissez hello identité toouse pour établir la connexion tooAzure AD.

Si vous êtes déjà familiarisé avec le modèle d’identité Azure AD hello et que vous souhaitez toolearn plus d’informations sur une méthode spécifique, consultez le lien approprié de hello :

* [Synchronisation de mot de passe](#password-synchronization) avec [authentification unique (SSO)](active-directory-aadconnect-sso.md)
* [Authentification directe](active-directory-aadconnect-pass-through-authentication.md)
* [Authentification unique fédérée (avec Active Directory Federation Services (AD FS))](#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)

## <a name="choosing-hello-user-sign-in-method-for-your-organization"></a>En choisissant l’option hello utilisateur méthode d’authentification pour votre organisation
La plupart des organisations qui intéresse tooenable utilisateur connectez-vous tooOffice 365 applications SaaS et autres ressources Azure basée sur Active Directory, nous vous recommandons de l’option de synchronisation de mot de passe par défaut hello. Toutefois, certaines organisations, n’ont une raison de particulier qu’ils ne sont pas en mesure de toouse cette option. Elles peuvent choisir une option de connexion fédérée, comme AD FS, ou l’authentification directe. Vous pouvez utiliser hello suivant toohelp table vous apportez choix hello.

J’ai besoin de trop| PS avec l’authentification unique| PA avec l’authentification unique| AD FS |
 --- | --- | --- | --- |
Synchroniser automatiquement le nouvel utilisateur, contact et comptes de groupe dans le cloud de toohello Active Directory local.|x|x|x|
Configurer mon client pour des scénarios hybrides Office 365.|x|x|x|
Activer mon toosign utilisateurs dans et les services de cloud d’accès à l’aide de leur mot de passe local.|x|x|x|
Implémenter l’authentification unique à l’aide des informations d’identification d’entreprise.|x|x|x|
Assurez-vous qu’aucun mot de passe n’est stockées dans le cloud de hello.||x*|x|
Activer des solutions d’authentification multifacteur locales.|||x|

*Via un connecteur léger.

>[!NOTE]
> L’authentification directe présente actuellement des limitations concernant les clients riches. Pour plus d’informations, consultez [Authentification directe](active-directory-aadconnect-pass-through-authentication.md).

### <a name="password-synchronization"></a>Synchronisation de mot de passe
Lorsque la synchronisation de mot de passe, les hachages des mots de passe utilisateur sont synchronisés à partir de tooAzure d’Active Directory sur site Active Directory. Lorsque des mots de passe sont modifiés ou réinitialiser local, des mots de passe hello sont synchronisé tooAzure AD immédiatement afin que vos utilisateurs peuvent toujours utiliser hello même mot de passe pour les ressources de cloud et les ressources locales. les mots de passe Hello ne sont jamais envoyés tooAzure AD ou stockés dans Azure AD en texte clair. Vous pouvez utiliser la synchronisation de mot de passe avec mot de passe tooenable d’écriture différée de mot de passe libre-service réinitialiser dans Azure AD.

En outre, vous pouvez activer [SSO](active-directory-aadconnect-sso.md) pour les utilisateurs sur des ordinateurs joints à un domaine qui se trouvent sur le réseau d’entreprise de hello. Avec l’authentification unique, activé les utilisateurs uniquement besoin de tooenter un toohelp de nom d’utilisateur les accès sécurisé aux ressources de cloud.

![Synchronisation de mot de passe](./media/active-directory-aadconnect-user-signin/passwordhash.png)

Pour plus d’informations, consultez hello [synchronisation de mot de passe](active-directory-aadconnectsync-implement-password-synchronization.md) l’article.

### <a name="pass-through-authentication"></a>Authentification directe
Avec l’authentification directe, hello mot de passe utilisateur est validé par rapport à contrôleur d’Active Directory local hello. mot de passe Hello n’a pas besoin toobe présent dans Azure AD dans n’importe quelle forme. Ainsi, pour les stratégies locales, telles que des restrictions sur les heures de connexion toobe évaluée au cours des services d’authentification toocloud.

Authentification directe utilise un agent simple sur un ordinateur joint au domaine de Windows Server 2012 R2 dans l’environnement local de hello. Cet agent écoute les requêtes de validation de mot de passe. Il ne nécessite pas tout toobe de ports entrants ouverts toohello Internet.

En outre, vous pouvez également activer l’authentification unique pour les utilisateurs sur des ordinateurs joints à un domaine qui se trouvent sur le réseau d’entreprise de hello. Avec l’authentification unique, activé les utilisateurs uniquement besoin de tooenter un toohelp de nom d’utilisateur les accès sécurisé aux ressources de cloud.
![Authentification directe](./media/active-directory-aadconnect-user-signin/pta.png)

Pour plus d'informations, consultez les pages suivantes :
- [Authentification directe](active-directory-aadconnect-pass-through-authentication.md)
- [Authentification unique](active-directory-aadconnect-sso.md)

### <a name="federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2"></a>Fédération utilisant des services AD FS nouveaux ou existants dans la batterie de serveurs Windows Server 2012 R2
Avec fédérée connexion, vos utilisateurs peuvent se connecter tooAzure basée sur Active Directory des services avec leurs mots de passe local. Lorsqu’ils sont sur le réseau d’entreprise de hello, ils n’ont pas tooenter leurs mots de passe. En utilisant l’option de fédération hello avec AD FS, vous pouvez déployer une batterie de serveurs nouvelle ou existante avec AD FS dans Windows Server 2012 R2. Si vous choisissez toospecify une batterie de serveurs existante, Azure AD Connect configure hello une approbation entre votre batterie de serveurs et les Azure AD afin que vos utilisateurs peuvent se connecter.

<center>![Fédération avec AD FS dans Windows Server 2012 R2](./media/active-directory-aadconnect-user-signin/federatedsignin.png)</center>

#### <a name="deploy-federation-with-ad-fs-in-windows-server-2012-r2"></a>Déploiement d’une fédération avec AD FS dans Windows Server 2012 R2

Si vous déployez une nouvelle batterie, il vous faut :

* Un serveur Windows Server 2012 R2 pour serveur de fédération hello.
* Un serveur Windows Server 2012 R2 pour hello Proxy d’Application Web.
* Un fichier .pfx avec un certificat SSL unique pour le nom de votre service de fédération. Par exemple : fs.contoso.com.

Si vous déployez une nouvelle batterie ou si vous utilisez une batterie existante, il vous faut :

* Les informations d’identification de l’administrateur local de vos serveurs de fédération.
* Informations d’identification administrateur local sur tous les serveurs du groupe de travail (non joints au domaine) que vous avez l’intention toodeploy hello rôle Proxy d’Application Web sur.
* ordinateur Hello que vous exécutez hello Assistant sur toobe tooconnect en mesure de tooany autres ordinateurs que vous souhaitez tooinstall AD FS ou sur le Proxy d’Application Web à l’aide de gestion à distance de Windows.

Pour plus d’informations, consultez [Configuration de l’authentification unique avec ADFS](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs).

#### <a name="sign-in-by-using-an-earlier-version-of-ad-fs-or-a-third-party-solution"></a>Authentification à l’aide d’une version antérieure d’AD FS ou d’une solution tierce
Si vous avez déjà configuré cloud connectez-vous à l’aide d’une version antérieure des services AD FS (par exemple, les services AD FS 2.0) ou d’un fournisseur de fédération de tiers, vous pouvez choisir tooskip signe dans configuration de l’utilisateur via Azure AD Connect. Cela vous permettra dernière synchronisation de tooget hello et d’autres fonctionnalités d’Azure AD Connect tout en utilisant votre solution existante pour la connexion.

Pour plus d’informations, consultez hello [liste de compatibilité de fédération de l’application tierce Azure AD](active-directory-aadconnect-federation-compatibility.md).


## <a name="user-sign-in-and-user-principal-name"></a>Connexion de l’utilisateur et nom d’utilisateur principal
### <a name="understanding-user-principal-name"></a>Présentation du nom d’utilisateur principal
Dans Active Directory, hello par défaut suffixe nom utilisateur principal (UPN) est le nom DNS de hello du domaine hello où le compte d’utilisateur hello a été créé. Dans la plupart des cas, cela est nom de domaine hello est inscrit en tant que domaine d’entreprise hello sur hello Internet. Toutefois, vous pouvez ajouter d’autres suffixes UPN avec les domaines et approbations Active Directory.

Hello UPN de hello utilisateur a le format de hello username@domain. Par exemple, pour un domaine Active Directory nommé « contoso.com », un utilisateur nommé John peut-être hello UPN «john@contoso.com». Hello UPN de l’utilisateur de hello est basée sur RFC 822. Bien que hello UPN et le partage de courrier électronique hello même format, la valeur hello Hello UPN pour un utilisateur peut ou peut ne pas être la même hello en tant qu’adresse de messagerie hello d’utilisateur de hello.

### <a name="user-principal-name-in-azure-ad"></a>Nom d’utilisateur principal dans Azure AD
Assistant d’Azure AD Connect Hello utilise l’attribut userPrincipalName de hello ou vous permet de que spécifier hello toobe attribut (dans une installation personnalisée) utilisée sur site en tant que nom d’utilisateur principal hello dans Azure AD. Il s’agit de valeur hello qui est utilisé pour établir la connexion tooAzure AD. Si la valeur hello de l’attribut userPrincipalName de hello ne correspond pas tooa vérifié domaine dans Azure AD, Azure AD remplace par une valeur par défaut. onmicrosoft.com valeur.

Chaque annuaire dans Azure Active Directory est fourni avec un nom de domaine intégré, avec hello format contoso.onmicrosoft.com, qui vous permet de commencer à l’aide de Azure ou autres services Microsoft. Vous pouvez améliorer et simplifier l’expérience de connexion hello à l’aide de domaines personnalisés. Pour plus d’informations sur les noms de domaines personnalisés dans Azure AD et comment tooverify un domaine, consultez [ajouter votre tooAzure de nom de domaine personnalisé Active Directory](../add-custom-domain.md#add-your-custom-domain).

## <a name="azure-ad-sign-in-configuration"></a>Configuration de connexion AD Azure
### <a name="azure-ad-sign-in-configuration-with-azure-ad-connect"></a>Configuration de connexion AD Azure avec Azure AD Connect
expérience de connexion Hello AD Azure dépend de si Azure AD peut correspondre suffixe UPN hello d’un utilisateur qui est en cours tooone synchronisé de domaines personnalisés hello qui sont vérifiées dans Windows Azure AD hello. Azure AD Connect fournit une aide lorsque vous configurez des paramètres de connexion Azure AD, afin que hello utilisateur expérience de connexion dans le cloud de hello est local de toohello similaire.

Azure AD Connect listes hello suffixes UPN qui sont définies pour toomatch domaines et les tentatives de hello avec un domaine personnalisé dans Azure AD. Puis il vous aide à vous par l’action appropriée hello nécessitant toobe prise.
Bonjour Azure AD-page de connexion répertorie les suffixes UPN hello qui sont définis pour Active Directory local et affiche l’état de correspondante hello par rapport à chaque suffixe. valeurs d’état Hello peuvent être hello suivantes :

| State | Description | Action requise |
|:--- |:--- |:--- |
| Verified |Azure AD Connect a trouvé un domaine vérifié correspondant dans Azure AD. Tous les utilisateurs de ce domaine peuvent se connecter en utilisant leurs informations d’identification locales. |Aucune action n'est nécessaire. |
| Non vérifié |Azure AD Connect a trouvé un domaine personnalisé correspondant dans Azure AD mais il n’est pas vérifié. suffixe UPN Hello utilisateurs hello de ce domaine sera modifié la valeur par défaut toohello. suffixe onmicrosoft.com après la synchronisation si hello n’est pas vérifié. | [Vérifiez le domaine personnalisé de hello dans Azure AD.](../add-custom-domain.md#verify-the-domain-name-with-azure-ad) |
| Non ajouté |Azure AD Connect n’a pas trouvé un domaine personnalisé suffixe UPN toohello correspondaient. suffixe UPN Hello utilisateurs hello de ce domaine sera modifié la valeur par défaut toohello. onmicrosoft.com suffixe si le domaine de hello n’est pas ajouté et vérifié dans Azure. | [Ajouter et vérifier un domaine personnalisé qui correspond le suffixe toohello.](../add-custom-domain.md) |

Bonjour Azure AD-page de connexion répertorie les suffixes UPN hello qui sont définis pour Active Directory local et hello correspondant domaine personnalisé dans Azure AD avec l’état de vérification en cours hello. Dans une installation personnalisée, vous pouvez maintenant sélectionner attribut hello hello nom d’utilisateur principal sur hello **signe dans Azure AD** page.

![Page de connexion d’Azure AD](./media/active-directory-aadconnect-user-signin/custom_azure_sign_in.png)

Vous pouvez cliquer sur hello actualisation bouton toore-extraction hello état le plus récent de domaines personnalisés de hello d’Azure AD.

### <a name="selecting-hello-attribute-for-hello-user-principal-name-in-azure-ad"></a>Sélection d’attribut hello pour le nom d’utilisateur principal hello dans Azure AD
Hello attribut userPrincipalName est l’attribut hello que les utilisateurs utilisent quand ils se connectent tooAzure AD et Office 365. Vous devez vérifier les domaines de hello (également connu sous les suffixes UPN) qui sont utilisés dans Azure AD avant que les utilisateurs de hello sont synchronisés.

Nous vous recommandons vivement de conserver hello par défaut attribut userPrincipalName. Si cet attribut est nonroutable et ne peut pas être vérifié, il est possible de tooselect un autre attribut (courrier électronique, par exemple) en tant qu’attribut hello conserve hello nom de connexion. Il s’agit hello ID de remplacement. valeur d’attribut d’un autre ID de Hello doit suivre hello RFC 822 standard. Vous pouvez utiliser un autre ID avec le mot de passe SSO et fédération SSO comme solution de connexion hello.

> [!NOTE]
> L’utilisation d’un ID secondaire n’est pas compatible avec toutes les charges de travail Office 365. Pour plus d’informations, consultez [Configuration d’un ID secondaire de connexion](https://technet.microsoft.com/library/dn659436.aspx).
>
>

#### <a name="different-custom-domain-states-and-their-effect-on-hello-azure-sign-in-experience"></a>États de l’autre domaine personnalisé et leur effet sur l’expérience hello signe dans Azure
Il s’agit de relation de hello toounderstand très important entre les États de domaine personnalisé de hello dans votre annuaire Azure AD et hello suffixes UPN qui sont définis localement. Examinons hello différentes possibles Azure connectez-vous expériences lorsque vous configurez la synchronisation à l’aide d’Azure AD Connect.

Pourquoi les informations suivantes, supposons que nous intéressent hello UPN suffixe contoso.com, qui est utilisé dans le répertoire local de hello en tant que partie de l’UPN--par exemple user@contoso.com.

###### <a name="express-settingspassword-synchronization"></a>Configuration rapide / Synchronisation de mot de passe
| State | Effet sur l’expérience de connexion utilisateur Azure |
|:---:|:--- |
| Non ajouté |Dans ce cas, aucun domaine personnalisé pour contoso.com n’a été ajoutée dans Windows Azure AD hello. Les utilisateurs qui ont l’UPN local avec le suffixe de hello @contoso.com ne sera pas en mesure de toouse leur toosign de nom UPN local dans tooAzure. Allez à la place sont-ils toouse un nouvel UPN qui a fourni toothem par Azure AD en ajoutant le suffixe hello pour hello par défaut Windows Azure AD. Par exemple, si vous synchronisez les utilisateurs toohello Azure AD directory azurecontoso.onmicrosoft.com, puis hello sur site utilisateur user@contoso.com a un UPN de user@azurecontoso.onmicrosoft.com. |
| Non vérifié |Dans ce cas, nous avons contoso.com un domaine personnalisé qui est ajouté dans le répertoire de hello Azure AD. Toutefois, la vérification n’est pas encore effectuée. Si vous poursuivez avec la synchronisation des utilisateurs sans vérification de domaine de hello, puis les utilisateurs hello recevra un nouvel UPN par Azure AD, comme Bonjour « Pas ajoutées » le scénario. |
| Verified |Dans ce cas, nous avons un domaine personnalisé de contoso.com qui a déjà ajouté et vérifié dans Azure AD pour hello suffixe UPN. Les utilisateurs est en mesure de toouse leur nom d’utilisateur principal local, par exemple user@contoso.com, toosign dans tooAzure une fois qu’ils sont synchronisés tooAzure AD. |

###### <a name="ad-fs-federation"></a>Fédération AD FS
Impossible de créer une fédération avec la valeur par défaut hello. domaine onmicrosoft.com dans Azure AD ou un domaine non vérifié personnalisé dans Azure AD. Lorsque vous exécutez Assistant de connexion hello Azure AD, si vous sélectionnez un domaine non vérifié de toocreate une fédération avec, Azure AD Connect demande ensuite vous hello nécessaire enregistre toobe créé dans lequel il est hébergé votre DNS pour le domaine de hello. Pour plus d’informations, consultez [vérifier le domaine Azure AD de hello sélectionné pour la fédération](active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation).

Si vous avez sélectionné l’option d’authentification de l’utilisateur du hello **fédération avec AD FS**, vous devez disposer d’un toocontinue de domaine personnalisé Création d’une fédération dans Azure AD. Pour notre présentation, cela signifie que nous devrions obtenir un domaine personnalisé est contoso.com ajouté dans le répertoire de hello Azure AD.

| State | Effet sur l’expérience utilisateur dans l’authentification Azure hello |
|:---:|:--- |
| Non ajouté |Dans ce cas, Azure AD Connect n’a pas trouvé un domaine personnalisé correspondant pour hello contoso.com de suffixe UPN dans Windows Azure AD hello. Vous devez tooadd un domaine personnalisé est contoso.com, si vous avez besoin de toosign d’utilisateurs dans à l’aide des services AD FS avec leur UPN local (comme user@contoso.com). |
| Non vérifié |Dans ce cas, Azure AD Connect vous fournira les informations appropriées sur les possibilités de vérification de votre domaine à un stade ultérieur. |
| Verified |Dans ce cas, vous pouvez commencer avec configuration hello sans autre intervention. |

## <a name="changing-hello-user-sign-in-method"></a>Modifier la méthode d’authentification de l’utilisateur du hello
Vous pouvez modifier la méthode d’authentification de l’utilisateur du hello à partir de la fédération, la synchronisation de mot de passe ou l’authentification directe à l’aide de tâches hello qui sont disponibles dans Azure AD Connect après hello la configuration initiale d’Azure AD Connect avec l’Assistant de hello. Réexécutez l’Assistant d’Azure AD Connect hello, et vous verrez une liste de tâches que vous pouvez effectuer. Sélectionnez **modifier la connexion d’utilisateur** à partir de la liste des tâches hello.

![Modifier la connexion de l’utilisateur](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

Sur la page suivante de hello, vous devez indiquer des informations d’identification de tooprovide hello pour Azure AD.

![Se connecter tooAzure AD](./media/active-directory-aadconnect-user-signin/changeusersignin2.png)

Sur hello **connexion d’utilisateur** , sélectionnez hello souhaité de connexion de l’utilisateur.

![Se connecter tooAzure AD](./media/active-directory-aadconnect-user-signin/changeusersignin2a.png)

> [!NOTE]
> Si vous effectuez uniquement une synchronisation de toopassword commutateur temporaire, puis sélectionnez hello **ne convertissent pas les comptes d’utilisateur** case à cocher. Non-activation de l’option de hello convertira toofederated de chaque utilisateur, et elle peut prendre plusieurs heures.
>
>

## <a name="next-steps"></a>Étapes suivantes
- En savoir plus sur [l’intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).
- En savoir plus sur [Azure AD Connect : principes de conception](active-directory-aadconnect-design-concepts.md).
