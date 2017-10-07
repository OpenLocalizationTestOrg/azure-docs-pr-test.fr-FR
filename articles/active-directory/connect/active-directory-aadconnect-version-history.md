---
title: 'Azure AD Connect : historique de publication des versions | Microsoft Docs'
description: "Cet article répertorie toutes les versions d’Azure AD Connect et d’Azure AD Sync"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: ef2797d7-d440-4a9a-a648-db32ad137494
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b55e0f2d426e34ceef9869d5a6d1b0956d8bd076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-version-release-history"></a>Azure AD Connect : historique de publication des versions
équipe Azure Active Directory (Azure AD) de Hello met régulièrement à jour Azure AD Connect avec de nouvelles fonctionnalités. Pas tous les compléments sont des audiences tooall applicable.

Cet article est conçu toohelp vous effectuer le suivi des versions hello qui ont été publiées et toounderstand tooupdate toohello version la plus récente si vous devez ou non.

Voici la liste des rubriques connexes :


Rubrique |  Détails
--------- | --------- |
Tooupgrade étapes d’Azure AD Connect | Différentes méthodes trop[mise à niveau à partir d’une précédente toohello de version plus récente](active-directory-aadconnect-upgrade-previous-version.md) version d’Azure AD Connect.
Autorisations requises | Pour les autorisations requises tooapply une mise à jour, consultez [comptes et autorisations](./active-directory-aadconnect-accounts-permissions.md#upgrade).
Télécharger| [Téléchargez Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771).

## <a name="115610"></a>1.1.561.0
État : 23 juillet 2017

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>Problème résolu

* Correction d’un problème qui a provoqué la règle de synchronisation d’out-of-box hello « sortie tooAD - ImmutableId de l’utilisateur » toobe supprimé :

  * problème de Hello se produit lorsque la mise à niveau de Azure AD Connect, ou lorsque hello option tâche *mise à jour de Configuration de la synchronisation* Bonjour Azure AD Connect Assistant est la configuration de la synchronisation tooupdate utilisé Azure AD Connect.
  
  * Cette règle de synchronisation est applicable toocustomers qui ont activé hello [msDS-ConsistencyGuid en tant que fonctionnalité d’ancre Source](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor). Cette fonctionnalité a été introduite dans la version 1.1.524.0 et les versions ultérieures. Lors de la règle de synchronisation hello est supprimé, Azure AD Connect peut remplir n’est plus local attribut ms-DS-ConsistencyGuid AD hello valeur de l’attribut ObjectGuid. Cela n’empêche pas la configuration de nouveaux utilisateurs dans Azure AD.
  
  * Hello correctif garantit cette règle de synchronisation hello est pas supprimée pendant la mise à niveau ou pendant la modification de la configuration, tant que fonctionnalité de hello est activée. Pour les clients existants qui ont été affectés par ce problème, corrigez d’hello garantit également que cette règle de synchronisation hello est ajoutée après la mise à niveau de version toothis d’Azure AD Connect.

* Correction d’un problème qui provoque la valeur de priorité toohave qui est inférieur à 100 règles de synchronisation d’out-of-box :

  * En général, les valeurs de précédence 0 - 99 sont réservées aux règles de synchronisation personnalisées. Au cours de la mise à niveau, les valeurs de priorité hello pour les règles de synchronisation d’out-of-box sont tooaccommodate mis à jour les modifications de règle de synchronisation. En raison du problème de toothis, les règles de synchronisation d’out-of-box peuvent être assignés à une valeur de priorité qui est inférieur à 100.
  
  * correctif de Hello empêche les problème de hello pendant la mise à niveau. Toutefois, il ne restaure pas les valeurs de priorité hello pour les clients existants qui ont été affectés par le problème de hello. Un correctif distinct sera fourni dans toohelp de futures hello avec la restauration de hello.

* Correction d’un problème où hello [écran de domaine et le filtrage de l’unité d’organisation](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) Bonjour Azure AD Connect de l’Assistant affiche *synchroniser tous les domaines et les unités d’organisation* option sélectionné, même si le filtrage basé sur une unité d’organisation est activé.

*   Correction d’un problème qui a causé hello [écran de configurer les Partitions d’annuaire](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) Bonjour Synchronization Service Manager tooreturn une erreur si hello *Actualiser* bouton est activé. message d’erreur Hello est *« une erreur s’est produite lors de l’actualisation des domaines : objet toocast impossible du type 'System.Collections.ArrayList' tootype ' Microsoft.DirectoryServices.MetadirectoryServices.UI.PropertySheetBase.MaPropertyPages.PartitionObject. »* Hello erreur se produit lorsque le nouveau domaine Active Directory a été ajouté à la forêt Active Directory existant tooan et que vous essayez tooupdate Azure AD Connect à l’aide de hello bouton Actualiser.

#### <a name="new-features-and-improvements"></a>Améliorations et nouvelles fonctionnalités

* [Fonctionnalité de mise à niveau automatique](active-directory-aadconnect-feature-automatic-upgrade.md) a été clients toosupport développée par hello suivant configurations :
  * Vous avez activé la fonctionnalité de l’écriture différée des appareils hello.
  * Vous avez activé la fonctionnalité d’écriture différée de groupe de hello.
  * installation de Hello n’est pas un paramètres Express ou une mise à niveau de DirSync.
  * Vous avez plus de 100 000 objets hello métaverse.
  * Vous vous connectez toomore qu’une seule forêt. Le programme d’installation Express connecte uniquement à tooone forêt.
  * Hello compte Active Directory Connector n’est pas plus compte MSOL_ hello par défaut.
  * serveur de Hello a la valeur toobe dans le mode de mise en lots.
  * Vous avez activé la fonctionnalité d’écriture différée hello utilisateur.
  
  >[!NOTE]
  >expansion d’étendue Hello de fonctionnalité de mise à niveau automatique de hello affecte les clients avec Azure AD Connect build 1.1.105.0 et après. Si vous ne souhaitez pas que votre toobe du serveur Azure AD Connect automatiquement mis à niveau, vous devez exécuter après l’applet de commande sur votre serveur Azure AD Connect : `Set-ADSyncAutoUpgrade -AutoUpgradeState disabled`. Pour plus d’informations sur l’activation/désactivation de la mise à niveau automatique, consultez tooarticle [Azure AD Connect : mise à niveau automatique](active-directory-aadconnect-feature-automatic-upgrade.md).

## <a name="115580"></a>1.1.558.0
État : ne sera pas mis en production. Les modifications apportées à ce build sont incluses dans la version 1.1.561.0.

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>Problème résolu

* Correction d’un problème qui a provoqué hello out-of-box synchronisation règle « hors tooAD - ImmutableId de l’utilisateur » toobe supprimés lorsque la mise à jour de configuration de filtrage basé sur une unité d’organisation. Cette règle de synchronisation est nécessaire pour hello [msDS-ConsistencyGuid en tant que fonctionnalité d’ancre Source](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor).

* Correction d’un problème où hello [écran de domaine et le filtrage de l’unité d’organisation](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) Bonjour Azure AD Connect de l’Assistant affiche *synchroniser tous les domaines et les unités d’organisation* option sélectionné, même si le filtrage basé sur une unité d’organisation est activé.

*   Correction d’un problème qui a causé hello [écran de configurer les Partitions d’annuaire](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) Bonjour Synchronization Service Manager tooreturn une erreur si hello *Actualiser* bouton est activé. message d’erreur Hello est *« une erreur s’est produite lors de l’actualisation des domaines : objet toocast impossible du type 'System.Collections.ArrayList' tootype ' Microsoft.DirectoryServices.MetadirectoryServices.UI.PropertySheetBase.MaPropertyPages.PartitionObject. »* Hello erreur se produit lorsque le nouveau domaine Active Directory a été ajouté à la forêt Active Directory existant tooan et que vous essayez tooupdate Azure AD Connect à l’aide de hello bouton Actualiser.

#### <a name="new-features-and-improvements"></a>Améliorations et nouvelles fonctionnalités

* [Fonctionnalité de mise à niveau automatique](active-directory-aadconnect-feature-automatic-upgrade.md) a été clients toosupport développée par hello suivant configurations :
  * Vous avez activé la fonctionnalité de l’écriture différée des appareils hello.
  * Vous avez activé la fonctionnalité d’écriture différée de groupe de hello.
  * installation de Hello n’est pas un paramètres Express ou une mise à niveau de DirSync.
  * Vous avez plus de 100 000 objets hello métaverse.
  * Vous vous connectez toomore qu’une seule forêt. Le programme d’installation Express connecte uniquement à tooone forêt.
  * Hello compte Active Directory Connector n’est pas plus compte MSOL_ hello par défaut.
  * serveur de Hello a la valeur toobe dans le mode de mise en lots.
  * Vous avez activé la fonctionnalité d’écriture différée hello utilisateur.
  
  >[!NOTE]
  >expansion d’étendue Hello de fonctionnalité de mise à niveau automatique de hello affecte les clients avec Azure AD Connect build 1.1.105.0 et après. Si vous ne souhaitez pas que votre toobe du serveur Azure AD Connect automatiquement mis à niveau, vous devez exécuter après l’applet de commande sur votre serveur Azure AD Connect : `Set-ADSyncAutoUpgrade -AutoUpgradeState disabled`. Pour plus d’informations sur l’activation/désactivation de la mise à niveau automatique, consultez tooarticle [Azure AD Connect : mise à niveau automatique](active-directory-aadconnect-feature-automatic-upgrade.md).

## <a name="115570"></a>1.1.557.0
État : juillet 2017

>[!NOTE]
>Cette build n’est pas disponible toocustomers via la fonctionnalité de connecter la mise à niveau automatique de hello Azure AD.

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>Problème résolu
* Correction d’un problème avec l’applet de commande hello Initialize-ADSyncDomainJoinedComputerSync qui a provoqué le domaine vérifié de hello configuré sur l’objet point de hello existant service connexion toobe soit modifiée même si elle est toujours un domaine valide. Ce problème se produit lorsque votre client Azure AD a plusieurs domaines vérifiés qui peuvent être utilisé pour la configuration de point de connexion de service hello.

#### <a name="new-features-and-improvements"></a>Améliorations et nouvelles fonctionnalités
* La réécriture du mot de passe est désormais disponible en version préliminaire avec le cloud Microsoft Azure Government et Microsoft Cloud Allemagne. Pour plus d’informations sur la prise en charge d’Azure AD Connect hello différentes instances de service, consultez tooarticle [Azure AD Connect : Considérations spéciales pour les instances](active-directory-aadconnect-instances.md).

* applet de commande Hello Initialize-ADSyncDomainJoinedComputerSync a maintenant un nouveau paramètre facultatif nommé AzureADDomain. Ce paramètre vous permet de spécifier qui vérifié toobe de domaine utilisé pour la configuration de point de connexion de service hello.

### <a name="pass-through-authentication"></a>Authentification directe

#### <a name="new-features-and-improvements"></a>Améliorations et nouvelles fonctionnalités
* nom Hello d’agent hello requis pour l’authentification directe a été modifiée à partir de *connecteur de Proxy d’Application Microsoft Azure AD* trop*Agent d’authentification Microsoft Azure AD Connect*.

* L’activation de l’authentification directe ne permet plus la synchronisation du hachage de mot de passe par défaut.


## <a name="115530"></a>1.1.553.0
État : juin 2017

> [!IMPORTANT]
> Des modifications de schéma et de règle de synchronisation ont été introduites dans cette build. Le service de synchronisation Azure AD Connect déclenchera des étapes d’importation et de synchronisation complètes après la mise à niveau. Détails des modifications de hello sont décrits ci-dessous. tootemporarily différer les étapes d’importation complète et synchronisation complète après mise à niveau, consultez le tooarticle [comment la synchronisation après mise à niveau de complète toodefer](active-directory-aadconnect-upgrade-previous-version.md#how-to-defer-full-synchronization-after-upgrade).
>
>

### <a name="azure-ad-connect-sync"></a>Synchronisation d’Azure AD Connect

#### <a name="known-issue"></a>Problème connu
* Il existe un problème qui affecte les clients utilisant le[filtrage basé sur une unité d’organisation](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) avec la synchronisation Azure AD Connect. Lorsque vous accédez toohello [page domaine et unité d’organisation filtrage](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) dans l’Assistant de connexion hello Azure AD, hello suivant le comportement est attendu :
  * Si le filtrage basé sur une unité d’organisation est activé, hello **domaines sélectionnés et les unités d’organisation de synchronisation** option est sélectionnée.
  * Dans le cas contraire, hello **synchroniser tous les domaines et les unités d’organisation** option est sélectionnée.

Hello pose problème est que hello **synchroniser tous les domaines et les unités d’organisation option** est toujours sélectionnée lorsque vous exécutez l’Assistant de hello.  Cela se produit même si le filtrage basé sur une unité d’organisation a été configuré précédemment. Avant d’enregistrer les modifications de configuration AAD Connect, assurez-vous que hello **synchroniser les domaines sélectionnés et unités d’organisation est sélectionnée** et vérifiez que toutes les unités d’organisation qui doivent toosynchronize sont activées à nouveau. Dans le cas contraire, le filtrage basé sur une unité d’organisation sera désactivé.

#### <a name="fixed-issues"></a>Problèmes résolus

* Correction d’un problème avec l’écriture différée de mot de passe qui permet une tooreset administrateur AD Azure mot de passe hello d’un site local AD privilégié du compte d’utilisateur. problème de Hello se produit lorsque Azure AD Connect a l’autorisation de réinitialiser le mot de passe hello sur le compte de hello privilégié. Hello problème est résolu dans cette version d’Azure AD Connect, en n’autorisant ne pas un tooreset administrateur AD Azure mot de passe hello arbitraire localement AD privilégié du compte d’utilisateur, sauf si l’administrateur de hello est propriétaire de hello de ce compte. Pour plus d’informations, consultez trop[4033453 avis de sécurité](https://technet.microsoft.com/library/security/4033453).

* Correction d’un problème lié toohello [msDS-ConsistencyGuid comme ancre Source](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) fonctionnalité où Azure AD Connect ne pas l’écriture différée tooon local attribut msDS-ConsistencyGuid d’Active Directory. Hello se produit lorsqu’il existe plusieurs locaux forêts AD ajouté tooAzure AD Connect et hello *identités utilisateurs existent sur plusieurs répertoires (option)* est sélectionnée. Lors de la configuration de ce type est utilisée, les règles de synchronisation résultant de hello ne remplissent pas attribut sourceAnchorBinary hello hello métaverse. attribut de sourceAnchorBinary Hello est utilisé en tant qu’attribut de source de hello pour l’attribut de l’attribut msDS-ConsistencyGuid. Par conséquent, l’écriture différée toohello ms-DSConsistencyGuid attribut n’a pas lieu. problème de hello toofix, les règles de synchronisation suivantes ont été tooensure mis à jour qui hello attribut sourceAnchorBinary Bonjour que métaverse est toujours rempli :
  * In from AD - InetOrgPerson AccountEnabled.xml
  * In from AD - InetOrgPerson Common.xml
  * In from AD - User AccountEnabled.xml
  * In from AD - User Common.xml
  * In from AD - User Join SOAInAAD.xml

* Auparavant, même si hello [msDS-ConsistencyGuid comme ancre Source](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) fonctionnalité n’est pas activée, hello « sortie tooAD – ImmutableId de l’utilisateur » règle de synchronisation est encore ajoutée tooAzure AD Connect. effet de Hello est sans gravité et n’entraîne pas l’écriture différée de toooccur d’attribut msDS-ConsistencyGuid. toute confusion tooavoid, logique a été ajoutée tooensure qui hello la règle de synchronisation est ajouté uniquement lorsque la fonctionnalité de hello est activée.

* Correction d’un problème à l’origine avec l’événement d’erreur 611 toofail de synchronisation de hachage de mot de passe. Ce problème se produit après qu’un ou plusieurs contrôleurs de domaine ont été supprimés de l’instance AD locale. À la fin de hello de chaque cycle de synchronisation de mot de passe, hello cookie de synchronisation émis par local AD contient les ID d’appel hello supprimé des contrôleurs de domaine avec 0 comme valeur USN (numéro de séquence de mise à jour). Hello Gestionnaire de synchronisation de mot de passe est impossible toopersist synchronisation cookie contenante valeur USN de 0 et échoue avec l’événement d’erreur 611. Lors de la synchronisation suivante de hello cycle, hello du Gestionnaire de synchronisation de mot de passe réutilise hello dernière persistante cookie de synchronisation qui ne contient pas de valeur USN de 0. Cela entraîne des modifications de mot de passe même hello toobe resynchronisé. Ce correctif hello Gestionnaire de synchronisation de mot de passe est conservé cookie de synchronisation hello correctement.

* Auparavant, même si la mise à niveau automatique a été désactivé à l’aide d’applet de commande hello ADSyncAutoUpgrade de jeu, hello processus de mise à niveau automatique continue toocheck pour la mise à niveau régulièrement et s’appuie sur la désactivation de toohonor hello téléchargé programme d’installation. Avec ce correctif, hello processus de mise à niveau automatique n’est plus mise à niveau vérifie régulièrement la présence. correctif de Hello est appliquée automatiquement lorsque le programme d’installation de mise à niveau pour cette version d’Azure AD Connect est exécutée une fois.

#### <a name="new-features-and-improvements"></a>Améliorations et nouvelles fonctionnalités

* Auparavant, hello [msDS-ConsistencyGuid comme ancre Source](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) fonctionnalité a été toonew disponible uniquement dans les déploiements. Il est désormais disponible tooexisting déploiements. Plus précisément :
  * tooaccess hello fonctionnalité, démarrer l’Assistant de connexion hello Azure AD et choisissez hello *ancre Source de mise à jour* option.
  * Cette option est visible tooexisting uniquement les déploiements qui utilisent objectGuid comme attribut sourceAnchor.
  * Lorsque vous configurez l’option de hello, Assistant de hello valide état hello de l’attribut msDS-ConsistencyGuid de hello dans votre annuaire Active Directory local. Si l’attribut de hello n’est pas configurée sur n’importe quel objet utilisateur dans le répertoire de hello, Assistant de hello utilise hello msDS-ConsistencyGuid en tant qu’attribut de sourceAnchor hello. Si l’attribut de hello est configuré sur un ou plusieurs objets utilisateur dans le répertoire de hello, hello fermeture de l’Assistant attribut de hello est utilisé par d’autres applications et n’est pas approprié en tant qu’attribut sourceAnchor et n’autorise pas hello ancre Source modification tooproceed. Si vous êtes certain que cet attribut hello n’est pas utilisé par les applications existantes, vous devez toocontact prise en charge pour plus d’informations sur la façon dont toosuppress hello erreur.

* Spécifique trop**userCertificate** recherche les attributs des objets de l’appareil, Azure AD Connect maintenant des valeurs de certificats requis pour [tooAzure de périphériques joints au domaine Active Directory pour Windows 10 expérience de connexion](https://docs.microsoft.com/azure/active-directory/active-directory-azureadjoin-devices-group-policy) filtres et reste hello avant la synchronisation tooAzure AD. tooenable ce comportement, la règle de synchronisation d’out-of-box hello « Out tooAAD - appareil joindre SOAInAD » a été mis à jour.

* Azure AD Connect maintenant prend en charge l’écriture différée d’Exchange Online **cloudPublicDelegates** tooon local d’attribut AD **publicDelegates** attribut. Cela permet de scénario hello où une boîte aux lettres Exchange Online peut être accordée toousers de droits SendOnBehalfTo avec boîte aux lettres de Exchange sur site. toosupport cette fonctionnalité, une nouvelle règle de synchronisation d’out-of-box « Out tooAD – l’écriture différée d’utilisateur Exchange hybride PublicDelegates » a été ajouté. Cette règle de synchronisation est ajoutée uniquement tooAzure AD se connecter quand Exchange hybride est activée.

*   Azure AD Connect prend désormais en charge la synchronisation de hello **altRecipient** attribut d’Azure AD. toosupport cette modification, suivant les règles de synchronisation d’out-of-box ont été mis à jour le flux d’attribut tooinclude hello requis :
  * Entrant depuis AD – Utilisateur Exchange
  * Out tooAAD – utilisateur ExchangeOnline
  
* Hello **cloudSOAExchMailbox** attribut Bonjour métaverse indique si un utilisateur donné possède une boîte aux lettres Exchange Online ou non. Sa définition a été mis à jour tooinclude supplémentaires RecipientDisplayTypes en ligne Exchange en tant que ces boîtes aux lettres de salle de conférence et de l’équipement. tooenable cette modification, la définition de hello d’attribut hello cloudSOAExchMailbox, qui se trouve sous la règle de synchronisation d’out-of-box « Dans à partir de AAD – utilisateur Exchange hybride », a été mis à jour à partir de :

```
CBool(IIF(IsNullOrEmpty([cloudMSExchRecipientDisplayType]),NULL,BitAnd([cloudMSExchRecipientDisplayType],&amp;HFF) = 0))
```

... toohello suivantes :

```
CBool(
  IIF(IsPresent([cloudMSExchRecipientDisplayType]),(
    IIF([cloudMSExchRecipientDisplayType]=0,True,(
      IIF([cloudMSExchRecipientDisplayType]=2,True,(
        IIF([cloudMSExchRecipientDisplayType]=7,True,(
          IIF([cloudMSExchRecipientDisplayType]=8,True,(
            IIF([cloudMSExchRecipientDisplayType]=10,True,(
              IIF([cloudMSExchRecipientDisplayType]=16,True,(
                IIF([cloudMSExchRecipientDisplayType]=17,True,(
                  IIF([cloudMSExchRecipientDisplayType]=18,True,(
                    IIF([cloudMSExchRecipientDisplayType]=1073741824,True,(
                       IF([cloudMSExchRecipientDisplayType]=1073741840,True,False)))))))))))))))))))),False))

```

* Suivant de hello ajoutés ensemble de fonctions de X509Certificate2 compatible pour la création de valeurs certificat toohandle expressions des règles de synchronisation dans l’attribut userCertificate de hello :

    ||||
    | --- | --- | --- |
    |CertSubject|CertIssuer|CertKeyAlgorithm|
    |CertSubjectNameDN|CertIssuerOid|CertNameInfo|
    |CertSubjectNameOid|CertIssuerDN|IsCert|
    |CertFriendlyName|CertThumbprint|CertExtensionOids|
    |CertFormat|CertNotAfter|CertPublicKeyOid|
    |CertSerialNumber|CertNotBefore|CertPublicKeyParametersOid|
    |CertVersion|CertSignatureAlgorithmOid|Sélectionnez|
    |CertKeyAlgorithmParams|CertHashString|Where|
    |||With|

* Modifications de schéma suivantes ont été introduites tooallow clients toocreate personnalisé de la synchronisation des règles tooflow sAMAccountName domainNetBios et domainFQDN pour les objets de groupe, ainsi que de distinguishedName pour les objets utilisateur :

  * TooMV schéma ont été ajoutés à des attributs suivants :
    * Groupe : AccountName
    * Groupe : domainNetBios
    * Groupe : domainFQDN
    * Personne : distinguishedName

  * Les attributs suivants ont été ajoutés tooAzure schéma de connecteur AD :
    * Groupe : OnPremisesSamAccountName
    * Groupe : NetbiosName
    * Groupe : DnsDomainName
    * Utilisateur : OnPremisesDistinguishedName

* Hello script d’applet de commande ADSyncDomainJoinedComputerSync a maintenant un nouveau paramètre facultatif nommé AzureEnvironment. paramètre Hello est utilisé toospecify le hello région client Azure Active Directory correspondant est hébergé dans. Les valeurs valides incluent :
  * AzureCloud (par défaut)
  * AzureChinaCloud
  * AzureGermanyCloud
  * USGovernment
 
* Toouse d’éditeur de règles de synchronisation des mises à jour joindre (au lieu de déployer) comme valeur par défaut de hello du type de lien lors de la création de règle de synchronisation.

### <a name="ad-fs-management"></a>Gestion AD FS.

#### <a name="issues-fixed"></a>Problèmes résolus

* Suivants URL sont introduites par la résilience de tooimprove Azure AD contre la panne de l’authentification de nouveaux points de terminaison WS-Federation et sera ajouté tooon local AD FS configuration d’approbation de partie de confiance :
  * https://ests.Login.microsoftonline.com/login.srf
  * https://stamp2.login.microsoftonline.com/login.srf
  * https://ccs.login.microsoftonline.com/login.srf
  * https://ccs-sdf.login.microsoftonline.com/login.srf
  
* Correction d’un problème qui a provoqué un valeur de revendication incorrect toogenerate AD FS pour IssuerID. problème de Hello se produit s’il existe plusieurs domaines vérifiés dans le locataire de hello Azure AD et le suffixe de domaine hello de hello userPrincipalName attribut utilisé toogenerate hello IssuerID revendication est au moins 3 niveaux approfondie (par exemple, johndoe@us.contoso.com). Hello est résolu en mettant à jour regex hello utilisé par les règles de revendication hello.

#### <a name="new-features-and-improvements"></a>Améliorations et nouvelles fonctionnalités
* Auparavant, hello gestion des certificats AD FS fonctionnalité fournie par Azure AD Connect peut uniquement être utilisée avec ADFS de batteries de serveurs gérés via Azure AD Connect. Maintenant, vous pouvez utiliser la fonctionnalité de hello avec les batteries de serveurs AD FS qui ne sont pas gérés à l’aide d’Azure AD Connect.

## <a name="115240"></a>1.1.524.0
Publication : mai 2017

> [!IMPORTANT]
> Des modifications de schéma et de règle de synchronisation ont été introduites dans cette build. Le service de synchronisation Azure AD Connect déclenchera des étapes d’importation complète et de synchronisation complète après la mise à niveau. Détails des modifications de hello sont décrits ci-dessous.
>
>

**Problèmes résolus :**

Synchronisation d’Azure AD Connect

* Correction d’un problème susceptible d’entraîner des toooccur de mise à niveau automatique sur le serveur d’Azure AD Connect hello même si le client a désactivé la fonctionnalité hello à l’aide d’applet de commande Set-ADSyncAutoUpgrade hello. Ce correctif hello processus de mise à niveau automatique sur le serveur de hello vérifie toujours pour la mise à niveau régulièrement, mais configuration de mise à niveau automatique de hello honore hello programme d’installation téléchargé.
* Au cours de la mise à niveau de DirSync, Azure AD Connect crée un toobe de compte de service Azure AD utilisé par le connecteur de hello Azure AD pour la synchronisation avec Azure AD. Après la création de compte de hello, Azure AD Connect s’authentifie auprès d’Azure AD à l’aide du compte de hello. Parfois, l’authentification échoue en raison de problèmes temporaires, ce qui entraîne à son tour toofail mise à niveau in situ de DirSync avec l’erreur *« une erreur s’est produite l’exécution de la tâche Configurer AAD Sync : AADSTS50034 : toosign dans cette application, le compte de hello doit être ajouté toohello xxx.onmicrosoft.com répertoire. »* résilience de hello tooimprove de mise à niveau de DirSync, Azure AD Connect maintenant de nouvelles tentatives hello étape d’authentification.
* En cas de problème avec la build 443 qui provoque toosucceed mise à niveau sur place de synchronisation d’annuaire, mais de profils d’exécution requis pour la synchronisation d’annuaires ne sont pas créés. Une logique de réparation est incluse dans cette build d’Azure AD Connect. Lorsque le client met à niveau toothis build, Azure AD Connect détecte pas les profils d’exécution et il les crée.
* Correction d’un problème qui provoque le toostart de toofail de processus de synchronisation de mot de passe 6900 d’ID d’événement et d’erreur *« Un élément avec hello même clé a déjà été ajoutée »*. Ce problème se produit si vous mettez à jour OU le filtrage de partition de configuration configuration tooinclude AD. toofix ce problème, la synchronisation de mot de passe traiter maintenant synchronise les modifications de mot de passe des partitions de domaine Active Directory uniquement. Les partitions autres que de domaine, telles que les partitions de configuration sont ignorées.
* Pendant l’installation d’Express, Azure AD Connect crée un site local de domaine Active Directory compte toobe utilisé par toocommunicate de connecteur hello AD locale Active Directory. Auparavant, compte de hello est créé avec l’indicateur PASSWD_NOTREQD hello défini sur l’attribut de contrôle de compte d’utilisateur hello et un mot de passe aléatoire est définie sur le compte de hello. Désormais, Azure AD Connect supprime explicitement indicateur PASSWD_NOTREQD hello après que hello le mot de passe est défini sur le compte de hello.
* Correction d’un problème qui provoque l’erreur toofail de mise à niveau DirSync *« un blocage s’est produite dans sql server qui tooacquire lors de la tentative un verrou d’application »* lorsque attribut mailNickname de hello se trouve dans hello schéma Active Directory local, mais n’est pas délimité toohello classe d’objet utilisateur Active Directory.
* Fixe à un problème qui provoque le dispositif d’écriture différée fonctionnalité tooautomatically désactivé lors de l’administrateur est mise à jour de configuration de la synchronisation Azure AD Connect à l’aide d’Assistant Azure AD Connect. Cela est dû à vérification des conditions préalables exécution hello Assistant de configuration de l’écriture différée de périphérique existante hello dans AD local et hello vérification échoue. correctif de Hello est vérification de hello tooskip si l’écriture différée de l’appareil est déjà activée précédemment.
* tooconfigure unité d’organisation de filtrage, vous pouvez utiliser l’Assistant d’Azure AD Connect hello ou hello Synchronization Service Manager. Auparavant, si vous utilisez le filtrage de l’unité d’organisation de hello Azure AD Connect Assistant tooconfigure, nouvelles unités d’organisation créées par la suite sont incluses pour la synchronisation d’annuaires. Si vous ne souhaitez pas que les nouvelles unités d’organisation toobe inclus, vous devez configurer unité d’organisation à l’aide de filtrage hello Synchronization Service Manager. Maintenant, vous pouvez obtenir hello même comportement à l’aide d’Assistant Azure AD Connect.
* Correction d’un problème qui provoque des procédures stockées requises par toobe Azure AD Connect créé sous le schéma hello Hello l’installation d’administration, au lieu de sous le schéma dbo de hello.
* Correction d’un problème qui provoque l’attribut de TrackingId hello retourné par toobe Azure AD omis Bonjour AAD connecter Server Event Logs. problème de Hello se produit si Azure AD Connect reçoit un message de redirection à partir d’Azure AD et Azure AD Connect est le point de terminaison toohello tooconnect Impossible fourni. Hello TrackingId est utilisé par toocorrelate ingénieurs du Support technique avec les journaux du côté service lors du dépannage.
* Lorsque Azure AD Connect reçoit LargeObject erreur d’Azure AD, Azure AD Connect génère un événement avec l’ID d’événement 6941 et le message *« objet approvisionné de hello est trop grande. Découpage d’hello plusieurs valeurs d’attribut sur cet objet. »* À hello même moment, Azure AD Connect également génère un événement trompeur avec EventID 6900 et message *« Microsoft.Online.Coexistence.ProvisionRetryException : Impossible de toocommunicate avec hello Windows service Azure Active Directory. »* toominimize confusions, Azure AD Connect n’est plus génère l’événement de ce dernier hello lorsque LargeObject erreur est reçue.
* Correction d’un problème qui provoque hello toobecome Synchronization Service Manager ne répond plus lors de la tentative de configuration de hello tooupdate pour connecteur LDAP générique.

**Nouvelles fonctionnalités/améliorations :**

Synchronisation d’Azure AD Connect
* Synchroniser les modifications de règle – hello suivant de la règle de synchronisation des modifications ont été implémentées :
  * Ensemble de règles de synchronisation de mises à jour par défaut toonot attributs d’exportation **userCertificate** et **userSMIMECertificate** si les attributs de hello ont des valeurs de plus de 15.
  * Attributs AD **employeeID** et **msExchBypassModerationLink** sont désormais incluses dans l’ensemble de règles de synchronisation par défaut hello.
  * L’attribut AD **photo** a été supprimé de l’ensemble de règles de synchronisation par défaut.
  * Ajouté **preferredDataLocation** toohello métaverse schémas et connecteur AAD. Les clients qui souhaitent tooupdate que des attributs dans Azure AD peuvent implémenter personnalisé de synchronisation donc toodo de règles. toofind plus d’informations sur l’attribut de hello, consultez tooarticle section [synchronisation Azure AD Connect : comment toomake un toohello de modification par défaut de configuration - Activer la synchronisation de PreferredDataLocation](active-directory-aadconnectsync-change-the-configuration.md#enable-synchronization-of-preferreddatalocation).
  * Ajouté **userType** toohello métaverse schémas et connecteur AAD. Les clients qui souhaitent tooupdate que des attributs dans Azure AD peuvent implémenter personnalisé de synchronisation donc toodo de règles.

* Azure AD Connect maintenant automatiquement Active hello utiliser ConsistencyGuid attribut comme attribut d’ancre Source hello pour local les objets Active Directory. En outre, Azure AD Connect remplit l’attribut de ConsistencyGuid hello avec la valeur de l’attribut objectGuid hello s’il est vide. Cette fonctionnalité est déploiement toonew applicables uniquement. toofind plus d’informations sur cette fonctionnalité, consultez tooarticle section [Azure AD Connect : concepts : à l’aide de msDS-ConsistencyGuid comme sourceAnchor de conception](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor).
* Nouvelle résolution des problèmes d’applet de commande Invoke-ADSyncDiagnostics a été ajouté toohelp diagnostiquer synchronisation du hachage de mot de passe les problèmes liés. Pour plus d’informations sur l’utilisation d’applet de commande hello, consultez tooarticle [résoudre les problèmes de synchronisation de mot de passe avec la synchronisation Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-troubleshoot-password-synchronization).
* Azure AD Connect maintenant prend en charge la synchronisation du dossier Public paramètres des objets de locaux AD tooAzure AD. Vous pouvez activer la fonctionnalité de hello à l’aide d’Assistant Azure AD Connect sous fonctionnalités facultatives. toofind plus d’informations sur cette fonctionnalité, consultez tooarticle [Office 365 Directory basé le blocage Edge la prise en charge pour les dossiers publics avec messagerie local](https://blogs.technet.microsoft.com/exchange/2017/05/19/office-365-directory-based-edge-blocking-support-for-on-premises-mail-enabled-public-folders).
* Azure AD Connect nécessite une toosynchronize de compte de domaine Active Directory sur site Active Directory. Auparavant, si vous avez installé Azure AD Connect à l’aide du mode de Express hello, vous pouvez fournir des informations d’identification hello d’un compte d’administrateur d’entreprise et Azure AD Connect créerait compte hello AD DS requis. Toutefois, pour une installation personnalisée et l’ajout de déploiement existant de forêts tooan, vous étiez requis tooprovide hello compte AD DS à la place. Maintenant, vous devez également hello option tooprovide hello des informations d’identification d’un compte d’administrateur d’entreprise au cours d’une installation personnalisée et permettent de créer le compte hello AD DS requis Azure AD Connect.
* Azure AD Connect prend désormais en charge SQL AOA. Vous devez activer SQL AOA avant d’installer Azure AD Connect. Pendant l’installation, Azure AD Connect détecte si instance SQL de hello fournie est activée pour SQL AOA ou non. Si SQL AOA est activée, Azure AD Connect davantage détermine si SQL AOA est toouse configuré une réplication synchrone ou asynchrone. Lorsque vous configurez hello écouteur du groupe de disponibilité, il est recommandé de définir hello RegisterAllProvidersIP propriété too0. Il s’agit, car Azure AD Connect utilise actuellement SQL Native Client tooconnect tooSQL et SQL Native Client ne prend pas en charge hello propriété MultiSubNetFailover.
* Si vous utilisez base de données locale en tant que base de données hello pour votre serveur Azure AD Connect et a atteint sa limite de taille de 10 Go, hello Service de synchronisation ne démarre plus. Auparavant, vous devez tooperform opération ShrinkDatabase sur hello LocalDB tooreclaim DB suffisamment d’espace pour toostart du Service de synchronisation hello. Après avoir qui, vous pouvez utilisez hello Synchronization Service Manager toodelete exécuter tooreclaim de l’historique plus d’espace de base de données. Maintenant, vous pouvez utiliser toopurge d’applet de commande Start-ADSyncPurgeRunHistory exécuter les données d’historique à partir de l’espace de base de données tooreclaim de base de données locale. En outre, cette applet de commande prend en charge le mode hors connexion (en spécifiant hello - paramètre hors connexion) qui peut être utilisé lorsque hello Service de synchronisation ne fonctionne pas. Remarque : en mode hors connexion hello utilisable uniquement si hello Service de synchronisation ne fonctionne pas et utilisé de la base de données hello est la base de données locale.
* tooreduce hello d’espace de stockage requis, Azure AD Connect compresse maintenant les détails des erreurs de synchronisation avant de les stocker dans les bases de données de base de données locale/SQL. Lors de la mise à niveau à partir d’une version antérieure de Azure AD Connect toothis version, Azure AD Connect effectue une compression à usage unique sur les détails de l’erreur synchronisation existant.
* Précédemment, après la mise à jour d’unité d’organisation de la configuration de filtrage, vous devez exécuter manuellement importation intégrale tooensure objets existants sont correctement inclus/exclus de la synchronisation d’annuaires. Désormais, Azure AD Connect déclenche automatiquement une importation intégrale durant la synchronisation suivante hello cycle. Importation supplémentaire, complète n’est appliqué toohello AD les connecteurs affectés par la mise à jour hello. Remarque : cette amélioration est applicable tooOU filtrage des mises à jour effectuées à l’aide d’Assistant uniquement de hello Azure AD Connect. Il n’est pas applicable tooOU filtrage des mises à jour apportées à l’aide de hello Synchronization Service Manager.
* Auparavant, le filtrage de groupe prenait en charge uniquement les objets Utilisateurs, Groupes et Contacts. Désormais, le filtrage de groupe prend également en charge les objets Ordinateur.
* Auparavant, vous pouviez supprimer les données de l’espace connecteur sans désactiver le planificateur de synchronisation Azure AD Connect. Maintenant, hello Synchronization Service Manager interdit la suppression hello de données de l’espace de connecteur s’il détecte que le planificateur hello est activée. En outre, un avertissement est renvoyé tooinform des clients sur la perte de données potentielle si hello données d’espace de connecteur est supprimé.
* Auparavant, vous devez désactiver la transcription PowerShell pour Azure AD Connect Assistant toorun correctement. Ce problème est partiellement résolu. Vous pouvez activer la transcription PowerShell si vous utilisez une configuration de synchronisation toomanage l’Assistant Azure AD Connect. Vous devez désactiver la transcription PowerShell si vous utilisez la configuration AD FS de toomanage l’Assistant Azure AD Connect.



## <a name="114860"></a>1.1.486.0
Publication : avril 2017

**Problèmes résolus :**
* Problème de hello fixe où Azure AD Connect n’installera pas correctement sur une version localisée de Windows Server.

## <a name="114840"></a>1.1.484.0
Publication : avril 2017

**Problèmes connus :**

* Cette version d’Azure AD Connect ne s’installe pas correctement si hello conditions suivantes est réunie :
   1. Vous mettez à niveau DirSync sur place ou vous effectuez une nouvelle installation d’Azure AD Connect.
   2. Vous utilisez une version localisée de Windows Server où nom hello du groupe d’administrateurs intégré sur le serveur de hello n’est pas « Administrateurs ».
   3. Vous utilisez hello par défaut, SQL Server 2012 Express LocalDB installé avec Azure AD Connect, au lieu de fournir votre propre SQL complète.

**Problèmes résolus :**

Synchronisation d’Azure AD Connect
* Correction d’un problème où le Planificateur de synchronisation hello ignore étape de synchronisation entier hello si un ou plusieurs connecteurs ne disposez pas de profil d’exécution de cette étape de synchronisation. Par exemple, vous avez ajouté manuellement un connecteur à l’aide de hello Gestionnaire de Service de synchronisation sans créer une importation Delta pour ce profil d’exécution. Ce correctif garantit que le planificateur hello synchronisation continue toorun importation Delta pour tous les autres connecteurs.
* Correction d’un problème où hello Service de synchronisation arrête immédiatement le traitement d’un profil d’exécution alors qu’elle ne rencontre un problème avec l’une des étapes de hello exécuter. Ce correctif garantit que hello ignore le Service de synchronisation qui permet d’exécuter étape et continue tooprocess hello rest. Par exemple, vous disposez d’un profil d’exécution Importation d’écart pour votre connecteur AD avec plusieurs étapes d’exécution (une pour chaque domaine AD local). Hello Service de synchronisation s’exécutera importation Delta avec hello autres domaines Active Directory même si un d’eux a des problèmes de connectivité réseau.
* Correction d’un problème qui provoque le toobe de mise à jour de connecteur Azure AD hello ignoré au cours de la mise à niveau automatique.
* Correction d’un problème que tooincorrectly Connect de Azure AD les causes déterminer si le serveur de hello est un contrôleur de domaine pendant l’installation, ce qui en activer provoque DirSync toofail de mise à niveau.
* Fixe à un problème qui provoque DirSync toonot de mise à niveau sur place créer toute exécution profil pour hello connecteur Azure AD.
* Correction d’un problème où interface utilisateur de gestionnaire de Service de synchronisation hello cesse de répondre lors de la tentative de tooconfigure connecteur LDAP générique.

Gestion AD FS.
* Correction d’un problème où Assistant d’Azure AD Connect hello échoue si le nœud principal de hello AD FS a été déplacé tooanother server.

Desktop SSO
* Correction d’un problème dans l’Assistant d’Azure AD Connect hello où hello écran de connexion ne permet pas d’activer la fonctionnalité d’authentification unique de bureau si vous avez choisi de synchronisation de mot de passe en tant que votre option de connexion lors de l’installation de nouveau.

**Nouvelles fonctionnalités/améliorations :**

Synchronisation d’Azure AD Connect
* Azure AD Sync vous connecter prend désormais en charge l’utilisation hello du compte de Service virtuel, compte de Service administré et compte de Service administré groupe comme compte de service. Installation de toonew d’Azure AD Connect seulement s’applique. Lorsque vous installez Azure AD Connect :
    * Par défaut, l’Assistant Azure AD Connect crée un compte de service virtuel et l’utilise en tant que compte de service.
    * Si vous installez sur un contrôleur de domaine, Azure AD Connect revient tooprevious comportement où il va créer un compte d’utilisateur de domaine et utilise à la place comme compte de service.
    * Vous pouvez substituer le comportement par défaut de hello en fournissant des valeurs hello suivantes :
      * Un compte de service géré de groupe
      * Un compte de service géré
      * Un compte d’utilisateur de domaine
      * Un compte d’utilisateur local
* Auparavant, si vous mettez à niveau tooa nouvelle build d’Azure AD Connect contenant connecteurs mettre à jour ou modifications de règle de synchronisation, Azure AD Connect déclenchera un cycle de synchronisation complète. À présent, Azure AD Connect déclenche l’étape Importation complète uniquement pour les connecteurs avec mise à jour, et l’étape Synchronisation complète uniquement pour les connecteurs avec modifications des règles de synchronisation.
* Auparavant, hello exporter un seuil de suppression s’applique uniquement tooexports qui sont déclenchées par le biais du Planificateur de synchronisation hello. Fonctionnalité de hello est désormais exportations tooinclude manuellement déclenchées par client hello hello Synchronization Service Manager.
* Sur votre locataire Azure AD, une configuration de service indique si la fonctionnalité de synchronisation de mot de passe est activée pour votre locataire. Auparavant, il est facile pour toobe de configuration de service hello incorrectement configuré par Azure AD Connect lorsque vous disposez d’un serveur intermédiaire et actif. Désormais, Azure AD Connect va tenter de configuration du service tookeep hello cohérente avec votre active server Azure AD Connect uniquement.
* L’Assistant Azure AD Connect détecte désormais si AD local n’a pas activé la Corbeille AD et envoie un avertissement.
* Précédemment, exportation tooAzure AD expire et échoue si hello combiné à la taille des objets hello dans un lot de hello dépasse certain seuil. Maintenant, hello Service de synchronisation effectue de nouvelles tentatives tooresend des objets de hello dans des lots distincts, plus petits si hello problème est rencontré.
* Hello, application de gestion de clés de Service de synchronisation a été supprimée à partir du Menu Démarrer de Windows. Gestion de clé de chiffrement continue toobe pris en charge via l’interface de ligne de commande à l’aide de miiskmu.exe. Pour plus d’informations sur la gestion de clé de chiffrement, consultez tooarticle [clé de chiffrement de connexion de synchronisation hello Azure AD Abandoning](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-change-serviceacct-pass#abandoning-the-azure-ad-connect-sync-encryption-key).
* Auparavant, si vous modifiez le mot de passe du compte service de synchronisation des Azure AD Connect de hello, hello Service de synchronisation sera pas en mesure de démarrer correctement jusqu'à ce que vous avez abandonné la clé de chiffrement hello et réinitialisation du mot de passe de compte hello Azure AD Connect sync service. À présent, cela n’est plus nécessaire.

Desktop SSO

* Assistant Azure AD Connect ne nécessite plus toobe 9090 de port ouvert sur le réseau de hello lorsque vous configurez l’authentification directe et l’authentification unique de bureau. Seul le port 443 est requis. 

## <a name="114430"></a>1.1.443.0
Publication : mars 2017

**Problèmes résolus :**

Synchronisation d’Azure AD Connect
* Correction d’un problème qui provoque Azure AD Connect Assistant toofail Si nom d’affichage hello Hello connecteur Azure AD ne contient-elle pas de hello initial onmicrosoft.com domaine affecté toohello Azure AD client.
* Correction d’un problème qui provoque toofail d’Assistant Azure AD Connect lorsque vous rendez le base de données de connexion tooSQL lorsque hello de mot de passe du compte de Service de synchronisation de hello contient des caractères spéciaux tels que l’apostrophe, deux-points et un espace.
* Correction d’un problème qui provoque l’erreur de hello toooccur de « hello dimage a une ancre qui est différente de celle des images de hello » sur un serveur en mode de mise en lots d’Azure AD Connect, une fois que vous avez temporairement exclus locale Active Directory de l’objet de la synchronisation et à nouveau pour incluse la synchronisation.
* Correction d’un problème qui provoque l’erreur de hello toooccur de « objet hello localisé par le nom unique est un fantôme » sur un serveur en mode de mise en lots d’Azure AD Connect, une fois que vous avez temporairement exclus locale Active Directory de l’objet de la synchronisation et inclus à nouveau pour la synchronisation.

Gestion AD FS.
* Correction d’un problème où Assistant Azure AD Connect ne pas mettre à jour la configuration AD FS et et hello revendications droite sur hello confiance après avoir configuré un autre ID de connexion.
* Correction d’un problème où Assistant Azure AD Connect est dont les comptes de service sont configurés à l’aide d’userPrincipalName format au lieu du format de sAMAccountName les serveurs toocorrectly Impossible de handle AD FS.

Authentification directe
* Correction d’un problème qui provoque Azure AD Connect Assistant toofail si passer par le biais de l’authentification est activée, mais l’inscription de son connecteur échoue.
* Correction d’un problème qui provoque Azure AD Connect, la validation toobypass Assistant vérifie sur la méthode de connexion sélectionné lors de la fonctionnalité d’authentification unique de bureau est activée.

Réinitialisation de mot de passe
* Correction d’un problème qui peut entraîner hello Azure AAD Connect server toonot tentative toore-se connecter si la connexion de hello a été supprimée par un pare-feu ou un proxy.

**Nouvelles fonctionnalités/améliorations :**

Synchronisation d’Azure AD Connect
* L’applet de commande Get-ADSyncScheduler renvoie désormais une nouvelle propriété booléenne nommée SyncCycleInProgress. Si hello a retourné la valeur est true, que cela signifie qu’il existe un cycle de synchronisation planifiée en cours d’exécution.
* Dossier de destination pour le stockage Azure AD Connect installation et fichiers journaux d’installation a été déplacé à partir de fichiers journaux de la toohello %localappdata%\AADConnect too%programdata%\AADConnect tooimprove d’accessibilité.

Gestion AD FS.
* Prise en charge supplémentaire de la mise à jour du certificat SSL de batterie de serveurs AD FS.
* Prise en charge ajoutée pour la gestion de serveurs AD FS 2016.
* Vous pouvez maintenant spécifier un gMSA (compte de service géré de groupe) existant lors de l’installation d’AD FS.
* Vous pouvez maintenant configurer SHA-256 comme algorithme de hachage de signature hello de confiance Azure AD.

Réinitialisation de mot de passe
* Les améliorations introduites tooallow hello produit toofunction dans des environnements avec des règles de pare-feu plus strictes.
* TooAzure de fiabilité améliorées de connexion Service Bus.

## <a name="113800"></a>1.1.380.0
Publication : décembre 2016

**Problème résolu :**

* Problème de hello fixe où hello issuerid de règles de revendication pour Active Directory Federation Services (ADFS) est manquant dans la génération.

>[!NOTE]
>Cette build n’est pas disponible toocustomers via la fonctionnalité de connecter la mise à niveau automatique de hello Azure AD.

## <a name="113710"></a>1.1.371.0
Publication : décembre 2016

**Problème connu :**

* règle de revendication issuerid Hello pour AD FS est manquant dans la génération. règle de revendication issuerid Hello est requise si vous vous fédérez plusieurs domaines avec Azure Active Directory (Azure AD). Si vous utilisez Azure AD Connect toomanage votre local déploiement AD FS, la mise à niveau de build de toothis supprime la règle de revendication issuerid hello existant de votre configuration AD FS. Vous pouvez contourner problème de hello en ajoutant la règle de revendication hello issuerid après hello installation/mise à niveau. Pour plus d’informations sur l’ajout de hello issuerid de règles de revendication, consultez l’article de toothis sur [prise en charge de plusieurs domaines pour fédérer avec Azure AD](active-directory-aadconnect-multiple-domains.md).

**Problème résolu :**

* Si le Port 9090 n’est pas ouvert pour les connexions sortantes hello, hello Azure AD Connect l’installation ou mise à niveau échoue.

>[!NOTE]
>Cette build n’est pas disponible toocustomers via la fonctionnalité de connecter la mise à niveau automatique de hello Azure AD.

## <a name="113700"></a>1.1.370.0
Publication : décembre 2016

**Problèmes connus :**

* règle de revendication issuerid Hello pour AD FS est manquant dans la génération. règle de revendication issuerid Hello est requise si vous vous fédérez plusieurs domaines avec Azure AD. Si vous utilisez Azure AD Connect toomanage votre local déploiement AD FS, la mise à niveau de build de toothis supprime la règle de revendication issuerid hello existant de votre configuration AD FS. Vous pouvez contourner problème de hello en ajoutant la règle de revendication hello issuerid après installation/mise à niveau. Pour plus d’informations sur l’ajout d’issuerid de règles de revendication, consultez l’article de toothis sur [prise en charge de plusieurs domaines pour fédérer avec Azure AD](active-directory-aadconnect-multiple-domains.md).
* Port 9090 doit être ouvert toocomplete sortant installation.

**Nouvelles fonctionnalités :**

* Authentification directe (version préliminaire).

>[!NOTE]
>Cette build n’est pas disponible toocustomers via la fonctionnalité de connecter la mise à niveau automatique de hello Azure AD.

## <a name="113430"></a>1.1.343.0
Publication : novembre 2016

**Problème connu :**

* règle de revendication issuerid Hello pour AD FS est manquant dans la génération. règle de revendication issuerid Hello est requise si vous vous fédérez plusieurs domaines avec Azure AD. Si vous utilisez Azure AD Connect toomanage votre local déploiement AD FS, la mise à niveau de build de toothis supprime la règle de revendication issuerid hello existant de votre configuration AD FS. Vous pouvez contourner problème de hello en ajoutant la règle de revendication hello issuerid après installation/mise à niveau. Pour plus d’informations sur l’ajout d’issuerid de règles de revendication, consultez l’article de toothis sur [prise en charge de plusieurs domaines pour fédérer avec Azure AD](active-directory-aadconnect-multiple-domains.md).

**Problèmes résolus :**

* Parfois, l’installation d’Azure AD Connect échoue, car il est impossible de toocreate un compte de service local dont un mot de passe est conforme hello de niveau de complexité spécifiée par la stratégie de mot de passe de l’organisation hello.
* Correction d’un problème où les règles de jointure ne sont pas réévaluées lorsqu’un objet dans l’espace de connecteur hello devient simultanément hors de portée pour une règle de jointure et deviennent dans la portée d’un autre. Cela peut se produire si vous avez deux ou plusieurs règles de jointure dont les conditions de jointure s’excluent mutuellement.
* Correction d’un problème dans lequel les règles de synchronisation entrante (à partir d’Azure AD) qui ne contiennent pas de règles de jointure ne sont pas traitées si elles ont des valeurs de priorité plus faibles que celles contenant des règles de jointure.

**Améliorations :**

* Ajout de la prise en charge de l’installation d’Azure AD Connect sur Windows Server 2016 standard ou version ultérieure.
* Ajout de la prise en charge l’utilisation de SQL Server 2016 comme base de données distante hello pour Azure AD Connect.

## <a name="112810"></a>1.1.281.0
Publication : août 2016

**Problèmes résolus :**

* Intervalle de toosync de modifications ne prendront place jusqu'à ce qu’après hello prochain cycle de synchronisation est terminée.
* L’Assistant Azure AD Connect n’accepte pas de compte Azure AD dont le nom d’utilisateur commence par un trait de soulignement (\_).
* Assistant Azure AD Connect échoue compte Azure AD de hello tooauthenticate si le mot de passe de compte hello contient trop de caractères spéciaux. Message d’erreur « Impossible de toovalidate les informations d’identification. Une erreur inattendue s’est produite. » est renvoyé.
* Désinstallation du serveur de test désactive la synchronisation de mot de passe dans le locataire Azure AD et provoque le toofail de synchronisation de mot de passe avec le serveur actif.
* Synchronisation de mot de passe échoue dans de rares cas, lorsqu’il n’existe aucun hachage de mot de passe stocké sur l’utilisateur de hello.
* Lorsque le serveur Azure AD Connect est activé pour le mode intermédiaire, la réécriture du mot de passe n’est pas temporairement désactivée.
* Assistant Azure AD Connect n’affiche pas de synchronisation de mot de passe réel hello et configuration de l’écriture différée de mot de passe lorsque le serveur est en mode de mise en lots. Il les affiche toujours comme étant désactivées.
* Synchronisation toopassword des modifications de configuration et d’écriture différée de mot de passe ne sont pas conservés par l’Assistant Azure AD Connect lorsque le serveur est en mode de mise en lots.

**Améliorations :**

* Mise à jour tooindicate d’applet de commande hello ADSyncSyncCycle de démarrer si elle est toosuccessfully en mesure de démarrer un nouveau cycle de synchronisation ou non.
* Cycle de synchronisation tooterminate ajouté hello Stop-ADSyncSyncCycle applet de commande et l’opération, qui sont actuellement en cours d’exécution.
* Cycle de synchronisation tooterminate mis à jour hello Stop-ADSyncScheduler applet de commande et l’opération, qui sont actuellement en cours d’exécution.
* Lors de la configuration [extensions d’annuaire](active-directory-aadconnectsync-feature-directory-extensions.md) dans l’Assistant Azure AD Connect, hello Azure AD attribut de type « Chaîne télétexte » peut maintenant être sélectionné.

## <a name="111890"></a>1.1.189.0
Publication : juin 2016

**Problèmes résolus et améliorations :**

* Vous pouvez maintenant installer Azure AD Connect sur un serveur compatible FIPS.
  * Pour la synchronisation du mot de passe, consultez [Synchronisation de mot de passe et FIPS](active-directory-aadconnectsync-implement-password-synchronization.md#password-synchronization-and-fips).
* Correction d’un problème où un nom NetBIOS ne pourrait pas être résolu toohello nom de domaine complet dans hello connecteur Active Directory.

## <a name="111800"></a>1.1.180.0
Publication : mai 2016

**Nouvelles fonctionnalités :**

* Vous avertit et vous permet de vérifier les domaines si vous ne l’avez pas fait avant d’exécuter Azure AD Connect.
* Ajout de la prise en charge de [Microsoft Cloud Allemagne](active-directory-aadconnect-instances.md#microsoft-cloud-germany).
* Prise en charge de hello dernières [cloud de Microsoft Azure Government](active-directory-aadconnect-instances.md#microsoft-azure-government-cloud) infrastructure avec les nouvelles exigences de l’URL.

**Problèmes résolus et améliorations :**

* Toohello filtrage ajouté toomake de l’éditeur de règles de synchronisation il toofind facilement les règles de synchronisation.
* Amélioration des performances lors de la suppression d’un espace connecteur.
* Correction d’un problème lorsque hello même objet a été supprimé et ajouté dans hello même série (appelée delete/ajouter).
* Une règle de synchronisation désactivée ne réactive plus les attributs et objets inclus lors d’une mise à niveau ou d’une actualisation de schéma d’annuaire.

## <a name="111300"></a>1.1.130.0
Publication : avril 2016

**Nouvelles fonctionnalités :**

* Prise en charge pour les attributs à valeurs multiples trop[extensions active](active-directory-aadconnectsync-feature-directory-extensions.md).
* Prise en charge de plusieurs variantes de configuration pour [mise à niveau automatique](active-directory-aadconnect-feature-automatic-upgrade.md) toobe considérés comme éligibles pour la mise à niveau.
* Ajout d’applets de commande pour le [planificateur personnalisé](active-directory-aadconnectsync-feature-scheduler.md#custom-scheduler).

## <a name="111190"></a>1.1.119.0
Publication : mars 2016

**Problèmes résolus :**

* Nous nous sommes assurés que l’installation Express ne peut pas être utilisée sur Windows Server 2008 (version antérieure à R2), car la synchronisation du mot de passe n’est pas prise en charge sur ce système d’exploitation.
* La mise à niveau à partir de DirSync avec une configuration de filtre personnalisée n’a pas fonctionné comme prévu.
* Lors de la mise à niveau tooa une version plus récente et il n’y aucune configuration toohello de modifications, une importation/la synchronisation complète ne doit pas être planifiée.

## <a name="111100"></a>1.1.110.0
Publication : février 2016

**Problèmes résolus :**

* Mise à niveau à partir de versions antérieures ne fonctionne pas si l’installation de hello n’est pas dans le dossier C:\Program Files de par défaut hello.
* Si vous installez et que vous désactivez **démarrer le processus de synchronisation hello** à fin hello de l’Assistant installation Bonjour, exécution de l’Assistant installation hello une deuxième fois n’active pas le planificateur hello.
* Hello planificateur ne fonctionne pas comme prévu sur les serveurs où hello format de date/heure US-en n'est pas utilisée. Il bloque également `Get-ADSyncScheduler` tooreturn les moments appropriés.
* Si vous avez installé une version antérieure d’Azure AD Connect avec AD FS comme hello mise à niveau et l’option de connexion, vous ne peut pas exécuter l’Assistant installation Bonjour à nouveau.

## <a name="111050"></a>1.1.105.0
Publication : février 2016

**Nouvelles fonctionnalités :**

* [Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) pour les clients de la configuration rapide.
* Prise en charge pour un administrateur global à l’aide de l’authentification multifacteur Azure et Privileged Identity Management dans l’Assistant installation hello hello.
  * Vous devez tooallow votre tooalso proxy autoriser le trafic toohttps://secure.aadcdn.microsoftonline-p.com si vous utilisez l’authentification multifacteur.
  * Vous avez besoin de liste de sites de confiance tooadd https://secure.aadcdn.microsoftonline-p.com tooyour pour travail tooproperly de l’authentification multifacteur.
* Autoriser la modification de la méthode d’authentification de l’utilisateur hello après l’installation initiale.
* Autoriser [domaine et unité d’organisation filtrage](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) dans l’Assistant installation hello. Cela vous permet également de connexion tooforests où pas tous les domaines sont disponibles.
* [Planificateur](active-directory-aadconnectsync-feature-scheduler.md) est généré dans le moteur de synchronisation toohello.

**Fonctionnalités promues à partir de la version préliminaire tooGA :**

* [Écriture différée des appareils](active-directory-aadconnect-feature-device-writeback.md).
* [Extensions d’annuaire](active-directory-aadconnectsync-feature-directory-extensions.md).

**Nouvelles fonctionnalités préliminaires :**

* Hello nouvelle valeur par défaut cycle de synchronisation intervalle est de 30 minutes. Utilisé toobe trois heures pour toutes les versions antérieures. Ajoute la prise en charge toochange hello [planificateur](active-directory-aadconnectsync-feature-scheduler.md) comportement.

**Problèmes résolus :**

* Hello Vérifiez la page de domaines DNS n’a pas toujours reconnaître les domaines hello.
* Demande d’informations d’identification de l’administrateur de domaine lors de la configuration AD FS.
* Hello localement les comptes Active Directory ne sont pas reconnues par l’Assistant installation hello si situé dans un domaine avec une autre arborescence DNS que le domaine racine de hello.

## <a name="1091310"></a>1.0.9131.0
Publication : décembre 2015

**Problèmes résolus :**

* La synchronisation de mot de passe peut ne pas fonctionner lorsque vous modifiez les mots de passe dans Active Directory Domain Services (AD DS), mais elle fonctionne lorsque vous définissez un mot de passe.
* Lorsque vous avez un serveur proxy, tooAzure d’authentification Active Directory risque d’échouer lors de l’installation, ou si une mise à niveau est annulée sur la page de configuration hello.
* La mise à jour à partir d’une version antérieure d’Azure AD Connect avec une instance SQL Server complète échoue si vous n’êtes pas administrateur système SQL Server (SA).
* Mise à jour d’une version précédente d’Azure AD Connect avec un serveur SQL distant affiche erreur « Impossible de tooaccess hello de base de données SQL ADSync » de hello.

## <a name="1091250"></a>1.0.9125.0
Publication : novembre 2015

**Nouvelles fonctionnalités :**

* Pouvez reconfigurer AD FS tooAzure AD trust.
* Peut actualiser le schéma Active Directory de hello et régénérer les règles de synchronisation.
* Désactivation d'une règle de synchronisation.
* Définition d’« AuthoritativeNull » comme nouvelle chaîne littérale dans une règle de synchronisation.

**Nouvelles fonctionnalités préliminaires :**

* [Azure AD Connect Health pour la synchronisation](../connect-health/active-directory-aadconnect-health-sync.md).
* Prise en charge de la synchronisation de mot de passe pour les [services de domaine Azure AD](../active-directory-passwords-update-your-own-password.md) .

**Nouveau scénario pris en charge :**

* Prise en charge de plusieurs organisations Exchange locales Pour plus d’informations, consultez la rubrique [Déploiements hybrides à forêts Active Directory multiples](https://technet.microsoft.com/library/jj873754.aspx).

**Problèmes résolus :**

* Problèmes liés à la synchronisation de mot de passe :
  * Un objet déplacé hors de portée tooin-champ d’application n’aura pas son mot de passe synchronisé. Cela est valable pour l’unité d’organisation et le filtrage des attributs.
  * Sélection d’un nouveau tooinclude d’unité d’organisation synchronisé ne nécessite pas une synchronisation de mot de passe.
  * Mot de passe hello n’est pas synchronisée lorsqu’un utilisateur désactivé est activé.
  * file d’attente des nouvelles tentatives de mot de passe Hello est infinie et limite précédente de hello de 5 000 objets toobe mis hors service a été supprimé.
* N’a pas pu tooconnect tooActive active avec le niveau fonctionnel de forêt de Windows Server 2016.
* N’a pas pu toochange groupe hello qui est utilisé pour le filtrage de groupe après l’installation initiale de hello.
* Ne plus crée un nouveau profil utilisateur sur le serveur d’Azure AD Connect hello pour chaque utilisateur effectuant une modification de mot de passe avec écriture différée de mot de passe activée.
* N’a pas pu toouse entier Long les valeurs des étendues de règles de synchronisation.
* case à cocher « l’écriture différée de l’appareil » Hello reste désactivé s’il existe des contrôleurs de domaine inaccessibles.

## <a name="1086670"></a>1.0.8667.0
Publication : août 2015

**Nouvelles fonctionnalités :**

* Bonjour Azure AD Connect, l’Assistant installation est désormais localisé langues de Windows Server tooall.
* Prise en charge du déverrouillage de compte lors de l’utilisation de la gestion des mots de passe d’Azure AD.

**Problèmes résolus :**

* Assistant installation de Azure AD Connect se bloque si un autre utilisateur poursuit installation plutôt que personne hello démarré pour la première installation de hello.
* Si une précédente désinstallation d’Azure AD Connect échoue synchronisation d’Azure AD Connect toouninstall correctement, il n’est pas possible de tooreinstall.
* Impossible d’installer Azure AD Connect à l’aide d’installation d’Express si hello n’est pas dans le domaine racine de hello de forêt de hello ou si une version non anglaise de Active Directory est utilisée.
* Si hello nom de domaine complet de hello compte d’utilisateur Active Directory ne peut pas être résolu, un message d’erreur trompeur « Schema de hello n’a pas pu toocommit » est indiqué.
* Si le compte hello utilisé sur hello connecteur Active Directory est modifié en dehors de l’Assistant de hello, Assistant de hello échoue lors des exécutions suivantes.
* Azure AD Connect échoue parfois tooinstall sur un contrôleur de domaine.
* Impossible d’activer et de désactiver le « Mode de préproduction » si des attributs d’extension ont été ajoutés.
* L’écriture différée de mot de passe échoue dans certaines configurations en raison d’un mot de passe incorrect sur hello connecteur Active Directory.
* Impossible de mettre à niveau DirSync si un nom unique (DN) est utilisé lors du filtrage des attributs.
* Utilisation du processeur excessive lors de la réinitialisation du mot de passe.

**Fonctionnalités préliminaires supprimées :**

* fonctionnalité d’aperçu Hello [l’écriture différée de l’utilisateur](active-directory-aadconnect-feature-preview.md#user-writeback) a été temporairement supprimé en fonction des commentaires de nos clients de la version préliminaire. Il est ajouté ultérieurement une fois que nous avons abordé hello fourni des commentaires.

## <a name="1086410"></a>1.0.8641.0
Publication : juin 2015

**Version initiale d’Azure AD Connect.**

Nom modifié à partir d’Azure AD Sync tooAzure AD Connect.

**Nouvelles fonctionnalités :**

* Installation à l’aide de la [configuration rapide](active-directory-aadconnect-get-started-express.md)
* [Configuration d’AD FS](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs)
* [Mise à niveau à partir de DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md)
* [Prévention des suppressions accidentelles](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)
* Introduction du [mode intermédiaire](active-directory-aadconnectsync-operations.md#staging-mode)

**Nouvelles fonctionnalités préliminaires :**

* [Écriture différée de l’utilisateur](active-directory-aadconnect-feature-preview.md#user-writeback)
* [Écriture différée de groupe](active-directory-aadconnect-feature-preview.md#group-writeback)
* [Écriture différée des appareils](active-directory-aadconnect-feature-device-writeback.md)
* [Extensions d’annuaire](active-directory-aadconnect-feature-preview.md)

## <a name="104940501"></a>1.0.494.0501
Publication : mai 2015

**Nouvelle condition requise**

* Azure AD Sync requiert désormais hello .NET Framework version 4.5.1 toobe est installé.

**Problèmes résolus :**

* L’écriture différée de mot de passe à partir d’Azure AD échoue en raison d’une erreur de connectivité Azure Service Bus.

## <a name="104910413"></a>1.0.491.0413
Publication : avril 2015

**Problèmes résolus et améliorations :**

* Hello connecteur Active Directory ne traite pas correctement les suppressions si Corbeille hello est activée et il existe plusieurs domaines dans la forêt de hello.
* performances Hello des opérations d’importation a été améliorée pour hello le connecteur Active Directory.
* Lorsqu’un groupe a dépassé la limite d’appartenance hello (par défaut, la limite de hello a la valeur too50, 000 objets), groupe de hello a été supprimé dans Azure Active Directory. Avec le nouveau comportement de hello, groupe de hello n’est pas supprimé, une erreur est générée et nouvelle modification d’appartenance n’est pas exportées.
* Un nouvel objet ne peut pas être configuré si une suppression intermédiaire avec hello que même nom de domaine est déjà présente dans l’espace de connecteur hello.
* Certains objets sont marquées pour la synchronisation pendant une synchronisation delta bien qu’il n’existe aucune modification intermédiaire sur l’objet de hello.
* Forcer une synchronisation de mot de passe supprime également la liste de contrôleur de domaine hello préféré.
* CSExportAnalyzer a des problèmes avec certains états des objets.

**Nouvelles fonctionnalités :**

* Une jointure peut maintenant se connecter à trop « ANY » type d’objet dans hello MV.

## <a name="104850222"></a>1.0.485.0222
Publication : février 2015

**Améliorations :**

* Performances de l’importation améliorées.

**Problèmes résolus :**

* Synchronisation de mot de passe respecte l’attribut cloudFiltered hello qui est utilisé par le filtrage d’attributs. Les objets filtrés ne sont plus dans la portée pour la synchronisation de mot de passe.
* Dans les rares cas où la topologie de hello avait plusieurs contrôleurs de domaine, synchronisation de mot de passe ne fonctionne pas.
* « Serveur arrêté » lors de l’importation à partir du connecteur Azure AD de hello après la gestion de périphérique a été activée dans Azure AD/Intune.
* La jonction d’entités de sécurité externes à partir de plusieurs domaines dans la même forêt provoque une erreur de jonction ambiguë.

## <a name="104751202"></a>1.0.475.1202
Publication : décembre 2014

**Nouvelles fonctionnalités :**

* Il est maintenant possible d’effectuer la synchronisation de mot de passe avec le filtrage basé sur les attributs. Pour plus d’informations, consultez [Synchronisation de mot de passe avec filtrage](active-directory-aadconnectsync-configure-filtering.md).
* attribut msDS-ExternalDirectoryObjectID de Hello est réécrites tooActive active. Cette fonctionnalité prend en charge les applications Office 365. Il utilise OAuth2 tooaccess des boîtes aux lettres en ligne et en local dans un déploiement Exchange hybride.

**Problèmes de mise à niveau résolus :**

* Une version plus récente de l’assistant de connexion hello est disponible sur le serveur de hello.
* Un chemin d’installation personnalisé a été utilisé tooinstall Azure AD Sync.
* Une jointure personnalisé incorrect critère blocs hello mise à niveau.

**Autres correctifs :**

* Modèles de hello fixe pour Office Pro Plus.
* Résolution des problèmes d’installation provoqué par des noms d’utilisateurs commençant par un tiret.
* Fixe perdante hello paramètre sourceAnchor lors de l’exécution de l’Assistant installation hello une deuxième fois.
* Résolution du traçage ETW pour la synchronisation de mot de passe.

## <a name="104701023"></a>1.0.470.1023
Publication : octobre 2014

**Nouvelles fonctionnalités :**

* Synchronisation de mot de passe à partir de plusieurs locaux Active Directory tooAzure AD.
* Langues de Windows Server tooall installation localisée l’interface utilisateur.

**Mise à niveau à partir d’Azure Active Directory Sync 1.0 GA**

Si vous avez déjà installé Azure AD Sync, il est une étape supplémentaire que vous avez tootake au cas où vous avez modifié une des règles de synchronisation d’out-of-box hello. Une fois que vous avez mis à niveau toohello 1.0.470.1023 version, vous avez modifié les règles de synchronisation hello sont dupliquées. Pour chaque règle de synchronisation modifiée, hello suivant :

1.  Recherchez la règle de synchronisation hello vous avez modifié et prenez note des modifications de hello.
* Supprimer la règle de synchronisation hello.
* Localisez hello nouvelle règle de synchronisation qui est créée par Azure AD Sync et réappliquez les modifications hello.

**Autorisations pour hello compte Active Directory**

Hello compte Active Directory doit disposer de hachages de mot de passe des autorisations supplémentaires toobe tooread en mesure de hello à partir d’Active Directory. Hello autorisations toogrant sont nommées « Réplication des modifications d’annuaire » et « Répertoire de la réplication de toutes les modifications. » Les deux autorisations sont des hachages de mot de passe requis toobe tooread en mesure de hello.

## <a name="104190911"></a>1.0.419.0911
Publication : septembre 2014

**Version initiale d’Azure AD Sync.**

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).
