---
title: "Application Insights tootroubleshoot stratégies personnalisées - Azure AD B2C | Documents Microsoft"
description: "Comment toosetup Application Insights tootrace hello l’exécution de stratégies personnalisées"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: saeda
ms.openlocfilehash: c02d7178512c7f9e022385371c3effd4f8cb7726
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-collecting-logs"></a><span data-ttu-id="7c967-103">Azure Active Directory B2C : collecte des journaux</span><span class="sxs-lookup"><span data-stu-id="7c967-103">Azure Active Directory B2C: Collecting Logs</span></span>

<span data-ttu-id="7c967-104">Cet article explique comment collecter les journaux à partir d’Azure AD B2C afin que vous puissiez diagnostiquer les problèmes liés à vos stratégies personnalisées.</span><span class="sxs-lookup"><span data-stu-id="7c967-104">This article provides steps for collecting logs from Azure AD B2C so that you can diagnose problems with your custom policies.</span></span>

>[!NOTE]
><span data-ttu-id="7c967-105">Actuellement, hello journaux d’activité détaillés décrites ici sont conçues **uniquement** tooaid dans le développement de stratégies personnalisées.</span><span class="sxs-lookup"><span data-stu-id="7c967-105">Currently, hello detailed activity logs described here are designed **ONLY** tooaid in development of custom policies.</span></span> <span data-ttu-id="7c967-106">N’utilisez pas le mode de développement en production.</span><span class="sxs-lookup"><span data-stu-id="7c967-106">Do not use development mode  in production.</span></span>  <span data-ttu-id="7c967-107">Journaux de collectent toutes les revendications envoyées tooand hello fournisseurs d’identité au cours du développement.</span><span class="sxs-lookup"><span data-stu-id="7c967-107">Logs collect all claims sent tooand from hello identity providers during development.</span></span>  <span data-ttu-id="7c967-108">Si utilisé en production, développeur de hello assume la responsabilité pour les informations d’identification personnelle (confidentiellement Identifiable Information) collectée dans le journal d’application Insights hello dont ils sont propriétaires.</span><span class="sxs-lookup"><span data-stu-id="7c967-108">If used in production, hello developer assumes responsibility for PII (Privately Identifiable Information) collected in hello App Insights log that they own.</span></span>  <span data-ttu-id="7c967-109">Ces journaux détaillés est collectés uniquement lorsque la stratégie de hello est placé sur **MODE de développement**.</span><span class="sxs-lookup"><span data-stu-id="7c967-109">These detailed logs are only collected when hello policy is placed on **DEVELOPMENT MODE**.</span></span>


## <a name="use-application-insights"></a><span data-ttu-id="7c967-110">Utiliser Application Insights</span><span class="sxs-lookup"><span data-stu-id="7c967-110">Use Application Insights</span></span>

<span data-ttu-id="7c967-111">Azure AD B2C prend en charge une fonctionnalité pour l’envoi de données tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="7c967-111">Azure AD B2C supports a feature for sending data tooApplication Insights.</span></span>  <span data-ttu-id="7c967-112">Application Insights fournit un moyen toodiagnose des exceptions et visualiser les problèmes de performances des applications.</span><span class="sxs-lookup"><span data-stu-id="7c967-112">Application Insights provides a way toodiagnose exceptions and visualize application performance issues.</span></span>

### <a name="setup-application-insights"></a><span data-ttu-id="7c967-113">Configurer Application Insights</span><span class="sxs-lookup"><span data-stu-id="7c967-113">Setup Application Insights</span></span>

