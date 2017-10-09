---
title: aaaPen test | Documents Microsoft
description: "article de Hello fournit une vue d’ensemble des intrusions hello (pentest) processus de test et comment effectuer pentest par rapport à vos applications en cours d’exécution dans l’infrastructure Azure."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 695d918c-a9ac-4eba-8692-af4526734ccc
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: yurid
ms.openlocfilehash: 202c239f46d8693ab7aa85e237235372e743e108
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="pen-testing"></a>Test de pénétration
Un des points forts hello pour le déploiement et de tester des applications à l’aide de Microsoft Azure est que vous n’avez pas besoin tooput ensemble une toodevelop d’infrastructure sur site, tester et déployer vos applications. Toute infrastructure hello est pris en charge par les services de la plateforme Microsoft Azure hello. Vous n’avez pas tooworry sur demande, l’acquisition et « montage en rack et empilage » votre propre matériel sur site.

C’est parfait, mais vous devez toomake que vous effectuez votre sécurité normale préalable. Un hello choses toodo est intrusion tester hello applications vous déployez dans Azure.

Vous savez sans doute déjà que Microsoft effectue le [test de pénétration de l’environnement Azure](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e). Ce processus nous aide à améliorer notre plateforme et oriente nos actions en faveur de l’amélioration des contrôles de sécurité, de l’introduction de nouveaux contrôles de sécurité et de l’amélioration de nos processus de sécurité.

Nous ne stylet tester votre application pour vous, mais nous ne comprennent que vous souhaitez et tooperform stylet test sur vos propres applications. C’est une bonne chose, car vous pouvez améliorer la sécurité hello de vos applications, vous aider à sécuriser davantage l’écosystème hello de Azure complet.

Quand le stylet vous testez vos applications, il peut se présenter comme une attaque toous. Nous [surveillons en permanence](http://blogs.msdn.com/b/azuresecurity/archive/2015/07/05/best-practices-to-protect-your-azure-deployment-against-cloud-drive-by-attacks.aspx) les schémas d’attaque et initions un processus de réponse aux incidents si les circonstances nous y obligent. Il ne vous aide pas et il ne permet pas nous si nous déclencher une réponse aux incidents échéance tooyour propre en raison du test de diligence du stylet.

Le toodo ?

Lorsque vous êtes prêt toopen tester vos applications hébergées dans Azure, vous avez la possibilité de trop[faites-nous savoir](https://portal.msrc.microsoft.com/en-us/engage/pentest). Une fois que nous savons que vous allez toobe effectuant des tests spécifiques, nous ne sera pas par inadvertance arrêter (par exemple, l’adresse IP hello que vous testez à partir de blocage), tant que vos tests conformes toohello Azure stylet test termes et conditions décrites dans [Microsoft nuage unifiée intrusion tester les règles d’Engagement](https://technet.microsoft.com/en-us/mt784683).
Vous avez la possibilité d’effectuer plusieurs tests :

* Les tests sur votre hello toouncover de points de terminaison [ouvrir Web Application sécurité projet (OWASP avoir) premiers 10 vulnérabilités](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)
* [Fuzzing](https://blogs.microsoft.com/cybertrust/2007/09/20/fuzz-testing-at-microsoft-and-the-triage-process/) de vos points de terminaison
* [Balayage des ports](https://en.wikipedia.org/wiki/Port_scanner) de vos points de terminaison

En revanche, vous ne pouvez effectuer aucune forme [d’attaque par déni de service (DoS)](https://en.wikipedia.org/wiki/Denial-of-service_attack), c’est-à-dire que nous ne pouvez ni initier une attaque par déni de service proprement dite, ni effectuer les tests associés permettant de déterminer, démontrer ou simuler n’importe quel type d’attaque de déni de service.

Sont que prêt de tooget a démarré avec le stylet du test de vos applications hébergées dans Microsoft Azure ? Si tel est le cas, puis accédez toohello [vue d’ensemble du Test d’intrusion](https://technet.microsoft.com/library/mt784683.aspx) page (et cliquez sur le bouton Créer un test de demande bas hello de page de hello de hello. Vous trouverez également plus d’informations sur le stylet hello test des conditions générales et des liens utiles sur la façon dont vous pouvez signaler tooAzure connexes des failles de sécurité ou tout autre service Microsoft.
