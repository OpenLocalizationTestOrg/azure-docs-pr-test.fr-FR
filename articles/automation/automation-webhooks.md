---
title: aaaStarting un runbook Azure Automation avec un webhook | Documents Microsoft
description: "Un webhook qui permet à un client toostart un runbook dans Azure Automation à partir d’un appel HTTP.  Cet article décrit comment toocreate un webhook et comment toostart d’un toocall un runbook."
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
ms.openlocfilehash: ca6cde66b3784ceb5d0bc5921cee87aea74cb150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a><span data-ttu-id="c1fe4-104">Démarrage d’un runbook Azure Automation avec un webhook</span><span class="sxs-lookup"><span data-stu-id="c1fe4-104">Starting an Azure Automation runbook with a webhook</span></span>
<span data-ttu-id="c1fe4-105">A *webhook* vous permet de toostart un runbook donné dans Azure Automation via une requête HTTP unique.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-105">A *webhook* allows you toostart a particular runbook in Azure Automation through a single HTTP request.</span></span> <span data-ttu-id="c1fe4-106">Cela permet à des services externes tels que Visual Studio Team Services, GitHub, Analytique de journal de Microsoft Operations Management Suite ou des applications personnalisées toostart runbooks sans avoir à implémenter une solution complète à l’aide de hello API Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-106">This allows external services such as Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analytics, or custom applications toostart runbooks without implementing a full solution using hello Azure Automation API.</span></span>  
<span data-ttu-id="c1fe4-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span><span class="sxs-lookup"><span data-stu-id="c1fe4-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span></span>

<span data-ttu-id="c1fe4-108">Vous pouvez comparer des méthodes de tooother webhooks de démarrage d’un runbook [démarrage d’un runbook dans Azure Automation](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="c1fe4-108">You can compare webhooks tooother methods of starting a runbook in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md)</span></span>

## <a name="details-of-a-webhook"></a><span data-ttu-id="c1fe4-109">Détails d'un webhook</span><span class="sxs-lookup"><span data-stu-id="c1fe4-109">Details of a webhook</span></span>
<span data-ttu-id="c1fe4-110">Hello tableau suivant décrit les propriétés hello que vous devez configurer pour un webhook.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-110">hello following table describes hello properties that you must configure for a webhook.</span></span>

| <span data-ttu-id="c1fe4-111">Propriété</span><span class="sxs-lookup"><span data-stu-id="c1fe4-111">Property</span></span> | <span data-ttu-id="c1fe4-112">Description</span><span class="sxs-lookup"><span data-stu-id="c1fe4-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1fe4-113">Nom</span><span class="sxs-lookup"><span data-stu-id="c1fe4-113">Name</span></span> |<span data-ttu-id="c1fe4-114">Vous pouvez fournir le nom de que votre choix pour un webhook car il s’agit pas exposées toohello client.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-114">You can provide any name you want for a webhook since this is not exposed toohello client.</span></span>  <span data-ttu-id="c1fe4-115">Elle est utilisée uniquement pour vous tooidentify hello runbook dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-115">It is only used for you tooidentify hello runbook in Azure Automation.</span></span> <br>  <span data-ttu-id="c1fe4-116">Comme meilleure pratique, vous devez donner hello webhook un client nom toohello connexes qui l’utilise.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-116">As a best practice, you should give hello webhook a name related toohello client that will use it.</span></span> |
| <span data-ttu-id="c1fe4-117">URL</span><span class="sxs-lookup"><span data-stu-id="c1fe4-117">URL</span></span> |<span data-ttu-id="c1fe4-118">URL de Hello de hello webhook est adresse unique de hello qu’un client appelle avec un runbook de hello HTTP POST toostart lié toohello webhook.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-118">hello URL of hello webhook is hello unique address that a client calls with an HTTP POST toostart hello runbook linked toohello webhook.</span></span>  <span data-ttu-id="c1fe4-119">Il est généré automatiquement lorsque vous créez hello webhook.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-119">It is automatically generated when you create hello webhook.</span></span>  <span data-ttu-id="c1fe4-120">Vous ne pouvez pas spécifier d'URL personnalisée.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-120">You cannot specify a custom URL.</span></span> <br> <br>  <span data-ttu-id="c1fe4-121">URL de Hello contient un jeton de sécurité qui permet de hello runbook toobe est appelée par un système tiers avec aucune authentification supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-121">hello URL contains a security token that allows hello runbook toobe invoked by a third party system with no further authentication.</span></span> <span data-ttu-id="c1fe4-122">Pour cette raison, elle doit être traitée comme un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-122">For this reason, it should be treated like a password.</span></span>  <span data-ttu-id="c1fe4-123">Pour des raisons de sécurité, vous pouvez uniquement les hello affichage QU'URL Bonjour Azure portal à hello temps hello webhook est créé.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-123">For security reasons, you can only view hello URL in hello Azure portal at hello time hello webhook is created.</span></span> <span data-ttu-id="c1fe4-124">Notez l’URL hello dans un emplacement sécurisé pour un usage ultérieur.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-124">You should note hello URL in a secure location for future use.</span></span> |
| <span data-ttu-id="c1fe4-125">Date d'expiration</span><span class="sxs-lookup"><span data-stu-id="c1fe4-125">Expiration date</span></span> |<span data-ttu-id="c1fe4-126">Comme un certificat, chaque webhook possède une date d'expiration à partir de laquelle il ne peut plus être utilisé.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-126">Like a certificate, each webhook has an expiration date at which time it can no longer be used.</span></span>  <span data-ttu-id="c1fe4-127">Cette date d’expiration peut être modifiée après la création de hello webhook.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-127">This expiration date can be modified after hello webhook is created.</span></span> |
| <span data-ttu-id="c1fe4-128">Activé</span><span class="sxs-lookup"><span data-stu-id="c1fe4-128">Enabled</span></span> |<span data-ttu-id="c1fe4-129">Un webhook est activé par défaut lorsqu'il est créé.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-129">A webhook is enabled by default when it is created.</span></span>  <span data-ttu-id="c1fe4-130">Si vous lui affectez tooDisabled, aucun client ne peut être en mesure de toouse il.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-130">If you set it tooDisabled, then no client will be able toouse it.</span></span>  <span data-ttu-id="c1fe4-131">Vous pouvez définir hello **activé** propriété lorsque vous créez hello webhook ou à tout moment une fois qu’il est créée.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-131">You can set hello **Enabled** property when you create hello webhook or anytime once it is created.</span></span> |