1. <span data-ttu-id="7c967-114">Accédez toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7c967-114">Go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7c967-115">Assurez-vous que vous êtes dans le locataire de hello avec votre abonnement Azure (pas votre locataire Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="7c967-115">Ensure you are in hello tenant with your Azure subscription (not your Azure AD B2C tenant).</span></span>
1. <span data-ttu-id="7c967-116">Cliquez sur **+ nouveau** dans le menu de navigation gauche hello.</span><span class="sxs-lookup"><span data-stu-id="7c967-116">Click **+ New** in hello left-hand navigation menu.</span></span>
1. <span data-ttu-id="7c967-117">Recherchez et sélectionnez **Application Insights**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="7c967-117">Search for and select **Application Insights**, then click **Create**.</span></span>
1. <span data-ttu-id="7c967-118">Complétez le formulaire de hello et cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="7c967-118">Complete hello form and click **Create**.</span></span> <span data-ttu-id="7c967-119">Sélectionnez **général** pour hello **Type d’Application**.</span><span class="sxs-lookup"><span data-stu-id="7c967-119">Select **General** for hello **Application Type**.</span></span>
1. <span data-ttu-id="7c967-120">Une fois que la ressource de hello a été créée, ouvrir la ressource d’Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="7c967-120">Once hello resource has been created, open hello Application Insights resource.</span></span>
1. <span data-ttu-id="7c967-121">Rechercher **propriétés** dans hello menu de gauche, puis cliquez sur celle-ci.</span><span class="sxs-lookup"><span data-stu-id="7c967-121">Find **Properties** in hello left-menu, and click on it.</span></span>
1. <span data-ttu-id="7c967-122">Hello de copie **clé d’Instrumentation** et l’enregistrer pour la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="7c967-122">Copy hello **Instrumentation Key** and save it for hello next section.</span></span>

### <a name="set-up-hello-custom-policy"></a><span data-ttu-id="7c967-123">Configurer la stratégie personnalisée de hello</span><span class="sxs-lookup"><span data-stu-id="7c967-123">Set up hello custom policy</span></span>

1. <span data-ttu-id="7c967-124">Ouvrir le fichier de partie de confiance hello (par exemple, SignUpOrSignin.xml).</span><span class="sxs-lookup"><span data-stu-id="7c967-124">Open hello RP file (for example, SignUpOrSignin.xml).</span></span>
1. <span data-ttu-id="7c967-125">Ajouter hello suivant attributs toohello `<TrustFrameworkPolicy>` élément :</span><span class="sxs-lookup"><span data-stu-id="7c967-125">Add hello following attributes toohello `<TrustFrameworkPolicy>` element:</span></span>

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. <span data-ttu-id="7c967-126">Si elle n’existe pas déjà, ajoutez un nœud enfant `<UserJourneyBehaviors>` toohello `<RelyingParty>` nœud.</span><span class="sxs-lookup"><span data-stu-id="7c967-126">If it doesn't exist already, add a child node `<UserJourneyBehaviors>` toohello `<RelyingParty>` node.</span></span> <span data-ttu-id="7c967-127">Il doit être placé immédiatement après hello`<DefaultUserJourney ReferenceId="YourPolicyName" />`</span><span class="sxs-lookup"><span data-stu-id="7c967-127">It must be located immediately after hello `<DefaultUserJourney ReferenceId="YourPolicyName" />`</span></span>
2. <span data-ttu-id="7c967-128">Ajouter hello suivant du nœud en tant qu’enfant de hello `<UserJourneyBehaviors>` élément.</span><span class="sxs-lookup"><span data-stu-id="7c967-128">Add hello following node as a child of hello `<UserJourneyBehaviors>` element.</span></span> <span data-ttu-id="7c967-129">Assurez-vous que tooreplace `{Your Application Insights Key}` avec hello **clé d’Instrumentation** que vous avez obtenue à partir de l’Application Insights dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="7c967-129">Make sure tooreplace `{Your Application Insights Key}` with hello **Instrumentation Key** that you obtained from Application Insights in hello previous section.</span></span>

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * <span data-ttu-id="7c967-130">`DeveloperMode="true"`Indique le bon ApplicationInsights tooexpedite les données de télémétrie hello via le pipeline de traitement de hello, pour le développement, mais limitée à des volumes élevés.</span><span class="sxs-lookup"><span data-stu-id="7c967-130">`DeveloperMode="true"` tells ApplicationInsights tooexpedite hello telemetry through hello processing pipeline, good for development, but constrained at high volumes.</span></span>
  * <span data-ttu-id="7c967-131">`ClientEnabled="true"`envoie hello ApplicationInsights un script côté client pour le suivi des erreurs de page côté client et de la vue (ne pas nécessaires).</span><span class="sxs-lookup"><span data-stu-id="7c967-131">`ClientEnabled="true"` sends hello ApplicationInsights client-side script for tracking page view and client-side errors (not needed).</span></span>
  * <span data-ttu-id="7c967-132">`ServerEnabled="true"`envoie hello existant UserJourneyRecorder JSON comme une événement personnalisé de tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="7c967-132">`ServerEnabled="true"` sends hello existing UserJourneyRecorder JSON as a custom event tooApplication Insights.</span></span>
<span data-ttu-id="7c967-133">Exemple :</span><span class="sxs-lookup"><span data-stu-id="7c967-133">Sample:</span></span>

  ```XML
  <TrustFrameworkPolicy
    ...
    TenantId="fabrikamb2c.onmicrosoft.com"
    PolicyId="SignUpOrSignInWithAAD"
    DeploymentMode="Development"
    UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  >
    ...
    <RelyingParty>
      <DefaultUserJourney ReferenceId="YourPolicyName" />
      <UserJourneyBehaviors>
        <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
      </UserJourneyBehaviors>
      ...
  </TrustFrameworkPolicy>
  ```

3. <span data-ttu-id="7c967-134">Télécharger la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="7c967-134">Upload hello policy.</span></span>

### <a name="see-hello-logs-in-application-insights"></a><span data-ttu-id="7c967-135">Consultez hello consigne dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="7c967-135">See hello logs in Application Insights</span></span>

>[!NOTE]
> <span data-ttu-id="7c967-136">Il y a un court délai (moins de cinq minutes) avant que les nouveaux journaux s’affichent dans Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7c967-136">There is a short delay (less than five minutes) before you can see new logs in Application Insights.</span></span>

1. <span data-ttu-id="7c967-137">Ouvrir la ressource Application Insights hello que vous avez créé dans hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7c967-137">Open hello Application Insights resource that you created in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="7c967-138">Bonjour **vue d’ensemble** menu, cliquez sur **Analytique**.</span><span class="sxs-lookup"><span data-stu-id="7c967-138">In hello **Overview** menu, click on **Analytics**.</span></span>
1. <span data-ttu-id="7c967-139">Ouvrez un nouvel onglet dans Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7c967-139">Open a new tab in Application Insights.</span></span>
1. <span data-ttu-id="7c967-140">Voici une liste de requêtes, que vous pouvez utiliser les journaux hello toosee</span><span class="sxs-lookup"><span data-stu-id="7c967-140">Here is a list of queries you can use toosee hello logs</span></span>

| <span data-ttu-id="7c967-141">Interroger</span><span class="sxs-lookup"><span data-stu-id="7c967-141">Query</span></span> | <span data-ttu-id="7c967-142">Description</span><span class="sxs-lookup"><span data-stu-id="7c967-142">Description</span></span> |
|---------------------|--------------------|
<span data-ttu-id="7c967-143">traces</span><span class="sxs-lookup"><span data-stu-id="7c967-143">traces</span></span> | <span data-ttu-id="7c967-144">Afficher tous les journaux de hello générés par Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="7c967-144">See all of hello logs generated by Azure AD B2C</span></span> |
<span data-ttu-id="7c967-145">traces \\</span><span class="sxs-lookup"><span data-stu-id="7c967-145">traces \\</span></span>| <span data-ttu-id="7c967-146">where timestamp > ago(1d)</span><span class="sxs-lookup"><span data-stu-id="7c967-146">where timestamp > ago(1d)</span></span> | <span data-ttu-id="7c967-147">Afficher tous les fichiers journaux hello générés par Azure AD B2C pour hello dernier jour</span><span class="sxs-lookup"><span data-stu-id="7c967-147">See all of hello logs generated by Azure AD B2C for hello last day</span></span>

<span data-ttu-id="7c967-148">les entrées de Hello peuvent être longues.</span><span class="sxs-lookup"><span data-stu-id="7c967-148">hello entries may be long.</span></span>  <span data-ttu-id="7c967-149">Exportez tooCSV pour une présentation détaillée.</span><span class="sxs-lookup"><span data-stu-id="7c967-149">Export tooCSV for a closer look.</span></span>

<span data-ttu-id="7c967-150">Vous en apprendrez davantage sur outil d’Analytique hello [ici](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span><span class="sxs-lookup"><span data-stu-id="7c967-150">You can learn more about hello Analytics tool [here](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span></span>

>[!NOTE]
><span data-ttu-id="7c967-151">Communauté de Hello a développé une développeurs d’identité toohelp visionneuse utilisateur voyage.</span><span class="sxs-lookup"><span data-stu-id="7c967-151">hello community has developed a user journey viewer toohelp identity developers.</span></span>  <span data-ttu-id="7c967-152">Elle n’est pas prise en charge par Microsoft et est mise à disposition tel quel.</span><span class="sxs-lookup"><span data-stu-id="7c967-152">It is not supported by Microsoft and made available strictly as-is.</span></span>  <span data-ttu-id="7c967-153">Il lit à partir de votre instance d’Application Insights et fournit une vue de structure de la barre d’outils des événements de voyage hello utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7c967-153">It reads from your Application Insights instance and provides a well-structure view of hello user journey events.</span></span>  <span data-ttu-id="7c967-154">Obtenir le code source de hello et de le déployer dans votre propre solution.</span><span class="sxs-lookup"><span data-stu-id="7c967-154">You obtain hello source code and deploy it in your own solution.</span></span>

>[!NOTE]
><span data-ttu-id="7c967-155">Actuellement, hello journaux d’activité détaillés décrites ici sont conçues **uniquement** tooaid dans le développement de stratégies personnalisées.</span><span class="sxs-lookup"><span data-stu-id="7c967-155">Currently, hello detailed activity logs described here are designed **ONLY** tooaid in development of custom policies.</span></span> <span data-ttu-id="7c967-156">N’utilisez pas le mode de développement en production.</span><span class="sxs-lookup"><span data-stu-id="7c967-156">Do not use development mode in production.</span></span>  <span data-ttu-id="7c967-157">Journaux de collectent toutes les revendications envoyées tooand hello fournisseurs d’identité au cours du développement.</span><span class="sxs-lookup"><span data-stu-id="7c967-157">Logs collect all claims sent tooand from hello identity providers during development.</span></span>  <span data-ttu-id="7c967-158">Si utilisé en production, développeur de hello assume la responsabilité pour les informations d’identification personnelle (confidentiellement Identifiable Information) collectée dans le journal d’application Insights hello dont ils sont propriétaires.</span><span class="sxs-lookup"><span data-stu-id="7c967-158">If used in production, hello developer assumes responsibility for PII (Privately Identifiable Information) collected in hello App Insights log that they own.</span></span>  <span data-ttu-id="7c967-159">Ces journaux détaillés est collectés uniquement lorsque la stratégie de hello est placé sur **MODE de développement**.</span><span class="sxs-lookup"><span data-stu-id="7c967-159">These detailed logs are only collected when hello policy is placed on **DEVELOPMENT MODE**.</span></span>

[<span data-ttu-id="7c967-160">Référentiel Github pour exemples de stratégies personnalisées non pris en charge et outils connexes</span><span class="sxs-lookup"><span data-stu-id="7c967-160">Github Repository for Unsupported Custom Policy Samples and Related tools</span></span>](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a><span data-ttu-id="7c967-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7c967-161">Next Steps</span></span>

<span data-ttu-id="7c967-162">Explorer les données hello dans toohelp Application Insights vous comprenez comment hello infrastructure d’identité expérience B2C sous-jacent fonctionne toodeliver rencontre de votre propre identité.</span><span class="sxs-lookup"><span data-stu-id="7c967-162">Explore hello data in Application Insights toohelp you understand how hello Identity Experience Framework underlying B2C works toodeliver your own identity experiences.</span></span>
