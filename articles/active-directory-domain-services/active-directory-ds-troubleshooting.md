---
title: "Services de domaine Azure Active Directory : guide de dépannage | Microsoft Docs"
description: "Guide de dépannage pour les services de domaine Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 4bc8c604-f57c-4f28-9dac-8b9164a0cf0b
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 86eb3513b7bc921c59287600b1b76eeda20c1356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services---troubleshooting-guide"></a>Services de domaine Azure AD : guide de dépannage
Cet article fournit des conseils de dépannage pour les problèmes que vous pouvez rencontrer pendant la configuration ou l’administration des services de domaine Azure Active Directory (AD).

## <a name="you-cannot-enable-azure-ad-domain-services-for-your-azure-ad-directory"></a>Vous ne pouvez pas activer les services de domaine Azure AD pour votre annuaire Azure AD
Cette section vous explique vous résoudre les erreurs lorsque vous essayez de tooenable des Services de domaine Active Directory de Azure pour votre annuaire et il échoue ou devient activé ou désactivé too'Disabled arrière ».

Choisissez hello étapes qui correspondent le message d’erreur toohello que vous rencontrez de dépannage.

| **Message d’erreur** | **Résolution :** |
| --- |:--- |
| *Hello nom contoso100.com est déjà en cours d’utilisation sur ce réseau. Spécifiez un nom qui n’est pas utilisé.* |[Conflit de nom de domaine dans le réseau virtuel de hello](active-directory-ds-troubleshooting.md#domain-name-conflict) |
| *Services de domaine n’a pas pu être activées dans ce locataire Azure AD. service de Hello n’a pas les autorisations adéquates toohello d’application appelé « Sync Services de domaine Active Directory de Azure ». Supprimer l’application hello appelée « Sync Services de domaine Active Directory de Azure », puis recommencez tooenable les Services de domaine pour votre locataire Azure AD.* |[Services de domaine n’a pas d’application de synchronisation des Services de domaine Active Directory de Azure toohello les autorisations adéquates](active-directory-ds-troubleshooting.md#inadequate-permissions) |
| *Services de domaine n’a pas pu être activées dans ce locataire Azure AD. Hello application dans votre locataire Azure AD ne pas avoir hello des Services de domaine requis autorisations tooenable Services de domaine. Supprimer l’application hello avec d87dcbc6-a371-462e-88e3-28ad15ec4e64 d’identificateur hello application, puis recommencez tooenable des Services de domaine pour votre locataire Azure AD.* |[Hello application des Services de domaine n’est pas configuré correctement dans votre client](active-directory-ds-troubleshooting.md#invalid-configuration) |
| *Services de domaine n’a pas pu être activées dans ce locataire Azure AD. Hello application Microsoft Azure AD est désactivée dans votre locataire Azure AD. Activer l’application hello avec 00000002-0000-0000-c000-000000000000 d’identificateur hello application, puis recommencez tooenable des Services de domaine pour votre locataire Azure AD.* |[Hello application Microsoft Graph est désactivé dans votre locataire Azure AD](active-directory-ds-troubleshooting.md#microsoft-graph-disabled) |

### <a name="domain-name-conflict"></a>Conflit de nom de domaine
**Message d’erreur :**

*Hello nom contoso100.com est déjà en cours d’utilisation sur ce réseau. Spécifiez un nom qui n’est pas utilisé.*

**Correction :**

Vérifiez que vous n’avez pas un domaine existant avec hello même nom de domaine disponible sur ce réseau virtuel. Par exemple, supposons que vous avez un domaine appelé « contoso.com » déjà disponible sur le réseau virtuel sélectionné de hello. Une version ultérieure, vous essayez de tooenable un domaine géré des Services de domaine Active Directory de Azure avec hello même nom de domaine (autrement dit, « contoso.com ») sur ce réseau virtuel. Une défaillance se produit lors de la tentative de Services de domaine tooenable Azure AD.

Cet échec est dû tooname des conflits de nom de domaine hello sur ce réseau virtuel. Dans ce cas, vous devez utiliser un nom différent de tooset votre domaine géré des Services de domaine Active Directory de Azure. Ou bien, vous pouvez annuler la configuration domaine hello et puis continuer les Services de domaine tooenable Azure AD.

### <a name="inadequate-permissions"></a>Autorisations inappropriées
**Message d’erreur :**

*Services de domaine n’a pas pu être activées dans ce locataire Azure AD. service de Hello n’a pas les autorisations adéquates toohello d’application appelé « Sync Services de domaine Active Directory de Azure ». Supprimer l’application hello appelée « Sync Services de domaine Active Directory de Azure », puis recommencez tooenable les Services de domaine pour votre locataire Azure AD.*

**Correction :**

Vérifiez toosee s’il existe une application portant le nom hello « Sync Services de domaine Active Directory de Azure » dans votre annuaire Azure AD. Si cette application existe, supprimez-la, puis réactivez les services de domaine Azure AD.

Effectuer hello suivant toocheck étapes présence hello de l’application hello et toodelete, si l’application hello existe :

1. Accédez toohello **portail Azure classic** ([https://manage.windowsazure.com](https://manage.windowsazure.com)).
2. Sélectionnez hello **Active Directory** nœud dans le volet gauche de hello.
3. Client de hello sélectionnez Azure Active Directory (répertoire) pour laquelle vous aimeriez tooenable de Services de domaine Azure AD.
4. Accédez toohello **Applications** onglet.
5. Sélectionnez hello **Applications que ma société possède** option dans la liste déroulante de hello.
6. Recherchez l’application **Synchronisation des services de domaine Azure AD**. Si l’application hello existe, passez toodelete il.
7. Une fois que vous avez supprimé l’application hello, réessayez les Services de domaine Azure AD de tooenable qu’une seule fois.

### <a name="invalid-configuration"></a>Configuration non valide
**Message d’erreur :**

*Services de domaine n’a pas pu être activées dans ce locataire Azure AD. Hello application dans votre locataire Azure AD ne pas avoir hello des Services de domaine requis autorisations tooenable Services de domaine. Supprimer l’application hello avec d87dcbc6-a371-462e-88e3-28ad15ec4e64 d’identificateur hello application, puis recommencez tooenable des Services de domaine pour votre locataire Azure AD.*

**Correction :**

Vérifiez toosee si vous avez une application portant le nom hello 'AzureActiveDirectoryDomainControllerServices' (avec un identificateur d’application de d87dcbc6-a371-462e-88e3-28ad15ec4e64) dans votre annuaire Azure AD. Si cette application existe, vous devez toodelete il et les Services de domaine Active Directory Azure réactiver puis.

Utilisez hello après application de PowerShell script toofind hello et supprimez-le.

> [!NOTE]
> Ce script utilise les applets de commande **Azure AD PowerShell version 2**. Pour obtenir une liste complète de toutes les applets de commande disponibles et module de hello toodownload, lecture hello [documentation de référence AzureAD PowerShell](https://msdn.microsoft.com/library/azure/mt757189.aspx).
>
>

```
$InformationPreference = "Continue"
$WarningPreference = "Continue"

$aadDsSp = Get-AzureADServicePrincipal -Filter "AppId eq 'd87dcbc6-a371-462e-88e3-28ad15ec4e64'" -ErrorAction Ignore
if ($aadDsSp -ne $null)
{
    Write-Information "Found Azure AD Domain Services application. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $aadDsSp.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services application."
}

$identifierUri = "https://sync.aaddc.activedirectory.windowsazure.com"
$appFilter = "IdentifierUris eq '" + $identifierUri + "'"
$app = Get-AzureADApplication -Filter $appFilter
if ($app -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync application. Deleting it ..."
    Remove-AzureADApplication -ObjectId $app.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services Sync application."
}

$spFilter = "ServicePrincipalNames eq '" + $identifierUri + "'"
$sp = Get-AzureADServicePrincipal -Filter $spFilter
if ($sp -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync service principal. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $sp.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services Sync service principal."
}
```
<br>

### <a name="microsoft-graph-disabled"></a>Microsoft Graph désactivé
**Message d’erreur :**

Les services de domaine n’ont pas pu être activés pour ce client Azure AD. Hello application Microsoft Azure AD est désactivée dans votre locataire Azure AD. Activer l’application hello avec 00000002-0000-0000-c000-000000000000 d’identificateur hello application, puis recommencez tooenable des Services de domaine pour votre locataire Azure AD.

**Correction :**

Vérifiez toosee si vous avez désactivé une application avec l’identificateur hello 00000002-0000-0000-c000-type "000000000000". Cette application est l’application de Microsoft Azure AD hello et fournit l’API Graph accès tooyour Azure AD client. Les Services de domaine Active Directory Azure a besoin de cette toosynchronize de toobe activée application gérée par votre tooyour de locataire Azure AD domaine.

tooresolve cette erreur, activer cette application et recommencez tooenable les Services de domaine pour votre locataire Azure AD.

## <a name="users-are-unable-toosign-in-toohello-azure-ad-domain-services-managed-domain"></a>Les utilisateurs sont toosign impossible dans toohello domaine géré des Services de domaine Active Directory de Azure
Si un ou plusieurs utilisateurs dans votre locataire Azure AD sont toosign impossible dans le domaine géré de toohello nouvellement créé, effectuez hello suivant les étapes de dépannage :

* **Connectez-vous à l’aide du format UPN :** essayez toosign à l’aide du format UPN de hello (par exemple, «joeuser@contoso.com») au lieu du format de SAMAccountName hello ('CONTOSO\joeuser'). Hello SAMAccountName peut être généré automatiquement pour les utilisateurs dont le préfixe UPN est trop long ou qu’il est même hello en tant qu’un autre utilisateur sur un domaine géré de hello. format de nom UPN Hello est garantie toobe unique au sein d’un locataire Azure AD.

> [!NOTE]
> Nous recommandons d’utiliser hello UPN format toosign dans le domaine géré de toohello des Services de domaine Active Directory de Azure.
>
>

* Assurez-vous d’avoir [activé la synchronisation de mot de passe](active-directory-ds-getting-started-password-sync.md) conformément aux étapes hello décrites dans le guide de prise en main de hello.
* **Comptes externes :** Vérifiez que compte d’utilisateur hello affecté n’est pas un compte externe dans le locataire de hello Azure AD. Les exemples de comptes externes incluent les comptes Microsoft (par exemple, « joe@live.com ») ou les comptes d’utilisateurs d’un annuaire Azure AD externe. Étant donné que les Services de domaine Active Directory de Azure n’a pas d’informations d’identification pour ces comptes d’utilisateur, ces utilisateurs ne peut pas se connecter dans le domaine géré de toohello.
* **Synchronisation des comptes :** si les comptes d’utilisateur hello affecté sont synchronisés à partir d’un répertoire local, vérifiez que :

  * Vous avez déployé ou mis à jour toohello [plus tard recommandé version d’Azure AD Connect](https://www.microsoft.com/en-us/download/details.aspx?id=47594).
  * Vous avez configuré trop Azure AD Connect[effectuer une synchronisation complète](active-directory-ds-getting-started-password-sync.md).
  * Selon la taille de hello de votre annuaire, il peut prendre un certain temps pour les comptes d’utilisateur et des informations d’identification toobe hachages disponibles dans les Services de domaine Active Directory de Azure. Vérifiez que vous attendez suffisamment longtemps avant une nouvelle tentative d’authentification (selon la taille de hello de votre annuaire - quelques heures tooa ou deux jours pour les répertoires volumineux).
  * Si le problème de hello persiste après avoir vérifié les étapes précédentes de hello, essayez de le redémarrer hello Service Microsoft Azure AD Sync. À partir de votre ordinateur de synchronisation, lancez une invite de commandes et exécutez les hello suivant de commandes :

    1. net stop 'Microsoft Azure AD Sync'
    2. net start 'Microsoft Azure AD Sync'
* **Comptes cloud uniquement**: si le compte d’utilisateur hello affecté est un compte d’utilisateur uniquement dans le cloud, assurez-vous que l’utilisateur hello a changé son mot de passe une fois que vous avez activé les Services de domaine Active Directory de Azure. Cette étape permet d’informations d’identification hello hachages requis pour toobe des Services de domaine Active Directory Azure généré.

## <a name="users-removed-from-your-azure-ad-tenant-are-not-removed-from-your-managed-domain"></a>Les utilisateurs supprimés de votre client Azure AD ne sont pas supprimés de votre domaine géré
Azure AD vous protège contre la suppression accidentelle d’objets utilisateur. Lorsque vous supprimez un compte d’utilisateur à partir de votre client Azure AD, objet utilisateur correspondant de hello est déplacé toohello la Corbeille. Lorsque cette opération de suppression est un domaine géré de tooyour synchronisé, elle force hello correspondant toobe de compte d’utilisateur marqué comme désactivé. Cette fonctionnalité vous permet de récupérer ou restaurer le compte d’utilisateur hello plus tard.

Bonjour de compte d’utilisateur reste Bonjour désactivé état dans votre domaine géré, même si vous recréer un compte d’utilisateur avec hello même UPN dans votre annuaire Azure AD. compte d’utilisateur tooremove hello à partir de votre domaine géré, vous devez tooforce supprimer de votre client Azure AD.

compte d’utilisateur tooremove hello entièrement à partir de votre domaine géré, définitivement utilisateur de hello à partir de votre client Azure AD. Utilisez l’applet de commande Remove-MsolUser PowerShell hello avec hello '-RemoveFromRecycleBin' option, comme décrit dans cette [article MSDN](https://msdn.microsoft.com/library/azure/dn194132.aspx).

## <a name="contact-us"></a>Nous contacter
Contacter l’équipe de produit de Azure des Services de domaine Active Directory de hello trop[faire part de commentaires ou pour la prise en charge](active-directory-ds-contact-us.md).
