---
title: "les notifications aaaConfigure et envoyer par courrier électronique des modèles de gestion des API Azure | Documents Microsoft"
description: "Découvrez comment tooconfigure notifications et modèles dans Azure API Management de courrier électronique."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: ee25f26d-4752-433b-af9c-3817db38aed5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: dc23289c25a1641992b73cb955099b3f207b6968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-notifications-and-email-templates-in-azure-api-management"></a><span data-ttu-id="93af9-103">Comment les notifications tooconfigure et envoyer par courrier électronique des modèles de gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="93af9-103">How tooconfigure notifications and email templates in Azure API Management</span></span>
<span data-ttu-id="93af9-104">Gestion des API permet hello tooconfigure des notifications d’événements spécifiques ou des modèles de messages électroniques hello tooconfigure sont toocommunicate utilisé avec les administrateurs de hello et aux développeurs d’une instance de la gestion des API.</span><span class="sxs-lookup"><span data-stu-id="93af9-104">API Management provides hello ability tooconfigure notifications for specific events, and tooconfigure hello email templates that are used toocommunicate with hello administrators and developers of an API Management instance.</span></span> <span data-ttu-id="93af9-105">Cette rubrique montre comment les notifications tooconfigure pour hello événements disponibles et fournit une vue d’ensemble de la configuration de modèles de messages électroniques hello utilisés pour ces événements.</span><span class="sxs-lookup"><span data-stu-id="93af9-105">This topic shows how tooconfigure notifications for hello available events, and provides an overview of configuring hello email templates used for these events.</span></span>

## <span data-ttu-id="93af9-106"><a name="publisher-notifications"></a>Configuration des notifications de l’éditeur</span><span class="sxs-lookup"><span data-stu-id="93af9-106"><a name="publisher-notifications"> </a>Configure publisher notifications</span></span>
<span data-ttu-id="93af9-107">notifications de tooconfigure, cliquez sur **portail de publication** Bonjour portail Azure pour votre service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="93af9-107">tooconfigure notifications, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="93af9-108">Cela vous prend un portail de publication de gestion des API toohello.</span><span class="sxs-lookup"><span data-stu-id="93af9-108">This takes you toohello API Management publisher portal.</span></span>

![Portail des éditeurs][api-management-management-console]

> [!NOTE] 
> <span data-ttu-id="93af9-110">Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main Azure API Management] [ Get started with Azure API Management] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="93af9-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

<span data-ttu-id="93af9-111">Cliquez sur **Notifications** de hello **gestion des API** hello menu gauche tooview notification hello est disponible.</span><span class="sxs-lookup"><span data-stu-id="93af9-111">Click **Notifications** from hello **API Management** menu on hello left tooview hello available notifications.</span></span>

![Notifications de l’éditeur][api-management-publisher-notifications]

<span data-ttu-id="93af9-113">Hello la liste suivante d’événements peut être configurée pour les notifications.</span><span class="sxs-lookup"><span data-stu-id="93af9-113">hello following list of events can be configured for notifications.</span></span>

* <span data-ttu-id="93af9-114">**Demandes d’abonnement (nécessitant l’approbation)** : hello destinataires spécifiés et les utilisateurs reçoivent des notifications par courrier électronique à propos des demandes d’abonnement pour les produits d’API nécessitant une approbation.</span><span class="sxs-lookup"><span data-stu-id="93af9-114">**Subscription requests (requiring approval)** - hello specified email recipients and users will receive email notifications about subscription requests for API products requiring approval.</span></span>
* <span data-ttu-id="93af9-115">**Les nouveaux abonnements** : hello destinataires spécifiés et les utilisateurs reçoivent des notifications par courrier électronique relatives à des abonnements de produit d’API.</span><span class="sxs-lookup"><span data-stu-id="93af9-115">**New subscriptions** - hello specified email recipients and users will receive email notifications about new API product subscriptions.</span></span>
* <span data-ttu-id="93af9-116">**Les demandes d’application de la galerie** : hello destinataires spécifiés et les utilisateurs reçoivent des notifications par courrier électronique lorsque les nouvelles applications sont soumis toohello Galerie d’applications.</span><span class="sxs-lookup"><span data-stu-id="93af9-116">**Application gallery requests** - hello specified email recipients and users will receive email notifications when new applications are submitted toohello application gallery.</span></span>
* <span data-ttu-id="93af9-117">**Cci** : hello destinataires spécifiés et les utilisateurs reçoivent par courrier électronique invisible copie de tous les messages électroniques envoyés toodevelopers.</span><span class="sxs-lookup"><span data-stu-id="93af9-117">**BCC** - hello specified email recipients and users will receive email blind carbon copies of all emails sent toodevelopers.</span></span>
* <span data-ttu-id="93af9-118">**Nouveau problème ou un commentaire** - hello destinataires spécifiés et les utilisateurs reçoivent des notifications par courrier électronique lorsqu’un nouveau problème ou commentaire est envoyé sur le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="93af9-118">**New issue or comment** - hello specified email recipients and users will receive email notifications when a new issue or comment is submitted on hello developer portal.</span></span>
* <span data-ttu-id="93af9-119">**Message de fermer le compte** : hello destinataires spécifiés et les utilisateurs reçoivent des notifications par courrier électronique quand un compte est fermé.</span><span class="sxs-lookup"><span data-stu-id="93af9-119">**Close account message** - hello specified email recipients and users will receive email notifications when an account is closed.</span></span>
* <span data-ttu-id="93af9-120">**Limite de quota approchant abonnement** : hello suivant des destinataires de courrier électronique et les utilisateurs reçoivent des notifications par courrier électronique lors de l’utilisation d’abonnement obtient toousage fermer quota.</span><span class="sxs-lookup"><span data-stu-id="93af9-120">**Approaching subscription quota limit** - hello following email recipients and users will receive email notifications when subscription usage gets close toousage quota.</span></span>

