---
title: "aaaResolve des problèmes de licence pour un groupe dans Azure Active Directory | Documents Microsoft"
description: "Comment tooidentify et résolution de licence des problèmes d’assignation lorsque vous utilisez Azure Active Directory basé sur le groupe de licence"
services: active-directory
keywords: Gestion des licences Azure AD
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ec9c74214a9e246f21fcf767b0bbd586ae702445
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="identify-and-resolve-license-assignment-problems-for-a-group-in-azure-active-directory"></a>Identification et résolution des problèmes d’affectation de licences pour un groupe dans Azure Active Directory

Basé sur le groupe de licences dans Azure Active Directory (Azure AD) d’introduit le concept de hello d’utilisateurs dans un état d’erreur licence. Dans cet article, nous expliquons raisons hello pour lesquelles les utilisateurs peuvent finir dans cet état.

Lorsque vous affectez des licences directement tooindividual les utilisateurs, sans l’aide basée sur le groupe de licences, l’opération d’assignation hello peut échouer. Par exemple, lorsque vous exécutez l’applet de commande PowerShell hello `Set-MsolUserLicense` sur un utilisateur, applet de commande hello peut échouer pour plusieurs raisons qui sont associées toobusiness logique. Par exemple, il peut y avoir un nombre insuffisant de licences ou d’un conflit entre deux plans de service qui ne peut pas être attribué au hello même temps. Hello problème est immédiatement signalée sauvegarder tooyou.

Lorsque vous utilisez basée sur le groupe de licences, hello mêmes erreurs peuvent se produire, mais ils se produisent en arrière-plan de hello lorsque hello service Azure AD est attribuer des licences. Pour cette raison, les erreurs de hello ne peut pas être communiquée tooyou immédiatement. Au lieu de cela, elles sont enregistrées sur l’objet utilisateur de hello et puis signalées via le portail d’administration de hello. Notez que hello toolicense intention hello utilisateur n’est jamais perdu, mais il est enregistré dans un état d’erreur pour un examen futures et la résolution.

## <a name="how-toofind-license-assignment-errors"></a>Comment toofind erreurs d’affectation de licence

1. utilisateurs toofind dans un état d’erreur dans un groupe spécifique, un panneau hello ouverte pour le groupe de hello. Sous **Licences**, une notification s’affiche si des utilisateurs se trouvent à l’état d’erreur.

![Groupe, notification d’erreur](media/active-directory-licensing-group-problem-resolution-azure-portal/group-error-notification.png)

2. Cliquez sur hello notification tooopen une liste de tous les utilisateurs concernés. Vous pouvez cliquer sur individuellement sur chaque utilisateur toosee plus en détail.

![Groupe, liste des utilisateurs en état d’erreur](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-users-with-errors.png)

3. toofind tous les groupes qui contiennent au moins une erreur sur hello **Azure Active Directory** panneau sélectionner **licences** , puis **vue d’ensemble**. Une fenêtre d’information s’affiche lorsque des groupes nécessitent votre attention.

![Vue d’ensemble, informations sur les groupes en état d’erreur](media/active-directory-licensing-group-problem-resolution-azure-portal/group-errors-widget.png)

4. Cliquez sur hello boîte toosee une liste de tous les groupes avec des erreurs. Vous pouvez cliquer sur chaque groupe pour plus de détails.

![Vue d’ensemble, liste des groupes contenant des erreurs](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-groups-with-errors.png)


Voici une description de chaque tooresolve potentielle de façon problème et hello il.

## <a name="not-enough-licenses"></a>Nombre insuffisant de licences

**Problème :** ne contient pas de suffisamment de licences disponibles pour un des produits hello qui est spécifié dans le groupe de hello. Vous devez tooeither acheter davantage de licences pour le produit de hello ou libérer des licences inutilisées à partir d’autres utilisateurs ou groupes.

toosee le nombre de licences est disponible, accédez trop**Azure Active Directory** > **licences** > **tous les produits**.

toosee consomme les utilisateurs et les groupes de licences, cliquez sur un produit. Sous **Utilisateurs sous licence**, vous pouvez voir tous les utilisateurs auxquels des licences ont été affectées directement ou par le biais d’un ou de plusieurs groupes. Sous **Groupes sous licence**, vous pouvez voir tous les groupes auxquels ce produit est attribué.

