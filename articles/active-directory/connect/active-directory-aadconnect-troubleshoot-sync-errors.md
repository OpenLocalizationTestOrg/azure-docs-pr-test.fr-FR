---
title: "Azure AD Connect : Résolution des erreurs lors de la synchronisation | Microsoft Docs"
description: Explique comment tootroubleshoot erreurs se produisent pendant la synchronisation avec Azure AD Connect.
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 2209d5ce-0a64-447b-be3a-6f06d47995f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: af262dfe95d686e34697454c0dfe8b4a6d8693c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-errors-during-synchronization"></a>Résolution des erreurs lors de la synchronisation
Erreurs peuvent se produire lorsque les données d’identité sont synchronisées à partir de Windows Server Active Directory (AD DS) tooAzure Active Directory (Azure AD). Cet article fournit une vue d’ensemble des différents types d’erreurs de synchronisation, certains des scénarios possibles hello qui provoquent ces erreurs et les erreurs de hello toofix façons potentielles. Cet article inclut les types d’erreurs courantes hello et ne peut-être pas couvrir toutes les erreurs possibles hello.

 Cet article suppose hello lecteur connaît hello sous-jacent [concevoir des concepts d’Azure AD et Azure AD Connect](active-directory-aadconnect-design-concepts.md).

Avec la version la plus récente d’Azure AD Connect hello \(août 2016 ou version ultérieure\), un rapport d’erreurs de synchronisation est disponible dans hello [portail Azure](https://aka.ms/aadconnecthealth) dans le cadre d’Azure AD Connect Health pour la synchronisation.

En commençant le 1er septembre 2016 [Azure Active Directory en double attribut résilience](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) fonctionnalité sera activée par défaut pour tous les hello *nouveau* clients Active Directory de Azure. Cette fonctionnalité sera automatiquement activée pour les clients existants dans les mois à venir hello.

Azure AD Connect effectue des 3 types d’opérations à partir de répertoires hello il maintient synchronisé : synchronisation, importation et l’exportation. Les erreurs peuvent avoir lieu dans toutes les opérations de hello. Cet article se concentre principalement sur les erreurs au cours de l’exportation tooAzure AD.

## <a name="errors-during-export-tooazure-ad"></a>Erreurs au cours de l’exportation tooAzure AD
Suivant la section décrit les différents types de synchronisation, les erreurs qui peuvent se produire pendant hello exportation opération tooAzure AD à l’aide hello connecteur Azure AD. Ce connecteur peut être identifié par le format du nom hello est « contoso. *onmicrosoft.com*».
Erreurs au cours de l’exportation tooAzure AD indiquent cette opération hello \(ajouter, mettre à jour, supprimer etc.\) tentée par Azure AD Connect \(moteur de synchronisation\) sur Azure Active Directory a échoué.

![Vue d’ensemble des erreurs d’exportation](./media/active-directory-aadconnect-troubleshoot-sync-errors/Export_Errors_Overview_01.png)

## <a name="data-mismatch-errors"></a>Erreurs d’incohérence de données
### <a name="invalidsoftmatch"></a>InvalidSoftMatch
#### <a name="description"></a>Description
* Lorsque Azure AD Connect \(moteur de synchronisation\) indique à Azure Active Directory tooadd mise à jour des objets ou, Azure AD correspondances hello objet entrant à l’aide de hello **sourceAnchor** attribut toohello  **immutableId** attribut des objets dans Azure AD. Cette correspondance est appelée une **Correspondance exacte**.
* Lorsque Azure AD **ne trouve pas** tout objet qui correspond à hello **immutableId** attribut avec hello **sourceAnchor** attribut d’objet entrants hello, avant de configurer un nouvel objet, il repasse toouse hello ProxyAddresses et les attributs UserPrincipalName toofind une correspondance. Cette correspondance est appelée une **Correspondance souple**. Hello correspondance conditionnelle est déjà présent dans Azure AD (qui sont générés dans Azure AD) d’objets toomatch conçue avec hello de nouveaux objets est ajouté ou mis à jour pendant la synchronisation qui représentent les hello même entité (utilisateurs, groupes) en local.
* **InvalidSoftMatch** erreur se produit lorsque hello correspondance exacte ne trouve pas de n’importe quel objet correspondant **AND** correspondance conditionnelle recherche un objet correspondant, mais cet objet a une valeur différente de *immutableId* que hello l’objet entrant *SourceAnchor*, suggérant que hello de correspondance d’objet a été synchronisé avec un autre objet à partir de l’annuaire Active Directory local.

En d’autres termes, dans l’ordre pour hello correspondance conditionnelle toowork, toobe d’objet hello soft-associée doit a pas de valeur pour hello *immutableId*. Si un objet avec *immutableId* ensemble avec une valeur échoue critères de soft-match hello hello correspondance permanente mais satisfaisant, opération de hello entraînerait une erreur de synchronisation InvalidSoftMatch.

Azure Active Directory schéma n’autorise pas les deux ou plusieurs objets toohave hello même valeur hello suivant d’attributs. \(Cette liste est non exhaustive :\)

* ProxyAddresses
* UserPrincipalName
* onPremisesSecurityIdentifier
* ID d’objet

> [!NOTE]
> [Azure AD attribut dupliquer la résilience d’attribut](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) fonctionnalité est également transférée en tant que comportement par défaut de hello d’Azure Active Directory.  Cela réduira le nombre de hello d’erreurs de synchronisation détectées par Azure AD Connect (ainsi que d’autres clients de synchronisation) en apportant Azure AD plus résilient de façon hello qu'il gère les dupliqué ProxyAddresses et UserPrincipalName attributs présents dans sur AD local environnements. Cette fonctionnalité ne résout pas les erreurs de duplication hello. Par conséquent, les données de salutation doivent toujours toobe fixe. Mais elle permet l’approvisionnement de nouveaux objets qui sont bloqués dans le cas contraire d’être configuré en raison de valeurs de tooduplicated dans Azure AD. Cela permet également de réduire nombre hello des erreurs de synchronisation retourné du client de synchronisation toohello.
> Si cette fonctionnalité est activée pour votre client, vous ne verrez pas les erreurs de synchronisation InvalidSoftMatch hello observés pendant la configuration de nouveaux objets.
>
>

#### <a name="example-scenarios-for-invalidsoftmatch"></a>Exemples de scénarios pour InvalidSoftMatch
1. Deux objets ou plus avec hello même valeur d’attribut ProxyAddresses existe dans Active Directory locale. Un seul est provisionné dans Azure AD.
2. Deux objets ou plus avec hello même valeur userPrincipalName existe dans Active Directory locale. Un seul est provisionné dans Azure AD.
3. Un objet a été ajouté dans hello sur le site Active Directory avec hello même valeur d’attribut ProxyAddresses que celle d’un objet existant dans Azure Active Directory. objet Hello ajouté localement n’est pas mise en route approvisionné dans Azure Active Directory.
4. Un objet a été ajouté dans sur le site Active Directory avec hello même valeur de l’attribut userPrincipalName que celle d’un compte dans Azure Active Directory. objet de Hello n’est pas mise en route approvisionné dans Azure Active Directory.
5. Un compte synchronisé a été déplacé à partir de la forêt A tooForest b. Azure AD Connect (moteur de synchronisation) utilisait hello de toocompute ObjectGUID attribut SourceAnchor. Après le déplacement de forêt hello, valeur hello hello SourceAnchor est différent. nouvel objet de Hello (à partir de la forêt B) est en cours toosync avec un objet existant de hello dans Azure AD.
6. Un objet synchronisé a été accidentellement supprimé sur l’annuaire Active Directory local et un nouvel objet a été créé dans Active Directory pour hello même entité (par exemple, utilisateur) sans supprimer le compte hello dans Azure Active Directory. nouveau compte de Hello échoue toosync avec l’objet d’Azure AD existant hello.
7. Azure AD Connect a été désinstallé et réinstallé. Au cours de la réinstallation de hello, un autre attribut a été choisi comme hello SourceAnchor. Tous les objets de hello qui étaient précédemment synchronisés arrêté la synchronisation avec l’erreur de InvalidSoftMatch.

#### <a name="example-case"></a>Exemple de scénario :
1. **Bob Smith** est un utilisateur synchronisé dans Azure Active Directory à partir d’un Active Directory local de *contoso.com*
2. La valeur **UserPrincipalName** de Bob Smith est définie sur **bobs@contoso.com**.
3. **« abcdefghijklmnopqrstuv == «** est hello **SourceAnchor** calculé par Azure AD Connect à l’aide de Bob Smith **objectGUID** sur le site Active Directory, qui est hello **immutableId** pour Bob Smith dans Azure Active Directory.
4. Bob a également les valeurs pour hello suivantes **proxyAddresses** attribut :
   * smtp:bobs@contoso.com
   * smtp:bob.smith@contoso.com
   * **smtp:bob@contoso.com**
5. Un nouvel utilisateur, **Bob Taylor**, est ajouté toohello sur le site Active Directory.
6. La valeur **UserPrincipalName** de Bob Taylor est définie sur **bobt@contoso.com**.
7. **« abcdefghijkl0123456789 == » «** est hello **sourceAnchor** calculé par Azure AD Connect à l’aide de Bob Taylor **objectGUID** des locaux à partir d’Active Directory. Les objets de Bob Taylor n’a pas encore synchronisé tooAzure Active Directory.
8. Bob Taylor a hello valeurs pour l’attribut proxyAddresses de hello suivantes
   * smtp:bobt@contoso.com
   * smtp:bob.taylor@contoso.com
   * **smtp:bob@contoso.com**
9. Pendant la synchronisation, Azure AD Connect sera reconnaît l’ajout de hello de Bob Taylor dans Active Directory localement et demandez à Azure AD toomake hello même modification.
10. Azure AD effectue d’abord la correspondance exacte. Autrement dit, il effectue une recherche si n’importe quel objet avec hello immutableId est trop égal » abcdefghijkl0123456789 == ». La correspondance exacte échoue car aucun autre objet dans Azure AD n’a cette valeur d’attribut immutableId.
11. Azure AD devra ensuite tenter de toosoft-match Bob Taylor. Autrement dit, il recherche si n’importe quel objet avec les toohello égal proxyAddresses trois valeurs, y comprissmtp:bob@contoso.com
12. Azure AD trouvera les objets de Bob Smith critères de correspondance de soft toomatch hello. Mais cet objet a la valeur hello immutableId = « abcdefghijklmnopqrstuv == ». qui indique cet objet a été synchronisé à partir d’un autre objet sur un Active Directory local. Par conséquent, Azure AD ne peut pas établir de correspondance souple sur ces objets et cause une erreur de synchronisation **InvalidSoftMatch**.

#### <a name="how-toofix-invalidsoftmatch-error"></a>Comment toofix InvalidSoftMatch erreur
deux objets différents SourceAnchor est Hello raison la plus courante pour hello InvalidSoftMatch erreur \(immutableId\) ont hello même valeur pour hello ProxyAddresses et/ou UserPrincipalName attributs qui sont utilisés pendant hello processus soft-match sur Azure AD. Dans l’ordre toofix hello correspondance conditionnelle non valide

1. Identifiez hello dupliqué proxyAddresses, userPrincipalName ou une autre valeur d’attribut qui provoque l’erreur de hello. Également identifier les deux \(ou plus\) objets impliqués dans le conflit de hello. Hello rapport généré par [Azure AD Connect Health pour la synchronisation](https://aka.ms/aadchsyncerrors) peut vous aider à identifier les hello deux objets.
2. Identifier l’objet qui doit continuer à valeur de hello dupliqué toohave et objet qui ne doit pas.
3. Supprimer les valeur hello dupliqué à partir de l’objet hello n’ayant pas cette valeur. Notez que vous devez vous hello modifier dans le répertoire hello où l’objet de hello en provenance de. Dans certains cas, vous devrez peut-être toodelete un des objets hello en conflit.
4. Si vous avez apporté hello modifier Bonjour sur AD local, permettent hello de synchronisation Azure AD Connect à modifier.

Notez que le rapport d’erreurs de synchronisation dans Azure AD Connect Health pour la synchronisation est de mise à jour toutes les 30 minutes et inclut les erreurs hello à partir de la dernière tentative de synchronisation hello.

> [!NOTE]
> ImmutableId, par définition, ne modifiez pas de durée de vie hello d’objet de hello. Si Azure AD Connect n’était pas configuré avec certains des scénarios hello dans une perspective hello au-dessus de liste, vous pourriez finir dans une situation où Azure AD Connect calcule une valeur différente de hello SourceAnchor pour objet hello AD que représente hello même entité (même utilisateur / groupe/contact, etc.) qui a un objet d’Active Directory Azure existant que vous le souhaitez à l’aide de toocontinue.
>
>

#### <a name="related-articles"></a>Articles connexes
* [Les attributs en double ou non valides empêchent la synchronisation d’annuaires dans Office 365](https://support.microsoft.com/en-us/kb/2647098)

### <a name="objecttypemismatch"></a>ObjectTypeMismatch
#### <a name="description"></a>Description
Quand Azure AD tente toosoft correspondance deux objets, il est possible que deux objets de différentes « type d’objet » (par exemple, utilisateur, groupe, Contact etc.) ont hello mêmes valeurs pour les attributs hello utilisé correspondance conditionnelle de tooperform hello. Comme la duplication de ces attributs n’est pas autorisée dans Azure AD, hello opération pouvez par erreur de synchronisation « ObjectTypeMismatch ».

#### <a name="example-scenarios-for-objecttypemismatch-error"></a>Exemples de scénarios pour l’erreur ObjectTypeMismatch
* Un groupe de sécurité activé pour la messagerie est créé dans Office 365. Administrateur ajoute un nouvel utilisateur ou un contact dans sur AD local (qui n’a pas synchronisé tooAzure AD encore) avec la même valeur pour l’attribut ProxyAddresses de hello que hello Office 365 de hello de groupe.

#### <a name="example-case"></a>Exemple de scénario
1. Administrateur crée un nouveau groupe de sécurité de messagerie dans Office 365 pour service de taxe hello et fournit une adresse de messagerie en tant que tax@contoso.com. Cela affecte l’attribut ProxyAddresses de hello pour ce groupe avec la valeur hello**smtp:tax@contoso.com**
2. Un nouvel utilisateur rejoint Contoso.com et un compte est créé pour l’utilisateur de hello sur site avec proxyAddress hello en tant que**smtp:tax@contoso.com**
3. Lorsque Azure AD Connect sera synchronisé le nouveau compte d’utilisateur hello, il obtient hello « ObjectTypeMismatch » erreur.

#### <a name="how-toofix-objecttypemismatch-error"></a>Comment toofix ObjectTypeMismatch erreur
Hello plus souvent pour l’erreur de ObjectTypeMismatch hello est de deux objets d’un type différent (utilisateur, groupe, Contact etc.) ont hello même valeur pour l’attribut ProxyAddresses de hello. Dans l’ordre toofix hello ObjectTypeMismatch :

1. Identifier hello dupliqué proxyAddresses (ou tout autre attribut) valeur d’erreur hello à l’origine. Également identifier les deux \(ou plus\) objets impliqués dans le conflit de hello. Hello rapport généré par [Azure AD Connect Health pour la synchronisation](https://aka.ms/aadchsyncerrors) peut vous aider à identifier les hello deux objets.
2. Identifier l’objet qui doit continuer à valeur de hello dupliqué toohave et objet qui ne doit pas.
3. Supprimer les valeur hello dupliqué à partir de l’objet hello n’ayant pas cette valeur. Notez que vous devez vous hello modifier dans le répertoire hello où l’objet de hello en provenance de. Dans certains cas, vous devrez peut-être toodelete un des objets hello en conflit.
4. Si vous avez apporté hello modifier Bonjour sur AD local, permettent hello de synchronisation Azure AD Connect à modifier. Rapport d’erreurs de synchronisation dans Azure AD Connect Health pour la synchronisation des mises à jour toutes les 30 minutes et inclut des erreurs hello à partir de la dernière tentative de synchronisation hello.

## <a name="duplicate-attributes"></a>Attributs en double
### <a name="attributevaluemustbeunique"></a>AttributeValueMustBeUnique
#### <a name="description"></a>Description
Azure Active Directory schéma n’autorise pas les deux ou plusieurs objets toohave hello même valeur hello suivant d’attributs. C'est-à-dire, que chaque objet dans Azure AD est forcé toohave une valeur unique de ces attributs à une instance donnée.

* ProxyAddresses
* UserPrincipalName

Si Azure AD Connect tente tooadd un nouvel objet ou mettre à jour un objet existant avec une valeur pour hello au-dessus des attributs qui est déjà affecté objet tooanother dans Azure Active Directory, hello opération entraîne erreur de synchronisation hello « AttributeValueMustBeUnique ».

#### <a name="possible-scenarios"></a>Scénarios possibles :
1. Valeur en double est un objet déjà synchronisé tooan attribué, qui est en conflit avec un autre objet synchronisé.

#### <a name="example-case"></a>Exemple de scénario :
1. **Bob Smith** est un utilisateur synchronisé dans Azure Active Directory à partir d’un Active Directory local de contoso.com
2. La valeur **UserPrincipalName** locale de Bob Smith est définie sur **bobs@contoso.com**.
3. Bob a également les valeurs pour hello suivantes **proxyAddresses** attribut :
   * smtp:bobs@contoso.com
   * smtp:bob.smith@contoso.com
   * **smtp:bob@contoso.com**
4. Un nouvel utilisateur, **Bob Taylor**, est ajouté toohello sur le site Active Directory.
5. La valeur **UserPrincipalName** de Bob Taylor est définie sur **bobt@contoso.com**.
6. **Bob Taylor** a hello valeurs pour hello suivantes **ProxyAddresses** attribut i. smtp:bobt@contoso.com ii. smtp:bob.taylor@contoso.com
7. L’objet de Bob Taylor est synchronisé avec Azure AD avec succès.
8. Administrateur a décidé de Taylor tooupdate Bob **ProxyAddresses** attribut avec la valeur suivante de hello : i. **smtp:bob@contoso.com**
9. Azure AD va tenter des objets de Taylor tooupdate Bob dans Azure AD avec hello au-dessus de valeur, mais qu’opération échoue en tant que que ProxyAddresses valeur a déjà tooBob Smith, provoquant une erreur de « AttributeValueMustBeUnique ».

#### <a name="how-toofix-attributevaluemustbeunique-error"></a>Comment toofix AttributeValueMustBeUnique erreur
deux objets différents SourceAnchor est Hello raison la plus courante pour hello AttributeValueMustBeUnique erreur \(immutableId\) ont la même valeur pour hello ProxyAddresses et/ou les attributs UserPrincipalName de hello. Dans l’ordre toofix AttributeValueMustBeUnique erreur

1. Identifiez hello dupliqué proxyAddresses, userPrincipalName ou une autre valeur d’attribut qui provoque l’erreur de hello. Également identifier les deux \(ou plus\) objets impliqués dans le conflit de hello. Hello rapport généré par [Azure AD Connect Health pour la synchronisation](https://aka.ms/aadchsyncerrors) peut vous aider à identifier les hello deux objets.
2. Identifier l’objet qui doit continuer à valeur de hello dupliqué toohave et objet qui ne doit pas.
3. Supprimer les valeur hello dupliqué à partir de l’objet hello n’ayant pas cette valeur. Notez que vous devez vous hello modifier dans le répertoire hello où l’objet de hello en provenance de. Dans certains cas, vous devrez peut-être toodelete un des objets hello en conflit.
4. Si vous avez apporté hello modifier Bonjour sur AD local, permettent de hello de synchronisation Azure AD Connect modifier pour hello erreur tooget est fixée.

#### <a name="related-articles"></a>Articles connexes
-[Les attributs en double ou non valides empêchent la synchronisation d’annuaires dans Office 365](https://support.microsoft.com/en-us/kb/2647098)

## <a name="data-validation-failures"></a>Échecs de validation de données
### <a name="identitydatavalidationfailed"></a>IdentityDataValidationFailed
#### <a name="description"></a>Description
Azure Active Directory applique des restrictions différentes sur des données avant d’autoriser ce toobe données écrite dans le répertoire de hello hello lui-même. Il s’agit de tooensure utilisateurs finaux obtiennent les expériences de possibles meilleures hello lors de l’utilisation des applications de hello qui dépendent de ces données.

#### <a name="scenarios"></a>Scénarios
a. valeur de l’attribut UserPrincipalName de Hello comporte des caractères de non valide/non pris en charge.
b. attribut UserPrincipalName de Hello ne suit pas le format requis de hello.

#### <a name="how-toofix-identitydatavalidationfailed-error"></a>Comment toofix IdentityDataValidationFailed erreur
a. Vérifiez le qu'attribut userPrincipalName hello a pris en charge les caractères et le format requis.

#### <a name="related-articles"></a>Articles connexes
* [Préparer les utilisateurs tooprovision via tooOffice de synchronisation d’annuaire 365](https://support.office.com/en-us/article/Prepare-to-provision-users-through-directory-synchronization-to-Office-365-01920974-9e6f-4331-a370-13aea4e82b3e)

### <a name="federateddomainchangeerror"></a>FederatedDomainChangeError
#### <a name="description"></a>Description
Il s’agit d’une casse spécifique qui entraîne un **« FederatedDomainChangeError »** erreur de synchronisation lorsque suffixe hello UserPrincipalName d’un utilisateur est modifié à partir d’un domaine fédéré tooanother de domaine fédéré.

#### <a name="scenarios"></a>Scénarios
Pour un utilisateur synchronisé, suffixe de UserPrincipalName hello a été modifiée à partir d’un domaine fédéré domaine fédéré tooanother localement. Par exemple, *UserPrincipalName = bob@contoso.com*  a été modifié trop*UserPrincipalName = bob@fabrikam.com* .

#### <a name="example"></a>Exemple
1. Bob Smith, un compte pour Contoso.com, est ajouté en tant qu’un nouvel utilisateur dans Active Directory avec hello UserPrincipalNamebob@contoso.com
2. Bob déplace division différente de tooa contoso.com appelé Fabrikam.com et son UserPrincipalName est modifiée.toobob@fabrikam.com
3. Les domaines contoso.com et fabrikam.com sont des domaines fédérés avec Azure Active Directory.
4. L’attribut UserPrincipalName n’est pas mis à jour et cause une erreur de synchronisation « FederatedDomainChangeError ».

#### <a name="how-toofix"></a>Comment toofix
Si le suffixe de UserPrincipalName d’un utilisateur a été mis à jour de Jean @**contoso.com** toobob @**fabrikam.com**, où les deux **contoso.com** et **fabrikam.com** sont **domaines fédérés**, puis suivez ces erreurs de synchronisation étapes toofix hello

1. Mettre à jour de UserPrincipalName l’utilisateur hello dans Azure AD à partir de bob@contoso.com toobob@contoso.onmicrosoft.com. Vous pouvez utiliser hello commande PowerShell avec hello Module Azure AD PowerShell suivante :`Set-MsolUserPrincipalName -UserPrincipalName bob@contoso.com -NewUserPrincipalName bob@contoso.onmicrosoft.com`
2. Autoriser la synchronisation de tooattempt hello prochaine synchronisation cycle. Cette synchronisation date / heure sera établie, et il met à jour hello UserPrincipalName de Bob toobob@fabrikam.com comme prévu.

#### <a name="related-articles"></a>Articles connexes
* [Les modifications ne sont pas synchronisées par l’outil de synchronisation Azure Active Directory hello après avoir modifié hello UPN d’un toouse de compte d’utilisateur un autre domaine fédéré](https://support.microsoft.com/en-us/help/2669550/changes-aren-t-synced-by-the-azure-active-directory-sync-tool-after-you-change-the-upn-of-a-user-account-to-use-a-different-federated-domain)

## <a name="largeobject"></a>LargeObject
### <a name="description"></a>Description
Lorsqu’un attribut dépasse hello autorisé limite de taille, limite de longueur ou limite du nombre défini par le schéma Active Directory de Azure, opération de synchronisation hello entraîne hello **LargeObject** ou **ExceededAllowedLength** erreur de synchronisation. Cette erreur se produit généralement pour hello suivant des attributs

* userCertificate
* userSMIMECertificate
* thumbnailPhoto
* proxyAddresses

### <a name="possible-scenarios"></a>Scénarios possibles
1. Attribut userCertificate de Bob est le stockage de trop de certificats assignés tooBob. Ceux-ci peuvent inclure des certificats plus anciens, expirés. limite Hello est 15 certificats. Pour plus d’informations sur comment toohandle LargeObject erreurs userCertificate d’attribut, veuillez consultez tooarticle [des erreurs de LargeObject de traitement provoquées par attribut userCertificate](active-directory-aadconnectsync-largeobjecterror-usercertificate.md).
2. Attribut de Bob userSMIMECertificate stocke trop de certificats assignés tooBob. Ceux-ci peuvent inclure des certificats plus anciens, expirés. limite Hello est 15 certificats.
3. ThumbnailPhoto Bob définie dans Active Directory est trop grande toobe synchronisé dans Azure AD.
4. Pendant le remplissage automatique de l’attribut ProxyAddresses de hello dans Active Directory, un objet a trop de ProxyAddresses attribués.

### <a name="how-toofix"></a>Comment toofix
1. Vérifiez cet attribut hello provoque l’erreur de hello est réglée hello autorisé de limitation.

## <a name="related-links"></a>Liens connexes
* [Recherche d’objets Active Directory dans le centre d’administration Active Directory](https://technet.microsoft.com/library/dd560661.aspx)
* [Comment tooquery Azure Active Directory pour un objet à l’aide d’Azure Active Directory PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx)