<span data-ttu-id="93af9-121">Pour chaque événement, vous pouvez spécifier des destinataires de courrier électronique à l’aide de la zone de texte adresse e-mail hello ou vous pouvez sélectionner des utilisateurs à partir d’une liste.</span><span class="sxs-lookup"><span data-stu-id="93af9-121">For each event, you can specify email recipients using hello email address text box or you can select users from a list.</span></span>

<span data-ttu-id="93af9-122">toospecify hello messagerie adresses toobe averti, entrez-les dans la zone de texte adresse e-mail hello.</span><span class="sxs-lookup"><span data-stu-id="93af9-122">toospecify hello email addresses toobe notified, enter them in hello email address text box.</span></span> <span data-ttu-id="93af9-123">Si vous devez entrer plusieurs adresses, séparez-les par des virgules.</span><span class="sxs-lookup"><span data-stu-id="93af9-123">If you have multiple email addresses, separate them using commas.</span></span>

![Notification recipients][api-management-email-addresses]

<span data-ttu-id="93af9-125">toospecify hello utilisateurs toobe la notification, cliquez sur **Ajouter destinataire**, hello la case en regard de hello utilisateurs toobe est notifiée, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="93af9-125">toospecify hello users toobe notified, click **add recipient**, check hello box beside hello users toobe notified, and click **OK**.</span></span>

> [!NOTE] 
> <span data-ttu-id="93af9-126">Seuls les administrateurs sont affichés dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="93af9-126">Only administrators are displayed in hello list.</span></span>


<span data-ttu-id="93af9-127">Après avoir configuré les destinataires des notifications hello, cliquez sur **enregistrer** tooapply hello mis à jour les destinataires des notifications.</span><span class="sxs-lookup"><span data-stu-id="93af9-127">After configuring hello notification recipients, click **Save** tooapply hello updated notification recipients.</span></span>

> [!NOTE] 
> <span data-ttu-id="93af9-128">Si vous quittez hello **Notifications du serveur de publication** portail de publication onglet hello vous avertit qu’il y a des modifications non enregistrées.</span><span class="sxs-lookup"><span data-stu-id="93af9-128">If you navigate away from hello **Publisher Notifications** tab hello publisher portal alerts you if there are unsaved changes.</span></span>


## <span data-ttu-id="93af9-129"><a name="email-templates"></a>Configuration des modèles de courrier électronique</span><span class="sxs-lookup"><span data-stu-id="93af9-129"><a name="email-templates"> </a>Configure email templates</span></span>
<span data-ttu-id="93af9-130">Gestion des API fournit des modèles de messagerie pourquoi les messages électroniques qui sont envoyés en cours hello d’administration et à l’aide du service de hello.</span><span class="sxs-lookup"><span data-stu-id="93af9-130">API Management provides email templates for hello email messages that are sent in hello course of administering and using hello service.</span></span> <span data-ttu-id="93af9-131">Hello suivant des modèles de messages électroniques est fournie.</span><span class="sxs-lookup"><span data-stu-id="93af9-131">hello following email templates are provided.</span></span>

