---
title: "Azure AD Connect : comptes et autorisations | Microsoft Docs"
description: "Cette rubrique décrit les comptes hello utilisées et créée et les autorisations requises."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.reviewer: cychua
ms.assetid: b93e595b-354a-479d-85ec-a95553dd9cc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: 70a7013e0353d74714ec8a3ff54b3e811789a0b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-accounts-and-permissions"></a>Autorisations et comptes Azure AD Connect
Assistant d’installation Bonjour Azure AD Connect offre deux chemins d’accès différents :

* Dans les paramètres Express, Assistant de hello nécessite davantage de privilèges.  Il s’agit afin qu’il peut définir votre configuration facilement, sans vous demander aux utilisateurs de toocreate ou configurer des autorisations.
* Dans les paramètres personnalisés, Assistant de hello vous offre plus de choix et d’options. Toutefois, il existe certains cas dans lesquels vous devez tooensure que vous possédez les autorisations appropriées hello vous-même.

## <a name="related-documentation"></a>documentation connexe
Si vous n’avez pas lu la documentation de hello sur [intégrer vos identités locales avec Azure Active Directory](../active-directory-aadconnect.md), hello tableau suivant fournit des liens toorelated rubriques.

|Rubrique |Lien|  
| --- | --- |
|Téléchargez Azure AD Connect | [Téléchargez Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)|
|Installation à l’aide des paramètres Express | [Installation rapide pour Azure AD Connect](./active-directory-aadconnect-get-started-express.md)|
|Installation à l’aide des paramètres personnalisés | [Installation personnalisée d’Azure AD Connect](./active-directory-aadconnect-get-started-custom.md)|
|Mise à niveau à partir de DirSync | [Effectuer une mise à niveau à partir de l’outil de synchronisation Azure AD (DirSync)](./active-directory-aadconnect-dirsync-upgrade-get-started.md)|
|Après l’installation | [Vérifier l’installation de hello et attribuer des licences](active-directory-aadconnect-whats-next.md)|

## <a name="express-settings-installation"></a>Installation à l’aide de la configuration rapide
Dans les paramètres Express, l’Assistant installation hello vous demande des informations d’identification d’administrateur d’entreprise AD DS.  De cette façon, votre instance locale d’Active Directory peut être configurée avec les autorisations nécessaires pour Azure AD Connect. Si vous mettez à niveau à partir de la synchronisation d’annuaire, informations d’identification de hello AD DS administrateurs de l’entreprise sont utilisés tooreset hello mot de passe hello compte utilisé par la synchronisation d’annuaire. Vous avez également besoin de vos informations d’identification d’administrateur général Azure AD.

