---
title: "aaaAutoscaling et l’environnement App Service v1"
description: "Mise à l’échelle automatique et environnement App Service"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: c23af2d8-d370-4b1f-9b3e-8782321ddccb
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 1a03cf494309e80596b64471d1a067b2f64a9fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="autoscaling-and-app-service-environment-v1"></a>Mise à l’échelle automatique et environnement App Service v1

> [!NOTE]
> Cet article porte sur hello environnement App Service v1.  Il existe une version plus récente de hello environnement App Service toouse plus facile et s’exécute sur une infrastructure plus puissante. toolearn plus d’informations sur la nouvelle version de hello commencent par Bonjour [Introduction toohello environnement App Service](../app-service/app-service-environment/intro.md).
> 

Les environnements Azure App Service prennent en charge la *mise à l’échelle automatique*. Vous pouvez mettre à l’échelle automatiquement des pools de Workers individuels en fonction de mesures ou de la planification.

![Options de mise à l’échelle automatique d’un pool de Workers.][intro]

Échelle permet d’optimiser votre utilisation des ressources par automatiquement agrandissement et réduction d’un toofit d’environnement du Service d’applications votre budget et charge profil.

## <a name="configure-worker-pool-autoscale"></a>Configurer la mise à l’échelle automatique du pool de Workers
Vous pouvez accéder à des fonctionnalités de mise à l’échelle hello de hello **paramètres** onglet du pool de travail hello.

![Onglet Paramètres de pool de travail hello.][settings-scale]

À partir de là, hello interface doit être assez familier, car elle est hello plan de la même expérience que vous voyez lorsque vous mettez à l’échelle un Service d’application. 

![Paramètres de mise à l’échelle manuelle.][scale-manual]

Vous pouvez également configurer un profil de mise à l’échelle automatique.

![Paramètres de mise à l’échelle automatique.][scale-profile]

Les profils de mise à l’échelle sont des limites de tooset utiles sur l’échelle. Ainsi, vous pouvez obtenir des résultats satisfaisants en définissant une valeur de mise à l’échelle limite inférieure (1) et une valeur de plafonnement prévisible en définissant une limite supérieure (2).

![Paramètres de mise à l’échelle dans le profil.][scale-profile2]

Après avoir défini un profil, vous pouvez ajouter tooscale de règles de mise à l’échelle pour monter ou descendre le nombre de hello d’instances dans le pool de travail hello dans les limites de hello définies par le profil de hello. Les règles de mise à l’échelle automatique sont basées sur les mesures.

![Règle de mise à l’échelle.][scale-rule]

 N’importe quel pool de travail ou les métriques frontal peut être utilisé toodefine les règles de mise à l’échelle. Ces mesures sont hello des alertes pour les mêmes métriques, vous pouvez surveiller dans les graphiques de panneau ressources hello ou définir.

## <a name="autoscale-example"></a>Exemple de mise à l’échelle automatique
La mise à l’échelle automatique d’un environnement App Service est mieux illustrée par un scénario.

Cet article explique toutes les considérations de hello nécessaires lorsque vous installez la mise à l’échelle. article de Hello vous guide tout au long de hello interactions qui entrent en lire lorsque vous factorisez les environnements App Service qui sont hébergées dans un environnement App Service dans l’échelle automatique.

### <a name="scenario-introduction"></a>Présentation du scénario
Frank est un administrateur système pour une entreprise qui a migré une partie des charges de travail hello qu’il gère tooan environnement App Service.

Hello est de l’environnement du Service d’applications configuré toomanual échelle comme suit :

* **Serveurs frontaux** : 3
* **Pool de Workers 1**: 10
* **Pool de Workers 2**: 5
* **Pool de Workers 3**: 5

Le pool de Workers 1 est utilisé pour les charges de travail, tandis que le pool de Workers 2 et le pool de Workers 3 sont utilisés pour les charges de travail de développement et d’assurance qualité.

Hello du Service d’applications des plans pour les questions et réponses et développement sont configurés toomanual mise à l’échelle. production de Hello plan App Service a la valeur toodeal tooautoscale avec des variations de charge et le trafic.

