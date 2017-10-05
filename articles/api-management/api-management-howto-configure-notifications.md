---
title: "Configurer des notifications et des modèles d’e-mails dans Gestion des API Azure | Microsoft Docs"
description: "Apprenez à configurer des notifications et des modèles de messages électroniques dans Gestion des API Azure."
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
ms.openlocfilehash: 3d8b74e32059cfc1a4c3a8fc7d3bd04676ee80c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-notifications-and-email-templates-in-azure-api-management"></a><span data-ttu-id="9eee9-103">Configuration des notifications et des modèles de messages électroniques dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="9eee9-103">How to configure notifications and email templates in Azure API Management</span></span>
<span data-ttu-id="9eee9-104">Gestion des API Azure permet de configurer les notifications pour des événements spécifiques et de configurer les modèles de courrier électronique utilisés pour communiquer avec les administrateurs et les développeurs de l’instance Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="9eee9-104">API Management provides the ability to configure notifications for specific events, and to configure the email templates that are used to communicate with the administrators and developers of an API Management instance.</span></span> <span data-ttu-id="9eee9-105">Cette rubrique vous présente comment configurer les notifications pour les événements disponibles. Elle offre également un aperçu de la configuration des modèles de messages électroniques utilisés pour ces événements.</span><span class="sxs-lookup"><span data-stu-id="9eee9-105">This topic shows how to configure notifications for the available events, and provides an overview of configuring the email templates used for these events.</span></span>

## <span data-ttu-id="9eee9-106"><a name="publisher-notifications"> </a>Configuration des notifications de l’éditeur</span><span class="sxs-lookup"><span data-stu-id="9eee9-106"><a name="publisher-notifications"> </a>Configure publisher notifications</span></span>
<span data-ttu-id="9eee9-107">Pour configurer les notifications, cliquez sur **Portail de publication** dans le portail Azure pour accéder à votre service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="9eee9-107">To configure notifications, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="9eee9-108">Vous accédez au portail des éditeurs Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="9eee9-108">This takes you to the API Management publisher portal.</span></span>

![Portail des éditeurs][api-management-management-console]

