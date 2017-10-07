---
title: "aaaPreview Office 365 regroupe d’expiration dans Azure Active Directory | Documents Microsoft"
description: "Façon dont les groupes tooset d’expiration pour Office 365 dans Azure Active Directory (version préliminaire)"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro
ms.openlocfilehash: a8c99961cff3aad3f4d8b0cc1b2eb8e8a4c9ba95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-office-365-groups-expiration-preview"></a>Configurer l’expiration des groupes Office 365 (préversion)

Vous pouvez désormais gérer hello du cycle de vie des groupes Office 365 en définissant la date d’expiration pour les groupes Office 365 que vous sélectionnez. Une fois cette expiration est définie, les propriétaires de ces groupes sont demandé toorenew leurs groupes s’ils doivent toujours les groupes hello. Les groupes Office 365 qui ne sont pas renouvelés seront supprimés. N’importe quel groupe Office 365 qui a été supprimé peut être restauré dans les 30 jours par les propriétaires de groupe hello ou un administrateur de hello.  


> [!NOTE]
> Vous pouvez définir l’expiration pour les groupes Office 365 uniquement.
>
> La définition de l’expiration pour les groupes O365 nécessite qu’une licence Azure AD Premium soit affectée à
>   - administrateur de Hello qui configure les paramètres d’expiration de hello pour le client de hello
>   - Tous les membres de groupes hello sélectionnés pour ce paramètre

## <a name="set-office-365-groups-expiration"></a>Définir l’expiration des groupes Office 365

1. Ouvrez hello [centre d’administration Azure AD](https://aad.portal.azure.com) avec un compte qui est un administrateur global dans votre locataire Azure AD.

2. Ouvrez Azure AD et sélectionnez **Utilisateurs et groupes**.

3. Sélectionnez **paramètres de groupe** , puis sélectionnez **Expiration** paramètres d’expiration de hello tooopen.
  
  ![Panneau Expiration](./media/active-directory-groups-lifecycle-azure-portal/expiration-settings.png)

4. Sur hello **Expiration** panneau, vous pouvez :

  * Définir la durée de vie de groupe hello en jours. Vous pouvez sélectionner un des hello prédéfinie de valeurs ou une valeur personnalisée (doit être 31 jours ou plus). 
  * Spécifiez une adresse de messagerie dans lequel les notifications d’expiration et le renouvellement hello entraînant l’envoi d’un groupe n’a aucun propriétaire. 
  * Sélectionnez les groupes Office 365 qui expirent. Vous pouvez activer l’expiration pour **tous les** les groupes Office 365, vous pouvez sélectionner parmi les groupes hello Office 365, ou que vous sélectionnez **aucun** pour désactiver la date d’expiration pour tous les groupes.
  * Enregistrer vos paramètres lorsque vous avez terminé en sélectionnant **Enregistrer**.

Pour obtenir des instructions sur la façon dont toodownload et installez hello d’expiration tooconfigure de module PowerShell de Microsoft pour les groupes Office 365 via PowerShell, consultez [Module Azure Active Directory V2 PowerShell - version préliminaire publique 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).

Les notifications par courrier électronique similaires sont envoyées à 30 jours, 15 jours, les propriétaires de groupe toohello Office 365 et tooexpiration préalable de 1 jour du groupe de hello.

![Notification par e-mail de l’expiration](./media/active-directory-groups-lifecycle-azure-portal/expiration-notification.png)

propriétaire du groupe Hello peut ensuite sélectionner **renouveler groupe** toorenew hello groupe Office 365, ou pouvez sélectionner **accédez toogroup** membres de hello toosee et d’autres détails sur hello groupe.

Lors de l’expiration d’un groupe, groupe de hello est supprimé d’un jour après la date d’expiration de hello. Une notification par courrier électronique, tels que celui-ci est envoyée de propriétaires du groupe toohello Office 365 pour l’informer sur d’expiration de hello ultérieure la suppression et de leur groupe Office 365.

![Notification par e-mail de la suppression du groupe](./media/active-directory-groups-lifecycle-azure-portal/deletion-notification.png)

groupe de Hello peut être restaurée en sélectionnant **groupe restauration** ou à l’aide des applets de commande PowerShell, comme décrit dans [groupe restauration un supprimé Office 365 dans Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/ Active-Directory-Groups-Restore-Azure-Portal).
    
Si le groupe hello que vous restaurez contient des documents, les sites SharePoint ou autres objets persistants, elle peut prendre le groupe hello restauration too24 heures toofully et son contenu.

> [!NOTE]
> * Lorsque vous déployez des paramètres d’expiration de hello, il peut y avoir certains groupes qui sont antérieurs à la fenêtre d’expiration hello. Ces groupes ne sont pas supprimées immédiatement, mais sont de définir les jours too30 avant l’expiration. Hello premier renouvellement notification par courrier électronique est envoyée au sein d’un jour. Par exemple, le groupe A a été créé 400 jours, et que l’intervalle d’expiration hello est défini too180 jours. Lorsque vous appliquez les paramètres d’expiration, le groupe A a 30 jours avant d’être supprimé, sauf si le propriétaire de hello renouvelle celui-ci.
> * Lorsqu’un groupe dynamique est supprimé et restauré, il est considéré comme un nouveau groupe et le nouveau remplis règle toohello correspondants. Ce processus peut prendre des heures de too24.

## <a name="next-steps"></a>Étapes suivantes
Ces articles fournissent des informations supplémentaires sur les groupes Azure AD.

* [Consulter les groupes existants](active-directory-groups-view-azure-portal.md)
* [Gérer les paramètres d’un groupe](active-directory-groups-settings-azure-portal.md)
* [Gérer les membres d’un groupe](active-directory-groups-members-azure-portal.md)
* [Gérer l’appartenance à un groupe](active-directory-groups-membership-azure-portal.md)
* [Gérer les règles dynamiques pour les utilisateurs dans un groupe](active-directory-groups-dynamic-membership-azure-portal.md)