Il est très familier avec l’application hello. Il sait que les heures de pointe hello de charge sont entre 9:00 AM et 6:00 PM, car il s’agit d’une application de métier (LOB) par les employés lorsqu’ils sont dans office de hello. Le taux d’utilisation chute une fois que les utilisateurs ont fini leur journée de travail. En dehors des heures de pointe, il existe toujours une charge, car les utilisateurs peuvent accéder à distance application hello, à l’aide de leurs appareils mobiles ou des ordinateurs. production Hello plan App Service est déjà configuré tooautoscale basée sur l’utilisation du processeur par hello suivant les règles :

![Paramètres spécifiques pour une application métier.][asp-scale]

| **Profil de la mise à l’échelle automatique – Jours de semaine – Plan App Service** | **Profil de la mise à l’échelle automatique – Week-ends – Plan App Service** |
| --- | --- |
| **Nom :** profil jour de semaine |**Nom :** profil week-end |
| **Mise à l’échelle selon :** Planification et règles de performances |**Mise à l’échelle selon :** Planification et règles de performances |
| **Profil :** jours de la semaine |**Profil :** week-end |
| **Type :** périodicité |**Type :** périodicité |
| **Target plage :** 5 instances too20 |**Target plage :** 3 instances too10 |
| **Jours :** lundi, mardi, mercredi, jeudi, vendredi |**Jours :** samedi, dimanche |
| **Heure de début :** 9 h |**Heure de début :** 9 h |
| **Fuseau horaire :** UTC-08 |**Fuseau horaire :** UTC-08 |
|  | |
| **Règle de mise à l’échelle automatique (mise à l’échelle supérieure)** |**Règle de mise à l’échelle automatique (mise à l’échelle supérieure)** |
| **Ressource :** Production (environnement App Service) |**Ressource :** Production (environnement App Service) |
| **Mesure :** % d’utilisation de l’unité centrale |**Mesure :** % d’utilisation de l’unité centrale |
| **Fonctionnement :** supérieur à 60 % |**Fonctionnement :** supérieur à 80 % |
| **Durée :** 5 minutes |**Durée :** 10 minutes |
| **Agrégation de temps :** moyenne |**Agrégation de temps :** moyenne |
| **Action :** augmenter le nombre de 2 |**Action :** augmenter le nombre de 1 |
| **Refroidissement (minutes) :** 15 |**Refroidissement (minutes) :** 20 |
|  | |
| **Règle de mise à l’échelle automatique (mise à l’échelle inférieure)** |**Règle de mise à l’échelle automatique (mise à l’échelle inférieure)** |
| **Ressource :** Production (environnement App Service) |**Ressource :** Production (environnement App Service) |
| **Mesure :** % d’utilisation de l’unité centrale |**Mesure :** % d’utilisation de l’unité centrale |
| **Fonctionnement :** inférieur à 30 % |**Fonctionnement :** inférieur à 20 % |
| **Durée :** 10 minutes |**Durée :** 15 minutes |
| **Agrégation de temps :** moyenne |**Agrégation de temps :** moyenne |
| **Action :** diminuer le nombre de 1 |**Action :** diminuer le nombre de 1 |
| **Refroidissement (minutes) :** 20 |**Refroidissement (minutes) :** 10 |

### <a name="app-service-plan-inflation-rate"></a>Taux d’inflation du plan App Service
Les plans App Service qui sont configuré tooautoscale le faire à un taux maximum par heure. Ce taux peut être calculé en fonction des valeurs hello fournis sur la règle de mise à l’échelle hello.

Présentation et de calcul hello *taux de gonflage du plan App Service* est important pour l’échelle d’environnement du Service d’applications, car le pool de travail de mise à l’échelle modifications tooa ne sont pas instantanées.

Hello taux de gonflage du plan App Service est calculé comme suit :

![Calcul du taux d’inflation du plan App Service.][ASP-Inflation]

En fonction de hello échelle – règle de mise à l’échelle pour le profil du jour de la semaine hello de production de hello plan App Service :

![Taux d’inflation du plan App Service pour les jours de la semaine selon la règle Mise à l’échelle automatique – Mise à l’échelle supérieure.][Equation1]

Dans les cas de hello Hello échelle – règle de mise à l’échelle pour le profil de week-end hello de production de hello plan App Service, la formule de hello se résoudra en :

![Taux d’inflation du plan App Service pour les week-ends selon la règle Mise à l’échelle automatique – Mise à l’échelle supérieure.][Equation2]

Cette valeur peut également être calculée pour les opérations de réduction.

En fonction de hello échelle – mise à l’échelle vers le bas la règle pour le profil du jour de la semaine hello de production de hello plan App Service, il se présente comme suit :

