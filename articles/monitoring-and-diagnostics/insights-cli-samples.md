---
title: "exemples de démarrage rapide d’aaaAzure moniteur CLI 1.0. | Microsoft Docs"
description: "Exemples de commandes de l’interface CLI 1.0 pour accéder aux fonctionnalités d’Azure Monitor. Moniteur de Azure est un service Microsoft Azure qui vous permet de toosend des notifications d’alerte, des URL web appel en fonction des valeurs de données de télémétrie configuré et les Services de cloud computing de mise à l’échelle, les ordinateurs virtuels et les applications Web."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1653aa81-0ee6-4622-9c65-d4801ed9006f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6cd9cd62b3a1977276563f5e43f5384ccca66247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a>Exemple de démarrage rapide de l’interface CLI 1.0 multiplateforme pour Azure Monitor
Cet article explique les exemples de toohelp de commandes de l’interface de ligne de commande (CLI) vous accéder aux fonctionnalités du moniteur de Windows Azure. Moniteur de Azure vous permet de tooAutoScale Services de cloud computing, Machines virtuelles et les applications Web et toosend des notifications d’alerte ou des URL web appel en fonction des valeurs de données de télémétrie configuré.

> [!NOTE]
> Moniteur de Azure est hello nouveau nom pour ce qui a été appelé « Azure Insights » jusqu'à 25 septembre 2016. Toutefois, les espaces de noms hello et, par conséquent, les commandes hello ci-dessous encore contient insights » l’hello ».
> 
> 

## <a name="prerequisites"></a>Composants requis
Si vous n’avez pas déjà installé hello CLI d’Azure, consultez [installation Bonjour Azure CLI](../cli-install-nodejs.md). Si vous n’êtes pas familiarisé avec l’interface CLI d’Azure, vous pouvez en savoir plus sur à l’adresse [hello d’utilisation CLI d’Azure pour Mac, Linux et Windows avec Azure Resource Manager](../xplat-cli-azure-resource-manager.md).

Dans Windows, installez npm de hello [site Web Node.js](https://nodejs.org/). Au terme de l’installation de hello, à l’aide de CMD.exe avec des privilèges d’exécution en tant qu’administrateur, exécutez les hello qui suit à partir du dossier hello où npm est installé :

```console
npm install azure-cli --global
```

Ensuite, accédez tooany/emplacement du dossier souhaitée, puis tapez sur hello de ligne de commande :

```console
azure help
```

## <a name="log-in-tooazure"></a>Connectez-vous à tooAzure
première étape de Hello est toologin tooyour compte Azure.

```console
azure login
```

Après avoir exécuté cette commande, vous avez toosign dans via des instructions sur l’écran hello hello. Une fois cette opération effectuée, vos compte, ID de locataire et ID d’abonnement par défaut s’affichent. Toutes les commandes de travail dans le contexte de hello de votre abonnement par défaut.

Détails de hello toolist de votre abonnement actuel, utilisez hello commande suivante.

```console
azure account show
```

toochange travail contexte tooa autre abonnement, hello utilisez commande suivante.

```console
azure account set "subscription ID or subscription name"
```

toouse Azure Resource Manager et Azure moniteur des commandes, vous devez toobe en mode Azure Resource Manager.

```console
azure config mode arm
```

tooview une liste de toutes les commandes prises en charge de moniteur de Windows Azure, effectuez des opérations suivantes de hello.

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a>Afficher le journal d’activité pour un abonnement
tooview une liste des événements de journal d’activité, effectuez des opérations suivantes de hello.

```console
azure insights logs list [options]
```

Essayez de hello suivant tooview toutes les options disponibles.

```console
azure insights logs list -help
```

Voici un exemple des journaux de toolist par un groupe de ressources

```console
azure insights logs list --resourceGroup "myrg1"
```

Journaux de toolist exemple par l’appelant

```console
azure insights logs list --caller "myname@company.com"
```

Journaux de toolist exemple par l’appelant sur un type de ressource au sein d’une date de début et de fin

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a>Utilisation des alertes
Vous pouvez utiliser les informations de hello dans toowork de section hello des alertes.

### <a name="get-alert-rules-in-a-resource-group"></a>Obtenir des règles d’alerte dans un groupe de ressources
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a>Créer une règle d’alerte métrique
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a>Créer une règle d’alerte de test web
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a>Supprimer une règle d’alerte
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a>Profils de journal
Utilisez les informations de hello toowork de cette section avec des profils de journal.

### <a name="get-a-log-profile"></a>Obtenir un profil de journal
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a>Ajouter un profil de journal sans rétention
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a>Supprimer un profil de journal
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a>Ajouter un profil de journal avec rétention
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a>Ajouter un profil de journal avec rétention et EventHub
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a>Diagnostics
Utilisez les informations de hello toowork de cette section avec les paramètres de diagnostic.

### <a name="get-a-diagnostic-setting"></a>Obtenir un paramètre de diagnostic
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a>Désactiver un paramètre de diagnostic
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a>Activer un paramètre de diagnostic sans rétention
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a>Autoscale
Utilisez les informations de hello toowork de cette section avec les paramètres de mise à l’échelle. Vous devez toomodify ces exemples.

### <a name="get-autoscale-settings-for-a-resource-group"></a>Obtenir les paramètres de mise à l’échelle automatique pour un groupe de ressources
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a>Obtenir les paramètres de mise à l’échelle automatique par nom dans un groupe de ressources
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a>Définir les paramètres de mise à l’échelle automatique
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
