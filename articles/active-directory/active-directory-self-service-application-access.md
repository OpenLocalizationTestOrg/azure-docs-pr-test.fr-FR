---
title: "accès à l’application de service aaaSelf et une administration déléguée avec Azure Active Directory | Documents Microsoft"
description: "Cet article décrit comment accéder aux applications en libre-service tooenable et la gestion déléguée avec Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 448a7fe8-a162-475e-9ba2-2e3ab59302bc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: asmalser
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 90bec3bd71796f22a782929b028db0d18c3aa1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-application-access-and-delegated-management-with-azure-active-directory"></a>Accès à l’application en libre-service et gestion déléguée avec Azure Active Directory
L’activation des fonctionnalités de libre-service pour les utilisateurs finaux est un scénario courant pour l’informatique d’entreprise. Un grand nombre d’utilisateurs, un grand nombre d’applications et de personne hello best-informed toomake accès accorder décisions ne peuvent pas être administrateur d’annuaire hello. Hello souvent meilleures toodecide de personnes qui peut accéder à une application est un responsable d’équipe ou un autre administrateur délégué. Toutefois, il est hello qui utilise l’application hello, hello utilisateur et sait qu’ils ont besoin toobe les toodo en mesure de leur travail.

> [!IMPORTANT]
> Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article. 

