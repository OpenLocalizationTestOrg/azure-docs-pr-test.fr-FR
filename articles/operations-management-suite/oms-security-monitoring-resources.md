---
title: "Ressources dans les opérations de gestion Suite de Solution de sécurité et d’Audit d’aaaMonitoring | Documents Microsoft"
description: "Ce document vous aide à vous toouse sécurité OMS et toomonitor des fonctionnalités d’Audit vos ressources et identifier les problèmes de sécurité."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: d6752120-821f-4aa7-a049-25bf5a653b95
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 932b946ae1ffa3b979c02f419702d42d46abf7ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-resources-in-operations-management-suite-security-and-audit-solution"></a>Surveillance des ressources dans la solution de sécurité et d’audit d’Operations Management Suite
Ce document vous aide à utiliser OMS sécurité et toomonitor des fonctionnalités d’Audit de vos ressources et à identifier les problèmes de sécurité.

## <a name="what-is-oms"></a>Qu’est-ce qu’OMS ?
Microsoft Operations Management Suite (OMS) est une solution de gestion informatique basée sur le cloud de Microsoft qui vous permet de gérer et de protéger votre infrastructure locale et de cloud. Pour plus d’informations sur OMS, consultez l’article de la hello [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

## <a name="monitoring-resources"></a>Surveillance des ressources
Chaque fois que possible, vous pouvez tooprevent des incidents de sécurité se produise en premier lieu de hello. Toutefois, il est impossible tooprevent tous les incidents de sécurité. Lorsqu’un incident de sécurité peut arriver, vous devez tooensure que son impact est réduit.  Il existe trois recommandations critiques qui peuvent être utilisé toominimize hello numéros et hello l’impact des incidents de sécurité :

* Évaluer régulièrement les vulnérabilités de votre environnement.
* Vérifier régulièrement tous les systèmes informatiques et tooensure de périphériques réseau qui ils ont tous les derniers correctifs hello.
* Vérifiez régulièrement tous les journaux et mécanismes de journalisation, y compris les journaux d’événements de système d’exploitation, les journaux spécifiques des applications et les journaux système de détection d’intrusion.

OMS sécurité et Audit permet de solution informatique tooactively surveiller toutes les ressources, ce qui peuvent aider à réduire l’impact de hello des incidents de sécurité. Cette solution possède des domaines de sécurité qui peuvent être utilisés pour la surveillance des ressources. domaines de sécurité Hello fournit un accès rapide tooa options, hello analyse de sécurité pour les domaines suivants seront abordées plus de détails :

* Évaluation des logiciels malveillants
* Évaluation des mises à jour
* Identité et accès

> [!NOTE]
> pour avoir une vue d’ensemble de toutes ces options, consultez [Getting started with Operations Management Suite Security and Audit Solution](oms-security-getting-started.md)(Prise en main de la solution de sécurité et d’audit d’Operations Management Suite).
> 
> 

### <a name="monitoring-system-protection"></a>Surveillance de la protection du système
Dans une approche défense en profondeur, chaque couche de protection est important pour hello état global de sécurité de votre élément multimédia. Ordinateurs avec détecté des menaces et des ordinateurs avec une protection insuffisante figurent dans hello vignette évaluation des logiciels malveillants dans les domaines de sécurité. En utilisant les informations de hello hello évaluation des logiciels malveillants, vous pouvez identifier un plan tooapply protection toohello les serveurs qui en ont besoin. tooaccess cette hello de suivi option étapes ci-dessous :

1. Bonjour **Microsoft Operations Management Suite** cliquez sur le tableau de bord principal **sécurité et Audit** vignette.
   
    ![Sécurité et audit](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. Bonjour **sécurité et Audit** tableau de bord, cliquez sur **évaluation du logiciel anti-programme malveillant** sous **domaines de sécurité**. Hello **évaluation du logiciel anti-programme malveillant** tableau de bord s’affiche comme indiqué ci-dessous :

![Évaluation des logiciels malveillants](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig2-ga.png)

Vous pouvez utiliser hello **évaluation des logiciels malveillants** hello tooidentify de tableau de bord suivant des problèmes de sécurité :

* **Menaces actives**: les ordinateurs qui ont été compromises et qui ont des menaces actives dans le système de hello.
* **Mis à jour de ces menaces**: ordinateurs qui ont été compromis, mais les menaces hello ont été mis à jour.
* **Signature obsolète**: les ordinateurs pour lesquels la protection contre les programmes malveillants activée mais la signature de hello est obsolète.
* **Aucune protection en temps réel**: ordinateurs sur lesquels aucun logiciel anti-programme malveillant n’est installé.

### <a name="monitoring-updates"></a>Surveillances des mises à jour
Application des mises à jour de sécurité les plus récentes hello est une meilleure pratique de sécurité, et il doit être incorporé dans votre stratégie de gestion des mises à jour. Le service Microsoft Monitoring Agent (HealthService.exe) lit les informations de mise à jour des ordinateurs analysés, puis envoie ce service OMS de toohello informations mises à jour dans le cloud hello pour le traitement. Hello service Microsoft Monitoring Agent est configuré comme un service automatique et il doit être toujours en cours d’exécution dans l’ordinateur cible de hello.

![Surveillances des mises à jour](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig3.png)

Logique est appliqué toohello mise à jour de données et service de cloud de hello enregistre les données de salutation. Si les mises à jour manquantes sont trouvées, elles sont affichées dans hello **mises à jour** tableau de bord. Vous pouvez utiliser hello **mises à jour** toowork de tableau de bord sans les mises à jour et développer un plan tooapply les toohello les serveurs qui en ont besoin. Suivez les étapes de hello ci-dessous tooaccess hello **mises à jour** tableau de bord :

1. Bonjour **Microsoft Operations Management Suite** cliquez sur le tableau de bord principal **sécurité et Audit** vignette.
2. Bonjour **sécurité et Audit** tableau de bord, cliquez sur **évaluation de mise à jour** sous **domaines de sécurité**. tableau de bord Hello mise à jour s’affiche comme indiqué ci-dessous :

![Évaluation des mises à jour](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig4.png)

Dans ce tableau de bord, vous pouvez effectuer un mise à jour évaluation toounderstand hello état actuel de vos ordinateurs et les menaces les plus critiques hello. À l’aide de hello **critiques ou mises à jour de sécurité** vignette, les administrateurs informatiques seront en mesure de tooaccess des informations détaillées sur les mises à jour de hello sont manquants, comme indiqué ci-dessous :

![résultat de la recherche](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig5.png)

Ce rapport inclut des informations critiques qui peuvent être utilisées type hello de tooidentify de menace ce système est vulnérable, qui inclut des articles de Microsoft KB hello associés à la mise à jour de sécurité hello et hello MS Bulletin qui a plus de détails sur hello vulnérabilité.

### <a name="monitoring-identity-and-access"></a>Surveillance des identités et des accès
Les utilisateurs travaillent en déplacement, utilisent différents appareils et accèdent à un grand nombre d’applications locales, c’est pourquoi il est impératif que leurs informations d’identification soient protégées. Vol des informations d’identification est celles dans lesquelles une personne malveillante parvient initialement tooaccess des informations d’identification de l’accès tooa utilisateur normal, l’un système dans le réseau de hello. De nombreux cas, cette attaque est uniquement un réseau de toohello accès moyen tooget, comme objectif ultime hello comptes à privilèges toodiscover. 

Les attaquants resteront dans le réseau de hello, à l’aide des outils tooextract les informations d’identification à partir de sessions hello d’autres comptes de session disponible gratuitement. Selon la configuration du système de hello, ces informations d’identification peuvent être extrait sous forme de hello de hachages, tickets ou même des mots de passe.  

> [!NOTE]
> les ordinateurs qui sont directement exposés toohello Qu'internet s’affiche de nombreux échec tente que toologin réessayez à l’aide de tous les types de noms d’utilisateurs connus (par exemple, administrateur). Dans la plupart des cas, il est OK si les noms d’utilisateur connu hello ne sont pas utilisés et si le mot de passe hello est suffisamment fort.
> 
> 

Il est possible de tooidentify ces intrus avant qu’ils compromettent un compte doté des privilèges. Vous pouvez tirer parti de **OMS Solution de sécurité et d’Audit** toomonitor identités et des accès. Suivez les étapes de hello ci-dessous tooaccess hello **identité et accès** tableau de bord :

1. Bonjour **Microsoft Operations Management Suite** tableau de bord principal cliquez sur sécurité et Audit vignette.
2. Bonjour **sécurité et Audit** tableau de bord, cliquez sur **identité et accès** sous **domaines de sécurité**. Hello **identité et accès** tableau de bord s’affiche comme indiqué ci-dessous :

![identité et accès](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig6-ga.png)

Dans le cadre de votre stratégie de surveillance régulière, vous devez inclure la surveillance des identités. L’administrateur informatique doit vérifier si un grand nombre de tentatives est associé à un nom d’utilisateur valide spécifique. Cela peut indiquer qu’un intrus acquis les nom d’utilisateur réel hello et essayez toobrute force ou un outil automatique qui utilise le mot de passe codé en dur a expiré.

Cette activation de tableau de bord informatique tooquickly identifier les ressources de potentiels menaces connexes tooidentity et accès toocompany. Il est notamment importante tooalso identifier des tendances potentiels, par exemple dans la vignette d’ouvertures de session au fil du temps hello, vous pouvez voir période combien de fois une tentative d’ouverture de session a été effectuée. Dans ce cas hello ordinateur **FileServer** reçu 35 les tentatives d’ouverture de session. Vous pouvez obtenir de plus amples informations sur cet ordinateur en cliquant dessus. 

![détails supplémentaires](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig7-new.png)

rapport Hello générée pour cet ordinateur apporte des informations précieuses sur ce modèle. Remarqué que hello **compte** hello donne colonne hello de compte d’utilisateur qui a été utilisé tootry tooaccess hello système, **TIMEGENERATED** donne de colonne vous hello intervalle de temps dans le hello tentative a été effectuée et Hello **LOGONTYPENAME** donne de colonne vous hello emplacement où cette tentative a été effectuée. Si ces tentatives ont été effectuées localement dans le système de hello par un programme, hello **processus** colonne lorsque vous souhaitez afficher nom du processus hello. Dans les scénarios où tentative d’ouverture de session hello provient d’un programme, vous avez déjà le nom du processus hello disponible et vous pouvez maintenant effectuer davantage enquête dans le système cible de hello.

## <a name="see-also"></a>Voir aussi
Dans ce document, vous avez appris comment toomonitor de solution de sécurité d’OMS et d’Audit toouse vos ressources. toolearn en savoir plus sur la sécurité d’OMS, consultez hello suivant des articles :

* [Présentation - Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Getting started with Operations Management Suite Security and Audit Solution (Prise en main de la solution de sécurité et d’audit d’Operations Management Suite)](oms-security-getting-started.md)
* [Surveillance et réponse tooSecurity alertes Operations Management Suite de Solution de sécurité et d’Audit](oms-security-responding-alerts.md)

