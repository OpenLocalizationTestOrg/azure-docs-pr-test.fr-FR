---
title: aaaPlanning pour la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources | Documents Microsoft
description: Planification de la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 78492a2c-2694-4023-a7b8-c97d3708dcb7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/01/2017
ms.author: kasing
ms.openlocfilehash: 53c6f640425b69cae2ef10afb8c92b8ac4394267
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="planning-for-migration-of-iaas-resources-from-classic-tooazure-resource-manager"></a>Planification de la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources
Alors que Azure Resource Manager offre un grand nombre de fonctionnalités, il est critique tooplan out votre toomake de parcours de migration que choses effectueront. Il est nécessaire de consacrer du temps à la planification pour être sûr de ne pas rencontrer de problèmes lors de l’exécution des activités de migration. 

> [!NOTE] 
> Hello suivant instructions a été équipe Azure Customer Advisory de tooby fortement contribué hello et les architectes de solutions de Cloud travaillant avec des clients sur la migration enviornments volumineux. Par conséquent, ce document continuera tooget mis à jour lorsque de nouveaux modèles de la réussite de l’émergence, alors vérifiez de temps tootime toosee s’il existe de nouvelles recommandations.

Il existe quatre phases générales de parcours de migration hello :

![Phases de migration](../media/virtual-machines-windows-migration-classic-resource-manager/plan-labtest-migrate-beyond.png)

## <a name="plan"></a>Planification

### <a name="technical-considerations-and-tradeoffs"></a>Considérations et concessions techniques

Selon votre taille de spécifications techniques, les zones géographiques différentes et les pratiques opérationnelles, vous pouvez envisager de tooconsider :

