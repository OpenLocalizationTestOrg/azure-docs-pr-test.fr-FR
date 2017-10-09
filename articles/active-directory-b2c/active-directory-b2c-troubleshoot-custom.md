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
# <a name="azure-active-directory-b2c-collecting-logs"></a>Azure Active Directory B2C : collecte des journaux

Cet article explique comment collecter les journaux à partir d’Azure AD B2C afin que vous puissiez diagnostiquer les problèmes liés à vos stratégies personnalisées.

>[!NOTE]
>Actuellement, hello journaux d’activité détaillés décrites ici sont conçues **uniquement** tooaid dans le développement de stratégies personnalisées. N’utilisez pas le mode de développement en production.  Journaux de collectent toutes les revendications envoyées tooand hello fournisseurs d’identité au cours du développement.  Si utilisé en production, développeur de hello assume la responsabilité pour les informations d’identification personnelle (confidentiellement Identifiable Information) collectée dans le journal d’application Insights hello dont ils sont propriétaires.  Ces journaux détaillés est collectés uniquement lorsque la stratégie de hello est placé sur **MODE de développement**.


## <a name="use-application-insights"></a>Utiliser Application Insights

Azure AD B2C prend en charge une fonctionnalité pour l’envoi de données tooApplication Insights.  Application Insights fournit un moyen toodiagnose des exceptions et visualiser les problèmes de performances des applications.

### <a name="setup-application-insights"></a>Configurer Application Insights

1. Accédez toohello [portail Azure](https://portal.azure.com). Assurez-vous que vous êtes dans le locataire de hello avec votre abonnement Azure (pas votre locataire Azure AD B2C).
1. Cliquez sur **+ nouveau** dans le menu de navigation gauche hello.
1. Recherchez et sélectionnez **Application Insights**, puis cliquez sur **Créer**.
1. Complétez le formulaire de hello et cliquez sur **créer**. Sélectionnez **général** pour hello **Type d’Application**.
1. Une fois que la ressource de hello a été créée, ouvrir la ressource d’Application Insights hello.
1. Rechercher **propriétés** dans hello menu de gauche, puis cliquez sur celle-ci.
1. Hello de copie **clé d’Instrumentation** et l’enregistrer pour la section suivante de hello.

### <a name="set-up-hello-custom-policy"></a>Configurer la stratégie personnalisée de hello

1. Ouvrir le fichier de partie de confiance hello (par exemple, SignUpOrSignin.xml).
1. Ajouter hello suivant attributs toohello `<TrustFrameworkPolicy>` élément :

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. Si elle n’existe pas déjà, ajoutez un nœud enfant `<UserJourneyBehaviors>` toohello `<RelyingParty>` nœud. Il doit être placé immédiatement après hello`<DefaultUserJourney ReferenceId="YourPolicyName" />`
2. Ajouter hello suivant du nœud en tant qu’enfant de hello `<UserJourneyBehaviors>` élément. Assurez-vous que tooreplace `{Your Application Insights Key}` avec hello **clé d’Instrumentation** que vous avez obtenue à partir de l’Application Insights dans la section précédente de hello.

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * `DeveloperMode="true"`Indique le bon ApplicationInsights tooexpedite les données de télémétrie hello via le pipeline de traitement de hello, pour le développement, mais limitée à des volumes élevés.
  * `ClientEnabled="true"`envoie hello ApplicationInsights un script côté client pour le suivi des erreurs de page côté client et de la vue (ne pas nécessaires).
  * `ServerEnabled="true"`envoie hello existant UserJourneyRecorder JSON comme une événement personnalisé de tooApplication Insights.
Exemple :

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

3. Télécharger la stratégie de hello.

### <a name="see-hello-logs-in-application-insights"></a>Consultez hello consigne dans Application Insights

>[!NOTE]
> Il y a un court délai (moins de cinq minutes) avant que les nouveaux journaux s’affichent dans Application Insights.

1. Ouvrir la ressource Application Insights hello que vous avez créé dans hello [portail Azure](https://portal.azure.com).
1. Bonjour **vue d’ensemble** menu, cliquez sur **Analytique**.
1. Ouvrez un nouvel onglet dans Application Insights.
1. Voici une liste de requêtes, que vous pouvez utiliser les journaux hello toosee

| Interroger | Description |
|---------------------|--------------------|
traces | Afficher tous les journaux de hello générés par Azure AD B2C |
traces \| where timestamp > ago(1d) | Afficher tous les fichiers journaux hello générés par Azure AD B2C pour hello dernier jour

les entrées de Hello peuvent être longues.  Exportez tooCSV pour une présentation détaillée.

Vous en apprendrez davantage sur outil d’Analytique hello [ici](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).

>[!NOTE]
>Communauté de Hello a développé une développeurs d’identité toohelp visionneuse utilisateur voyage.  Elle n’est pas prise en charge par Microsoft et est mise à disposition tel quel.  Il lit à partir de votre instance d’Application Insights et fournit une vue de structure de la barre d’outils des événements de voyage hello utilisateur.  Obtenir le code source de hello et de le déployer dans votre propre solution.

>[!NOTE]
>Actuellement, hello journaux d’activité détaillés décrites ici sont conçues **uniquement** tooaid dans le développement de stratégies personnalisées. N’utilisez pas le mode de développement en production.  Journaux de collectent toutes les revendications envoyées tooand hello fournisseurs d’identité au cours du développement.  Si utilisé en production, développeur de hello assume la responsabilité pour les informations d’identification personnelle (confidentiellement Identifiable Information) collectée dans le journal d’application Insights hello dont ils sont propriétaires.  Ces journaux détaillés est collectés uniquement lorsque la stratégie de hello est placé sur **MODE de développement**.

[Référentiel Github pour exemples de stratégies personnalisées non pris en charge et outils connexes](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a>Étapes suivantes

Explorer les données hello dans toohelp Application Insights vous comprenez comment hello infrastructure d’identité expérience B2C sous-jacent fonctionne toodeliver rencontre de votre propre identité.
