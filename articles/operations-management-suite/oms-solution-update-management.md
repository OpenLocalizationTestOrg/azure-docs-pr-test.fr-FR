---
title: aaaUpdate solution de gestion dans OMS | Documents Microsoft
description: "Cet article est prévue toohelp vous comprenez comment toouse toomanage de cette solution met à jour pour vos ordinateurs Windows et Linux."
services: operations-management-suite
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: e33ce6f9-d9b0-4a03-b94e-8ddedcc595d2
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: magoedte
ms.openlocfilehash: 2dd321913bf049ab1996fd60a2f74b8417084dcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="update-management-solution-in-oms"></a>Solution de gestion des mises à jour dans OMS

![Symbole de gestion des mises à jour](./media/oms-solution-update-management/update-management-symbol.png)

Hello solution de gestion de la mise à jour dans OMS vous permet de mises à jour de sécurité de système d’exploitation toomanage pour vos ordinateurs Windows et Linux déployés dans Azure, localement environnements, ou autres fournisseurs de cloud.  Vous pouvez rapidement évaluer l’état hello de mises à jour disponibles sur tous les ordinateurs de l’agent et gérer des processus hello de l’installation des mises à jour requises pour les serveurs.


## <a name="solution-overview"></a>Vue d’ensemble de la solution
Ordinateurs gérés par OMS utilisent suivant de hello pour effectuer des déploiements de mises à jour et d’évaluation :

* Agent OMS pour Windows ou Linux
* PowerShell DSC (Desired State Configuration, configuration d’état souhaité) pour Linux
* Runbook Worker hybride Automation
* Services Microsoft Update ou Windows Server Update pour ordinateurs Windows

Hello suivant diagrammes montre une vue conceptuelle du flux de données et le comportement hello avec la solution de hello évalue et applique tooall de mises à jour de sécurité de connexion Windows Server et les ordinateurs Linux dans un espace de travail.    

#### <a name="windows-server"></a>Windows Server
![Flux de processus de gestion des mises à jour Windows Server](media/oms-solution-update-management/update-mgmt-windows-updateworkflow.png)

#### <a name="linux"></a>Linux
![Flux de processus de gestion des mises à jour Linux](media/oms-solution-update-management/update-mgmt-linux-updateworkflow.png)

Une fois que l’ordinateur de hello effectue une analyse de conformité de mise à jour, l’agent OMS de hello transfère les informations de hello dans les tooOMS en bloc. Sur un ordinateur de la fenêtre, analyse de compatibilité hello est effectuée toutes les 12 heures par défaut.  En outre toohello analyse hello pour la conformité de mise à jour, planification de l’analyse est lancée dans les 15 minutes si hello Microsoft Monitoring Agent (MMA) est redémarré, préalable tooupdate installation et après l’installation de la mise à jour.  Avec un ordinateur Linux, analyse de compatibilité hello est exécutée toutes les 3 heures par défaut, et une analyse de conformité est lancée dans les 15 minutes si l’agent MMA hello est redémarré.  

Hello les informations de compatibilité sont ensuite traitées et résumées dans les tableaux de bord hello inclus dans les solutions hello ou consultable à l’aide de défini par l’utilisateur ou pre-défini des requêtes.  solution Hello signale la hello ordinateur est basée sur la source que vous êtes configuré toosynchronize avec.  Si l’ordinateur Windows hello est tooWSUS tooreport configuré, en fonction de lorsque WSUS dernière synchronisation avec Microsoft Update, les résultats hello peuvent différer de ce que montre Microsoft Updates.  Hello même pour les ordinateurs Linux qui sont configurés tooreport tooa de référentiel local par rapport à un référentiel public.   

Vous pouvez déployer et installer des mises à jour logicielles sur les ordinateurs qui nécessitent des mises à jour de hello en créant un déploiement planifié.  Les mises à jour classées comme *facultatif* ne sont pas inclus dans la portée de déploiement hello pour les ordinateurs Windows, uniquement les mises à jour requises.  Hello déploiement planifié définit quels ordinateurs cibles mises à jour hello applicable, soit en spécifiant les ordinateurs explicitement ou en sélectionnant un [groupe d’ordinateurs](../log-analytics/log-analytics-computer-groups.md) qui est basé sur les recherches de journal d’un ensemble particulier de ordinateurs.  Également, vous spécifiez un tooapprove de planification et que vous désignez un certain temps lorsque les mises à jour sont autorisées toobe installé au sein de.  Les mises à jour sont installées par des Runbooks dans Azure Automation.  Vous ne pouvez pas visualiser ces Runbooks, qui ne nécessitent aucune configuration.  Lors de la création d’un déploiement de mise à jour, il crée une planification que démarre un runbook maître de mise à jour à hello spécifié pour les ordinateurs hello inclus.  Ce Runbook principal lance un Runbook enfant sur chaque agent qui effectue l’installation des mises à jour obligatoires.       

À la date de hello et l’heure spécifiées dans le déploiement de mises à jour hello, ordinateurs cibles de hello exécute le déploiement de hello en parallèle.  Une analyse est le premier mises à jour de hello tooverify effectuées sont toujours nécessaires et les installe.  Il est important de toonote pour les ordinateurs clients WSUS si les mises à jour hello ne sont pas approuvées dans WSUS, le déploiement de mises à jour hello échouera.  Hello des mises à jour hello appliqué sont transmises tooOMS toobe traités et résumées dans les tableaux de bord hello ou par hello recherche d’événements de hello.     

