---
title: "Évaluation de la ligne de base dans Operations Management Suite de sécurité et de la ligne de base de la Solution d’Audit d’aaaWeb | Documents Microsoft"
description: "Ce document explique comment toouse web évaluation de la ligne de base dans OMS sécurité et Audit solution tooperform une évaluation de la ligne de base de tous les serveurs web analysés fins de conformité et sécurité."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: yurid
ms.openlocfilehash: dafa9d3d93fae31748306b60ee40b285dd59c802
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Évaluation de la base de référence web dans la solution de sécurité et d’audit d’Operations Management Suite
Ce document vous aide à utiliser OMS sécurité et Audit web planifié évaluation fonctionnalités tooaccess hello état de sécurisation de vos ressources analysés.

## <a name="what-is-web-baseline-assessment"></a>Qu’est-ce qu’une évaluation de la base de référence web ?
La solution de sécurité d’OMS permet actuellement d’évaluer la base de référence de sécurité pour les systèmes d’exploitation. Il analyse les paramètres de système d’exploitation hello de vos serveurs toutes les 24 heures et fournit un affichage des paramètres potentiellement vulnérables. Pour plus d’informations à ce sujet, consultez [Évaluation de la base de référence dans la solution de sécurité et d’audit d’Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/oms-security-baseline).

Hello hello évaluation de la ligne de base de Web vise toofind les paramètres de serveur web potentiellement vulnérables. Hello trois sources principales pour les configurations de base hello web sont : configuration .NET, ASP.NET et IIS.  Simplement comme hello évaluation de ligne de base du système d’exploitation, sécurité OMS va tooscan votre chaque 24 heures des serveurs web et fournissent une vue à l’état de sécurité d’eux.  Dans les services Internet (IIS), la configurations sont hautement personnalisables, et qui permet à différents toobe niveaux de site et l’application remplacée. le scanneur Hello vérifie les paramètres de hello à chaque niveau de site/application de niveau racine d’addition toohello par défaut. Cela vous permet de tooidentify des paramètres potentiellement vulnérables et corriger rapidement, ainsi que nos recommandations pour ces paramètres.

>[!NOTE] 
>Vous pouvez télécharger des identificateurs de Configuration courantes hello et les règles de ligne de base utilisées par OMS sécurité dans ce [page](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335?redir=0).


## <a name="web-security-baseline-assessment"></a>Évaluation de la base de référence de la sécurité web

Fonctionnalité de hello accessibles via hello option de recherche d’OMS et hello sécurité OMS et tableau de bord d’Audit pour cette version préliminaire. Suivez les étapes de hello sous requête hello affecté de tooperform :

1. Bonjour **Microsoft Operations Management Suite** dans le tableau de bord principal, cliquez sur **sécurité et Audit** vignette.
2. Bonjour **sécurité et Audit** tableau de bord, vous pouvez voir hello Web de ligne de base du point de vue suivant toohello du système d’exploitation de ligne de base du point de vue.
   
    ![Évaluation de la base de référence de la sécurité web de la solution de sécurité et d’audit d’OMS](./media/oms-security-web-baseline/oms-security-web-baseline-fig5.png)

3. volet de gauche de Hello affiche le nombre de hello de serveurs Web comparé toohello de ligne de base, pourcentage moyen de hello de règles passé sur tous les serveurs hello évaluée et liste hello des serveurs qui ont été évaluées.
4. Hello droite répertorie hello unique des règles qui ont échoué par *gravité*, et *TypeRègle*. Vous pouvez afficher les détails de hello de cette règle en cliquant sur une des règles du volet droit hello. Un exemple est illustré hello sous l’image. règle de Hello est évaluée est répertorié sous *paramètre de la règle*. Hello *AzId* champ qui est un identificateur unique pour chaque règle utilisée par Microsoft pour le suivi des règles de ligne de base hello. En outre toothat utilisateurs peuvent voir hello *résultat attendu* (valeur de recommandée par Microsoft), et d’autres détails concernant l’impact sur la sécurité de la règle de hello hello.
    
    ![Interroger](./media/oms-security-web-baseline/oms-security-web-baseline-fig6.png)

5. Vous pouvez créer vos propres requêtes de résultats de hello tooreview. 

Hello première requête que vous pouvez utiliser est hello **résumé de l’évaluation de ligne de base Web**. Bonjour **rechercher ici** , tapez cette requête : *Type = SecurityBaselineSummary BaselineType = Web*. Hello Voici un exemple de sortie :

![Résultat de la requête](./media/oms-security-web-baseline/oms-security-web-baseline-fig7.png)

>[!NOTE] 
>Dans cette requête, chaque enregistrement indique un récapitulatif de l’évaluation sur un serveur donné.

Une fois que vous êtes dans hello **recherche de journal**, vous pouvez taper des requêtes différentes tooobtain plus d’informations sur l’évaluation de ligne de base hello web. En outre toohello de requête précédente, vous pouvez également utiliser hello celles dans cette version préliminaire suivant :

**Évaluation de la règle de base de référence web** : chaque enregistrement représente une seule évaluation de la règle de base de référence web sur un seul serveur. Il inclut toutes les données pour une règle d’échec, hello *SitePath* sur le hello règle a été évaluée, hello *résultat attendu*et hello *résultat réel*.

Requête : *Type=SecurityBaseline BaselineType=Web AnalyzeResult=Failed*

![Résultat de la requête 2](./media/oms-security-web-baseline/oms-security-web-baseline-fig8.png)

**Afficher tous les résultats d’un serveur spécifique**: cette requête montre l’affichage des résultats de toosee d’un serveur spécifique : requête : *Type = SecurityBaseline BaselineType = ordinateur Web = BaselineTestVM1*

![Résultat de la requête 3](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

Vous pouvez utiliser ces toocreate enregistrements/requêtes vos propres tableaux de bord, rapports ou les alertes. Voici un exemple de contrôle d’interface utilisateur que vous pouvez ajouter tooyour le tableau de bord. Vous pouvez apprendre comment toovisualize vos données à l’aide du Concepteur de vue OMS [ici](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/). écran Hello ci-dessous est un exemple de comment hello vignette ressemblera une fois que vous apportez cette personnalisation.

![dashboard](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

## <a name="see-also"></a>Voir aussi
Dans ce document, vous avez découvert l’évaluation de la base de référence web de la solution de sécurité et d’audit d’OMS. toolearn en savoir plus sur la sécurité d’OMS, consultez hello suivant des articles :

* [Présentation - Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Surveillance et réponse tooSecurity alertes Operations Management Suite de Solution de sécurité et d’Audit](oms-security-responding-alerts.md)
* [Surveillance des ressources dans la solution de sécurité et d’audit d’Operations Management Suite](oms-security-monitoring-resources.md)

