---
title: "résilience d’attribut de synchronisation et doublon aaaIdentity | Documents Microsoft"
description: "Nouveau comportement de comment les objets présentant des conflits de nom UPN ou ProxyAddress toohandle pendant la synchronisation d’annuaires à l’aide d’Azure AD Connect."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 537a92b7-7a84-4c89-88b0-9bce0eacd931
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.openlocfilehash: e27dcbf9d71f83fa9566cae2fd99350297d1cd9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="identity-synchronization-and-duplicate-attribute-resiliency"></a>Synchronisation des identités et résilience d’attribut en double
La résilience d’attribut en double est une fonctionnalité d’Azure Active Directory qui élimine les problèmes liés aux conflits entre **UserPrincipalName** et **ProxyAddress** lors de l’exécution de l’un des outils de synchronisation de Microsoft.

Ces deux attributs sont généralement requis toobe unique dans toutes les **utilisateur**, **groupe**, ou **Contact** objets dans un locataire Azure Active Directory donné.

> [!NOTE]
> Seuls les Utilisateurs peuvent avoir des noms UPN.
> 
> 

Hello nouveau comportement permettant à cette fonctionnalité est en partie du cloud hello du pipeline de synchronisation hello, par conséquent, il est client agnostique et pertinente pour les produits de synchronisation de Microsoft, y compris le connecteur Azure AD Connect, DirSync et MIM. terme générique de Hello « client de synchronisation » est utilisé dans cette toorepresent document l’un de ces produits.

## <a name="current-behavior"></a>Comportement actuel
S’il existe une tooprovision tentative d’un nouvel objet avec une valeur UPN ou ProxyAddress qui viole cette contrainte d’unicité, Azure Active Directory se bloque en cours de création de cet objet. De même, si un objet est mis à jour avec un non uniques UPN ou ProxyAddress, mise à jour hello échoue. Hello mise à jour ou la tentative de configuration est une nouvelle tentative par le client de synchronisation hello lors de chaque cycle d’exportation et continue toofail jusqu'à ce que hello conflit est résolu. Un e-mail de rapport d’erreur est généré lors de chaque tentative et une erreur est enregistrée par le client de synchronisation hello.

## <a name="behavior-with-duplicate-attribute-resiliency"></a>Comportement avec une résilience d’attribut en double
Au lieu de complètement échouent tooprovision ou mettre à jour un objet avec un attribut en double, Azure Active Directory « quarantaine » des attributs en double hello qui violent une contrainte d’unicité hello. Si cet attribut est requis pour la configuration, comme UserPrincipalName, service de hello assigne une valeur de l’espace réservé. le format de ces valeurs temporaires Hello est  
« ***<OriginalPrefix>+<4chiffres>@<InitialTenantDomain>.onmicrosoft.com*** ».  
Si l’attribut de hello n’est pas requis, comme un **ProxyAddress**, Azure Active Directory met en quarantaine d’attribut de conflit hello simplement et se poursuit avec la création d’objet hello ou mise à jour.

Lors de la mise en quarantaine d’attribut de hello, plus d’informations sur les conflits hello sont envoyés dans hello même e-mail de rapport d’erreur utilisé dans l’ancien comportement de hello. Toutefois, cette information apparaît uniquement dans les rapports d’erreurs hello une seule fois, en cas de mise en quarantaine hello, il ne continue pas toobe enregistrés dans les futures des messages électroniques. En outre, étant donné que l’exportation de hello pour cet objet a réussi, client de synchronisation hello n’enregistre pas d’une erreur et ne pas de nouvelle tentative hello créer / mettre à jour l’opération lors de cycles de synchronisation ultérieure.

toosupport que ce comportement, un nouvel attribut a été ajouté les classes d’objets utilisateur, groupe et Contact toohello :  
**DirSyncProvisioningErrors**

Il s’agit d’un attribut à valeurs multiples qui est utilisé toostore hello des attributs en conflit qui violent une contrainte d’unicité hello doivent leur être ajoutés normalement. Une tâche d’arrière-plan du minuteur a été activée dans Azure Active Directory qui s’exécute chaque toolook heure pour les conflits d’attributs en double qui ont été résolus et supprime automatiquement les attributs de hello en question à partir de la mise en quarantaine.

### <a name="enabling-duplicate-attribute-resiliency"></a>Activer la résilience d’attribut en double
Résilience d’attribut en double sera le nouveau comportement par défaut de hello sur tous les locataires Azure Active Directory. Il s’agit sur par défaut pour tous les clients qui a activé la synchronisation pour hello première 22 août 2016 ou version ultérieure. Clients qui a activé la synchronisation précédente toothis date seront hello la fonctionnalité est activée par lots. Ce déploiement commence en septembre 2016, et une notification par courrier électronique recevront un contact notification technique du locataire tooeach avec une date spécifique hello lorsque hello fonctionnalité sera activée.

