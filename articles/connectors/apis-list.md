---
title: aaaConnectors pour Azure Logic Apps | Documents Microsoft
description: "Choisissez parmi tous les toobuild de connecteurs de centres de données disponibles hello et créer des applications de logique"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: f1f1fd50-b7f9-4d13-824a-39678619aa7a
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: mandia; ladocs
ms.openlocfilehash: d681d13d642e6e1512d1f8ab0e1078a194b5da83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connectors-list"></a>Liste des connecteurs
> [!TIP]
> Hello [liste complète de A-Z](#az) (dans cette rubrique) répertorie tous les connecteurs hello disponibles que vous pouvez utiliser dans vos applications logiques. [Détails du connecteur](/connectors/) répertorie les déclencheurs et les actions définies dans les swagger hello et répertorie les limites pour chaque connecteur.

Les connecteurs font partie intégrante de la création d’applications logiques. À l’aide de ces connecteurs, vous pouvez réellement développer vos locaux et cloud des applications toodo différentes choses avec les données que vous créez et les données que vous avez déjà. Hello connecteurs sont disponibles dans hello suivant des catégories : 

* **Connecteurs standard** : disponibles et inclus automatiquement lorsque vous utilisez des applications logiques. Il s’agit par exemple de Service Bus, Power BI, Oracle Database, OneDrive, et bien d’autres encore.

* **Connecteurs de compte d’intégration** : disponibles lorsque vous achetez un compte d’intégration. À l’aide de ces connecteurs, vous pouvez transformer et valider du code XML, traiter les messages entreprise-entreprise avec AS2/X12/EDIFACT, ainsi que coder et décoder des fichiers plats. Si vous travaillez avec BizTalk Server, ces connecteurs sont que parfaitement tooexpand vos workflows BizTalk dans Azure.  

    BizTalk Server a également un [l’adaptateur Logic Apps](https://msdn.microsoft.com/library/mt787163.aspx) qui inclut la réception d’une application de la logique et l’envoi d’application logique de tooa.

* **Connecteurs d’entreprise** : inclut MQ et SAP. Disponibles moyennant un coût supplémentaire. 

[Tarification d’applications logique](https://azure.microsoft.com/pricing/details/logic-apps/) et [modèle de tarification](../logic-apps/logic-apps-pricing.md) fournissent plus de détails sur les coûts de hello. 

## <a name="popular-connectors"></a>Connecteurs les plus courants
Des milliers d’applications et des millions d’exécutions utilisent ces connecteurs pour traiter correctement les données et les informations. Hello tableau suivant répertorie les plus populaires de hello et certains favoris avec nos utilisateurs :

| |  |  |  |
| --- | --- | --- | --- |
| [![API Icon][AzureBlobStorageicon]<br/>**Azure Blob<br/>Storage**][AzureBlobStoragedoc] | Si vous le souhaitez tooautomate toutes les tâches avec votre compte de stockage, vous devez examiner ce connecteur. Prend en charge les opérations CRUD (créer, lire, mettre à jour, supprimer). | [![API Icon][Azure-Functionsicon]<br/>**Azure Functions**][azure-functionsdoc] | Créez des fonctions qui exécutent des extraits de code personnalisés de C# ou node.js, puis utilisez ces fonctions dans vos applications logiques.  |
| [![API Icon][Dynamics-365icon]<br/>**Dynamics 365<br/>CRM Online**][Dynamics-365doc] | Une des hello plus posées pour les connecteurs. Il a toohelp déclencheurs et actions d’automatiser les flux de travail avec les prospects et bien plus encore. | [![API Icon][Event-Hubs-icon]<br/>**Event Hubs**][event-hubs-doc] | Consommez et publiez des événements sur un Event Hub. Par exemple, vous pouvez obtenir une sortie à partir de votre application logique à l’aide de concentrateurs d’événements et envoyez ensuite le fournisseur de hello sortie tooa analytique en temps réel. |
| [![API Icon][FTPicon]<br/>**FTP**][FTPdoc] | Si votre serveur FTP est accessible à partir de hello internet, puis vous pouvez automatiser toowork de flux de travail de fichiers et dossiers. <br/><br/>SFTP est également disponible avec le connecteur SFTP hello. | [![API Icon][HTTPicon]<br/>**HTTP**][httpdoc] | Utilisez logique applications toocommunicate avec n’importe quel point de terminaison via HTTP. |
| [![API Icon][Office-365-Outlookicon]<br/>**Office 365<br/>Outlook**][office365-outlookdoc] | Grand nombre de déclencheurs et beaucoup plus de courrier électronique d’actions toouse Office 365 et événements au sein de votre flux de travail. <br/><br/>Ce connecteur inclut un *d’approbation par e-mail* demandes de congés action tooapprove, notes de frais et ainsi de suite. <br/><br/>Utilisateurs Office 365 sont également disponibles avec connecteur d’utilisateurs d’Office 365 hello.| [![API Icon][HTTP-Requesticon]<br/>**Request / Response**][HTTP-Requestdoc] | Ce connecteur fournit une URL HTTPS. Lors de l’application logique de hello reçoit une URL de la demande toothis, hello logique application démarre. |
| [![API Icon][Salesforceicon]<br/>**Salesforce**][salesforcedoc] | Connectez-vous facilement votre accès tooobjects Salesforce compte tooget, tels que des prospects et bien plus encore. |  [![API Icon][Service-Busicon]<br/>**Service Bus**][Service-Busdoc] | connecteur les plus populaires de Hello dans les applications de la logique, inclut les déclencheurs et actions une messagerie asynchrone toodo et publication/abonnement avec les files d’attente, les rubriques et les abonnements. |
|  [![API Icon][SharePointicon]<br/>**SharePoint<br/>Online**][SharePointdoc] | Si vous devez utiliser SharePoint et que vous pouvez tirer parti d’automatisation, nous vous recommandons d’envisager ce connecteur. Peut être utilisé avec une installation SharePoint locale et SharePoint Online. | [![API Icon][SQL-Servericon]<br/>**SQL Server**][SQL-Serverdoc] | L’une de hello utilisée plus connecteurs, il peut se connecter tooan local SQL Server et une base de données SQL Azure. | 
| [![API Icon][Twittericon]<br/>**Twitter**][Twitterdoc] | Connectez-vous facilement avec un compte Twitter, puis démarrez un flux de travail dès qu’un nouveau tweet est publié. Ensuite, enregistrez ces de base de données de tweets tooa SQL ou une liste SharePoint. | | | 

## <a name="integration-account-connectors"></a>Connecteurs de compte d’intégration 

Hello Pack d’intégration d’entreprise (EIP) inclut les connecteurs sont bien connu toohello Communauté BizTalk Server. Lorsque vous achetez un [compte d’intégration](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md), vous obtenez également hello suivant connecteurs : 

|  |  |  |  |
| --- | --- | --- | --- |
| [![API Icon][as2icon]<br/>**AS2 :</br> décodage**][as2decode] | [![API Icon][as2icon]<br/>**AS2 :</br> encodage**][as2encode] | [![API Icon][x12icon]<br/>**EDIFACT :</br> décodage**][EDIFACTdecode] | [![API Icon][x12icon]<br/>**EDIFACT :</br> encodage**][EDIFACTencode] |
[![API Icon][flatfileicon]<br/>**Fichier plat :</br> encodage**][flatfiledoc] | [![API Icon][flatfileicon]<br/>**Fichier plat :</br> décodage**][flatfiledecodedoc] | [![API Icon][integrationaccounticon]<br/>**Integration<br/>account**][integrationaccountdoc] | [![API Icon][xmltransformicon]<br/>**Transform<br/>XML**][xmltransformdoc] |
| [![API Icon][x12icon]<br/>**X12 :</br> décodage**][x12decode] | [![API Icon][x12icon]<br/>**X12 :</br> encodage**][x12encode] | [![API Icon][xmlvalidateicon]<br/>**XML <br/>validation**][xmlvalidatedoc] | |

## <a name="enterprise-connectors"></a>Connecteurs d’entreprise

Se connecter tooyour des applications d’entreprise au sein de vos applications logiques.

|  |  |
| --- | --- |
|[![API Icon][MQicon]<br/>**MQ**][mqdoc]|[![API Icon][SAPicon]<br/>**SAP**][sapconnector]|


## <a name="az"></a>Liste complète de A à Z

[Détails du connecteur](/connectors/) liste les déclencheurs et les actions définies dans les swagger hello et répertorie les limites pour chaque connecteur.

| | | | | | | | | | | | | |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| [**1**](#1) | [**A**](#a) | [**B**](#b) | [**C**](#c) | [**D**](#d) | [**E**](#e) | [**F**](#f) | [**G**](#g) | [**H**](#h) | [**I**](#i) | [**J**](#j) | [**L**](#l) | [**M**](#m) |
| [**N**](#n) | [**O**](#o) | [**P**](#p) | [**R**](#r) | [**S**](#s) | [**T**](#t) | [**U**](#u) | [**V**](#v) | [**W**](#w) | [**X**](#x) | [**Y**](#y) | [**Z**](#z) | | 

| | |
|---|---|
|<a name="1"></a>10to8 Appointment Scheduling<br/><br/><a name="a"></a>Act!<br/>Adobe Creative Cloud<br/>appFigures<br/>[AS2][as2doc]<br/>Asana<br/>Azure Active Directory (AD)<br/>Gestion des API Azure<br/>Azure App Services<br/>Azure Application<br/>Azure Automation<br/>[Azure Blob Storage][azureblobstoragedoc]<br/>Azure Data Lake<br/>Azure DocumentDB (Cosmos DB)<br/>[Azure Functions][azure-functionsdoc]<br/>[Azure Logic Apps][nested-logic-appdoc]<br/>AzureML<br/>Files d'attente Azure<br/>Azure Resource Manager<br/>[Azure SQL Database][sql-serverdoc]<br/><br/><a name="b"></a>Basecamp 2<br/>Basecamp 3<br/>Batch<br/>Benchmark Email<br/>Bing Search<br/>Bitbucket<br/>Bitly<br/>BizTalk Server<br/>Blogger<br/>Box<br/>Buffer<br/><br/><a name="c"></a>Calendly<br/>Campfire<br/>Capsule CRM<br/>Chatter<br/>Cognito Forms<br/>Cognitive Services Computer Vision API<br/>Cognitive Services Face API<br/>Cognitive Services LUIS<br/>Cognitive Services Text Analytics<br/>Common Data Service<br/>Content Conversion<br/>Control-Terminate<br/>[Custom APIs / web apps][api/web-appdoc]<br/><br/><a name="d"></a>Data Operations<br/>[DB2][db2doc]<br/>Disqus<br/>DocuSign<br/>Do Until<br/>Dropbox<br/>[Dynamics 365 CRM Online][Dynamics-365doc]<br/>Dynamics 365 for Financials<br/>Dynamics 365 for Operations<br/>Dynamics NAV<br/><br/><a name="e"></a>Easy Redmine<br/>EDIFACT<br/>[Event Hubs][event-hubs-doc]<br/>Eventbrite<br/><br/><a name="f"></a>Facebook<br/>[File System][filesystemdoc]<br/>[Flat File][flatfiledoc]<br/>FreshBooks<br/>Freshdesk<br/>FreshService<br/>[FTP][ftpdoc]<br/><br/><a name="g"></a>GitHub<br/>Gmail<br/>Google Calendar<br/>Google Contacts<br/>Google Drive<br/>Google Sheets<br/>Google Tasks<br/>GoToMeeting<br/>GoToTraining<br/>GoToWebinar<br/><br/><a name="h"></a>Harvest<br/>HelloSign<br/>HipChat<br/>[HTTP][httpdoc]<br/>[HTTP + Swagger][http-swaggerdoc]<br/>[HTTP Webhook][webhookdoc]<br/><br/><a name="i"></a>[Informix][informixdoc]<br/>Infusionsoft<br/>Inoreader<br/>Insightly<br/>Instagram<br/>Instapaper<br/>Integration Account<br/>Intercom | <a name="j"></a>JotForm<br/>JIRA<br/><br/><a name="l"></a>LeanKit<br/>LiveChat<br/><br/><a name="m"></a>MailChimp<br/>Mandrill<br/>Moyenne<br/>Microsoft Forms<br/>Microsoft Teams<br/>Microsoft Translator<br/>[MQ][mqdoc]<br/>MSN Weather<br/>Muhimbi PDF<br/>MySQL<br/><br/><a name="n"></a>Nexmo<br/><br/><a name="o"></a>[Office 365 Outlook][office365-outlookdoc]<br/>Office 365 Users<br/>Office 365 Video<br/>OneDrive<br/>OneDrive Entreprise<br/>OneNote (Business)<br/>[Oracle Database][oracle-db-doc]<br/>Outlook Customer Manager<br/>Outlook Tasks<br/>Outlook.com<br/><br/><a name="p"></a>PagerDuty<br/>Parserr<br/>Paylocity<br/>Pinterest<br/>Pipedrive<br/>Pivotal Tracker<br/>Planner<br/>PostgreSQL<br/>Power BI<br/>Project Online<br/><br/><a name="r"></a>Redmine<br/>[Request / Response][http-requestdoc]<br/>RSS<br/><br/><a name="s"></a>[Salesforce][salesforcedoc]<br/>[SAP Application Server][sapconnector]<br/>[SAP Message Server][sapconnector]<br/>[Schedule][recurrencedoc]<br/>Scope<br/>SendGrid<br/>Envoyer des messages toobatch<br/>[Service Bus][service-busdoc]<br/>SFTP<br/>[SharePoint Online][sharepointdoc]<br/>[SharePoint Server][sharepointserver]<br/>Slack<br/>Smartsheet<br/>SMTP<br/>SparkPost<br/>[SQL Server][sql-serverdoc]<br/>Stripe<br/>SurveyMonkey<br/>Switch Case<br/><br/><a name="t"></a>Teamwork Projects<br/>Teradata<br/>Todoist<br/>Toodledo<br/>[Transform XML][xmltransformdoc]<br/>Trello<br/>Twilio<br/>[Twitter][twitterdoc]<br/>Typeform<br/><br/><a name="u"></a>UserVoice<br/><br/><a name="v"></a>Variables<br/>Vimeo<br/>Visual Studio Team Services<br/><br/><a name="w"></a>WebMerge<br/>WordPress<br/>Wunderlist<br/><br/><a name="x"></a>[X12][x12doc]<br/>[XML Validation][xmlvalidatedoc]<br/><br/><a name="y"></a>Yammer<br/>YouTube<br/><br/><a name="z"></a>Zendesk |

> [!TIP]
> tooget main Azure Logic Apps avant de s’inscrire pour un compte Azure, accédez trop[essayez Logic Apps](https://tryappservice.azure.com/?appservice=logic). Vous pouvez créer immédiatement une application logique temporaire. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.

## <a name="connectors-as-triggers-and-actions"></a>Connecteurs en tant que déclencheurs et actions

Un **déclencheur** démarre ou exécute une instance de votre application logique. Certains connecteurs fournissent des déclencheurs qui préviennent votre application lorsque des événements spécifiques se produisent. Par exemple, le connecteur de hello FTP a hello `OnUpdatedFile` déclencheur qui démarre votre application logique, lorsqu’un fichier est mis à jour. 

Les applications logique incluent hello les types de déclencheurs suivants :  

* *Interroger des déclencheurs*: ces déclencheurs interrogent votre service à un toocheck fréquence spécifiée pour les nouvelles données. 

    Lorsque de nouvelles données sont disponibles, une nouvelle instance de votre application logique s’exécute avec les données de salutation en tant qu’entrée. 

* *Push déclencheurs*: ces déclencheurs écoutent pour les données sur un point de terminaison ou d’un événement toohappen, déclenche ensuite une nouvelle instance de votre application logique.

* *Déclencheur récurrence* : ce déclencheur instancie une instance de votre application logique sur une planification prescrite.

Les connecteurs fournissent également des **actions** que vous pouvez utiliser dans votre flux de travail. Par exemple, votre application logique peut rechercher des données et les utiliser par la suite. Plus spécifiquement, vous pouvez rechercher des données client à partir d’une base de données SQL et ensuite utiliser cette toobuild de données client à votre flux de travail. 

> [!TIP]
> [Vue d’ensemble des connecteurs](connectors-overview.md) fournit des informations détaillées sur les déclencheurs et actions. 


## <a name="message-manipulation-actions"></a>Actions de manipulation des messages

Les applications logiques incluent les actions intégrées qui peuvent changer ou manipuler vos données de charge utile. Hello intégré **des opérations de données** connecteur inclut hello suivant des actions : 

| | |
|---|---|
| **Composer** | Générer ou générer des valeurs ou des objets toouse ultérieurement ou que vous générez votre flux de travail. Par exemple, vous pouvez créer un objet JSON avec les valeurs de plusieurs étapes, ou calculer une constante tooreference ultérieurement dans une application de logique s’exécuter. |
| **Créer un tableau CSV**<br/>**Créer un tableau HTML** | Transformez un tableau de jeu de résultats en tableau CSV ou HTML. Par exemple, ajouter une action « Enregistrements de la liste » hello CRM et ajouter un filtre pour les enregistrements ajoutés aujourd'hui. Puis, envoyer les résultats hello comme un tableau HTML dans un message électronique. |
| **Filtrer un tableau** (requête) | Filtrer les entrées de toohello un jeu des résultats qui vous intéressent. Par exemple, rechercher toutes les tweets avec `#Azure`, et puis hello de « filtre » a retourné tweets tooonly retournent des résultats qui sont `Tweeted_by_followers > 50`. |
| **Join** | Joignez un tableau en utilisant un délimiteur. Par exemple, hello opération de détecter des expressions clés retourne un tableau d’expressions clés. Vous pouvez les « joindre » avec une `,` ou quelque chose de similaire. Dans ce cas au lieu de `["Some", "Phrase"]`, vous avez `"Some, Phrase"`. |
| **Analyser JSON** | Analyser et accéder aux valeurs d’un objet JSON dans le Concepteur de hello. Par exemple, si votre fonction Azure retourne une charge utile JSON, puis vous pourrez analyser les propriétés JSON tooaccess hello plus tard dans une autre étape. action de Hello valide également que hello JSON correspondances hello schéma spécifié lors de l’exécution. | 
| **Sélection** | Sélectionnez certaines propriétés d’un tableau pour un traitement ultérieur. Si vous « répertoriez les enregistrements » à partir de SQL et que vous obtenez 15 colonnes, n’en sélectionnez que quelques-unes en vue d’un traitement supplémentaire. sortie de Hello est un tableau qui contient uniquement les propriétés que vous sélectionnez hello. |

## <a name="custom-connectors-and-azure-certification"></a>Connecteurs personnalisés et certification Azure 

toocall des API qui exécuter du code personnalisé ou ne sont pas disponibles en tant que les connecteurs, vous pouvez étendre plateforme de Logic Apps hello par [création basée sur REST API Apps en tant que les connecteurs personnalisés](../logic-apps/logic-apps-create-api-app.md). 

Si vous souhaitez toomake votre personnalisé toouse d’applications API publique et disponible dans Azure, puis soumettez votre toohello les candidatures [programme Microsoft Azure Certified](https://azure.microsoft.com/marketplace/programs/certified/logic-apps/).

## <a name="get-help"></a>Obtenir de l’aide

tooask questions, répondez aux questions et voir les autres utilisateurs Azure Logic Apps font, accédez à toohello [forum de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp améliorer Azure Logic Apps et connecteurs, voter pour ou envoyer vos idées à hello [site de commentaires utilisateur Logic Apps](http://aka.ms/logicapps-wish).

Manque-t-il une rubrique de connecteur ou des informations que vous jugez importantes ? Si Oui, nous aider à en ajoutant tooour des rubriques existantes ou écrire votre propre. Notre documentation est open source et hébergée sur GitHub. Commencez sans tarder dans notre [référentiel GitHub](https://github.com/Microsoft/azure-docs). 

## <a name="next-steps"></a>Étapes suivantes
* [Créez votre première application logique](../logic-apps/logic-apps-create-a-logic-app.md)
* [Créer des API personnalisées pour les applications logiques](../logic-apps/logic-apps-create-api-app.md)
* [Analyser vos applications logiques](../logic-apps/logic-apps-monitor-your-logic-apps.md)

<!--Connectors Documentation-->

[api/web-appdoc]: ../logic-apps/logic-apps-custom-hosted-api.md "Permet d’intégrer des applications logiques à App Service API Apps"
[azureblobstoragedoc]: ./connectors-create-api-azureblobstorage.md "Gérer les fichiers de votre conteneur d’objets blob avec le connecteur Azure Blob Storage"
[azure-functionsdoc]: ../logic-apps/logic-apps-azure-functions.md "Permet d’intégrer des applications logiques à Azure Functions"
[db2doc]: ./connectors-create-api-db2.md "Se connecter tooIBM DB2 dans le cloud de hello ou localement. Mettre à jour une ligne, obtenir une table et bien plus encore"
[Dynamics-365doc]: ./connectors-create-api-crmonline.md "Se connecter tooDynamics CRM Online afin de pouvoir travailler avec des données CRM Online"
[event-hubs-doc]: ./connectors-create-api-azure-event-hubs.md "Se connecter tooAzure concentrateurs d’événements. Recevez et envoyez des événements entre les applications logiques et Azure Event Hubs"
[filesystemdoc]: ../logic-apps/logic-apps-using-file-connector.md "Connexion de système de fichiers local tooan"
[ftpdoc]: ./connectors-create-api-ftp.md "Se connecter tooan FTP / serveur FTPS pour les tâches FTP, telles que le téléchargement, mise en route, la suppression des fichiers et bien plus encore"
[httpdoc]: ./connectors-native-http.md "Passer des appels HTTP avec le connecteur de hello HTTP"
[http-requestdoc]: ./connectors-native-reqres.md "Ajouter des actions pour HTTP demandes et réponses tooyour logic apps"
[http-swaggerdoc]: ./connectors-native-http-swagger.md "Passer des appels HTTP avec le connecteur HTTP + Swagger"
[informixdoc]: ./connectors-create-api-informix.md "Se connecter tooInformix dans le cloud de hello ou localement. Lire une ligne, les tables hello de liste, etc."
[nested-logic-appdoc]: ../logic-apps/logic-apps-http-endpoint.md "Intégrer des applications logiques à des flux de travail imbriqués"
[office365-outlookdoc]: ./connectors-create-api-office365-outlook.md "Connectez les compte tooyour Office 365. Envoyer et recevoir du courrier électronique, gérer votre calendrier et vos contacts et bien plus encore"
[oracle-db-doc]: ./connectors-create-api-oracledatabase.md "Se connecter tooadd de base de données Oracle tooan, insérer, supprimer des lignes et bien plus encore"
[mqdoc]: ./connectors-create-api-mq.md "Se connecter tooMQ localement ou sur Azure et envoyer et recevoir des messages"
[recurrencedoc]:  ./connectors-native-recurrence.md "Déclencher des actions récurrentes pour les applications logiques"
[salesforcedoc]: ./connectors-create-api-salesforce.md "Se connecter tooyour Salesforce compte. Gérer les comptes, les prospects, les opportunités et bien plus encore"
[sapconnector]: ../logic-apps/logic-apps-using-sap-connector.md "Connecter tooan local SAP système"
[service-busdoc]: ./connectors-create-api-servicebus.md "Envoyer des messages à partir de files d’attente et de rubriques Service Bus, et recevoir des messages de files d’attente et d’abonnements ServiceBus"
[sharepointdoc]: ./connectors-create-api-sharepointonline.md "Se connecter tooSharePoint en ligne. Gérer des documents, des éléments de liste et bien plus encore"
[sharepointserver]: ./connectors-create-api-sharepointserver.md "Se connecter tooSharePoint sur le serveur local. Gérer des documents, des éléments de liste et bien plus encore"
[sql-serverdoc]: ./connectors-create-api-sqlazure.md "Se connecter tooAzure base de données SQL ou SQL server. Créer, mettre à jour, obtenir et supprimer des entrées dans une table de base de données SQL."
[twitterdoc]: ./connectors-create-api-twitter.md "Se connecter tooTwitter. Consulter les fils d’actualité, publier des tweets et bien plus encore"
[webhookdoc]: ./connectors-native-webhook.md "Ajouter des applications de logique tooyour actions et les déclencheurs des Webhook"

[as2doc]: ../logic-apps/logic-apps-enterprise-integration-as2.md "Découvrez l’intégration d’entreprise AS2."
[x12doc]: ../logic-apps/logic-apps-enterprise-integration-x12.md "Découvrez l’intégration d’entreprise X12"
[flatfiledoc]:../logic-apps/logic-apps-enterprise-integration-flatfile.md "Découvrez le fichier plat d’intégration d’entreprise."
[flatfiledecodedoc]:../logic-apps/logic-apps-enterprise-integration-flatfile.md "Découvrez le fichier plat d’intégration d’entreprise."
[xmlvalidatedoc]: ../logic-apps/logic-apps-enterprise-integration-xml-validation.md "Découvrez la validation XML d’intégration d’entreprise."
[xmltransformdoc]: ../logic-apps/logic-apps-enterprise-integration-transform.md "Découvrez les transformations d’intégration d’entreprise."
[as2decode]: ../logic-apps/logic-apps-enterprise-integration-as2-decode.md "Découvrez le décodage AS2 pour intégration d’entreprise"
[as2encode]:../logic-apps/logic-apps-enterprise-integration-as2-encode.md "Découvrez le codage AS2 pour intégration d’entreprise"
[X12decode]: ../logic-apps/logic-apps-enterprise-integration-X12-decode.md "Découvrez le décodage X12 pour intégration d’entreprise"
[X12encode]: ../logic-apps/logic-apps-enterprise-integration-X12-encode.md "Découvrez le codage X12 pour intégration d’entreprise"
[EDIFACTdecode]: ../logic-apps/logic-apps-enterprise-integration-EDIFACT-decode.md "Découvrez le décodage EDIFACT pour intégration d’entreprise"
[EDIFACTencode]: ../logic-apps/logic-apps-enterprise-integration-EDIFACT-encode.md "Découvrez le codage EDIFACT pour intégration d’entreprise"
[integrationaccountdoc]: ../logic-apps/logic-apps-enterprise-integration-metadata.md "Recherchez des schémas, des cartes, des partenaires et autres dans votre compte d’intégration"


[boxDoc]: ./connectors-create-api-box.md "Se connecter tooBox. Télécharger, obtenir, supprimer, répertorier vos fichiers et bien plus encore"
[delaydoc]: ./connectors-native-delay.md "Effectuer des actions différées"
[dropboxdoc]: ./connectors-create-api-dropbox.md "Se connecter tooDropbox. Télécharger, obtenir, supprimer, répertorier vos fichiers et bien plus encore"
[facebookdoc]: ./connectors-create-api-facebook.md "Se connecter tooFacebook. Valider tooa chronologie, obtenir une page de flux et bien plus encore"
[githubdoc]: ./connectors-create-api-github.md "Se connecter tooGitHub et le suivi des problèmes"
[google-drivedoc]: ./connectors-create-api-googledrive.md "Se connecter tooGoogleDrive afin de pouvoir travailler avec vos données"
[google-sheetsdoc]: ./connectors-create-api-googlesheet.md "Se connecter tooGoogle feuilles peut modifier vos feuilles"
[google-tasksdoc]: ./connectors-create-api-googletasks.md "Se connecte tooGoogle tâches vous pouvez de gérer vos tâches"
[google-calendardoc]: ./connectors-create-api-googlecalendar.md "Se connecte tooGoogle Calendrier et peut gérer le calendrier."
[http-responsedoc]: ./connectors-native-reqres.md "Ajouter des actions pour HTTP demandes et réponses tooyour logic apps"
[instagramdoc]: ./connectors-create-api-instagram.md "Se connecter tooInstagram. Déclencher ou agir sur les événements"
[mailchimpdoc]: ./connectors-create-api-mailchimp.md "Se connecter tooyour MailChimp compte. Gérer et automatiser les courriers électroniques"
[mandrilldoc]: ./connectors-create-api-mandrill.md "Se connecter tooMandrill pour la communication"
[microsoft-translatordoc]: ./connectors-create-api-microsofttranslator.md "Se connecter tooMicrosoft traducteur. Traduire du texte, détecter les langues et bien plus encore" 
[office365-usersdoc]: ./connectors-create-api-office365-users.md 
[office365-videodoc]: ./connectors-create-api-office365-video.md "Obtenir des informations vidéo, des listes et des canaux vidéo, et des URL de lecture pour les vidéos Office 365"
[onedrivedoc]: ./connectors-create-api-onedrive.md "Se connecter tooyour personnel Microsoft OneDrive. Télécharger, supprimer, répertorier des fichiers et bien plus encore"
[onedrive-for-businessdoc]: ./connectors-create-api-onedriveforbusiness.md "Se connecter tooyour entreprise Microsoft OneDrive. Télécharger, supprimer, répertorier vos fichiers et bien plus encore"
[outlook.comdoc]: ./connectors-create-api-outlook.md "Connecter la boîte aux lettres de tooyour Outlook. Gérer votre courrier électronique, vos calendriers, vos contacts et bien plus encore"
[project-onlinedoc]: ./connectors-create-api-projectonline.md "Se connecter tooMicrosoft Project Online. Gérer vos projets, vos tâches, vos ressources et bien plus encore"
[querydoc]: ./connectors-native-query.md "Sélectionner et filtrer les tableaux avec l’action de requête hello"
[rssdoc]: ./connectors-create-api-rss.md "Publier et de récupérer des éléments de flux, de déclencher des opérations lorsqu’un nouvel élément est publié tooan RSS flux."
[sendgriddoc]: ./connectors-create-api-sendgrid.md "Se connecter tooSendGrid. Envoyer un courrier électronique et gérer les listes des destinataires"
[sftpdoc]: ./connectors-create-api-sftp.md "Connecter tooyour SFTP compte. Télécharger, obtenir, supprimer des fichiers et bien plus encore"
[slackdoc]: ./connectors-create-api-slack.md "Se connecter tooSlack et publier des messages tooSlack canaux"
[smtpdoc]: ./connectors-create-api-smtp.md "Connecter le serveur SMTP de tooa et envoyer un courrier électronique avec des pièces jointes"
[sparkpostdoc]: ./connectors-create-api-sparkpost.md "Se connecte tooSparkPost pour la communication"
[trellodoc]: ./connectors-create-api-trello.md "Se connecter tooTrello. Gérer vos projets et organiser ce que vous voulez avec qui vous voulez"
[twiliodoc]: ./connectors-create-api-twilio.md "Se connecter tooTwilio. Envoyer et obtenir des messages, obtenir des numéros disponibles, gérer des numéros de téléphone entrants et bien plus encore"
[wunderlistdoc]: ./connectors-create-api-wunderlist.md "Se connecter tooWunderlist. Gérer vos tâches et vos listes de tâches, tenir votre vie à jour et bien plus encore"
[yammerdoc]: ./connectors-create-api-yammer.md "Se connecter tooYammer. Publier des messages, obtenir de nouveaux messages et bien plus encore"
[youtubedoc]: ./connectors-create-api-youtube.md "Se connecter tooYouTube. Gérer vos vidéos et vos canaux"


<!--Icon references-->
[appFiguresicon]: ./media/apis-list/appfigures.png
[Asanaicon]: ./media/apis-list/asana.png
[Azure-Automation-icon]: ./media/apis-list/azure-automation.png
[AzureBlobStorageicon]: ./media/apis-list/azureblob.png
[Azure-Data-Lake-icon]: ./media/apis-list/azure-data-lake.png
[Azure-DocumentDBicon]: ./media/apis-list/azure-documentdb.png
[Azure-MLicon]: ./media/apis-list/azureml.png
[Azure-Resource-Manager-icon]: ./media/apis-list/azure-resource-manager.png
[Azure-Queues-icon]: ./media/apis-list/azure-queues.png
[Basecamp-3icon]: ./media/apis-list/basecamp.png
[Bitbucket-icon]: ./media/apis-list/bitbucket.png
[Bitlyicon]: ./media/apis-list/bitly.png
[BizTalk-Servericon]: ./media/apis-list/biztalk.png
[Bloggericon]: ./media/apis-list/blogger.png
[Boxicon]: ./media/apis-list/box.png
[Campfireicon]: ./media/apis-list/campfire.png
[Cognitive-Services-Text-Analyticsicon]: ./media/apis-list/cognitiveservicestextanalytics.png
[DB2icon]: ./media/apis-list/db2.png
[Dropboxicon]: ./media/apis-list/dropbox.png
[Dynamics-365icon]: ./media/apis-list/dynamicscrmonline.png
[Dynamics-365-for-Financialsicon]: ./media/apis-list/madeira.png
[Dynamics-365-for-Operationsicon]: ./media/apis-list/dynamicsax.png
[Easy-Redmineicon]: ./media/apis-list/easyredmine.png
[Event-Hubs-icon]: ./media/apis-list/eventhubs.png
[Facebookicon]: ./media/apis-list/facebook.png
[FTPicon]: ./media/apis-list/ftp.png
[GitHubicon]: ./media/apis-list/github.png
[Google-Calendaricon]: ./media/apis-list/googlecalendar.png
[Google-Driveicon]: ./media/apis-list/googledrive.png
[Google-Sheetsicon]: ./media/apis-list/googlesheet.png
[Google-Tasksicon]: ./media/apis-list/googletasks.png
[HideKeyicon]: ./media/apis-list/hidekey.png
[HipChaticon]: ./media/apis-list/hipchat.png
[Informixicon]: ./media/apis-list/informix.png
[Insightlyicon]: ./media/apis-list/insightly.png
[Instagramicon]: ./media/apis-list/instagram.png
[Instapapericon]: ./media/apis-list/instapaper.png
[JIRAicon]: ./media/apis-list/jira.png
[MailChimpicon]: ./media/apis-list/mailchimp.png
[Mandrillicon]: ./media/apis-list/mandrill.png
[Microsoft-Translatoricon]: ./media/apis-list/microsofttranslator.png
[MQicon]: ./media/apis-list/mq.png
[Office-365-Outlookicon]: ./media/apis-list/office365.png
[Office-365-Usersicon]: ./media/apis-list/office365users.png
[Office-365-Videoicon]: ./media/apis-list/office365video.png
[OneDriveicon]: ./media/apis-list/onedrive.png
[OneDrive-for-Businessicon]: ./media/apis-list/onedriveforbusiness.png
[Oracle-DB-icon]: ./media/apis-list/oracle-db.png
[Outlook.comicon]: ./media/apis-list/outlook.png
[PagerDutyicon]: ./media/apis-list/pagerduty.png
[Pinteresticon]: ./media/apis-list/pinterest.png
[Project-Onlineicon]: ./media/apis-list/projectonline.png
[Redmineicon]: ./media/apis-list/redmine.png
[RSSicon]: ./media/apis-list/rss.png
[Common-Data-Serviceicon]: ./media/apis-list/runtimeservice.png
[Salesforceicon]: ./media/apis-list/salesforce.png
[SAPicon]: ./media/apis-list/sap.png
[SendGridicon]: ./media/apis-list/sendgrid.png
[Service-Busicon]: ./media/apis-list/servicebus.png
[SFTPicon]: ./media/apis-list/sftp.png
[SharePointicon]: ./media/apis-list/sharepointonline.png
[Slackicon]: ./media/apis-list/slack.png
[Smartsheeticon]: ./media/apis-list/smartsheet.png
[SMTPicon]: ./media/apis-list/smtp.png
[SparkPosticon]: ./media/apis-list/sparkpost.png
[SQL-Servericon]: ./media/apis-list/sql.png
[Todoisticon]: ./media/apis-list/todoist.png
[Trelloicon]: ./media/apis-list/trello.png
[Twilioicon]: ./media/apis-list/twilio.png
[Twittericon]: ./media/apis-list/twitter.png
[Vimeoicon]: ./media/apis-list/vimeo.png
[Visual-Studio-Team-Servicesicon]: ./media/apis-list/visualstudioteamservices.png
[WordPressicon]: ./media/apis-list/wordpress.png
[Wunderlisticon]: ./media/apis-list/wunderlist.png
[Yammericon]: ./media/apis-list/yammer.png
[YouTubeicon]: ./media/apis-list/youtube.png

<!-- Primitive Icons -->
[API/Web-Appicon]: ./media/apis-list/api.png
[Azure-Functionsicon]: ./media/apis-list/function.png
[Delayicon]: ./media/apis-list/delay.png
[FileSystemIcon]: ./media/apis-list/filesystem.png
[HTTPicon]: ./media/apis-list/http.png
[HTTP-Requesticon]: ./media/apis-list/request.png
[HTTP-Responseicon]: ./media/apis-list/response.png
[HTTP-Swaggericon]: ./media/apis-list/http_swagger.png
[Nested-Logic-Appicon]: ./media/apis-list/workflow.png
[Recurrenceicon]: ./media/apis-list/recurrence.png
[Queryicon]: ./media/apis-list/query.png
[Webhookicon]: ./media/apis-list/webhook.png

<!-- EIP Icons -->
[as2icon]: ./media/apis-list/as2.png
[x12icon]: ./media/apis-list/x12new.png
[flatfileicon]: ./media/apis-list/flatfileencoding.png
[flatfiledecodeicon]: ./media/apis-list/flatfiledecoding.png
[xmlvalidateicon]: ./media/apis-list/xmlvalidation.png
[xmltransformicon]: ./media/apis-list/xsltransform.png
[integrationaccounticon]: ./media/apis-list/integrationaccount.png