| Page de l’Assistant | Informations d’identification collectées | Autorisations requises | Utilisation |
| --- | --- | --- | --- |
| N/A |Assistant d’installation hello utilisateur en cours d’exécution |Administrateur de serveur local de hello |<li>Crée le compte local hello qui est utilisé comme hello [compte de service de moteur de synchronisation](#azure-ad-connect-sync-service-account). |
| Se connecter tooAzure AD |Informations d’identification Azure Active Directory |Rôle Administrateur général dans Azure AD |<li>Activation de la synchronisation dans Windows Azure AD hello.</li>  <li>Création de hello [compte Azure AD](#azure-ad-service-account) qui est utilisé pour les opérations de la synchronisation en cours dans Azure AD.</li> |
| Se connecter tooAD DS |Informations d’identification Active Directory locales |Membre du groupe des administrateurs de l’entreprise (EA) hello dans Active Directory |<li>Crée un [compte](#active-directory-account) dans Active Directory et accorde des autorisations tooit. Ce compte est tooread et écriture Active les informations utilisées lors de la synchronisation.</li> |

### <a name="enterprise-admin-credentials"></a>Informations d’identification d’administrateur d’entreprise
Ces informations d’identification sont utilisées uniquement lors de l’installation de hello et ne sont pas utilisées après installation hello. Hello administrateur d’entreprise, pas hello administrateur de domaine doit Assurez-vous que les autorisations de hello dans Active Directory peuvent être définies dans tous les domaines.

### <a name="global-admin-credentials"></a>Informations d’identification d’administrateur général
Ces informations d’identification sont utilisées uniquement lors de l’installation de hello et ne sont pas utilisées après installation hello. Il est utilisé toocreate hello [compte Azure AD](#azure-ad-service-account) utilisés pour la synchronisation des modifications tooAzure AD. compte de Hello permet également la synchronisation en tant que fonctionnalité dans Azure AD.

### <a name="permissions-for-hello-created-ad-ds-account-for-express-settings"></a>Autorisations pour hello créé de compte de domaine Active Directory pour les paramètres express
Hello [compte](#active-directory-account) créé pour lire et écrire tooAD DS ont hello autorisations lors de la création par les paramètres express suivantes :

| Autorisation | Utilisé pour |
| --- | --- |
| <li>Répliquer les changements d’annuaires</li><li>Répliquer les changements d’annuaire Tout |Synchronisation de mot de passe |
| Toutes les propriétés en lecture/écriture Utilisateur |Importation et Exchange hybride |
| Toutes les propriétés en lecture/écriture iNetOrgPerson |Importation et Exchange hybride |
| Toutes les propriétés en lecture/écriture Groupe |Importation et Exchange hybride |
| Toutes les propriétés en lecture/écriture Contact |Importation et Exchange hybride |
| Réinitialiser le mot de passe |Préparation pour l’activation de l’écriture différée du mot de passe |

## <a name="custom-settings-installation"></a>Installation à l’aide des paramètres personnalisés
Azure AD Connect version 1.1.524.0 et ultérieurement hello option toolet hello Azure AD Connect Assistant créer hello compte utilisé tooconnect tooActive active.  Les versions antérieures nécessitent que le compte de hello est créé avant l’installation de hello. Vous devez accorder à ce compte des autorisations Hello se trouvent dans [créer hello AD DS compte](#create-the-ad-ds-account). 

| Page de l’Assistant | Informations d’identification collectées | Autorisations requises | Utilisation |
| --- | --- | --- | --- |
| N/A |Assistant d’installation hello utilisateur en cours d’exécution |<li>Administrateur de serveur local de hello</li><li>Si vous utilisez un serveur SQL Server complet, utilisateur de hello doit être administrateur système (SA) SQL</li> |Par défaut, crée le compte local hello qui est utilisé comme hello [compte de service de moteur de synchronisation](#azure-ad-connect-sync-service-account). Hello compte est uniquement créé lorsque hello admin ne spécifie pas un compte particulier. |
| Installation des services de synchronisation, option Compte de service |Informations d’identification du compte d’utilisateur local ou AD |Utilisateur, les autorisations sont accordées par l’Assistant installation Bonjour |Si l’administrateur hello spécifie un compte, ce compte est utilisé comme compte de service hello hello service de synchronisation. |
| Se connecter tooAzure AD |Informations d’identification Azure Active Directory |Rôle Administrateur général dans Azure AD |<li>Activation de la synchronisation dans Windows Azure AD hello.</li>  <li>Création de hello [compte Azure AD](#azure-ad-service-account) qui est utilisé pour les opérations de la synchronisation en cours dans Azure AD.</li> |
| Connexion de vos annuaires |Informations d’identification Active Directory pour chaque forêt qui est connecté tooAzure AD locale |les autorisations Hello selon les fonctionnalités qui vous activez et se trouvent dans [créer le compte de hello AD DS](#create-the-ad-ds-account) |Ce compte est tooread et écriture Active les informations utilisées lors de la synchronisation. |
| Serveurs AD FS |Pour chaque serveur dans la liste de hello, Assistant de hello collecte les informations d’identification lorsque hello d’identification d’utilisateur hello exécutant l’Assistant de hello est insuffisante tooconnect |Administrateur de domaine |Installation et configuration du rôle de serveur hello AD FS. |
| Serveurs proxy d’application web |Pour chaque serveur dans la liste de hello, Assistant de hello collecte les informations d’identification lorsque hello d’identification d’utilisateur hello exécutant l’Assistant de hello est insuffisante tooconnect |Administrateur local sur l’ordinateur cible hello |Installation et configuration du rôle de serveur WAP |
| Informations d’identification de confiance du proxy |Informations d’identification du approbation Federation service (proxy de hello d’informations d’identification hello utilise tooenroll pour un certificat de confiance de hello FS |Compte de domaine qui est un administrateur local du serveur de hello AD FS |Inscription initiale du certificat d’approbation FS-WAP. |
| Page Compte de service AD FS, option Utilisation d’un compte d’utilisateur de domaine |Informations d’identification du compte d’utilisateur AD |Utilisateur de domaine |compte d’utilisateur Hello AD dont informations d’identification sont fournies est utilisé comme compte d’ouverture de session de hello du service de hello AD FS. |

### <a name="create-hello-ad-ds-account"></a>Créer le compte de hello AD DS
Hello compte que vous spécifiez sur hello **connecter vos annuaires** page doit être présente dans tooinstallation préalable d’Active Directory.  Il doit également disposer des autorisations hello requis. l’Assistant installation Hello ne vérifie pas les autorisations hello et aux problèmes sont trouvés uniquement pendant la synchronisation.

Les autorisations que vous avez besoin dépend des fonctionnalités facultatives de hello, vous activez. Si vous avez plusieurs domaines, les autorisations de hello doivent être accordées pour tous les domaines dans la forêt de hello. Si vous n’activez pas une de ces fonctionnalités, hello par défaut **utilisateur de domaine** les autorisations sont suffisantes.

| Fonctionnalité | Autorisations |
| --- | --- |
| Fonctionnalité msDS-ConsistencyGuid |Autorisations d’écriture toohello msDS-ConsistencyGuid attribut documentée dans [les Concepts de conception : à l’aide de msDS-ConsistencyGuid comme sourceAnchor](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor). | 
| Synchronisation de mot de passe |<li>Répliquer les changements d’annuaires</li>  <li>Répliquer les changements d’annuaire Tout |
| Déploiement Exchange hybride |Écrire des attributs toohello autorisations documentés dans [l’écriture différée de Exchange hybride](active-directory-aadconnectsync-attributes-synchronized.md#exchange-hybrid-writeback) pour les utilisateurs, groupes et contacts. |
| Dossier public de messagerie Exchange |Lecture des attributs toohello autorisations documentées dans [dossier Public de messagerie Exchange](active-directory-aadconnectsync-attributes-synchronized.md#exchange-mail-public-folder) des dossiers publics. | 
| Réécriture du mot de passe |Écrire des attributs toohello autorisations documentés dans [mise en route de la gestion de mot de passe](../active-directory-passwords-writeback.md) pour les utilisateurs. |
| Écriture différée des appareils |Autorisations accordées avec un script PowerShell comme décrit dans [Écriture différée des appareils](active-directory-aadconnect-feature-device-writeback.md). |
| Écriture différée de groupe |Lire, créer, mettre à jour et supprimer des objets de groupe pour les **groupes Office 365** synchronisés.  Pour plus d’informations, consultez [Écriture différée de groupe](active-directory-aadconnect-feature-preview.md#group-writeback).|

## <a name="upgrade"></a>Mise à niveau
Lorsque vous mettez à niveau une version d’Azure AD Connect tooa mise en production, vous devez hello les autorisations suivantes :

| Principal | Autorisations requises | Utilisation |
| --- | --- | --- |
| Assistant d’installation hello utilisateur en cours d’exécution |Administrateur de serveur local de hello |Mettre à jour des fichiers binaires. |
| Assistant d’installation hello utilisateur en cours d’exécution |Membre d'ADSyncAdmins |Apporter des modifications tooSync règles et autres configurations. |
| Assistant d’installation hello utilisateur en cours d’exécution |Si vous utilisez un serveur SQL server complet : DBO (ou similaire) de la base de données du moteur de synchronisation hello |Apporter des modifications au niveau de la base de données, telles que la mise à jour des tables avec de nouvelles colonnes. |

## <a name="more-about-hello-created-accounts"></a>En savoir plus sur hello créé des comptes
### <a name="active-directory-account"></a>Compte Active Directory
Si vous utilisez la configuration rapide, un compte à utiliser pour la synchronisation est créé dans Active Directory. compte de Hello créé se trouve dans le domaine racine de forêt hello dans le conteneur d’utilisateurs hello et a son nom précédé de **MSOL_**. compte de Hello est créé avec un mot de passe longs et complexe qui n’expire pas. Si vous avez une stratégie de mot de passe dans votre domaine, assurez-vous que les mots de passe longs et complexes sont autorisés pour ce compte.

![Compte AD](./media/active-directory-aadconnect-accounts-permissions/adsyncserviceaccount.png)

Si vous utilisez des paramètres personnalisés, vous êtes chargé de créer le compte de hello avant de démarrer hello installation.

### <a name="azure-ad-connect-sync-service-account"></a>Compte de service de synchronisation d'Azure AD Connect
le service de synchronisation Hello peut s’exécuter sous des comptes différents. Il peut s’exécuter sous un **Compte de service virtuel** (VSA), un **Compte de service géré de groupe** (gMSA/sMSA), ou un compte d’utilisateur normal. options de Hello pris en charge ont été modifiées par hello build d’avril 2017 de se connecter lorsque vous effectuez une nouvelle installation. Si vous mettez à niveau depuis une version antérieure d’Azure AD Connect, ces options supplémentaires ne sont pas disponibles.

| Type de compte | Option d’installation | Description |
| --- | --- | --- |
| [Compte de service virtuel](#virtual-service-account) | Rapide et personnalisée, avril 2017 et versions ultérieures | Il s’agit d’option hello utilisée pour toutes les installations express, sauf pour les installations sur un contrôleur de domaine. Personnalisée, il est option par défaut de hello sauf si une autre option est utilisée. |
| [Compte de service géré de groupe](#group-managed-service-account) | Installation personnalisée, avril 2017 et versions ultérieures | Si vous utilisez un serveur SQL distant, il est recommandé de toouse un groupe de compte de service administré. |
| [Compte d’utilisateur](#user-account) | Rapide et personnalisée, avril 2017 et versions ultérieures | Un compte d’utilisateur avec le préfixe AAD_ est créé uniquement lors de l’installation sur Windows Server 2008 ou sur un contrôleur de domaine. |
| [Compte d’utilisateur](#user-account) | Installation rapide et personnalisée, mars 2017 et versions antérieures | Un compte local avec le préfixe AAD_ est créé pendant l’installation. Lorsque vous utilisez l’installation personnalisée, vous pouvez spécifier un autre compte. |

Si vous utilisez la connexion avec une build à partir de mars de 2017 ou antérieure, vous devez réinitialiser le mot de passe hello sur le compte de service hello depuis Windows détruit les clés de chiffrement hello pour des raisons de sécurité. Vous ne pouvez pas modifier hello compte tooany autre compte sans avoir à réinstaller Azure AD Connect. Si vous mettez à niveau tooa build 2017 avril ou version ultérieure, puis il s’agit d’un mot de passe hello toochange pris en charge sur le compte de service hello mais vous ne pouvez pas modifier le compte hello utilisé.

> [!Important]
> Vous pouvez uniquement définir le compte de service hello sur la première installation. Il n’est pas prise en charge du compte de service toochange hello après installation hello.

Il s’agit d’une table de valeur par défaut de hello, recommandé, et le compte de service de synchronisation des options prises en charge pour hello.

Légende :

- **Gras** indique l’option par défaut de hello et dans la plupart des hello de cas option recommandée.
- *Italique* indique hello option recommandée lorsqu’il n’est pas option par défaut de hello.
- 2008 - Option par défaut lors de l’installation sur Windows Server 2008
- Non gras - Option prise en charge
- Compte local - compte d’utilisateur Local sur le serveur de hello
- Compte de domaine - Compte d’utilisateur de domaine
- sMSA - [Compte de service géré autonome](https://technet.microsoft.com/library/dd548356.aspx)
- gMSA - [Compte de service géré de groupe](https://technet.microsoft.com/library/hh831782.aspx)

| | LocalDB</br>Express | LocalDB/LocalSQL</br>Personnalisée | SQL à distance</br>Personnalisée |
| --- | --- | --- | --- |
| **Machine de groupe de travail/autonome** | Non pris en charge | **VSA**</br>Compte local (2008)</br>Compte local |  Non pris en charge |
| **ordinateur joint à un domaine** | **VSA**</br>Compte local (2008) | **VSA**</br>Compte local (2008)</br>Compte local</br>Compte du domaine</br>sMSA, gMSA | **gMSA**</br>Compte du domaine |
| **Contrôleur de domaine** | **Compte du domaine** | *gMSA*</br>**Compte du domaine**</br>sMSA| *gMSA*</br>**Compte du domaine**|

#### <a name="virtual-service-account"></a>Compte de service virtuel
Un compte de service virtuel est un type spécial de compte qui ne dispose pas d’un mot de passe et qui est géré par Windows.

![VSA](./media/active-directory-aadconnect-accounts-permissions/aadsyncvsa.png)

Hello VSA est prévue toobe utilisée avec les scénarios où le moteur de synchronisation hello et SQL sont sur hello même serveur. Si vous utilisez SQL à distance, nous vous recommandons de toouse un [groupe compte de Service administré](#managed-service-account) à la place.

Cette fonctionnalité nécessite Windows Server 2008 R2 ou version ultérieure. Si vous installez Azure AD Connect sur Windows Server 2008, puis installation de hello revient toousing un [compte d’utilisateur](#user-account) à la place.

#### <a name="group-managed-service-account"></a>Compte de service géré de groupe
Si vous utilisez un serveur SQL distant, il est recommandé de toousing un **compte de service administré de groupe**. Pour plus d’informations sur la façon de voir de votre annuaire Active Directory pour le compte de Service géré de groupe, tooprepare [groupe Managed Service Accounts Overview](https://technet.microsoft.com/library/hh831782.aspx).

toouse cette option sur hello [installe les composants requis](active-directory-aadconnect-get-started-custom.md#install-required-components) page, sélectionnez **utiliser un compte de service existant**, puis sélectionnez **compte de Service administré**.  
![VSA](./media/active-directory-aadconnect-accounts-permissions/serviceaccount.png)  
Il est également pris en charge toouse un [autonome de compte de service administré](https://technet.microsoft.com/library/dd548356.aspx). Toutefois, ils peuvent uniquement être utilisés sur l’ordinateur local de hello et il n’existe aucun toouse offre de leur compte de service virtuel hello par défaut.

Cette fonctionnalité nécessite Windows Server 2012 ou version ultérieure. Si toouse un ancien système d’exploitation et d’utiliser SQL à distance, vous devez utiliser un [compte d’utilisateur](#user-account).

#### <a name="user-account"></a>Compte d’utilisateur
Un compte de service local est créé par l’Assistant installation hello (sauf si vous spécifiez hello compte toouse dans les paramètres personnalisés). compte de Hello est préfixé **AAD_** et utilisé pour toorun de service de synchronisation réel hello en tant que. Si vous installez Azure AD Connect sur un contrôleur de domaine, le compte de hello est créé dans le domaine de hello. Hello **AAD_** compte de service doit se trouver dans le domaine de hello si :
   - Vous utilisez un serveur distant exécutant SQL Server.
   - Vous utilisez un proxy qui nécessite une authentification.

![Compte de service de synchronisation](./media/active-directory-aadconnect-accounts-permissions/syncserviceaccount.png)

compte de Hello est créé avec un mot de passe longs et complexe qui n’expire pas.

Ce compte est utilisé toostore hello des mots de passe pour hello autres comptes de manière sécurisée. Ces autres comptes les mots de passe sont stockées dans la base de données hello. les clés privées Hello hello clés de chiffrement sont protégés par chiffrement à clé secrète hello services de chiffrement à l’aide des API de Protection des données (DPAPI) Windows.

Si vous utilisez un serveur SQL Server complet, compte de service hello est hello DBO de la base de données hello créé pour le moteur de synchronisation hello. service de Hello ne fonctionnera pas comme prévu avec toutes les autres autorisations. Une connexion SQL est également créée.

Hello reçoit également les autorisations toofiles, clés de Registre et autres toohello de connexes d’objets du moteur de synchronisation.

### <a name="azure-ad-service-account"></a>Compte de service Azure AD
Un compte dans Azure AD est créé pour une utilisation du service de synchronisation hello. Ce compte peut être identifié par son nom d’affichage.

![Compte AD](./media/active-directory-aadconnect-accounts-permissions/aadsyncserviceaccount.png)

nom de Hello du compte hello du serveur hello est utilisé dans peut être identifiée dans la deuxième partie de hello hello nom d’utilisateur. Dans l’image de hello, nom du serveur hello est FABRIKAMCON. Si vous disposez de serveurs intermédiaires, chaque serveur a son propre compte.

compte de service Hello est créé avec un mot de passe longs et complexe qui n’expire pas. Il bénéficie d’un rôle particulier **comptes de synchronisation Active Directory** qui a uniquement les tâches de synchronisation du répertoire autorisations tooperform. Ce rôle intégré spécial ne peut pas être accordé en dehors de l’Assistant d’Azure AD Connect hello. portail Azure Hello affiche ce compte avec le rôle de hello **utilisateur**.

Il existe une limite de 20 comptes de service de synchronisation dans Azure AD. liste de hello tooget existants Azure AD de comptes de service dans Azure AD, exécutez hello suivant l’applet de commande PowerShell Azure AD :`Get-AzureADDirectoryRole | where {$_.DisplayName -eq "Directory Synchronization Accounts"} | Get-AzureADDirectoryRoleMember`

tooremove les comptes de service Azure AD, exécutez hello suivant l’applet de commande PowerShell Azure AD :`Remove-AzureADUser -ObjectId <ObjectId-of-the-account-you-wish-to-remove>`

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](../active-directory-aadconnect.md).
