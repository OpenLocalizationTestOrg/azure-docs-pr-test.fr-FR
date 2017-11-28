---
title: "Résoudre les problèmes liés aux stratégies personnalisées grâce à Application Insights - Azure AD B2C | Documents Microsoft"
description: "configuration d’Application Insights pour suivre l’exécution de stratégies personnalisées"
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
ms.openlocfilehash: 8c79df33cd5f04f490e2cc6372f7e8ac1c4d9bbe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-collecting-logs"></a><span data-ttu-id="27355-103">Azure Active Directory B2C : collecte des journaux</span><span class="sxs-lookup"><span data-stu-id="27355-103">Azure Active Directory B2C: Collecting Logs</span></span>

<span data-ttu-id="27355-104">Cet article explique comment collecter les journaux à partir d’Azure AD B2C afin que vous puissiez diagnostiquer les problèmes liés à vos stratégies personnalisées.</span><span class="sxs-lookup"><span data-stu-id="27355-104">This article provides steps for collecting logs from Azure AD B2C so that you can diagnose problems with your custom policies.</span></span>

>[!NOTE]
><span data-ttu-id="27355-105">Actuellement, les journaux d’activité détaillés décrits ici sont conçus **UNIQUEMENT** pour faciliter le développement de stratégies personnalisées.</span><span class="sxs-lookup"><span data-stu-id="27355-105">Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies.</span></span> <span data-ttu-id="27355-106">N’utilisez pas le mode de développement en production.</span><span class="sxs-lookup"><span data-stu-id="27355-106">Do not use development mode  in production.</span></span>  <span data-ttu-id="27355-107">Les journaux recueillent toutes les revendications envoyées par et aux fournisseurs d’identité au cours du développement.</span><span class="sxs-lookup"><span data-stu-id="27355-107">Logs collect all claims sent to and from the identity providers during development.</span></span>  <span data-ttu-id="27355-108">En cas d’utilisation en production, le développeur assume la responsabilité des informations d’identification personnelle (PII) recueillies dans le journal Application Insights dont il est propriétaire.</span><span class="sxs-lookup"><span data-stu-id="27355-108">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span></span>  <span data-ttu-id="27355-109">Ces journaux détaillés ne sont collectés que si la stratégie est en **MODE DE DÉVELOPPEMENT**.</span><span class="sxs-lookup"><span data-stu-id="27355-109">These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.</span></span>


## <a name="use-application-insights"></a><span data-ttu-id="27355-110">Utiliser Application Insights</span><span class="sxs-lookup"><span data-stu-id="27355-110">Use Application Insights</span></span>

<span data-ttu-id="27355-111">Azure AD B2C prend en charge une fonctionnalité d’envoi de données à Application Insights.</span><span class="sxs-lookup"><span data-stu-id="27355-111">Azure AD B2C supports a feature for sending data to Application Insights.</span></span>  <span data-ttu-id="27355-112">Application Insights permet de diagnostiquer les exceptions et de visualiser les problèmes de performances des applications.</span><span class="sxs-lookup"><span data-stu-id="27355-112">Application Insights provides a way to diagnose exceptions and visualize application performance issues.</span></span>

### <a name="setup-application-insights"></a><span data-ttu-id="27355-113">Configurer Application Insights</span><span class="sxs-lookup"><span data-stu-id="27355-113">Setup Application Insights</span></span>

