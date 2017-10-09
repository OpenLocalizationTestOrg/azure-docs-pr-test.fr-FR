---
title: "certificats de fédération aaaManage dans Azure AD | Documents Microsoft"
description: "Découvrez comment celle toocustomize hello pour vos certificats de fédération et utilisation des certificats toorenew qui expire sous peu."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f516f7f0-b25a-4901-8247-f5964666ce23
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/09/2017
ms.author: jeedes
ms.openlocfilehash: e17622d25c9babfa295cc0bb68c24e21b8c574d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-certificates-for-federated-single-sign-on-in-azure-active-directory"></a>Gérer des certificats pour l’authentification unique fédérée sur Azure Active Directory
Cet article traite des questions courantes et les informations relatives à des certificats toohello que Azure Active Directory (Azure AD) crée tooestablish fédéré unique sign-on (SSO) tooyour applications SaaS. Ajouter des applications à partir de la galerie d’applications Azure AD hello ou à l’aide d’un modèle d’application non-gallery. Configurer l’application hello à l’aide d’option d’authentification unique fédérée de hello.

Cet article est tooapps uniquement pertinentes qui sont toouse configuré l’authentification unique de Azure AD via la fédération SAML, comme indiqué dans hello l’exemple suivant :

![Authentification unique Azure AD](./media/active-directory-sso-certs/saml_sso.PNG)

## <a name="auto-generated-certificate-for-gallery-and-non-gallery-applications"></a>Certificat généré automatiquement pour les applications de la galerie et celles ne figurant pas dans la galerie
Lorsque vous ajoutez une nouvelle application à partir de la galerie de hello et que vous configurez une SAML-authentification, Azure AD génère un certificat pour l’application hello qui n’est valide pendant trois ans. Vous pouvez télécharger ce certificat à partir de hello **le certificat de signature SAML** section. Pour les applications de la galerie, cette section peut afficher un certificat de hello toodownload option ou les métadonnées, selon la spécification hello pour application hello.

![Authentification unique Azure AD](./media/active-directory-sso-certs/saml_certificate_download.png)

## <a name="customize-hello-expiration-date-for-your-federation-certificate-and-roll-it-over-tooa-new-certificate"></a>Personnaliser la date d’expiration de hello pour votre certificat de la fédération et de le déployer sur le nouveau certificat de tooa
Par défaut, les certificats sont configurés tooexpire après trois ans. Vous pouvez choisir une autre date d’expiration votre certificat en effectuant hello comme suit.
captures d’écran Hello utilisent Salesforce pour l’exploration de l’exemple hello, mais ces étapes peuvent s’appliquent tooany fédéré SaaS application.

1. Bonjour [portail Azure](https://aad.portal.azure.com), cliquez sur **application d’entreprise** dans hello du volet gauche, puis cliquez sur **nouvelle application** sur hello **vue d’ensemble** page :

   ![Assistant de configuration de l’authentification unique hello ouvert](./media/active-directory-sso-certs/enterprise_application_new_application.png)

2. Rechercher des applications de la galerie hello, puis sélectionnez application hello que vous souhaitez tooadd. Si vous ne trouvez pas application hello requis, ajouter application hello à l’aide de hello **application Non-gallery** option. Cette fonctionnalité est disponible uniquement dans hello référence (SKU) de Azure AD Premium (P1 et P2).

    ![Authentification unique Azure AD](./media/active-directory-sso-certs/add_gallery_application.png)

3. Cliquez sur hello **l’authentification unique** lien Bonjour gauche du volet et changez **Mode d’authentification unique** trop**SAML-authentification**. Cette étape génère pour votre application un certificat valide trois ans.

4. toocreate un nouveau certificat, cliquez sur hello **créer un nouveau certificat** lien Bonjour **le certificat de signature SAML** section.

    ![Générer un nouveau certificat](./media/active-directory-sso-certs/create_new_certficate.png)

5. Hello **créer un nouveau certificat** lien ouvre le contrôle de calendrier hello. Vous pouvez définir toute date et heure des années de toothree de hello date actuelle. Hello sélectionné de date et heure est date d’expiration de la nouvelle hello et l’heure de votre nouveau certificat. Cliquez sur **Enregistrer**.

    ![Téléchargez, puis télécharger le certificat de hello](./media/active-directory-sso-certs/certifcate_date_selection.PNG)

6. À présent, un nouveau certificat hello toodownload disponible. Cliquez sur hello **certificat** toodownload de lien il. À ce stade, votre certificat n’est pas encore actif. Lorsque vous souhaitez tooroll par toothis certificat, sélectionnez hello **activer le nouveau certificat** case à cocher et cliquez sur **enregistrer**. À partir de là, Azure AD démarre à l’aide d’un nouveau certificat hello pour la signature de réponse de hello.

7.  toolearn comment hello de tooupload certificat tooyour les application SaaS spécifique, cliquez sur hello **afficher le didacticiel configuration application** lien.

## <a name="renew-a-certificate-that-will-soon-expire"></a>Renouvellement d’un certificat arrivant à expiration
Hello suit le renouvellement doit-elle entraîner aucune interruption de service importantes pour vos utilisateurs. captures d’écran Hello dans cette fonctionnalité section Salesforce comme un exemple, mais ces étapes peuvent s’appliquer tooany fédéré SaaS application.

1. Sur hello **Azure Active Directory** application **l’authentification unique** page, générer hello nouveau certificat pour votre application. Vous pouvez faire cela en cliquant sur hello **créer un nouveau certificat** lien Bonjour **le certificat de signature SAML** section.

    ![Générer un nouveau certificat](./media/active-directory-sso-certs/create_new_certficate.png)

2. Sélectionnez hello souhaité date d’expiration et l’heure pour votre nouveau certificat cliquez sur **enregistrer**.

3. Télécharger le certificat hello Bonjour **certificat de signature de SAML** option. Écran de configuration de l’authentification unique de téléchargement hello certificat toohello SaaS de nouvelle application. toolearn comment toodo pour que votre application SaaS spécifique, cliquez sur hello **afficher le didacticiel configuration application** lien.
   
4. tooactivate hello nouveau certificat dans Azure AD, sélectionnez hello **activer le nouveau certificat** case à cocher et cliquez sur hello **enregistrer** bouton en hello haut hello. Cette procédure restaure sur le nouveau certificat de hello sur hello côté d’Azure AD. Hello certificat de hello l’état à partir de **nouveau** trop**Active**. À partir de là, Azure AD démarre à l’aide d’un nouveau certificat hello pour la signature de réponse de hello. 
   
    ![Générer un nouveau certificat](./media/active-directory-sso-certs/new_certificate_download.png)

## <a name="related-articles"></a>Articles connexes
* [Liste des didacticiels sur la façon de toointegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)
* [Accès aux applications et authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Dépannage de l’authentification unique basée sur SAML](active-directory-saml-debugging.md)
