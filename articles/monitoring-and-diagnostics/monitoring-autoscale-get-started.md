---
title: "aaaGet main de la mise à l’échelle dans Azure | Documents Microsoft"
description: "Découvrez comment tooscale vos ressources dans Azure."
author: rajram
manager: rboucher
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: rajram
ms.openlocfilehash: 6b3c3f4529018dcaf9691c538fec63dfbb3cea06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-autoscale-in-azure"></a>Bien démarrer avec la mise à l’échelle automatique dans Azure
Cet article décrit comment tooset vos paramètres de mise à l’échelle pour votre ressource dans le portail de Microsoft Azure hello.

Azure moniteur de mise à l’échelle s’applique uniquement toovirtual machines identiques, services de cloud computing, les plans de Service d’applications Azure et les environnements App Service. 

## <a name="discover-hello-autoscale-settings-in-your-subscription"></a>Découvrir les paramètres de mise à l’échelle hello dans votre abonnement
Vous pouvez découvrir toutes les ressources hello pour lesquels la mise à l’échelle est applicable dans le moniteur de Azure. Utilisez hello pour une procédure pas à pas comme suit :

1. Ouvrez hello [portail Azure.][1]
2. Cliquez sur icône du moniteur de Windows Azure hello dans le volet gauche de hello.
  ![Ouvrez Azure Monitor][2]
3. Cliquez sur **mise à l’échelle** tooview toutes les ressources de hello pour le mise à l’échelle n’est applicable, ainsi que leur état actuel de la mise à l’échelle.
  ![Découvrir la mise à l’échelle automatique dans Azure Monitor][3]

Vous pouvez utiliser le volet de filtre hello à tooscope supérieur de hello vers le bas des ressources de tooselect liste hello dans un groupe de ressources spécifique, les types de ressource spécifique ou une ressource spécifique.

Pour chaque ressource, vous trouverez du nombre d’instances actuelles hello et l’état de mise à l’échelle hello. Hello état de mise à l’échelle peut être :

- **Non configuré** : vous n’avez pas encore activé la mise à l’échelle automatique pour cette ressource.
- **Activé** : vous avez activé la mise à l’échelle automatique pour cette ressource.
- **Désactivé** : vous avez désactivé la mise à l’échelle automatique pour cette ressource.

## <a name="create-your-first-autoscale-setting"></a>Créez votre premier paramètre de mise à l’échelle automatique

Nous allons maintenant passer par un toocreate simple de procédure pas à pas le premier paramètre de mise à l’échelle.

1. Ouvrez hello **mise à l’échelle** panneau dans le moniteur de Windows Azure et sélectionnez une ressource que vous souhaitez tooscale. (hello étapes suivantes utilisent un plan App Service associé à une application web. Vous pouvez [créer votre première application Web ASP.NET dans Azure en 5 minutes][4])
2. Notez que le nombre d’instances actuelles hello est 1. Cliquez sur **Activer la mise à l’échelle automatique**.
  ![Paramètre d’échelle pour la nouvelle application web][5]
3. Fournissez un nom pour le paramètre d’échelle de hello, puis cliquez sur **ajouter une règle**. Notez que les options de règle de mise à l’échelle de hello qui s’ouvrent un volet contextuel à droite hello. Par défaut, cette opération définit tooscale d’option hello votre instance compter à 1 si hello pourcentage d’UC de ressource de hello dépasse 70 pour cent. Laissez les valeurs par défaut et cliquez sur **Ajouter**.
  ![Créer le paramètre de mise à l’échelle pour une application web][6]
4. Vous avez créé votre première règle de mise à l’échelle. Notez que hello UX recommande les meilleures pratiques et qui indique « il est recommandé de toohave au moins une échelle de la règle. » toodo pour :
  
    a. Cliquez sur **Ajouter une règle**. 

    b. Définissez **opérateur** trop**moins**.

    c. Définissez **seuil** trop**20**.

    d. Définissez **opération** trop**de diminuer le nombre par**.

   Vous devez maintenant avoir un paramètre de mise à l’échelle qui fait monter/diminuer en puissance en fonction de l’utilisation du processeur.
   ![Mise à l’échelle en fonction du processeur][8]
5. Cliquez sur **Enregistrer**.

Félicitations ! Vous avez maintenant créé votre premier tooautoscale de paramètre de mise à l’échelle votre application web basée sur l’utilisation du processeur.

> [!NOTE] 
> la même procédure Hello est applicable tooget démarré avec une échelle de machine virtuelle rôle du service cloud ou de jeu.

## <a name="other-considerations"></a>Autres points à considérer
### <a name="scale-based-on-a-schedule"></a>Mise à l'échelle en fonction d’une planification
En outre tooscale en fonction de l’UC, vous pouvez définir votre échelle différemment pour des jours spécifiques de la semaine de hello.