![Taux d’inflation du plan App Service pour les jours de la semaine selon la règle Mise à l’échelle automatique – Mise à l’échelle inférieure.][Equation3]

Dans les cas de hello Hello échelle – règle de mise à l’échelle vers le bas pour le profil de week-end hello de production de hello plan App Service, la formule de hello se résoudra en :  

![Taux d’inflation du plan App Service pour les week-ends selon la règle Mise à l’échelle automatique – Mise à l’échelle inférieure.][Equation4]

production de Hello plan App Service peut atteindre un taux maximum de huit heures instances semaine hello et quatre instances/heure week-end hello. Il peut diffuser des instances à un taux maximum de quatre instances/heure au cours de la semaine de hello et six instances/heure pendant le week-end.

Si plusieurs plans App Service sont hébergés dans un pool de travail, vous avez toocalculate hello *taux total de complications* en tant que somme hello du taux de complications hello pour hello tous les plans de Service de l’application et qui sont en cours d’hébergement dans ce pool de travail.

![Calcul du taux d’inflation total pour plusieurs plans App Service hébergés dans un pool de workers.][ASP-Total-Inflation]

### <a name="use-hello-app-service-plan-inflation-rate-toodefine-worker-pool-autoscale-rules"></a>Hello d’utilisation du Service d’applications planifier les règles de mise à l’échelle de taux de complications toodefine worker pool
Travail qui hébergent les plans App Service qui sont configuré tooautoscale doivent être affectée à une mémoire tampon de la capacité des pools. mémoire tampon de Hello permet hello échelle opérations toogrow et réduire le plan App Service en fonction des besoins. mémoire tampon minimale de Hello serait hello calculé Total App Service planifier la fréquence de complications.

Étant donné que les opérations d’échelle environnement App Service prennent certaines tooapply de temps, toute modification doit prendre en compte plus les modifications à la demande qui peut se produire pendant une opération de mise à l’échelle est en cours d’exécution. tooaccommodate cette latence, nous vous recommandons d’utiliser hello calculé Total App Service planifier la fréquence de complications comme nombre minimal de hello d’instances qui sont ajoutés pour chaque opération de mise à l’échelle.

Avec cette information, Frank peut définir hello suivant le profil de mise à l’échelle et de règles :

![Règles de profil de mise à l’échelle automatique pour un exemple d’application métier.][Worker-Pool-Scale]

| **Profil de mise à l’échelle automatique – Jours de la semaine** | **Profil de mise à l’échelle automatique – Week-ends** |
| --- | --- |
| **Nom :** profil jour de semaine |**Nom :** profil week-end |
| **Mise à l’échelle selon :** Planification et règles de performances |**Mise à l’échelle selon :** Planification et règles de performances |
| **Profil :** jours de la semaine |**Profil :** week-end |
| **Type :** périodicité |**Type :** périodicité |
| **Target plage :** 13 too25 instances |**Target plage :** 6 instances too15 |
| **Jours :** lundi, mardi, mercredi, jeudi, vendredi |**Jours :** samedi, dimanche |
| **Heure de début :** 7 h |**Heure de début :** 9 h |
| **Fuseau horaire :** UTC-08 |**Fuseau horaire :** UTC-08 |
|  | |
| **Règle de mise à l’échelle automatique (mise à l’échelle supérieure)** |**Règle de mise à l’échelle automatique (mise à l’échelle supérieure)** |
| **Ressource :** pool de Workers 1 |**Ressource :** pool de Workers 1 |
| **Mesure :** Employés disponibles |**Mesure :** Employés disponibles |
| **Fonctionnement :** inférieur à 8 |**Fonctionnement :** inférieur à 3 |
| **Durée :** 20 minutes |**Durée :** 30 minutes |
| **Agrégation de temps :** moyenne |**Agrégation de temps :** moyenne |
| **Action :** augmenter le nombre de 8 |**Action :** augmenter le nombre de 3 |
| **Refroidissement (minutes) :** 180 |**Refroidissement (minutes) :** 180 |
|  | |
| **Règle de mise à l’échelle automatique (mise à l’échelle inférieure)** |**Règle de mise à l’échelle automatique (mise à l’échelle inférieure)** |
| **Ressource :** pool de Workers 1 |**Ressource :** pool de Workers 1 |
| **Mesure :** Employés disponibles |**Mesure :** Employés disponibles |
| **Fonctionnement :** supérieur à 8 |**Fonctionnement :** supérieur à 3 |
| **Durée :** 20 minutes |**Durée :** 15 minutes |
| **Agrégation de temps :** moyenne |**Agrégation de temps :** moyenne |
| **Action :** diminuer le nombre de 2 |**Action :** diminuer le nombre de 3 |
| **Refroidissement (minutes) :** 120 |**Refroidissement (minutes) :** 120 |

