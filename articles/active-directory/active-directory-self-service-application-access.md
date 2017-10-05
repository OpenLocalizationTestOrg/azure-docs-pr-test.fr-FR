---
title: "Accès à l’application en libre-service et gestion déléguée avec Azure Active Directory | Microsoft Docs"
description: "Cet article explique comment octroyer l’accès en libre-service à l’application et la gestion déléguée avec Azure Active Directory"
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
ms.openlocfilehash: 7872d5229cdc053bfb9dc8ddba01785b0f8e5a9a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="self-service-application-access-and-delegated-management-with-azure-active-directory"></a>Accès à l’application en libre-service et gestion déléguée avec Azure Active Directory
L’activation des fonctionnalités de libre-service pour les utilisateurs finaux est un scénario courant pour l’informatique d’entreprise. Un grand nombre d’utilisateurs, d’applications, et la personne la mieux informée pour prendre des décisions d’autorisation d’accès n’est pas nécessairement l’administrateur de l’annuaire. Souvent, la personne la mieux à même de décider de qui peut accéder à une application est le responsable d’équipe ou un autre administrateur délégué. Toutefois, c’est l’utilisateur qui se sert de l’application et qui sait ce dont il a besoin pour faire le travail.

> [!IMPORTANT]
> Microsoft recommande de gérer Azure AD à l’aide du [Centre d’administration Azure AD](https://aad.portal.azure.com) dans le portail Azure au lieu d’utiliser le portail Azure classique référencé dans cet article. 

L’accès à l’application en libre-service est une fonctionnalité [Azure Active Directory Premium](https://azure.microsoft.com/trial/get-started-active-directory/), disponible avec les licences P1 et P2, qui permet aux administrateurs d’annuaire d’effectuer ce qui suit :

* Donner aux utilisateurs la possibilité de demander l’accès aux applications à l’aide d’une vignette « Obtenir d’autres applications » dans le [Panneau d’accès Azure AD](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)
* Déterminer quels utilisateurs peuvent demander l’accès
* Définir si une approbation est obligatoire ou non pour que les utilisateurs puissent s’accorder à eux-mêmes l’accès à une application
* Définir qui doit approuver les requêtes et gérer l’accès à chaque application

Aujourd’hui cette fonctionnalité est prise en charge pour toutes les applications préintégrées et personnalisées qui prennent en charge les connexions fédérées ou basées sur un mot de passe de session unique dans la [Galerie d’applications Azure Active Directory](https://azure.microsoft.com/marketplace/active-directory/all/), et notamment les applications telles que Salesforce, échange, Google Apps, entre autres.
Cet article explique comment :

* Configuration de l’accès des applications en libre-service pour les utilisateurs finaux, notamment la configuration d’un workflow d’approbation facultatif 
* Déléguer la gestion de l’accès à des applications spécifiques pour les personnes de votre organisation les plus concernées et leur permettre d’utiliser le volet d’accès Azure AD pour approuver les demandes d’accès, attribuer directement l’accès aux utilisateurs sélectionnés ou (éventuellement) les informations d’identification pour l’accès à l’application lorsque l’authentification par mot de passe est configurée

## <a name="configuring-self-service-application-access"></a>Configuration de l’accès aux applications en libre-service
Pour activer l’accès aux applications en libre-service et configurer les applications qui peuvent être ajoutées ou demandées par vos utilisateurs finaux, suivez ces instructions.

1. Connectez-vous au [Portail Azure Classic](https://manage.windowsazure.com/).

2.   Dans la section **Active Directory**, sélectionnez votre annuaire, puis sélectionnez l’onglet **Applications**. 

3. Sélectionnez le bouton **Ajouter** et utiliser l’option de galerie pour sélectionner et ajouter une application.

4. Une fois que votre application a été ajoutée, vous obtiendrez la page de démarrage rapide de l’application. Cliquez sur **Configurer l’authentification unique**, sélectionnez le mode d’authentification et enregistrez la configuration. 

5. Sélectionnez ensuite l’onglet **Configurer**. Pour permettre aux utilisateurs de demander l’accès à cette application depuis le panneau d’accès Azure AD, définissez **Autoriser l’accès à l’application en libre-service** sur **Oui**.
  
  ![][1]

6. Pour configurer éventuellement un workflow d’approbation pour les demandes d’accès, définissez **Exiger une approbation avant d’accorder l’accès** sur **Oui**. Puis un ou plusieurs approbateurs peuvent être sélectionnés à l’aide du bouton **Approbateurs** .

  Un approbateur peut être un utilisateur quelconque de l’organisation titulaire d’un compte Azure AD et peut être responsable de la configuration du compte, de l’octroi de licence ou d’un autre processus métier dont votre organisation a besoin avant d’accorder l’accès à une application. L’approbateur peut également être le propriétaire de groupe d’un ou de plusieurs groupes de comptes partagés et peut affecter les utilisateurs à l’un de ces groupes pour leur donner accès via un compte partagé. 

  Si aucune approbation n’est requise, les utilisateurs reçoivent instantanément l’application ajoutée à leur volet d’accès Azure AD. Si l’application a été configurée pour l’[Attribution automatique d'utilisateurs](active-directory-saas-app-provisioning.md) ou a été configurée sur le [mode authentification unique par mot de passe « gérée par l’utilisateur »](active-directory-appssoaccess-whatis.md#password-based-single-sign-on), l’utilisateur a déjà un compte d’utilisateur et connaît le mot de passe.

7. Si l’application a été configurée pour utiliser l’authentification unique par mot de passe, puis une option permettant à l’approbateur de définir les informations d’identification de l’authentification unique au nom de chaque utilisateur est également disponible. Pour plus d’informations, consultez la section concernant la [gestion d’accès délégué](#delegated-application-access-management).

8. Enfin, le **Groupe pour les utilisateurs auto-affectés** affiche le nom du groupe servant à stocker les utilisateurs qui se sont vu accorder ou affecter l’accès à l’application. L’approbateur d’accès devient le propriétaire de ce groupe. Si le nom du groupe indiqué n’existe pas, il est automatiquement créé. Le nom du groupe peut éventuellement être défini sur le nom d’un groupe existant.

9. Cliquez sur **Enregistrer** en bas de l’écran pour enregistrer la configuration. Désormais les utilisateurs peuvent demander l’accès à cette application depuis le volet d’accès.

10. Pour tester l’expérience utilisateur final, connectez-vous au volet d’accès Azure AD de votre organisation dans https://myapps.microsoft.com, de préférence à l’aide d’un autre compte, qui n’est pas un approbateur de l’application. 

11. Sous l’onglet **Applications**, cliquez sur la vignette **Obtenir plus d’applications**. Cette vignette affiche une galerie de l’ensemble des applications activées pour l’accès aux applications en libre-service dans le répertoire, avec la possibilité de rechercher et de filtrer par catégorie d’application sur la gauche. 

12. Un clic sur une application lance le processus de demande. Si aucun processus d’approbation n’est requis, l’application est ajoutée immédiatement sous l’onglet **Applications** après une brève confirmation. Si l’approbation est requise, vous voyez une boîte de dialogue l’indiquant et ce message électronique est envoyé aux approbateurs. Vous devez être connecté au volet d’accès avec un rôle autre que celui d’approbateur pour voir ce processus de demande.

13. Le courrier électronique demande à l’approbateur de se connecter au volet d’accès Azure AD et d’approuver la demande. Une fois la demande approuvée (et tous les processus spéciaux définis exécutés par l’approbateur), l’utilisateur voit alors l’application s’afficher sous l’onglet **Applications** , où ils peuvent se connecter.

## <a name="delegated-application-access-management"></a>Gestion de l’accès à l’application déléguée
L’approbateur de l’accès à l’application peut être n’importe quel utilisateur de votre organisation désigné comme étant la personne la plus à même d’accepter ou de refuser l’accès à l’application en question. Il peut être responsable de la configuration de compte, de l’octroi de licence ou d’un autre processus métier dont votre organisation a besoin avant d’accorder l’accès à une application.

Lorsque vous configurez l’accès aux applications en libre-service décrites ci-dessus, les approbateurs affectés à l’application voient une vignette **Gérer les applications** supplémentaire dans le volet d’accès Azure AD qui contient les applications dont ils sont gestionnaires d’accès. Un clic sur une application permet d’afficher un écran avec plusieurs options.

![][2]

### <a name="approve-requests"></a>Approuver des demandes
La vignette **Approuver les demandes** permet aux approbateurs d’afficher les approbations spécifiques à cette application en attente et est redirigée vers l’onglet Approbations où les demandes peuvent être confirmées ou refusées. À la création d’une requête, l’approbateur reçoit également les e-mails automatiques lui expliquant quoi faire.

### <a name="add-users"></a>Ajouter des utilisateurs
La vignette **Ajouter des utilisateurs** permet à vos approbateurs d’accorder directement l’accès à l’application à des utilisateurs sélectionnés. Lorsque vous cliquez sur cette vignette, l’approbateur voit s’afficher une boîte de dialogue et rechercher des utilisateurs dans leur annuaire. Ajout de résultats d’un utilisateur dans l’application présentée dans les panneaux d’accès Azure AD ou Office 365 de ces utilisateurs. Si un des processus de configuration manuelle de l’utilisateur est nécessaire à l’application avant que l’utilisateur soit en mesure de se connecter, l’approbateur doit effectuer cette opération avant d’attribuer l’accès.  

### <a name="manage-users"></a>Gérer les utilisateurs
La vignette **Gérer les utilisateurs** permet aux approbateurs de directement mettre à jour ou supprimer les utilisateurs ayant un accès direct à l’application. 

### <a name="configure-password-sso-credentials-if-applicable"></a>Configurer les informations d’identification avec authentification unique par mot de passe (le cas échéant)
La vignette **Configurer** apparaît uniquement si l’application a été configurée par l’administrateur informatique pour utiliser l’authentification unique par mot de passe et si l’administrateur a accordé à l’approbateur la possibilité de définir les informations d’identification d’authentification par mot de passe comme décrit précédemment. Lorsqu’il est sélectionné, l’approbateur est présenté avec plusieurs options de propagation des informations d’identification aux utilisateurs affectés :

![][3]

* **Les utilisateurs se connectent avec leurs propres mots de passe** : dans ce mode, les utilisateurs affectés connaissent le nom d’utilisateur et les mots de passe de l’application et sont invités à les saisir lors de leur première connexion à l’application. Ce scénario correspond aux cas d’authentification unique par mot de passe, dans lesquels [les utilisateurs gèrent les informations d’authentification](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).
* **Les utilisateurs sont automatiquement connectés lorsqu’ils utilisent des comptes séparés que je gère** : dans ce mode, les utilisateurs affectés ne sont pas tenus de saisir ou de connaître leurs informations d’identification spécifiques au moment de se connecter à l’application. Au lieu de cela, l’approbateur définit les informations d’identification pour chaque utilisateur après l’affectation d’accès à l’aide avec la vignette **Ajouter un utilisateur** . Lorsque l’utilisateur clique sur l’application dans le volet d’accès ou Office 365, il est automatiquement connecté à l’aide des informations d’identification définies par l’approbateur. Ce scénario correspond également au cas d’authentification unique par mot de passe dans lesquels ce sont [les administrateurs qui gèrent les informations d’identification](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).
* **Les utilisateurs sont automatiquement connectés lorsqu’ils utilisent un compte unique que je gère** : il s’agit d’un cas spécial, recommandé lorsque des utilisateurs affectés doivent se voir accorder un accès avec un compte partagé unique. Le cas d’utilisation le plus courant pour cette fonctionnalité concerne les applications de médias sociaux, où une organisation possède un compte « société » et où plusieurs utilisateurs doivent effectuer des mises à jour. Ce scénario correspond également au cas d’authentification unique par mot de passe dans lesquels ce sont [les administrateurs qui gèrent les informations d’identification](active-directory-appssoaccess-whatis.md#password-based-single-sign-on). Toutefois, après avoir sélectionné cette option, l’approbateur est invité à entrer le nom d’utilisateur et le mot de passe pour le compte partagé unique. Une fois l’opération terminée, tous les utilisateurs affectés sont connectés à l’aide de ce compte lorsque vous cliquez sur l’application sur leur volet d’accès Azure AD ou sur Office 365.

## <a name="additional-resources"></a>Ressources supplémentaires
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)

<!--Image references-->
[1]: ./media/active-directory-self-service-application-access/ssaa_admin.PNG
[2]: ./media/active-directory-self-service-application-access/ssaa_ap_manage_app.PNG
[3]: ./media/active-directory-self-service-application-access/ssaa_ap_manage_app_config.PNG