> [!NOTE] 
> <span data-ttu-id="9eee9-110">Si vous n’avez pas encore créé une instance de service Gestion des API, consultez la page de [création d’une instance de service Gestion des API][Create an API Management service instance] dans le didacticiel de [prise en main de Gestion des API Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="9eee9-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

<span data-ttu-id="9eee9-111">Cliquez sur **Notifications** dans le menu **Gestion des API** à gauche pour voir les notifications disponibles.</span><span class="sxs-lookup"><span data-stu-id="9eee9-111">Click **Notifications** from the **API Management** menu on the left to view the available notifications.</span></span>

![Notifications de l’éditeur][api-management-publisher-notifications]

<span data-ttu-id="9eee9-113">La liste suivante répertorie les événements pour lesquels il est possible de configurer des notifications.</span><span class="sxs-lookup"><span data-stu-id="9eee9-113">The following list of events can be configured for notifications.</span></span>

* <span data-ttu-id="9eee9-114">**Demandes d'abonnement (approbation nécessaire)** : les destinataires du message et les utilisateurs spécifiés reçoivent une notification pour les demandes d'abonnement aux produits API nécessitant une approbation.</span><span class="sxs-lookup"><span data-stu-id="9eee9-114">**Subscription requests (requiring approval)** - The specified email recipients and users will receive email notifications about subscription requests for API products requiring approval.</span></span>
* <span data-ttu-id="9eee9-115">**Nouveaux abonnements** : les destinataires du message et les utilisateurs spécifiés reçoivent une notification concernant les nouveaux abonnements aux produits API.</span><span class="sxs-lookup"><span data-stu-id="9eee9-115">**New subscriptions** - The specified email recipients and users will receive email notifications about new API product subscriptions.</span></span>
* <span data-ttu-id="9eee9-116">**Demandes de la galerie d'applications** : les destinataires du message et les utilisateurs spécifiés reçoivent une notification lorsque de nouvelles applications sont proposées dans la galerie d'applications.</span><span class="sxs-lookup"><span data-stu-id="9eee9-116">**Application gallery requests** - The specified email recipients and users will receive email notifications when new applications are submitted to the application gallery.</span></span>
* <span data-ttu-id="9eee9-117">**CCI** : les destinataires du message et les utilisateurs spécifiés reçoivent une copie cachée de tous les messages envoyés aux développeurs.</span><span class="sxs-lookup"><span data-stu-id="9eee9-117">**BCC** - The specified email recipients and users will receive email blind carbon copies of all emails sent to developers.</span></span>
* <span data-ttu-id="9eee9-118">**Nouveau problème ou commentaire** : les destinataires du message et les utilisateurs spécifiés reçoivent une notification lorsqu'un problème ou un commentaire est envoyé sur le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="9eee9-118">**New issue or comment** - The specified email recipients and users will receive email notifications when a new issue or comment is submitted on the developer portal.</span></span>
* <span data-ttu-id="9eee9-119">**Message de fermeture de compte** : les destinataires du message et les utilisateurs spécifiés reçoivent une notification lorsqu'un compte est fermé.</span><span class="sxs-lookup"><span data-stu-id="9eee9-119">**Close account message** - The specified email recipients and users will receive email notifications when an account is closed.</span></span>
* <span data-ttu-id="9eee9-120">**Limite du quota d'abonnements bientôt atteint** : les destinataires du message et les utilisateurs spécifiés reçoivent une notification lorsque l'utilisation de l'abonnement approche le quota.</span><span class="sxs-lookup"><span data-stu-id="9eee9-120">**Approaching subscription quota limit** - The following email recipients and users will receive email notifications when subscription usage gets close to usage quota.</span></span>

<span data-ttu-id="9eee9-121">Pour chaque événement, vous pouvez spécifier les destinataires du message via la zone de texte d'adresse. Vous pouvez également sélectionner les utilisateurs dans une liste.</span><span class="sxs-lookup"><span data-stu-id="9eee9-121">For each event, you can specify email recipients using the email address text box or you can select users from a list.</span></span>

<span data-ttu-id="9eee9-122">Pour spécifier les adresses à notifier, entrez-les dans la zone de texte d'adresse.</span><span class="sxs-lookup"><span data-stu-id="9eee9-122">To specify the email addresses to be notified, enter them in the email address text box.</span></span> <span data-ttu-id="9eee9-123">Si vous devez entrer plusieurs adresses, séparez-les par des virgules.</span><span class="sxs-lookup"><span data-stu-id="9eee9-123">If you have multiple email addresses, separate them using commas.</span></span>

![Notification recipients][api-management-email-addresses]

<span data-ttu-id="9eee9-125">Pour spécifier les utilisateurs à notifier, cliquez sur **Ajouter un destinataire**, activez la case à cocher à côté de l’utilisateur à notifier, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="9eee9-125">To specify the users to be notified, click **add recipient**, check the box beside the users to be notified, and click **OK**.</span></span>

> [!NOTE] 
> <span data-ttu-id="9eee9-126">Seuls les administrateurs sont affichés dans la liste.</span><span class="sxs-lookup"><span data-stu-id="9eee9-126">Only administrators are displayed in the list.</span></span>


<span data-ttu-id="9eee9-127">Une fois les destinataires de la notification configurés, cliquez sur **Enregistrer** pour appliquer les modifications des destinataires.</span><span class="sxs-lookup"><span data-stu-id="9eee9-127">After configuring the notification recipients, click **Save** to apply the updated notification recipients.</span></span>

> [!NOTE] 
> <span data-ttu-id="9eee9-128">Si vous quittez l’onglet **Notifications de l’éditeur** , le portail de publication vous avertit si des modifications n’ont pas été enregistrées.</span><span class="sxs-lookup"><span data-stu-id="9eee9-128">If you navigate away from the **Publisher Notifications** tab the publisher portal alerts you if there are unsaved changes.</span></span>


## <span data-ttu-id="9eee9-129"><a name="email-templates"> </a>Configuration des modèles de courrier électronique</span><span class="sxs-lookup"><span data-stu-id="9eee9-129"><a name="email-templates"> </a>Configure email templates</span></span>
<span data-ttu-id="9eee9-130">L'outil Gestion des API contient des modèles de messages électroniques pour les messages envoyés dans le cadre de l'administration et de l'utilisation du service.</span><span class="sxs-lookup"><span data-stu-id="9eee9-130">API Management provides email templates for the email messages that are sent in the course of administering and using the service.</span></span> <span data-ttu-id="9eee9-131">Les modèles suivants sont fournis.</span><span class="sxs-lookup"><span data-stu-id="9eee9-131">The following email templates are provided.</span></span>

* <span data-ttu-id="9eee9-132">Demande d'ajout à la galerie d'applications approuvée</span><span class="sxs-lookup"><span data-stu-id="9eee9-132">Application gallery submission approved</span></span>
* <span data-ttu-id="9eee9-133">Lettre d'adieu au développeur</span><span class="sxs-lookup"><span data-stu-id="9eee9-133">Developer farewell letter</span></span>
* <span data-ttu-id="9eee9-134">Notification de la limite du quota d'abonnement bientôt atteinte</span><span class="sxs-lookup"><span data-stu-id="9eee9-134">Developer quota limit approaching notification</span></span>
* <span data-ttu-id="9eee9-135">Invitation de l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="9eee9-135">Invite user</span></span>
* <span data-ttu-id="9eee9-136">Nouveau commentaire ajouté à un problème</span><span class="sxs-lookup"><span data-stu-id="9eee9-136">New comment added to an issue</span></span>
* <span data-ttu-id="9eee9-137">Nouveau problème reçu</span><span class="sxs-lookup"><span data-stu-id="9eee9-137">New issue received</span></span>
* <span data-ttu-id="9eee9-138">Nouvel abonnement activé</span><span class="sxs-lookup"><span data-stu-id="9eee9-138">New subscription activated</span></span>
* <span data-ttu-id="9eee9-139">Confirmation du renouvellement de l'abonnement</span><span class="sxs-lookup"><span data-stu-id="9eee9-139">Subscription renewed confirmation</span></span>
* <span data-ttu-id="9eee9-140">Refus de la demande d'abonnement</span><span class="sxs-lookup"><span data-stu-id="9eee9-140">Subscription request declines</span></span>
* <span data-ttu-id="9eee9-141">Réception de la demande d'abonnement</span><span class="sxs-lookup"><span data-stu-id="9eee9-141">Subscription request received</span></span>

<span data-ttu-id="9eee9-142">Ces modèles peuvent être modifiés comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="9eee9-142">These templates can be modified as desired.</span></span>

<span data-ttu-id="9eee9-143">Pour voir et configurer les modèles de messages électroniques de votre instance Gestion des API, cliquez sur **Notifications** dans le menu **Gestion des API** à gauche, puis sélectionnez l’onglet **Modèles de messages électroniques**.</span><span class="sxs-lookup"><span data-stu-id="9eee9-143">To view and configure the email templates for your API Management instance, click **Notifications** from the **API Management** menu on the left, and select the **Email Templates** tab.</span></span>

![Email templates][api-management-email-templates]

<span data-ttu-id="9eee9-145">Pour consulter ou modifier un modèle en particulier, sélectionnez-le dans la liste déroulante **Modèles** .</span><span class="sxs-lookup"><span data-stu-id="9eee9-145">To view or modify a specific template, select it from the **Templates** drop-down list.</span></span>

![Email templates list][api-management-email-templates-list]

<span data-ttu-id="9eee9-147">Pour chaque modèle de message, l'objet est au format texte et le corps au format HTML.</span><span class="sxs-lookup"><span data-stu-id="9eee9-147">Each email template has a subject in plain text, and a body definition in HTML format.</span></span> <span data-ttu-id="9eee9-148">Chaque élément peut être personnalisé.</span><span class="sxs-lookup"><span data-stu-id="9eee9-148">Each item can be customized as desired.</span></span>

![Email template editor][api-management-email-template]

<span data-ttu-id="9eee9-150">La liste **Paramètres** contient une liste de paramètres qui, lorsqu'ils sont insérés dans l'objet ou dans le corps du message, sont remplacés par une valeur définie lorsque le message est envoyé.</span><span class="sxs-lookup"><span data-stu-id="9eee9-150">The **Parameters** list contains a list of parameters, which when inserted into the subject or body, will be replaced the designated value when the email is sent.</span></span> <span data-ttu-id="9eee9-151">Pour insérer un paramètre, placez le curseur là où vous voulez insérer le paramètre, puis cliquez sur la flèche à gauche du nom du paramètre.</span><span class="sxs-lookup"><span data-stu-id="9eee9-151">To insert a parameter, place the cursor where you wish the parameter to go, and click the arrow to the left of the parameter name.</span></span>

<span data-ttu-id="9eee9-152">Cliquez sur **Aperçu** ou **Envoyer un test** pour voir à quoi ressemble le message ou bien pour envoyer un message test.</span><span class="sxs-lookup"><span data-stu-id="9eee9-152">Click **Preview** or **Send a test** to see how the email will look or send a test email.</span></span>

> [!NOTE] 
> <span data-ttu-id="9eee9-153">Les paramètres ne sont pas remplacés par les valeurs réelles lors de l’aperçu ou du test.</span><span class="sxs-lookup"><span data-stu-id="9eee9-153">The parameters are not replaced with actual values when previewing or sending a test.</span></span>

<span data-ttu-id="9eee9-154">Pour enregistrer les modifications apportées au modèle de message, cliquez sur **Enregistrer**. Pour annuler les modifications, cliquez sur **Annuler**.</span><span class="sxs-lookup"><span data-stu-id="9eee9-154">To save the changes to the email template, click **Save**, or to cancel the changes click **Cancel**.</span></span>
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
