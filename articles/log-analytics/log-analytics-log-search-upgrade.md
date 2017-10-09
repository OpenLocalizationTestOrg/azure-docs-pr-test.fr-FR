---
title: recherche de journal toonew aaaUpgrading Analytique de journal Azure | Documents Microsoft
description: "nouveau langage de requête Analytique de journal Hello est presque ici, et vous pouvez participer en version préliminaire publique de hello.  Cet article décrit les avantages de hello du nouveau langage de hello et comment tooconvert votre espace de travail."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 7659c9d1467cab79d3a16e73b52b507ed281b002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-azure-log-analytics-workspace-toonew-log-search"></a>Mise à niveau de votre recherche de journal toonew espace de travail Analytique des journaux Azure

> [!NOTE]
> Mise à niveau toohello nouveau langage de requête Analytique de journal est actuellement facultatif du temps trop[rampe sur le nouveau langage de hello](https://go.microsoft.com/fwlink/?linkid=856078).  

nouveau langage de requête Analytique de journal Hello est ici, et vous devez tooupgrade votre espace de travail tootake tirer parti.  Cet article décrit les avantages de hello du nouveau langage de hello et comment tooconvert votre espace de travail.  Si vous ne choisissez pas tooupgrade maintenant, votre espace de travail continue toooperate comme il a toujours, mais il sera automatiquement converti à une date ultérieure.  Vous serez averti bien à l’avance de cette conversion.

Cet article fournit des détails sur le nouveau langage de hello et mise à niveau de hello.

## <a name="why-hello-new-language"></a>Pourquoi hello nouvelle langue ?
Nous sommes conscients qu’il existe des difficultés dans toute transition, et que nous ne changez simplement le langage de requête hello fun hello de celui-ci.  Il existe plusieurs raisons cette modification fournir une valeur ajoutée significative aux clients de tooour Analytique de journal.

- **Simple, mais puissant.** nouveau langage de Hello est toounderstand plus facile et tooSQL similaire avec des constructions plus comme un langage naturel celle hello hérité.
- **Des fonctionnalités de redirection complètes.**  nouveau langage de Hello a des fonctions tuyauterie plus étendues que le langage de hérité hello.  N’importe quel de sortie peut être dirigée tooanother commande toocreate des requêtes plus complexes qu’étaient précédemment disponibles.
- **Extraction des champs au moment de la recherche.**  nouveau langage de Hello prend en charge des champs de runtime calculée plus avancées que le langage de hérité hello.  Vous pouvez utiliser des calculs complexes pour les champs étendus et utilisez les champs de hello calculée pour les commandes supplémentaires, y compris les jointures et agrégations.
- **Jointures avancées.**  nouveau langage de Hello fournit des jointures plus avancées que le langage de hérité hello y compris les tables de toojoin possibilité hello sur plusieurs champs, utilisez des jointures internes et externes et joindre sur les champs étendus.
- **Fonctions de date et d’heure.**  nouveau langage de Hello d’autres avancées des fonctions de date/heure que le langage de hérité hello.
- **Analyses intelligentes.**  nouveau langage de Hello dispose de modèles de tooevaluate algorithmes dans les jeux de données et de comparer différents jeux de données avancés.
- **Portail Analytique avancée.**  portail d’Analytique avancée Hello offre des fonctionnalités d’analyse non disponibles dans le portail d’Analytique de journal hello notamment multiligne modification des requêtes, des visualisations supplémentaires et des diagnostics avancés.
- **Cohérence avec les autres applications.**  Bonjour nouveau langage et hello Portal d’Analytique avancée sont déjà utilisés pour analytique dans Application Insights.  L’implémentation du nouveau langage pour Log Analytics permet une cohérence entre les services Azure.
- **Meilleure intégration avec Power BI.** Requêtes dans un nouveau langage de hello peuvent être exporté tooPower BI Desktop, vous pouvez utiliser ses fonctionnalités de transformation de données enrichies.
- **Et bien plus encore...** Consultez toohello [langage de requête Analytique Azure journal](https://docs.loganalytics.io) site pour obtenir des informations détaillées et des didacticiels sur le nouveau langage de hello.


## <a name="when-can-i-upgrade"></a>À quel moment puis-je effectuer la mise à niveau ?
mise à niveau Hello est déployée dans toutes les régions Azure elle peut être disponible dans certaines régions avant les autres.  Vous savez quand votre espace de travail est disponible toobe mis à niveau lorsque vous consultez la bannière de hello violet haut hello de votre espace de travail vous invite tooupgrade.

![Mise à niveau 1](media/log-analytics-log-search-upgrade/upgrade-01a.png)

## <a name="what-happens-when-i-upgrade"></a>Que se passe-t-il quand j’effectue la mise à niveau ?
Lorsque vous convertissez votre espace de travail, toutes les recherches enregistrées, les règles d’alerte et les vues que vous avez créée avec hello Concepteur de vue sont automatiquement convertis toohello nouveau langage.  Inclus dans les solutions de recherche n’est pas convertis automatiquement, mais ils sont convertis au lieu de cela volée hello lorsque vous les ouvrez.  Il s’agit de tooyou totalement transparente.

## <a name="can-i-go-back-after-i-upgrade"></a>Puis-je annuler la mise à niveau ?
Lorsque vous effectuez la mise à niveau, une sauvegarde complète de votre espace de travail est créée. La sauvegarde est constituée de la capture instantanée de toutes vos recherches enregistrées, de vos règles d’alerte et de vos vues.  Cela vous permet de toorestore votre ancien espace de travail si vous le souhaitez devez ultérieurement.

toorestore votre espace de travail hérité, accédez trop**paramètres** dans votre espace de travail, puis **résumé de mise à niveau**.  Vous pouvez ensuite sélectionner les option hello trop**restaurer l’espace de travail hérité**.  

![Restaurer l’espace de travail hérité](media/log-analytics-log-search-upgrade/restore-legacy-b.png)

## <a name="how-do-i-perform-hello-upgrade"></a>Comment effectuer la mise à niveau hello ?
Vous pouvez mettre à niveau votre espace de travail lorsque vous consultez bannière hello violet haut hello du portail de hello.  

1.  Démarrer le processus de mise à niveau de hello en cliquant sur la bannière hello violet indiquant **en savoir plus et mettre à niveau**.<br>![Mise à niveau 2](media/log-analytics-log-search-upgrade/upgrade-01a.png)<br>
2.  Lisez hello plus d’informations sur la mise à niveau hello sur la page des informations de mise à niveau hello.<br>![Mise à niveau 2](media/log-analytics-log-search-upgrade/upgrade-03.png)<br>
3.  Cliquez sur **mettre à niveau maintenant** mise à niveau de toostart hello.<br>![Mettre à niveau 4](media/log-analytics-log-search-upgrade/upgrade-04.png)<br>Une zone de notification dans le coin supérieur droit de hello affiche l’état de hello.<br>![Mettre à niveau 5](media/log-analytics-log-search-upgrade/upgrade-05.png)
4.  Et voilà !  Passez en revue toohave de page de recherche de journal toohello examiner votre espace de travail mis à niveau.<br>![Mise à jour 6](media/log-analytics-log-search-upgrade/upgrade-06.png)<br>

Si vous rencontrez un problème qui provoque le toofail de mise à niveau de hello, vous pouvez accéder toohello [forum de discussion](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) et publiez votre question ou [créer une demande de support](../azure-supportability/how-to-create-azure-support-request.md) de hello portail Azure.

## <a name="how-do-i-learn-hello-new-language"></a>Comment savoir le nouveau langage de hello ?
Dans la mesure où il est utilisé par plusieurs services, nous avons créé un [documentation du site externe toohost hello](https://docs.loganalytics.io/) pour le nouveau langage de hello.  Cela inclut des didacticiels, des exemples et un toohelp de référence complète que vous pensez toospeed. Vous pouvez parcourir un didacticiel de nouveau langage de hello à [mise en route avec les requêtes](https://go.microsoft.com/fwlink/?linkid=856078) et accéder à la référence du langage hello à [langue de requête Analytique de journal](https://go.microsoft.com/fwlink/?linkid=856079).  

Si vous êtes déjà familiarisé avec hello hérité Analytique de journal de langage de requête Cependant, vous pouvez ensuite utiliser convertisseur de langage hello qui est ajouté tooyour espace de travail dans le cadre de la mise à niveau hello.

Tapez simplement dans votre requête hérité, puis **convertir** toosee hello traduction.  Vous pouvez ensuite cliquez hello bouton toorun hello recherche ou copier et coller toouse de requête hello converti vers un autre emplacement comme une règle d’alerte.

![Convertisseur de langage](media/log-analytics-log-search-upgrade/language-converter.png)


## <a name="next-steps"></a>Étapes suivantes
- Extraire un [didacticiel sur le nouveau langage de hello](https://go.microsoft.com/fwlink/?linkid=856078).
- Parcourir un [didacticiel sur l’utilisation du portail de recherche de journal hello](log-analytics-log-search-log-search-portal.md) avec un nouveau langage de requête hello.
- Obtenir une présentation toohello nouvelle [portal d’Analytique de Advanced](https://go.microsoft.com/fwlink/?linkid=856587).