**PowerShell :** les applets de commande PowerShell signalent cette erreur en tant que _CountViolation_.

## <a name="conflicting-service-plans"></a>Plans de service en conflit

**Problème :** un des produits hello qui est spécifié dans le groupe de hello contient un plan de service qui est en conflit avec un autre plan de service qui est déjà attribué toohello utilisateur via un autre produit. Certains plans de service sont configurés de sorte qu’ils ne peuvent pas être assignés toohello même utilisateur que celui d’un autre plan de service connexes.

Envisagez de hello l’exemple suivant. Un utilisateur possède une licence pour Office 365 Enterprise **E1** affectée directement, avec tous les plans de hello activées. groupe tooa a hello Office 365 Enterprise a été ajouté à utilisateur de Hello **E3** tooit du produit associé. Ce produit contient des plans de service ne peut pas se chevaucher avec les plans hello inclus dans E1, afin de l’attribution de licence de groupe hello échouera avec hello erreur de « Plans de service en conflit ». Dans cet exemple, les plans de service hello en conflit sont :

-   SharePoint Online (Plan 2) est en conflit avec SharePoint Online (Plan 1).
-   Exchange Online (Plan 2) est en conflit avec Exchange Online (Plan 1).

toosolve ce conflit, vous devez toodisable ces deux plans sur hello E1 de licence qui toohello directement attribué utilisateur. Ou bien, vous avez besoin d’attribution de licence de tout groupe toomodify hello et désactivez les plans hello dans la licence de E3 hello. Ou bien, vous pouvez décider de licence de E1 hello tooremove à partir de l’utilisateur de hello si elle est redondante dans le contexte de hello de licence de E3 hello.

la décision de Hello sur comment licences toujours des produits en conflit de tooresolve appartient toohello administrateur. Azure AD ne résout pas automatiquement les conflits de licences.

**PowerShell :** les applets de commande PowerShell signalent cette erreur en tant que _MutuallyExclusiveViolation_.

## <a name="other-products-depend-on-this-license"></a>D’autres produits dépendent de cette licence

**Problème :** un des produits hello qui est spécifié dans le groupe de hello contient un plan de service qui doit être activé pour un autre plan de service, dans un autre produit, de la fonction. Cette erreur se produit lorsque le plan de service sous-jacent tooremove hello tente d’Azure AD. Par exemple, cela peut se produire en raison de l’utilisateur hello en cours de suppression du groupe de hello.

toosolve ce problème, vous devez toomake que ce plan requis hello est toujours affecté toousers via une autre méthode, ou que les services dépendants hello sont désactivées pour les utilisateurs. Après cela, vous pouvez correctement supprimer la licence de groupe hello à partir de ces utilisateurs.

**PowerShell :** les applets de commande PowerShell signalent cette erreur en tant que _DependencyViolation_.

## <a name="usage-location-isnt-allowed"></a>L’emplacement d’utilisation n’est pas autorisé

**Problème :** certains services Microsoft ne sont pas disponibles partout en raison de lois et réglementations locales. Avant de pouvoir affecter un utilisateur tooa de licence, vous disposez de propriété de « Emplacement d’utilisation » hello toospecify pour l’utilisateur de hello. Cela sous hello **utilisateur** > **profil** > **paramètres** section Bonjour portail Azure.

Quand Azure AD tente tooassign un utilisateur tooa de licence de groupe dont l’emplacement d’utilisation n’est pas pris en charge, il échouera et enregistrer cette erreur sur l’utilisateur de hello.

toosolve ce problème, supprimer des utilisateurs à partir d’emplacements non pris en charge à partir du groupe de hello concédé sous licence. Ou bien, si les valeurs d’emplacement hello en cours d’utilisation ne pas représenter l’emplacement de l’utilisateur réel hello, vous pouvez les modifier afin que les licences hello soient affectées prochaine (si le nouvel emplacement de hello est pris en charge).

**PowerShell :** les applets de commande PowerShell signalent cette erreur en tant que _ProhibitedInUsageLocationViolation_.

> [!NOTE]
> Lorsque Azure AD affecte des licences d’un groupe, tous les utilisateurs sans un emplacement d’utilisation spécifié héritent emplacement hello du répertoire de hello. Nous vous recommandons que les administrateurs d’utilisation correcte de hello valeurs d’emplacement sur les utilisateurs avant d’utiliser basée sur le groupe de licences toocomply avec les lois et réglementations locales.

