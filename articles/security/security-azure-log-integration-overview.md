---
title: "les journaux à partir des ressources Azure dans vos systèmes SIEM aaaIntegrate | Documents Microsoft"
description: "Découvrez l’intégration des journaux Azure, ses fonctionnalités principales et son fonctionnement."
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: 9c1346e1-baf8-4975-b2f2-42ae05b2dc0a
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/10/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: 4a59ce625702e5266a7c8eb020473cfeaf6b1964
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toomicrosoft-azure-log-integration"></a>Introduction tooMicrosoft intégration d’Azure log
Découvrez l’intégration des journaux Azure, ses fonctionnalités principales et son fonctionnement.

## <a name="overview"></a>Vue d'ensemble

L’intégration des journaux Azure est une solution gratuite qui vous permet de toointegrate les journaux brut à partir de vos ressources Azure dans les systèmes tooyour localement les informations de sécurité et de gestion des événements (SIEM).

Le service Azure Log Integration collecte les événements Windows à partir des journaux de l’Observateur d’événements, des [journaux d’activité Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md), des [alertes Azure Security Center](../security-center/security-center-intro.md) et des [journaux de diagnostic Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) des ressources Azure. Cette intégration permet à votre solution SIEM fournissent un tableau de bord unifiée pour tous vos actifs, en local ou dans le cloud de hello, afin que vous pouvez agréger, mettre en corrélation, analyser et d’alerte pour les événements de sécurité.

>[!NOTE]
À ce stade, les clouds hello uniquement pris en charge sont Azure commercial et Azure Government. Les autres clouds ne sont pas pris en charge.

![Intégration des journaux Azure][1]

## <a name="what-logs-can-i-integrate"></a>Quels journaux puis-je intégrer ?
Azure génère une journalisation complète pour chaque service Azure. Ces journaux représentent trois types de journaux :

* **Des journaux de contrôle/gestion** offrent une visibilité hello [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) les opérations CREATE, UPDATE et DELETE. Les journaux d’activité Azure sont un exemple de ce type de journal.
* **Données plan journaux** fournissent une visibilité en événements hello déclenché dans le cadre de l’utilisation de hello d’une ressource Azure. Un exemple de ce type de journal est l’Observateur d’événements Windows hello **système**, **sécurité**, et **Application** canaux dans une machine virtuelle Windows. Les journaux de diagnostics, configurés via Azure Monitor, en sont un autre exemple.
* Les **Événements traités** fournissent des informations sur les alertes et les événements analysés en votre nom. Un exemple de ce type d’événement est alertes du centre de sécurité Azure, où Azure Security Center a traité et analyser votre posture de sécurité abonnement tooprovide alertes tooyour pertinentes en cours.

Azure Log Integration prend en charge ArcSight, QRadar et Splunk. Dans tous les cas, contactez votre tooassess de fournisseur SIEM s’ils disposent d’un connecteur natif. Dans certains cas, vous aurez pas toouse Azure journal intégration lorsque les connecteurs natifs sont disponibles. Pour plus d’informations sur le journal pris en charge, visitez de types hello Forum aux questions.

>[!NOTE]
Lors de l’intégration du journal Azure est une solution disponible, il existe des coûts de stockage Azure qui résulte de stockage des informations de fichier journal hello.

Aide de la Communauté est disponible via hello [Forum MSDN de Azure journal intégration](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration). Hello forum de hello AzLog Communauté hello capacité toosupport eux avec des questions, des réponses, des conseils et astuces sur comment tooget hello plus en dehors de l’intégration du journal Azure. En outre, l’équipe d’intégration du journal Azure hello surveille ce forum et aidera à chaque fois que nous pouvons.

Vous pouvez également ouvrir une [demande de support](../azure-supportability/how-to-create-azure-support-request.md). toodo cette option, sélectionnez **journal intégration** en tant que service hello pour lequel vous demandez la prise en charge.

## <a name="next-steps"></a>Étapes suivantes
Dans ce document, vous ont été introduites tooAzure intégration du journal. toolearn plus sur Azure consigner l’intégration et types hello des journaux de prise en charge, voir hello :

* [Microsoft Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) : centre de téléchargement pour plus d’informations, la configuration système requise et les instructions d’installation pour l’intégration des journaux Azure.
* [Prise en main de l’intégration des journaux Azure](security-azure-log-integration-get-started.md) : ce didacticiel vous guide dans la procédure d’installation de l’intégration des journaux Azure et d’intégration des journaux du stockage Azure WAD, des journaux d’activité Azure, des alertes Azure Security Center et des journaux d’audit Azure Active Directory.
* [Étapes de configuration du partenaire](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – ce billet de blog montre comment tooconfigure Azure du journal toowork d’intégration avec les solutions de partenaire Splunk, HP ArcSight et QRadar d’IBM. Ce billet de blog représente notre position actuelle sur la configuration des solutions de partenaire hello. Dans tous les cas, consultez documentation de solution toopartner tout d’abord.
* [Alertes d’activité et ASC sur syslog tooQRadar](https://blogs.msdn.microsoft.com/azuresecurity/2016/09/24/integrate-azure-logs-to-qradar/) – ce billet de blog explique hello alertes d’activité et le centre de sécurité Azure toosend sur tooQRadar de syslog
* [FAQ de l’intégration des journaux Azure](security-azure-log-integration-faq.md) : ce forum aux questions répond aux questions sur l’intégration des journaux Azure.
* [Intégration de centre de sécurité les alertes avec Azure journal intégration](../security-center/security-center-integrating-alerts-with-log-integration.md) – ce document vous montre comment les alertes avec l’intégration des journaux Azure toosync Azure Security Center.

<!--Image references-->
[1]: ./media/security-azure-log-integration-overview/azure-log-integration.png
