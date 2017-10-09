---
title: "aaaGetting main Operations Management Suite de Solution de sécurité et d’Audit | Documents Microsoft"
description: "Vous aide à ce document vous tooget main toomonitor de fonctionnalités de solution Operations Management Suite de sécurité et d’Audit de votre cloud hybride."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 754796ef-a43e-468a-86c9-04a2eda55b5b
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: get-started-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 5cb3e5dbb3e60f9702a34c9413ddc1bf2b14b411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-operations-management-suite-security-and-audit-solution"></a>Prise en main de la solution de sécurité et d’audit d’Operations Management Suite
Ce document vous aide à prendre rapidement en main les fonctionnalités de la solution de sécurité et d’audit d’Operations Management Suite (OMS), en vous présentant chaque option.

## <a name="what-is-oms"></a>Qu’est-ce qu’OMS ?
Microsoft Operations Management Suite (OMS) est une solution de gestion informatique de Microsoft qui vous permet de gérer et de protéger votre infrastructure locale et de cloud. Pour plus d’informations sur OMS, consultez l’article de la hello [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

## <a name="oms-security-and-audit-dashboard"></a>Tableau de bord de la solution de sécurité et d’audit d’OMS
Hello solution OMS sécurité et Audit fournit une vue globale de votre organisation posture de sécurité informatique avec des requêtes de recherche intégrées pour détecter les problèmes importants qui requièrent votre attention. Hello **sécurité et Audit** tableau de bord est l’écran d’accueil hello pour tous les éléments liés toosecurity d’OMS. Il fournit un aperçu de haut niveau dans l’état de sécurité hello de vos ordinateurs. Il inclut également hello capacité tooview tous les événements de hello dernières 24 heures, 7 jours, ou n’importe quel autre intervalle de temps personnalisé. tooaccess hello **sécurité et Audit** tableau de bord, procédez comme suit :

1. Bonjour **Microsoft Operations Management Suite** cliquez sur le tableau de bord principal **paramètres** vignette dans hello gauche.
2. Bonjour **paramètres** panneau, sous **Solutions** cliquez sur **sécurité et Audit** option.
3. Hello **sécurité et Audit** tableau de bord s’affiche :
   
    ![Tableau de bord de la solution de sécurité et d’audit d’OMS](./media/oms-security-getting-started/oms-getting-started-fig1-ga.png)

Si vous accédez à ce tableau de bord pour hello première fois et que vous n’avez pas les périphériques analysés par OMS, hello vignettes ne seront pas remplies avec les données obtenues à partir de l’agent de hello. Une fois que vous installez l’agent de hello, il peut prendre quelques toopopulate de temps, par conséquent ce que vous voyez initialement manque peut-être des données qu’ils téléchargent toujours toohello cloud.  Dans ce cas, il est normal toosee certaines vignettes sans informations tangibles. Lecture [connecter des ordinateurs Windows directement tooOMS](https://technet.microsoft.com/library/mt484108.aspx) pour plus d’informations sur la façon de l’agent OMS de tooinstall dans un système Windows et [tooOMS des ordinateurs Linux de se connecter](https://technet.microsoft.com/library/mt622052.aspx) pour plus d’informations sur la façon de tooperform cette tâche dans le système Linux.

> [!NOTE]
> l’agent de Hello collecte des informations de hello basées sur hello actuel des événements qui sont activés, par exemple le nom de l’ordinateur, nom d’utilisateur et d’adresse IP. Toutefois, aucun document/fichier, aucun nom de base de données ni aucune donnée privée ne sont collectés.   
> 
> 

Les solutions sont un ensemble de règles de logique, de visualisation et d’acquisition des données qui répondent aux principaux problèmes que rencontrent les clients. Sécurité et audit est une solution ; d’autres peuvent être ajoutées séparément. Lire l’article de hello [ajouter des solutions](https://technet.microsoft.com/library/mt674635.aspx) pour plus d’informations sur la façon de tooadd une nouvelle solution.

tableau de bord OMS sécurité et Audit Hello est organisé en quatre catégories principales :

* **Domaines de sécurité**: dans cette zone, vous serez en mesure de toofurther Explorer les enregistrements de sécurité au fil du temps, accéder l’évaluation des logiciels malveillants, mettre à jour d’évaluation, la sécurité du réseau, informations d’identité et accès, les ordinateurs avec des événements de sécurité et rapidement tableau de bord du centre de sécurité de tooAzure accès.
* **Problèmes importants**: cette option vous permettra de tooquickly identifier le numéro de hello de problèmes actifs et hello gravité de ces problèmes.
* **Détections (version préliminaire)**: vous permet de modèles d’attaque tooidentify en affichant les alertes de sécurité qu’elles ont lieu par rapport à vos ressources.
* **La menace d’Intelligence**: vous permet de modèles d’attaque tooidentify en affichant le nombre total de hello de serveurs avec le trafic malveillant IP sortant, type de menace nuisible hello et une carte qui montre la provenance des ces adresses IP. 
* **Requêtes de sécurité courantes**: cette option permet de vous une liste de sécurité les plus courantes hello des requêtes que vous pouvez utiliser toomonitor votre environnement. Lorsque vous cliquez sur une de ces requêtes, il s’ouvre hello **recherche** panneau avec les résultats hello pour cette requête.

> [!NOTE]
> pour en savoir plus sur la manière dont OMS conserve vos données sécurisées, lisez How OMS secures your data (Comment OMS sécurise vos données).
> 
> 

## <a name="security-domains"></a>Security domains (Domaines de sécurité)
Lors de l’analyse des ressources, il est important toobe tooquickly en mesure d’accès hello état actuel de votre environnement. Toutefois il est également important toobe tootrack en mesure de retour les événements qui se sont produites dans hello dernier pouvant conduire tooa mieux comprendre ce qui se passe dans votre environnement à certain point dans le temps. 

> [!NOTE]
> rétention des données est selon le plan de tarification toohello OMS. Pour plus d’informations, visitez hello [Microsoft Operations Management Suite](https://www.microsoft.com/server-cloud/operations-management-suite/pricing.aspx) page de tarification.
> 
> 

Scénarios d’enquête légales et de réponse aux incidents bénéficieront directement à partir des résultats hello disponibles dans hello **au fil du temps, les enregistrements de sécurité** vignette.

![Enregistrements de sécurité au fil du temps](./media/oms-security-getting-started/oms-getting-started-fig2.JPG)

Lorsque vous cliquez sur cette vignette, hello **recherche** panneau s’ouvre, affichant les résultats d’une requête pour **les événements de sécurité** (Type = SecurityEvents) selon hello des sept derniers jours, comme indiqué ci-dessous :

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Enregistrements de sécurité au fil du temps](./media/oms-security-getting-started/oms-getting-started-fig3.JPG)

résultat de recherche Hello est divisé en deux volets : volet de gauche hello vous donne une répartition du nombre de hello des événements de sécurité qui ont été trouvés, ordinateurs hello dans lequel ces événements ont été trouvés, nombre de hello de comptes qui ont été détectés dans ces ordinateurs et les types de hello de activités. volet de droite Hello vous fournit les résultats total hello et un affichage chronologique hello des événements de sécurité avec l’activité de nom et de l’ordinateur hello. Vous pouvez également cliquer sur **afficher plus** tooview plus d’informations sur cet événement, telles que les données d’événement hello, ID d’événement hello et source d’événement hello.

> [!NOTE]
> Pour plus d’informations sur la requête de recherche OMS, consultez [OMS search reference](https://technet.microsoft.com/library/mt450427.aspx)(Référence de recherche OMS).
> 
> 

### <a name="antimalware-assessment"></a>Analyse anti-programme malveillant
Cela permet d’option tooquickly vous identifiez les ordinateurs avec une protection insuffisante et les ordinateurs qui ont été compromis par un programme malveillant. Évaluation des logiciels malveillants état et les menaces détectées sur les serveurs hello analysé sont lues et hello puis les données est envoyée service OMS de toohello dans le cloud hello pour le traitement. Serveurs avec menaces détectées et une protection insuffisante figurent dans hello contre les programmes malveillants évaluation du tableau de bord, qui est accessible après avoir cliqué sur Bonjour **évaluation du logiciel anti-programme malveillant** vignette. 

![évaluation des programmes malveillants](./media/oms-security-getting-started/oms-getting-started-fig4-ga.png)

Tout comme n’importe quel autre vignette dynamique disponible dans le tableau de bord OMS, lorsque vous cliquez dessus, hello **recherche** panneau s’ouvre avec le résultat de la requête hello. Pour cette option, si vous cliquez dans hello **Reporting pas** sous **état de la Protection**, vous aurez le résultat de la requête hello qui illustre cette entrée unique qui contient le nom de l’ordinateur hello et son rang, en tant que Vous trouverez ci-dessous :

![résultat de la recherche](./media/oms-security-getting-started/oms-getting-started-fig5.png)

> [!NOTE]
> *rang* est une notation donnant l’état de hello tooreflect de protection de hello (on, off, mis à jour, etc.) et les menaces qui sont trouvent. Ayant pour que les agrégations de toomake vous aide à un nombre.
> 
> 

Si vous cliquez dans le nom de l’ordinateur hello, vous aurez affichage chronologique de hello du statut de protection hello pour cet ordinateur. Cela est très utile pour les scénarios dans lesquels vous devez toounderstand si hello contre les logiciels malveillants a été installé qu’une seule fois et à un moment donné, il a été supprimé.   

### <a name="update-assessment"></a>Update assessment (Évaluation des mises à jour)
Cela permet d’option vous tooquickly déterminer hello problèmes de sécurité toopotential exposition globale et si ou l’importance de ces mises à jour sont pour votre environnement. OMS solution de sécurité et d’Audit uniquement fournissent visualisation hello de ces mises à jour, les données réelles hello vient de [Solutions de gestion des mises à jour](oms-solution-update-management.md), qui est un module différent dans OMS. Voici un exemple de mises à jour hello :

![mises à jour du système](./media/oms-security-getting-started/oms-getting-started-fig6-new.png)

> [!NOTE]
> Pour plus d’informations sur la solution Update Management, voir [solution Update Management dans OMS](oms-solution-update-management.md).
> 
> 

### <a name="identity-and-access"></a>Identité et accès
L’identité doit être le contrôle de hello plan pour votre entreprise, la protection de votre identité doit être votre priorité. Bien que Bonjour précédentes ont été périmètre autour des organisations et ces périmètre ont été une des limites de défense principal hello, aujourd'hui avec davantage de données et des applications plus déplacement toohello cloud identité de hello devient périmètre de nouveau hello. 

> [!NOTE]
> actuellement les données hello sont basées uniquement sur les données de connexion d’événements de sécurité (événement ID 4624) dans les connexions d’Office 365 futures hello et données Azure Active Directory sera également incluses.
> 
> 

En surveillant vos activités d’identité, vous serez proactives en mesure de tootake avant un incident prend place ou actions réactives toostop une tentative d’attaque. Hello **identité et accès** tableau de bord vous fournit une vue d’ensemble de l’état de votre identité, notamment le numéro de hello de toolog de tentatives ayant échoué sur compte d’utilisateur hello qui ont été utilisés lors de ces tentatives, les comptes qui ont été verrouillés comptes avec modifier ou réinitialiser un mot de passe et, actuellement, le nombre de comptes qui sont enregistrés dans. 

Lorsque vous cliquez sur Bonjour **identité et accès** vignette hello suivant du tableau de bord s’affiche :

![identité et accès](./media/oms-security-getting-started/oms-getting-started-fig7-ga.png)

informations de Hello disponibles dans ce tableau de bord peuvent aider immédiatement tooidentify une activité suspecte potentielle. Par exemple, il n’y 338 tentatives toolog sur comme **administrateur** et 100 % de ces tentatives a échoué. Ce compte a peut-être été l’objet d’une attaque en force brute. Si vous cliquez sur ce compte vous obtiendrez plus d’informations qui peuvent vous aider ressource de cible toodetermine hello pour ce type d’attaque potentiel :

![Recherche de résultats](./media/oms-security-getting-started/oms-getting-started-fig8.JPG)

rapport détaillé Hello fournit des informations sur cet événement, y compris : ordinateur cible de hello, de type hello d’ouverture de session (dans ce cas de connexion réseau), l’activité hello (dans ce cas cas 4625) et d’une chronologie complète de chaque nouvelle tentative. 

### <a name="computers"></a>Ordinateurs
Cette vignette peut être utilisé tooaccess tous les ordinateurs qui ont activement les événements de sécurité. Lorsque vous cliquez dans cette vignette vous verrez la liste de hello des ordinateurs avec des événements de sécurité et de nombre hello d’événements sur chaque ordinateur :

![Ordinateurs](./media/oms-security-getting-started/oms-getting-started-fig9.JPG)

Vous pouvez continuer votre examen en cliquant sur chaque ordinateur et passez en revue les événements de sécurité hello qui ont été signalés.

### <a name="threat-intelligence"></a>Informations sur les menaces

À l’aide d’option d’informations sur les menaces hello disponible dans OMS sécurité et Audit, les administrateurs informatiques peuvent identifier les menaces de sécurité sur l’environnement de hello, par exemple, identifier si un ordinateur particulier fait partie d’un botnet. Les ordinateurs peuvent devenir des nœuds dans un botnet lorsque des personnes malveillantes installer de manière illicite contre les programmes malveillants qui secrètement se connecte cette commande toohello d’ordinateur et le contrôle. Cette option peut également identifier les menaces potentielles provenant de canaux de communication obscurs, tel que le Darknet. En savoir plus sur les menaces en lisant [toosecurity de surveillance et de réponse des alertes dans Operations Management Suite de Solution de sécurité et d’Audit](oms-security-responding-alerts.md) l’article.

Dans certains scénarios, vous pouvez remarquer qu’un ordinateur surveillé a accédé à une adresse IP potentiellement malveillante :

![carte d’informations sur les menaces](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

Cette alerte et autres dans hello même catégorie, sont générés via la sécurité d’OMS en tirant parti [Microsoft Threat Intelligence](https://youtu.be/O4WtxgUrDc8). Hello les données sur les menaces recueillie par Microsoft ainsi que les acheté fournisseurs threat intelligence. Ces données sont fréquemment mis à jour et adapter le déplacement de toofast des menaces. En raison de la nature de tooits, il doit être combiné avec d’autres sources d’informations de sécurité lors de la [examen](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) une alerte de sécurité. 

### <a name="baseline-assessment"></a>Évaluation de la ligne de base

Avec de nombreuses organisations gouvernementales et entreprises du secteur, Microsoft définit une configuration Windows qui représente des déploiements de serveur hautement sécurisés. Cette configuration regroupe un ensemble de clés de Registre, de paramètres de stratégie d’audit et de paramètres de stratégie de sécurité, ainsi que les valeurs recommandées par Microsoft pour ces paramètres. Cet ensemble de règles est appelé « base de référence de la sécurité ». Pour plus d’informations sur cette option, lire [Évaluation de la base de référence dans la solution de sécurité et d’audit d’Operations Management Suite](oms-security-baseline.md).

### <a name="azure-security-center"></a>Azure Security Center
Cette vignette est essentiellement un tableau de bord du centre de sécurité Azure tooaccess contextuel. Pour en savoir plus sur cette solution, consultez [Prise en main du Centre de sécurité Azure](../security-center/security-center-get-started.md) .

## <a name="notable-issues"></a>Notable issues (Problèmes importants)
Hello principal objectif de ce groupe d’options est tooprovide un aperçu rapide des problèmes de hello que vous avez dans votre environnement, en les classant dans critique, avertissement et information. Hello vignette de type de problème actif il s’agit d’une visualisation de ces problèmes, mais il ne vous permet pas tooexplore plus des détails les concernant, pour ce faire, vous devez partie inférieure de hello toouse de cette vignette ayant nom hello du problème de hello (nom), le nombre d’objets avait cela se produire (nombre) et combien il est important (gravité).

![Notable issues (Problèmes importants)](./media/oms-security-getting-started/oms-getting-started-fig10.JPG)

Vous pouvez voir que ces problèmes ont été déjà traités dans différentes zones de hello **domaines de sécurité** groupe, ce qui renforce l’intention de hello de cette vue : visualiser hello plus importants dans votre environnement à partir d’un emplacement unique.

## <a name="detections-preview"></a>Détections (préversion)
Hello principal objectif de cette option est tooallow informatique tooquickly identifier l’environnement de tootheir les menaces potentielles via et gravité hello de cette menace.

![Informations sur les menaces](./media/oms-security-getting-started/oms-getting-started-fig12.png)

Cette option peut également être utilisée pendant un [enquête de réponse aux incidents](https://blogs.msdn.microsoft.com/azuresecurity/2016/11/30/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) tooperform hello évaluation et obtenir plus d’informations sur les attaques hello.

> [!NOTE]
> Pour plus d’informations sur la façon de toouse OMS pour la réponse aux incidents, regardez cette vidéo : [comment tooLeverage hello Azure Security Center & Microsoft Operations Management Suite pour une réponse aux incidents](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703).
> 
> 

## <a name="threat-intelligence"></a>Informations sur les menaces
Hello menace pour la nouvelle section intelligence de la solution de sécurité et Audit hello visualise les modèles d’attaque hello de plusieurs façons : hello nombre total de serveurs avec trafic sortant d’IP malveillant, hello du type de menace nuisible et un mappage qui indique où ces adresses IP proviennent. Vous pouvez interagir avec hello carte et cliquez sur hello IPs pour plus d’informations.

Jaunes clics-infos sur la carte de hello indiquent le trafic entrant à partir d’adresses IP malveillantes. Il n’est pas rare pour les serveurs qui sont exposés toohello internet toosee malveillant le trafic entrant, mais nous vous recommandons de consulter ces toomake de tentatives qu’aucune d'entre elles a réussi. Ces indicateurs sont basés sur les journaux IIS, WireData et les journaux du pare-feu Windows.  

![Informations sur les menaces](./media/oms-security-getting-started/oms-getting-started-fig11-ga.png)

## <a name="common-security-queries"></a>Common security queries
liste Hello de requêtes courantes de sécurité disponibles permettre être utiles pour vous toorapidly accès aux informations sur la ressource et personnaliser en fonction des besoins de votre environnement. Ces requêtes courantes sont les suivantes :

* Toutes les activités de sécurité
* Activités de sécurité sur hello ordinateur « ordinateur01.contoso.com » (à remplacer par le nom de votre ordinateur)
* Activités de sécurité sur hello ordinateur « ordinateur01.contoso.com » pour le compte « Administrateur » (à remplacer par vos propres noms d’ordinateur et de compte)
* Activité de connexion par ordinateur
* Comptes ayant arrêté le logiciel anti-programmes malveillants de Microsoft sur n’importe quel ordinateur
* Ordinateurs où hello processus Microsoft antimalware a été arrêté
* Les ordinateurs où la commande « hash.exe » a été exécutée (remplacez par d’autres noms de processus)
* Tous les noms de processus qui ont été exécutés
* Activité de connexion par compte
* Comptes qui connectés à distance sur hello ordinateur « ordinateur01.contoso.com » (à remplacer par le nom de votre ordinateur)

## <a name="see-also"></a>Voir aussi
Dans ce document, vous ont été introduites tooOMS solution de sécurité et d’Audit. toolearn en savoir plus sur la sécurité d’OMS, consultez hello suivant des articles :

* [Présentation - Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Surveillance et réponse tooSecurity alertes Operations Management Suite de Solution de sécurité et d’Audit](oms-security-responding-alerts.md)
* [Surveillance des ressources dans la solution de sécurité et d’audit d’Operations Management Suite](oms-security-monitoring-resources.md)

