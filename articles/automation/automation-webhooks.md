---
title: "Démarrage d’un runbook Azure Automation avec un webhook | Microsoft Docs"
description: "Webhook qui permet à un client de démarrer un runbook dans Azure Automation à partir d’un appel HTTP.  Cet article décrit comment créer un webhook et l’appeler pour démarrer un runbook."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9b20237c-a593-4299-bbdc-35c47ee9e55d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: 6c65427fcd18e41a90dfb872aa9525f758b17b87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a><span data-ttu-id="44dd0-104">Démarrage d’un runbook Azure Automation avec un webhook</span><span class="sxs-lookup"><span data-stu-id="44dd0-104">Starting an Azure Automation runbook with a webhook</span></span>
<span data-ttu-id="44dd0-105">Un *webhook* vous permet de démarrer un Runbook dans Azure Automation via une simple requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="44dd0-105">A *webhook* allows you to start a particular runbook in Azure Automation through a single HTTP request.</span></span> <span data-ttu-id="44dd0-106">Les services externes, tels que Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analytics ou les applications personnalisées peuvent ainsi démarrer les runbooks sans avoir à implémenter une solution complète à l’aide de l’API Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="44dd0-106">This allows external services such as Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analytics, or custom applications to start runbooks without implementing a full solution using the Azure Automation API.</span></span>  
<span data-ttu-id="44dd0-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span><span class="sxs-lookup"><span data-stu-id="44dd0-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span></span>

