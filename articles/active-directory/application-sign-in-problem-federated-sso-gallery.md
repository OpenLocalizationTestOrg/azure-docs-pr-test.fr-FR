---
title: "aaaProblems d’application de la galerie tooa configurée pour fédéré de signature sur l’authentification unique | Documents Microsoft"
description: "Conseils pour les erreurs spécifiques de hello lorsque vous vous connectez à une application que vous avez configuré pour SAML-fédéré-authentification auprès d’Azure AD"
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
ms.openlocfilehash: ba20a4904860cf063967029cad33fb80f16e4956
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooa-gallery-application-configured-for-federated-single-sign-on"></a>Problèmes de connexion d’application de la galerie tooa configurée pour fédérée l’authentification unique

tootroubleshoot votre problème, vous avez besoin de configuration de l’application hello tooverify dans Azure AD comme suit :

-   Vous avez suivi toutes les étapes de configuration hello pour hello application de la galerie Azure AD.

-   Hello identificateur et l’URL de réponse configurée dans AAD correspond à elles, les valeurs attendues dans l’application hello

-   Vous avez affecté des utilisateurs toohello application

## <a name="application-not-found-in-directory"></a>Application introuvable dans le répertoire

*Erreur AADSTS70001 : Application avec l’identificateur « https://contoso.com » est introuvable dans le répertoire de hello*.

**Cause possible**

attribut de l’émetteur Hello envoie hello application tooAzure AD dans la demande SAML hello ne correspond pas à valeur de l’identificateur hello configuré dans l’application hello Azure AD.

**Résolution :**

Vérifiez que cet attribut de l’émetteur hello dans la demande SAML hello qu'est mise en correspondance le hello valeur d’identificateur configuré dans Azure AD :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

  * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez application hello tooconfigure l’authentification unique

7.  Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.

8.  Accédez trop**domaine et les URL** section. Vérifiez cette valeur hello Bonjour identificateur valeur hello pour la valeur de l’identificateur hello affiché par erreur de hello est correspondant à la zone de texte.

Une fois que vous avez mis à jour de valeur d’identificateur hello dans Azure AD et sa correspondance hello valeur envoie par application hello dans la demande SAML hello, vous devez être en mesure de toosign dans toohello application.

## <a name="hello-reply-address-does-not-match-hello-reply-addresses-configured-for-hello-application"></a>adresse de réponse Hello ne correspondent pas aux adresses de réponse de hello configurés pour l’application hello.

*Erreur AADSTS50011 : adresse de réponse hello 'https://contoso.com' ne correspond pas à des adresses de réponse hello configurés pour l’application hello*

**Cause possible**

valeur de l’URL de réponse hello ou un modèle configuré dans Azure AD ne correspond pas Hello valeur AssertionConsumerServiceURL dans la demande SAML hello. Hello valeur AssertionConsumerServiceURL dans la demande SAML hello est URL hello vous voyez dans l’erreur de hello.

**Résolution :**

Vérifiez que cette valeur de AssertionConsumerServiceURL hello dans la demande SAML hello sa correspondance hello valeur de l’URL de réponse est configuré dans Azure AD.

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

  * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez application hello tooconfigure l’authentification unique

7.  Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.

8.  Accédez trop**domaine et les URL** section. Vérifier ou mettre à jour la valeur de hello dans la zone de texte toomatch hello valeur AssertionConsumerServiceURL dans la demande SAML hello de hello URL de réponse.  
    * Si vous ne voyez pas de zone de texte URL de réponse hello sélectionnez hello **afficher les paramètres d’URL avancés** case à cocher.

Une fois que vous avez mis à jour valeur de l’URL de réponse hello dans Azure AD et qu’il a correspondant hello valeur envoie par application hello Bonjour demande SAML, vous devez être en mesure de toosign dans toohello application.

## <a name="user-not-assigned-a-role"></a>Utilisateur non affecté à un rôle

*Erreur AADSTS50105 : hello utilisateur connecté 'brian@contoso.com' ne possède pas de rôle tooa pour l’application hello*.

**Cause possible**

Hello lui n'ont pas été accordées application toohello d’accès dans Azure AD.

**Résolution :**

tooassign un ou plusieurs utilisateurs tooan application directement, comme suit hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

  * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello tooassign une liste des utilisateurs toofrom hello.

7.  Une fois le charge de l’application hello, cliquez sur **utilisateurs et groupes** à partir du menu de navigation de gauche de l’application hello.

8.  Cliquez sur hello **ajouter** bouton par-dessus hello **utilisateurs et groupes** hello tooopen de liste **ajouter l’affectation** panneau.

9.  Cliquez sur hello **utilisateurs et groupes** sélecteur de hello **ajouter l’affectation** panneau.

10. Type Bonjour **nom complet** ou **adresse de messagerie** d’utilisateur hello vous êtes intéressé par attribution dans hello **recherche par nom ou adresse de messagerie** zone de recherche.

11. Placez le curseur sur hello **utilisateur** dans hello liste tooreveal un **case à cocher**. Cliquez sur tooadd de photo ou le logo de profil hello case à cocher suivante toohello l’utilisateur à votre toohello utilisateur **sélectionnés** liste.

