---
title: "aaaGet a démarré avec un espace de travail Analytique des journaux Azure | Documents Microsoft"
description: "Vous pouvez devenir opérationnel avec un espace de travail dans Log Analytics en quelques minutes."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 508716de-72d3-4c06-9218-1ede631f23a6
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/08/2017
ms.author: magoedte
ms.openlocfilehash: 442a9258a37ee79e8f0b45759ef24b5e3dae0130
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-a-log-analytics-workspace"></a>Prise en main d’un espace de travail Log Analytics
Vous pouvez devenir rapidement opérationnel avec Azure Log Analytics, qui vous aide à évaluer l’intelligence opérationnelle collectée à partir de votre infrastructure informatique. Grâce à cet article, vous pouvez facilement commencer à découvrir, analyser et agir sur les données que vous collectez, et cela *gratuitement*.

Cet article sert un tooLog introduction Analytique à l’aide d’une brève toowalk didacticiel vous via un déploiement minimal dans Azure afin que vous pouvez démarrer à l’aide du service de hello. conteneur logique de Hello où sont stockées vos données de gestion dans Azure est appelé un espace de travail. Après avoir consulté ces informations et terminé votre propre version d’évaluation, vous pouvez supprimer l’espace de travail d’évaluation hello. Étant donné que cet article est un didacticiel, il ne fournit aucune information sur la configuration requise, la planification ou l’architecture.