1. Pourquoi votre organisation souhaite-t-elle passer à Azure Resource Manager ?  Quelles sont les raisons professionnelles de hello pour une migration ?
2. Quelles sont les raisons techniques de hello pour le Gestionnaire de ressources Azure ?  Quel (le cas échéant) des services Azure supplémentaires voulez-vous tooleverage ?
3. Quelle application (ou ensembles d’ordinateurs virtuels) sont inclus dans la migration hello ?
4. Les scénarios sont pris en charge la migration hello API ?  Hello de révision [non pris en charge des fonctionnalités et configurations](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#unsupported-features-and-configurations).
5. Vos équipes opérationnelles prennent-elles maintenant en charge les applications/machines virtuelles dans les modes Classic et Azure Resource Manager ?
6. En quoi Azure Resource Manager modifie-t-il les processus de déploiement, de gestion, de surveillance et de création de rapports concernant vos machines virtuelles ?  Vos scripts de déploiement doivent-elles toobe mis à jour ?
7. Nouveautés pour les communications hello planifier les parties prenantes tooalert (les utilisateurs finaux, les propriétaires de l’application et propriétaires d’infrastructure) ?
8. Selon la complexité hello d’environnement de hello, il convient une période de maintenance où application hello est indisponible tooend utilisateurs et les propriétaires de tooapplication ?  Si oui, pendant combien de temps ?
9. Nouveautés des parties prenantes tooensure du plan de formation hello sont bien informé et expert dans le Gestionnaire de ressources Azure ?
10. Quelle est la gestion des programmes hello ou plan de gestion de projet pour la migration de hello ?
11. Quelles sont les chronologies hello pour la migration d’Azure Resource Manager hello et d’autres liées technologie route mappages ?  Sont-elles parfaitement coordonnées ?

### <a name="patterns-of-success"></a>Modèles de réussite

Clients satisfaits ont détaillé les plans où hello ci-dessus sont présentés, documenté et régie.  Vérifier les plans de migration hello toosponsors largement communiquée et les parties prenantes.  Informez-vous sur les options de migration à votre disposition ; il est fortement recommandé de lire cet ensemble de documents sur la migration.

* [Vue d’ensemble de la plateforme prise en charge la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Techniques détaillées sur la plateforme prise en charge la migration à partir de tooAzure classique Gestionnaire de ressources](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Planification de la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Utiliser les ressources IaaS PowerShell toomigrate classique tooAzure Gestionnaire de ressources](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Utiliser les ressources IaaS CLI toomigrate classique tooAzure Gestionnaire de ressources](migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Outils de communauté qui contribuent à la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Passer en revue les erreurs courantes de migration](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Hello de révision plus Forum aux questions sur la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="pitfalls-tooavoid"></a>Pièges tooavoid

- Échec tooplan.  étapes de la technologie Hello de cette migration éprouvées et résultat de hello est prévisible.
- L’hypothèse selon laquelle hello plateforme prise en charge les API de migration en compte pour tous les scénarios. Hello de lecture [non pris en charge des fonctionnalités et configurations](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#unsupported-features-and-configurations) toounderstand quels scénarios sont pris en charge.
- Absence de planification d’une interruption potentielle de l’application pour les utilisateurs finaux.  Planifier la mémoire tampon insuffisante tooadequately avertir les utilisateurs finaux de temps d’application potentiellement non disponible.


## <a name="lab-test"></a>Test en labo 

**Répliquer un environnement et effectuer un test de migration**
  > [!NOTE]
  > La réplication à l’exact de l’environnement existant est réalisée à l’aide d’un outil développé par la communauté, qui n’est pas pris en charge officiellement par le Support Microsoft. Par conséquent, il est un **facultatif** étape, mais il est hello meilleure manière toofind problèmes sans toucher vos environnements de production. Si à l’aide d’un outil conçu par la Communauté n’est pas une option, puis lire sur hello recommandation de validation/préparation/Abort sec exécuter ci-dessous.
  >
  
  Un laboratoire de test de votre scénario (calcul, de mise en réseau et stockage) est hello meilleure manière tooensure une migration en douceur. afin de garantir :

  - Un laboratoire totalement distinct ou un tootest hors environnement de production existant. Nous recommandons un laboratoire totalement distinct qui peut faire l’objet de plusieurs migrations et de modifications destructrices.  Les métadonnées de toocollect/hydrate de scripts à partir d’abonnements réel de hello sont répertoriées ci-dessous.
  - Il s’agit d’un laboratoire de hello toocreate conseillé dans un abonnement distinct. Hello raison est que lab de hello sera détruit à plusieurs reprises, et avoir un distinct, abonnement isolé réduit hello probabilité que quelque chose de réel est accidentellement supprimé.

  Cela peut être accompli en utilisant l’outil de AsmMetadataParser hello. [En savoir plus sur cet outil](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

### <a name="patterns-of-success"></a>Modèles de réussite

suivant de Hello ont été problèmes découverts dans la plupart des migrations de plus grandes hello. Cela n’est pas une liste exhaustive, consultez toohello [non pris en charge des fonctionnalités et configurations](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#unsupported-features-and-configurations) pour plus de détails. Il n’est pas certain que vous rencontriez ces problèmes techniques ; si c’est le cas, vous garantirez une meilleure expérience en résolvant ces points avant de tenter la migration.

- **Faites un essai Validate/Prepare/Abort** -il s’agit peut-être de hello plus importante étape tooensure classique tooAzure Gestionnaire de ressources du succès de la migration. migration de Hello API comporte trois étapes principales : valider, la préparation et la validation. Valider va lire l’état hello de votre environnement classique et retourner un résultat de tous les problèmes. Toutefois, étant donné que certains problèmes peuvent exister dans la pile du Gestionnaire de ressources Azure hello, valider n’intercepte pas tous les éléments. étape suivante de Hello dans le processus de migration, préparer aidera à exposer ces problèmes. Préparer va déplacer hello des métadonnées à partir de classique tooAzure Gestionnaire de ressources, mais ne sera pas de validation hello déplacement et sera pas supprimer ou apporter des modifications à côté de classique de hello. Hello sec implique la préparation de la migration de hello, puis abandon (**n’est ne pas validé**) préparer la migration de hello. Hello valider/préparer/abort sec exécuter vise toosee toutes les métadonnées hello dans la pile du Gestionnaire de ressources Azure hello, de l’examiner (*par programmation ou dans le portail*) et vérifiez que tous les éléments migre correctement et par le biais de travail problèmes techniques.  Il donne également une idée de la durée de la migration de façon à permettre de planifier un temps d’arrêt adapté.  Une validation/préparer/abort ne provoque pas de tout temps d’arrêt de l’utilisateur ; Par conséquent, il est l’utilisation de tooapplication sans interruption de service.
  - éléments Hello ci-dessous doivent toobe résolu avant l’exécution de sec hello, mais un test d’essai effacera également en toute sécurité ces étapes de préparation si elles sont ignorées par. Pendant la migration de l’entreprise, nous avons trouvé hello essai toobe une préparation à la migration tooensure moyen sûr et précieux.
  - Préparer lorsque est en cours d’exécution, contrôle de hello plan (opérations de gestion Azure) est verrouillé pour hello tout réseau virtuel, et donc aucune peuvent être modifiées tooVM métadonnées pendant la validation/préparer/abort.  Par ailleurs, aucune fonction de l’application (bureau à distance, utilisation de la machine virtuelle, etc.) ne sera affectée.  Les utilisateurs d’ordinateurs virtuels de hello ne saura pas que qui s’exécutent sec de hello est en cours d’exécution.

- **Circuits ExpressRoute et VPN**. Actuellement, il n’est pas possible de migrer les passerelles ExpressRoute avec liens d’autorisation sans temps mort. Pour résoudre ce problème de hello, consultez [ExpressRoute de migrer des circuits et associé des réseaux virtuels à partir du modèle de déploiement du Gestionnaire de ressources hello classique toohello](../../expressroute/expressroute-migration-classic-resource-manager.md).

- **Extensions de machine virtuelle** -extensions de Machine virtuelle sont potentiellement un des plus grand toomigrating obstacles éventuels hello, machines virtuelles en cours d’exécution. La correction des extensions de machines virtuelles peut prendre plus d’un ou deux jours : adaptez votre planification en conséquence.  Une travail de l’agent Azure est nécessaire tooreport état Extension de machine virtuelle de l’exécution de machines virtuelles. Si l’état de hello reviennent en tant qu’incorrect pour une machine virtuelle en cours d’exécution, il s’arrêtera la migration. agent Hello lui-même ne pas besoin toobe de migration de tooenable marche, mais s’il existent des extensions sur hello machine virtuelle, puis à la fois un agent de travail et une connectivité internet sortante (avec DNS) est nécessaires pour toomove de migration vers l’avant.
  - Si le serveur DNS de tooa connectivité est perdue pendant la migration, toutes les Extensions de machine virtuelle à l’exception BGInfo v1. \* devez toofirst supprimées de chaque machine virtuelle avant de préparer la migration et toohello précédent par la suite rajouté machine virtuelle après la migration d’Azure Resource Manager.  **Cela concerne uniquement les machines virtuelles en cours d’exécution.**  Si hello machines virtuelles est arrêtée désallouée, les Extensions de machine virtuelle n’avez pas besoin de toobe supprimé. **Remarque :** de nombreuses extensions, par exemple les diagnostics Azure et le contrôle de Security Center, se réinstallent après la migration ; les supprimer n’est donc pas un problème.
  - Par ailleurs, assurez-vous que les groupes de sécurité réseau ne restreignent pas l’accès à Internet sortant. Cela peut se produire avec certaines configurations de groupes de sécurité réseau. Un accès internet sortant (et DNS) est nécessaire pour les Extensions de machine virtuelle toobe migré tooAzure Gestionnaire de ressources. 
  - Il existe deux versions de hello extension BGInfo : v1 et v2.  Hello machine virtuelle a été créé à l’aide du portail classique de hello ou PowerShell, hello VM aura probablement extension v1 de hello sur celui-ci. Cette extension n’a pas besoin toobe supprimée et sera ignorée (ne pas migré) par la migration de hello API. Toutefois, si hello classique de machine virtuelle a été créé avec le nouveau portail de Azure hello, il aura version hello v2 de JSON en fonction de BGInfo, ce qui peut être migrée tooAzure Gestionnaire de ressources fourni l’agent de hello fonctionne et a un accès internet sortant (et DNS). 
  - **Option de correction 1**. Si vous savez que vos machines virtuelles n’aura pas internet sortant, accéder à un service DNS de travail et vous utilisez Azure agents sur des machines virtuelles de hello, puis désinstallez toutes les extensions de machine virtuelle dans le cadre de la migration de hello avant de préparer, puis réinstallez les Extensions de machine virtuelle hello après la migration. 
  - **Option de correction 2**. Si les extensions de machine virtuelle sont trop volumineuses d’un obstacle, une autre option consiste à tooshutdown/libérer tous les ordinateurs virtuels avant la migration. Migrer hello désalloué des machines virtuelles, puis les redémarrer sur hello Azure Resource Manager côté. Hello avantage est que les extensions de machine virtuelle seront migrer. Hello inconvénient est que tous les public faisant face à des adresses IP virtuelles seront perdues (Cela peut être un starter-non), et évidemment hello machines virtuelles s’arrête à l’origine d’un impact beaucoup plus important sur les applications de travail.

    > [!NOTE] 
    > Si une stratégie de centre de sécurité Azure est configurée sur hello en cours de migration de machines virtuelles en cours d’exécution, la stratégie de sécurité hello doit toobe arrêté avant de supprimer des extensions, sinon sécurité hello extension de surveillance sera automatiquement réinstallée sur hello machine virtuelle après supprimez.

- **Haute disponibilité** - pour un réseau virtuel (vNet) de toobe migré tooAzure Gestionnaire de ressources, hello machines virtuelles de déploiement (par exemple, le service cloud) contenu standard doit être dans un ensemble de disponibilité ou hello machines virtuelles ne doit pas tous être dans n’importe quel jeu de disponibilité. Plus d’une haute disponibilité dans le service cloud hello n’est pas compatible avec le Gestionnaire de ressources Azure et va s’interrompre la migration.  En outre, il ne peut pas y avoir des machines virtuelles dans un groupe à haute disponibilité et d’autres ailleurs que dans un groupe à haute disponibilité. tooresolve, vous devez tooremediate ou remanier votre service cloud.  Adaptez votre planification en conséquence, car cette opération peut prendre du temps. 

- **Déploiements de rôle Web/de travail** -Services de cloud computing contenant les rôles web et de travail ne peut pas migrer tooAzure Gestionnaire de ressources. les rôles web/de travail Hello doivent tout d’abord supprimer du réseau virtuel de hello avant de démarrer la migration.  Une solution classique est toojust déplacement web/de travail rôle instances tooa classique réseau virtuel distinct qui est également lié tooan ExpressRoute circuit ou toomigrate hello code toonewer application Services PaaS (cette discussion est abordée dans ce document hello). Dans ancien de hello redéployer le cas, créez un réseau virtuel classique, déplacement/redéployer hello web/de travail rôles toothat nouveau réseau virtuel, puis supprimer les déploiements hello à partir du réseau virtuel de hello en cours de déplacement. Aucune modification de code requise : Hello nouvelle [d’homologation de réseau virtuel](../../virtual-network/virtual-network-peering-overview.md) capacité peut être utilisé toopeer hello ensemble classique réseaux contenant les rôles web/de travail hello et d’autres réseaux virtuels dans hello même région Azure, par exemple, hello réseau virtuel migration (**après la migration du réseau virtuel comme ressources des réseaux virtuels ne peuvent pas être migrés**), assurant ainsi une hello mêmes fonctionnalités avec aucune perte de performance et sans aucune pénalité de latence et bande passante. Ajout de hello des [d’homologation de réseau virtuel](../../virtual-network/virtual-network-peering-overview.md), les déploiements de rôle web/de travail peut désormais facilement être atténuées et ne pas bloquer hello migration tooAzure Gestionnaire de ressources.

- **Quotas d’Azure Resource Manager** : les régions Azure disposent de quotas/limites distincts pour Classic et Azure Resource Manager. Bien que dans un scénario de migration de nouveau matériel n’est pas consommée *(nous allons le remplacement des machines virtuelles existantes à partir de classique tooAzure Gestionnaire de ressources)*, les quotas Azure Resource Manager doivent encore toobe en place avec une capacité suffisante avant la migration peut démarrer. Vous trouverez ci-dessous les limites principales hello que nous l’avons vu causer des problèmes.  Ouvrez un Bonjour tooraise de quota prise en charge de ticket limite. 

    > [!NOTE]
    > Ces limites doivent toobe déclenché dans hello même région lors de la migration de votre toobe environnement actuel.
    >

    - Interfaces réseau
    - Équilibreurs de charge
    - Adresses IP publiques
    - Adresses IP publiques statiques
    - Cœurs
    - Groupes de sécurité réseau
    - Tables de routage

    Vous pouvez vérifier vos quotas Azure Resource Manager en cours à l’aide de hello suivant de commandes avec la version la plus récente de Azure CLI 2.0 hello.

    **Calcul***(cœurs, groupes à haute disponibilité)*

    ```bash
    az vm list-usage -l <azure-region> -o jsonc 
    ```

    **Réseau***(réseaux virtuels, adresses IP publiques statiques, adresses IP publiques, groupes de sécurité réseau, interfaces réseau, équilibreurs de charge, tables de routage)*
    
    ```bash
    az network list-usages -l <azure-region> -o jsonc
    ```

    **Stockage***(compte de stockage)*
    
    ```bash
    az storage account show-usage
    ```

- **Limitations de l’API Azure Resource Manager** : si vous avez un environnement de grande taille (par exemple, > 400 machines virtuelles dans un réseau virtuel), vous pourrez atteindre API par défaut de hello limites pour les écritures (actuellement **1200 écritures/heure**) dans le Gestionnaire de ressources Azure. Avant de commencer la migration, vous devez déclencher un tooincrease de ticket de support à cette limite pour votre abonnement.

- **Configuration d’état a expiré à la machine virtuelle** - si toutes les machines virtuelles a l’état hello **de configuration a expiré**, cette besoins toobe résolus avant la migration. Hello seule façon toodo il s’agit avec un temps mort par la mise hors service/la préparation hello VM (delete, conservez hello disque et les recréer hello machine virtuelle). 

- **État de machine virtuelle RoleStateUnknown** - si la migration s’arrête en raison tooa **état du rôle inconnu** erreur message, d’inspecter hello machine virtuelle à l’aide du portail de hello et assurez-vous qu’il est en cours d’exécution. Cette erreur disparaîtra normalement toute seule (aucune correction n’est requise) après quelques minutes ; souvent de type temporaire, elle est généralement constatée au cours des opérations **start**, **stop**, **restart** de machine virtuelle. **Pratique recommandée :** effectuez une nouvelle tentative de migration après quelques minutes. 

- **La structure du cluster n’existe pas** : il arrive qu’il ne soit pas possible de migrer une machine virtuelle pour d’obscures raisons. Un de ces cas connus est hello machine virtuelle a été créé récemment (dans hello la semaine dernière ou ainsi) et est devenu tooland un cluster Azure qui n’est pas encore équipé pour les charges de travail Azure Resource Manager.  Vous obtiendrez une erreur indiquant que **cluster fabric n’existe pas** et hello machine virtuelle ne peut pas être migrée. En attente de quelques jours sera généralement résoudre ce problème particulier comme cluster de hello sera bientôt Azure Resource Manager est activé. Toutefois, une solution de contournement immédiate est trop`stop-deallocate` hello de machine virtuelle, puis continuer avec la migration et de démarrer hello VM sauvegarder dans Azure Resource Manager après la migration.

### <a name="pitfalls-tooavoid"></a>Pièges tooavoid

- Ne pas prendre des raccourcis et omettre les migrations de valider/préparer/abort sec exécuter hello.
- La plupart, voire la totalité, des problèmes potentiels de votre affichera au cours des étapes de validation/préparer/abort hello.

## <a name="migration"></a>Migration

### <a name="technical-considerations-and-tradeoffs"></a>Considérations et concessions techniques

Vous êtes prêt, car vous avez travaillé via hello problèmes connus avec votre environnement.

Pour les migrations de réel hello, vous pourriez tooconsider :

1. Planifier et programmer de réseau virtuel hello (plus petite unité de la migration) avec l’augmentation de la priorité.  Hello tout d’abord les réseaux virtuels simples, et la progression avec hello plus compliqué de réseaux virtuels.
2. La plupart des clients ont des environnements de production et hors production.  Planifiez la production en dernier.
3. **(FACULTATIF)** Planifiez un temps d’arrêt pour maintenance avec suffisamment de mémoire tampon en cas de problème inattendu.
4. Communiquez et coordonnez-vous avec vos équipes du support technique au cas où des problèmes surviendraient.

### <a name="patterns-of-success"></a>Modèles de réussite

des conseils techniques Hello de hello section de laboratoire de Test ci-dessus doivent être considérée comme réflexion et la migration réelle tooa préalable.  Avec les tests appropriés, migration de hello est en fait un non-événement.  Pour les environnements de production, il peut être utile toohave prise en charge supplémentaire, par exemple un partenaire Microsoft ou des services Microsoft Premier.

### <a name="pitfalls-tooavoid"></a>Pièges tooavoid

Test pas totalement peut causer des problèmes et délai de migration de hello.  

## <a name="beyond-migration"></a>Au-delà de la migration

### <a name="technical-considerations-and-tradeoffs"></a>Considérations et concessions techniques

Maintenant que vous êtes dans le Gestionnaire de ressources Azure, agrandissez la plateforme de hello.  Hello de lecture [vue d’ensemble du Gestionnaire de ressources Azure](../../azure-resource-manager/resource-group-overview.md) toofind out sur les avantages supplémentaires.

Éléments tooconsider :

- Regroupement de migration hello avec d’autres activités.  La plupart des clients choisissent une fenêtre de maintenance des applications.  Si, par conséquent, vous souhaiterez peut-être toouse tooenable de ce temps d’arrêt autres fonctionnalités Azure Resource Manager, comme le chiffrement et migration tooManaged disques.
- Revoient hello technique et des raisons professionnelles pour le Gestionnaire de ressources Azure ; Activer hello des services supplémentaires disponibles uniquement sur Azure Resource Manager qui s’appliquent tooyour environnement.
- Modernisez votre environnement avec les services PaaS.

### <a name="patterns-of-success"></a>Modèles de réussite

Être collectées sur les services vous maintenant que vous souhaitez tooenable dans Azure Resource Manager.  De nombreux clients recherche hello ci-dessous intéressantes pour leurs environnements Azure :

- [Contrôle d’accès en fonction du rôle](../../azure-resource-manager/resource-group-overview.md#access-control).
- [Modèles Azure Resource Manager, pour un déploiement plus facile et mieux contrôlé](../../azure-resource-manager/resource-group-overview.md#template-deployment).
- [Tags](../../azure-resource-manager/resource-group-using-tags.md) (balises).
- [Contrôle d’activité](../../azure-resource-manager/resource-group-audit.md)
- [Stratégies de ressources](../../azure-resource-manager/resource-manager-policy.md)

### <a name="pitfalls-tooavoid"></a>Pièges tooavoid

N’oubliez pas de raison pour laquelle vous avez démarré ce parcours de migration classique tooAzure Gestionnaire de ressources.  Quels sont les raisons professionnelles d’origine hello ? Avez-vous obtenu bonne raison de hello ?


## <a name="next-steps"></a>Étapes suivantes

* [Vue d’ensemble de la plateforme prise en charge la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Techniques détaillées sur la plateforme prise en charge la migration à partir de tooAzure classique Gestionnaire de ressources](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Planification de la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Utiliser les ressources IaaS PowerShell toomigrate classique tooAzure Gestionnaire de ressources](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Outils de communauté qui contribuent à la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Passer en revue les erreurs courantes de migration](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Hello de révision plus Forum aux questions sur la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