12. **Facultatif :** si vous souhaitez que trop**ajouter plusieurs utilisateurs**, type dans un autre **nom complet** ou **adresse de messagerie** dans hello **Rechercher par nom ou l’adresse de messagerie** zone de recherche, cliquez sur tooadd de case à cocher hello cette toohello utilisateur **sélectionnés** liste.

13. Lorsque vous avez fini de sélectionner les utilisateurs, cliquez sur hello **sélectionnez** bouton tooadd les toohello la liste des toobe utilisateurs et groupes affectés toohello application.

14. **Facultatif :** cliquez sur hello **sélectionner un rôle** sélecteur Bonjour **ajouter l’affectation** panneau tooselect un rôle aux utilisateurs de toohello tooassign que vous avez sélectionné.

15. Cliquez sur hello **affecter** bouton tooassign hello application toohello les utilisateurs sélectionnés.

Après une courte période de temps, les utilisateurs de hello que vous avez sélectionné en toolaunch en mesure de ces applications à l’aide de hello des méthodes décrites dans la section de description de solution hello.

## <a name="not-a-valid-saml-request"></a>Demande SAML non valide

*Erreur AADSTS75005 : demande de hello n’est pas un message de protocole Saml2 valid.*

**Cause possible**

Azure AD ne prend pas en charge hello SAML de demande envoyé par l’application hello pour l’authentification unique. Voici certains problèmes courants :

-   Les champs requis dans la demande SAML hello manquants

-   La méthode de demande SAML encodée

**Résolution :**

1.  Capturez la demande SAML. Suivez le didacticiel de hello [comment toodebug basé sur SAML uniques authentification tooapplications dans Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn toocapture hello SAML demander.

2.  Contactez le fournisseur de l’application hello et partage :

   -   Demande SAML

   -   [Spécifications du protocole SAML d’authentification unique Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

Ils doivent valider ils prennent en charge l’implémentation d’Azure AD SAML hello pour l’authentification unique.

## <a name="no-resource-in-requiredresourceaccess-list"></a>Aucune ressource dans la liste requiredResourceAccess

*Erreur d’application client AADSTS65005:hello a demandé l’accès tooresource ' 00000002-0000-0000-c000-type "000000000000"'. Cette demande a échoué, car le client de hello, cette ressource n’a pas spécifié dans sa liste requiredResourceAccess*.

**Cause possible**

objet de l’application Hello est endommagé.

**Résolution : option 1**

problème de hello toosolve, ajouter la valeur d’identificateur unique hello dans la configuration de hello Azure AD. tooadd une valeur d’identificateur, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

  * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello que vous avez configuré l’authentification unique.

7.  Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello

8.  Sous hello **domaine et l’URL** section, vérifiez sur hello **afficher les paramètres d’URL avancés**.

9.  Bonjour **identificateur** un identificateur unique pour l’application hello de type zone de texte.

10. **Enregistrer** configuration de hello.


**Résolution : option 2**

Si l’option 1 ci-dessus n’a pas fonctionné pour vous, essayez de supprimer des application hello de répertoire de hello. Ensuite, ajoutez et reconfigurer l’application hello, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

  * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez application hello tooconfigure l’authentification unique

7.  Cliquez sur **supprimer** en hello en haut à gauche de l’application hello **vue d’ensemble** panneau.

8.  Actualiser Azure AD et ajouter l’application hello à partir de la galerie d’Azure AD hello. Ensuite, configurez l’application hello

<span id="_Hlk477190176" class="anchor"></span>Après la reconfiguration d’application hello, vous devez être en mesure de toosign dans toohello application.

## <a name="certificate-or-key-not-configured"></a>Certificat ou clé non configuré(e)

*Erreur AADSTS50003 : Aucune clé de signature configurée.*

**Cause possible**

objet de l’application Hello est endommagé et Azure AD ne reconnaît pas certificat hello configuré pour l’application hello.

**Résolution :**

toodelete et créer un nouveau certificat, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

 * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez application hello tooconfigure l’authentification unique

7.  Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.

8.  Cliquez sur **créer un nouveau certificat** sous hello **SAML certificat de signature** section.

9.  Sélectionnez une date d’expiration. Cliquez ensuite sur **Enregistrer**.

10. Vérifiez **activer le nouveau certificat** certificat de toooverride hello active. Ensuite, cliquez sur **enregistrer** haut hello du Panneau de hello et accepter le certificat de substitution tooactivate hello.

11. Sous hello **le certificat de signature SAML** , cliquez sur **supprimer** tooremove hello **inutilisé** certificat.

## <a name="problem-when-customizing-hello-saml-claims-sent-tooan-application"></a>Problème lors de la personnalisation des revendications de hello SAML envoyé tooan application

toolearn toocustomize hello SAML attribut revendications envoyées tooyour application, voir [revendications mappage dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) pour plus d’informations.

## <a name="next-steps"></a>Étapes suivantes
[Comment toodebug basé sur SAML uniques authentification tooapplications dans Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging)
