---
title: "aaaCustomize vous connecter à la page Bonjour Azure Active Directory | Documents Microsoft"
description: "Découvrez comment tooadd une page toohello connectez-vous Azure marque de société"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 151521e3b9cbc6a438a589735058fbff78443cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a>Ajouter des logos tooyour-page de connexion Bonjour Azure Active Directory de la société
tooavoid confusion, de nombreuses sociétés souhaitent tooapply une apparence cohérente sur tous les sites Web de hello et services qu’ils gèrent. Azure Active Directory offre cette possibilité en vous donnant l’apparence de hello toocustomize de hello-page de connexion avec votre logo de l’entreprise et les jeux de couleurs personnalisées. page de connexion Hello est page hello qui s’affiche lorsque vous vous connectez tooOffice 365 ou autres applications web qui utilisent Azure AD comme fournisseur d’identité. Vous interagissez avec cette tooenter page vos informations d’identification.

Si vous souhaitez tooshow marque de votre société, les couleurs et les autres éléments personnalisables sur cette page, consultez hello suivant images toounderstand hello différence deux expériences de hello.

Hello capture d’écran affiche et l’exemple hello Office 365-page de connexion sur un ordinateur de bureau **avant** une personnalisation :

![Page de connexion Office 365 avant la personnalisation](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

Hello capture d’écran affiche et l’exemple hello Office 365-page de connexion sur un ordinateur de bureau **après** une personnalisation :

![Page de connexion d’Office 365 après la personnalisation](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-hello-sign-in-page"></a>Personnalisation de hello-page de connexion
En règle générale, si vous avez besoin d’accès basé sur un navigateur tooyour applications et services cloud que votre organisation est abonnée à, vous utilisez hello-page de connexion.

Si vous avez appliqué les modifications tooyour-page de connexion, il peut prendre les horaires de tooan pour tooappear de modifications hello.

Une page de connexion personnalisée s’affiche uniquement lorsque vous accédez à un service avec une URL spécifique au client, telle que https://outlook.com/**contoso**.com, ou https://mail.**contoso**.com.

Lorsque vous visitez un service avec une URL non spécifique au client (par exemple : https://mail.office365.com), une page de connexion non personnalisée s’affiche. Dans ce cas, votre marque apparaît une fois que vous avez entré votre ID d’utilisateur ou que vous avez sélectionné une vignette utilisateur.

> [!NOTE]
> * Votre nom de domaine doit être « Actif » dans hello **domaines** partie de hello portail Azure, dans lequel vous avez effectué la personnalisation. Pour plus d’informations, consultez [Ajouter des noms de domaine personnalisés](active-directory-domains-add-azure-portal.md).
> * Personnalisation de la page de connexion n’est pas reflétée sur la page de Microsoft de connexion consommateur toohello. Si vous vous connectez avec un compte Microsoft, vous pouvez voir une liste personnalisée de vignettes utilisateur rendues par Azure AD, mais toohello Microsoft compte-page de connexion ne s’applique pas hello de personnalisation de votre organisation.
>
>

Sur votre page de connexion, hello **maintenir la connexion** case à cocher permet un tooremain utilisateur connecté lorsqu’ils ferment et rouvrir leur navigateur.

   ![Maintenir la connexion](./media/active-directory-branding-custom-signon-azure-portal/01.png)

Elle n’a pas d’effet sur la durée de vie de session. Vous pouvez masquer la case à cocher hello sur hello Azure Active Directory-page de connexion.
Si la case à cocher hello est affiché en fonction de définition de hello de **maintenir la connexion désactivée**.

   ![Maintenir la connexion](./media/active-directory-branding-custom-signon-azure-portal/02.png)

toohide hello case à cocher, configurez ce paramètre trop**Oui**.

> [!NOTE]
> Certaines fonctionnalités de SharePoint Online et Office 2010 dépendent des utilisateurs en mesure de toocheck cette case. Si vous configurez ce paramètre toohidden, vos utilisateurs peuvent voir des invites de supplémentaires et inattendues dans toosign.
>
>

**marque active de tooyour de l’entreprise de tooadd :**

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.
2. Sélectionnez **davantage de services**, entrez **utilisateurs et groupes** dans hello de zone de texte, puis sélectionnez **entrée**.

   ![Ouvrir la gestion des utilisateurs](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. Sur hello **utilisateurs et groupes** panneau, sélectionnez **de personnalisation de la société**.
4. Sur hello **utilisateurs et groupes - personnalisation de la société** panneau, sélectionnez hello **modifier** commande.

    ![Modifier la personnalisation de société](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. Modifier les éléments hello toocustomize. Tous ces éléments sont facultatifs.
6. Cliquez sur **Enregistrer**.

Pour les modifications éventuelles apportées toohello connectez-vous page tooappear marque peut prendre jusqu'à tooan heure.

## <a name="next-steps"></a>Étapes suivantes
[Ajouter la marque de l’entreprise spécifique à une langue](active-directory-branding-localize-azure-portal.md)
