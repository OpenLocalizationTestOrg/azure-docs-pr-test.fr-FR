---
title: les applications SaaS aaaConfigure pour une collaboration B2B dans Azure Active Directory | Documents Microsoft
description: Code et exemples PowerShell pour Azure Active Directory B2B Collaboration
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c3f22f81567c04ac23ef2316c09de718ecb15d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a>Configurer des applications SaaS pour B2B Collaboration

Azure Active Directory (Azure AD) B2B Collaboration fonctionne avec la plupart des applications qui s’intègrent à Azure AD. Dans cette section, nous vous fournissons des instructions sur la configuration de certaines applications SAP populaires à utiliser avec Azure AD B2B.

Avant d’examiner les instructions propres aux applications, voici quelques règles générales :

* Pour la plupart des applications de hello, programme d’installation de l’utilisateur a besoin de toohappen manuellement. Autrement dit, les utilisateurs doivent être créés manuellement dans l’application hello également.

* Pour les applications qui prennent en charge le programme d’installation automatique, telles que l’échange, invitations distinctes sont créées à partir d’applications de hello. Les utilisateurs doit être tooaccept que chaque invitation.

* Dans les attributs utilisateur hello, toomitigate les problèmes avec le disque de profil utilisateur altéré (UPD) dans les utilisateurs invités, toujours la valeur **identificateur de l’utilisateur** trop**user.mail**.


## <a name="dropbox-business"></a>Dropbox Business

tooenable les toosign les utilisateurs à l’aide de leur compte d’organisation, vous devez configurer manuellement échange Business toouse Azure AD comme fournisseur d’identité Security Assertion Markup Language (SAML). Si l’entreprise de l’échange n’a pas été configuré toodo par conséquent, il ne peut pas demander ou autorisent toosign les utilisateurs à l’aide d’Azure AD.

1. application d’entreprise de l’échange hello tooadd dans Azure AD, sélectionnez **des applications d’entreprise** dans hello du volet gauche, puis cliquez sur **ajouter**.

  ![bouton « Ajouter » de Hello sur la page des applications Enterprise hello](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. Bonjour **ajouter une application** fenêtre, entrez **dropbox** dans hello de zone de recherche, puis sélectionnez **Dropbox for Business** dans la liste des résultats hello.

  ![Recherchez « échange » sur hello ajouter une page d’application](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. Sur hello **l’authentification unique** page, sélectionnez **l’authentification unique** dans hello du volet gauche, puis entrez **user.mail** Bonjour **identificateur de l’utilisateur** zone. (Il est défini comme UPN par défaut).

  ![Configuration de l’authentification unique pour l’application hello](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. toodownload hello certificat toouse pour la configuration de l’échange, sélectionnez **configurer un échange**, puis sélectionnez **SAML Service URL d’authentification unique** dans la liste de hello.

  ![Téléchargement du certificat hello pour la configuration de l’échange](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. Connexion tooDropbox avec hello authentification URL à partir de hello **l’authentification unique** page.

  ![page de Hello signe dans l’échange](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. Dans le menu de hello, sélectionnez **Console d’administration**.

  ![lien « Console d’administration » Hello menu de Dropbox de hello](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. Bonjour **authentification** boîte de dialogue, sélectionnez **plus**, télécharger hello certificat puis, dans hello **URL de connexion** , entrez l’URL de hello SAML l’authentification unique.

  ![Hello le lien « Plus » dans la boîte de dialogue d’authentification hello réduit](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![Hello « URL de connexion » Bonjour développé la boîte de dialogue d’authentification](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. le programme d’installation automatique de l’utilisateur de tooconfigure Bonjour portail Azure, sélectionnez **Provisioning** dans le volet gauche de hello, sélectionnez **automatique** Bonjour **Mode d’approvisionnement** zone, puis sélectionnez **Autoriser**.

  ![Configuration de l’approvisionnement automatique d’un utilisateur Bonjour portail Azure](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

Une fois que les utilisateurs invités ou les membres ont été configurées dans l’application d’échange hello, ils reçoivent une invitation distincte à partir de Dropbox. toouse de l’authentification unique de l’échange, invités doivent accepter d’invitation hello en cliquant sur un lien.

## <a name="box"></a>Box
Vous pouvez activer les utilisateurs invités boîte du utilisateurs tooauthenticate avec leur compte Azure AD à l’aide de fédération qui est basée sur hello protocole SAML. Dans cette procédure, vous téléchargez tooBox.com de métadonnées.

1. Ajouter l’application hello Box à partir d’applications d’entreprise hello.

2. Configurer l’authentification unique sur Bonjour suivant l’ordre :

  ![Configurer l’authentification unique de Box](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 a. Bonjour **URL de connexion** zone, assurez-vous que les URL de connexion hello est définie correctement pour la zone Bonjour portail Azure. Cette URL est hello de votre locataire Box.com. Elle doit suivre la convention d’affectation de noms de hello *https://.box.com*.  
 Hello **identificateur** ne s’applique pas toothis application, mais il apparaît toujours comme un champ obligatoire.

 b. Bonjour **identificateur de l’utilisateur** , entrez **user.mail** (pour l’authentification unique pour les comptes invité).

 c. Sous **Certificat de signature SAML**, cliquez sur **Créer un certificat**.

 d. toobegin la configuration de votre toouse de locataire Box.com Azure AD comme fournisseur d’identité, téléchargez le fichier de métadonnées hello et enregistrez-le tooyour le disque local.

 e. Transférer hello métadonnées fichier toohello zone équipe de support technique, qui permet de configurer l’authentification unique pour vous.

3. Pour l’installation automatique d’un utilisateur Azure AD, dans le volet gauche de hello, sélectionnez **Provisioning**, puis sélectionnez **Authorize**.

  ![Autoriser Azure AD tooconnect tooBox](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

Comme invités de l’échange, invités de la zone doivent échanger leur invitation à partir de l’application hello Box.

## <a name="next-steps"></a>Étapes suivantes

Consultez hello suivant des articles sur Azure AD B2B collaboration :

* [Qu’est-ce qu’Azure AD B2B Collaboration ?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Propriétés de l’utilisateur B2B Collaboration](active-directory-b2b-user-properties.md)
* [Ajout d’un rôle tooa B2B collaboration](active-directory-b2b-add-guest-to-role.md)
* [Déléguer des invitations B2B Collaboration](active-directory-b2b-delegate-invitations.md)
* [Groupes dynamiques et B2B Collaboration](active-directory-b2b-dynamic-groups.md)
* [Code B2B Collaboration et exemples PowerShell](active-directory-b2b-code-samples.md)
* [Jetons utilisateur B2B Collaboration](active-directory-b2b-user-token.md)
* [Mappage des revendications utilisateur B2B Collaboration](active-directory-b2b-claims-mapping.md)
* [Partage externe d’Office 365](active-directory-b2b-o365-external-user.md)
* [Limitations actuelles de B2B Collaboration](active-directory-b2b-current-limitations.md)
