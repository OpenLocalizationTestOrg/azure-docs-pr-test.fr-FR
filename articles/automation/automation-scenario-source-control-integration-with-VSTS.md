---
title: "Intégration d’Azure Automation au contrôle de code source Visual Studio Team Services | Microsoft Docs"
description: "Ce scénario vous guide pour la configuration de l’intégration dans un compte Azure Automation et pour le contrôle de code source Visual Studio Team Services."
services: automation
documentationcenter: 
author: eamono
manager: 
editor: 
keywords: "Azure powershell, VSTS, contrôle de code source, automation"
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.openlocfilehash: 01f9c01c9e04e02dbb548b68cf99684ba6ddd57e
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-visual-studio-team-services"></a>Scénario Azure Automation - Intégration du contrôle de code source Automation dans Visual Studio Team Services

Dans ce scénario, vous avez un projet Visual Studio Team Services que vous utilisez pour gérer des runbook Azure Automation ou des configurations DSC avec un contrôle de code source.
Cet article décrit comment intégrer VSTS dans votre environnement Azure Automation pour assurer une intégration continue pour chaque archivage.

## <a name="getting-the-scenario"></a>Obtention du scénario

Ce scénario se compose de deux runbooks PowerShell que vous pouvez importer directement depuis la [galerie de runbooks](automation-runbook-gallery.md) dans le portail Azure ou télécharger depuis [PowerShell Gallery](https://www.powershellgallery.com).

### <a name="runbooks"></a>Runbooks

Runbook | Description| 
--------|------------|
Sync-VSTS | Importer des runbooks ou des configurations à partir du contrôle de code source VSTS lorsqu’un archivage est effectué. En cas d’exécution manuelle, cette fonction importe et publie tous les runbooks et toutes les configurations dans le compte Automation.| 
Sync-VSTSGit | Importer des runbooks ou des configurations à partir du contrôle de code source VSTS sous Git lorsqu’un archivage est effectué. En cas d’exécution manuelle, cette fonction importe et publie tous les runbooks et toutes les configurations dans le compte Automation.|

### <a name="variables"></a>Variables

Variable | Description|
-----------|------------|
VSToken | Ressource de variable sécurisée que vous allez créer qui contient le jeton d’accès personnel VSTS. Vous pouvez apprendre à créer un jeton d’accès personnel VSTS sur la [page d’authentification VSTS](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview). 
## <a name="installing-and-configuring-this-scenario"></a>Installation et configuration de ce scénario

Créez un [jeton d’accès personnel](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) dans VSTS que vous utiliserez pour synchroniser les runbooks ou les configurations dans votre compte Automation.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPersonalToken.png) 

Créez une [variable securisée](automation-variables.md) dans votre compte Automation pour stocker le jeton d’accès personnel afin que le runbook puisse s’authentifier dans VSTS et synchroniser les runbooks ou les configurations dans le compte Automation. Vous pouvez la nommer VSToken. 

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSTokenVariable.png)

Importez le runbook qui se synchronise vos runbooks ou configurations dans le compte Automation. Vous pouvez utiliser [l’exemple de runbook VSTS](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) ou [l’exemple de runbook VSTS avec Git] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) à partir de PowerShellGallery.com selon que vous utilisez VSTS ou le contrôle de code source VSTS avec Git pour effectuer un déploiement dans votre compte automation.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPowerShellGallery.png)

Vous pouvez à présent [publier](automation-creating-importing-runbook.md#publishing-a-runbook) ce runbook pour créer un webhook. 
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPublishRunbook.png)

Créez un [webhook](automation-webhooks.md) pour ce runbook Sync-VSTS et renseigner les paramètres comme indiqué ci-dessous. Veillez à effectuer une copie de l’URL du webhook, car vous en aurez besoin pour un crochet de service dans VSTS. VSAccessTokenVariableName est le nom (VSToken) de la variable sécurisée que vous avez créée précédemment pour stocker le jeton d’accès personnel. 

L’intégration dans VSTS (Sync-VSTS.ps1) aura les paramètres suivants.
### <a name="sync-vsts-parameters"></a>Paramètres Sync-VSTS

Paramètre | Description| 
--------|------------|
WebhookData | Ce paramètre contiendra les informations d’archivage envoyées dans le crochet de service VSTS. Laissez ce paramètre vide.| 
ResourceGroup | Nom du groupe de ressources dans lequel se trouve le compte Automation.|
AutomationAccountName | Le nom du compte Automation qui se synchronise sur VSTS.|
VSFolder | Nom du dossier dans VSTS dans lequel se trouvent les runbooks et les configurations.|
VSAccount | Nom du compte Visual Studio Team Services.| 
VSAccessTokenVariableName | Nom de la variable sécurisée (VSToken) qui contient le jeton d’accès personnel VSTS.| 


![](media/automation-scenario-source-control-integration-with-VSTS/VSTSWebhook.png)

Si vous utilisez VSTS avec GIT (Sync-VSTSGit.ps1), il aura les paramètres suivants.

Paramètre | Description|
--------|------------|
WebhookData | Ce paramètre contiendra les informations d’archivage envoyées dans le crochet de service VSTS. Laissez ce paramètre vide.| ResourceGroup | Nom du groupe de ressources dans lequel se trouve le compte Automation.|
AutomationAccountName | Le nom du compte Automation qui se synchronise sur VSTS.|
VSAccount | Nom du compte Visual Studio Team Services.|
VSProject | Nom du projet dans VSTS dans lequel se trouvent les runbooks et les configurations.|
GitRepo | Nom du référentiel Git.|
GitBranch | Le nom de la branche de référentiel Git VSTS.|
Dossier | Nom du dossier dans la branche Git VSTS.|
VSAccessTokenVariableName | Nom de la variable sécurisée (VSToken) qui contient le jeton d’accès personnel VSTS.|

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSGitWebhook.png)

Créer un crochet de service dans VSTS pour les archivages dans le dossier qui déclenche ce webhook lors de l’archivage de code. Sélectionnez Web Hooks en tant que service à intégrer lorsque vous créez un nouvel abonnement. Pour en savoir plus sur les webhooks de service, consultez la [documentation sur les webhooks de service VSTS](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started).
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSServiceHook.png)

Vous êtes maintenant être en mesure d’effectuer tous les archivages de vos runbooks et configurations dans VSTS et de les synchroniser automatiquement dans votre compte Automation.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSSyncRunbookOutput.png)

Si vous exécutez ce runbook manuellement sans déclenchement par VSTS, vous pouvez laisser le paramètre webhookdata vide et il effectuera une synchronisation complète du dossier VSTS spécifié.

Si vous souhaitez désinstaller le scénario, supprimez le crochet de service de VSTS, supprimez le runbook et la variable VSToken.
