---
title: "aaaHow tootroubleshoot des problèmes courants lors de la création du disque dur virtuel | Documents Microsoft"
description: "Résolution des problèmes toocommon des réponses aux questions et problèmes lors de la création du disque dur virtuel."
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: 
editor: 
ms.assetid: e39563d8-8646-4cb7-b078-8b10ac35b494
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 09/26/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: e4ff09a979bdf575badff2d33f2299abb17c947d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-common-issues-encountered-during-vhd-creation"></a>Comment tootroubleshoot les problèmes courants rencontrés lors de la création du disque dur virtuel
Cet article est toohelp a fourni un serveur de publication Azure Marketplace et/ou un coadministrateur peut rencontrer un problème ou avez des questions courantes lors de la publication ou la gestion de leurs solutions de machine virtuelle.

1. Comment modifier le nom hello d’hôte de hello ?
   
    Une fois que la machine virtuelle est créée, les utilisateurs ne peut pas mettre à jour le nom hello d’hôte de hello.
2. Comment tooreset hello service Bureau à distance ou son mot de passe de connexion ?
   
   * [Référence pour les machines virtuelles Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-reset-rdp/)
   * [Référence pour les machines virtuelles Linux](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)
3. Utilisation toogenerate nouveau ssh des certificats ?
   
   Consultez le lien de toohello : [https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)
4. Comment tooconfigure un certificat VPN de l’ouvrir ?
   
   Consultez le lien de toohello : [https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/)
5. Quelle est la politique de support hello pour l’exécution du logiciel serveur Microsoft dans un environnement de machine virtuelle Microsoft Azure hello (infrastructure-as-a-service) ?
   
   Consultez le lien de toohello : [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)
6. Les machines virtuelles ont-elles un identificateur unique ?
   
   Azure encode l’ID unique de machine virtuelle Azure dans chaque machine virtuelle. Pour plus d’informations, consultez le blog et la documentation.
7. Dans une machine virtuelle comment puis-je gérer extension de script personnalisé hello dans la tâche de démarrage hello ?
   
   Consultez le lien de toohello : [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/)
8. Comment toocreate une machine virtuelle à partir du portail Azure à l’aide de hello hello disque dur virtuel qui est téléchargé toopremium stockage ?
   
   Nous ne prenons pas encore en charge cette fonctionnalité.
9. Une application 32 bits est pris en charge dans Azure Marketplace de hello ?
   
   Pour plus d’informations sur la politique de support hello, consultez toohello lien : [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)
10. Chaque fois que j’essaie de toocreate une image à partir de mes disques durs virtuels, j’obtiens l’erreur de hello ». Disque dur virtuel est déjà inscrit avec le référentiel d’images en tant que ressource de hello » dans PowerShell. Je n’ai pas créé d’image au préalable et je n’ai trouvé aucune image portant ce nom dans Azure. Comment résoudre ce problème ?
    
    Généralement, cela se produire si l’utilisateur de hello configuré une machine virtuelle à partir de ce disque dur virtuel et qu’il existe un verrou sur ce disque dur virtuel. Vérifiez qu’aucune machine virtuelle n’est allouée à partir de ce disque dur virtuel. Si les erreurs hello persistent, veuillez déclenchent un ticket de support à l’aide de ce lien, ou à partir de hello publication portail relatives (les détails sont indiquées dans la réponse de question 11 hello).
