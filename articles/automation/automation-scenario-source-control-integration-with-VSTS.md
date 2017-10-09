---
title: "aaaIntegrate Azure Automation avec contrôle de code source Visual Studio Team Services | Documents Microsoft"
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
ms.openlocfilehash: 8f6faa596a5ad1f8b72e820ca320b3e103d83579
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-visual-studio-team-services"></a>Scénario Azure Automation - Intégration du contrôle de code source Automation dans Visual Studio Team Services

Dans ce scénario, vous avez un projet Visual Studio Team Services que vous utilisez des runbooks d’automatisation Azure toomanage ou les configurations DSC sous contrôle de code source.
Cet article décrit comment toointegrate VSTS à votre environnement Azure Automation afin que l’intégration continue se produit pour chaque archivage.

## <a name="getting-hello-scenario"></a>Scénario de hello mise en route

Ce scénario se compose de deux procédures opérationnelles PowerShell que vous pouvez importer directement à partir de hello [galerie de runbooks](automation-runbook-gallery.md) dans hello portail Azure ou les télécharger à partir de hello [PowerShell Gallery](https://www.powershellgallery.com).

### <a name="runbooks"></a>Runbooks

Runbook | Description| 
--------|------------|
Sync-VSTS | Importer des runbooks ou des configurations à partir du contrôle de code source VSTS lorsqu’un archivage est effectué. Si vous exécutez manuellement, il importer et publier toutes les procédures opérationnelles ou les configurations dans hello compte Automation.| 
Sync-VSTSGit | Importer des runbooks ou des configurations à partir du contrôle de code source VSTS sous Git lorsqu’un archivage est effectué. Si vous exécutez manuellement, il importer et publier toutes les procédures opérationnelles ou les configurations dans hello compte Automation.|

### <a name="variables"></a>variables

Variable | Description|
-----------|------------|
VSToken | Ressource de variable sécurisé, vous allez créer qui contient le jeton d’accès personnel hello VSTS. Vous pouvez apprendre comment toocreate personnelle VSTS aux jetons sur hello [page d’authentification VSTS](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview). 
## <a name="installing-and-configuring-this-scenario"></a>Installation et configuration de ce scénario

Créer un [jeton d’accès personnel](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) dans VSTS que vous utiliserez toosync hello runbooks ou les configurations dans votre compte automation.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPersonalToken.png) 

Créer un [variable secure](automation-variables.md) dans votre hello toohold du compte automation accès personnel jeton afin que hello runbook peut authentifier les runbooks hello tooVSTS et la synchronisation ou les configurations dans hello compte Automation. Vous pouvez la nommer VSToken. 

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSTokenVariable.png)

Importer le runbook hello synchroniser votre runbook ou les configurations dans le compte d’automatisation hello. Vous pouvez utiliser hello [VSTS exemple runbook](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) ou hello [VSTS avec l’exemple de runbook Git] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) à partir de hello PowerShellGallery.com selon que vous utilisez VSTS VSTS avec Git ou contrôle de source et déployer le compte d’automatisation tooyour.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPowerShellGallery.png)

Vous pouvez à présent [publier](automation-creating-importing-runbook.md#publishing-a-runbook) ce runbook pour créer un webhook. 
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPublishRunbook.png)

Créer un [webhook](automation-webhooks.md) pour ce runbook de VSTS de synchronisation et de remplissage dans paramètres hello comme indiqué ci-dessous. Veillez à que copier l’url du webhook hello car vous en aurez besoin pour un crochet de service dans VSTS. Hello VSAccessTokenVariableName est le nom de hello (VSToken) de la variable sécurisé de hello que vous avez créé le jeton d’accès personnel hello antérieur toohold. 

Intégration avec VSTS (synchronisation-VSTS.ps1) prendra hello paramètres suivants.
### <a name="sync-vsts-parameters"></a>Paramètres Sync-VSTS

Paramètre | Description| 
--------|------------|
WebhookData | Cela contient les informations de consignation hello envoyées à partir de raccordement de service hello VSTS. Laissez ce paramètre vide.| 
ResourceGroup | Il s’agit de nom hello hello du groupe de ressources qui hello automation compte se trouve dans.|
AutomationAccountName | nom de Hello du compte automation hello qui est synchronisés avec VSTS.|
VSFolder | Le nom du dossier de hello dans VSTS où hello runbooks et les configurations existent.|
VSAccount | nom Hello Hello compte Visual Studio Team Services.| 
VSAccessTokenVariableName | nom Hello de variable sécurisé hello (VSToken) qui contient le jeton d’accès personnel hello VSTS.| 


![](media/automation-scenario-source-control-integration-with-VSTS/VSTSWebhook.png)

Si vous utilisez VSTS avec GIT (synchronisation-VSTSGit.ps1), il prendra hello paramètres suivants.

Paramètre | Description|
--------|------------|
WebhookData | Cela contient les informations de consignation hello envoyées à partir de raccordement de service hello VSTS. Laissez ce paramètre vide.| ResourceGroup | Ce nom hello hello du groupe de ressources qui hello compte automation est.|
AutomationAccountName | nom de Hello du compte automation hello qui est synchronisés avec VSTS.|
VSAccount | nom Hello Hello compte Visual Studio Team Services.|
VSProject | nom Hello du projet hello dans VSTS où hello runbooks et les configurations existent.|
GitRepo | nom de Hello du référentiel Git de hello.|
GitBranch | nom de Hello de branche hello dans le référentiel Git de VSTS.|
Dossier | nom Hello du dossier hello dans la branche Git de VSTS.|
VSAccessTokenVariableName | nom Hello de variable sécurisé hello (VSToken) qui contient le jeton d’accès personnel hello VSTS.|

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSGitWebhook.png)

Créer un raccordement de service dans VSTS dossier toohello des archivages qui déclenche cet webhook sur l’archivage du code. Sélectionnez Web Hooks comme toointegrate de service hello avec lorsque vous créez un nouvel abonnement. Pour en savoir plus sur les webhooks de service, consultez la [documentation sur les webhooks de service VSTS](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started).
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSServiceHook.png)

Doit maintenant être en mesure de toodo tous les archivages de vos procédures opérationnelles et de configurations dans VSTS et que ces automatiquement synchronisation avait dans votre compte automation.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSSyncRunbookOutput.png)

Si vous exécutez ce runbook manuellement sans déclenchées par VSTS, vous pouvez laisser un paramètre de webhookdata hello vide et il effectuera une synchronisation complète à partir du dossier VSTS hello spécifié.

Si vous souhaitez le scénario de hello toouninstall, supprimez hello service raccordement VSTS, supprimer hello runbook et hello VSToken variable.
