---
title: "aaaAzure Migration de plateforme de centre de sécurité | Documents Microsoft"
description: "Ce document explique de manière toohello modifications des données de centre de sécurité Azure est collectée."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 80246b00-bdb8-4bbc-af54-06b7d12acf58
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: yurid
ms.openlocfilehash: 28cb8d85912a3f62941cf113da51070081b5eda2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-platform-migration"></a>Migration de plateforme Azure Security Center

À compter de début juin 2017, centre de sécurité Azure déploie les importante modifications toohello façon dont les données de sécurité sont collectées et stockées.  Ces modifications déverrouiller les nouvelles fonctionnalités telles que les données de sécurité hello capacité tooeasily recherche et permet de mieux aligner avec les autres tâches de gestion Azure et de surveiller les services.

> [!NOTE]
> migration de la plate-forme Hello ne devrait pas affecter vos ressources de production, et aucune action n’est nécessaire à partir de votre côté.


## <a name="whats-happening-during-this-platform-migration"></a>Que se passe-t-il lors de la migration de la plateforme ?

Auparavant, le centre de sécurité utilisé toocollect les données de sécurité à partir de vos machines virtuelles salutation l’Agent d’analyse Azure. Cela inclut des informations sur les configurations de sécurité, qui sont utilisés tooidentify vulnérabilités, et les événements de sécurité, qui sont les menaces toodetect utilisé. Ces données étaient stockées dans vos comptes de stockage dans Azure.

À l’avenir, que le centre de sécurité utilise hello Microsoft Monitoring Agent – il s’agit hello même agent utilisé par hello Operations Management Suite et de service de journal Analytique. Données collectées à partir de cet agent sont stockées dans deux existant *Analytique de journal* [espace de travail](../log-analytics/log-analytics-manage-access.md) associé à votre abonnement Azure ou d’un nouvel espace, en prenant en compte de géolocalisation hello Hello machine virtuelle .

## <a name="agent"></a>Agent

Dans le cadre du passage de hello, hello Microsoft Monitoring Agent (pour [Windows](../log-analytics/log-analytics-windows-agents.md) ou [Linux](../log-analytics/log-analytics-linux-agents.md)) est installé sur tous les ordinateurs virtuels de Azure à partir de laquelle données sont actuellement recueillies.  Si hello que machine virtuelle a déjà hello Microsoft Monitoring Agent est installé, le centre de sécurité tire parti de hello actuel installé l’agent.

Pour une période de temps (en général quelques jours), les deux agents s’exécutent côte à côte tooensure une transition en douceur sans aucune perte de données. Cela permet à Microsoft toovalidate qui hello nouveau pipeline de données est opérationnelle avant l’arrêt de l’utilisation de pipeline actuel de hello. Une fois vérifié, hello Agent de surveillance Azure sera supprimé de vos machines virtuelles. Aucune action n’est requise de votre part. Un message électronique vous informera lorsque tous les clients auront été migrés.
 
Il est déconseillé de désinstaller manuellement hello Agent de surveillance Azure pendant la migration de hello comme entraîner des écarts dans les données de sécurité. Veuillez consulter le [service clientèle et support technique de Microsoft](https://support.microsoft.com/contactus/) si vous avez besoin d’aide. 

Hello Microsoft Monitoring Agent pour Windows requiert utilisent le port TCP 443, lire [Guide de résolution des problèmes de centre de sécurité Azure](security-center-troubleshooting-guide.md) pour plus d’informations.


> [!NOTE] 
> Étant donné que hello Microsoft Monitoring Agent peut être utilisé par les autres tâches de gestion Azure et de surveillance des services, l’agent de hello ne sera pas désinstallé automatiquement lorsque vous désactivez collecte de données dans le centre de sécurité. Toutefois, vous pouvez la désinstaller manuellement l’agent de hello si nécessaire.

## <a name="workspace"></a>Espace de travail

Comme décrit précédemment, les données collectées à partir de Microsoft Monitoring Agent (pour le compte du centre de sécurité) sont stockés dans soit un Analytique de journal existants de hello espace associé à votre abonnement Azure ou d’un nouvel espace, tenant hello de compte GÉOLOCALISATION de hello machine virtuelle.

Bonjour portail Azure, vous pouvez parcourir toosee une liste de vos espaces de travail Analytique des journaux, y compris ceux créés par le centre de sécurité. Un groupe de ressources associées sera créé pour les nouveaux espaces de travail. Les deux respectent la convention d’affectation de noms suivante :

- Espace de travail : *DefaultWorkspace-[ID d’abonnement]-[zone géographique]*
- Groupe de ressources : *DefaultResouceGroup-[zone géographique]* 
 
Pour les espaces de travail créés par Security Center, les données sont conservées pendant 30 jours. Pour les espaces de travail existants, rétention est basée sur l’espace de travail hello niveau tarifaire.

> [!NOTE]
> Les données précédemment collectées par Security Center demeurent dans vos comptes de stockage. Une fois la migration de hello est terminée, vous pouvez supprimer ces comptes de stockage.

### <a name="oms-security-solution"></a>Solution de sécurité OMS 

Pour les clients existants qui n’ont pas installé la solution de sécurité OMS, Microsoft l’installe dans leur espace de travail, mais en ciblant uniquement les machines virtuelles Azure. Ne désinstallez pas cette solution, car il n’existe aucune correction automatique si cette opération est effectuée à partir de la console de gestion OMS.


## <a name="other-updates"></a>Autres mises à jour

Conjointement avec la migration de la plate-forme hello, nous allons déploiement de certaines mises à jour mineures supplémentaires :

- Des versions de système d’exploitation supplémentaires seront prises en charge. Consultez la liste de hello [ici](security-center-faq.md#virtual-machines).
- liste de Hello des vulnérabilités du système d’exploitation sera développée. Consultez la liste de hello [ici](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).
- Les [prix](https://azure.microsoft.com/pricing/details/security-center/) seront calculés au prorata toutes les heures (au lieu de tous les jours, comme auparavant), ce qui entraînera des économies pour certains clients.
- Collecte de données sera nécessaire et automatiquement activée pour les clients de la tarification Standard hello.
- Azure Security Center commencera à détecter des solutions anti-programme malveillant qui n’ont pas été déployées via des extensions Azure. La détection de Symantec Endpoint Protection et Defender pour Windows 2016 sera disponible dans un premier temps.
- Les stratégies de prévention et les notifications sont uniquement configurables à hello *abonnement* niveau, mais la tarification peut toujours être défini sur hello *groupe de ressources* niveau

