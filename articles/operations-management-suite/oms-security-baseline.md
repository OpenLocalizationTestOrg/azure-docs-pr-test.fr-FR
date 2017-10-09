---
title: "aaaOperations gestion Suite de sécurité et la ligne de base de la Solution d’Audit | Documents Microsoft"
description: "Ce document explique comment solution de sécurité d’OMS et d’Audit toouse tooperform une évaluation de la ligne de base de tous les ordinateurs analysés à des fins de conformité et sécurité."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: ea52408cb9d2598728fe3826a946067e1c99318f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Évaluation de la base de référence dans la solution de sécurité et d’audit d’Operations Management Suite
Ce document vous aide à toouse [Operations Management Suite (OMS) Solution de sécurité et d’Audit](operations-management-suite-overview.md) évaluation planifié fonctionnalités tooaccess hello état de sécurisation de vos ressources analysés.

## <a name="what-is-baseline-assessment"></a>Qu’est-ce qu’une évaluation de la base de référence ?
Avec de nombreuses organisations gouvernementales et entreprises du secteur, Microsoft définit une configuration Windows qui représente des déploiements de serveur hautement sécurisés. Cette configuration regroupe un ensemble de clés de Registre, de paramètres de stratégie d’audit et de paramètres de stratégie de sécurité, ainsi que les valeurs recommandées par Microsoft pour ces paramètres. Cet ensemble de règles est appelé « base de référence de la sécurité ». La fonctionnalité d’évaluation de la base de référence de la solution de sécurité et d’audit d’OMS peut analyser l’ensemble de vos ordinateurs de manière transparente, afin de déterminer leur degré de conformité. 

Il existe trois types de règle :

* **Règles de Registre** : vérifiez que les clés de Registre sont correctement définies.
* **Règles de stratégie d’audit** : règles relatives à votre stratégie d’audit.
* **Règles de stratégie de sécurité**: règles d’autorisations de l’utilisateur de hello concernant sur l’ordinateur de hello.