## <a name="prerequisites"></a>Composants requis
* solution de Hello prend en charge d’exécution des évaluations de mise à jour par rapport à Windows Server 2008 et versions ultérieures et mettre à jour des déploiements sur Windows Server 2008 R2 SP1 et versions ultérieures.  Les options d’installation Server Core et Nano Server ne sont pas prises en charge.

    > [!NOTE]
    > Prise en charge pour le déploiement de mises à jour tooWindows Server 2008 R2 SP1 nécessite .NET Framework 4.5 et WMF 5.0 ou version ultérieure.
    >  
* Les systèmes d’exploitation clients Windows ne sont pas pris en charge.  
* Les agents Windows doivent être toocommunicate configuré avec un serveur Windows Server Update Services (WSUS) ou avoir accès tooMicrosoft mise à jour.  

    > [!NOTE]
    > l’agent Windows Hello ne peut pas être géré simultanément par System Center Configuration Manager.  
    >
* CentOS 6 (x86/x64) et 7 (x 64)  
* Red Hat Enterprise 6 (x86/x64) et 7 (x 64)  
* SUSE Linux Enterprise Server 11 (x86/x64) et 12 (x64)  
* Ubuntu 12.04 LTS et x86/x64 plus récente   
    > [!NOTE]  
    > mises à jour tooavoid appliquées en dehors d’une fenêtre de maintenance sur Ubuntu, reconfigurez les mises à jour automatiques de mise à niveau sans assistance package toodisable. Pour plus d’informations sur la façon de tooconfigure, consultez [rubrique mises à jour automatiques dans hello Ubuntu Server Guide](https://help.ubuntu.com/lts/serverguide/automatic-updates.html).

* Agents Linux doivent avoir le référentiel de mise à jour tooan accès.  

    > [!NOTE]
    > Un Agent OMS pour Linux configuré des espaces de travail OMS tooreport toomultiple n'est pas pris en charge avec cette solution.  
    >

Pour plus d’informations sur comment tooinstall hello Agent OMS pour Linux et télécharger la version la plus récente hello, consultez trop[Operations Management Suite Agent for Linux](https://github.com/microsoft/oms-agent-for-linux).  Pour plus d’informations sur la façon dont tooinstall hello OMS Agent pour Windows, consultez [Operations Management Suite Agent pour Windows](../log-analytics/log-analytics-windows-agents.md).  

### <a name="permissions"></a>Autorisations
Dans l’ordre toocreate les déploiements de mise à jour, vous devez toobe accordé le rôle de collaborateur hello dans votre compte Automation et l’espace de travail Analytique de journal.  

## <a name="solution-components"></a>Composants de la solution
Cette solution se compose de hello suivant les ressources qui sont ajoutées compte Automation de tooyour et des agents connectés directement ou groupe d’administration connecté Operations Manager.

### <a name="management-packs"></a>Packs d’administration
Si votre groupe d’administration System Center Operations Manager est un espace de travail OMS tooan connecté, hello suivant des packs d’administration est installé dans Operations Manager.  Ces packs d’administration sont également installés sur des ordinateurs Windows directement connectés après l’ajout de cette solution. Il n’y a rien tooconfigure ou gérer ces packs d’administration.

* Microsoft System Center Advisor Update Assessment Intelligence Pack (Microsoft.IntelligencePacks.UpdateAssessment)
* Microsoft.IntelligencePack.UpdateAssessment.Configuration (Microsoft.IntelligencePack.UpdateAssessment.Configuration)
* Pack d’administration du déploiement des mises à jour

Pour plus d’informations sur la façon dont les packs d’administration de solution sont mises à jour, consultez [connecter Operations Manager tooLog Analytique](../log-analytics/log-analytics-om-agents.md).

### <a name="hybrid-worker-groups"></a>Groupes de Workers hybrides
Après avoir activé cette solution, tous les ordinateurs Windows directement connecté tooyour espace de travail OMS est automatiquement configuré comme un runbook de hello Runbook Worker hybride toosupport inclus dans cette solution.  Pour chaque ordinateur Windows géré par la solution de hello, il sera répertorié sous le panneau de groupes de travail de Runbook hybride hello du compte d’automatisation hello respectent les conventions d’affectation de noms de hello *Hostname FQDN_GUID*.  Vous ne pouvez pas cibler ces groupes avec des Runbooks dans votre compte ; sinon ils échouent. Ces groupes sont uniquement les solutions de gestion hello toosupport prévue.   

Toutefois, vous pouvez d’ajouter le groupe de travail de Runbook hybride de hello Windows ordinateurs tooa dans votre toosupport de compte d’automatisation de runbook Automation tant que vous utilisez le même compte pour les solutions hello et l’appartenance au groupe de travail de Runbook hybride de hello.  Cette fonctionnalité a été ajoutée tooversion 7.2.12024.0 Hello Runbook Worker hybride.  

## <a name="configuration"></a>Configuration
Effectuer hello suivant les étapes tooadd hello Update Management solution tooyour espace de travail OMS et confirmez le reporting des agents. Espace de travail Windows agents tooyour déjà connectés sont ajoutés automatiquement sans aucune configuration supplémentaire.

Vous pouvez déployer la solution hello à l’aide de hello méthodes suivantes :

* À partir d’Azure Marketplace Bonjour portail Azure en sélectionnant l’offre d’Automation & contrôle hello ou de solution de gestion de la mise à jour
* À partir de la galerie de Solutions OMS dans votre espace de travail OMS de hello

Si vous avez déjà un compte Automation et l’espace de travail OMS lié dans hello même groupe de ressources et de la région, en sélectionnant Automation & contrôle seront vérifier votre configuration et uniquement installer la solution de hello et configurez-le dans les deux services.  Sélection de solution de gestion de la mise à jour de hello dans Azure Marketplace offre hello même comportement.  Si vous n’avez pas les deux services déployés dans votre abonnement, suivez les étapes de hello Bonjour **créer une nouvelle Solution** panneau et confirmer tooinstall hello autres présélectionnée solutions recommandées.  Si vous le souhaitez, vous pouvez ajouter tooyour de solution de gestion de la mise à jour hello espace de travail OMS à l’aide des étapes de hello décrit dans [solutions OMS d’ajouter](../log-analytics/log-analytics-add-solutions.md) à partir de la galerie des Solutions de hello.  

### <a name="confirm-oms-agents-and-operations-manager-management-group-connected-toooms"></a>Confirmer les agents OMS et Operations Manager management groupe connecté tooOMS

tooconfirm directement connecté l’Agent OMS pour Linux et Windows communiquent avec OMS, après quelques minutes vous pouvez exécuter hello suivant recherche de journal :

* Linux - `Type=Heartbeat OSType=Linux | top 500000 | dedup SourceComputerId | Sort Computer | display Table`.  

* Windows - `Type=Heartbeat OSType=Windows | top 500000 | dedup SourceComputerId | Sort Computer | display Table`

Sur un ordinateur Windows, vous pouvez examiner hello suivant tooverify connectivité de l’agent avec OMS :

1.  Ouvrez Microsoft Monitoring Agent dans le panneau de configuration et sur hello **Azure Analytique des journaux (OMS)** , onglet de hello agent affiche un message indiquant : **hello Microsoft Monitoring Agent n’est pas connecté toohello Microsoft Service Operations Management Suite**.   
2.  Ouvrez hello journal des événements Windows, accédez trop**Application et le Gestionnaire des Services Logs\Operations** et recherchez des événements ID 3000 et 5002 à partir de la source de connecteur de Service.  Ces événements indiquent les ordinateur hello a enregistré avec l’espace de travail OMS hello et reçoit configuration.  

Si l’agent hello n’est pas en mesure de toocommunicate avec hello service OMS et il est configuré toocommunicate avec hello internet via un pare-feu ou un serveur proxy, confirmez hello pare-feu ou serveur proxy est configuré correctement en consultant [réseau configuration de l’agent Windows](../log-analytics/log-analytics-windows-agents.md#network) ou [configuration réseau pour l’agent Linux](../log-analytics/log-analytics-agent-linux.md#network).

> [!NOTE]
> Si vos systèmes Linux sont toocommunicate configuré avec un proxy ou une passerelle d’OMS et l’intégration de cette solution, mettez à jour hello *proxy.conf* groupe d’autorisations toogrant hello omiuser autorisation de lecture sur le fichier hello en exécution hello suivant de commandes :  
> `sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf`  
> `sudo chmod 644 /etc/opt/microsoft/omsagent/proxy.conf`


Les nouveaux agents Linux ajoutés affichent l’état **Mis à jour** après l’exécution d’une évaluation.  Ce processus peut prendre des heures de too6.

tooconfirm Operations Manager groupe d’administration est en communication avec OMS, consultez [valider l’intégration d’Operations Manager avec OMS](../log-analytics/log-analytics-om-agents.md#validate-operations-manager-integration-with-oms).

## <a name="data-collection"></a>Collecte des données
### <a name="supported-agents"></a>Agents pris en charge
Hello tableau suivant décrit les sources de hello connecté sont pris en charge par cette solution.

| Source connectée | Pris en charge | Description |
| --- | --- | --- |
| Agents Windows |Oui |solution de Hello collecte des informations sur les mises à jour du système à partir d’agents Windows et lance l’installation de mises à jour. |
| Agents Linux |Oui |solution de Hello collecte des informations sur les mises à jour du système à partir des agents de Linux et lance l’installation de mises à jour sur les versions prises en charge. |
| Groupe d’administration d’Operations Manager |Oui |solution de Hello collecte des informations sur les mises à jour du système à partir des agents dans un groupe d’administration connecté.<br>Une connexion directe à partir de tooLog de l’agent Operations Manager hello Analytique n’est pas nécessaire. Données sont transférées depuis le référentiel OMS toohello hello gestion groupe. |
| Compte Azure Storage |Non |Le stockage Azure n’inclut aucune information sur les mises à jour du système. |

### <a name="collection-frequency"></a>Fréquence de collecte
Pour chaque ordinateur Windows géré, une analyse est effectuée deux fois par jour. Hello de toutes les 15 minutes API Windows est appelé tooquery pour hello dernière mise à jour heure toodetermine si l’état a changé, et cas dans ce une analyse de conformité est lancée.  Pour chaque ordinateur Linux géré, une analyse est effectuée toutes les 3 heures.

Il peut prendre de 30 minutes, les heures too6 pour les données hello du tableau de bord toodisplay mis à jour sur les ordinateurs gérés.   

## <a name="using-hello-solution"></a>À l’aide de la solution de hello
Lorsque vous ajoutez d’espace de travail hello Update Management solution tooyour OMS, hello **gestion de la mise à jour** vignette sera ajoutée tooyour du tableau de bord OMS. Cette vignette affiche un nombre et une représentation graphique du nombre de hello d’ordinateurs dans votre environnement et leur conformité de mise à jour.<br><br>
![Mosaïque représentant un résumé de la gestion des mises à jour](media/oms-solution-update-management/update-management-summary-tile.png)  


## <a name="viewing-update-assessments"></a>Affichage des évaluations de mises à jour
Cliquez sur hello **gestion de la mise à jour** vignette tooopen hello **gestion de la mise à jour** tableau de bord.<br><br> ![Tableau de bord résumant la gestion des mises à jour](./media/oms-solution-update-management/update-management-dashboard.png)<br>

Ce tableau de bord fournit une description détaillée de l’état de mise à jour classé par type de système d’exploitation et classification de mise à jour : critique, sécurité ou autres (par exemple, une mise à jour de définition). résultats de Hello dans chaque vignette du tableau de bord reflètent uniquement les mises à jour sont approuvées pour le déploiement, qui est basé en fonction de la source de synchronisation des ordinateurs hello.   Hello **des déploiements de mise à jour** vignette lorsque sélectionné, vous redirige la page de mise à jour des déploiements toohello où vous pouvez afficher les planifications, les déploiements en cours d’exécution, les déploiements terminées, ou planifier un nouveau déploiement.  

Vous pouvez exécuter une recherche de journal qui retourne tous les enregistrements en cliquant sur la vignette hello ou toorun une requête d’une catégorie particulière et des critères prédéfinis, sélectionnez-en un dans la liste hello disponible sous hello **requêtes courantes de mise à jour** colonne.    

## <a name="installing-updates"></a>Installation des mises à jour
Une fois que les mises à jour ont été évalués pour tous les hello Linux et les ordinateurs Windows dans votre espace de travail, vous pouvez requis mises à jour installées en créant un *mise à jour de déploiement*.  Un déploiement de mises à jour est une installation planifiée de mises à jour obligatoires pour un ou plusieurs ordinateurs.  Vous spécifiez hello date et l’heure pour le déploiement de hello en outre tooa ordinateur ou groupe d’ordinateurs qui doivent être inclus dans la portée de hello d’un déploiement.  toolearn savoir plus sur les groupes d’ordinateurs, consultez [groupes d’ordinateurs dans le journal Analytique](../log-analytics/log-analytics-computer-groups.md).  Lorsque vous incluez des groupes d’ordinateurs dans votre déploiement de mises à jour, memnbership de groupe est évaluée qu’une seule fois lors de la création de la planification hello.  Groupe de tooa les modifications ultérieures ne sont pas reflétées.  toowork résoudre ce problème, supprimer le déploiement de mise à jour planifiée de hello et recréez-le.

> [!NOTE]
> Machines virtuelles Windows déployée à partir de hello Azure Marketplace par défaut sont définies les mises à jour automatiques tooreceive à partir du Service de mise à jour de Windows.  Ce comportement ne change pas après l’ajout de cette solution ou un espace de travail de machines virtuelles Windows tooyour.  Si vous le faites pas activement gérés mises à jour avec cette solution, hello le comportement par défaut (appliquer automatiquement les mises à jour) s’applique.  

Pour les ordinateurs virtuels créés à partir de hello sur demande Red Hat Enterprise Linux (RHEL) images disponibles dans Azure Marketplace, ils sont inscrits tooaccess hello [Red Hat mise à jour Infrastructure (RHUI)](../virtual-machines/virtual-machines-linux-update-infrastructure-redhat.md) déployé dans Azure.  Les autres distributions Linux doivent être mis à jour à partir du référentiel de fichiers en ligne hello versions suivant leurs méthodes prises en charge.  

### <a name="viewing-update-deployments"></a>Affichage des déploiements de mises à jour
Cliquez sur hello **mise à jour de déploiement** vignette tooview hello liste des déploiements de mises à jour existantes.  Ces déploiements sont regroupés par état : **Planifié**, **Exécution en cours** et **Terminé**.<br><br> ![Page de planification des déploiements de mises à jour](./media/oms-solution-update-management/update-updatedeployment-schedule-page.png)<br>  

hello tableau suivant décrit les propriétés Hello affichées pour chaque déploiement de mises à jour.

| Propriété | Description |
| --- | --- |
| Nom |Nom de déploiement de mise à jour de hello. |
| Planification |Type de planification.  Les options disponibles sont *une fois*, *hebdomadaire récurrente*, ou *mensuelle récurrente*. |
| Heure de début |Date et heure auxquelles hello de déploiement de mise à jour est toostart planifiée. |
| Duration |Nombre de minutes hello déploiement de mise à jour est autorisée toorun.  Si les mises à jour ne sont pas installés dans ce délai, puis hello mises à jour restantes doive attendre hello déploiement de mises à jour suivant. |
| Serveurs |Nombre d’ordinateurs affectés par hello déploiement de mise à jour.  |
| État |État actuel de hello déploiement de mise à jour.<br><br>Les valeurs possibles sont les suivantes :<br>- Non commencé<br>- Exécution en cours<br>- Terminé |

Sélectionnez un terminé détail écran déploiement de mise à jour tooview hello qui inclut les colonnes hello Bonjour tableau suivant.  Ces colonnes ne seront pas être remplies si hello déploiement de mise à jour n’a pas encore démarrés.<br><br> ![Vue d’ensemble des résultats d’un déploiement de mises à jour](./media/oms-solution-update-management/update-management-deploymentresults-dashboard.png)

| Colonne | Description |
| --- | --- |
| **Vue des ordinateurs** | |
| Ordinateurs Windows |Affiche le numéro de hello des ordinateurs Windows hello déploiement de mise à jour par état.  Cliquez sur un état toorun une recherche de journal retournant que tous les mettre à jour les enregistrements avec cet état pour mettre à jour le déploiement de hello. |
| Ordinateurs Linux |Affiche le numéro de hello des ordinateurs Linux Bonjour déploiement de mise à jour par état.  Cliquez sur un état toorun une recherche de journal retournant que tous les mettre à jour les enregistrements avec cet état pour mettre à jour le déploiement de hello. |
| État de l’installation de l’ordinateur |Répertorie les ordinateurs hello impliqués dans hello déploiement de mise à jour et pourcentage de hello de mises à jour installées avec succès. Cliquez sur un hello entrées toorun une recherche de journal retournant les mises à jour critiques et manquants. |
| **Vue des mises à jour** | |
| Mises à jour Windows |Répertorie les mises à jour Windows inclus dans hello mettre à jour le déploiement et leur état d’installation par chaque mise à jour.  Sélectionnez une mise à jour toorun une recherche de journal renvoi de tous les mettre à jour des enregistrements pour cette mise à jour spécifique ou cliquez sur hello état toorun une recherche de journal retournant que tous les mettre à jour des enregistrements pour le déploiement de hello. |
| Mises à jour Linux |Répertorie les mises à jour de Linux incluses dans hello mettre à jour le déploiement et leur état d’installation par chaque mise à jour.  Sélectionnez une mise à jour toorun une recherche de journal renvoi de tous les mettre à jour des enregistrements pour cette mise à jour spécifique ou cliquez sur hello état toorun une recherche de journal retournant que tous les mettre à jour des enregistrements pour le déploiement de hello. |

### <a name="creating-an-update-deployment"></a>Création d’un déploiement de mises à jour
Créer un nouveau déploiement de mise à jour en cliquant sur hello **ajouter** bouton haut hello hello de tooopen écran hello **nouveau déploiement de mises à jour** page.  Vous devez fournir des valeurs pour les propriétés hello Bonjour tableau suivant.

| Propriété | Description |
| --- | --- |
| Nom |Déploiement de mises à jour tooidentify hello nom unique. |
| Time Zone (Fuseau horaire) |Toouse de fuseau horaire pour l’heure de début hello. |
| Type de planification | Type de planification.  Les options disponibles sont *une fois*, *hebdomadaire récurrente*, ou *mensuelle récurrente*.  
| Heure de début |Date et heure toostart hello déploiement mises à jour. **Remarque :** est de 30 minutes à partir de l’heure actuelle par le plus tôt hello pour un déploiement peut s’exécuter si vous avez besoin de toodeploy immédiatement. |
| Duration |Nombre de minutes hello déploiement de mise à jour est autorisée toorun.  Si les mises à jour ne sont pas installés dans ce délai, puis hello mises à jour restantes doive attendre hello déploiement de mises à jour suivant. |
| Ordinateurs |Noms d’ordinateurs ou ordinateur groupes tooinclude et cible Bonjour déploiement de mise à jour.  Sélectionnez une ou plusieurs entrées à partir de la liste déroulante hello. |

<br><br> ![Page Nouveau déploiement de mises à jour](./media/oms-solution-update-management/update-newupdaterun-page.png)

### <a name="time-range"></a>Période
Par défaut, hello étendue hello analysé dans hello solution de gestion de la mise à jour est à partir de tous les groupes d’administration connectés générés dans hello dernières 24 heures.

plage de temps hello toochange de données de hello, sélectionnez **les données basées sur** haut hello du tableau de bord hello. Vous pouvez sélectionner des enregistrements créés ou mis à jour dans hello 7 derniers jours, 1 jour, ou 6 heures. Vous pouvez également sélectionner **Personnalisé** et spécifier une plage de dates personnalisée.

## <a name="log-analytics-records"></a>Enregistrements Log Analytics
Hello solution de gestion de la mise à jour crée deux types d’enregistrements dans le référentiel d’OMS hello.

### <a name="update-records"></a>Enregistrements de mises à jour
Un enregistrement présentant le type **Update** est créé pour chaque mise à jour installée ou requise sur chaque ordinateur. Mise à jour les enregistrements ont des propriétés de hello Bonjour tableau suivant.

| Propriété | Description |
| --- | --- |
| Type |*Mettre à jour* |
| SourceSystem |source de Hello approuvé d’installation de mise à jour hello.<br>Les valeurs possibles sont les suivantes :<br>- Microsoft Update<br>- Windows Update<br>- SCCM<br>- Serveurs Linux (extraits des gestionnaires de packages) |
| Approved |Spécifie si la mise à jour hello a été approuvée pour l’installation.<br> Pour les serveurs Linux, cette opération est actuellement considérée comme facultative, car l’application de mises à jour corrective n’est pas gérée par OMS. |
| Classification for Windows |Classification de mise à jour hello.<br>Les valeurs possibles sont les suivantes :<br>-    Applications<br>- Mises à jour critiques<br>- Mises à jour de définitions<br>- Packs de fonctionnalités<br>- Mises à jour de sécurité<br>- Service Packs<br>- Correctifs cumulatifs<br>- Mises à jour |
| Classification for Linux |Cassification de mise à jour hello.<br>Les valeurs possibles sont les suivantes :<br>- Mises à jour critiques<br>- Mises à jour de sécurité<br>- Autres mises à jour |
| Ordinateur |Nom de l’ordinateur de hello. |
| InstallTimeAvailable |Spécifie si l’heure d’installation hello est disponible à partir d’autres agents installés hello même mettre à jour. |
| InstallTimePredictionSeconds |Estimation de la durée d’installation en secondes sur d’autres agents installés hello même mise à jour. |
| KBID |ID de l’article hello Ko qui décrit la mise à jour hello. |
| ManagementGroupName |Nom du groupe d’administration hello pour les agents SCOM.  Pour les autres agents, il s’agit d’AOI-<workspace ID>. |
| MSRCBulletinID |ID du bulletin de sécurité Microsoft hello décrivant la mise à jour hello. |
| MSRCSeverity |Niveau de gravité du bulletin de sécurité Microsoft hello.<br>Les valeurs possibles sont les suivantes :<br>- Critique<br>- Important<br>- Modéré |
| Facultatif |Spécifie si la mise à jour hello est facultatif. |
| Produit |Nom de la mise à jour hello hello est pour.  Cliquez sur **vue** article de hello tooopen dans un navigateur. |
| PackageSeverity |niveau de gravité Hello de vulnérabilité hello corrigée dans cette mise à jour, comme indiqué par les fournisseurs de distribution de Linux hello. |
| PublishDate |Date et heure auxquelles hello mise à jour a été installé. |
| RebootBehavior |Spécifie si les mises à jour hello force un redémarrage.<br>Les valeurs possibles sont les suivantes :<br>- canrequestreboot<br>- neverreboots |
| RevisionNumber |Numéro de révision de mise à jour hello. |
| SourceComputerId |GUID toouniquely identifier l’ordinateur de hello. |
| TimeGenerated |Date et heure auxquelles hello enregistrement a été modifié. |
| Intitulé |Titre de la mise à jour hello. |
| UpdateID |GUID toouniquely identifier la mise à jour hello. |
| UpdateState |Spécifie si la mise à jour hello est installé sur cet ordinateur.<br>Les valeurs possibles sont les suivantes :<br>-- Mise à jour hello est installé sur cet ordinateur.<br>-Nécessaire - mise à jour hello n’est pas installé et est requis sur cet ordinateur. |

Lorsque vous effectuez une recherche de journal qui retourne les enregistrements avec un type de **mise à jour** vous pouvez sélectionner hello **mises à jour** vue qui affiche un ensemble de vignettes de résumé des mises à jour hello retournées par la recherche de hello. Vous pouvez cliquer sur les entrées de hello Bonjour **manquant et mises à jour** et **mises à jour obligatoires et facultatifs** tooscope hello afficher toothat définir des mises à jour les vignettes. Sélectionnez hello **liste** ou **Table** consulter tooreturn hello des enregistrements.<br>

![Vue Mise à jour de la recherche de journal pour le type d’enregistrement Update](./media/oms-solution-update-management/update-la-view-updates.png)  

Bonjour **Table** vue, que vous pouvez cliquer sur hello **KBID** pour n’importe quel enregistrement tooopen un navigateur avec l’article hello Ko. Cela permet de vous tooquickly en savoir plus sur les détails de hello de mise à jour particulière de hello.<br>

![Vue Table de la recherche de journal incluant les mosaïques pour le type d’enregistrement Updates](./media/oms-solution-update-management/update-la-view-table.png)

Bonjour **liste** vue, vous cliquez sur hello **vue** lien toohello KBID tooopen hello Ko d’article suivant.<br>

![Vue Liste de la recherche de journal incluant les mosaïques pour le type d’enregistrement Mises à jour](./media/oms-solution-update-management/update-la-view-list.png)

### <a name="updatesummary-records"></a>Enregistrements UpdateSummary
Un enregistrement avec un type **UpdateSummary** est créé pour chaque ordinateur agent. Cet enregistrement est mis à jour chaque fois que hello ordinateur est analysé pour les mises à jour. **UpdateSummary** enregistrements ont les propriétés hello Bonjour tableau suivant.

| Propriété | Description |
| --- | --- |
| Type |UpdateSummary |
| SourceSystem |OpsManager |
| Ordinateur |Nom de l’ordinateur de hello. |
| CriticalUpdatesMissing |Nombre de mises à jour critiques manquants sur l’ordinateur de hello. |
| ManagementGroupName |Nom du groupe d’administration hello pour les agents SCOM. Pour les autres agents, il s’agit d’AOI-<workspace ID>. |
| NETRuntimeVersion |Version du runtime .NET de hello installé sur l’ordinateur de hello. |
| OldestMissingSecurityUpdateBucket |Compartiment toocategorize durée hello time depuis la publication de hello plus ancienne sécurité mise à jour manquante sur cet ordinateur.<br>Les valeurs possibles sont les suivantes :<br>- Antérieur<br>-    Il y a 180 jours<br>- Il y a 150 jours<br>-    Il y a 120 jours<br>- Il y a 90 jours<br>- Il y a 60 jours<br>-    Il y a 30 jours<br>-    Récent |
| OldestMissingSecurityUpdateInDays |Nombre de jours depuis la publication de hello plus ancienne sécurité mise à jour manquante sur cet ordinateur. |
| OsVersion |Version du système d’exploitation de hello installé sur l’ordinateur de hello. |
| OtherUpdatesMissing |Nombre d’autres mises à jour manquantes sur un ordinateur de hello. |
| SecurityUpdatesMissing |Nombre de mises à jour de sécurité manquantes sur l’ordinateur de hello. |
| SourceComputerId |GUID toouniquely identifier l’ordinateur de hello. |
| TimeGenerated |Date et heure auxquelles hello enregistrement a été modifié. |
| TotalUpdatesMissing |Nombre total de mises à jour absentes sur l’ordinateur de hello. |
| WindowsUpdateAgentVersion |Numéro de version de l’agent de mise à jour de Windows hello sur l’ordinateur de hello. |
| WindowsUpdateSetting |Paramètre de la façon dont les ordinateur hello va installer les mises à jour importantes.<br>Les valeurs possibles sont les suivantes :<br>- Désactivé<br>- Notify before installation (Notifier avant l’installation)<br>- Scheduled installation (Installation planifiée) |
| WSUSServer |URL de WSUS le serveur si hello ordinateur est configuré toouse une. |

## <a name="sample-log-searches"></a>Exemples de recherches dans les journaux
Hello tableau suivant fournit des exemples des recherches de journaux pour les enregistrements de mise à jour collectées par cette solution.

| Interroger | Description |
| --- | --- |
| Type:Update OSType!=Linux UpdateState=Needed Optional=false Approved!=false &#124; measure count() by Computer |Ordinateurs serveur Windows nécessitant des mises à jour |
| Type:Update OSType=Linux UpdateState!="Not needed" &#124; measure count() by Computer |Serveurs Linux nécessitant des mises à jour | 
| Type=Update UpdateState=Needed Optional=false &#124; select Computer,Title,KBID,Classification,UpdateSeverity,PublishedDate |Ensemble des ordinateurs avec des mises à jour manquantes |
| Type=Update UpdateState=Needed Optional=false Computer="ORDINATEUR01.contoso.com" &#124; select Computer,Title,KBID,Product,UpdateSeverity,PublishedDate |Mises à jour manquantes pour un ordinateur spécifique (remplacer la valeur par le nom de votre ordinateur)|
| Type=Update UpdateState=Needed Optional=false (Classification="Mises à jour de sécurité" OR Classification="Mises à jour critiques") |Ensemble des ordinateurs avec des mises à jour critiques ou de sécurité manquantes | 
| Type=Update UpdateState=Needed Optional=false (Classification="Mises à jour de sécurité" OR Classification="Mises à jour critiques") Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual &#124; Distinct Computer} &#124; Distinct KBID |Mises à jour critiques ou de sécurité nécessaires sur les machines où des mises à jour ont été appliquées manuellement |
| Type=Event EventLevelName=error Computer IN {Type=Update (Classification="Mises à jour critiques" OR Classification="Mises à jour critiques") UpdateState=Needed Optional=false &#124; Distinct Computer} |Événements d’erreur pour les machines où des mises à jour critiques ou de sécurité obligatoires sont manquantes |
| Type=Update Optional=false Classification="Correctifs cumulatifs" UpdateState=Needed &#124; select Computer,Title,KBID,Classification,UpdateSeverity,PublishedDate |Ensemble des ordinateurs avec des correctifs cumulatifs | 
| Type=Update UpdateState=Needed Optional=false &#124; Distinct Title |Mises à jour manquantes distinctes sur tous les ordinateurs | 
| Type:UpdateRunProgress InstallationStatus=failed &#124; measure count() by Computer, Title, UpdateRunName |Ordinateur serveur Windows avec des mises à jour ayant échoué pendant l’exécution d’une mise à jour | 
| Type:UpdateRunProgress InstallationStatus=failed &#124; measure count() by Computer, Product, UpdateRunName |Serveur Linux avec des mises à jour ayant échoué pendant l’exécution d’une mise à jour | 
| Type=UpdateSummary &#124; measure count() by WSUSServer |Appartenance des ordinateurs WSUS | 
| Type=UpdateSummary &#124; measure count() by WindowsUpdateSetting |Configuration de la mise à jour automatique | 
| Type=UpdateSummary WindowsUpdateSetting=Manual |Ordinateurs où la mise à jour automatique est désactivée | 
| Type=Update and OSType=Linux and UpdateState!="Non requis" &#124; measure count() by Computer |Liste de tous les ordinateurs de Linux hello ayant une mise à jour du package | 
| Type=Update and OSType=Linux and UpdateState!="Non requis" and (Classification="Mises à jour critiques" OR Classification="Mises à jour de sécurité") &#124; measure count() by Computer |Liste de tous les ordinateurs de Linux hello ayant une mise à jour du package qui résout une vulnérabilité de sécurité ou critique | 
| Type=Update and OSType=Linux and UpdateState!="Non requis" |Liste de tous les packages pour lesquels une mise à jour est disponible | 
| Type=Update  and OSType=Linux and UpdateState!="Non requis" and (Classification="Mises à jour critiques" OR Classification="Mises à jour de sécurité") |Liste de tous les packages pour lesquels une mise à jour de package corrigeant une vulnérabilité critique ou de sécurité est disponible | 
| Type:UpdateRunProgress &#124; measure Count() by UpdateRunName |Répertorier les déploiements de mises à jour ayant modifié des ordinateurs | 
| Type:UpdateRunProgress UpdateRunName="DeploymentName" &#124; measure Count() by Computer |Ordinateurs mis à jour dans cette mise à jour (remplacer la valeur par le nom de votre déploiement de mises à jour) | 
| Type=Update and OSType=Linux and OSName = Ubuntu &#124; measure count() by Computer |Liste de tous les ordinateurs de « Ubuntu » hello toute mise à jour disponibles | 

## <a name="troubleshooting"></a>Résolution des problèmes

Cette section fournit des informations toohelp résoudre les problèmes de hello solution de gestion de la mise à jour.  

### <a name="how-do-i-troubleshoot-onboarding-issues"></a>Comment puis-je résoudre les problèmes d’intégration ?
Si vous rencontrez des problèmes lors de la solution de hello tooonboard ou d’un ordinateur virtuel, vérifiez hello **Application et le Gestionnaire des Services Logs\Operations** journal des événements pour les événements avec le message d’événement 4502 d’ID et les événements contenant **Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent**.  Hello tableau suivant met en évidence les messages d’erreur et une résolution possible pour chacun.  

| Message | Motif | Solution |   
|----------|----------|----------|  
| Impossible de tooRegister ordinateur pour la gestion des correctifs<br>Registration Failed with Exception<br>System.InvalidOperationException: {"Message":"Machine is already<br>inscrit tooa autre compte. "} (Impossible d’inscrire la machine pour la gestion des correctifs, l’inscription a échoué avec l’exception System.InvalidOperationException : {"Message" :"La machine est déjà inscrite sur un autre compte."} | Ordinateur est déjà embarquées tooanother espace de travail pour la gestion de la mise à jour | Effectuer un nettoyage des artefacts de l’ancien par [la suppression du groupe de runbook hybride hello](../automation/automation-hybrid-runbook-worker.md#remove-hybrid-worker-groups)|  
| Impossible d’inscrire trop ordinateur pour la gestion des correctifs<br>Registration Failed with Exception<br>System.Net.Http.HttpRequestException : Une erreur s’est produite lors de l’envoi de demande de hello. ---><br>System.Net.WebException : connexion sous-jacente hello<br>was closed: An unexpected error<br>occurred on a receive. ---> System.ComponentModel.Win32Exception:<br>hello client et serveur ne peut pas communiquer,<br>because they do not possess a common algorithm (Impossible d’inscrire la machine pour la gestion des correctifs, l’inscription a échoué avec l’exception System.Net.Http.HttpRequestException : une erreur s’est produite lors de l’envoi de la requête. --->System.Net.WebException : la connexion sous-jacente était fermée : une erreur inattendue s’est produite à la réception. ---> System.ComponentModel.Win32Exception : le client et le serveur ne peuvent pas communiquer car ils n’ont pas d’algorithme en commun) | Proxy/passerelle/pare-feu bloquant la communication | [Passez en revue la configuration requise pour le réseau](../automation/automation-offering-get-started.md#network-planning)|  
| Impossible de tooRegister ordinateur pour la gestion des correctifs<br>Registration Failed with Exception<br>Newtonsoft.Json.JsonReaderException: Error parsing positive infinity value. (Impossible d’inscrire la machine pour la gestion des correctifs, l’inscription a échoué avec l’exception Newtonsoft.Json.JsonReaderException : erreur d’analyse de valeur infinie positive.) | Proxy/passerelle/pare-feu bloquant la communication | [Passez en revue la configuration requise pour le réseau](../automation/automation-offering-get-started.md#network-planning)| 
| certificat Hello présenté par le service de hello <wsid>. oms.opinsights.azure.com<br>was not issued by a certificate authority<br>used for Microsoft services. Please contact<br>votre toosee d’administrateur réseau s’ils exécutent un proxy qui intercepte<br>TLS/SSL communication. (Le certificat présenté par le service .oms.opinsights.azure.com n’a pas été émis par une autorité de certification utilisée par les services Microsoft. Veuillez contacter votre administrateur réseau pour déterminer si un proxy en cours d’exécution intercepte la communication TLS/SSL.) |Proxy/passerelle/pare-feu bloquant la communication | [Passez en revue la configuration requise pour le réseau](../automation/automation-offering-get-started.md#network-planning)|  
| Impossible de tooRegister ordinateur pour la gestion des correctifs<br>Registration Failed with Exception<br>AgentService.HybridRegistration.<br>PowerShell.Certificates.CertificateCreationException:<br>Échec de toocreate un certificat auto-signé. ---><br>System.UnauthorizedAccessException: Access is denied. (Impossible d’inscrire la machine pour la gestion des correctifs, l’inscription a échoué avec l’exception AgentService.HybridRegistration. PowerShell.Certificates.CertificateCreationException : échec de la création d’un certificat auto-signé. --->System.UnauthorizedAccessException : accès refusé.) | Échec de génération du certificat auto-signé | Vérifiez que le compte système a<br>accès en lecture toofolder :<br>**C:\ProgramData\Microsoft\**<br>**Crypto\RSA**|  

### <a name="how-do-i-troubleshoot-update-deployments"></a>Comment résoudre les déploiements de mises à jour ?
Vous pouvez afficher les résultats de hello du runbook hello responsable du déploiement des mises à jour hello inclus dans le déploiement de mises à jour hello planifiée à partir du Panneau de travaux hello de votre compte Automation qui est lié à l’espace de travail OMS hello prenant en charge cette solution.  Hello runbook **MicrosoftOMSComputer-correctif** est un runbook enfant qui cible un ordinateur géré spécifique, et consulter les flux détaillé hello présente des informations détaillées pour ce déploiement.  sortie de Hello s’afficher qui nécessaires mises à jour sont applicables, télécharger l’état, l’état de l’installation et des détails supplémentaires.<br><br> ![Statut de tâche du déploiement de mises à jour](media/oms-solution-update-management/update-la-patchrunbook-outputstream.png)<br>

Pour plus d’informations, consultez [Sortie et messages de runbook Automation](../automation/automation-runbook-output-and-messages.md).   

## <a name="next-steps"></a>Étapes suivantes
* Utiliser des recherches de journaux dans [Analytique de journal](../log-analytics/log-analytics-log-searches.md) tooview détaillé les données de mise à jour.
* [Créez vos propres tableaux de bord](../log-analytics/log-analytics-dashboards.md) affichant la conformité des mises à jour de vos ordinateurs gérés.
* [Créez des alertes](../log-analytics/log-analytics-alerts.md) lorsque des mises à jour critiques sont détectées comme manquantes sur des ordinateurs ou lorsque les mises à jour automatiques sont désactivées sur un ordinateur.  