<span data-ttu-id="44dd0-108">Vous pouvez comparer les webhooks à d'autres méthodes de démarrage d'un Runbook dans [Démarrage d'un Runbook dans Azure Automation](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="44dd0-108">You can compare webhooks to other methods of starting a runbook in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md)</span></span>

## <a name="details-of-a-webhook"></a><span data-ttu-id="44dd0-109">Détails d'un webhook</span><span class="sxs-lookup"><span data-stu-id="44dd0-109">Details of a webhook</span></span>
<span data-ttu-id="44dd0-110">Le tableau suivant décrit les propriétés que vous devez configurer pour un webhook.</span><span class="sxs-lookup"><span data-stu-id="44dd0-110">The following table describes the properties that you must configure for a webhook.</span></span>

| <span data-ttu-id="44dd0-111">Propriété</span><span class="sxs-lookup"><span data-stu-id="44dd0-111">Property</span></span> | <span data-ttu-id="44dd0-112">Description</span><span class="sxs-lookup"><span data-stu-id="44dd0-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="44dd0-113">Nom</span><span class="sxs-lookup"><span data-stu-id="44dd0-113">Name</span></span> |<span data-ttu-id="44dd0-114">Vous pouvez attribuer le nom de votre choix à un webhook, car il n'apparaît pas au client.</span><span class="sxs-lookup"><span data-stu-id="44dd0-114">You can provide any name you want for a webhook since this is not exposed to the client.</span></span>  <span data-ttu-id="44dd0-115">Il est uniquement utilisé pour que vous puissiez identifier le Runbook dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="44dd0-115">It is only used for you to identify the runbook in Azure Automation.</span></span> <br>  <span data-ttu-id="44dd0-116">À titre de meilleure pratique, nommez le webhook d'après le client qui l'utilise.</span><span class="sxs-lookup"><span data-stu-id="44dd0-116">As a best practice, you should give the webhook a name related to the client that will use it.</span></span> |
| <span data-ttu-id="44dd0-117">URL</span><span class="sxs-lookup"><span data-stu-id="44dd0-117">URL</span></span> |<span data-ttu-id="44dd0-118">L'URL du webhook est l'adresse unique qu'un client appelle avec une méthode HTTP POST pour démarrer le Runbook lié au webhook.</span><span class="sxs-lookup"><span data-stu-id="44dd0-118">The URL of the webhook is the unique address that a client calls with an HTTP POST to start the runbook linked to the webhook.</span></span>  <span data-ttu-id="44dd0-119">Elle est générée automatiquement lorsque vous créez le webhook.</span><span class="sxs-lookup"><span data-stu-id="44dd0-119">It is automatically generated when you create the webhook.</span></span>  <span data-ttu-id="44dd0-120">Vous ne pouvez pas spécifier d'URL personnalisée.</span><span class="sxs-lookup"><span data-stu-id="44dd0-120">You cannot specify a custom URL.</span></span> <br> <br>  <span data-ttu-id="44dd0-121">L'URL contient un jeton de sécurité qui permet que le Runbook soit appelé par un système tiers sans authentification supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="44dd0-121">The URL contains a security token that allows the runbook to be invoked by a third party system with no further authentication.</span></span> <span data-ttu-id="44dd0-122">Pour cette raison, elle doit être traitée comme un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="44dd0-122">For this reason, it should be treated like a password.</span></span>  <span data-ttu-id="44dd0-123">Pour des raisons de sécurité, vous pouvez uniquement afficher l’URL dans le portail Azure au moment de la création du webhook.</span><span class="sxs-lookup"><span data-stu-id="44dd0-123">For security reasons, you can only view the URL in the Azure portal at the time the webhook is created.</span></span> <span data-ttu-id="44dd0-124">Notez l'URL dans un emplacement sécurisé en vue d'une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="44dd0-124">You should note the URL in a secure location for future use.</span></span> |
| <span data-ttu-id="44dd0-125">Date d'expiration</span><span class="sxs-lookup"><span data-stu-id="44dd0-125">Expiration date</span></span> |<span data-ttu-id="44dd0-126">Comme un certificat, chaque webhook possède une date d'expiration à partir de laquelle il ne peut plus être utilisé.</span><span class="sxs-lookup"><span data-stu-id="44dd0-126">Like a certificate, each webhook has an expiration date at which time it can no longer be used.</span></span>  <span data-ttu-id="44dd0-127">Cette date d’expiration peut être modifiée après la création du webhook.</span><span class="sxs-lookup"><span data-stu-id="44dd0-127">This expiration date can be modified after the webhook is created.</span></span> |
| <span data-ttu-id="44dd0-128">Activé</span><span class="sxs-lookup"><span data-stu-id="44dd0-128">Enabled</span></span> |<span data-ttu-id="44dd0-129">Un webhook est activé par défaut lorsqu'il est créé.</span><span class="sxs-lookup"><span data-stu-id="44dd0-129">A webhook is enabled by default when it is created.</span></span>  <span data-ttu-id="44dd0-130">Si vous le définissez sur Disabled, aucun client ne sera en mesure de l'utiliser.</span><span class="sxs-lookup"><span data-stu-id="44dd0-130">If you set it to Disabled, then no client will be able to use it.</span></span>  <span data-ttu-id="44dd0-131">Vous pouvez définir la propriété **Enabled** lorsque vous créez le webhook ou à tout moment après qu'il a été créé.</span><span class="sxs-lookup"><span data-stu-id="44dd0-131">You can set the **Enabled** property when you create the webhook or anytime once it is created.</span></span> |

### <a name="parameters"></a><span data-ttu-id="44dd0-132">Paramètres</span><span class="sxs-lookup"><span data-stu-id="44dd0-132">Parameters</span></span>
<span data-ttu-id="44dd0-133">Un webhook peut définir les valeurs des paramètres du Runbook qui sont utilisées lorsque le Runbook est démarré par ce webhook.</span><span class="sxs-lookup"><span data-stu-id="44dd0-133">A webhook can define values for runbook parameters that are used when the runbook is started by that webhook.</span></span> <span data-ttu-id="44dd0-134">Le webhook doit inclure les valeurs de tous les paramètres obligatoires du Runbook et peut inclure les valeurs des paramètres optionnels.</span><span class="sxs-lookup"><span data-stu-id="44dd0-134">The webhook must include values for any mandatory parameters of the runbook and may include values for optional parameters.</span></span> <span data-ttu-id="44dd0-135">Une valeur de paramètre configurée pour un webhook peut être modifiée même après la création du webhook.</span><span class="sxs-lookup"><span data-stu-id="44dd0-135">A parameter value configured to a webhook can be modified even after creating the webhoook.</span></span> <span data-ttu-id="44dd0-136">Plusieurs webhooks liés à un même Runbook peuvent utiliser différentes valeurs de paramètres.</span><span class="sxs-lookup"><span data-stu-id="44dd0-136">Multiple webhooks linked to a single runbook can each use different parameter values.</span></span>

<span data-ttu-id="44dd0-137">Lorsqu'un client démarre un Runbook à l'aide d'un webhook, il ne peut pas remplacer les valeurs de paramètres définies dans le webhook.</span><span class="sxs-lookup"><span data-stu-id="44dd0-137">When a client starts a runbook using a webhook, it cannot override the parameter values defined in the webhook.</span></span>  <span data-ttu-id="44dd0-138">Pour recevoir les données du client, le Runbook peut accepter un paramètre unique appelé **$WebhookData** de type [object] qui contient les données que le client inclut dans la requête POST.</span><span class="sxs-lookup"><span data-stu-id="44dd0-138">To receive data from the client, the runbook can accept a single parameter called **$WebhookData** of type [object] that will contain data that the client includes in the POST request.</span></span>

![Propriétés Webhookdata](media/automation-webhooks/webhook-data-properties.png)

<span data-ttu-id="44dd0-140">L'objet **$WebhookData** possède les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="44dd0-140">The **$WebhookData** object will have the following properties:</span></span>

| <span data-ttu-id="44dd0-141">Propriété</span><span class="sxs-lookup"><span data-stu-id="44dd0-141">Property</span></span> | <span data-ttu-id="44dd0-142">Description</span><span class="sxs-lookup"><span data-stu-id="44dd0-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="44dd0-143">WebhookName</span><span class="sxs-lookup"><span data-stu-id="44dd0-143">WebhookName</span></span> |<span data-ttu-id="44dd0-144">Nom du webhook.</span><span class="sxs-lookup"><span data-stu-id="44dd0-144">The name of the webhook.</span></span> |
| <span data-ttu-id="44dd0-145">RequestHeader</span><span class="sxs-lookup"><span data-stu-id="44dd0-145">RequestHeader</span></span> |<span data-ttu-id="44dd0-146">Table de hachage contenant les en-têtes de la requête POST entrante.</span><span class="sxs-lookup"><span data-stu-id="44dd0-146">Hash table containing the headers of the incoming POST request.</span></span> |
| <span data-ttu-id="44dd0-147">RequestBody</span><span class="sxs-lookup"><span data-stu-id="44dd0-147">RequestBody</span></span> |<span data-ttu-id="44dd0-148">Corps de la requête POST entrante.</span><span class="sxs-lookup"><span data-stu-id="44dd0-148">The body of the incoming POST request.</span></span>  <span data-ttu-id="44dd0-149">Ceci conserve les mises en forme telles que les chaînes, JSON, XML ou les données de formulaire codées.</span><span class="sxs-lookup"><span data-stu-id="44dd0-149">This will retain any formatting such as string, JSON, XML, or form encoded data.</span></span> <span data-ttu-id="44dd0-150">Le Runbook doit être écrit pour fonctionner avec le format de données qui est attendu.</span><span class="sxs-lookup"><span data-stu-id="44dd0-150">The runbook must be written to work with the data format that is expected.</span></span> |

<span data-ttu-id="44dd0-151">Il n'existe aucune configuration du webhook requise pour prendre en charge le paramètre **$WebhookData** et le Runbook n'est pas obligé de l'accepter.</span><span class="sxs-lookup"><span data-stu-id="44dd0-151">There is no configuration of the webhook required to support the **$WebhookData** parameter, and the runbook is not required to accept it.</span></span>  <span data-ttu-id="44dd0-152">Si le Runbook ne définit pas le paramètre, tous les détails de la demande envoyée depuis le client sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="44dd0-152">If the runbook does not define the parameter, then any details of the request sent from the client is ignored.</span></span>

<span data-ttu-id="44dd0-153">Si vous spécifiez une valeur pour $WebhookData lorsque vous créez le webhook, cette valeur est remplacée lorsque le webhook démarre le Runbook avec les données de la demande POST du client, même si le client n'inclut pas toutes les données dans le corps de la demande.</span><span class="sxs-lookup"><span data-stu-id="44dd0-153">If you specify a value for $WebhookData when you create the webhook, that value will be overriden when the webhook starts the runbook with the data from the client POST request, even if the client does not include any data in the request body.</span></span>  <span data-ttu-id="44dd0-154">Si vous démarrez un Runbook ayant $WebhookData à l'aide d'une méthode autre qu'un webhook, vous pouvez fournir une valeur pour $Webhookdata qui sera reconnue par le Runbook.</span><span class="sxs-lookup"><span data-stu-id="44dd0-154">If you start a runbook that has $WebhookData using a method other than a webhook, you can provide a value for $Webhookdata that will be recognized by the runbook.</span></span>  <span data-ttu-id="44dd0-155">Cette valeur doit être un objet avec les mêmes [propriétés](#details-of-a-webhook) que $Webhookdata afin que le Runbook puisse l'utiliser correctement comme s’il s’agissait d’une valeur WebhookData réelle transmise par un webhook.</span><span class="sxs-lookup"><span data-stu-id="44dd0-155">This value should be an object with the same [properties](#details-of-a-webhook) as $Webhookdata so that the runbook can properly work with it as if it was working with actual WebhookData passed by a webhook.</span></span>

<span data-ttu-id="44dd0-156">Par exemple, si vous démarrez le runbook suivant à partir du portail Azure et que vous souhaitez passer certains exemples WebhookData à des fins de test, étant donné que WebhookData est un objet, ils doivent être transmis en tant que valeur JSON dans l'interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="44dd0-156">For example, if you are starting the following runbook from the Azure Portal and want to pass some sample WebhookData for testing, since WebhookData is an object, it should be passed as JSON in the UI.</span></span>

![Paramètre WebhookData à partir de l'interface utilisateur](media/automation-webhooks/WebhookData-parameter-from-UI.png)

<span data-ttu-id="44dd0-158">Pour le runbook ci-dessus, si vous avez les propriétés suivantes pour le paramètre WebhookData :</span><span class="sxs-lookup"><span data-stu-id="44dd0-158">For the above runbook, if you have the following properties for the WebhookData parameter:</span></span>

1. <span data-ttu-id="44dd0-159">WebhookName: *MyWebhook*</span><span class="sxs-lookup"><span data-stu-id="44dd0-159">WebhookName: *MyWebhook*</span></span>
2. <span data-ttu-id="44dd0-160">RequestHeader: *From=Test User*</span><span class="sxs-lookup"><span data-stu-id="44dd0-160">RequestHeader: *From=Test User*</span></span>
3. <span data-ttu-id="44dd0-161">RequestBody: *[“VM1”, “VM2”]*</span><span class="sxs-lookup"><span data-stu-id="44dd0-161">RequestBody: *[“VM1”, “VM2”]*</span></span>

<span data-ttu-id="44dd0-162">Vous pouvez alors transmettre la valeur JSON suivante dans l'interface utilisateur pour le paramètre WebhookData :</span><span class="sxs-lookup"><span data-stu-id="44dd0-162">Then you would pass the following JSON value in the UI for the WebhookData parameter:</span></span>  

* <span data-ttu-id="44dd0-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span><span class="sxs-lookup"><span data-stu-id="44dd0-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span></span>

![Démarrage du paramètre WebhookData à partir de l'interface utilisateur](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> <span data-ttu-id="44dd0-165">Les valeurs de tous les paramètres d'entrée sont enregistrés avec la tâche du Runbook.</span><span class="sxs-lookup"><span data-stu-id="44dd0-165">The values of all input parameters are logged with the runbook job.</span></span>  <span data-ttu-id="44dd0-166">Cela signifie qu'une entrée fournie par le client dans la requête webhook sera enregistrée et accessible à toute personne ayant accès à la tâche Automation.</span><span class="sxs-lookup"><span data-stu-id="44dd0-166">This means that any input provided by the client in the webhook request will be logged and available to anyone with access to the automation job.</span></span>  <span data-ttu-id="44dd0-167">Pour cette raison, soyez prudent lorsque vous incluez des informations sensibles dans les appels du webhook.</span><span class="sxs-lookup"><span data-stu-id="44dd0-167">For this reason, you should be cautious about including sensitive information in webhook calls.</span></span>
>

## <a name="security"></a><span data-ttu-id="44dd0-168">Sécurité</span><span class="sxs-lookup"><span data-stu-id="44dd0-168">Security</span></span>
<span data-ttu-id="44dd0-169">La sécurité d'un webhook s'appuie sur la confidentialité de son URL, laquelle contient un jeton de sécurité lui permettant d'être appelée.</span><span class="sxs-lookup"><span data-stu-id="44dd0-169">The security of a webhook relies on the privacy of its URL which contains a security token that allows it to be invoked.</span></span> <span data-ttu-id="44dd0-170">Azure Automation n'effectue pas d'authentification de la demande tant qu'elle est adressée à la bonne URL.</span><span class="sxs-lookup"><span data-stu-id="44dd0-170">Azure Automation does not perform any authentication on the request as long as it is made to the correct URL.</span></span> <span data-ttu-id="44dd0-171">Pour cette raison, les webhooks ne doivent pas être utilisés pour les Runbooks qui exécutent des fonctions très sensibles sans recourir à un autre moyen de validation de la demande.</span><span class="sxs-lookup"><span data-stu-id="44dd0-171">For this reason, webhooks should not be used for runbooks that perform highly sensitive functions without using an alternate means of validating the request.</span></span>

<span data-ttu-id="44dd0-172">Vous pouvez inclure une logique dans le Runbook pour déterminer qu'il a été appelé par un webhook en vérifiant la propriété **WebhookName** du paramètre $WebhookData.</span><span class="sxs-lookup"><span data-stu-id="44dd0-172">You can include logic within the runbook to determine that it was called by a webhook by checking the **WebhookName** property of the $WebhookData parameter.</span></span> <span data-ttu-id="44dd0-173">Le Runbook peut effectuer une validation supplémentaire en recherchant des informations spécifiques dans les propriétés **RequestHeader** ou **RequestBody**.</span><span class="sxs-lookup"><span data-stu-id="44dd0-173">The runbook could perform further validation by looking for particular information in the **RequestHeader** or **RequestBody** properties.</span></span>

<span data-ttu-id="44dd0-174">Une autre stratégie consiste à ce que le Runbook effectue la validation d'une condition externe lorsqu'il reçoit une demande du webhook.</span><span class="sxs-lookup"><span data-stu-id="44dd0-174">Another strategy is to have the runbook perform some validation of an external condition when it received a webhook request.</span></span>  <span data-ttu-id="44dd0-175">Par exemple, envisagez un Runbook appelé par GitHub chaque fois qu'il est procédé à une nouvelle validation d'un référentiel GitHub.</span><span class="sxs-lookup"><span data-stu-id="44dd0-175">For example, consider a runbook that is called by GitHub whenever there is a new commit to a GitHub repository.</span></span>  <span data-ttu-id="44dd0-176">Le Runbook peut se connecter à GitHub pour s'assurer qu'une nouvelle validation vient juste de se produire avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="44dd0-176">The runbook might connect to GitHub to validate that a new commit had actually just occurred before continuing.</span></span>

## <a name="creating-a-webhook"></a><span data-ttu-id="44dd0-177">Création d'un webhook</span><span class="sxs-lookup"><span data-stu-id="44dd0-177">Creating a webhook</span></span>
<span data-ttu-id="44dd0-178">Utilisez la procédure suivante pour créer un webhook lié à un Runbook dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="44dd0-178">Use the following procedure to create a new webhook linked to a runbook in the Azure portal.</span></span>

1. <span data-ttu-id="44dd0-179">À partir du panneau **Runbooks** du portail Azure, cliquez sur le Runbook que le webhook démarrera pour afficher son panneau Détails.</span><span class="sxs-lookup"><span data-stu-id="44dd0-179">From the **Runbooks blade** in the Azure portal, click the runbook that the webhook will start to view its detail blade.</span></span>
2. <span data-ttu-id="44dd0-180">Cliquez sur **Webhook** en haut du panneau pour ouvrir le panneau **Ajouter un webhook**.</span><span class="sxs-lookup"><span data-stu-id="44dd0-180">Click **Webhook** at the top of the blade to open the **Add Webhook** blade.</span></span> <br><span data-ttu-id="44dd0-181">
   ![Bouton Webhooks](media/automation-webhooks/webhooks-button.png)</span><span class="sxs-lookup"><span data-stu-id="44dd0-181">
![Webhooks button](media/automation-webhooks/webhooks-button.png)</span></span>
3. <span data-ttu-id="44dd0-182">Cliquez sur **Créer un nouveau webhook** pour ouvrir le panneau **Créer un webhook**.</span><span class="sxs-lookup"><span data-stu-id="44dd0-182">Click **Create new webhook** to open the **Create webhook blade**.</span></span>
4. <span data-ttu-id="44dd0-183">Spécifiez un **Nom** et une **Date d’expiration** pour le webhook, ainsi que s’il doit être activé.</span><span class="sxs-lookup"><span data-stu-id="44dd0-183">Specify a **Name**, **Expiration Date** for the webhook and whether it should be enabled.</span></span> <span data-ttu-id="44dd0-184">Pour plus d'informations sur ces propriétés, consultez [Détails d'un webhook](#details-of-a-webhook) .</span><span class="sxs-lookup"><span data-stu-id="44dd0-184">See [Details of a webhook](#details-of-a-webhook) for more information these properties.</span></span>
5. <span data-ttu-id="44dd0-185">Cliquez sur l'icône de copie et appuyez sur Ctrl + C pour copier l'URL du webhook.</span><span class="sxs-lookup"><span data-stu-id="44dd0-185">Click the copy icon and press Ctrl+C to copy the URL of the webhook.</span></span>  <span data-ttu-id="44dd0-186">Puis enregistrez-la dans un endroit sûr.</span><span class="sxs-lookup"><span data-stu-id="44dd0-186">Then record it in a safe place.</span></span>  <span data-ttu-id="44dd0-187">**Une fois que vous avez créé le webhook,vous ne pouvez pas récupérer l’URL à nouveau.**</span><span class="sxs-lookup"><span data-stu-id="44dd0-187">**Once you create the webhook, you cannot retrieve the URL again.**</span></span> <br><span data-ttu-id="44dd0-188">
   ![URL du webhook](media/automation-webhooks/copy-webhook-url.png)</span><span class="sxs-lookup"><span data-stu-id="44dd0-188">
![Webhook URL](media/automation-webhooks/copy-webhook-url.png)</span></span>
6. <span data-ttu-id="44dd0-189">Cliquez sur **Paramètres** pour fournir les valeurs des paramètres du Runbook.</span><span class="sxs-lookup"><span data-stu-id="44dd0-189">Click **Parameters** to provide values for the runbook parameters.</span></span>  <span data-ttu-id="44dd0-190">Si le Runbook possède des paramètres obligatoires, vous ne pourrez pas créer le webhook, sauf si des valeurs sont fournies.</span><span class="sxs-lookup"><span data-stu-id="44dd0-190">If the runbook has mandatory parameters, then you will not be able to create the webhook unless values are provided.</span></span>
7. <span data-ttu-id="44dd0-191">Cliquez sur **Créer** pour créer le webhook.</span><span class="sxs-lookup"><span data-stu-id="44dd0-191">Click **Create** to create the webhook.</span></span>

## <a name="using-a-webhook"></a><span data-ttu-id="44dd0-192">Utilisation d'un webhook</span><span class="sxs-lookup"><span data-stu-id="44dd0-192">Using a webhook</span></span>
<span data-ttu-id="44dd0-193">Pour utiliser un webhook après sa création, votre application cliente doit émettre une requête HTTP POST avec l'URL du webhook.</span><span class="sxs-lookup"><span data-stu-id="44dd0-193">To use a webhook after it has been created, your client application must issue an HTTP POST with the URL for the webhook.</span></span>  <span data-ttu-id="44dd0-194">La syntaxe du webhook sera au format suivant.</span><span class="sxs-lookup"><span data-stu-id="44dd0-194">The syntax of the webhook will be in the following format.</span></span>

    http://<Webhook Server>/token?=<Token Value>

<span data-ttu-id="44dd0-195">Le client reçoit l'un des codes de réponse suivants à la requête POST.</span><span class="sxs-lookup"><span data-stu-id="44dd0-195">The client will receive one of the following return codes from the POST request.</span></span>  

| <span data-ttu-id="44dd0-196">Code</span><span class="sxs-lookup"><span data-stu-id="44dd0-196">Code</span></span> | <span data-ttu-id="44dd0-197">Texte</span><span class="sxs-lookup"><span data-stu-id="44dd0-197">Text</span></span> | <span data-ttu-id="44dd0-198">Description</span><span class="sxs-lookup"><span data-stu-id="44dd0-198">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="44dd0-199">202</span><span class="sxs-lookup"><span data-stu-id="44dd0-199">202</span></span> |<span data-ttu-id="44dd0-200">Acceptée</span><span class="sxs-lookup"><span data-stu-id="44dd0-200">Accepted</span></span> |<span data-ttu-id="44dd0-201">La requête a été acceptée et le Runbook a été mis en file d'attente avec succès.</span><span class="sxs-lookup"><span data-stu-id="44dd0-201">The request was accepted, and the runbook was successfully queued.</span></span> |
| <span data-ttu-id="44dd0-202">400</span><span class="sxs-lookup"><span data-stu-id="44dd0-202">400</span></span> |<span data-ttu-id="44dd0-203">Demande incorrecte</span><span class="sxs-lookup"><span data-stu-id="44dd0-203">Bad Request</span></span> |<span data-ttu-id="44dd0-204">La demande a été refusée pour l'une des raisons suivantes.</span><span class="sxs-lookup"><span data-stu-id="44dd0-204">The request was not accepted for one of the following reasons.</span></span> <ul> <li><span data-ttu-id="44dd0-205">Le webhook a expiré.</span><span class="sxs-lookup"><span data-stu-id="44dd0-205">The webhook has expired.</span></span></li> <li><span data-ttu-id="44dd0-206">Le webhook est désactivé.</span><span class="sxs-lookup"><span data-stu-id="44dd0-206">The webhook is disabled.</span></span></li> <li><span data-ttu-id="44dd0-207">Le jeton de l’URL n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="44dd0-207">The token in the URL is invalid.</span></span></li>  </ul> |
| <span data-ttu-id="44dd0-208">404</span><span class="sxs-lookup"><span data-stu-id="44dd0-208">404</span></span> |<span data-ttu-id="44dd0-209">Introuvable</span><span class="sxs-lookup"><span data-stu-id="44dd0-209">Not Found</span></span> |<span data-ttu-id="44dd0-210">La demande a été refusée pour l'une des raisons suivantes.</span><span class="sxs-lookup"><span data-stu-id="44dd0-210">The request was not accepted for one of the following reasons.</span></span> <ul> <li><span data-ttu-id="44dd0-211">Le webhook est introuvable.</span><span class="sxs-lookup"><span data-stu-id="44dd0-211">The webhook was not found.</span></span></li> <li><span data-ttu-id="44dd0-212">Le Runbook est introuvable.</span><span class="sxs-lookup"><span data-stu-id="44dd0-212">The runbook was not found.</span></span></li> <li><span data-ttu-id="44dd0-213">Le compte est introuvable.</span><span class="sxs-lookup"><span data-stu-id="44dd0-213">The account was not found.</span></span></li>  </ul> |
| <span data-ttu-id="44dd0-214">500</span><span class="sxs-lookup"><span data-stu-id="44dd0-214">500</span></span> |<span data-ttu-id="44dd0-215">Erreur interne du serveur</span><span class="sxs-lookup"><span data-stu-id="44dd0-215">Internal Server Error</span></span> |<span data-ttu-id="44dd0-216">L'URL est valide, mais une erreur s'est produite.</span><span class="sxs-lookup"><span data-stu-id="44dd0-216">The URL was valid, but an error occurred.</span></span>  <span data-ttu-id="44dd0-217">Soumettez à nouveau la demande.</span><span class="sxs-lookup"><span data-stu-id="44dd0-217">Please resubmit the request.</span></span> |

<span data-ttu-id="44dd0-218">En supposant que la requête aboutisse, la réponse webhook contient l'ID de travail au format JSON comme suit.</span><span class="sxs-lookup"><span data-stu-id="44dd0-218">Assuming the request is successful, the webhook response contains the job id in JSON format as follows.</span></span> <span data-ttu-id="44dd0-219">Elle contient un ID de tâche unique, mais le format JSON permet des améliorations ultérieures potentielles.</span><span class="sxs-lookup"><span data-stu-id="44dd0-219">It will contain a single job id, but the JSON format allows for potential future enhancements.</span></span>

    {"JobIds":["<JobId>"]}  

<span data-ttu-id="44dd0-220">Le client ne peut pas déterminer l'issue du travail du Runbook ou de son état d'achèvement à partir du webhook.</span><span class="sxs-lookup"><span data-stu-id="44dd0-220">The client cannot determine when the runbook job completes or its completion status from the webhook.</span></span>  <span data-ttu-id="44dd0-221">Il peut déterminer ces informations à l’aide de l’ID de travail avec une autre méthode telle que [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) ou [API d’Azure Automation](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span><span class="sxs-lookup"><span data-stu-id="44dd0-221">It can determine this information using the job id with another method such as [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) or the [Azure Automation API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span></span>

### <a name="example"></a><span data-ttu-id="44dd0-222">Exemple</span><span class="sxs-lookup"><span data-stu-id="44dd0-222">Example</span></span>
<span data-ttu-id="44dd0-223">L'exemple suivant utilise Windows PowerShell pour démarrer un Runbook avec un webhook.</span><span class="sxs-lookup"><span data-stu-id="44dd0-223">The following example uses Windows PowerShell to start a runbook with a webhook.</span></span>  <span data-ttu-id="44dd0-224">Notez que n'importe quel langage qui peut effectuer une requête HTTP peut utiliser un webhook ; Windows PowerShell est uniquement utilisé ici à titre d'exemple.</span><span class="sxs-lookup"><span data-stu-id="44dd0-224">Note that any language that can make an HTTP request can use a webhook; Windows PowerShell is just used here as an example.</span></span>

<span data-ttu-id="44dd0-225">Le Runbook s'attend à une liste de machines virtuelles au format JSON dans le corps de la requête.</span><span class="sxs-lookup"><span data-stu-id="44dd0-225">The runbook is expecting a list of virtual machines formatted in JSON in the body of the request.</span></span> <span data-ttu-id="44dd0-226">Nous allons également inclure des informations sur qui démarre le Runbook, ainsi que la date et l'heure de son démarrage dans l'en-tête de la requête.</span><span class="sxs-lookup"><span data-stu-id="44dd0-226">We also are including information about who is starting the runbook and the date and time it is being started in the header of the request.</span></span>      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


<span data-ttu-id="44dd0-227">L'illustration suivante montre les informations d'en-tête (à l'aide d'un suivi [Fiddler](http://www.telerik.com/fiddler) ) à partir de cette requête.</span><span class="sxs-lookup"><span data-stu-id="44dd0-227">The following image shows the header information (using a [Fiddler](http://www.telerik.com/fiddler) trace) from this request.</span></span> <span data-ttu-id="44dd0-228">Cela inclut les en-têtes standard d'une requête HTTP en plus des en-têtes Date et De personnalisés que nous avons ajoutés.</span><span class="sxs-lookup"><span data-stu-id="44dd0-228">This includes standard headers of an HTTP request in addition to the custom Date and From headers that we added.</span></span>  <span data-ttu-id="44dd0-229">Chacune de ces valeurs est disponible pour le Runbook dans la propriété **RequestHeaders** de **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="44dd0-229">Each of these values is available to the runbook in the **RequestHeaders** property of **WebhookData**.</span></span>

![Bouton Webhooks](media/automation-webhooks/webhook-request-headers.png)

<span data-ttu-id="44dd0-231">L’illustration suivante montre le corps de la requête (à l’aide d’un suivi [Fiddler](http://www.telerik.com/fiddler)) qui est disponible pour le Runbook dans la propriété **RequestBody** de **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="44dd0-231">The following image shows the body of the request (using a [Fiddler](http://www.telerik.com/fiddler) trace)  that is available to the runbook in the **RequestBody** property of **WebhookData**.</span></span> <span data-ttu-id="44dd0-232">Il est au format JSON car il s'agit du format qui a été inclus dans le corps de la requête.</span><span class="sxs-lookup"><span data-stu-id="44dd0-232">This is formatted as JSON because that was the format that was included in the body of the request.</span></span>     

![Bouton Webhooks](media/automation-webhooks/webhook-request-body.png)

<span data-ttu-id="44dd0-234">L'illustration suivante montre la requête envoyée à partir de Windows PowerShell et sa réponse.</span><span class="sxs-lookup"><span data-stu-id="44dd0-234">The following image shows the request being sent from Windows PowerShell and the resulting response.</span></span>  <span data-ttu-id="44dd0-235">L'ID de travail est extrait de la réponse et converti en une chaîne.</span><span class="sxs-lookup"><span data-stu-id="44dd0-235">The job id is extracted from the response and converted to a string.</span></span>

![Bouton Webhooks](media/automation-webhooks/webhook-request-response.png)

<span data-ttu-id="44dd0-237">L’exemple suivant de runbook accepte la requête de l’exemple précédent et démarre les machines virtuelles spécifiées dans le corps de la requête.</span><span class="sxs-lookup"><span data-stu-id="44dd0-237">The following sample runbook accepts the previous example request and starts the virtual machines specified in the request body.</span></span>

    workflow Test-StartVirtualMachinesFromWebhook
    {
        param (
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {

            # Collect properties of WebhookData
            $WebhookName     =     $WebhookData.WebhookName
            $WebhookHeaders =     $WebhookData.RequestHeader
            $WebhookBody     =     $WebhookData.RequestBody

            # Collect individual headers. VMList converted from JSON.
            $From = $WebhookHeaders.From
            $VMList = ConvertFrom-Json -InputObject $WebhookBody
            Write-Output "Runbook started from webhook $WebhookName by $From."

            # Authenticate to Azure resources
            $Cred = Get-AutomationPSCredential -Name 'MyAzureCredential'
            Add-AzureAccount -Credential $Cred

            # Start each virtual machine
            foreach ($VM in $VMList)
            {
                $VMName = $VM.Name
                Write-Output "Starting $VMName"
                Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName
            }
        }
        else {
            Write-Error "Runbook mean to be started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-to-azure-alerts"></a><span data-ttu-id="44dd0-238">Démarrage de runbooks en réponse aux alertes Azure</span><span class="sxs-lookup"><span data-stu-id="44dd0-238">Starting runbooks in response to Azure alerts</span></span>
<span data-ttu-id="44dd0-239">Les runbooks webhook peuvent être utilisés pour réagir aux [alertes Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="44dd0-239">Webhook-enabled runbooks can be used to react to [Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="44dd0-240">Les ressources dans Azure peuvent être surveillées en collectant, au moyen d’alertes Azure, des statistiques telles que les performances, la disponibilité et l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="44dd0-240">Resources in Azure can be monitored by collecting the statistics like performance, availability and usage with the help of Azure alerts.</span></span> <span data-ttu-id="44dd0-241">Vous pouvez recevoir une alerte basée sur des métriques ou événements de surveillance pour vos ressources Azure ; actuellement les comptes Automation prennent uniquement en charge les métriques.</span><span class="sxs-lookup"><span data-stu-id="44dd0-241">You can receive an alert based on monitoring metrics or events for your Azure resources, currently Automation Accounts support only metrics.</span></span> <span data-ttu-id="44dd0-242">Quand la valeur d’une métrique spécifiée dépasse le seuil attribué ou si l’événement configuré est déclenché, une notification est envoyée à l’administrateur ou aux co-administrateurs du service pour résoudre l’alerte. Pour plus d’informations sur les métriques et les événements, reportez-vous aux [alertes Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="44dd0-242">When the value of a specified metric exceeds the threshold assigned or if the configured event is triggered then a notification is sent to the service admin or co-admins to resolve the alert, for more information on metrics and events please refer to [Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="44dd0-243">Outre l’utilisation des alertes Azure comme système de notification, vous pouvez aussi lancer des runbooks en réponse aux alertes.</span><span class="sxs-lookup"><span data-stu-id="44dd0-243">Besides using Azure alerts as a notification system, you can also kick off runbooks in response to alerts.</span></span> <span data-ttu-id="44dd0-244">Azure Automation vous permet d’exécuter des runbooks webhook compatibles avec les alertes Azure.</span><span class="sxs-lookup"><span data-stu-id="44dd0-244">Azure Automation provides the capability to run webhook-enabled runbooks with Azure alerts.</span></span> <span data-ttu-id="44dd0-245">Quand une métrique dépasse la valeur configurée du seuil, la règle d’alerte devient active et déclenche le webhook Automation qui, à son tour, exécute le runbook.</span><span class="sxs-lookup"><span data-stu-id="44dd0-245">When a metric exceeds the configured threshold value then the alert rule becomes active and triggers the automation webhook which in turn executes the runbook.</span></span>

![Webhooks](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a><span data-ttu-id="44dd0-247">Contexte de l’alerte</span><span class="sxs-lookup"><span data-stu-id="44dd0-247">Alert context</span></span>
<span data-ttu-id="44dd0-248">Prenons une ressource Azure, par exemple, une machine virtuelle. L’utilisation du processeur de cette machine est l’une des principales métriques de performance.</span><span class="sxs-lookup"><span data-stu-id="44dd0-248">Consider an Azure resource such as a virtual machine, CPU utilization of this machine is one of the key performance metric.</span></span> <span data-ttu-id="44dd0-249">Si l’utilisation du processeur est de 100 % ou qu’elle est supérieure à une certaine quantité pendant une longue période de temps, vous voudrez probablement redémarrer la machine virtuelle pour résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="44dd0-249">If the CPU utilization is 100% or more than a certain amount for long period of time, you might want to restart the virtual machine to fix the problem.</span></span> <span data-ttu-id="44dd0-250">Pour ce faire, vous pouvez configurer une règle d’alerte sur la machine virtuelle avec le pourcentage UC en guise de métrique.</span><span class="sxs-lookup"><span data-stu-id="44dd0-250">This can be solved by configuring an alert rule to the virtual machine and this rule takes CPU percentage as its metric.</span></span> <span data-ttu-id="44dd0-251">Dans ce scénario, le pourcentage UC est choisi à titre d’exemple, mais vous pouvez configurer beaucoup d’autres métriques pour vos ressources Azure. De même, le redémarrage de la machine virtuelle est l’action choisie pour résoudre ce problème, mais vous pouvez configurer le runbook pour exécuter d’autres actions.</span><span class="sxs-lookup"><span data-stu-id="44dd0-251">CPU percentage here is just taken as an example but there are many other metrics that you can configure to your Azure resources and restarting the virtual machine is an action that is taken to fix this issue, you can configure the runbook to take other actions.</span></span>

<span data-ttu-id="44dd0-252">Quand cette règle d’alerte devient active et déclenche le runbook webhook, elle envoie le contexte de l’alerte au runbook.</span><span class="sxs-lookup"><span data-stu-id="44dd0-252">When this the alert rule becomes active and triggers the webhook-enabled runbook, it sends the alert context to the runbook.</span></span> <span data-ttu-id="44dd0-253">Le [contexte de l’alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contient des informations, notamment **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** et **Timestamp**, qui sont utilisées par le Runbook pour identifier la ressource sur laquelle il doit exécuter une action.</span><span class="sxs-lookup"><span data-stu-id="44dd0-253">[Alert context](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contains details including **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** and **Timestamp** which are required for the runbook to identify the resource on which it will be taking action.</span></span> <span data-ttu-id="44dd0-254">Le contexte de l’alerte est incorporé dans le corps de l’objet **WebhookData** envoyé au runbook, et il est accessible avec la propriété **Webhook.RequestBody**</span><span class="sxs-lookup"><span data-stu-id="44dd0-254">Alert context is embedded in the body part of the **WebhookData** object sent to the runbook and it can be accessed with **Webhook.RequestBody** property</span></span>

### <a name="example"></a><span data-ttu-id="44dd0-255">Exemple</span><span class="sxs-lookup"><span data-stu-id="44dd0-255">Example</span></span>
<span data-ttu-id="44dd0-256">Créez une machine virtuelle Azure dans votre abonnement, puis associez une [alerte pour surveiller la métrique du pourcentage UC](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="44dd0-256">Create an Azure virtual machine in your subscription and associate an [alert to monitor CPU percentage metric](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="44dd0-257">Quand vous créez l’alerte, veillez à remplir le champ webhook par l’URL du webhook qui a été générée pendant la création de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="44dd0-257">While creating the alert make sure you populate the webhook field with the URL of the webhook which was generated while creating the webhook.</span></span>

<span data-ttu-id="44dd0-258">L’exemple de runbook suivant est déclenché quand la règle d’alerte devient active et collecte les paramètres de contexte de l’alerte qui servent au runbook pour identifier la ressource sur laquelle il devra exécuter une action.</span><span class="sxs-lookup"><span data-stu-id="44dd0-258">The following sample runbook is triggered when the alert rule becomes active and it collects the Alert context parameters which are required for the runbook to identify the resource on which it will be taking action.</span></span>

    workflow Invoke-RunbookUsingAlerts
    {
        param (      
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {   
            # Collect properties of WebhookData.
            $WebhookName    =   $WebhookData.WebhookName
            $WebhookBody    =   $WebhookData.RequestBody
            $WebhookHeaders =   $WebhookData.RequestHeader

            # Outputs information on the webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain the WebhookBody containing the AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain the AlertContext     
            $AlertContext = [object]$WebhookBody.context

            # Some selected AlertContext information
            Write-Output "`nALERT CONTEXT DATA"
            Write-Output "==================="
            Write-Output $AlertContext.name
            Write-Output $AlertContext.subscriptionId
            Write-Output $AlertContext.resourceGroupName
            Write-Output $AlertContext.resourceName
            Write-Output $AlertContext.resourceType
            Write-Output $AlertContext.resourceId
            Write-Output $AlertContext.timestamp

            # Act on the AlertContext data, in our case restarting the VM.
            # Authenticate to your Azure subscription using Organization ID to be able to restart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check the status property of the VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart the VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant to only be started from a webhook."  
        }  
    }



## <a name="next-steps"></a><span data-ttu-id="44dd0-259">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="44dd0-259">Next steps</span></span>
* <span data-ttu-id="44dd0-260">Pour plus d’informations sur les différentes façons de démarrer un runbook, consultez l’article [Démarrage d’un Runbook](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="44dd0-260">For details on different ways to start a runbook, see [Starting a Runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="44dd0-261">Pour plus d’informations sur l’affichage de l’état d’un travail de runbook, consultez l’article [Exécution d’un Runbook dans Azure Automation](automation-runbook-execution.md).</span><span class="sxs-lookup"><span data-stu-id="44dd0-261">For information on viewing the Status of a Runbook Job, refer to [Runbook execution in Azure Automation](automation-runbook-execution.md).</span></span>
* <span data-ttu-id="44dd0-262">Pour découvrir comment utiliser Azure Automation pour gérer les alertes Azure, consultez l’article [Résoudre des alertes de machine virtuelle Azure avec des Runbooks Automation](automation-azure-vm-alert-integration.md).</span><span class="sxs-lookup"><span data-stu-id="44dd0-262">To learn how to use Azure Automation to take action on Azure Alerts, see [Remediate Azure VM Alerts with Automation Runbooks](automation-azure-vm-alert-integration.md).</span></span>