* <span data-ttu-id="93af9-132">Demande d'ajout à la galerie d'applications approuvée</span><span class="sxs-lookup"><span data-stu-id="93af9-132">Application gallery submission approved</span></span>
* <span data-ttu-id="93af9-133">Lettre d'adieu au développeur</span><span class="sxs-lookup"><span data-stu-id="93af9-133">Developer farewell letter</span></span>
* <span data-ttu-id="93af9-134">Notification de la limite du quota d'abonnement bientôt atteinte</span><span class="sxs-lookup"><span data-stu-id="93af9-134">Developer quota limit approaching notification</span></span>
* <span data-ttu-id="93af9-135">Invitation de l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="93af9-135">Invite user</span></span>
* <span data-ttu-id="93af9-136">Nouveau commentaire ajouté tooan problème</span><span class="sxs-lookup"><span data-stu-id="93af9-136">New comment added tooan issue</span></span>
* <span data-ttu-id="93af9-137">Nouveau problème reçu</span><span class="sxs-lookup"><span data-stu-id="93af9-137">New issue received</span></span>
* <span data-ttu-id="93af9-138">Nouvel abonnement activé</span><span class="sxs-lookup"><span data-stu-id="93af9-138">New subscription activated</span></span>
* <span data-ttu-id="93af9-139">Confirmation du renouvellement de l'abonnement</span><span class="sxs-lookup"><span data-stu-id="93af9-139">Subscription renewed confirmation</span></span>
* <span data-ttu-id="93af9-140">Refus de la demande d'abonnement</span><span class="sxs-lookup"><span data-stu-id="93af9-140">Subscription request declines</span></span>
* <span data-ttu-id="93af9-141">Réception de la demande d'abonnement</span><span class="sxs-lookup"><span data-stu-id="93af9-141">Subscription request received</span></span>

<span data-ttu-id="93af9-142">Ces modèles peuvent être modifiés comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="93af9-142">These templates can be modified as desired.</span></span>

<span data-ttu-id="93af9-143">tooview et configurer les modèles de messagerie hello pour votre instance de la gestion des API, cliquez sur **Notifications** de hello **gestion des API** menu hello gauche et sélectionnez hello **modèles de messages électroniques**  onglet.</span><span class="sxs-lookup"><span data-stu-id="93af9-143">tooview and configure hello email templates for your API Management instance, click **Notifications** from hello **API Management** menu on hello left, and select hello **Email Templates** tab.</span></span>

![Email templates][api-management-email-templates]

<span data-ttu-id="93af9-145">tooview ou modifier un modèle spécifique, sélectionnez-le dans hello **modèles** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="93af9-145">tooview or modify a specific template, select it from hello **Templates** drop-down list.</span></span>

![Email templates list][api-management-email-templates-list]

<span data-ttu-id="93af9-147">Pour chaque modèle de message, l'objet est au format texte et le corps au format HTML.</span><span class="sxs-lookup"><span data-stu-id="93af9-147">Each email template has a subject in plain text, and a body definition in HTML format.</span></span> <span data-ttu-id="93af9-148">Chaque élément peut être personnalisé.</span><span class="sxs-lookup"><span data-stu-id="93af9-148">Each item can be customized as desired.</span></span>

![Email template editor][api-management-email-template]

<span data-ttu-id="93af9-150">Hello **paramètres** liste contient une liste de paramètres, où insérées dans hello objet ou le corps, sera remplacé hello désigné lorsque hello e-mail est envoyé.</span><span class="sxs-lookup"><span data-stu-id="93af9-150">hello **Parameters** list contains a list of parameters, which when inserted into hello subject or body, will be replaced hello designated value when hello email is sent.</span></span> <span data-ttu-id="93af9-151">tooinsert un paramètre, placez le curseur à hello où vous le souhaitez toogo de paramètre hello et cliquez sur hello flèche toohello à gauche du nom de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="93af9-151">tooinsert a parameter, place hello cursor where you wish hello parameter toogo, and click hello arrow toohello left of hello parameter name.</span></span>

<span data-ttu-id="93af9-152">Cliquez sur **aperçu** ou **envoyer un test** toosee comment par courrier électronique hello sera rechercher ou envoyer un courrier électronique de test.</span><span class="sxs-lookup"><span data-stu-id="93af9-152">Click **Preview** or **Send a test** toosee how hello email will look or send a test email.</span></span>

> [!NOTE] 
> <span data-ttu-id="93af9-153">paramètres de Hello ne sont pas remplacées par des valeurs réelles lors de l’aperçu ou l’envoi d’un test.</span><span class="sxs-lookup"><span data-stu-id="93af9-153">hello parameters are not replaced with actual values when previewing or sending a test.</span></span>

<span data-ttu-id="93af9-154">modèle d’e-mail toohello toosave hello modifications, cliquez sur **enregistrer**, ou cliquez sur les modifications de hello toocancel **Annuler**.</span><span class="sxs-lookup"><span data-stu-id="93af9-154">toosave hello changes toohello email template, click **Save**, or toocancel hello changes click **Cancel**.</span></span>
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
