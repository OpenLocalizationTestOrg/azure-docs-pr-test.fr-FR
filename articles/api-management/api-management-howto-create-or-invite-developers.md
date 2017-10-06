---
title: "gérer les comptes d’utilisateur de gestion des API Azure aaaHow | Documents Microsoft"
description: "Découvrez comment toocreate ou inviter les utilisateurs dans la gestion des API Azure"
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
ms.openlocfilehash: 3966f4454e29621d7c615beefee352ec91b48b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-user-accounts-in-azure-api-management"></a>Le mode toomanage utilisateur comptes dans Gestion des API Azure
Dans Gestion des API, les développeurs sont les utilisateurs hello Hello API qui vous exposez à l’aide de la gestion des API. Ce guide montre toohow toocreate et inviter les développeurs toouse hello API et les produits que vous apportez toothem disponible avec votre instance de la gestion des API. Pour plus d’informations sur la gestion des comptes d’utilisateur par programme, consultez hello [entité utilisateur](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation Bonjour [REST de gestion des API](https://msdn.microsoft.com/library/azure/dn776326.aspx) référence.

## <a name="create-developer"></a>Création d’un développeur
toocreate un développeur de nouveau, cliquez sur **portail de publication** Bonjour portail Azure pour votre service de gestion des API. Cela vous prend un portail de publication de gestion des API toohello. Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main Azure API Management] [ Get started with Azure API Management] didacticiel.

![Portail des éditeurs][api-management-management-console]

Cliquez sur **utilisateurs** de hello **gestion des API** menu sur hello gauche, puis cliquez sur **Ajouter utilisateur**.

![Create developer][api-management-create-developer]

Entrez hello **messagerie**, **mot de passe**, et **nom** pour le développement de nouveau hello et cliquez sur **enregistrer**.

![Create developer][api-management-add-new-user]

Par défaut, les comptes de développeur nouvellement créé sont **Active**et associés hello **les développeurs** groupe.

![New developer][api-management-new-developer]

Comptes de développeur qui se trouvent dans un **active** état peut être utilisé tooaccess toutes les API hello pour lesquels ils disposent des abonnements. développeur de hello nouvellement créé tooassociate par d’autres groupes, consultez [comment les groupes avec les développeurs tooassociate][How tooassociate groups with developers].

## <a name="invite-developer"></a>Invitation d’un développeur
tooinvite un développeur, cliquez sur **utilisateurs** de hello **gestion des API** menu sur hello gauche, puis cliquez sur **inviter l’utilisateur**.

![Invite developer][api-management-invite-developer]

Entrez hello nom et adresse de messagerie du développeur de hello, puis cliquez sur **inviter**.

![Invite developer][api-management-invite-developer-window]

Un message de confirmation s’affiche, mais le développeur de hello qui vient d’être invité n’apparaît pas dans la liste hello jusqu'à ce qu’une fois qu’ils acceptent d’invitation hello. 

![Invite confirmation][api-management-invite-developer-confirmation]

Lorsqu’un développeur est invité, un e-mail est envoyé toohello développeur. Ce message est généré à partir d'un modèle. Il est personnalisable. Pour plus d’informations, consultez la page [Configuration des modèles de courrier électronique][Configure email templates].

Une fois hello invitation est acceptée, le compte de hello devient actif.

## <a name="block-developer"></a> Désactivation ou réactivation d’un compte de développeur
Par défaut, les comptes de développeur nouvellement créés ou invités sont **actifs**. toodeactivate un compte de développeur, cliquez sur **bloc**. tooreactivate un compte de développeur bloqué, cliquez sur **activer**. Un compte de développeur bloqués ne permettre pas accéder au portail des développeurs hello ni appeler des API. toodelete un compte d’utilisateur, cliquez sur **supprimer**.

![Block developer][api-management-new-developer]

## <a name="reset-a-user-password"></a>Réinitialiser le mot de passe d’un utilisateur
mot de passe tooreset hello pour un compte d’utilisateur, cliquez sur nom hello du compte de hello.

![Réinitialiser le mot de passe][api-management-view-developer]

Cliquez sur **réinitialisation de mot de passe** toosend un tooreset d’utilisateur lien toohello leur mot de passe.

![Réinitialiser le mot de passe][api-management-reset-password]

travail tooprogrammatically avec les comptes d’utilisateur, consultez hello [entité utilisateur](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation Bonjour [REST de gestion des API](https://msdn.microsoft.com/library/azure/dn776326.aspx) référence. tooreset une valeur tooa spécifique mot de passe de compte utilisateur, vous pouvez utiliser hello [mettre à jour un utilisateur](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) opération et spécifiez le mot de passe souhaité hello.

## <a name="pending-verification"></a>Vérification en attente
![Vérification en attente][api-management-pending-verification]

## <a name="next-steps"></a>Étapes suivantes
Après la création d’un compte de développeur, vous pouvez associer à des rôles et abonner tooproducts et API. Pour plus d’informations, consultez [comment toocreate et l’utilisation de groupes][How toocreate and use groups].

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
[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
