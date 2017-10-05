---
title: "Gestion des comptes d’utilisateur dans Gestion des API Azure | Microsoft Docs"
description: "Apprenez à créer ou à inviter des utilisateurs dans Gestion des API Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 078abfa5-1e4f-4c9d-b9c7-a172bd19c1a2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: d3a50f6d22cbf1797f580078bc0d2cc9cefe5064
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-user-accounts-in-azure-api-management"></a>Gestion des comptes d’utilisateur dans Gestion des API Azure
Dans Gestion des API Azure, les développeurs sont les utilisateurs des API que vous exposez via Gestion des API. Ce guide vous montre comment créer et inviter des développeurs à utiliser les API et les produits que vous mettez à leur disposition dans votre instance Gestion des API. Pour plus d’informations sur la gestion des comptes d’utilisateur par programme, consultez la documentation [Entité utilisateur](https://msdn.microsoft.com/library/azure/dn776330.aspx) dans la référence [API REST de gestion](https://msdn.microsoft.com/library/azure/dn776326.aspx).

## <a name="create-developer"> </a>Création d’un développeur
Pour créer un développeur, cliquez sur **Portail des éditeurs** dans le portail Azure de votre service Gestion des API. Vous accédez au portail des éditeurs Gestion des API. Si vous n’avez pas encore créé une instance de service Gestion des API, consultez la page de [création d’une instance de service Gestion des API][Create an API Management service instance] dans le didacticiel de [prise en main de Gestion des API Azure][Get started with Azure API Management].

![Portail des éditeurs][api-management-management-console]

Cliquez sur **Utilisateurs** dans le menu **Gestion des API** à gauche, puis sur **Ajouter un utilisateur**.

![Create developer][api-management-create-developer]

Entrez l’**adresse électronique**, le **mot de passe** et le **nom** du nouveau développeur et cliquez sur **Enregistrer**.

![Create developer][api-management-add-new-user]

Par défaut, les comptes de développeurs nouvellement créés sont **actifs**. Ils sont associés au groupe **Développeurs**.

![New developer][api-management-new-developer]

Les comptes de développeurs dont l'état est **actif** peuvent être utilisés pour accéder à toutes les API auxquelles ils sont abonnés. Pour associer les développeurs nouvellement créés à d’autres groupes, consultez la rubrique [Association de groupes à des développeurs][How to associate groups with developers].

## <a name="invite-developer"> </a>Invitation d’un développeur
Pour inviter un développeur, cliquez sur **Utilisateurs** dans le menu **Gestion des API** à gauche, puis sur **Inviter un utilisateur**.

![Invite developer][api-management-invite-developer]

Entrez le nom et l'adresse électronique du développeur, puis cliquez sur **Inviter**.

![Invite developer][api-management-invite-developer-window]

Un message de confirmation s’affiche, mais le développeur qui vient d’être invité n’apparaît pas dans la liste tant qu’il n’a pas accepté l’invitation. 

![Invite confirmation][api-management-invite-developer-confirmation]

Quand un développeur est invité, un message lui est envoyé. Ce message est généré à partir d'un modèle. Il est personnalisable. Pour plus d’informations, consultez la page [Configuration des modèles de courrier électronique][Configure email templates].

Une fois l'invitation acceptée, le compte est activé.

## <a name="block-developer"> </a> Désactivation ou réactivation d’un compte de développeur
Par défaut, les comptes de développeur nouvellement créés ou invités sont **actifs**. Pour désactiver un compte de développeur, cliquez sur **Bloquer**. Pour réactiver un compte de développeur bloqué, cliquez sur **Activer**. Les comptes de développeurs bloqués ne peuvent pas accéder au portail des développeurs, ni appeler les API. Pour supprimer un compte d’utilisateur, cliquez sur **Supprimer**.

![Block developer][api-management-new-developer]

## <a name="reset-a-user-password"></a>Réinitialiser le mot de passe d’un utilisateur
Pour réinitialiser le mot de passe d’un compte d’utilisateur, cliquez sur le nom du compte.

![Réinitialiser le mot de passe][api-management-view-developer]

Cliquez sur **Réinitialiser le mot de passe** pour envoyer un lien à l’utilisateur lui permettant de réinitialiser son mot de passe.

![Réinitialiser le mot de passe][api-management-reset-password]

Pour utiliser les comptes d’utilisateur par programme, consultez la documentation [Entité utilisateur](https://msdn.microsoft.com/library/azure/dn776330.aspx) dans la référence [API REST de gestion](https://msdn.microsoft.com/library/azure/dn776326.aspx). Pour réinitialiser le mot de passe d’un compte d’utilisateur sur une valeur spécifique, vous pouvez utiliser l’opération [Mettre à jour un utilisateur](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) et spécifier le mot de passe nécessaire.

## <a name="pending-verification"></a>Vérification en attente
![Vérification en attente][api-management-pending-verification]

## <a name="next-steps"> </a>Étapes suivantes
Une fois le compte de développeur créé, vous pouvez l'associer à des rôles et l'abonner à des produits et des API. Pour plus d’informations, consultez la page [Création et utilisation de groupes][How to create and use groups].

[api-management-management-console]: ./media/api-management-howto-create-or-invite-developers/api-management-management-console.png
[api-management-add-new-user]: ./media/api-management-howto-create-or-invite-developers/api-management-add-new-user.png
[api-management-create-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-create-developer.png
[api-management-invite-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer.png
[api-management-new-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-new-developer.png
[api-management-invite-developer-window]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-window.png
[api-management-invite-developer-confirmation]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-confirmation.png
[api-management-pending-verification]: ./media/api-management-howto-create-or-invite-developers/api-management-pending-verification.png
[api-management-view-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-view-developer.png
[api-management-reset-password]: ./media/api-management-howto-create-or-invite-developers/api-management-reset-password.png


[Create a new developer]: #create-developer
[Invite a developer]: #invite-developer
[Deactivate or reactivate a developer account]: #block-developer
[Next steps]: #next-steps
[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
