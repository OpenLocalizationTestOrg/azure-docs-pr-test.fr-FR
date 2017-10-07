---
title: "aaaCustomize vous connecter à la page Bonjour Azure Active Directory | Documents Microsoft"
description: "Découvrez comment tooadd une page toohello connectez-vous Azure marque de société"
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeffgilb
custom: it-pro
ms.openlocfilehash: 7a7ccdeef0764f6cf9e9e224acd4350983031fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-company-branding-tooyour-sign-in-page-in-azure-ad"></a>Démarrage rapide : Ajouter la marque de société tooyour-page de connexion dans Azure AD
tooavoid confusion, de nombreuses sociétés souhaitent tooapply une apparence cohérente sur tous les sites Web de hello et services qu’ils gèrent. Azure Active Directory (Azure AD) offre cette possibilité en vous donnant l’apparence de hello toocustomize de hello-page de connexion avec votre logo de l’entreprise et les jeux de couleurs personnalisées. page de connexion Hello est page hello qui s’affiche lorsque vous vous connectez tooOffice 365 ou autres applications web qui utilisent Azure AD comme fournisseur d’identité. Vous interagissez avec cette tooenter page vos informations d’identification.

> [!NOTE]
> * Marque de société est disponible uniquement si la mise à niveau toohello Premium ou édition Basic d’Azure AD, ou disposer d’une licence Office 365. toolearn si une fonctionnalité est prise en charge par votre type de licence, vérifiez hello [page d’informations de la tarification Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).
> 
> * Azure Active Directory Premium et les éditions de base sont disponibles pour les clients en Chine utilisent hello instance mondiale d’Azure Active Directory. Azure Active Directory Premium et les éditions de base ne sont pas actuellement pris en charge dans le service Microsoft Azure hello géré par 21Vianet en Chine. Pour plus d’informations, veuillez nous contacter à hello [Forum Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/).

## <a name="customizing-hello-sign-in-page"></a>Personnalisation de hello-page de connexion

<!--You can customize hello following elements on hello sign-in page: <attach image>-->

