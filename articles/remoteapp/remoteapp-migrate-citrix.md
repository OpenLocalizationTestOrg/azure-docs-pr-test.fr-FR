---
title: "aaaMigrate à partir d’Azure RemoteApp tooCitrix XenApp Essentials | Documents Microsoft"
description: "Comment toomigrate à partir d’Azure RemoteApp tooCitrix XenApp Essentials"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 695a8165-3454-4855-8e21-f2eb2c61201b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aa3ce28bc5a86d5b1dd3408196d51935395f55c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-azure-remoteapp-toocitrix-xenapp-essentials"></a>Migrer à partir d’Azure RemoteApp tooCitrix XenApp Essentials

Si vous utilisez Azure RemoteApp et toomigrate tooCitrix XenApp Essentials, il existe quelques conditions préalables tookeep à l’esprit. Pour commencer, lisez le [guide de déploiement technique pas à pas de Citrix XenApp Essentials](https://docs.citrix.com/content/dam/docs/en-us/citrix-cloud/downloads/xenapp-essentials-deployment-guide.pdf), ainsi que la [bibliothèque technique en ligne](http://docs.citrix.com/en-us/citrix-cloud/xenapp-and-xendesktop-service/xenapp-essentials.html) de Citrix. 

## <a name="prerequisite-steps-for-migration"></a>Étapes préalable à la migration

1. Créez un réseau virtuel ou déterminez le réseau virtuel Azure Resource Manager sur lequel vous allez déployer Citrix XenApp Essentials. Azure RemoteApp utilise hello portail classique Azure ; Citrix XenApp Essentials prend uniquement en charge Azure Resource Manager.  
2. Vérifiez ce réseau virtuel hello que vous avez sélectionné est mise en réseau du contrôleur de domaine accès tooyour, étant donné que Citrix prend uniquement en charge les déploiements hybrides. Si vous utilisez un déploiement de cloud d’Azure RemoteApp, vérifiez que votre réseau virtuel a une mise en réseau du contrôleur de domaine Active Directory access tooan. Vous pouvez aussi utiliser Azure Active Directory Domain Services (Azure AD DS). 
3. Assurez-vous que DNS est correctement configuré pour le réseau virtuel de hello, afin que jonction de domaine réussit à votre première tentative de hello. Vous pouvez créer un ordinateur virtuel (VM) dans le réseau virtuel de hello sélectionné et effectuer une tooverify de jointure de domaine manuelle que hello DNS et la jonction de domaine fonctionne comme prévu. Cela garantit que vous êtes hello réussie première fois que vous déployez Citrix XenApp Essentials. 
4. Si nécessaire, créez une homologation de réseau virtuel entre un réseau virtuel du portail Azure Classic que vous utilisez avec Azure RemoteApp et votre réseau virtuel Azure Resource Manager. Ce processus d’homologation fonctionne si les réseaux hello deux trouvent sur hello même région. Si ce n’est pas le cas, utilisez des réseaux virtuels de site à site VPN tooconnect hello de mise en réseau. 
5. Si nécessaire, en lecture [comment toomigrate des données dans et hors d’Azure RemoteApp](remoteapp-migrate.md). 
6. Mettre à jour votre hello de tooinclude image Azure RemoteApp existant composant de Citrix VDA (pour obtenir des instructions, consultez la documentation de Citrix hello). 
7. Accédez toohello Azure Marketplace et commencer le déploiement de Citrix XenApp Essentials.

## <a name="other-considerations"></a>Autres points à considérer

Tenez compte des hello suivant des considérations supplémentaires lors de la migration :
- Citrix XenApp Essentials prend uniquement en charge les déploiements hybrides. En d’autres termes, il nécessite le contrôleur de domaine réseau accès tooa de jonction de domaine tooperform de commande. Si vous utilisez un déploiement de cloud d’Azure RemoteApp, utiliser Azure AD DS, ou vous assurer que votre réseau virtuel a accès tooActive active pour la jonction de domaine. 
- toolearn toomove utilisateur données tooCitrix XenApp Essentials, voir [comment toomigrate des données dans et hors d’Azure RemoteApp](remoteapp-migrate.md). 
- Citrix XenApp Essentials prend uniquement en charge les comptes Active Directory. Il ne prend pas en charge les comptes Microsoft (comme outlook.com, msn.com ou hotmail.com). 

## <a name="citrix-xenapp-essentials-billing"></a>Facturation de Citrix XenApp Essentials

Pour plus d’informations sur la tarification, consultez hello [FAQ](https://www.citrix.com/global-partners/microsoft/resources/xenapp-essentials-faq.html#tab-30699) et [l’article de vue d’ensemble de Citrix](https://www.citrix.com/global-partners/microsoft/remote-app.html). Il existe trois composants facturation tooCitrix XenApp Essentials :

- Hello Citrix service frais, 12 $ par utilisateur par mois. Comme tous les achats Azure Marketplace, il s’agit de facturation toohello de paiement associé à votre abonnement Azure. Les clients titulaires d’un Contrat Entreprise (EA) ne peuvent pas avoir recours au crédit financier Azure. 
- Licences d’accès client (CAL) Remote Data Service (RDS). Actuellement, vous pouvez acheter hello frais accès à distance fourni avec hello paiement de Citrix XenApp Essentials pour $6,25. Si vous êtes un client EA, vous pouvez utiliser les crédits Azure toopay pour ce. Si vous souhaitez toouse vos licences existantes, contactez-nous à l’adresse [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com), de sorte que nous pouvons appliquer cette facture tooyour. 
- Calcul et stockage Azure. C’est le coût du stockage Azure hello et la consommation de calcul pour les machines virtuelles hello consommée. N’oubliez pas de prendre la tarification en considération lors de la sélection de la taille de votre machine virtuelle et de la densité des utilisateurs. Si vous êtes un client EA, vous pouvez utiliser les crédits Azure toopay pour ce.

Si vous vous posez encore des questions :
- Envoyez-nous un e-mail à l’adresse [arainfo@microsoft.com](mailto:arainfo@microsoft.com).
- [Contactez le support Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Commencez par [ouverture d’un cas de support Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toohelp avec la condition préalable les étapes 1 à 5. Pour connaître les étapes 6 et 7, contactez Citrix en ouvrant un ticket de support dans le portail de gestion de Citrix hello. 
