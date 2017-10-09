---
title: "aaaCustomizing les revendications émises dans un jeton SAML de hello pour les applications pré-intégrées dans Azure Active Directory | Documents Microsoft"
description: "Découvrez comment toocustomize hello revendications émises dans hello jeton SAML pour les applications pré-intégrées dans Azure Active Directory"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f1daad62-ac8a-44cd-ac76-e97455e47803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.custom: aaddev
ms.openlocfilehash: a376318929472403e799f02fdd3fbddc91d0a70c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-claims-issued-in-hello-saml-token-for-pre-integrated-apps-in-azure-active-directory"></a>Personnalisation des revendications émises dans hello jeton SAML pour les applications pré-intégrées dans Azure Active Directory
Aujourd'hui Azure Active Directory prend en charge des milliers d’applications pré-intégrées Bonjour Galerie d’applications Azure AD, y compris supérieures à 360 qui prennent en charge l’authentification unique à l’aide du protocole de hello SAML 2.0. Lorsqu’un utilisateur s’authentifie application tooan via Azure AD à l’aide de SAML, Azure AD envoie une application de jeton toohello (via une requête HTTP POST). Puis, application hello valide utilise hello toolog jeton hello utilisateur au lieu de demander un nom d’utilisateur et un mot de passe. Ces jetons SAML contiennent des informations sur l’utilisateur hello appelé « revendications ».