Société personnalisations marque apparaissent sur la page de connexion hello Azure AD lorsque les utilisateurs accèdent à une URL spécifique du client tel que [ *https://outlook.com/contoso.com*](https://outlook.com/contoso.com).

Lorsque les utilisateurs ont accès à une URL générique, telle que www.office.com, hello-page de connexion ne contient pas de marque les personnalisations, car le système de hello ne sait pas qui hello utilisateur de l’entreprise. La marque de société s’affiche une fois que les utilisateurs ont indiqué leur identifiant d’utilisateur, ou sélectionné la mosaïque d’un utilisateur.

> [!NOTE]
> * Votre nom de domaine doit être « Actif » dans hello **domaines** partie de hello portail Azure, dans lequel vous avez effectué la personnalisation. Pour plus d’informations, consultez [Ajouter un nom de domaine personnalisé](add-custom-domain.md).
> * Personnalisation de la page de connexion n’est pas reflétée sur toohello-page de connexion pour les comptes Microsoft personnels. Si vos employés ou les invités à vous connecter avec un compte Microsoft personnel, leur page de connexion ne reflète pas hello de personnalisation de votre organisation.


### <a name="banner-logo"></a>Logo de bannière 

Description | Contraintes | Recommandations
------- | ------- | ----------
logo de bannière Hello est affichée sur hello connexion et la page du volet d’accès hello.<br>Sur la page de connexion hello, cela indique une fois que l’organisation de l’utilisateur hello est déterminée, généralement après que le nom d’utilisateur hello est entré.  | JPG ou PNG transparent<br>Hauteur max. : 36 px<br>Largeur max. : 245 px | Utilisez le logo de votre organisation ici.<br>Utilisez une image transparente. Ne supposez pas que hello arrière-plan apparaîtra en blanc.<br>N’ajoutez pas de marge intérieure autour de votre logo dans l’image de hello ou votre logo ressemblera disproportionnellement petit.

### <a name="username-hint"></a>Indication sur le nom d’utilisateur   
Description | Contraintes | Recommandations
------- | ------- | ----------
Cela personnalise le texte d’indication hello dans le champ de nom d’utilisateur hello. | Texte Unicode des caractères de too64<br>Texte brut uniquement | Nous vous recommandons de ne pas définir cela si vous pensez que les utilisateurs invités à l’extérieur de votre toosign d’organisation dans tooyour application.
            
### <a name="sign-in-page-text"></a>Texte de la page de connexion   
Description | Contraintes | Recommandations
------- | ------- | ----------
Cela s’affiche en bas de hello du formulaire de connexion hello et peut être utilisé toocommunicate des informations supplémentaires telles que hello phone numéro tooyour d’assistance ou une mention légale. | Texte Unicode des caractères de too256<br>Texte brut uniquement (aucun lien ni balise HTML) 

### <a name="sign-in-page-image"></a>Image de la page de connexion  
Description | Contraintes | Recommandations
------- | ------- | ----------
Cette propriété apparaît en arrière-plan hello de hello-page de connexion, est ancré toohello centre d’espace visible de hello et sera mise à l’échelle et rogner toofill fenêtre du navigateur hello.  <br>Sur les écrans étroits tels que les téléphones mobiles, l’image n’est pas affichée.<br>Un masque noir avec opacité 0,55 sera appliqué sur cette image par notre code lorsque hello est chargée. | JPG ou PNG<br>Dimensions de l’image : 1 920 x 1 080 px<br>Taille de fichier : &gt; 300 Ko | <br>Utilisez des images lorsqu’il n’y a pas de focalisation forte sur l’objet. Hello opaque-formulaire de connexion s’affiche sur le centre de hello de cette image et peut couvrir une partie de l’image de hello en fonction de la taille de fenêtre du navigateur hello de hello.<br>Conserver la taille du fichier hello aussi petit que le temps de chargement rapide de tooensure possible. 

### <a name="background-color"></a>Couleur d’arrière-plan
Description | Contraintes | Recommandations
------- | ------- | ----------
Cette couleur est utilisée à la place d’image d’arrière-plan hello sur les connexions à faible bande passante. |   Couleur RVB en hexadécimal (par exemple #FFFFFF) | Nous vous suggérons d’à l’aide de la couleur de principal de hello de logo de bannière hello ou votre organisation.

### <a name="show-option-tooremain-signed-in"></a>Afficher les tooremain option connecté
Description | Contraintes | Recommandations
------- | ------- | ----------
Connexion Azure AD offre hello utilisateur hello option tooremain connecté lorsqu’ils ferment et rouvrir leur navigateur. Utilisez cette toohide cette option.<br>Définissez cette trop « non » toohide cette option à partir de vos utilisateurs. | &nbsp; | Cela n’a pas d’effet sur la durée de vie de session.<br>Certaines fonctionnalités de SharePoint Online et Office 2010 dépendent des utilisateurs tooremain en mesure de toochoose connecté. Si vous définissez cette toobe masqué, vos utilisateurs peuvent voir des invites de supplémentaires et inattendues dans toosign.

> [!NOTE]
> Tous ces éléments sont facultatifs. Par exemple, si vous spécifiez un logo de bannière avec aucune image d’arrière-plan, hello-page de connexion affiche votre image d’arrière-plan hello et le logo hello site de destination (par exemple, Office 365).

## <a name="add-company-branding-tooyour-directory"></a>Ajouter des logos tooyour active de la société

1. Connectez-vous trop[hello portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.
2. Sélectionnez **davantage de services**, entrez **utilisateurs et groupes** dans hello de zone de texte, puis sélectionnez **entrée**.

   ![Ouvrir la gestion des utilisateurs](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. Sur hello **utilisateurs et groupes** panneau, sélectionnez **de personnalisation de la société**.
4. Sur hello **utilisateurs et groupes - personnalisation de la société** panneau, sélectionnez hello **modifier** commande.

    ![Modifier la personnalisation de société](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. Modifier les éléments hello toocustomize. Tous ces éléments sont facultatifs.
6. Cliquez sur **Enregistrer**.

Pour les modifications éventuelles apportées toohello connectez-vous page tooappear marque peut prendre jusqu'à tooan heure.

## <a name="add-language-specific-company-branding-tooyour-directory"></a>Ajouter des logos tooyour active de la société spécifiques au langage

1. Connectez-vous à toohello [centre d’administration Azure AD](https://aad.portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.
2. Sélectionnez **utilisateurs et groupes** dans hello de zone de texte, puis sélectionnez **entrée**.

   ![Ouvrir la gestion des utilisateurs](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. Sur hello **utilisateurs et groupes** panneau, sélectionnez **de personnalisation de la société**.
4. Sur hello **utilisateurs et groupes - personnalisation de la société** panneau, sélectionnez hello **Ajouter langue** commande.

    ![Ajouter des éléments spécifiques à une langue](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. Modifier les éléments hello toocustomize. Tous ces éléments sont facultatifs.
6. Cliquez sur **Enregistrer**.

Pour les modifications éventuelles apportées toohello connectez-vous page tooappear marque peut prendre jusqu'à tooan heure.

## <a name="next-steps"></a>Étapes suivantes
Dans ce démarrage rapide, vous avez appris comment tooadd marque tooyour Azure AD directory d’entreprise. 

Vous pouvez utiliser hello suivant lien tooconfigure votre marque de société dans Azure AD à partir de hello portail Azure.

> [!div class="nextstepaction"]
> [Configurer la marque de la société](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/LoginTenantBrandingBlade) 