1. <span data-ttu-id="27355-114">Accédez au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="27355-114">Go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="27355-115">Vérifiez que vous êtes sur le locataire avec votre abonnement Azure (pas votre locataire Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="27355-115">Ensure you are in the tenant with your Azure subscription (not your Azure AD B2C tenant).</span></span>
1. <span data-ttu-id="27355-116">Cliquez sur **+ Nouveau** dans le menu de navigation de gauche.</span><span class="sxs-lookup"><span data-stu-id="27355-116">Click **+ New** in the left-hand navigation menu.</span></span>
1. <span data-ttu-id="27355-117">Recherchez et sélectionnez **Application Insights**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="27355-117">Search for and select **Application Insights**, then click **Create**.</span></span>
1. <span data-ttu-id="27355-118">Remplissez le formulaire et cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="27355-118">Complete the form and click **Create**.</span></span> <span data-ttu-id="27355-119">Sélectionnez **Général** comme **Type d’application**.</span><span class="sxs-lookup"><span data-stu-id="27355-119">Select **General** for the **Application Type**.</span></span>
1. <span data-ttu-id="27355-120">Une fois que la ressource a été créée, ouvrez la ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="27355-120">Once the resource has been created, open the Application Insights resource.</span></span>
1. <span data-ttu-id="27355-121">Recherchez **Propriétés** dans le menu de gauche, puis cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="27355-121">Find **Properties** in the left-menu, and click on it.</span></span>
1. <span data-ttu-id="27355-122">Copiez la **Clé d’instrumentation** et enregistrez-la pour la section suivante.</span><span class="sxs-lookup"><span data-stu-id="27355-122">Copy the **Instrumentation Key** and save it for the next section.</span></span>

### <a name="set-up-the-custom-policy"></a><span data-ttu-id="27355-123">Configurer la stratégie personnalisée</span><span class="sxs-lookup"><span data-stu-id="27355-123">Set up the custom policy</span></span>

1. <span data-ttu-id="27355-124">Ouvrez le fichier RP (par exemple, SignUpOrSignin.xml).</span><span class="sxs-lookup"><span data-stu-id="27355-124">Open the RP file (for example, SignUpOrSignin.xml).</span></span>
1. <span data-ttu-id="27355-125">Ajoutez les attributs suivants à l’élément `<TrustFrameworkPolicy>` :</span><span class="sxs-lookup"><span data-stu-id="27355-125">Add the following attributes to the `<TrustFrameworkPolicy>` element:</span></span>

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. <span data-ttu-id="27355-126">S’il n’existe pas déjà, ajoutez un nœud enfant `<UserJourneyBehaviors>` au nœud `<RelyingParty>`.</span><span class="sxs-lookup"><span data-stu-id="27355-126">If it doesn't exist already, add a child node `<UserJourneyBehaviors>` to the `<RelyingParty>` node.</span></span> <span data-ttu-id="27355-127">Il doit être placé immédiatement après le `<DefaultUserJourney ReferenceId="YourPolicyName" />`</span><span class="sxs-lookup"><span data-stu-id="27355-127">It must be located immediately after the `<DefaultUserJourney ReferenceId="YourPolicyName" />`</span></span>
2. <span data-ttu-id="27355-128">Ajoutez le nœud suivant en tant qu’enfant de l’élément `<UserJourneyBehaviors>`.</span><span class="sxs-lookup"><span data-stu-id="27355-128">Add the following node as a child of the `<UserJourneyBehaviors>` element.</span></span> <span data-ttu-id="27355-129">Veillez à remplacer `{Your Application Insights Key}` par la **Clé d’instrumentation** que vous avez obtenue à partir d’Application Insights dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="27355-129">Make sure to replace `{Your Application Insights Key}` with the **Instrumentation Key** that you obtained from Application Insights in the previous section.</span></span>

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * <span data-ttu-id="27355-130">`DeveloperMode="true"` indique à ApplicationInsights d’accélérer l’envoi de la télémétrie via le pipeline de traitement, valable pour le développement, mais limité à des volumes élevés.</span><span class="sxs-lookup"><span data-stu-id="27355-130">`DeveloperMode="true"` tells ApplicationInsights to expedite the telemetry through the processing pipeline, good for development, but constrained at high volumes.</span></span>
  * <span data-ttu-id="27355-131">`ClientEnabled="true"` envoie le script côté client ApplicationInsights pour l’affichage de la page de suivi et les erreurs côté client (pas nécessaire).</span><span class="sxs-lookup"><span data-stu-id="27355-131">`ClientEnabled="true"` sends the ApplicationInsights client-side script for tracking page view and client-side errors (not needed).</span></span>
  * <span data-ttu-id="27355-132">`ServerEnabled="true"` envoie le JSON UserJourneyRecorder existant en tant qu’événement personnalisé à Application Insights.</span><span class="sxs-lookup"><span data-stu-id="27355-132">`ServerEnabled="true"` sends the existing UserJourneyRecorder JSON as a custom event to Application Insights.</span></span>
<span data-ttu-id="27355-133">Exemple :</span><span class="sxs-lookup"><span data-stu-id="27355-133">Sample:</span></span>

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

3. <span data-ttu-id="27355-134">Téléchargez la stratégie.</span><span class="sxs-lookup"><span data-stu-id="27355-134">Upload the policy.</span></span>

### <a name="see-the-logs-in-application-insights"></a><span data-ttu-id="27355-135">Afficher des journaux dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="27355-135">See the logs in Application Insights</span></span>

>[!NOTE]
> <span data-ttu-id="27355-136">Il y a un court délai (moins de cinq minutes) avant que les nouveaux journaux s’affichent dans Application Insights.</span><span class="sxs-lookup"><span data-stu-id="27355-136">There is a short delay (less than five minutes) before you can see new logs in Application Insights.</span></span>

1. <span data-ttu-id="27355-137">Ouvrez la ressource Application Insights que vous avez créée sur le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="27355-137">Open the Application Insights resource that you created in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="27355-138">Dans le menu **Aperçu**, cliquez sur **Analytics**.</span><span class="sxs-lookup"><span data-stu-id="27355-138">In the **Overview** menu, click on **Analytics**.</span></span>
1. <span data-ttu-id="27355-139">Ouvrez un nouvel onglet dans Application Insights.</span><span class="sxs-lookup"><span data-stu-id="27355-139">Open a new tab in Application Insights.</span></span>
1. <span data-ttu-id="27355-140">Voici une liste de requêtes que vous pouvez utiliser pour afficher les journaux</span><span class="sxs-lookup"><span data-stu-id="27355-140">Here is a list of queries you can use to see the logs</span></span>

| <span data-ttu-id="27355-141">Requête</span><span class="sxs-lookup"><span data-stu-id="27355-141">Query</span></span> | <span data-ttu-id="27355-142">Description</span><span class="sxs-lookup"><span data-stu-id="27355-142">Description</span></span> |
|---------------------|--------------------|
<span data-ttu-id="27355-143">traces</span><span class="sxs-lookup"><span data-stu-id="27355-143">traces</span></span> | <span data-ttu-id="27355-144">Consultez tous les journaux générés par Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="27355-144">See all of the logs generated by Azure AD B2C</span></span> |
<span data-ttu-id="27355-145">traces \\</span><span class="sxs-lookup"><span data-stu-id="27355-145">traces \\</span></span>| <span data-ttu-id="27355-146">where timestamp > ago(1d)</span><span class="sxs-lookup"><span data-stu-id="27355-146">where timestamp > ago(1d)</span></span> | <span data-ttu-id="27355-147">Consultez tous les journaux générés par Azure AD B2C pour le dernier jour</span><span class="sxs-lookup"><span data-stu-id="27355-147">See all of the logs generated by Azure AD B2C for the last day</span></span>

<span data-ttu-id="27355-148">Les entrées peuvent être longues.</span><span class="sxs-lookup"><span data-stu-id="27355-148">The entries may be long.</span></span>  <span data-ttu-id="27355-149">Exporter au format CSV pour une étude plus approfondie.</span><span class="sxs-lookup"><span data-stu-id="27355-149">Export to CSV for a closer look.</span></span>

<span data-ttu-id="27355-150">Pour plus d’informations sur l’outil Analytics, cliquez [ici](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span><span class="sxs-lookup"><span data-stu-id="27355-150">You can learn more about the Analytics tool [here](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span></span>

>[!NOTE]
><span data-ttu-id="27355-151">La communauté a développé une visionneuse du parcours utilisateur pour aider les développeurs d’identité.</span><span class="sxs-lookup"><span data-stu-id="27355-151">The community has developed a user journey viewer to help identity developers.</span></span>  <span data-ttu-id="27355-152">Elle n’est pas prise en charge par Microsoft et est mise à disposition tel quel.</span><span class="sxs-lookup"><span data-stu-id="27355-152">It is not supported by Microsoft and made available strictly as-is.</span></span>  <span data-ttu-id="27355-153">Elle lit les données de votre instance d’Application Insights et présente les événements du parcours utilisateur d’une façon bien structurée.</span><span class="sxs-lookup"><span data-stu-id="27355-153">It reads from your Application Insights instance and provides a well-structure view of the user journey events.</span></span>  <span data-ttu-id="27355-154">Vous obtenez le code source et le déployez dans votre propre solution.</span><span class="sxs-lookup"><span data-stu-id="27355-154">You obtain the source code and deploy it in your own solution.</span></span>

>[!NOTE]
><span data-ttu-id="27355-155">Actuellement, les journaux d’activité détaillés décrits ici sont conçus **UNIQUEMENT** pour faciliter le développement de stratégies personnalisées.</span><span class="sxs-lookup"><span data-stu-id="27355-155">Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies.</span></span> <span data-ttu-id="27355-156">N’utilisez pas le mode de développement en production.</span><span class="sxs-lookup"><span data-stu-id="27355-156">Do not use development mode in production.</span></span>  <span data-ttu-id="27355-157">Les journaux recueillent toutes les revendications envoyées par et aux fournisseurs d’identité au cours du développement.</span><span class="sxs-lookup"><span data-stu-id="27355-157">Logs collect all claims sent to and from the identity providers during development.</span></span>  <span data-ttu-id="27355-158">En cas d’utilisation en production, le développeur assume la responsabilité des informations d’identification personnelle (PII) recueillies dans le journal Application Insights dont il est propriétaire.</span><span class="sxs-lookup"><span data-stu-id="27355-158">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span></span>  <span data-ttu-id="27355-159">Ces journaux détaillés ne sont collectés que si la stratégie est en **MODE DE DÉVELOPPEMENT**.</span><span class="sxs-lookup"><span data-stu-id="27355-159">These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.</span></span>

[<span data-ttu-id="27355-160">Référentiel Github pour exemples de stratégies personnalisées non pris en charge et outils connexes</span><span class="sxs-lookup"><span data-stu-id="27355-160">Github Repository for Unsupported Custom Policy Samples and Related tools</span></span>](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a><span data-ttu-id="27355-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="27355-161">Next Steps</span></span>

<span data-ttu-id="27355-162">Explorez les données d’Application Insights pour mieux comprendre la façon dont l’infrastructure d’expérience d’identité B2C sous-jacente fournit vos propres expériences d’identité.</span><span class="sxs-lookup"><span data-stu-id="27355-162">Explore the data in Application Insights to help you understand how the Identity Experience Framework underlying B2C works to deliver your own identity experiences.</span></span>