## <a name="what-happens-when-theres-more-than-one-product-license-on-a-group"></a>Que se passe-t-il lorsqu’un groupe est concerné par plusieurs licences produit ?

Vous pouvez affecter plusieurs groupes de tooa de licence de produit. Par exemple, vous pouvez affecter à Office 365 entreprise E3 et Enterprise Mobility + Security tooa groupe tooeasily Active inclus tous les services pour les utilisateurs.

Azure AD tentatives tooassign toutes les licences qui sont spécifiés dans hello groupe tooeach utilisateur. Si Azure AD ne peut pas affecter un des produits de hello en raison de problèmes de logique métier (par exemple, si vous ne contient pas de suffisamment de licences pour tous les, ou s’il existe des conflits avec d’autres services qui sont activés sur l’utilisateur de hello), il ne sera pas affecter hello autres licences dans le groupe de hello soit.

Vous serez hello toosee en mesure des utilisateurs qui a échoué tooget affecté a échoué et vérification les produits qui ont été affectés.

## <a name="license-assignment-fails-silently-for-a-user-due-tooduplicate-proxy-addresses-in-exchange-online"></a>Attribution de licence échoue sans avertissement pour un utilisateur en raison des adresses de proxy tooduplicate dans Exchange Online

Si vous utilisez Exchange Online, certains utilisateurs de votre client peuvent être mal configurés avec hello même valeur d’adresse de proxy. Quand basée sur le groupe de licences tente de tooassign un toosuch de licence utilisateur, il échouera et enregistrera pas une erreur (contrairement à dans hello autres cas d’erreur décrites ci-dessus) - il s’agit d’une limitation dans la version d’évaluation hello de cette fonctionnalité et nous allons tooaddress avant  *Disponibilité générale*.

> [!TIP]
> Si vous remarquez que certains utilisateurs n’ont pas reçu de licence et qu’aucune erreur n’est enregistrée les concernant, vérifiez tout d’abord s’ils ont une adresse proxy en double.
> Pour ce faire, vous pouvez exécuter hello suivant l’applet de commande PowerShell par rapport à Exchange Online :
```
Run Get-Recipient | where {$_.EmailAddresses -match "user@contoso.onmicrosoft.com"} | fL Name, RecipientType,emailaddresses
```
> [Cet article](https://support.microsoft.com/help/3042584/-proxy-address-address-is-already-being-used-error-message-in-exchange-online) contient plus de détails sur ce problème, y compris des informations sur [comment tooExchange tooconnect en ligne à l’aide de PowerShell à distance](https://technet.microsoft.com/library/jj984289.aspx).

Après que proxy résoudre des problèmes ont été résolus pour les utilisateurs de hello affectée, assurez-vous que licence tooforce de traitement sur hello toomake de groupe que les licences peuvent maintenant être appliquées à nouveau.

## <a name="how-do-you-force-license-processing-in-a-group-tooresolve-errors"></a>Comment forcer la licence dans un tooresolve regrouper des erreurs de traitement ?

Selon les étapes que vous avez pris les erreurs tooresolve, il peut être nécessaire de toomanually déclencher le traitement de l’état utilisateur groupe tooupdate hello.

Par exemple, si vous libéré certaines licences en supprimant les affectations de licence directe des utilisateurs, vous devez le traitement de tootrigger de groupes qui ont échoué précédemment toofully licence tous les membres de l’utilisateur. toodo qui, trouver le panneau de groupe hello, ouvrez **licences**et sélectionnez hello **retraiter** bouton dans la barre d’outils hello.

## <a name="next-steps"></a>Étapes suivantes

toolearn en savoir plus sur les autres scénarios de gestion des licences via des groupes, voir hello :

* [Affectation d’un groupe de tooa de licences dans Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [What is group-based licensing in Azure Active Directory? (Présentation des licences basées sur le groupe dans Azure Active Directory)](active-directory-licensing-whatis-azure-portal.md)
* [Comment toomigrate individuels titulaires d’une licence dans Azure Active Directory en fonction des toogroup](active-directory-licensing-group-migration-azure-portal.md)
* [Azure Active Directory group-based licensing additional scenarios (Autres scénarios de licence basée sur le groupe Azure Active Directory)](active-directory-licensing-group-advanced.md)