> [!NOTE]
> Une fois que la résilience des attributs en double a été activée, elle ne peut pas être désactivée.

toocheck si hello est activée pour votre client, vous pouvez le faire en téléchargeant la version la plus récente du module d’Azure Active Directory PowerShell hello hello et exécutant :

`Get-MsolDirSyncFeatures -Feature DuplicateUPNResiliency`

`Get-MsolDirSyncFeatures -Feature DuplicateProxyAddressResiliency`

> [!NOTE]
> Vous pouvez utiliser n’est plus de fonctionnalité de résilience d’attribut en double de Set-MsolDirSyncFeature applet de commande tooproactively activer hello avant qu’il est activé pour votre client. fonctionnalité de hello toobe tootest en mesure, vous devez toocreate un nouveau locataire Azure Active Directory.

## <a name="identifying-objects-with-dirsyncprovisioningerrors"></a>Identification des objets avec DirSyncProvisioningErrors
Il existe actuellement deux méthodes tooidentify les objets qui ont ces erreurs en raison de conflits de propriété tooduplicate, Azure Active Directory PowerShell et hello portail d’administration d’Office 365. Il existe des plans tooextend tooadditional basé sur un portail reporting Bonjour futures.

### <a name="azure-active-directory-powershell"></a>Azure Active Directory PowerShell
Pourquoi les applets de commande PowerShell dans cette rubrique, hello Voici true :

* Tous les hello suivant d’applets de commande respectent la casse.
* Hello **– ErrorCategory PropertyConflict** doit toujours être inclus. Il n’existe actuellement aucun autre type de **ErrorCategory**, mais cela peut être étendue Bonjour futures.

Commencez par exécuter **Connect-MsolService** et entrer les informations d’identification d’un administrateur client.

Ensuite, utilisez hello après des erreurs tooview applets de commande et les opérateurs de différentes façons :