En jargon d’identité, une revendication » » informations indiquant à un fournisseur d’identité sur un utilisateur à l’intérieur du jeton hello qu’elles émettent pour cet utilisateur. Dans [jeton SAML](http://en.wikipedia.org/wiki/SAML_2.0), ces données sont généralement contenues dans hello instruction d’attribut SAML. Hello ID unique de l’utilisateur est généralement représentée dans hello que SAML Subject est également appelé en tant qu’identificateur de nom.

Par défaut, Azure Active Directory émet une application tooyour jeton SAML qui contient une revendication NameIdentifier, avec la valeur du nom d’utilisateur de l’utilisateur hello (AKA nom d’utilisateur principal) dans Azure AD. Cette valeur peut identifier les utilisateurs hello. jeton SAML de Hello contient également des revendications supplémentaires contenant l’adresse de messagerie de l’utilisateur hello, prénom et nom.

les revendications hello tooview ou modifier émis Bonjour application de toohello jeton SAML, application hello ouvert dans le portail Azure. Puis sélectionnez hello **afficher et modifier tous les autres attributs utilisateur** case à cocher Bonjour **attributs utilisateur** section de l’application hello.

![Section Attributs utilisateur][1]

Il existe deux raisons pour lesquelles vous devrez peut-être les revendications de hello tooedit émises dans un jeton SAML de hello :
* application Hello a été écrit toorequire une autre valeur de revendication URI ou des valeurs de revendication.
* application Hello a été déployée dans une manière requérant toobe de revendication NameIdentifier hello autre chose qu’un nom d’utilisateur de hello (AKA nom d’utilisateur principal) stockées dans Azure Active Directory.

Vous pouvez modifier une des valeurs de revendication hello par défaut. Sélectionnez la ligne de revendication de hello dans la table d’attributs du jeton hello SAML. Cette opération ouvre hello **modifier l’attribut** section et que vous pouvez modifier les espace de noms associé hello revendication, valeur et nom de la revendication.

![Modifier un attribut utilisateur][2]

Vous pouvez également supprimer les revendications (autres que NameIdentifier) à l’aide du menu contextuel de hello, qui s’ouvre en cliquant sur hello **...**  icône.  Vous pouvez également ajouter des revendications de nouveau à l’aide de hello **ajouter un attribut** bouton.

![Modifier un attribut utilisateur][3]

## <a name="editing-hello-nameidentifier-claim"></a>Modification hello revendication NameIdentifier
problème de hello toosolve où l’application hello a été déployée à l’aide d’un nom d’utilisateur différent, cliquez sur hello **identificateur de l’utilisateur** déroulante Bonjour **attributs utilisateur** section. Cette action donne accès à une boîte de dialogue qui contient différentes options :

![Modifier un attribut utilisateur][4]

Dans la liste déroulante de hello, sélectionnez **user.mail** tooset hello NameIdentifier revendication d’adresse de messagerie de l’utilisateur toobe hello dans le répertoire de hello. Ou bien, sélectionnez **user.onpremisessamaccountname** tooset toohello SAM nom du compte utilisateur qui a été synchronisé à partir d’Azure AD local.

Vous pouvez également utiliser hello spéciaux **ExtractMailPrefix()** suffixe de domaine tooremove hello fonction de l’adresse de messagerie hello, nom de compte SAM ou nom d’utilisateur principal hello. Cette opération extrait uniquement la première partie de hello d’utilisateur de hello nom transmises par l’intermédiaire (par exemple, « joe_smith » au lieu de joe_smith@contoso.com).

![Modifier un attribut utilisateur][5]

Nous avons ajouté désormais également hello **join()** hello toojoin de fonction vérifié domaine avec la valeur de l’identificateur hello utilisateur. Lorsque vous sélectionnez la fonction de join() hello Bonjour **identificateur de l’utilisateur** Sélectionnez tout d’abord hello identificateur d’utilisateur comme nom principal de messagerie utilisateur ou une adresse, puis dans hello seconde liste déroulante votre domaine vérifié. Si vous sélectionnez une adresse de messagerie hello avec le domaine vérifié de hello, Azure AD extrait hello première valeur joe_smith de nom d’utilisateur hello joe_smith@contoso.com et l’ajoute à contoso.onmicrosoft.com. Consultez hello l’exemple suivant :

![Modifier un attribut utilisateur][6]

## <a name="adding-claims"></a>Ajout de revendications
Lorsque vous ajoutez une revendication, vous pouvez spécifier le nom de l’attribut hello (qui n’a pas besoin strictement toofollow un modèle d’URI conformément aux spécifications SAML hello). Définir l’attribut hello valeur tooany utilisateur qui est stocké dans le répertoire de hello.

![Ajouter un attribut utilisateur][7]

Par exemple, vous devez toosend département hello hello utilisateur appartient tooin leur organisation en tant que revendication (par exemple, ventes). Entrez le nom de la revendication hello comme prévu par l’application hello et sélectionnez **user.department** en tant que valeur de hello.

> [!NOTE]
> Si aucune valeur ne stockée pour un attribut sélectionné est pour un utilisateur donné, puis cette revendication n’est pas émise dans un jeton de hello.

> [!TIP]
> Hello **user.onpremisesecurityidentifier** et **user.onpremisesamaccountname** sont uniquement pris en charge lors de la synchronisation des données utilisateur à partir de sur site Active Directory à l’aide de hello [Azure Outil de connexion AD](../active-directory-aadconnect.md).

## <a name="restricted-claims"></a>Revendications restreintes

Il existe certaines revendications restreintes dans SAML. Si vous ajoutez ces revendications, Azure AD ne les enverra pas. Voici hello SAML restreint l’ensemble de revendications :

    | Type de revendication (URI) |
    | ------------------- |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/expired |
    | http://schemas.microsoft.com/identity/claims/accesstoken |
    | http://schemas.microsoft.com/identity/claims/openid2_id |
    | http://schemas.microsoft.com/identity/claims/identityprovider |
    | http://schemas.microsoft.com/identity/claims/objectidentifier |
    | http://schemas.microsoft.com/identity/claims/puid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1] |
    | http://schemas.microsoft.com/identity/claims/tenantid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod |
    | http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/groups |
    | http://schemas.microsoft.com/claims/groups.link |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/role |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/wids |
    | http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant |
    | http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown |
    | http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged |
    | http://schemas.microsoft.com/2014/03/psso |
    | http://schemas.microsoft.com/claims/authnmethodsreferences |
    | http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier |
    | http://schemas.microsoft.com/identity/claims/scope |

## <a name="next-steps"></a>Étapes suivantes
* [Index d’articles pour la gestion des applications dans Azure Active Directory](../active-directory-apps-index.md)
* [Configuration uniques tooapplications ouverture de session qui ne sont pas dans la galerie d’applications Azure Active Directory hello](../active-directory-saas-custom-apps.md)
* [Dépannage de l’authentification unique basée sur SAML](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saml-claims-customization/user-attribute-section.png
[2]: ./media/active-directory-saml-claims-customization/edit-claim-name-value.png
[3]: ./media/active-directory-saml-claims-customization/delete-claim.png
[4]: ./media/active-directory-saml-claims-customization/user-identifier.png
[5]: ./media/active-directory-saml-claims-customization/extractemailprefix-function.png
[6]: ./media/active-directory-saml-claims-customization/join-function.png
[7]: ./media/active-directory-saml-claims-customization/add-attribute.png