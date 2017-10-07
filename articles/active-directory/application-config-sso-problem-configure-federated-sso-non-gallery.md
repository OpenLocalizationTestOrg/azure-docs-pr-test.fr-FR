---
title: "aaaProblem configuration fédérée l’authentification unique pour une application non-galerie | Documents Microsoft"
description: "Résoudre certains des problèmes courants de hello que vous pouvez rencontrer lors de la configuration d’application SAML personnalisée tooyour d’authentification unique fédérée qui n’est pas répertoriée dans hello Galerie d’applications Azure AD"
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
ms.openlocfilehash: 8c80f0001de01cbc9930ef0441cd804082ee8578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a>Problème de configuration de l’authentification unique fédérée pour une application non issue de la galerie

Si vous rencontrez un problème lors de la configuration d’une application, Vérifiez que vous avez suivi toutes les étapes de hello dans l’article de hello [configuration uniques tooapplications ouverture de session qui ne sont pas dans la galerie d’applications Azure Active Directory hello.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)

## <a name="cant-add-another-instance-of-hello-application"></a>Impossible d’ajouter une autre instance de l’application hello

tooadd une deuxième instance d’une application, vous devez toobe en mesure de :

-   Configurer un identificateur unique pour la deuxième instance de hello. Vous ne serez pas hello tooconfigure en mesure de même identificateur utilisé pour première instance de hello.

-   Configurer un certificat différent que hello celui utilisé pour la première instance de hello.

Si hello application ne prend en charge des hello ci-dessus. Ensuite, vous ne serez pas en mesure de tooconfigure une deuxième instance.

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a>Où définir le format de hello EntityID (identifiant d’utilisateur)

Vous ne sont pas être en mesure de tooselect hello au format EntityID (identifiant d’utilisateur) que Azure AD envoie toohello application dans la réponse de hello après l’authentification des utilisateurs.

Format de hello sélectionnez Azure AD pour l’attribut de NameID hello (identifiant d’utilisateur) en fonction de la valeur hello sélectionnée ou hello format demandé par l’application hello Bonjour SAML AuthRequest. Pour plus d’informations, consultez l’article de hello [protocole SAML de l’authentification unique](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) section hello NameIDPolicy,

## <a name="where-do-i-get-hello-application-metadata-or-certificate-from-azure-ad"></a>Où obtenir les métadonnées de l’application hello ou un certificat auprès d’Azure AD

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
