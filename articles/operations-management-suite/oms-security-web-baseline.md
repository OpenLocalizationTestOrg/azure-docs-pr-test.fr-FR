---
title: "aaaOperations gestion Suite de sécurité et Audit Solution Web base | Documents Microsoft"
description: "Ce document explique comment solution de sécurité d’OMS et d’Audit toouse tooperform une évaluation de la ligne de base web de tous les serveurs web analysés fins de conformité et sécurité."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ROBOTS: NOINDEX
redirect_url: https://www.microsoft.com/cloud-platform/security-and-compliance
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: 8aa87fa404ff97ab549dda3f9bebb75766055963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Évaluation de la base de référence web dans la solution de sécurité et d’audit d’Operations Management Suite
Ce document vous aide à toouse [Operations Management Suite (OMS) Solution de sécurité et d’Audit](operations-management-suite-overview.md) web d’évaluation de la ligne de base fonctionnalités tooaccess hello état de sécurisation de vos ressources analysés.

## <a name="what-is-web-baseline-assessment"></a>Qu’est-ce qu’une évaluation de la base de référence web ?
La solution de sécurité d’OMS permet actuellement d’évaluer la base de référence de sécurité pour les systèmes d’exploitation. Il analyse les paramètres de système d’exploitation hello de vos serveurs toutes les 24 heures et fournit un affichage des paramètres potentiellement vulnérables. Pour plus d’informations à ce sujet, consultez [Évaluation de la base de référence dans la solution de sécurité et d’audit d’Operations Management Suite](oms-security-baseline.md).

Hello vise d’évaluation de la ligne de base hello web paramètres du serveur web potentiellement vulnérables toofind. Hello trois sources principales pour les configurations de base hello web sont : configuration .NET, ASP.NET et IIS.  Simplement comme hello évaluation de ligne de base du système d’exploitation, sécurité OMS va tooscan votre chaque 24 heures des serveurs web et fournissent une vue à l’état de sécurité d’eux.  Dans les services Internet (IIS), la configurations sont hautement personnalisables, et qui permet à différents toobe niveaux de site et l’application remplacée. le scanneur Hello vérifie les paramètres de hello à chaque niveau de site/application de niveau racine d’addition toohello par défaut. Cela vous permet des emplacements des paramètres de la vulnérabilité potentielle tooidentify et résoudre rapidement.


## <a name="web-security-baseline-assessment"></a>Évaluation de la base de référence de la sécurité web
Cette fonctionnalité va toobe accédé à l’aide d’option de recherche d’OMS hello pour cette version préliminaire. Suivez les étapes de hello sous requête hello affecté de tooperform :

1. Bonjour **Microsoft Operations Management Suite** cliquez sur le tableau de bord principal **sécurité et Audit** vignette.
2. Bonjour **sécurité et Audit** tableau de bord, cliquez sur **recherche de journal** bouton.
3. Hello première requête que vous pouvez utiliser est hello **résumé de l’évaluation de ligne de base Web**. Bonjour **rechercher ici** , tapez cette requête : Type*= SecurityBaselineSummary BaselineType = web*. Hello suivant écran présente un exemple de sortie :

![Résumé de l’évaluation de la base de référence web](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> Dans cette requête, chaque enregistrement indique un récapitulatif de l’évaluation sur un serveur donné.

Une fois que vous êtes dans hello **recherche de journal**, vous pouvez taper des requêtes différentes tooobtain plus d’informations sur l’évaluation de ligne de base hello web. En outre toohello de requête précédente, vous pouvez également utiliser hello suivant celles dans cette version préliminaire.

**Évaluation de la règle de base de référence web** : chaque enregistrement représente une seule évaluation de la règle de base de référence web sur un seul serveur. Elle inclut toutes les données de règle de hello, l’emplacement, les résultats hello attendu et de résultats réel hello.

**Requête** : Type*=SecurityBaseline BaselineType=web*

![Évaluation de la règle de base de référence web](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

**Afficher tous les résultats d’un serveur spécifique**: cette requête montre l’affichage des résultats de toosee d’un serveur spécifique.

**Requête** : *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*

![Tous les résultats](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

Vous pouvez également utiliser ces toocreate enregistrements/requêtes vos propres tableaux de bord, rapports ou les alertes. écran de Hello ci-dessous présente un exemple de contrôle d’interface utilisateur que vous pouvez ajouter tooyour le tableau de bord. Vous pouvez apprendre comment toovisualize vos données à l’aide du Concepteur de vue OMS [ici](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/). écran Hello ci-dessous est un exemple de comment hello vignette ressemblera une fois que vous apportez cette personnalisation.

![Exemple d’interface utilisateur](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> Si vous souhaitez que les paramètres de hello tooknow qui sont vérifiées pour l’évaluation de ligne de base hello, vous pouvez télécharger [cette feuille de calcul Excel](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) qui contient ces paramètres.

## <a name="see-also"></a>Voir aussi
Dans ce document, vous avez découvert la fonction d’évaluation de la base de référence web de la solution de sécurité et d’audit d’OMS. toolearn en savoir plus sur la sécurité d’OMS, consultez hello suivant des articles :

* [Présentation - Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Surveillance et réponse tooSecurity alertes Operations Management Suite de Solution de sécurité et d’Audit](oms-security-responding-alerts.md)
* [Surveillance des ressources dans la solution de sécurité et d’audit d’Operations Management Suite](oms-security-monitoring-resources.md)