1. [Afficher tout](#see-all)
2. [Par type de propriété](#by-property-type)
3. [Par valeur en conflit](#by-conflicting-value)
4. [À l’aide d’une recherche de chaîne](#using-a-string-search)
5. [Triées](#sorted)
6. [Par quantité limitée ou l’ensemble des erreurs](#in-a-limited-quantity-or-all)

#### <a name="see-all"></a>Afficher tout
Une fois connecté, toosee une liste générale d’attribut de mise en service des erreurs dans le client de hello exécuter :

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict`

Ce code produit un résultat semblable à hello suivante :  
 ![Get-MsolDirSyncProvisioningError](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1.png "Get-MsolDirSyncProvisioningError")  

#### <a name="by-property-type"></a>Par type de propriété
erreurs toosee par type de propriété, ajoutez hello **- PropertyName** indicateur avec hello **UserPrincipalName** ou **ProxyAddresses** argument :

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName UserPrincipalName`

Ou

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName ProxyAddresses`

#### <a name="by-conflicting-value"></a>Par valeur en conflit
erreurs toosee concernant la propriété spécifique de tooa ajouter hello **- PropertyValue** indicateur (**- PropertyName** doit également être utilisé lors de l’ajout de cet indicateur) :

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyValue User@domain.com -PropertyName UserPrincipalName`

#### <a name="using-a-string-search"></a>À l’aide d’une recherche de chaîne
toodo une recherche de chaîne large utiliser hello **- SearchString** indicateur. Cela peut être utilisée indépendamment de toutes les hello au-dessus des indicateurs, à l’exception de hello de **- ErrorCategory PropertyConflict**, qui est toujours requis :

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -SearchString User`

#### <a name="in-a-limited-quantity-or-all"></a>Par quantité limitée ou l’ensemble des erreurs
1. **MaxResults <Int>**  peut être utilisé toolimit hello requête tooa nombre spécifique de valeurs.
2. **Tous les** peut être utilisé tooensure tous les résultats sont récupérés dans les cas de hello où il existe un grand nombre d’erreurs.

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -MaxResults 5`

## <a name="office-365-admin-portal"></a>Portail d’administration Office 365
Vous pouvez afficher les erreurs de synchronisation d’annuaire dans le centre d’administration Office 365 hello. Hello rapport dans affiche portail Office 365 de hello **utilisateur** objets qui ont ces erreurs. Il n’indique pas d’informations sur les conflits entre **Groupes** et **Contacts**.

![Utilisateurs actifs](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1234.png "Utilisateurs actifs")

Pour savoir comment les erreurs de synchronisation d’annuaire tooview hello Office 365 administration center, consultez [identifier les erreurs de synchronisation d’annuaires dans Office 365](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067).

### <a name="identity-synchronization-error-report"></a>Rapport d’erreur de synchronisation d’identité
Lors du traitement d’un objet avec un conflit d’attribut en double avec ce nouveau comportement, dans qu'une notification est incluse standard hello rapport d’erreurs de synchronisation d’identité de la messagerie électronique est envoyé de contact de Notification technique toohello pour le client de hello. Toutefois, ce comportement présente un changement majeur. Bonjour passées, informations de conflit d’attribut en double sont incluses dans chaque rapport d’erreurs suivantes jusqu'à ce que hello conflit a été résolu. Avec ce nouveau comportement, notification d’erreur hello pour qu’un conflit donné uniquement semble-t-il - une fois au moment de hello attribut en conflit de hello est mis en quarantaine.

Voici un exemple de quel type hello par courrier électronique de notification à quoi ressemble un conflit d’adresse proxy :  
    ![Utilisateurs actifs](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "Utilisateurs actifs")  

## <a name="resolving-conflicts"></a>Résolution des conflits
Résolution des problèmes de stratégies de stratégie et la résolution de ces erreurs ne doivent pas différer de manière hello erreurs d’attribut en double ont été traitées dans hello passée. Hello seule différence est que les balayages de tâche du minuteur hello via locataire hello sur hello côté service tooautomatically Ajouter attribut de hello dans l’objet approprié de question toohello une fois hello conflit est résolu.

Hello ci-dessous décrit les différentes stratégies de dépannage et la résolution : [en double ou des attributs non valides empêchent la synchronisation d’annuaire dans Office 365](https://support.microsoft.com/kb/2647098).

## <a name="known-issues"></a>Problèmes connus
Aucun de ces problèmes connus n’entraîne une dégradation du service ou une perte des données. Plusieurs d'entre eux sont esthétiques, d’autres provoquent standard «*résilience préliminaire*« certaines erreurs toorequire manuel supplémentaire correctives provoque l’attribut en double erreurs toobe est levée au lieu de l’attribut de conflit hello et l’autre les mettre en quarantaine.

**Comportement de base :**

1. Les objets avec des configurations d’attribut spécifique continuent erreurs d’exportation tooreceive comme toohello exécutée en double ou les attributs mis en quarantaine.  
   Par exemple :
   
    a. Le nouvel utilisateur est créé dans AD avec les attributs UPN **Joe@contoso.com** et ProxyAddress **smtp:Joe@contoso.com**
   
    b. Hello propriétés de cet objet sont en conflit avec un groupe existant, où ProxyAddress est  **SMTP:Joe@contoso.com** .
   
    c. Lors de l’exportation, un **ProxyAddress conflit** erreur est levée au lieu d’avoir les attributs de conflit hello mis en quarantaine. Hello opération est tentée à nouveau lors de chaque cycle de synchronisation ultérieures, comme elle l’aurait été avant l’activation de la fonctionnalité de résilience hello.
2. Si les deux groupes sont créés localement avec hello même adresse SMTP, tooprovision échoue une première tentative de hello standard en double **ProxyAddress** erreur. Toutefois, les valeur dupliquée hello sont correctement mis en quarantaine sur hello prochain cycle de synchronisation.

**Rapport du portail Office**:

1. message d’erreur détaillé Hello pour deux objets dans un jeu de conflit de nom UPN est le même hello. Cela indique que l’UPN des deux objets a changé/été mis en quarantaine, alors que seules les données de l’un d’entre eux ont changé.
2. message d’erreur détaillé Hello pour qu’un conflit de nom UPN montre hello mauvais nom d’affichage d’un utilisateur qui a été leur UPN modifié/mis en quarantaine. Par exemple :
   
    a. **L’utilisateur A** est synchronisé en premier avec **UPN = User@contoso.com**.
   
    b. **L’utilisateur B** toobe tentative la synchronisation suivante avec **UPN = User@contoso.com** .
   
    c. **L’utilisateur B** UPN est modifié trop **User1234@contoso.onmicrosoft.com**  et  **User@contoso.com**  est ajouté trop**DirSyncProvisioningErrors**.
   
    d. message d’erreur Hello pour **utilisateur B** doit indiquer que **l’utilisateur A** a déjà  **User@contoso.com**  comme un UPN, mais il montre **l’utilisateur B** propre displayName.

**Rapport d’erreur de synchronisation d’identité** :

lien Hello pour *la procédure tooresolve ce problème* est incorrect :  
    ![Utilisateurs actifs](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "Utilisateurs actifs")  

Il doit pointer trop[https://aka.ms/duplicateattributeresiliency](https://aka.ms/duplicateattributeresiliency).

## <a name="see-also"></a>Voir aussi
* [Synchronisation d’Azure AD Connect](active-directory-aadconnectsync-whatis.md)
* [Intégration des identités locales dans Azure Active Directory](active-directory-aadconnect.md)
* [Identifier les erreurs de synchronisation d’annuaires dans Office 365](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067)