> [!NOTE]
> Lecture [tooassess d’utiliser la sécurité OMS hello de ligne de base de Configuration de sécurité](https://blogs.technet.microsoft.com/msoms/2016/08/12/use-oms-security-to-assess-the-security-configuration-baseline/) pour une vue d’ensemble de cette fonctionnalité.
> 
> 

## <a name="security-baseline-assessment"></a>Évaluation de la base de référence de la sécurité
Vous pouvez consulter votre évaluation de ligne de base de sécurité en cours pour tous les ordinateurs qui sont analysés par OMS sécurité et d’Audit à l’aide du tableau de bord hello.  Exécutez hello suivant les étapes tooaccess hello sécurité planifié évaluation du tableau de bord :

1. Bonjour **Microsoft Operations Management Suite** dans le tableau de bord principal, cliquez sur **sécurité et Audit** vignette.
2. Bonjour **sécurité et Audit** tableau de bord, cliquez sur **évaluation de la ligne de base de** sous **domaines de sécurité**. Hello **évaluation de la ligne de base de sécurité** tableau de bord s’affiche comme illustré dans hello suivant image :
   
    ![Évaluation de la base de référence de la solution de sécurité et d’audit d’OMS](./media/oms-security-baseline/oms-security-baseline-fig1.png)

Ce tableau de bord est divisé en trois zones principales :

* **Ordinateurs comparés toobaseline**: cette section fournit un résumé de nombre de hello d’ordinateurs qui ont été consultés et hello pourcentage d’ordinateurs ayant passé l’évaluation de hello. Elle donne également hello top 10 ordinateurs et résultats de pourcentage hello pour l’évaluation de hello.
* **État des règles requise**: cette section comporte des reconnaissance d’intention toobring hello de règles de hello a échoué par niveau de gravité et Échec de règles par type. En regardant toohello premier graphique vous pouvez rapidement identifier si hello la plupart des échecs de règle sont critiques, ou non. Elle donne également une liste de règles ayant échoué 10 premières hello et leur gravité. graphique de deuxième Hello montre de type hello de règle qui a échoué au cours de l’évaluation de hello. 
* **Ordinateurs manquant d’évaluation de la ligne de base**: cette section répertorie les ordinateurs de hello qui n’ont pas eu accès en raison d’incompatibilité du système toooperating ou des défaillances. 

### <a name="accessing-computers-compared-toobaseline"></a>L’accès à des ordinateurs par rapport à toobaseline
Dans l’idéal, vos ordinateurs sont être conformes avec l’évaluation de ligne de base de sécurité hello. Cependant, il se peut que certains ne le soient pas. Ce comportement est prévu. Dans le cadre du processus de gestion de sécurité hello, il est important tooinclude examen des ordinateurs hello ayant échoué toopass tous les tests d’évaluation de la sécurité. Toovisualize un moyen rapide qui est en sélectionnant l’option de hello **ordinateurs auxquels a accédé** situé dans hello **ordinateurs comparés toobaseline** section. Vous devez normalement voir hello journal recherche de résultats affichant hello une liste des ordinateurs s’affiche dans hello suivant l’écran :

![Résultats du champ Computers accessed (Ordinateurs ouverts)](./media/oms-security-baseline/oms-security-baseline-fig2.png)

résultat de recherche Hello est indiqué dans un format de table, où hello première les colonnes nom d’ordinateur hello et seconde couleur d’hello a plusieurs hello règles ayant échoué. tooretrieve hello d’informations relative au type hello de règle qui a échoué, cliquez sur nombre hello de règles ayant échouées en plus du nom de l’ordinateur hello. Vous devez voir un toohello similaire résultat montre hello suivant image :

![Détails des résultats de l’opération d’accès aux ordinateurs](./media/oms-security-baseline/oms-security-baseline-fig3.png)

Dans ce résultat de recherche, d’avoir total hello de règles d’accès, hello du nombre de règles critiques qui ont échoué, hello des règles d’avertissements et hello des règles d’informations a échoué.

### <a name="accessing-required-rules-status"></a>Accès au statut des règles obligatoires
Après avoir obtenu les informations hello concernant hello pourcentage nombre d’ordinateurs ayant passé l’évaluation de hello, vous souhaiterez peut-être tooobtain plus d’informations sur les règles qui échouent conséquente toohello importance. Cela permet de visualisation tooprioritize les ordinateurs qui doivent être traités tooensure première elles seront conformes dans la prochaine évaluation de hello. Survolez essentiel graphique hello situé dans hello hello **règles ayant échoué par niveau de gravité** vignette sous **règles état requise** et cliquez dessus. Vous devez voir un toohello similaire de résultat suivant d’écran :

![Détails du champ Règles ayant échoué par gravité](./media/oms-security-baseline/oms-security-baseline-fig4.png) 

Type hello de règle de ligne de base qui ont échoué, la description de hello de cette règle et l’ID de Configuration CCE (Common Enumeration) de hello de cette règle de sécurité s’affichent dans ce résultat de journal. Ces attributs doit être suffisamment tooperform un toofix action corrective ce problème dans l’ordinateur cible de hello.

> [!NOTE]
> Pour plus d’informations sur CCE, accès hello [base de données National vulnérabilité](https://nvd.nist.gov/cce/index.cfm).
> 
> 

### <a name="accessing-computers-missing-baseline-assessment"></a>Accès aux ordinateurs sans évaluation de la ligne de base
OMS prend en charge membre du domaine hello et un profil de ligne de base de contrôleur de domaine sur Windows Server 2008 R2 jusqu'à tooWindows Server 2012 R2. La ligne de base de Windows Server 2016 n’est pas encore finalisée. Elle sera ajoutée dès sa publication. Tous les autres systèmes d’exploitation analysés par OMS sécurité et Audit évaluation de la ligne de base apparaît sous hello **ordinateurs manquant d’évaluation de la ligne de base** section.

## <a name="see-also"></a>Voir aussi
Dans ce document, vous avez découvert la fonction d’évaluation de la base de référence de la solution de sécurité et d’audit d’OMS. toolearn en savoir plus sur la sécurité d’OMS, consultez hello suivant des articles :

* [Présentation - Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Surveillance et réponse tooSecurity alertes Operations Management Suite de Solution de sécurité et d’Audit](oms-security-responding-alerts.md)
* [Surveillance des ressources dans la solution de sécurité et d’audit d’Operations Management Suite](oms-security-monitoring-resources.md)