Hello plage cible défini dans le profil de hello est calculée par les instances minimale hello définis dans le profil pour hello plan App Service + la mémoire tampon.

plage de Maximum Hello serait somme hello de toutes les plages maximale hello pour tous les plans de Service de l’application hébergées dans le pool de travail hello.

Hello nombre augmentation d’échelle hello des règles doit être tooat ensemble au moins 1 X le taux de complications App Service Plan pour l’échelle haut.

Nombre de diminution peut être ajustée toosomething entre le 1/2 X ou 1 X hello taux de complications Plan App Service de mise à l’échelle vers le bas.

### <a name="autoscale-for-front-end-pool"></a>Mise à l’échelle automatique du pool frontend
Les règles de mise à l’échelle automatique des frontends sont plus simples que pour les pools de workers. Le plus important est de  
Vérifiez que la durée de mesure de hello et les minuteurs de ralentissement hello que les opérations de mise à l’échelle sur un plan App Service ne sont pas instantanées.

Pour ce scénario, Frank sait ce taux d’erreur hello augmente après que frontaux atteint 80 % d’utilisation du processeur et définit des instances de règle tooincrease hello échelle comme suit :

![Paramètres de mise à l’échelle automatique du pool frontend.][Front-End-Scale]

| **Profil de l’échelle automatique : serveurs frontaux** |
| --- |
| **Nom :** Mise à l’échelle automatique – Frontends |
| **Mise à l’échelle selon :** Planification et règles de performances |
| **Profil :** tous les jours |
| **Type :** périodicité |
| **Target plage :** 3 instances too10 |
| **Jours :** tous les jours |
| **Heure de début :** 9 h |
| **Fuseau horaire :** UTC-08 |
|  |
| **Règle de mise à l’échelle automatique (mise à l’échelle supérieure)** |
| **Ressource :** Pool frontal |
| **Mesure :** % d’utilisation de l’unité centrale |
| **Fonctionnement :** supérieur à 60 % |
| **Durée :** 20 minutes |
| **Agrégation de temps :** moyenne |
| **Action :** augmenter le nombre de 3 |
| **Refroidissement (minutes) :** 120 |
|  |
| **Règle de mise à l’échelle automatique (mise à l’échelle inférieure)** |
| **Ressource :** pool de Workers 1 |
| **Mesure :** % d’utilisation de l’unité centrale |
| **Fonctionnement :** inférieur à 30 % |
| **Durée :** 20 minutes |
| **Agrégation de temps :** moyenne |
| **Action :** diminuer le nombre de 3 |
| **Refroidissement (minutes) :** 120 |

<!-- IMAGES -->
[intro]: ./media/app-service-environment-auto-scale/introduction.png
[settings-scale]: ./media/app-service-environment-auto-scale/settings-scale.png
[scale-manual]: ./media/app-service-environment-auto-scale/scale-manual.png
[scale-profile]: ./media/app-service-environment-auto-scale/scale-profile.png
[scale-profile2]: ./media/app-service-environment-auto-scale/scale-profile-2.png
[scale-rule]: ./media/app-service-environment-auto-scale/scale-rule.png
[asp-scale]: ./media/app-service-environment-auto-scale/asp-scale.png
[ASP-Inflation]: ./media/app-service-environment-auto-scale/asp-inflation-rate.png
[Equation1]: ./media/app-service-environment-auto-scale/equation1.png
[Equation2]: ./media/app-service-environment-auto-scale/equation2.png
[Equation3]: ./media/app-service-environment-auto-scale/equation3.png
[Equation4]: ./media/app-service-environment-auto-scale/equation4.png
[ASP-Total-Inflation]: ./media/app-service-environment-auto-scale/asp-total-inflation-rate.png
[Worker-Pool-Scale]: ./media/app-service-environment-auto-scale/wp-scale.png
[Front-End-Scale]: ./media/app-service-environment-auto-scale/fe-scale.png