>[!NOTE]
>Si vous utilisez hello Microsoft Azure Government Cloud, utilisez [d’analyse Azure Government + documentation sur la gestion](https://docs.microsoft.com/azure/azure-government/documentation-government-services-monitoringandmanagement#log-analytics) à la place.

Voici un aperçu rapide tooget de processus utilisé hello démarré :

![diagramme du processus](./media/log-analytics-get-started/onboard-oms.png)

## <a name="1-create-an-azure-account-and-sign-in"></a>1 Créer un compte Azure et se connecter

Si vous n’avez pas déjà un compte Azure, vous devez toouse d’un toocreate Analytique de journal. Vous pouvez créer un [compte gratuit](https://azure.microsoft.com/free/) vous permettant d’accéder à n’importe quel service Azure pendant 30 jours.

### <a name="toocreate-a-free-account-and-sign-in"></a>toocreate un compte gratuit et vous connecter
1. Suivez les instructions de hello au [créer gratuitement un compte Azure](https://azure.microsoft.com/free/).
2. Accédez toohello [portail Azure](https://portal.azure.com) et connectez-vous.

## <a name="2-create-a-workspace"></a>2 Créer un espace de travail

étape suivante de Hello est toocreate un espace de travail.

1. Bonjour portail Azure, rechercher liste hello de services Bonjour Marketplace pour *Analytique de journal*, puis sélectionnez **Analytique de journal**.  
    ![Portail Azure](./media/log-analytics-get-started/log-analytics-portal.png)
2. Cliquez sur **créer**, puis sélectionnez les options pour hello éléments suivants :
   * **Espace de travail OMS** : entrez un nom pour votre espace de travail.
   * **Abonnement** : Si vous avez plusieurs abonnements, choisissez celui que vous souhaitez tooassociate avec le nouvel espace de travail hello hello.
   * **Groupe de ressources**
   * **Emplacement**
   * **Niveau de tarification**  
       ![création rapide](./media/log-analytics-get-started/oms-onboard-quick-create.png)
3. Cliquez sur **OK** toosee une liste de vos espaces de travail.
4. Sélectionnez un espace de travail toosee ses détails dans hello portail Azure.       
    ![détails sur l’espace de travail](./media/log-analytics-get-started/oms-onboard-workspace-details.png)         

## <a name="3-upgrade-workspace-toonew-log-search"></a>Recherche de journal toonew espace de travail de mise à niveau 3
Un nouveau langage de requête Analytique de journal a été publié et dans l’ordre tootake bénéficier, vous devez tooconvert votre espace de travail.  Si la région de hello hébergé dans votre espace de travail a été mis à niveau, vous devez voir une bannière violette haut hello de votre espace de travail vous invite tooconvert. mise à niveau Hello est facultative et n’affecte pas votre expérience avec Analytique de journal et les solutions que vous ajoutez.  

Pour autres avantages de hello informations toounderstand, considérations et tooupgrade de processus, consultez [recherche de journal de la mise à niveau Analytique de journal Azure toonew](log-analytics-log-search-upgrade.md).  

## <a name="4-add-solutions-and-solution-offerings"></a>4 Ajouter des solutions et des offres de solutions

Ajoutez ensuite des solutions de gestion et des offres de solutions. Les solutions de gestion représentent une collection de règles logiques, de visualisation et d'acquisition des données qui fournissent des mesures cernant un domaine problématique en particulier. Une offre de solution est un ensemble de solutions de gestion.

Ajout d’espace de travail tooyour solutions permet Analytique de journal toocollect différents types de données à partir d’ordinateurs qui sont connectés tooyour espace de travail à l’aide d’agents. Nous aborderons l’intégration des agents ultérieurement.

### <a name="tooadd-solutions-and-solution-offerings"></a>tooadd des solutions et des offres de solutions

1. Dans le portail Azure, cliquez sur **nouveau** , puis dans hello **marketplace de hello recherche** , tapez **Analytique de journal d’activité** puis appuyez sur ENTRÉE.
2. Dans hello tout ce panneau, sélectionnez **Analytique de journal d’activité** puis cliquez sur **créer**.  
    ![Log Analytics des activités](./media/log-analytics-get-started/activity-log-analytics.png)  
3. Bonjour *nom de la solution gestion* panneau, sélectionnez un espace de travail que vous souhaitez tooassociate avec la solution de gestion hello.
4. Cliquez sur **Créer**.  
    ![espace de travail de la solution](./media/log-analytics-get-started/solution-workspace.png)  
5. Répétez les étapes 1 à 4 tooadd :
    - Hello **sécurité et conformité** offre de service avec les solutions d’évaluation du logiciel anti-programme malveillant et sécurité et Audit hello.
    - Hello **Automation & contrôle** offre de service avec hello Worker hybride Automation, le suivi des modifications et des solutions d’évaluation de mise à jour système (également appelé gestion de la mise à jour). Vous devez créer un compte Automation lorsque vous ajoutez offre des solutions hello.  
        ![Compte Automation](./media/log-analytics-get-started/automation-account.png)  
6. Vous pouvez afficher les solutions de gestion hello que vous avez ajouté un espace de travail tooyour en naviguant trop**Analytique de journal** > **abonnements** > ***nom de l’espace de travail***  >  **Vue d’ensemble**. Vignettes pour les solutions de gestion hello que vous avez ajoutés sont affichés.  
    >[!NOTE]
    >Étant donné que nous n’avons pas encore connecté n’importe quel espace de travail toohello agents, vous ne voyez pas toutes les données pour les solutions hello que vous avez ajouté.  

    ![mosaïques de solution sans données](./media/log-analytics-get-started/solutions-no-data.png)

## <a name="4-create-a-vm-and-onboard-an-agent"></a>4 Créer une machine virtuelle et intégrer un agent

Créez ensuite une machine virtuelle simple dans Azure. Après avoir créé une machine virtuelle, intégrer hello OMS agent tooenable il. L’activation agent de hello commence la collecte de données à partir de la machine virtuelle de hello et envoie des données tooLog Analytique.

### <a name="toocreate-a-virtual-machine"></a>toocreate une machine virtuelle

- Suivez les instructions de hello au [créer votre première machine virtuelle de Windows Bonjour Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md) et démarrer la machine virtuelle hello.

### <a name="connect-hello-virtual-machine-toolog-analytics"></a>Se connecter tooLog de machine virtuelle hello Analytique

- Suivez les instructions de hello au [tooLog de machines virtuelles Azure de se connecter Analytique](log-analytics-azure-vm-extension.md) tooconnect hello VM tooLog Analytique à l’aide de hello portail Azure.

## <a name="6-view-and-act-on-data"></a>6 Visualiser et manipuler les données

Auparavant, vous activé solution Analytique de journal d’activité de hello et des offres de service de sécurité et de conformité et d’Automation et de contrôle hello. Nous observons ensuite les données collectées par les solutions et les résultats des recherches dans les journaux.

toostart, examinez les données affichées dans les solutions à partir de. Examinez ensuite certaines recherches dans les journaux accessibles à partir de recherches dans les journaux. Recherches de journal vous toocombine et mettre en corrélation des données machine de plusieurs sources dans votre environnement. Pour plus d’informations, consultez [connecter recherche Analytique de journal](log-analytics-log-searches.md) ou si vous avez converti votre espace de travail toohello nouveau langage de requête, consultez [recherche de journal de présentation dans Analytique de journal](log-analytics-log-search-new.md). 

### <a name="tooview-antimalware-data"></a>tooview les données contre les logiciels malveillants

1. Dans l’hello portail Azure, accédez trop**Analytique de journal** > ***votre espace de travail***.
2. Dans le panneau de hello pour votre espace de travail, sous **général**, cliquez sur **vue d’ensemble**.  
    ![Vue d'ensemble](./media/log-analytics-get-started/overview.png)
3. Cliquez sur hello **évaluation du logiciel anti-programme malveillant** vignette. Dans cet exemple, vous pouvez voir que Windows Defender est installé sur un ordinateur, mais que sa signature est obsolète.  
    ![Logiciel anti-programme malveillant](./media/log-analytics-get-started/solution-antimalware.png)
4. Pour cet exemple, sous **état de la Protection**, cliquez sur **Signature obsolète** tooopen recherche de journal et consulter les détails sur les ordinateurs hello qui ont des signatures obsolètes. Dans cet exemple, Notez cet ordinateur hello est nommé *getstarted*. S’il existe plusieurs ordinateurs avec des signatures obsolètes, ils tous apparaissent dans hello recherche de journal de résultats.  
    ![Logiciel anti-programme malveillant obsolète](./media/log-analytics-get-started/antimalware-search.png)

### <a name="tooview-security-and-audit-data"></a>tooview données sécurité et Audit

1. Dans le panneau de hello pour votre espace de travail, sous **général**, cliquez sur **vue d’ensemble**.  
2. Cliquez sur hello **sécurité et Audit** vignette. Dans cet exemple, vous pouvez voir deux problèmes importants : des mises à jour critiques sont manquantes sur un ordinateur et la protection est insuffisante sur un autre ordinateur.  
    ![Sécurité et audit](./media/log-analytics-get-started/security-audit.png)
3. Pour cet exemple, sous **problèmes importants**, cliquez sur **ordinateurs les mises à jour critiques manquantes** tooopen recherche de journal et consulter les détails sur les ordinateurs des mises à jour critiques manquantes. Dans cet exemple, une mise à jour critique est manquante et 63 autres mises à jour sont manquantes.  
    ![Recherche dans les journaux Sécurité et audit](./media/log-analytics-get-started/security-audit-log-search.png)

### <a name="tooview-and-act-on-system-update-data"></a>tooview et agir sur les données de mise à jour du système

1. Dans le panneau de hello pour votre espace de travail, sous **général**, cliquez sur **vue d’ensemble**.  
2. Cliquez sur hello **évaluation des mises à jour du système** vignette. Dans cet exemple, vous pouvez voir qu’il existe un ordinateur Windows nommé *getstarted* nécessitant des mises à jour critiques et un qui nécessite des mises à jour de définition.  
    ![Mises à jour du système](./media/log-analytics-get-started/system-updates.png)
3. Pour cet exemple, sous **les mises à jour manquantes**, cliquez sur **mises à jour critiques** tooopen recherche de journal et consulter les détails sur les ordinateurs des mises à jour critiques manquantes. Dans cet exemple, une mise à jour est manquante et une mise à jour est obligatoire.  
    ![Recherche dans les journaux de mises à jour du système](./media/log-analytics-get-started/system-updates-log-search.png)
4. Accédez toohello [Operations Management Suite](http://microsoft.com/oms) site Web et connectez-vous avec votre compte Azure. Lorsque connecté, notez que les informations sur la solution hello soient similaire toowhat affiche Bonjour portail Azure.  
    ![Portail OMS](./media/log-analytics-get-started/oms-portal.png)
5. Cliquez sur hello **gestion de la mise à jour** vignette.
6. Dans le tableau de bord de gestion de mise à jour hello, notez que les informations de mise à jour système hello sont toohello système mettre à jour des informations similaires que vous avez vu Bonjour portail Azure. Toutefois, hello **gérer les déploiements de mises à jour** vignette est nouveau. Cliquez sur hello **gérer les déploiements de mises à jour** vignette.  
    ![Mosaïque de gestion des mises à jour](./media/log-analytics-get-started/update-management.png)
7. Sur hello **mettre à jour des déploiements** , cliquez sur **ajouter** toocreate un *mise à jour de l’exécution*.  
    ![Update Deployments](./media/log-analytics-get-started/update-management-update-deployments.png) (Déploiements de mises à jour)
8.  Sur hello **nouveau déploiement de mise à jour** , tapez un nom pour le déploiement de mises à jour hello, sélectionnez les ordinateurs tooupdate (dans cet exemple, *getstarted*), choisissez une planification, puis cliquez sur **enregistrer**.  
    ![Nouveau déploiement](./media/log-analytics-get-started/new-deployment.png)  
    Après avoir enregistré le déploiement de mises à jour hello, vous voyez hello planifiée mettre à jour.  
    ![mise à jour planifiée](./media/log-analytics-get-started/scheduled-update.png)  
    Une fois l’exécution de la mise à jour hello est terminée, hello état montre **terminé**.
    ![mise à jour terminée](./media/log-analytics-get-started/completed-update.png)
9. Une fois l’exécution de la mise à jour hello terminée, vous pouvez afficher si hello exécuter a réussi ou non, et vous pouvez afficher plus d’informations sur les mises à jour en cas d’application.

## <a name="after-evaluation"></a>Après l’évaluation

Dans ce didacticiel, vous avez installé un agent sur une machine virtuelle et vous avez démarré rapidement. Hello étapes ont été simple et rapide. Toutefois, la plupart des grandes organisations et entreprises ont des infrastructures informatiques locales complexes. Par conséquent, la collecte de données à partir de ces environnements complexes prend supplémentaires de planification et de l’effort que hello didacticiel effectue. Vérifiez les informations de hello Bonjour suivant la section étapes suivante pour les articles toohelpful de liens.

Vous pouvez éventuellement supprimer espace de travail hello que vous avez créé avec ce didacticiel.

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur la connexion [agents Windows](log-analytics-windows-agents.md) tooLog Analytique.
* En savoir plus sur la connexion [agents Operations Manager](log-analytics-om-agents.md) tooLog Analytique.
* [Ajouter des solutions d’Analytique de journal à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md) tooadd fonctionnalité et collecter les données.
* Se familiariser avec [recherche de journal](log-analytics-log-searches.md) tooview détaillées des informations collectées par les solutions.
