---
title: "aaaMonitoring et réponse tooSecurity alertes Operations Management Suite de Solution de sécurité et d’Audit | Documents Microsoft"
description: "Ce document vous aide à vous toouse hello threat intelligence option disponible dans OMS sécurité et Audit toomonitor et répond toosecurity alertes."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 7d45a32b-1341-4bb5-a436-1f42a8a2590a
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/13/2017
ms.author: yurid
ms.openlocfilehash: 3d92b6809b7bd934c889afc119e5e34ff2b85f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-responding-toosecurity-alerts-in-operations-management-suite-security-and-audit-solution"></a>Surveiller et réagir toosecurity des alertes dans Operations Management Suite de Solution de sécurité et d’Audit
Ce document vous aide à utiliser hello threat intelligence option disponible dans OMS sécurité et Audit toomonitor et répondre toosecurity alertes.

## <a name="what-is-oms"></a>Qu’est-ce qu’OMS ?
Microsoft Operations Management Suite (OMS) est une solution de gestion informatique basée sur le cloud de Microsoft qui vous permet de gérer et de protéger votre infrastructure locale et de cloud. Pour plus d’informations sur OMS, consultez l’article de la hello [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

## <a name="threat-intelligence"></a>Informations sur les menaces
Dans un environnement où les utilisateurs un accès large toohello réseau et utilisent une gamme de périphériques tooconnect toocorporate données d’entreprise, il est impératif que vous pouvez en surveillant activement vos ressources et répondre rapidement toosecurity incidents. Cela est particulièrement important du point de vue du cycle de vie de sécurité hello, car certaines inquiétudes menaces peut ne pas déclenchent des alertes ou des activités suspectes qui peuvent être identifiées par des contrôles techniques traditionnelles de sécurité. 

À l’aide de hello **menaces** option disponibles dans OMS sécurité et Audit, les administrateurs informatiques peuvent identifier les menaces de sécurité sur l’environnement de hello, par exemple, identifier si un ordinateur particulier fait partie d’un [ botnet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection). Les ordinateurs peuvent devenir des nœuds dans un botnet lorsque des personnes malveillantes installer de manière illicite contre les programmes malveillants qui secrètement se connecte cette commande toohello d’ordinateur et le contrôle. Cette option peut également identifier les menaces potentielles provenant de canaux de communication obscurs, tel que le [Darknet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection_honeypots_darkents). 

Dans commande toobuild cette menaces OMS sécurité et Audit utilisent des données provenant de plusieurs sources au sein de Microsoft. OMS sécurité et Audit reposera sur ce données tooidentify les menaces potentielles dans votre environnement.

volet d’informations sur les menaces Hello est constitué par les trois options principales :

* Servers with outbound malicious traffic (Serveurs avec trafic sortant malveillant)
* Detected threats types (Types de menaces détectés)
* Threat intelligence map (Carte d’informations sur les menaces)

> [!NOTE]
> pour avoir une vue d’ensemble de toutes ces options, consultez [Getting started with Operations Management Suite Security and Audit Solution](oms-security-getting-started.md)(Prise en main de la solution de sécurité et d’audit d’Operations Management Suite).
> 
> 

### <a name="responding-toosecurity-alerts"></a>Répondre toosecurity alertes
Une des étapes hello d’un [réponse aux incidents de sécurité](https://technet.microsoft.com/library/cc512623.aspx) processus est gravité hello tooidentify hello compromis ou des systèmes. Dans cette phase, vous devez effectuer hello tâches suivantes :

* Déterminer la nature hello d’attaque de hello
* Déterminer le point d’attaque hello d’origine
* Déterminer l’intention de hello d’attaque de hello. Attaque hello spécifiquement dirigées vers des informations spécifiques à tooacquire votre organisation, ou a été aléatoire ?
* Identifier les systèmes hello qui ont été compromis.
* Identifier les fichiers hello qui ont accédé et déterminent la sensibilité hello de ces fichiers

Vous pouvez tirer parti de **menaces** informations dans OMS sécurité et Audit toohelp solution avec ces tâches. Étapes hello ci-dessous tooaccess cela **menaces** options :

1. Bonjour **Microsoft Operations Management Suite** cliquez sur le tableau de bord principal **sécurité et Audit** vignette.
   
    ![Sécurité et audit](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. Bonjour **sécurité et Audit** tableau de bord, vous verrez hello **menaces** options dans la droite de hello, comme indiqué ci-dessous :
   
    ![Informations sur les menaces](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig2-ga.png)

Ces trois vignettes vous donne une vue d’ensemble des menaces courantes de hello. Bonjour **serveur avec le trafic sortant malveillant** vous serez en mesure de tooidentify si elle existe sur n’importe quel ordinateur que vous analysez (à l’intérieur ou en dehors de votre réseau) qui est envoi du trafic malveillant toohello Internet. 

Hello **a détecté des types de menaces** vignette affiche un résumé des menaces hello qui sont en cours « dans hello wild », si vous cliquez sur cette vignette s’affiche plus de détails sur ces menaces comme indiqué ci-dessous :

![Detected threat types (Types de menaces détectés)](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig3.png)

Vous pouvez obtenir plus d’informations sur chacune des menaces en cliquant dessus. exemple Hello ci-dessous montre un Botnet plus en détail :

![plus de détails sur une menace](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig4.png)

Comme décrit dans début hello de cette section, ces informations peuvent être très utiles au cours d’un cas de réponse aux incidents. Il peut également être important pendant une investigation informatique, où vous avez besoin de source de hello toofind d’attaque hello, le système a été compromis et hello chronologie. Dans ce rapport, vous pouvez facilement identifier certains détails importants sur les attaques hello, telles que : hello source d’attaque de hello, hello IP local qui a été compromis et hello d’état de session en cours de connexion de hello. 

Hello **carte d’intelligence des menaces** vous permettra de tooidentify hello emplacements actuels du monde hello dont le trafic malveillant. Il existe orange (entrant) et flèches (sortants) rouges dans ce mappage qui identifient la direction du trafic de hello, si vous cliquez sur une de ces flèches, il affiche type hello de direction du trafic des menaces et hello comme indiqué ci-dessous :

![carte d’informations sur les menaces](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig5.png)

> [!NOTE]
> Vous pouvez voir une démonstration sur toouse cette fonctionnalité en réponse à un incident du processus en regardant la présentation de hello [atténuer les menaces de sécurité de centre de données avec une enquête interactive à l’aide d’Operations Management Suite](https://myignite.microsoft.com/videos/5000) envoyées à Microsoft Ignite.
> 

### <a name="responding-toodistinct-malicious-ip-accessed"></a>Adresses IP malveillantes toodistinct accédé de réponse
Dans certains scénarios, vous pouvez remarquer qu’un ordinateur surveillé a accédé à une adresse IP potentiellement malveillante :

![carte d’informations sur les menaces](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

Cette alerte et autres dans hello même catégorie, sont générés via la sécurité d’OMS en tirant parti [Microsoft Threat Intelligence](https://youtu.be/O4WtxgUrDc8). Hello les données sur les menaces recueillie par Microsoft ainsi que les acheté fournisseurs threat intelligence. Ces données sont fréquemment mis à jour et adapter le déplacement de toofast des menaces. En raison de la nature de tooits, il doit être combiné avec d’autres sources d’informations de sécurité lors de la [examen](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) une alerte de sécurité. 

## <a name="customize-alerts-received-via-e-mail"></a>Personnaliser les alertes reçues par e-mail

Vous pouvez choisir quels utilisateurs de votre organisation seront informés en cas de déclenchement d’alertes de sécurité par la sécurité OMS. Cette option est disponible sous la vue d’ensemble / paramètres au hello du tableau de bord OMS :

![Email](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig7.png)

## <a name="see-also"></a>Voir aussi
Dans ce document, vous avez appris comment toouse hello **menaces** option dans OMS sécurité et Audit solution toorespond toosecurity les alertes. toolearn en savoir plus sur la sécurité d’OMS, consultez hello suivant des articles :

* [Présentation - Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Getting started with Operations Management Suite Security and Audit Solution](oms-security-getting-started.md)
* [Surveillance des ressources dans la solution de sécurité et d’audit d’Operations Management Suite](oms-security-monitoring-resources.md)

