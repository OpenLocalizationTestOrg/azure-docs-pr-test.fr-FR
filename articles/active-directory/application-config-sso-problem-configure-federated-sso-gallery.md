---
title: "aaaProblem configuration fédérée l’authentification unique pour une application Azure AD galerie | Documents Microsoft"
description: "Résoudre certains des problèmes courants de hello vous pouvez rencontrer lors de la configuration fédérée seule l’authentification à l’aide de SAML pour les applications qui sont répertoriées dans la galerie d’applications Azure AD de hello"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 2ae1e511bd49b19159e1ab83cf79a7db5403b9a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>Problème de configuration de l’authentification unique fédérée pour une application de la galerie Azure AD

Si vous rencontrez un problème lors de la configuration d’une application, Vérifiez que vous avez suivi toutes les étapes de hello dans didacticiel hello pour une application hello. Dans la configuration de l’application hello, vous disposez de la documentation inline sur la façon dont tooconfigure hello application. Vous pouvez également accéder à hello [liste des didacticiels sur la façon de toointegrate les applications SaaS avec Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) pour obtenir une aide pas à pas détaillé.

## <a name="cant-add-another-instance-of-hello-application"></a>Impossible d’ajouter une autre instance de l’application hello

tooadd une deuxième instance d’une application, vous devez toobe en mesure de :

-   Configurer un identificateur unique pour la deuxième instance de hello. Vous ne serez pas hello tooconfigure en mesure de même identificateur utilisé pour première instance de hello.

-   Configurer un certificat différent que hello celui utilisé pour la première instance de hello.

Si hello application ne prend en charge des hello ci-dessus. Ensuite, vous ne serez pas en mesure de tooconfigure une deuxième instance.

## <a name="cant-add-hello-identifier-or-hello-reply-url"></a>Impossible d’ajouter hello identificateur ou de hello URL de réponse

Si vous n’êtes pas en mesure de tooconfigure hello identificateur ou hello URL de réponse, confirmez hello identificateur et valeurs de l’URL de réponse correspondent hello préconfiguré pour l’application hello.

modèles de hello tooknow préconfigurés pour l’application hello :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.** Accédez à toostep 7. Si vous êtes déjà dans le panneau de configuration d’application hello sur Azure AD.

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

   * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello tooconfigure l’authentification unique.

7.  Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.

8.  Sélectionnez **SAML-authentification** de hello **Mode** liste déroulante.

9.  Accédez toohello **identificateur** ou **URL de réponse** zone de texte, sous hello **section URL et de domaine.**

10. Il existe trois façons de tooknow des modèles de hello pris en charge pour l’application hello :

   * Dans la zone de texte hello, vous consultez ou hello pris en charge les modèles comme un espace réservé *exemple :* <https://contoso.com>.

   * Si le modèle de hello n’est pas pris en charge, vous consultez un point d’exclamation rouge lorsque vous essayez de valeur de hello tooenter dans la zone de texte hello. Si vous pointez votre souris sur le point d’exclamation rouge de hello, vous voir les modèles de hello pris en charge.

   * Dans le didacticiel hello pour une application hello, vous pouvez également obtenir des informations sur les modèles de hello pris en charge. Sous hello **Azure AD de configurer l’authentification unique sur** section. Étape accédez toohello pour les valeurs hello configuré sous hello **domaine et les URL** section.

Si les valeurs hello ne correspondent pas avec les modèles hello préconfigurés sur Azure AD. Vous pouvez :

-   Travailler avec des valeurs de tooget du fournisseur d’application hello qui correspondent au modèle hello préconfiguré sur Azure AD

-   Ou bien, vous pouvez contacter l’équipe d’Azure AD à < aadapprequest@microsoft.com > ou laisser un commentaire dans hello toorequest didacticiel hello mise à jour des modèles de hello pris en charge pour l’application hello

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a>Où définir le format de hello EntityID (identifiant d’utilisateur)

Vous ne sont pas être en mesure de tooselect hello au format EntityID (identifiant d’utilisateur) que Azure AD envoie toohello application dans la réponse de hello après l’authentification des utilisateurs.

Format de hello sélectionnez Azure AD pour l’attribut de NameID hello (identifiant d’utilisateur) en fonction de la valeur hello sélectionnée ou hello format demandé par l’application hello Bonjour SAML AuthRequest. Pour plus d’informations, consultez l’article de hello [protocole SAML de l’authentification unique](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) section hello NameIDPolicy,

## <a name="cant-find-hello-azure-ad-metadata-toocomplete-hello-configuration-with-hello-application"></a>Impossible de trouver hello Azure AD métadonnées toocomplete hello configuration avec l’application hello

métadonnées de l’application hello toodownload ou un certificat d’Azure AD, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

   * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello que vous avez configuré l’authentification unique.

7.  Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.

8.  Accédez trop**le certificat de signature SAML** section, puis cliquez sur **télécharger** valeur de la colonne. En fonction de l’application hello nécessite la configuration de l’authentification unique, vous voyez deux toodownload d’option hello hello Metadata XML ou hello du certificat.

Azure AD ne fournit pas une URL de métadonnées hello tooget. Hello métadonnées peuvent uniquement être récupérées dans un fichier XML.

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a>Ne connaissez pas comment toocustomize SAML revendications envoyé tooan application

toolearn toocustomize hello SAML attribut revendications envoyées tooyour application, voir [revendications mappage dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) pour plus d’informations.

## <a name="next-steps"></a>Étapes suivantes
[Gestion des applications avec Azure Active Directory](active-directory-enable-sso-scenario.md)
