---
title: Forum aux questions sur la migration des plates-formes aaaSecurity Center | Documents Microsoft
description: "Ce forum aux questions répond aux questions sur hello migration de plateforme de Centre de sécurité Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4d1364cd-7847-425a-bb3a-722cb0779f78
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: terrylan
ms.openlocfilehash: fcb14ae83167ef79a60371e4fcb625cf99bee6c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="security-center-platform-migration-faq"></a>FAQ sur la migration de plateforme Security Center
Dans les premières juin 2017, Azure Security Center a commencé à l’aide de Microsoft Monitoring Agent toocollect et le magasin de données d’hello. toolearn, voir [Azure Security Center Platform Migration](security-center-platform-migration.md). Ce forum aux questions répond aux questions sur la migration de la plate-forme hello.

## <a name="data-collection-agents-and-workspaces"></a>Collecte de données, agents et espaces de travail

### <a name="how-is-data-collected"></a>Comment les données sont-elles collectées ?
Centre de sécurité utilise des données de sécurité toocollect hello Microsoft Monitoring Agent à partir de vos machines virtuelles. les données de sécurité Hello incluent des informations sur les configurations de sécurité, qui sont utilisés tooidentify vulnérabilités, et les événements de sécurité, qui sont les menaces toodetect utilisé. Les données collectées par l’agent de hello sont stockées dans un toohello d’espace de travail connecté Analytique de journal existant machine virtuelle ou un espace de travail créé par le centre de sécurité. Lorsque le centre de sécurité crée un nouvel espace de travail, géolocalisation hello Hello machine virtuelle est prise en compte.

> [!NOTE]
> Hello Microsoft Monitoring Agent est hello même agent utilisé par hello Operations Management Suite (OMS), le service de journal Analytique et System Center Operations Manager (SCOM).
>
>

Lors de la collecte de données est activée pour hello première fois ou lorsque vos abonnements sont migrés, le centre de sécurité vérifie toosee si hello Microsoft Monitoring Agent est déjà installé comme une extension d’Azure sur chacun de vos machines virtuelles. Si hello Microsoft Monitoring Agent n’est pas installé, le centre de sécurité seront :

- installer l’agent Microsoft Monitoring de hello sur hello machine virtuelle
   - Si un espace de travail créé par le centre de sécurité déjà existe dans hello même emplacement géographique comme hello de machine virtuelle, hello agent est connecté toothis espace de travail
   - Si un espace de travail n’existe pas, le centre de sécurité crée un nouveau groupe de ressources par défaut d’espace de travail dans cet emplacement géographique et connecter l’espace de travail toothat hello agent. convention d’affectation de noms de Hello pour le groupe de ressources et d’espace de travail hello sont les suivantes :

       Espace de travail : DefaultWorkspace-[ID d’abonnement]-[zone géographique]

       Groupe de ressources : DefaultResouceGroup-[zone géographique]
- installer une solution de centre de sécurité sur l’espace de travail hello

emplacement Hello d’espace de travail hello est basée sur emplacement hello Hello machine virtuelle. toolearn, voir [sécurité des données](security-center-data-security.md).

> [!NOTE]
> Tooplatform préalable migration, centre de sécurité des données de sécurité collectées à partir de vos machines virtuelles à l’aide de hello Agent de surveillance Azure et stockage de données dans votre compte de stockage. Après la migration de plate-forme hello, centre de sécurité utilise hello Microsoft Monitoring Agent et magasin et espace de travail toocollect hello des mêmes données. compte de stockage Hello peut être supprimé après la migration de hello.
>
>

### <a name="am-i-billed-for-log-analytics-or-oms-on-hello-workspaces-created-by-security-center"></a>Facturation pour l’Analytique de journal ou OMS sur les espaces de travail hello créés par le centre de sécurité ?
Non. Les espaces de travail créés par Security Center, bien qu’ils soient configurés pour une facturation OMS par nœud, n’entraînent pas de frais OMS. Centre de sécurité facturation est toujours basé sur votre centre de sécurité stratégie hello solutions de sécurité et installées sur un espace de travail :

- **Niveau gratuit** – centre de sécurité installe la solution de 'SecurityCenterFree' de hello sur l’espace de travail par défaut hello. Vous n’êtes pas facturé pour le niveau gratuit de hello.
- **Niveau standard** : centre de sécurité installe hello 'SecurityCenterFree' et les solutions de « Sécurité » sur hello espace de travail par défaut.