### <a name="parameters"></a><span data-ttu-id="c1fe4-132">Paramètres</span><span class="sxs-lookup"><span data-stu-id="c1fe4-132">Parameters</span></span>
<span data-ttu-id="c1fe4-133">Un webhook peut définir les valeurs des paramètres de runbook qui sont utilisés quand hello runbook est démarrée par ce webhook.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-133">A webhook can define values for runbook parameters that are used when hello runbook is started by that webhook.</span></span> <span data-ttu-id="c1fe4-134">Hello webhook doit inclure des valeurs pour tous les paramètres obligatoires du runbook de hello et peut-être inclure des valeurs pour les paramètres optionnels.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-134">hello webhook must include values for any mandatory parameters of hello runbook and may include values for optional parameters.</span></span> <span data-ttu-id="c1fe4-135">Un webhook de tooa de valeur configurée de paramètre peut être modifié même après la création de hello webhoook.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-135">A parameter value configured tooa webhook can be modified even after creating hello webhoook.</span></span> <span data-ttu-id="c1fe4-136">Plusieurs webhooks lié tooa unique runbook peut utiliser différentes valeurs de paramètre.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-136">Multiple webhooks linked tooa single runbook can each use different parameter values.</span></span>

<span data-ttu-id="c1fe4-137">Lorsqu’un client démarre un runbook à l’aide d’un webhook, il ne peut pas remplacer les valeurs de paramètre hello définies dans hello webhook.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-137">When a client starts a runbook using a webhook, it cannot override hello parameter values defined in hello webhook.</span></span>  <span data-ttu-id="c1fe4-138">tooreceive des données à partir du client de hello, hello runbook peut accepter un paramètre unique appelé **$WebhookData** de type (objet) qui contiendra les données que le client hello inclut dans la demande POST hello.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-138">tooreceive data from hello client, hello runbook can accept a single parameter called **$WebhookData** of type [object] that will contain data that hello client includes in hello POST request.</span></span>

![Propriétés Webhookdata](media/automation-webhooks/webhook-data-properties.png)

<span data-ttu-id="c1fe4-140">Hello **$WebhookData** objet aura hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="c1fe4-140">hello **$WebhookData** object will have hello following properties:</span></span>

| <span data-ttu-id="c1fe4-141">Propriété</span><span class="sxs-lookup"><span data-stu-id="c1fe4-141">Property</span></span> | <span data-ttu-id="c1fe4-142">Description</span><span class="sxs-lookup"><span data-stu-id="c1fe4-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1fe4-143">WebhookName</span><span class="sxs-lookup"><span data-stu-id="c1fe4-143">WebhookName</span></span> |<span data-ttu-id="c1fe4-144">nom de Hello de hello webhook.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-144">hello name of hello webhook.</span></span> |
| <span data-ttu-id="c1fe4-145">RequestHeader</span><span class="sxs-lookup"><span data-stu-id="c1fe4-145">RequestHeader</span></span> |<span data-ttu-id="c1fe4-146">Table de hachage qui contient des en-têtes de hello de requête de publication entrant hello.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-146">Hash table containing hello headers of hello incoming POST request.</span></span> |
| <span data-ttu-id="c1fe4-147">RequestBody</span><span class="sxs-lookup"><span data-stu-id="c1fe4-147">RequestBody</span></span> |<span data-ttu-id="c1fe4-148">corps Hello de requête de publication entrant hello.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-148">hello body of hello incoming POST request.</span></span>  <span data-ttu-id="c1fe4-149">Ceci conserve les mises en forme telles que les chaînes, JSON, XML ou les données de formulaire codées.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-149">This will retain any formatting such as string, JSON, XML, or form encoded data.</span></span> <span data-ttu-id="c1fe4-150">Hello runbook doit être écrites toowork au format de données hello est attendu.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-150">hello runbook must be written toowork with hello data format that is expected.</span></span> |

