---
title: "aaaConnecting vos produits de sécurité toohello sécurité d’Operations Management Suite (OMS) et la Solution d’Audit | Documents Microsoft"
description: "Ce document vous aide à vous tooconnect votre tooOperations de produits de sécurité Gestion Suite de Solution de sécurité et d’Audit à l’aide du Format d’événement commun."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 46eee484-e078-4bad-8c89-c88a3508f6aa
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 0f4b372d0379987c4e249628a3c8d52733be65c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-your-security-products-toohello-operations-management-suite-oms-security-and-audit-solution"></a>La connexion de vos produits de sécurité toohello sécurité d’Operations Management Suite (OMS) et la Solution d’Audit 
Ce document vous permet de connecter vos produits de sécurité en hello sécurité OMS et de la Solution d’Audit. Hello sources suivantes est prises en charge :

- Événements au format d’événement courant (CEF)
- Événements Cisco ASA


## <a name="what-is-cef"></a>Qu’est-ce que CEF ?
Format d’événement commun (CEF) est un format standard en plus des messages Syslog, utilisé par nombreux fournisseurs tooallow événement interopérabilité de la sécurité entre différentes plateformes. OMS Solution de sécurité et d’Audit prennent en charge les intégrer les données à l’aide de CEF, ce qui vous permet de tooconnect vos produits de sécurité avec la sécurité d’OMS. 

En connectant votre tooOMS de source de données, vous êtes parti tootake en mesure de hello suivant des fonctions qui font partie de cette plateforme :

- Recherche et corrélation
- Audit
- Alerte
- Informations sur les menaces
- Problèmes notables

## <a name="collection-of-security-solution-logs"></a>Collection des journaux des solutions de sécurité

OMS Security prend en charge la collecte de journaux à l’aide du format CEF sur Syslogs et des journaux [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/). Dans cet exemple, la source de hello (ordinateur qui génère des journaux de hello) est un ordinateur Linux en cours d’exécution les démon syslog-ng et cible de hello est sécurité OMS. Vous devez hello tooperform suivant l’ordinateur Linux hello tooprepare tâches :

- Téléchargez hello Agent OMS pour Linux, version 1.2.0-25 ou version ultérieure.
- Suivez hello section **Guide d’installation rapide** de [cet article](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall et espace de travail tooyour hello intégrer l’agent.

En règle générale, l’agent de hello est installé sur un ordinateur différent de hello un sur les journaux de hello sont générés. Ordinateur de l’agent de transfert hello journaux toohello nécessitent généralement hello comme suit :

- Configurer hello journalisation produit/machine tooforward hello événements requis toohello démon syslog (rsyslog ou syslog-ng) sur l’ordinateur agent hello.
- Activer le démon syslog hello messages de tooreceive hello agent ordinateur à partir d’un système distant.

Sur l’ordinateur agent hello, les événements de hello doivent toobe envoyé à partir de hello syslog démon toolocal le port UDP 25226. Hello agent est en attente pour les événements entrants sur ce port. Hello Voici un exemple de configuration pour l’envoi de tous les événements à partir de l’agent toohello hello système local (vous pouvez modifier hello configuration toofit vos paramètres locaux) :

1. Fenêtre de terminal ouverte hello et accédez toohello active */etc/syslog-ng /* 
2. Créer un nouveau fichier *sécurité-config-omsagent.conf* et ajoutez hello suivant contenu : OMS_facility = local4
    
    filter f_local4_oms { facility(local4); };

    destination security_oms { tcp("127.0.0.1" port(25226)); };

    log { source(src); filter(f_local4_oms); destination(security_oms); };
    
3. Télécharger le fichier de hello *security_events.conf* et le placer à */etc/opt/microsoft/omsagent/conf/omsagent.d/* dans l’ordinateur de l’Agent OMS hello.
4. Tapez la commande hello ci-dessous démon syslog de hello toorestart : *pour exécuter syslog-ng :*
    
    ```
    sudo service rsyslog restart
    ```

    *Pour rsyslog exécutez :*
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. Tapez la commande hello ci-dessous toorestart hello OMS Agent :

    *Pour syslog-ng, exécutez :*
    
    ```
    sudo service omsagent restart
    ```

    *Pour rsyslog exécutez :*
    
    ```
    systemctl restart omsagent
    ```
6. Tapez la commande hello ci-dessous et examinez les hello tooconfirm de résultats qu’il n’y a pas d’erreurs dans le journal de l’Agent OMS hello :

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a>Examen des événements de sécurité collectés

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

Après la hello configuration, les événements de sécurité hello démarrera toobe ingéré par la sécurité d’OMS. toovisualize ces événements, ouvrez hello recherche de journal, tapez la commande hello *Type = CommonSecurityLog* hello du champ de recherche et appuyez sur ENTRÉE. Hello suivant montre les résultats hello de cette commande, notez que dans ce cas OMS sécurité déjà ingéré des journaux de sécurité à partir de plusieurs fournisseurs :
   
![Évaluation de la base de référence de la solution de sécurité et d’audit d’OMS](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

Vous pouvez affiner la recherche pour un fournisseur unique, par exemple, toovisualize Cisco en ligne se connecte, tapez : *Type = CommonSecurityLog DeviceVendor = Cisco*. Hello « CommonSecurityLog » a des champs prédéfinis, pour n’importe quel en-tête CEF, y compris l’extensios base hello, lors d’une autre extension « Extension personnalisée » ou non, est inséré dans le champ de « AdditionalExtensions ». Vous pouvez utiliser les champs de tooget dédié de fonction de champs personnalisés hello à partir de celui-ci. 

### <a name="accessing-computers-missing-baseline-assessment"></a>Accès aux ordinateurs sans évaluation de la ligne de base
OMS prend en charge le profil de base de membre de domaine hello sur Windows Server 2008 R2 jusqu'à tooWindows Server 2012 R2. La ligne de base de Windows Server 2016 n’est pas encore finalisée. Elle sera ajoutée dès sa publication. Tous les autres systèmes d’exploitation analysés par OMS sécurité et Audit évaluation de la ligne de base apparaissent sous hello **ordinateurs manquant d’évaluation de la ligne de base** section.

## <a name="see-also"></a>Voir aussi
Dans ce document, vous avez appris comment tooconnect votre tooOMS de solution CEF. toolearn en savoir plus sur la sécurité d’OMS, consultez hello suivant des articles :

* [Présentation - Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Surveillance et réponse tooSecurity alertes Operations Management Suite de Solution de sécurité et d’Audit](oms-security-responding-alerts.md)
* [Surveillance des ressources dans la solution de sécurité et d’audit d’Operations Management Suite](oms-security-monitoring-resources.md)

