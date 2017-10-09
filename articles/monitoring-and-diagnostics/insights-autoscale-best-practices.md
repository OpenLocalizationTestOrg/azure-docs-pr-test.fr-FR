---
title: "pratiques aaaBest pour la mise à l’échelle | Documents Microsoft"
description: "Modèles de mise à l’échelle automatique d’Azure pour Web Apps, Virtual Machine Scale Sets et Cloud Services"
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 9fa2b94b-dfa5-4106-96ff-74fd1fba4657
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: ancav
ms.openlocfilehash: eb731c15e440af93a2675210583878814d0d8818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-autoscale"></a>Meilleures pratiques pour la mise à l’échelle automatique
Cet article explique les meilleures pratiques tooautoscale, dans Azure. Mise à l’échelle du moniteur Azure s’applique uniquement trop[machines virtuelles identiques](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [Services de cloud computing](https://azure.microsoft.com/services/cloud-services/), et [du Service d’applications - applications Web](https://azure.microsoft.com/services/app-service/web/). Les autres services Azure utilisent des méthodes de mise à l’échelle différentes.

## <a name="autoscale-concepts"></a>Concepts de la mise à l’échelle automatique
* Une ressource ne peut avoir qu’ *un* paramètre de mise à l’échelle automatique
* Un paramètre de mise à l’échelle automatique peut comporter un ou plusieurs profils et chaque profil peut avoir une ou plusieurs règles de mise à l’échelle automatique.
* Un paramètre de mise à l’échelle s’adapte instances horizontalement, qui est *hors* en augmentant les instances hello et *dans* en diminuant le nombre de hello d’instances.
  Un paramètre de mise à l’échelle automatique a une valeur d’instances maximum, minimum et par défaut.
* Un travail de mise à l’échelle lit toujours hello associés aux métrique tooscale en vérifiant si elle a atteint hello le seuil configuré pour la montée en puissance parallèle ou d’échelle. Vous pouvez afficher une liste des mesures pour la mise à l’échelle automatique dans la rubrique [Mesures courantes de mise à l’échelle automatique Azure Monitor](insights-autoscale-common-metrics.md).
* Tous les seuils sont calculés au niveau de l’instance. Par exemple, « montée en puissance par 1 instance lorsque moyenne du processeur > 80 % lorsque le nombre d’instances est 2 », signifie la montée en puissance parallèle lorsque hello moyenne du processeur entre toutes les instances est supérieur à 80 %.
* Vous recevez toujours les notifications d’erreur par e-mail. Plus précisément, hello propriétaire, collaborateur et les lecteurs de ressources cible de hello reçoivent le message électronique. Vous recevez également un e-mail de *récupération* lorsque la mise à l’échelle automatique se rétablit après une défaillance et fonctionne à nouveau normalement.
* Vous pouvez participer tooreceive une notification d’action réussie de l’échelle par e-mail et de webhooks.

## <a name="autoscale-best-practices"></a>Meilleures pratiques relatives à la mise à l’échelle automatique
Utilisez hello suivant les meilleures pratiques que vous utilisez la mise à l’échelle.

### <a name="ensure-hello-maximum-and-minimum-values-are-different-and-have-an-adequate-margin-between-them"></a>Vérifiez les valeurs minimale et maximale hello sont différents et ont une marge suffisante entre eux
Si vous disposez d’un paramètre qui a minimum = 2, maximale = 2 et le nombre d’instances actuelles hello est 2, aucune action de mise à l’échelle ne peut se produire. Conserver une marge suffisante entre les nombres d’instance minimum et maximum hello, qui sont inclus. La mise à l’échelle agit toujours entre ces limites.

### <a name="manual-scaling-is-reset-by-autoscale-min-and-max"></a>La mise à l’échelle manuelle est réinitialisée par les valeurs min et max de mise à l’échelle
Si vous mettez à jour hello instance nombre tooa valeur ci-dessus manuellement ou que vous inférieure hello, hello du moteur de mise à l’échelle automatiquement met à l’échelle minimale de toohello précédent (le cas ci-dessous) ou hello maximale (le cas ci-dessus). Par exemple, vous définissez plage hello entre 3 et 6. Si vous avez une instance en cours d’exécution, moteur de mise à l’échelle hello dimensionne too3 instances lors de sa prochaine exécution. De même, il serait mise à l’échelle de 8 instances sauvegarder too6 lors de sa prochaine exécution.  Mise à l’échelle manuelle est temporaire, sauf si vous réinitialisez également les règles de mise à l’échelle hello.

### <a name="always-use-a-scale-out-and-scale-in-rule-combination-that-performs-an-increase-and-decrease"></a>Utilisez toujours une combinaison de règle d’augmentation et de diminution de la taille des instances qui exécute une augmentation et une diminution
Si vous utilisez uniquement une partie de la combinaison de hello, mise à l’échelle mise à l’échelle en unique, ou, jusqu'à ce que hello maximum ou minimum, a été atteint.

### <a name="do-not-switch-between-hello-azure-portal-and-hello-azure-classic-portal-when-managing-autoscale"></a>Ne passez pas de type hello portail Azure et hello portail Azure classic, lors de la gestion de mise à l’échelle
Pour les Services de cloud computing et les Services d’application (applications Web), utilisez hello portail Azure (portal.azure.com) toocreate et gérer les paramètres de mise à l’échelle. Pour les machines virtuelles identiques toocreate PowerShell, CLI ou l’API REST et gérer le paramètre de mise à l’échelle. Ne change pas entre hello portail Azure classic (manage.windowsazure.com) et hello portail Azure (portal.azure.com) lors de la gestion des configurations de mise à l’échelle. Hello portail Azure classic et ses principales sous-jacente présente des limitations. Déplacez la mise à l’échelle de toohello toomanage portail Azure à l’aide d’une interface utilisateur graphique. les options de Hello sont toouse hello échelle PowerShell, CLI ou une API REST (via l’Explorateur de ressources Azure).

### <a name="choose-hello-appropriate-statistic-for-your-diagnostics-metric"></a>Choisir hello de statistique appropriée pour vos métriques de diagnostic
Pour les métriques de diagnostics, vous pouvez choisir parmi *moyenne*, *Minimum*, *maximale* et *Total* comme une mesure tooscale par. Hello plus courante est *moyenne*.

### <a name="choose-hello-thresholds-carefully-for-all-metric-types"></a>Choisissez les seuils hello avec soin pour tous les types de mesure
Nous vous recommandons de choisir avec soin des seuils différents pour l’augmentation de la taille des instances et la diminution de la taille des instances en fonction des pratiques.

Nous *déconseillons* comme exemples hello ci-dessous avec les paramètres de mise à l’échelle hello des valeurs de seuil d’identiques ou très similaires pour et dans les conditions :

* Augmenter les instances de 1 lorsque le nombre de threads <= 600
* Diminuer les instances de 1 lorsque le nombre de threads >= 600

Examinons un exemple de ce qui peut entraîner le comportement tooa qui peut sembler déroutant. Envisagez de hello suivant la séquence.

1. Supposons il existe 2 toobegin instances avec et le nombre moyen de hello de threads par instance développe ensuite too625.
2. La mise à l’échelle automatique augmente la taille des instances en ajoutant une 3ème instance.
3. Ensuite, supposons que le nombre de threads de moyenne hello sur l’instance trouve too575.
4. Avant la mise à l’échelle vers le bas, mise à l’échelle tente tooestimate quel état final hello sera si elle est redimensionnée dans. Par exemple, 575 x 3 (nombre d’instances actuel) = 1 725 / 2 (nombre final d’instances lors de la descente en puissance) = 862,5 threads. Cela signifie qu’autoscale aurait tooimmediately montée en puissance parallèle à nouveau même après que elle à l’échelle, si hello moyen thread count reste hello même ou même situe uniquement une petite quantité. Toutefois, si elle mis à l’échelle, reprenez d’ensemble du processus hello, début boucle infinie de tooan.
5. tooavoid cette situation (appelée « battements »), mise à l’échelle n’évolue pas vers le bas du tout. Au lieu de cela, il ignore et réévalue condition hello nouveau hello prochaine heure hello du service s’exécute. Cela pourrait perturber de nombreuses personnes, car la mise à l’échelle ne s’affichent toowork lorsque le nombre de threads moyenne hello était 575.

Estimation lors d’une mise à l’échelle est prévue tooavoid « bagottement » les situations où les actions de mise à l’échelle et de montée en puissance parallèle accéder en permanence dans les deux sens. Gardez ce comportement à l’esprit lorsque vous choisissez hello mêmes seuils pour la montée en puissance parallèle et dans.

Nous vous recommandons de choisir une marge suffisante entre hello montée en puissance parallèle et de seuils. Par exemple, considérez hello suivant la meilleure combinaison de la règle.

* Augmenter les instances de 1 lorsque le % du processeur >= 80
* Diminuer les instances de 1 lorsque le % du processeur <= 60

Dans ce cas  

1. Supposons que 2 toostart instances avec.
2. Si hello % de l’UC moyenne entre les instances est too80, mise à l’échelle dotée de l’ajout d’une troisième instance de.
3. Supposons maintenant que sur le temps hello processeur % situe too60.
4. L’échelle de règle de mise à l’échelle évalue l’état final de hello s’il s’agissait de tooscale. Par exemple, 60 x 3 (nombre d’instances actuel) = 180 / 2 (nombre final d’instances lors de la descente en puissance) = 90. Par conséquent, mise à l’échelle ne pas échelle-dans, car cela aurait tooscale montée immédiatement. Au lieu de cela, elle ignore la descente en puissance.
5. échelle de temps suivant Hello vérifie, hello du processeur continue toofall too50. Elle estime à nouveau - instance 50 x 3 = 150 / 2 instances = 75, ce qui est sous le seuil de montée en puissance parallèle hello 80, afin qu’il met à l’échelle dans les instances de too2 avec succès.

### <a name="considerations-for-scaling-threshold-values-for-special-metrics"></a>Considérations relatives aux valeurs de seuil de la mise à l’échelle pour les mesures spéciales
 Pour les mesures spéciales telles que métrique de longueur de file d’attente du Bus de Service ou de stockage, seuil de hello est le nombre moyen de hello de messages disponibles par le nombre actuel d’instances. Choisissez soigneusement hello choisir la valeur de seuil de hello pour cette mesure.

Nous allons illustrer avec un exemple tooensure vous comprenez le comportement de hello mieux.

* Augmenter les instances de 1 lorsque le nombre de messages de file d’attente de stockage >= 50
* Diminuer les instances de 1 lorsque le nombre de messages de file d’attente de stockage <= 10

Tenez compte des hello suivant séquence :

1. Il existe 2 instances de file d’attente de stockage.
2. Messages conservent à venir et lorsque vous examinez la file d’attente de stockage hello, nombre total de hello lit 50. Vous pourriez supposer que la mise à l’échelle automatique devrait démarrer une action de montée en charge. Toutefois, notez que le nombre de messages par instance est de 50/2 = 25 messages. Par conséquent, la montée en charge ne se produit pas. Pour hello premier toohappen de montée en puissance parallèle, le nombre de messages total hello dans la file d’attente de stockage hello doit être 100.
3. Ensuite, supposons que le nombre de messages total hello atteint 100.
4. Une instance de file d’attente de stockage 3e est ajoutée en raison de l’action de montée en puissance parallèle tooa.  Hello prochaine action montée en puissance parallèle n’aura lieu que hello total nombre de messages dans la file d’attente hello atteint 150 car 150/3 = 50.
5. Nombre de hello de messages dans la file d’attente hello obtient désormais plus petit. Avec 3 instances, hello première échelle dans action qui se produit lorsque hello nombre total de messages dans les files d’attente additionner too30 car 30/3 = 10 messages par instance, qui est le seuil d’échelle dans hello.

### <a name="considerations-for-scaling-when-multiple-profiles-are-configured-in-an-autoscale-setting"></a>Considérations relatives à la mise à l’échelle lorsque plusieurs profils sont configurés dans un paramètre de mise à l’échelle automatique
Dans un paramètre de mise à l’échelle automatique, vous pouvez choisir un profil par défaut, qui est toujours appliqué indépendamment de toute planification ou de l’heure, ou vous pouvez choisir un profil récurrent ou un profil pour une durée fixe avec une plage de dates et d’heures.

Lorsque le service de mise à l’échelle les traite, il vérifie toujours Bonjour suivant l’ordre :

1. Profil de date fixe
2. Profil récurrent
3. Profil par défaut (« Toujours »)

Si une profil condition est remplie, mise à l’échelle ne vérifie pas de condition de profil suivante hello en dessous. La mise à l’échelle automatique ne traite qu’un seul profil à la fois. Cela signifie que si vous souhaitez tooalso incluent une condition de traitement d’un profil de niveau inférieur, vous devez inclure ces règles également dans le profil actuel de hello.

Examinons cela à l’aide d’un exemple :

image de Hello ci-dessous illustre un paramètre de mise à l’échelle avec un profil par défaut d’instances minimum = instances 2 et maximales = 10. Dans cet exemple, les règles sont tooscale configuré à la sortie lorsque le nombre de messages hello dans la file d’attente hello est supérieur à 10 et de la mise à l’échelle lorsque le nombre de messages hello dans la file d’attente hello est inférieure à 3. Désormais, les ressources hello peuvent évoluer entre 2 et 10 instances.

En outre, il existe un profil récurrent défini pour Lundi. Il est défini pour des instances minimum = 2 et des instances maximum = 12. Cela signifie que le lundi, échelle de temps de première hello vérifie cette condition, si le nombre d’instances hello est 2, il met à l’échelle toohello nouveau minimum de 3. Tant que la mise à l’échelle continue toofind cette condition profil mis en correspondance (lundi), elle traite uniquement en fonction de l’UC scale-out/dans règles hello configurés pour ce profil. À ce stade, il ne vérifie pas la longueur de file d’attente hello. Toutefois, si vous voulez également hello toobe du condition longueur de file d’attente activée, vous devez inclure également ces règles de profil par défaut de hello dans votre profil lundi.

De même, lors de la mise à l’échelle bascule le profil par défaut de toohello précédent, il vérifie d’abord si les conditions minimales et maximales hello sont remplies. Si le nombre de hello d’instances au moment de hello est 12, il met à l’échelle dans too10, hello maximale autorisée pour le profil par défaut de hello.

![paramètres de mise à l’échelle automatique](./media/insights-autoscale-best-practices/insights-autoscale-best-practices-2.png)

### <a name="considerations-for-scaling-when-multiple-rules-are-configured-in-a-profile"></a>Considérations relatives à la mise à l’échelle lorsque plusieurs règles sont configurées dans un profil
Il existe des cas où vous avez peut-être tooset plusieurs règles dans un profil. Hello suivant l’ensemble de règles de mise à l’échelle est utilisé par les services utilisent lorsque plusieurs règles sont définies.

Pour *l’augmentation de la taille des instances*, la mise à l’échelle automatique s’exécute si une règle est respectée.
Sur *dans l’échelle*, mise à l’échelle requièrent toutes les règles toobe remplie.

tooillustrate, supposez que vous avez hello suivant les règles de mise à l’échelle 4 :

* Si UC < 30 %, diminuer la taille des instances de 1
* Si Mémoire < 50 %, diminuer la taille des instances de 1
* Si UC > 75 %, augmenter la taille des instances de 1
* Si Mémoire > 75 %, augmenter la taille des instances de 1

Puis hello suivante se produit :

* Si le processeur est de 76 % et la mémoire est de 50 %, une augmentation de la taille des instances se produit.
* Si le processeur est de 50 % et la mémoire est de 76 %, une augmentation de la taille des instances se produit.

Hello d’autre part, si le processeur est 25 % et la mémoire est mise à l’échelle de 51 % **pas** dans l’échelle. Dans l’ordre dans tooscale, processeur doit être 29 % et la mémoire 49 %.

### <a name="always-select-a-safe-default-instance-count"></a>Sélectionnez toujours un nombre d’instances par défaut sans échec
nombre d’instances par défaut Hello est important de mise à l’échelle met à l’échelle le nombre de toothat service lorsque les mesures ne sont pas disponibles. Par conséquent, sélectionnez un nombre d’instances par défaut qui est sécurisé pour vos charges de travail.

### <a name="configure-autoscale-notifications"></a>Configuration des notifications de mise à l’échelle automatique
Mise à l’échelle avertit les administrateurs de hello et collaborateurs de ressource de hello par courrier électronique en cas de hello conditions suivantes :

* service de mise à l’échelle échoue tootake une action.
* Métriques ne sont pas disponibles pour le service de mise à l’échelle toomake une décision de mise à l’échelle.
* Les métriques sont disponible (récupération) à nouveau toomake une décision de mise à l’échelle.
  En outre toohello les conditions ci-dessus, vous pouvez configurer tooget de notifications par courrier électronique ou webhook notifié des actions de mise à l’échelle réussie.
  
Vous pouvez également utiliser un état d’intégrité de journal d’activité toomonitor alerte hello du moteur de mise à l’échelle hello. Voici des exemples trop[créer une alerte de journal activité toomonitor toutes les opérations du moteur de mise à l’échelle de votre abonnement](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert) ou trop[créer une alerte de journal activité toomonitor tout échec de la mise à l’échelle de la mise à l’échelle dans / mise à l’échelle des opérations votre abonnement](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).

## <a name="next-steps"></a>Étapes suivantes
- [Créer une alerte de journal activité toomonitor toutes les opérations du moteur de mise à l’échelle de votre abonnement.](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [Créer une alerte de journal activité toomonitor tout échec de la mise à l’échelle de la mise à l’échelle dans / monter en charge les opérations de votre abonnement](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)