<span data-ttu-id="c1fe4-151">Aucune configuration de hello de hello webhook toosupport requis est **$WebhookData** paramètre, et hello runbook n’est pas requis tooaccept il.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-151">There is no configuration of hello webhook required toosupport hello **$WebhookData** parameter, and hello runbook is not required tooaccept it.</span></span>  <span data-ttu-id="c1fe4-152">Si les runbook hello ne définit pas de paramètre hello, tous les détails de demande hello envoyés à partir du client de hello est ignoré.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-152">If hello runbook does not define hello parameter, then any details of hello request sent from hello client is ignored.</span></span>

<span data-ttu-id="c1fe4-153">Si vous spécifiez une valeur pour $WebhookData lorsque vous créez hello webhook, cette valeur sera remplacée au démarrage hello webhook hello runbook avec des données hello de demande de publication hello client, même si le client de hello n’inclut pas de données dans le corps de la demande hello.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-153">If you specify a value for $WebhookData when you create hello webhook, that value will be overriden when hello webhook starts hello runbook with hello data from hello client POST request, even if hello client does not include any data in hello request body.</span></span>  <span data-ttu-id="c1fe4-154">Si vous démarrez un runbook qui a $WebhookData à l’aide d’une méthode autre qu’un webhook, vous pouvez fournir une valeur pour $Webhookdata qui peut être reconnu par les runbook hello.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-154">If you start a runbook that has $WebhookData using a method other than a webhook, you can provide a value for $Webhookdata that will be recognized by hello runbook.</span></span>  <span data-ttu-id="c1fe4-155">Cette valeur doit être un objet avec hello même [propriétés](#details-of-a-webhook) comme $Webhookdata afin que runbook hello correctement les utiliser comme s’il fonctionnait avec WebhookData réel passé par un webhook.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-155">This value should be an object with hello same [properties](#details-of-a-webhook) as $Webhookdata so that hello runbook can properly work with it as if it was working with actual WebhookData passed by a webhook.</span></span>

<span data-ttu-id="c1fe4-156">Par exemple, si vous démarrez hello suivant runbook hello portail Azure et que vous souhaitez toopass certains exemples WebhookData de test, étant donné que WebhookData est un objet, il doit être passé au format JSON hello l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-156">For example, if you are starting hello following runbook from hello Azure Portal and want toopass some sample WebhookData for testing, since WebhookData is an object, it should be passed as JSON in hello UI.</span></span>

![Paramètre WebhookData à partir de l'interface utilisateur](media/automation-webhooks/WebhookData-parameter-from-UI.png)

<span data-ttu-id="c1fe4-158">Pourquoi au-dessus de runbook, si vous avez hello propriétés pour le paramètre de WebhookData hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="c1fe4-158">For hello above runbook, if you have hello following properties for hello WebhookData parameter:</span></span>

1. <span data-ttu-id="c1fe4-159">WebhookName: *MyWebhook*</span><span class="sxs-lookup"><span data-stu-id="c1fe4-159">WebhookName: *MyWebhook*</span></span>
2. <span data-ttu-id="c1fe4-160">RequestHeader: *From=Test User*</span><span class="sxs-lookup"><span data-stu-id="c1fe4-160">RequestHeader: *From=Test User*</span></span>
3. <span data-ttu-id="c1fe4-161">RequestBody: *[“VM1”, “VM2”]*</span><span class="sxs-lookup"><span data-stu-id="c1fe4-161">RequestBody: *[“VM1”, “VM2”]*</span></span>

<span data-ttu-id="c1fe4-162">Vous pouvez ensuite transmettre hello valeur JSON Bonjour l’interface utilisateur pour le paramètre de WebhookData hello suivante :</span><span class="sxs-lookup"><span data-stu-id="c1fe4-162">Then you would pass hello following JSON value in hello UI for hello WebhookData parameter:</span></span>  

* <span data-ttu-id="c1fe4-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span><span class="sxs-lookup"><span data-stu-id="c1fe4-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span></span>

![Démarrage du paramètre WebhookData à partir de l'interface utilisateur](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> <span data-ttu-id="c1fe4-165">les valeurs de Hello de tous les paramètres d’entrée sont enregistrées avec la tâche du runbook hello.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-165">hello values of all input parameters are logged with hello runbook job.</span></span>  <span data-ttu-id="c1fe4-166">Cela signifie que les entrées fournies par le client hello dans la demande de webhook hello sera tooanyone connecté et disponible avec la tâche d’automatisation toohello accès.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-166">This means that any input provided by hello client in hello webhook request will be logged and available tooanyone with access toohello automation job.</span></span>  <span data-ttu-id="c1fe4-167">Pour cette raison, soyez prudent lorsque vous incluez des informations sensibles dans les appels du webhook.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-167">For this reason, you should be cautious about including sensitive information in webhook calls.</span></span>
>

## <a name="security"></a><span data-ttu-id="c1fe4-168">Sécurité</span><span class="sxs-lookup"><span data-stu-id="c1fe4-168">Security</span></span>
<span data-ttu-id="c1fe4-169">sécurité Hello d’un webhook s’appuie sur la confidentialité hello de son URL qui contient un jeton de sécurité qui lui permet de toobe appelé.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-169">hello security of a webhook relies on hello privacy of its URL which contains a security token that allows it toobe invoked.</span></span> <span data-ttu-id="c1fe4-170">Azure Automation n’effectue pas d’authentification à la demande de hello tant que rend toohello l’URL appropriée.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-170">Azure Automation does not perform any authentication on hello request as long as it is made toohello correct URL.</span></span> <span data-ttu-id="c1fe4-171">Pour cette raison, webhooks ne doit pas servir de runbook qui exécutent des fonctions très sensibles sans utiliser un autre moyen de la validation de demande de hello.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-171">For this reason, webhooks should not be used for runbooks that perform highly sensitive functions without using an alternate means of validating hello request.</span></span>

<span data-ttu-id="c1fe4-172">Vous pouvez inclure une logique dans hello toodetermine de runbook qu’elle a été appelée par un webhook en vérifiant hello **WebhookName** propriété de paramètre hello $WebhookData.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-172">You can include logic within hello runbook toodetermine that it was called by a webhook by checking hello **WebhookName** property of hello $WebhookData parameter.</span></span> <span data-ttu-id="c1fe4-173">Hello runbook peut effectuer une validation supplémentaire en recherchant des informations spécifiques contenues dans hello **RequestHeader** ou **RequestBody** propriétés.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-173">hello runbook could perform further validation by looking for particular information in hello **RequestHeader** or **RequestBody** properties.</span></span>

<span data-ttu-id="c1fe4-174">Une autre stratégie consiste à toohave hello runbook effectuer une validation d’une condition externe lorsqu’il a reçu une demande de webhook.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-174">Another strategy is toohave hello runbook perform some validation of an external condition when it received a webhook request.</span></span>  <span data-ttu-id="c1fe4-175">Par exemple, considérez un runbook qui est appelé par GitHub chaque fois qu’il existe un référentiel GitHub tooa validation.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-175">For example, consider a runbook that is called by GitHub whenever there is a new commit tooa GitHub repository.</span></span>  <span data-ttu-id="c1fe4-176">Hello runbook risquent de se connecter toovalidate de tooGitHub une nouvelle validation s’est produite en fait juste avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-176">hello runbook might connect tooGitHub toovalidate that a new commit had actually just occurred before continuing.</span></span>

## <a name="creating-a-webhook"></a><span data-ttu-id="c1fe4-177">Création d'un webhook</span><span class="sxs-lookup"><span data-stu-id="c1fe4-177">Creating a webhook</span></span>
<span data-ttu-id="c1fe4-178">Utilisez hello suivant la procédure toocreate un runbook tooa webhook lié Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-178">Use hello following procedure toocreate a new webhook linked tooa runbook in hello Azure portal.</span></span>

1. <span data-ttu-id="c1fe4-179">À partir de hello **Runbooks panneau** Bonjour portail Azure, cliquez sur runbook hello hello webhook démarrera tooview son panneau de détails.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-179">From hello **Runbooks blade** in hello Azure portal, click hello runbook that hello webhook will start tooview its detail blade.</span></span>
2. <span data-ttu-id="c1fe4-180">Cliquez sur **Webhook** haut hello hello de hello panneau tooopen **ajouter un Webhook** panneau.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-180">Click **Webhook** at hello top of hello blade tooopen hello **Add Webhook** blade.</span></span> <br><span data-ttu-id="c1fe4-181">
   ![Bouton Webhooks](media/automation-webhooks/webhooks-button.png)</span><span class="sxs-lookup"><span data-stu-id="c1fe4-181">
![Webhooks button](media/automation-webhooks/webhooks-button.png)</span></span>
3. <span data-ttu-id="c1fe4-182">Cliquez sur **créer nouveau webhook** tooopen hello **créer webhook panneau**.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-182">Click **Create new webhook** tooopen hello **Create webhook blade**.</span></span>
4. <span data-ttu-id="c1fe4-183">Spécifiez un **nom**, **Date d’Expiration** pour hello webhook et si elle doit être activée.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-183">Specify a **Name**, **Expiration Date** for hello webhook and whether it should be enabled.</span></span> <span data-ttu-id="c1fe4-184">Pour plus d'informations sur ces propriétés, consultez [Détails d'un webhook](#details-of-a-webhook) .</span><span class="sxs-lookup"><span data-stu-id="c1fe4-184">See [Details of a webhook](#details-of-a-webhook) for more information these properties.</span></span>
5. <span data-ttu-id="c1fe4-185">Cliquez sur icône de copie hello et appuyez sur Ctrl + C toocopy hello URL de hello webhook.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-185">Click hello copy icon and press Ctrl+C toocopy hello URL of hello webhook.</span></span>  <span data-ttu-id="c1fe4-186">Puis enregistrez-la dans un endroit sûr.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-186">Then record it in a safe place.</span></span>  <span data-ttu-id="c1fe4-187">**Une fois que vous créez hello webhook, vous ne pouvez pas récupérer l’URL de hello à nouveau.**</span><span class="sxs-lookup"><span data-stu-id="c1fe4-187">**Once you create hello webhook, you cannot retrieve hello URL again.**</span></span> <br><span data-ttu-id="c1fe4-188">
   ![URL du webhook](media/automation-webhooks/copy-webhook-url.png)</span><span class="sxs-lookup"><span data-stu-id="c1fe4-188">
![Webhook URL](media/automation-webhooks/copy-webhook-url.png)</span></span>
6. <span data-ttu-id="c1fe4-189">Cliquez sur **paramètres** tooprovide les valeurs des paramètres de runbook hello.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-189">Click **Parameters** tooprovide values for hello runbook parameters.</span></span>  <span data-ttu-id="c1fe4-190">Si hello runbook a des paramètres obligatoires, puis vous ne serez pas en mesure de toocreate hello webhook, sauf si les valeurs sont fournies.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-190">If hello runbook has mandatory parameters, then you will not be able toocreate hello webhook unless values are provided.</span></span>
7. <span data-ttu-id="c1fe4-191">Cliquez sur **créer** toocreate hello webhook.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-191">Click **Create** toocreate hello webhook.</span></span>

## <a name="using-a-webhook"></a><span data-ttu-id="c1fe4-192">Utilisation d'un webhook</span><span class="sxs-lookup"><span data-stu-id="c1fe4-192">Using a webhook</span></span>
<span data-ttu-id="c1fe4-193">toouse un webhook après que qu’il a été créé, votre application cliente doit émettre une requête HTTP POST avec l’URL de hello hello webhook.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-193">toouse a webhook after it has been created, your client application must issue an HTTP POST with hello URL for hello webhook.</span></span>  <span data-ttu-id="c1fe4-194">syntaxe de Hello de hello webhook sera Bonjour suivant le format.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-194">hello syntax of hello webhook will be in hello following format.</span></span>

    http://<Webhook Server>/token?=<Token Value>

<span data-ttu-id="c1fe4-195">Hello client reçoit un des hello suivant des codes de retour de demande de publication hello.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-195">hello client will receive one of hello following return codes from hello POST request.</span></span>  

| <span data-ttu-id="c1fe4-196">Code</span><span class="sxs-lookup"><span data-stu-id="c1fe4-196">Code</span></span> | <span data-ttu-id="c1fe4-197">Texte</span><span class="sxs-lookup"><span data-stu-id="c1fe4-197">Text</span></span> | <span data-ttu-id="c1fe4-198">Description</span><span class="sxs-lookup"><span data-stu-id="c1fe4-198">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="c1fe4-199">202</span><span class="sxs-lookup"><span data-stu-id="c1fe4-199">202</span></span> |<span data-ttu-id="c1fe4-200">Acceptée</span><span class="sxs-lookup"><span data-stu-id="c1fe4-200">Accepted</span></span> |<span data-ttu-id="c1fe4-201">Hello demande a été acceptée et hello runbook a été correctement en file d’attente.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-201">hello request was accepted, and hello runbook was successfully queued.</span></span> |
| <span data-ttu-id="c1fe4-202">400</span><span class="sxs-lookup"><span data-stu-id="c1fe4-202">400</span></span> |<span data-ttu-id="c1fe4-203">Demande incorrecte</span><span class="sxs-lookup"><span data-stu-id="c1fe4-203">Bad Request</span></span> |<span data-ttu-id="c1fe4-204">demande de Hello n’a pas été acceptée pour l’une des hello suivant raisons.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-204">hello request was not accepted for one of hello following reasons.</span></span> <ul> <li><span data-ttu-id="c1fe4-205">Hello webhook a expiré.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-205">hello webhook has expired.</span></span></li> <li><span data-ttu-id="c1fe4-206">Hello webhook est désactivé.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-206">hello webhook is disabled.</span></span></li> <li><span data-ttu-id="c1fe4-207">jeton Hello dans hello URL n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-207">hello token in hello URL is invalid.</span></span></li>  </ul> |
| <span data-ttu-id="c1fe4-208">404</span><span class="sxs-lookup"><span data-stu-id="c1fe4-208">404</span></span> |<span data-ttu-id="c1fe4-209">Introuvable</span><span class="sxs-lookup"><span data-stu-id="c1fe4-209">Not Found</span></span> |<span data-ttu-id="c1fe4-210">demande de Hello n’a pas été acceptée pour l’une des hello suivant raisons.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-210">hello request was not accepted for one of hello following reasons.</span></span> <ul> <li><span data-ttu-id="c1fe4-211">Hello webhook est introuvable.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-211">hello webhook was not found.</span></span></li> <li><span data-ttu-id="c1fe4-212">Hello runbook est introuvable.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-212">hello runbook was not found.</span></span></li> <li><span data-ttu-id="c1fe4-213">Impossible de trouver le compte de Hello.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-213">hello account was not found.</span></span></li>  </ul> |
| <span data-ttu-id="c1fe4-214">500</span><span class="sxs-lookup"><span data-stu-id="c1fe4-214">500</span></span> |<span data-ttu-id="c1fe4-215">Erreur interne du serveur</span><span class="sxs-lookup"><span data-stu-id="c1fe4-215">Internal Server Error</span></span> |<span data-ttu-id="c1fe4-216">URL de Hello était valide, mais une erreur s’est produite.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-216">hello URL was valid, but an error occurred.</span></span>  <span data-ttu-id="c1fe4-217">Soumettez la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-217">Please resubmit hello request.</span></span> |

<span data-ttu-id="c1fe4-218">En supposant que hello demande réussit, la réponse de webhook hello contient les id de tâche hello au format JSON comme suit.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-218">Assuming hello request is successful, hello webhook response contains hello job id in JSON format as follows.</span></span> <span data-ttu-id="c1fe4-219">Il contient un id de tâche unique, mais permet de format JSON de hello pour les améliorations futures potentielles.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-219">It will contain a single job id, but hello JSON format allows for potential future enhancements.</span></span>

    {"JobIds":["<JobId>"]}  

<span data-ttu-id="c1fe4-220">Impossible de déterminer les client Hello hello runbook tâche se termine ou son état d’achèvement de hello webhook.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-220">hello client cannot determine when hello runbook job completes or its completion status from hello webhook.</span></span>  <span data-ttu-id="c1fe4-221">Il peut déterminer ces informations à l’aide d’id de tâche hello avec une autre méthode comme [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) ou hello [API Azure Automation](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span><span class="sxs-lookup"><span data-stu-id="c1fe4-221">It can determine this information using hello job id with another method such as [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) or hello [Azure Automation API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span></span>

### <a name="example"></a><span data-ttu-id="c1fe4-222">Exemple</span><span class="sxs-lookup"><span data-stu-id="c1fe4-222">Example</span></span>
<span data-ttu-id="c1fe4-223">Bonjour à l’exemple suivant utilise Windows PowerShell toostart un runbook avec un webhook.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-223">hello following example uses Windows PowerShell toostart a runbook with a webhook.</span></span>  <span data-ttu-id="c1fe4-224">Notez que n'importe quel langage qui peut effectuer une requête HTTP peut utiliser un webhook ; Windows PowerShell est uniquement utilisé ici à titre d'exemple.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-224">Note that any language that can make an HTTP request can use a webhook; Windows PowerShell is just used here as an example.</span></span>

<span data-ttu-id="c1fe4-225">Hello runbook attend une liste d’ordinateurs virtuels au format JSON dans des corps de hello de demande de hello.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-225">hello runbook is expecting a list of virtual machines formatted in JSON in hello body of hello request.</span></span> <span data-ttu-id="c1fe4-226">Nous allons également inclure des informations qui démarre hello runbook et hello date et l’heure en cours de démarrage dans l’en-tête hello de demande de hello.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-226">We also are including information about who is starting hello runbook and hello date and time it is being started in hello header of hello request.</span></span>      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


<span data-ttu-id="c1fe4-227">Hello image suivante montre les informations d’en-tête hello (à l’aide un [Fiddler](http://www.telerik.com/fiddler) trace) à partir de cette demande.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-227">hello following image shows hello header information (using a [Fiddler](http://www.telerik.com/fiddler) trace) from this request.</span></span> <span data-ttu-id="c1fe4-228">Cela inclut les en-têtes standard d’une requête HTTP dans Ajout toohello Date personnalisé et des en-têtes que nous avons ajouté.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-228">This includes standard headers of an HTTP request in addition toohello custom Date and From headers that we added.</span></span>  <span data-ttu-id="c1fe4-229">Chacune de ces valeurs est runbook toohello disponible Bonjour **RequestHeaders** propriété du **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-229">Each of these values is available toohello runbook in hello **RequestHeaders** property of **WebhookData**.</span></span>

![Bouton Webhooks](media/automation-webhooks/webhook-request-headers.png)

<span data-ttu-id="c1fe4-231">Hello image suivante montre les corps de hello de demande de hello (à l’aide un [Fiddler](http://www.telerik.com/fiddler) trace) qui est disponible toohello runbook Bonjour **RequestBody** propriété du **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-231">hello following image shows hello body of hello request (using a [Fiddler](http://www.telerik.com/fiddler) trace)  that is available toohello runbook in hello **RequestBody** property of **WebhookData**.</span></span> <span data-ttu-id="c1fe4-232">Il est mis en forme en tant que JSON car il s’agit de format hello qui était inclus dans le corps de hello de demande de hello.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-232">This is formatted as JSON because that was hello format that was included in hello body of hello request.</span></span>     

![Bouton Webhooks](media/automation-webhooks/webhook-request-body.png)

<span data-ttu-id="c1fe4-234">Hello image suivante illustre les demande hello envoyé à partir de Windows PowerShell et les réponses hello.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-234">hello following image shows hello request being sent from Windows PowerShell and hello resulting response.</span></span>  <span data-ttu-id="c1fe4-235">id de tâche Hello est extraite de la réponse de hello et de chaîne de tooa converti.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-235">hello job id is extracted from hello response and converted tooa string.</span></span>

![Bouton Webhooks](media/automation-webhooks/webhook-request-response.png)

<span data-ttu-id="c1fe4-237">Bonjour exemple de runbook suivant accepte hello précédent exemple de demande et démarre les ordinateurs virtuels de hello spécifiés dans le corps de la demande hello.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-237">hello following sample runbook accepts hello previous example request and starts hello virtual machines specified in hello request body.</span></span>

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

            # Authenticate tooAzure resources
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
            Write-Error "Runbook mean toobe started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-tooazure-alerts"></a><span data-ttu-id="c1fe4-238">À partir de procédures opérationnelles alertes de réponse de tooAzure</span><span class="sxs-lookup"><span data-stu-id="c1fe4-238">Starting runbooks in response tooAzure alerts</span></span>
<span data-ttu-id="c1fe4-239">Compatible Webhook les procédures opérationnelles peut être utilisé tooreact trop[alertes Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="c1fe4-239">Webhook-enabled runbooks can be used tooreact too[Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="c1fe4-240">Ressources dans Azure peuvent être surveillés par la collecte des statistiques telles que les performances, la disponibilité et d’utilisation à l’aide de hello d’alertes Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-240">Resources in Azure can be monitored by collecting hello statistics like performance, availability and usage with hello help of Azure alerts.</span></span> <span data-ttu-id="c1fe4-241">Vous pouvez recevoir une alerte basée sur des métriques ou événements de surveillance pour vos ressources Azure ; actuellement les comptes Automation prennent uniquement en charge les métriques.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-241">You can receive an alert based on monitoring metrics or events for your Azure resources, currently Automation Accounts support only metrics.</span></span> <span data-ttu-id="c1fe4-242">Lorsque la valeur hello d’une métrique spécifique dépasse seuil hello affectée ou si hello configuré est déclenché une notification est envoyée toohello service admin coadministrateurs tooresolve hello alerte ou, pour plus d’informations sur les métriques et événements, consultez trop[ Alertes Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="c1fe4-242">When hello value of a specified metric exceeds hello threshold assigned or if hello configured event is triggered then a notification is sent toohello service admin or co-admins tooresolve hello alert, for more information on metrics and events please refer too[Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="c1fe4-243">Outre l’utilisation des alertes Azure comme un système de notification, vous pouvez également déclencher procédures opérationnelles dans la réponse tooalerts.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-243">Besides using Azure alerts as a notification system, you can also kick off runbooks in response tooalerts.</span></span> <span data-ttu-id="c1fe4-244">Azure Automation fournit des runbooks hello capacité toorun compatible webhook alertes Azure.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-244">Azure Automation provides hello capability toorun webhook-enabled runbooks with Azure alerts.</span></span> <span data-ttu-id="c1fe4-245">Quand une métrique dépasse hello configuré valeur de seuil, une règle d’alerte hello devient active et déclencheurs hello webhook automation qui à son tour exécute hello runbook.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-245">When a metric exceeds hello configured threshold value then hello alert rule becomes active and triggers hello automation webhook which in turn executes hello runbook.</span></span>

![Webhooks](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a><span data-ttu-id="c1fe4-247">Contexte de l’alerte</span><span class="sxs-lookup"><span data-stu-id="c1fe4-247">Alert context</span></span>
<span data-ttu-id="c1fe4-248">Considérez une ressource Azure comme un ordinateur virtuel, l’utilisation du processeur de cet ordinateur est une des mesures de performance clés hello.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-248">Consider an Azure resource such as a virtual machine, CPU utilization of this machine is one of hello key performance metric.</span></span> <span data-ttu-id="c1fe4-249">Si hello l’utilisation du processeur est de 100 % ou supérieure à une certaine quantité pour une longue période de temps, vous pourriez le problème hello toofix toorestart hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-249">If hello CPU utilization is 100% or more than a certain amount for long period of time, you might want toorestart hello virtual machine toofix hello problem.</span></span> <span data-ttu-id="c1fe4-250">Cela peut être résolu en configurant une machine virtuelle de toohello une règle d’alerte et cette règle prend le pourcentage de processeur comme métrique.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-250">This can be solved by configuring an alert rule toohello virtual machine and this rule takes CPU percentage as its metric.</span></span> <span data-ttu-id="c1fe4-251">Pourcentage d’UC est uniquement exécutée par exemple, mais il existe de nombreuses autres métriques que vous pouvez configurer tooyour Azure de ressources et de redémarrer la machine virtuelle de hello est une action qui est effectuée toofix ce problème, vous pouvez configurer d’autres actions hello runbook tootake.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-251">CPU percentage here is just taken as an example but there are many other metrics that you can configure tooyour Azure resources and restarting hello virtual machine is an action that is taken toofix this issue, you can configure hello runbook tootake other actions.</span></span>

<span data-ttu-id="c1fe4-252">Lorsque cette règle d’alerte hello devient active et déclencheurs hello compatible webhook de runbook, il envoie hello contexte de l’alerte toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-252">When this hello alert rule becomes active and triggers hello webhook-enabled runbook, it sends hello alert context toohello runbook.</span></span> <span data-ttu-id="c1fe4-253">[Contexte de l’alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contient les détails, notamment **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** et **Timestamp** qui sont requis pour hello runbook tooidentify hello ressource sur laquelle il effectuer action.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-253">[Alert context](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contains details including **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** and **Timestamp** which are required for hello runbook tooidentify hello resource on which it will be taking action.</span></span> <span data-ttu-id="c1fe4-254">Alerte de contexte est incorporé dans le corps de hello Hello **WebhookData** toohello envoyé runbook de l’objet et il est accessible avec **Webhook.RequestBody** propriété</span><span class="sxs-lookup"><span data-stu-id="c1fe4-254">Alert context is embedded in hello body part of hello **WebhookData** object sent toohello runbook and it can be accessed with **Webhook.RequestBody** property</span></span>

### <a name="example"></a><span data-ttu-id="c1fe4-255">Exemple</span><span class="sxs-lookup"><span data-stu-id="c1fe4-255">Example</span></span>
<span data-ttu-id="c1fe4-256">Créer une machine virtuelle Azure dans votre abonnement et à associer un [toomonitor processeur pourcentage métrique d’alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="c1fe4-256">Create an Azure virtual machine in your subscription and associate an [alert toomonitor CPU percentage metric](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="c1fe4-257">Lors de la création d’alerte de hello Assurez-vous de que remplir le champ de webhook hello avec l’URL de hello de webhook hello qui a été généré lors de la création du webhook de hello.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-257">While creating hello alert make sure you populate hello webhook field with hello URL of hello webhook which was generated while creating hello webhook.</span></span>

<span data-ttu-id="c1fe4-258">exemple de runbook suivant Hello est déclenchée lorsque la règle d’alerte hello devient active et collecte des paramètres de contexte de l’alerte hello qui sont requis pour hello runbook tooidentify hello ressource sur laquelle il prendra action.</span><span class="sxs-lookup"><span data-stu-id="c1fe4-258">hello following sample runbook is triggered when hello alert rule becomes active and it collects hello Alert context parameters which are required for hello runbook tooidentify hello resource on which it will be taking action.</span></span>

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

            # Outputs information on hello webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain hello WebhookBody containing hello AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain hello AlertContext     
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

            # Act on hello AlertContext data, in our case restarting hello VM.
            # Authenticate tooyour Azure subscription using Organization ID toobe able toorestart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check hello status property of hello VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart hello VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant tooonly be started from a webhook."  
        }  
    }



## <a name="next-steps"></a><span data-ttu-id="c1fe4-259">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c1fe4-259">Next steps</span></span>
* <span data-ttu-id="c1fe4-260">Pour plus d’informations sur les différentes façons toostart un runbook, consultez [démarrage d’un Runbook](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="c1fe4-260">For details on different ways toostart a runbook, see [Starting a Runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="c1fe4-261">Pour plus d’informations sur l’affichage hello état d’un Job de Runbook, consultez trop[l’exécution du Runbook dans Azure Automation](automation-runbook-execution.md).</span><span class="sxs-lookup"><span data-stu-id="c1fe4-261">For information on viewing hello Status of a Runbook Job, refer too[Runbook execution in Azure Automation](automation-runbook-execution.md).</span></span>
* <span data-ttu-id="c1fe4-262">toolearn toouse action de tootake Azure Automation sur Azure, alertes, voir [corriger des alertes de machine virtuelle Azure avec des Runbooks Automation](automation-azure-vm-alert-integration.md).</span><span class="sxs-lookup"><span data-stu-id="c1fe4-262">toolearn how toouse Azure Automation tootake action on Azure Alerts, see [Remediate Azure VM Alerts with Automation Runbooks](automation-azure-vm-alert-integration.md).</span></span>