Pour plus d’informations sur la tarification, consultez la page de [tarification de Security Center](https://azure.microsoft.com/pricing/details/security-center/). Hello tarification des adresses des pages change toosecurity le stockage de données et le démarrage de facturation au prorata en juin 2017.

> [!NOTE]
> niveau de tarification OMS Hello d’espaces de travail créés par le centre de sécurité n’affecte pas la facturation du centre de sécurité.
>
>

### <a name="can-i-delete-hello-default-workspaces-created-by-security-center"></a>Puis-je supprimer les espaces de travail hello par défaut créés par le centre de sécurité ?
**Suppression d’espace de travail par défaut hello n’est pas recommandée.** Centre de sécurité utilise des données de sécurité toostore hello par défaut les espaces de travail à partir de vos machines virtuelles.  Si vous supprimez un espace de travail, le centre de sécurité est impossible toocollect ces données et certaines recommandations de sécurité et les alertes ne sont pas disponibles

toorecover, remove hello Microsoft Monitoring Agent sur l’espace de travail connecté toohello supprimé hello machines virtuelles. Centre de sécurité permet de réinstaller l’agent de hello et crée des nouveaux espaces de travail par défaut.

### <a name="what-if-hello-microsoft-monitoring-agent-was-already-installed-as-an-extension-on-hello-vm"></a>Que se passe-t-il si hello Microsoft Monitoring Agent a déjà été installé en tant qu’extension sur hello machine virtuelle ?
Centre de sécurité ne remplace pas les espaces de travail connexions toouser existants. Centre de sécurité stocke les données de sécurité à partir de hello machine virtuelle dans l’espace de travail hello est déjà connecté.

### <a name="what-if-i-had-a-microsoft-monitoring-agent-installed-on-hello-machine-but-not-as-an-extension"></a>Que se passe-t-il si j’avais un Agent de surveillance Microsoft installés sur l’ordinateur de hello, mais pas en tant qu’extension ?
Si hello Microsoft Monitoring Agent est installé directement sur hello VM (et non comme une extension d’Azure), le centre de sécurité n’installera pas hello Microsoft Monitoring Agent et analyse de la sécurité est limité.

### <a name="what-is-hello-impact-of-removing-these-extensions"></a>Nouveautés d’impact hello de la suppression de ces extensions ?
Si vous supprimez hello Extension de surveillance de Microsoft, le centre de sécurité n’est pas en mesure de toocollect les données de sécurité à partir de la machine virtuelle de hello et certaines recommandations de sécurité et des alertes ne sont pas disponibles. Dans les 24 heures, centre de sécurité détermine que hello machine virtuelle est manquant pour extension de hello et réinstalle hello extension.

### <a name="how-do-i-stop-hello-automatic-agent-installation-and-workspace-creation"></a>Comment arrêter l’installation d’agent automatique hello et création de l’espace de travail ?
Vous pouvez désactiver la collecte de données pour vos abonnements dans la stratégie de sécurité hello, mais cela n’est pas recommandé. La désactivation de la collecte de données a pour effet de limiter les recommandations Security Center et les alertes. Collecte de données est requise pour les abonnements sur la tarification Standard hello. collecte des données toodisable :

1. Si votre abonnement est configuré pour le niveau Standard de hello, ouvrir la stratégie de sécurité hello pour cet abonnement et sélectionnez hello **libre** couche.

   ![Niveau tarifaire ][1]

2. Ensuite, désactiver la collecte de données en sélectionnant **hors** sur hello **stratégie de sécurité : collecte de données** panneau.

   ![Collecte des données][2]

### <a name="how-do-i-remove-oms-extensions-installed-by-security-center"></a>Comment supprimer des extensions OMS installées par Security Center ?
Vous pouvez supprimer manuellement hello Microsoft Monitoring Agent. Ce n’est pas recommandé car cela limite les recommandations de Security Center et les alertes.

> [!NOTE]
> Si la collecte de données est activée, le centre de sécurité réinstalle l’agent de hello après que l’avoir supprimé.  Vous devez toodisable collecte des données avant de supprimer manuellement l’agent de hello. Consultez [comment faire cesser la création automatique de l’agent installation et l’espace de travail hello ?](#how-do-i-stop-the-automatic-agent-installation-and-workspace-creation?) pour obtenir des instructions sur la désactivation de la collecte de données.
>
>

toomanually supprimer l’agent de hello :

1.  Dans le portail de hello, ouvrez **Analytique de journal**.
2.  Dans Panneau de journal Analytique hello, sélectionnez un espace de travail :
3.  Sélectionnez chaque ordinateur virtuel que vous ne souhaitez toomonitor, sélectionnez **déconnexion**.

   ![Supprimer l’agent de hello][3]

> [!NOTE]
> Si un VM Linux possède déjà un agent OMS sans extension, suppression hello extension supprime également l’agent hello et un client de hello tooreinstall il.
>
>

## <a name="existing-oms-customers"></a>Clients OMS existants

### <a name="does-security-center-override-any-existing-connections-between-vms-and-workspaces"></a>Est-ce que Security Center peut écraser les connexions existantes entre les machines virtuelles et les espaces de travail ?
Si un ordinateur virtuel a déjà hello Microsoft Monitoring Agent est installé comme une extension d’Azure, le centre de sécurité ne remplace pas de connexion d’espace de travail existante hello. En revanche, le centre de sécurité utilise espace de travail existant hello.

Une solution de centre de sécurité est installé sur l’espace de travail hello si n’est pas présent déjà, et les solutions hello est appliqué toohello uniquement machines virtuelles appropriés. Lorsque vous ajoutez une solution, il est déployé automatiquement par défaut tooall Windows et Linux agents connectés tooyour Analytique de journal espace de travail. [Ciblage de la solution](../operations-management-suite/operations-management-suite-solution-targeting.md), qui est une fonctionnalité d’OMS, vous permet de tooapply une étendue tooyour solutions.

Si hello Microsoft Monitoring Agent est installé directement sur hello VM (et non comme une extension d’Azure), le centre de sécurité n’installera pas hello Microsoft Monitoring Agent et analyse de la sécurité est limitée.

### <a name="what-should-i-do-if-i-suspect-that-hello-data-platform-migration-broke-hello-connection-between-one-of-my-vms-and-my-workspace"></a>Que dois-je faire si je pense que migration hello de la plate-forme de données a interrompu la connexion hello entre un de mes machines virtuelles et mon espace de travail ?
Cela ne devrait pas se produire. S’il peut arriver, puis [créer une demande de support Azure](../azure-supportability/how-to-create-azure-support-request.md) et inclure hello les détails suivants :

- ID de ressource Azure Hello Hello incidence sur la machine virtuelle
- ID de ressource Azure Hello d’espace de travail hello configuré sur l’extension de hello avant hello connexion a été interrompue
- l’agent de Hello et de version qui a déjà été installée

### <a name="does-security-center-install-solutions-on-my-existing-oms-workspaces-what-are-hello-billing-implications"></a>Est-ce que Security Center installe des solutions sur mes espaces de travail OMS existants ? Quelles sont les conséquences de facturation hello ?
Lorsque le centre de sécurité identifie qu’une machine virtuelle est déjà connecté tooa espace de travail créé, le centre de sécurité offrent des solutions sur cet espace de travail en fonction de tooyour niveau tarifaire. Hello solutions est des machines virtuelles Azure pertinentes, toohello uniquement appliqué [solution ciblant](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting), de sorte que le reste de facturation hello hello identiques.

- **Niveau gratuit** – centre de sécurité installe la solution de 'SecurityCenterFree' de hello sur l’espace de travail hello. Vous n’êtes pas facturé pour le niveau gratuit de hello.
- **Niveau standard** : centre de sécurité installe hello 'SecurityCenterFree' et les solutions de « Sécurité » sur hello espace de travail.

   ![Solutions sur l’espace de travail par défaut][4]

> [!NOTE]
> Hello solution « Sécurité » dans le journal Analytique est sécurité Bonjour solution d’Audit d’OMS.
>
>

### <a name="i-already-have-workspaces-in-my-environment-can-i-use-them-toocollect-security-data"></a>Espaces de travail est déjà dans mon environnement, puis-je utiliser les données de sécurité toocollect ?
Si un ordinateur virtuel a déjà hello Microsoft Monitoring Agent est installé comme une extension d’Azure, le centre de sécurité utilise espace de travail connecté hello existant. Une solution de centre de sécurité est installé sur l’espace de travail hello si n’est pas présent déjà et solution de hello est appliqué toohello uniquement pertinentes machines virtuelles via [solution ciblant](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting).

Lorsque le centre de sécurité installe hello Microsoft Monitoring Agent sur des machines virtuelles, il utilise hello espace de valeur par défaut créé par le centre de sécurité. Bientôt, les clients seront en mesure de tooconfigure quel espace est utilisés.

### <a name="i-already-have-security-solution-on-my-workspaces-what-are-hello-billing-implications"></a>Je dispose déjà de la solution de sécurité sur mes espaces de travail. Quelles sont les conséquences de facturation hello ?
Hello solution sécurité et Audit est tooenable utilisé les fonctionnalités de couche Security Center Standard pour les machines virtuelles Azure. Si la solution de sécurité et Audit hello est déjà installée sur un espace de travail, le centre de sécurité utilise les solutions existantes hello. Il n’y aura aucune modification de la facturation.

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur la migration de la plate-forme hello centre de sécurité, consultez

- [Migration de plateforme Azure Security Center](security-center-platform-migration.md)
- [Guide de résolution des problèmes d’Azure Security Center](security-center-troubleshooting-guide.md)

<!--Image references-->
[1]: ./media/security-center-platform-migration-faq/pricing-tier.png
[2]: ./media/security-center-platform-migration-faq/data-collection.png
[3]: ./media/security-center-platform-migration-faq/remove-the-agent.png
[4]: ./media/security-center-platform-migration-faq/solutions.png