L’accès à l’application en libre-service est une fonctionnalité [Azure Active Directory Premium](https://azure.microsoft.com/trial/get-started-active-directory/), disponible avec les licences P1 et P2, qui permet aux administrateurs d’annuaire d’effectuer ce qui suit :

* Activer l’accès aux utilisateurs toorequest tooapplications à l’aide d’un « obtenir d’autres applications » vignette Bonjour [panneau d’accès Azure AD](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)
* Déterminer quels utilisateurs peuvent demander l’accès
* Définir ou non une approbation est requise pour l’application de tooan utilisateurs toobe tooself en mesure de l’attribution d’accès
* Jeu qui doit approuver les demandes de hello et gérer l’accès pour chaque application

Aujourd'hui cette fonctionnalité est prise en charge pour toutes les applications déjà intégrées et personnalisées qui prennent en charge fédéré ou mot de passe de session unique Bonjour [Galerie d’applications Azure Active Directory](https://azure.microsoft.com/marketplace/active-directory/all/), y compris les applications telles que Salesforce, Dropbox, Google Apps et bien plus encore.
Cet article explique comment :

* Configuration de l’accès des applications en libre-service pour les utilisateurs finaux, notamment la configuration d’un workflow d’approbation facultatif 
* Déléguer la gestion de l’accès aux personnes plus appropriés de toohello des applications spécifiques dans votre organisation et activer les demandes d’accès accès panneau tooapprove toouse hello Azure AD, attribuer directement accès aux utilisateurs de tooselected ou (en option) informations d’identification pour l’accès à l’application lorsque le mot de passe de session unique est configuré

## <a name="configuring-self-service-application-access"></a>Configuration de l’accès aux applications en libre-service
accès à l’application automatique tooenable et configuré les applications qui peuvent être ajoutées ou demandées par vos utilisateurs finaux, suivent ces instructions.

1. L’authentification à hello [portail Azure classic](https://manage.windowsazure.com/).

2.   Sous hello **Active Directory** section, sélectionnez votre annuaire, puis sélectionnez hello **Applications** onglet. 

3. Sélectionnez hello **ajouter** bouton et utilisez hello galerie option tooselect et ajouter une application.

4. Une fois que votre application a été ajoutée, vous obtenez la page de démarrage rapide de l’application hello. Cliquez sur **configurer l’authentification unique sur**hello souhaitée seul mode d’authentification et sélectionnez Enregistrer la configuration de hello. 

5. Ensuite, sélectionnez hello **configurer** application toothis onglet tooenable utilisateurs toorequest access à partir du volet d’accès hello Azure AD, définissez **autoriser l’accès des applications en libre-service** trop**Oui**.
  
  ![][1]

6. toooptionally configurer un workflow d’approbation pour les demandes d’accès, définissez **exiger l’approbation avant d’accorder l’accès** trop**Oui**. Ensuite, un ou plusieurs approbateurs peuvent être sélectionnées à l’aide de hello **approbateurs** bouton.

  Un approbateur peut être n’importe quel utilisateur dans l’organisation hello avec un compte Azure AD et peut être responsable de l’approvisionnement de comptes, Gestionnaire de licences, ou tout autre processus d’entreprise nécessite de votre organisation avant d’accorder l’accès tooan application. Hello approbateur peut même être propriétaire du groupe hello d’un ou plusieurs des groupes de comptes partagés et peut affecter tooone d’utilisateurs hello de ces toogive groupes les accèdent via un compte partagé. 

  Si aucune approbation n’est requise, les utilisateurs obtiennent instantanément volet d’accès hello application tootheir ajouté Azure AD. Si l’application hello a été définie pour [configuration automatique d’utilisateurs](active-directory-saas-app-provisioning.md), ou a été configuré [le mode « géré par l’utilisateur » le mot de passe SSO](active-directory-appssoaccess-whatis.md#password-based-single-sign-on), utilisateur de hello doit avoir déjà un utilisateur de compte et de connaître le mot de passe hello.

7. Si l’application hello a été configuré toouse mot de passe authentification unique, puis une option pour autoriser les approbateurs hello informations d’identification de l’authentification unique de hello tooset au nom de chaque utilisateur est également disponible. Pour plus d’informations, consultez la section de hello sur [accès gestion déléguée](#delegated-application-access-management).

8. Enfin, hello **groupe pour les utilisateurs Self-Assigned** affiche hello nom du groupe de hello est utilisé toostore hello utilisateurs ont été accordées ou affectés accès toohello application. approbateur de l’accès Hello devient propriétaire de hello de ce groupe. Si le nom du groupe hello indiqué n’existe pas, il est créé automatiquement. Si vous le souhaitez nom du groupe hello peut être défini toohello les nom d’un groupe existant.

9. configuration de hello toosave, cliquez sur **enregistrer** bas hello écran hello. Désormais, les utilisateurs peuvent toorequest accès toothis application à partir du volet d’accès hello.

10. tootry hello l’utilisateur final, l’authentification sur le volet d’accès Azure AD de votre organisation à https://myapps.microsoft.com, de préférence à l’aide d’un autre compte qui n’est pas un approbateur de l’application. 

11. Sous hello **Applications** , cliquez sur hello **obtenir d’autres applications** vignette. Cette vignette affiche une galerie de toutes les applications hello qui ont été activées pour l’accès des applications en libre-service dans hello répertoire, avec toosearch de capacité hello et filtrer par catégorie d’application sur hello gauche. 

12. En cliquant sur une application démarre, processus de demande de hello. Si aucun processus d’approbation n’est requise, puis application hello immédiatement figurera sous hello **Applications** onglet après une courte confirmation. Si une approbation est requise, vous verrez une boîte de dialogue indiquant cela et un e-mail est envoyé toohello approbateurs. Vous devez être connecté à hello volet d’accès comme un toosee non-approbateur ce processus de demande.

13. messagerie de Hello dirige hello approbateur toosign dans le volet d’accès Azure AD hello et approuver la demande de hello. Une fois hello demande est approuvée (et des processus spéciaux que vous définissez ont été effectuées par l’approbateur de hello), hello peut voir hello application apparaissent sous leur **Applications** onglet où ils peuvent vous connectez.

## <a name="delegated-application-access-management"></a>Gestion de l’accès à l’application déléguée
Un approbateur de l’accès d’application peut être n’importe quel utilisateur de votre organisation qui est hello plus approprié personne tooapprove ou refuser l’accès toohello l’application en question. Cet utilisateur peut être responsable de l’approvisionnement de comptes, Gestionnaire de licences, ou tout autre processus d’entreprise nécessite de votre organisation avant d’accorder l’accès tooan application.

Lors de la configuration de l’accès des applications en libre-service décrites ci-dessus, les affecté application approbateurs consultez supplémentaire **gérer les Applications** vignette dans le volet d’accès hello Azure AD, qui les affiche les applications qu’ils sont Hello accès administrateur. Un clic sur une application permet d’afficher un écran avec plusieurs options.

![][2]

### <a name="approve-requests"></a>Approuver des demandes
Hello **approuver les demandes** vignette permet d’approbateurs toosee en attente d’application spécifique toothat approbations et onglet Approbations de redirections toohello où hello demande peut être confirmée ou refusée. approbateur de Hello reçoit également les e-mails automatiques chaque fois qu’une demande est créée en sollicitant le toodo.

### <a name="add-users"></a>Ajouter des utilisateurs
Hello **ajouter des utilisateurs** vignette permet d’approbateurs toodirectly grant sélectionné aux utilisateurs accès toohello application. Lorsque vous cliquez sur cette vignette, approbateur de hello voit qu'une boîte de dialogue permet de les tooview et rechercher des utilisateurs dans leur annuaire. Ajout d’un résultats de l’utilisateur dans l’application hello est affichée dans les panneaux d’accès de ces utilisateurs Azure AD ou Office 365. Si n’importe quel processus de configuration manuelle de l’utilisateur est nécessaire à l’application hello avant que l’utilisateur de hello est en mesure de toosign dans, puis approbateur de hello doit effectuer ce processus avant d’attribuer l’accès.  

### <a name="manage-users"></a>Gérer les utilisateurs
Hello **gérer les utilisateurs** vignette permet la mise à jour de toodirectly approbateurs ou de supprimer les utilisateurs qui ont accès toohello application. 

### <a name="configure-password-sso-credentials-if-applicable"></a>Configurer les informations d’identification avec authentification unique par mot de passe (le cas échéant)
Hello **configurer** vignette apparaît uniquement si application hello a été configurée par hello informatique administrateur toouse mot de passe de session unique, et administrateur de hello disposent d’informations d’identification du mot de passe SSO hello capacité tooset un approbateur de hello comme décrit précédemment. Lorsque sélectionné, hello approbateur est présenté avec plusieurs options pour comment les informations d’identification hello sont propagés tooassigned utilisateurs :

![][3]

* **Les utilisateurs se connectent avec leurs propres mots de passe** – dans ce mode, les utilisateurs de hello affecté connaissent les leurs noms d’utilisateur et les mots de passe pour l’application hello et sont invités à tooenter les lors de leur première demande de connexion toohello. Hello scénario correspond cas de l’authentification unique de mot de passe toohello où hello [utilisateurs gérer les informations d’identification](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).
* **Les utilisateurs sont automatiquement connectés à l’aide des comptes distincts pour gérer les** – dans ce mode, les utilisateurs de hello affecté ne sont pas requis tooenter ou connaître leurs informations d’identification spécifiques de l’application lors de la signature dans l’application hello. Au lieu de cela, approbateur de hello définit des informations d’identification de hello pour chaque utilisateur après avoir affecté les accès à l’aide de hello **ajouter un utilisateur** vignette. Lorsque l’utilisateur de hello clique sur application hello dans leur volet d’accès ou d’Office 365, ils sont automatiquement connectés à l’aide des informations d’identification hello définies par l’approbateur de hello. Hello scénario correspond cas de l’authentification unique de mot de passe toohello où hello [administrateurs de gérer les informations d’identification](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).
* **Les utilisateurs sont automatiquement connectés à l’aide d’un seul compte gérer** -est un cas particulier, ce cas toouse appropriée lorsque tous les utilisateurs affectés doivent toobe accordé l’accès à l’aide d’un compte partagé unique. Hello principaux cas d’utilisation de cette fonctionnalité est avec des applications de médias sociaux, où une organisation dispose d’un compte de « company » unique et plusieurs utilisateurs doivent toomake mises à jour toothat compte. Hello scénario correspond aussi cas de l’authentification unique de mot de passe toohello où hello [administrateurs de gérer les informations d’identification](active-directory-appssoaccess-whatis.md#password-based-single-sign-on). Toutefois, après avoir sélectionné cette option, hello approbateur sera le nom d’utilisateur de tooenter demandées hello et de mot de passe de compte partagé unique de hello. Une fois terminé, tous les utilisateurs affectés sont signés à l’aide de ce compte lorsque vous cliquez sur l’application hello dans les panneaux d’accès Azure AD ou d’Office 365.

## <a name="additional-resources"></a>Ressources supplémentaires
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)

<!--Image references-->
[1]: ./media/active-directory-self-service-application-access/ssaa_admin.PNG
[2]: ./media/active-directory-self-service-application-access/ssaa_ap_manage_app.PNG
[3]: ./media/active-directory-self-service-application-access/ssaa_ap_manage_app_config.PNG
