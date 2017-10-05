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
# <a name="how-to-manage-user-accounts-in-azure-api-management"></a><span data-ttu-id="529ea-103">Gestion des comptes d’utilisateur dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="529ea-103">How to manage user accounts in Azure API Management</span></span>
<span data-ttu-id="529ea-104">Dans Gestion des API Azure, les développeurs sont les utilisateurs des API que vous exposez via Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="529ea-104">In API Management, developers are the users of the APIs that you expose using API Management.</span></span> <span data-ttu-id="529ea-105">Ce guide vous montre comment créer et inviter des développeurs à utiliser les API et les produits que vous mettez à leur disposition dans votre instance Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="529ea-105">This guide shows to how to create and invite developers to use the APIs and products that you make available to them with your API Management instance.</span></span> <span data-ttu-id="529ea-106">Pour plus d’informations sur la gestion des comptes d’utilisateur par programme, consultez la documentation [Entité utilisateur](https://msdn.microsoft.com/library/azure/dn776330.aspx) dans la référence [API REST de gestion](https://msdn.microsoft.com/library/azure/dn776326.aspx).</span><span class="sxs-lookup"><span data-stu-id="529ea-106">For information on managing user accounts programmatically, see the [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span>

## <span data-ttu-id="529ea-107"><a name="create-developer"> </a>Création d’un développeur</span><span class="sxs-lookup"><span data-stu-id="529ea-107"><a name="create-developer"> </a>Create a new developer</span></span>
<span data-ttu-id="529ea-108">Pour créer un développeur, cliquez sur **Portail des éditeurs** dans le portail Azure de votre service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="529ea-108">To create a new developer, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="529ea-109">Vous accédez au portail des éditeurs Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="529ea-109">This takes you to the API Management publisher portal.</span></span> <span data-ttu-id="529ea-110">Si vous n’avez pas encore créé une instance de service Gestion des API, consultez la page de [création d’une instance de service Gestion des API][Create an API Management service instance] dans le didacticiel de [prise en main de Gestion des API Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="529ea-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Portail des éditeurs][api-management-management-console]

<span data-ttu-id="529ea-112">Cliquez sur **Utilisateurs** dans le menu **Gestion des API** à gauche, puis sur **Ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="529ea-112">Click **Users** from the **API Management** menu on the left, and then click **add user**.</span></span>

![Create developer][api-management-create-developer]

<span data-ttu-id="529ea-114">Entrez l’**adresse électronique**, le **mot de passe** et le **nom** du nouveau développeur et cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="529ea-114">Enter the **Email**, **Password**, and **Name** for the new developer and click **Save**.</span></span>

![Create developer][api-management-add-new-user]

<span data-ttu-id="529ea-116">Par défaut, les comptes de développeurs nouvellement créés sont **actifs**. Ils sont associés au groupe **Développeurs**.</span><span class="sxs-lookup"><span data-stu-id="529ea-116">By default, newly created developer accounts are **Active**, and associated with the **Developers** group.</span></span>

![New developer][api-management-new-developer]

<span data-ttu-id="529ea-118">Les comptes de développeurs dont l'état est **actif** peuvent être utilisés pour accéder à toutes les API auxquelles ils sont abonnés.</span><span class="sxs-lookup"><span data-stu-id="529ea-118">Developer accounts that are in an **active** state can be used to access all of the APIs for which they have subscriptions.</span></span> <span data-ttu-id="529ea-119">Pour associer les développeurs nouvellement créés à d’autres groupes, consultez la rubrique [Association de groupes à des développeurs][How to associate groups with developers].</span><span class="sxs-lookup"><span data-stu-id="529ea-119">To associate the newly created developer with additional groups, see [How to associate groups with developers][How to associate groups with developers].</span></span>

## <span data-ttu-id="529ea-120"><a name="invite-developer"> </a>Invitation d’un développeur</span><span class="sxs-lookup"><span data-stu-id="529ea-120"><a name="invite-developer"> </a>Invite a developer</span></span>
<span data-ttu-id="529ea-121">Pour inviter un développeur, cliquez sur **Utilisateurs** dans le menu **Gestion des API** à gauche, puis sur **Inviter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="529ea-121">To invite a developer, click **Users** from the **API Management** menu on the left, and then click **Invite User**.</span></span>

![Invite developer][api-management-invite-developer]

<span data-ttu-id="529ea-123">Entrez le nom et l'adresse électronique du développeur, puis cliquez sur **Inviter**.</span><span class="sxs-lookup"><span data-stu-id="529ea-123">Enter the name and email address of the developer, and click **Invite**.</span></span>

![Invite developer][api-management-invite-developer-window]

<span data-ttu-id="529ea-125">Un message de confirmation s’affiche, mais le développeur qui vient d’être invité n’apparaît pas dans la liste tant qu’il n’a pas accepté l’invitation.</span><span class="sxs-lookup"><span data-stu-id="529ea-125">A confirmation message is displayed, but the newly invited developer does not appear in the list until after they accept the invitation.</span></span> 

![Invite confirmation][api-management-invite-developer-confirmation]

<span data-ttu-id="529ea-127">Quand un développeur est invité, un message lui est envoyé.</span><span class="sxs-lookup"><span data-stu-id="529ea-127">When a developer is invited, an email is sent to the developer.</span></span> <span data-ttu-id="529ea-128">Ce message est généré à partir d'un modèle. Il est personnalisable.</span><span class="sxs-lookup"><span data-stu-id="529ea-128">This email is generated using a template and is customizable.</span></span> <span data-ttu-id="529ea-129">Pour plus d’informations, consultez la page [Configuration des modèles de courrier électronique][Configure email templates].</span><span class="sxs-lookup"><span data-stu-id="529ea-129">For more information, see [Configure email templates][Configure email templates].</span></span>

<span data-ttu-id="529ea-130">Une fois l'invitation acceptée, le compte est activé.</span><span class="sxs-lookup"><span data-stu-id="529ea-130">Once the invitation is accepted, the account becomes active.</span></span>

## <span data-ttu-id="529ea-131"><a name="block-developer"> </a> Désactivation ou réactivation d’un compte de développeur</span><span class="sxs-lookup"><span data-stu-id="529ea-131"><a name="block-developer"> </a> Deactivate or reactivate a developer account</span></span>
<span data-ttu-id="529ea-132">Par défaut, les comptes de développeur nouvellement créés ou invités sont **actifs**.</span><span class="sxs-lookup"><span data-stu-id="529ea-132">By default, newly created or invited developer accounts are **Active**.</span></span> <span data-ttu-id="529ea-133">Pour désactiver un compte de développeur, cliquez sur **Bloquer**.</span><span class="sxs-lookup"><span data-stu-id="529ea-133">To deactivate a developer account, click **Block**.</span></span> <span data-ttu-id="529ea-134">Pour réactiver un compte de développeur bloqué, cliquez sur **Activer**.</span><span class="sxs-lookup"><span data-stu-id="529ea-134">To reactivate a blocked developer account, click **Activate**.</span></span> <span data-ttu-id="529ea-135">Les comptes de développeurs bloqués ne peuvent pas accéder au portail des développeurs, ni appeler les API.</span><span class="sxs-lookup"><span data-stu-id="529ea-135">A blocked developer account can not access the developer portal or call any APIs.</span></span> <span data-ttu-id="529ea-136">Pour supprimer un compte d’utilisateur, cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="529ea-136">To delete a user account, click **Delete**.</span></span>

![Block developer][api-management-new-developer]

## <a name="reset-a-user-password"></a><span data-ttu-id="529ea-138">Réinitialiser le mot de passe d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="529ea-138">Reset a user password</span></span>
<span data-ttu-id="529ea-139">Pour réinitialiser le mot de passe d’un compte d’utilisateur, cliquez sur le nom du compte.</span><span class="sxs-lookup"><span data-stu-id="529ea-139">To reset the password for a user account, click the name of the account.</span></span>

![Réinitialiser le mot de passe][api-management-view-developer]

<span data-ttu-id="529ea-141">Cliquez sur **Réinitialiser le mot de passe** pour envoyer un lien à l’utilisateur lui permettant de réinitialiser son mot de passe.</span><span class="sxs-lookup"><span data-stu-id="529ea-141">Click **Reset password** to send a link to the user to reset their password.</span></span>

![Réinitialiser le mot de passe][api-management-reset-password]

<span data-ttu-id="529ea-143">Pour utiliser les comptes d’utilisateur par programme, consultez la documentation [Entité utilisateur](https://msdn.microsoft.com/library/azure/dn776330.aspx) dans la référence [API REST de gestion](https://msdn.microsoft.com/library/azure/dn776326.aspx).</span><span class="sxs-lookup"><span data-stu-id="529ea-143">To programmatically work with user accounts, see the [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span> <span data-ttu-id="529ea-144">Pour réinitialiser le mot de passe d’un compte d’utilisateur sur une valeur spécifique, vous pouvez utiliser l’opération [Mettre à jour un utilisateur](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) et spécifier le mot de passe nécessaire.</span><span class="sxs-lookup"><span data-stu-id="529ea-144">To reset a user account password to a specific value, you can use the [Update a user](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operation and specify the desired password.</span></span>

## <a name="pending-verification"></a><span data-ttu-id="529ea-145">Vérification en attente</span><span class="sxs-lookup"><span data-stu-id="529ea-145">Pending verification</span></span>
![Vérification en attente][api-management-pending-verification]

## <span data-ttu-id="529ea-147"><a name="next-steps"> </a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="529ea-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="529ea-148">Une fois le compte de développeur créé, vous pouvez l'associer à des rôles et l'abonner à des produits et des API.</span><span class="sxs-lookup"><span data-stu-id="529ea-148">Once a developer account is created, you can associate it with roles and subscribe it to products and APIs.</span></span> <span data-ttu-id="529ea-149">Pour plus d’informations, consultez la page [Création et utilisation de groupes][How to create and use groups].</span><span class="sxs-lookup"><span data-stu-id="529ea-149">For more information, see [How to create and use groups][How to create and use groups].</span></span>

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