1. Cliquez sur **Ajouter une condition de mise à l’échelle**.
2. Définition des règles de mode et hello de montée en puissance hello est même hello en tant que condition de hello par défaut.
3. Sélectionnez **répéter des jours spécifiques** de planification de hello.
4. Sélectionnez les jours hello et l’heure de début et de fin de hello pour lorsque la condition de l’échelle hello doit être appliquée.

![Condition de mise à l’échelle basée sur une planification][9]
### <a name="scale-differently-on-specific-dates"></a>Mettre à l’échelle différemment à des dates spécifiques
En outre tooscale en fonction de l’UC, vous pouvez définir votre échelle différemment pour des dates spécifiques.

1. Cliquez sur **Ajouter une condition de mise à l’échelle**.
2. Définition des règles de mode et hello de montée en puissance hello est même hello en tant que condition de hello par défaut.
3. Sélectionnez **spécifier les dates de début et de fin** de planification de hello.
4. Sélectionnez les dates de début/fin hello et l’heure de début et de fin de hello pour lorsque la condition de l’échelle hello doit être appliquée.

![Condition de mise à l’échelle en fonction des dates][10]

### <a name="view-hello-scale-history-of-your-resource"></a>Afficher l’historique de l’échelle hello de votre ressource
Chaque fois que votre ressource est mise à l’échelle vers le haut ou vers le bas, un événement est consigné dans le journal d’activité hello. Vous pouvez afficher l’historique de l’échelle hello de votre ressource pour hello dernières 24 heures en basculant toohello **l’historique d’exécution** onglet.

![Historique d’exécution][11]

Si vous souhaitez que l’historique de l’échelle complète tooview hello (pour les jours d’activité too90), sélectionnez **cliquez ici toosee plus de détails**. journal d’activité Hello s’ouvre, avec mise à l’échelle présélectionnée pour votre ressource et la catégorie.

### <a name="view-hello-scale-definition-of-your-resource"></a>Afficher la définition de l’échelle hello de votre ressource
La mise à l’échelle est une ressource Azure Resource Manager. Vous pouvez afficher la définition de l’échelle de hello dans JSON en basculant toohello **JSON** onglet.

![Définition de mise à l’échelle][12]

Vous pouvez apporter des modifications dans le JSON directement, si nécessaire. Ces modifications apparaîtront après que les avoir enregistrées.

### <a name="disable-autoscale-and-manually-scale-your-instances"></a>Désactiver la mise à l’échelle automatique et mettre à l’échelle manuellement vos instances
Il peut y avoir heures lorsque vous souhaitez toodisable vos paramètres actuels de la mise à l’échelle et manuellement mettre à l’échelle de votre ressource.

Cliquez sur hello **désactiver la mise à l’échelle** bouton en haut de hello.
![Désactiver la mise à l’échelle automatique][13]

> [!NOTE] 
> Cette option désactive votre configuration. Toutefois, vous pouvez revenir tooit après avoir activé la mise à l’échelle. 

Vous pouvez maintenant définir le nombre de hello d’instances que vous souhaitez tooscale toomanually.

![Définir l’échelle manuelle][14]

Vous pouvez toujours revenir tooAutoscale en cliquant sur **activez** , puis **enregistrer**.

## <a name="next-steps"></a>Étapes suivantes
- [Créer une alerte de journal activité toomonitor toutes les opérations du moteur de mise à l’échelle de votre abonnement](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [Créer une alerte de journal activité toomonitor toutes les opérations de montée/mise à l’échelle mise à l’échelle sur votre abonnement](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)

<!--Reference-->
[1]:https://portal.azure.com
[2]: ./media/monitoring-autoscale-get-started/azure-monitor-launch.png
[3]: ./media/monitoring-autoscale-get-started/discover-autoscale-azure-monitor.png
[4]: https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-get-started-dotnet
[5]: ./media/monitoring-autoscale-get-started/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-get-started/create-scale-setting-web-app.png
[7]: ./media/monitoring-autoscale-get-started/scale-in-recommendation.png
[8]: ./media/monitoring-autoscale-get-started/scale-based-on-cpu.png
[9]: ./media/monitoring-autoscale-get-started/scale-condition-schedule.png
[10]: ./media/monitoring-autoscale-get-started/scale-condition-dates.png
[11]: ./media/monitoring-autoscale-get-started/scale-history.png
[12]: ./media/monitoring-autoscale-get-started/scale-definition-json.png
[13]: ./media/monitoring-autoscale-get-started/disable-autoscale.png
[14]: ./media/monitoring-autoscale-get-started/set-manualscale.png

