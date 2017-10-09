---
title: "Notez de retrait de 1 aaaGuest du système d’exploitation famille | Documents Microsoft"
description: "Fournit des informations sur lors de la mise hors service hello Azure invité famille 1 s’est produite et comment toodetermine si vous êtes concerné"
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 37b422e9-0713-4a81-a942-f553ef478064
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/21/2017
ms.author: raiye
ms.openlocfilehash: fa8b904c6560dbbe4982c301f818c7a5cbc4eacb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="guest-os-family-1-retirement-notice"></a>Informations relatives à la suppression de la famille 1 des systèmes d’exploitation invités
retrait de Hello de la famille 1 a été annoncé le 1er juin 2013.

**2 septembre 2014** hello système de d’exploitation invité Azure (s’invité) famille 1.x, qui est basé sur le système d’exploitation de hello Windows Server 2008, a été officiellement supprimé. Tous les services de nouvelles tentatives toodeploy ou mise à niveau des services existants à l’aide de la famille 1 échoue avec un message d’erreur vous informant que hello du système d’exploitation invités de famille 1 a été retirée.

**3 novembre 2014** La prise en charge étendue de la famille 1 des SE invités a pris fin et a été complètement supprimée. Tous les services toujours liés à la famille 1 seront affectés. Nous pouvons arrêter ces services à tout moment. Il n’existe aucune garantie que vos services continueront toorun, sauf si vous mettre à niveau manuellement les vous-même.

Si vous avez des questions supplémentaires, visitez hello [Forums des Services Cloud](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) ou [contactez le support Azure](https://azure.microsoft.com/support/options/).

## <a name="are-you-affected"></a>Êtes-vous concerné ?
Vos Services Cloud sont affectées si l’un des éléments suivants de hello s’applique :

1. Vous avez une valeur de « osFamily = « 1 » explicitement spécifiée dans le fichier ServiceConfiguration.cscfg de hello pour votre Service Cloud.
2. Il est inutile de valeur pour osFamily spécifié explicitement dans le fichier ServiceConfiguration.cscfg de hello pour votre Service Cloud. Actuellement, hello hello par défaut valeur par « 1 » dans ce cas.
3. Hello portail Azure répertorie la valeur de votre famille de système d’exploitation invité en tant que « Windows Server 2008 ».

toofind qui sont en cours d’exécution quelle famille du système d’exploitation de vos services cloud, vous pouvez exécuter hello suivant le script dans Azure PowerShell, toutefois vous devez [configurer Azure PowerShell](/powershell/azureps-cmdlets-docs) première. Pour plus d’informations sur le script de hello, consultez [Azure invité du système d’exploitation famille 1 fin de vie : juin 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

Vos services cloud seront affectées par la mise hors service de la famille 1 si la colonne osFamily de hello dans la sortie du script hello est vide ou contient des « 1 ».

## <a name="recommendations-if-you-are-affected"></a>Recommandations si vous êtes concerné
Nous vous conseillons de que migrer votre tooone de rôles de Service de cloud computing de familles de système d’exploitation invité hello pris en charge :

**Famille 4.x du SE invité** - Windows Server 2012 R2 *(recommandé)*

1. Assurez-vous que votre application utilise SDK 2.1 ou une version ultérieure avec .NET framework 4.0, 4.5 ou 4.5.1.
2. Définir le fichier ServiceConfiguration.cscfg de hello osFamily attribut hello en trop « 4 » et redéployez votre service cloud.

**Famille 3.x du SE invité** - Windows Server 2012

1. Assurez-vous que votre application utilise SDK 1.8 ou une version ultérieure avec .NET framework 4.0 ou 4.5.
2. Définir le fichier ServiceConfiguration.cscfg trop « 3 » hello en hello osFamily attribut et redéployez votre service cloud.

**Famille 2.x du SE invité** - Windows Server 2008 R2

1. Assurez-vous que votre application utilise SDK 1.3 ou une version ultérieure avec .NET framework 3.5 ou 4.0.
2. Définir le fichier ServiceConfiguration.cscfg de hello osFamily attribut hello en trop « 2 » et redéployez votre service cloud.

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a>Fin de la prise en charge étendue pour la famille 1 des SE invités depuis le 3 novembre 2014
Les services cloud de la famille 1 des SE invités ne sont plus pris en charge. Migrer la famille 1 dès que possible tooavoid toute interruption de service.  

## <a name="next-steps"></a>Étapes suivantes
Hello révision dernières [mises à jour de système d’exploitation invité](cloud-services-guestos-update-matrix.md).
