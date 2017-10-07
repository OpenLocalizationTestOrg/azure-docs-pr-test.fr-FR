---
title: "aaaEnable d’analyse et des diagnostics dans Microsoft Azure | Documents Microsoft"
description: "Découvrez comment tooset des diagnostics pour vos ressources dans Azure."
author: rboucher
manager: carolz
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: af1947a9-c211-4aa1-8924-880a86240be4
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: robb
ms.openlocfilehash: 865d010c5846fff6d871e20eca2bc4ac35028354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-monitoring-and-diagnostics"></a>Activation de la surveillance et des diagnostics
Bonjour [Azure Portal](https://portal.azure.com), vous pouvez configurer les données de surveillance et de diagnostic riches, fréquentes, sur vos ressources. Vous pouvez également utiliser hello [API REST](https://msdn.microsoft.com/library/azure/dn931932.aspx) ou [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooconfigure diagnostics par programme.

Les données de diagnostic, de surveillance et de mesure d’Azure sont enregistrées dans le compte de stockage de votre choix. Cela vous permet de toouse les outils vous voulez des données de hello tooread, à partir d’un Explorateur de stockage, outils de tiers toothird tooPower BI.

## <a name="when-you-create-a-resource"></a>Lorsque vous créez une ressource
La plupart des services autoriser tooenable diagnostics lorsque vous les créez tout d’abord Bonjour [Azure Portal](https://portal.azure.com).

1. Accédez trop**nouveau** et sélectionnez une ressource hello vous intéressez.
2. Sélectionnez **Configuration facultative**.
    ![Panneau des diagnostics](./media/insights-how-to-use-diagnostics/Insights_CreateTime.png)
3. Sélectionnez **Diagnostics**, puis cliquez sur **Activé**. Vous devrez le compte de stockage hello toochoose que vous souhaitez toobe diagnostics enregistré dans. Vous seront facturés tarif de données normal pour le stockage et les transactions lorsque vous envoyez le compte de stockage de diagnostics tooa.
4. Cliquez sur **OK** et créer la ressource de hello.

## <a name="change-settings-for-an-existing-resource"></a>Modifiez les paramètres d'une ressource existante
Si vous avez déjà créé une ressource et les paramètres de diagnostic toochange hello (niveau toochange hello de collecte de données, par exemple), vous pouvez effectuer ce droit Bonjour portail Azure.

1. Accédez toohello ressource et cliquez sur hello **paramètres** commande.
2. Sélectionnez **Diagnostics**.
3. Hello **Diagnostics** panneau a tous les diagnostics de possibles hello et analyse des données de regroupement pour cette ressource. Pour certaines ressources vous pouvez également choisir une **rétention** stratégie pour les données hello, tooclean, configurez-le à partir de votre compte de stockage.
    ![Diagnostics de stockage](./media/insights-how-to-use-diagnostics/Insights_StorageDiagnostics.png)
4. Une fois que vous avez choisi vos paramètres, cliquez sur hello **enregistrer** commande. Il peut prendre un peu alors que pour l’analyse des données tooshow des si vous activez il pour hello première fois.

### <a name="categories-of-data-collection-for-virtual-machines"></a>Catégories de collecte de données pour les machines virtuelles
Pour les ordinateurs virtuels toutes les mesures et les journaux seront enregistrés à des intervalles d’une minute, ainsi, vous pouvez hello la plupart des informations à jour sur votre ordinateur.

* **Mesures de base** : mesures sur l'état d'intégrité de votre machine virtuelle (par ex., processeur et mémoire)
* **Mesures réseau et mesures Web** : mesures concernant vos connexions réseau et services Web
* **Les métriques .NET** : mesures à propos des applications .NET et ASP.NET hello en cours d’exécution sur votre machine virtuelle
* **Mesures SQL** : si vous exécutez Microsoft SQL Service, ses mesures de performances
* **Journaux des événements application Windows** : des événements Windows qui sont envoyés de canal d’application toohello
* **Journaux des événements système Windows** : des événements Windows qui sont envoyés de canal du système toohello. Cela inclut également tous les événements de [Microsoft Antimalware](http://go.microsoft.com/fwlink/?LinkID=404171&clcid=0x409).
* **Journaux des événements sécurité Windows** : des événements Windows qui sont envoyés de canal de sécurité toohello
* **Journaux d’infrastructure de diagnostics** : journalisation sur l’infrastructure de collecte des diagnostics hello
* **Journaux IIS** : journaux concernant votre serveur IIS

Notez que pour l’instant certaines distributions de Linux ne sont pas pris en charge, et hello Agent invité doit être installé sur l’ordinateur virtuel de hello.

## <a name="next-steps"></a>Étapes suivantes
* [Réceptions de notifications d’alerte](insights-receive-alert-notifications.md) lorsque des événements opérationnels se produisent ou que des mesures dépassent un seuil.
* [Surveiller les métriques de service](insights-how-to-customize-monitoring.md) toomake que votre service est disponible et réactive.
* [Mettre automatiquement à l’échelle le nombre d’instances](insights-how-to-scale.md) toomake que la mise à l’échelle votre service basé sur la demande.
* [Surveiller les performances de l’application](../application-insights/app-insights-azure-web-apps.md) si vous souhaitez toounderstand exactement comment votre code s’exécute dans le cloud de hello.
* [Afficher les événements et le journal d’activité](insights-debugging-with-events.md) toolearn tout ce qui s’est produite dans votre service.
* [Effectuer le suivi de l’intégrité du service](insights-service-health.md) toofind out lorsque Azure a rencontré des interruptions de service ou une dégradation des performances.

