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
# <a name="how-toomanage-user-accounts-in-azure-api-management"></a><span data-ttu-id="d3236-103">Le mode toomanage utilisateur comptes dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="d3236-103">How toomanage user accounts in Azure API Management</span></span>
<span data-ttu-id="d3236-104">Dans Gestion des API, les développeurs sont les utilisateurs hello Hello API qui vous exposez à l’aide de la gestion des API.</span><span class="sxs-lookup"><span data-stu-id="d3236-104">In API Management, developers are hello users of hello APIs that you expose using API Management.</span></span> <span data-ttu-id="d3236-105">Ce guide montre toohow toocreate et inviter les développeurs toouse hello API et les produits que vous apportez toothem disponible avec votre instance de la gestion des API.</span><span class="sxs-lookup"><span data-stu-id="d3236-105">This guide shows toohow toocreate and invite developers toouse hello APIs and products that you make available toothem with your API Management instance.</span></span> <span data-ttu-id="d3236-106">Pour plus d’informations sur la gestion des comptes d’utilisateur par programme, consultez hello [entité utilisateur](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation Bonjour [REST de gestion des API](https://msdn.microsoft.com/library/azure/dn776326.aspx) référence.</span><span class="sxs-lookup"><span data-stu-id="d3236-106">For information on managing user accounts programmatically, see hello [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in hello [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span>

## <span data-ttu-id="d3236-107"><a name="create-developer"></a>Création d’un développeur</span><span class="sxs-lookup"><span data-stu-id="d3236-107"><a name="create-developer"> </a>Create a new developer</span></span>
<span data-ttu-id="d3236-108">toocreate un développeur de nouveau, cliquez sur **portail de publication** Bonjour portail Azure pour votre service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="d3236-108">toocreate a new developer, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="d3236-109">Cela vous prend un portail de publication de gestion des API toohello.</span><span class="sxs-lookup"><span data-stu-id="d3236-109">This takes you toohello API Management publisher portal.</span></span> <span data-ttu-id="d3236-110">Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main Azure API Management] [ Get started with Azure API Management] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="d3236-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Portail des éditeurs][api-management-management-console]

<span data-ttu-id="d3236-112">Cliquez sur **utilisateurs** de hello **gestion des API** menu sur hello gauche, puis cliquez sur **Ajouter utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="d3236-112">Click **Users** from hello **API Management** menu on hello left, and then click **add user**.</span></span>

![Create developer][api-management-create-developer]

<span data-ttu-id="d3236-114">Entrez hello **messagerie**, **mot de passe**, et **nom** pour le développement de nouveau hello et cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d3236-114">Enter hello **Email**, **Password**, and **Name** for hello new developer and click **Save**.</span></span>

![Create developer][api-management-add-new-user]

<span data-ttu-id="d3236-116">Par défaut, les comptes de développeur nouvellement créé sont **Active**et associés hello **les développeurs** groupe.</span><span class="sxs-lookup"><span data-stu-id="d3236-116">By default, newly created developer accounts are **Active**, and associated with hello **Developers** group.</span></span>

![New developer][api-management-new-developer]

<span data-ttu-id="d3236-118">Comptes de développeur qui se trouvent dans un **active** état peut être utilisé tooaccess toutes les API hello pour lesquels ils disposent des abonnements.</span><span class="sxs-lookup"><span data-stu-id="d3236-118">Developer accounts that are in an **active** state can be used tooaccess all of hello APIs for which they have subscriptions.</span></span> <span data-ttu-id="d3236-119">développeur de hello nouvellement créé tooassociate par d’autres groupes, consultez [comment les groupes avec les développeurs tooassociate][How tooassociate groups with developers].</span><span class="sxs-lookup"><span data-stu-id="d3236-119">tooassociate hello newly created developer with additional groups, see [How tooassociate groups with developers][How tooassociate groups with developers].</span></span>

## <span data-ttu-id="d3236-120"><a name="invite-developer"></a>Invitation d’un développeur</span><span class="sxs-lookup"><span data-stu-id="d3236-120"><a name="invite-developer"> </a>Invite a developer</span></span>
<span data-ttu-id="d3236-121">tooinvite un développeur, cliquez sur **utilisateurs** de hello **gestion des API** menu sur hello gauche, puis cliquez sur **inviter l’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="d3236-121">tooinvite a developer, click **Users** from hello **API Management** menu on hello left, and then click **Invite User**.</span></span>

![Invite developer][api-management-invite-developer]

<span data-ttu-id="d3236-123">Entrez hello nom et adresse de messagerie du développeur de hello, puis cliquez sur **inviter**.</span><span class="sxs-lookup"><span data-stu-id="d3236-123">Enter hello name and email address of hello developer, and click **Invite**.</span></span>

![Invite developer][api-management-invite-developer-window]

<span data-ttu-id="d3236-125">Un message de confirmation s’affiche, mais le développeur de hello qui vient d’être invité n’apparaît pas dans la liste hello jusqu'à ce qu’une fois qu’ils acceptent d’invitation hello.</span><span class="sxs-lookup"><span data-stu-id="d3236-125">A confirmation message is displayed, but hello newly invited developer does not appear in hello list until after they accept hello invitation.</span></span> 

![Invite confirmation][api-management-invite-developer-confirmation]

<span data-ttu-id="d3236-127">Lorsqu’un développeur est invité, un e-mail est envoyé toohello développeur.</span><span class="sxs-lookup"><span data-stu-id="d3236-127">When a developer is invited, an email is sent toohello developer.</span></span> <span data-ttu-id="d3236-128">Ce message est généré à partir d'un modèle. Il est personnalisable.</span><span class="sxs-lookup"><span data-stu-id="d3236-128">This email is generated using a template and is customizable.</span></span> <span data-ttu-id="d3236-129">Pour plus d’informations, consultez la page [Configuration des modèles de courrier électronique][Configure email templates].</span><span class="sxs-lookup"><span data-stu-id="d3236-129">For more information, see [Configure email templates][Configure email templates].</span></span>

<span data-ttu-id="d3236-130">Une fois hello invitation est acceptée, le compte de hello devient actif.</span><span class="sxs-lookup"><span data-stu-id="d3236-130">Once hello invitation is accepted, hello account becomes active.</span></span>

## <span data-ttu-id="d3236-131"><a name="block-developer"></a> Désactivation ou réactivation d’un compte de développeur</span><span class="sxs-lookup"><span data-stu-id="d3236-131"><a name="block-developer"> </a> Deactivate or reactivate a developer account</span></span>
<span data-ttu-id="d3236-132">Par défaut, les comptes de développeur nouvellement créés ou invités sont **actifs**.</span><span class="sxs-lookup"><span data-stu-id="d3236-132">By default, newly created or invited developer accounts are **Active**.</span></span> <span data-ttu-id="d3236-133">toodeactivate un compte de développeur, cliquez sur **bloc**.</span><span class="sxs-lookup"><span data-stu-id="d3236-133">toodeactivate a developer account, click **Block**.</span></span> <span data-ttu-id="d3236-134">tooreactivate un compte de développeur bloqué, cliquez sur **activer**.</span><span class="sxs-lookup"><span data-stu-id="d3236-134">tooreactivate a blocked developer account, click **Activate**.</span></span> <span data-ttu-id="d3236-135">Un compte de développeur bloqués ne permettre pas accéder au portail des développeurs hello ni appeler des API.</span><span class="sxs-lookup"><span data-stu-id="d3236-135">A blocked developer account can not access hello developer portal or call any APIs.</span></span> <span data-ttu-id="d3236-136">toodelete un compte d’utilisateur, cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="d3236-136">toodelete a user account, click **Delete**.</span></span>

![Block developer][api-management-new-developer]

## <a name="reset-a-user-password"></a><span data-ttu-id="d3236-138">Réinitialiser le mot de passe d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="d3236-138">Reset a user password</span></span>
<span data-ttu-id="d3236-139">mot de passe tooreset hello pour un compte d’utilisateur, cliquez sur nom hello du compte de hello.</span><span class="sxs-lookup"><span data-stu-id="d3236-139">tooreset hello password for a user account, click hello name of hello account.</span></span>

![Réinitialiser le mot de passe][api-management-view-developer]

<span data-ttu-id="d3236-141">Cliquez sur **réinitialisation de mot de passe** toosend un tooreset d’utilisateur lien toohello leur mot de passe.</span><span class="sxs-lookup"><span data-stu-id="d3236-141">Click **Reset password** toosend a link toohello user tooreset their password.</span></span>

![Réinitialiser le mot de passe][api-management-reset-password]

<span data-ttu-id="d3236-143">travail tooprogrammatically avec les comptes d’utilisateur, consultez hello [entité utilisateur](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation Bonjour [REST de gestion des API](https://msdn.microsoft.com/library/azure/dn776326.aspx) référence.</span><span class="sxs-lookup"><span data-stu-id="d3236-143">tooprogrammatically work with user accounts, see hello [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in hello [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span> <span data-ttu-id="d3236-144">tooreset une valeur tooa spécifique mot de passe de compte utilisateur, vous pouvez utiliser hello [mettre à jour un utilisateur](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) opération et spécifiez le mot de passe souhaité hello.</span><span class="sxs-lookup"><span data-stu-id="d3236-144">tooreset a user account password tooa specific value, you can use hello [Update a user](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operation and specify hello desired password.</span></span>

## <a name="pending-verification"></a><span data-ttu-id="d3236-145">Vérification en attente</span><span class="sxs-lookup"><span data-stu-id="d3236-145">Pending verification</span></span>
![Vérification en attente][api-management-pending-verification]

## <span data-ttu-id="d3236-147"><a name="next-steps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d3236-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="d3236-148">Après la création d’un compte de développeur, vous pouvez associer à des rôles et abonner tooproducts et API.</span><span class="sxs-lookup"><span data-stu-id="d3236-148">Once a developer account is created, you can associate it with roles and subscribe it tooproducts and APIs.</span></span> <span data-ttu-id="d3236-149">Pour plus d’informations, consultez [comment toocreate et l’utilisation de groupes][How toocreate and use groups].</span><span class="sxs-lookup"><span data-stu-id="d3236-149">For more information, see [How toocreate and use groups][How toocreate and use groups].</span></span>

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
