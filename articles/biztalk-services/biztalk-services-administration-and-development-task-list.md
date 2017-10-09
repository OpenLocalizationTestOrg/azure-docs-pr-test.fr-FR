---
title: "aaaAdministration et liste des tâches de développement dans BizTalk Services | Documents Microsoft"
description: "Documentation de travail et de planification pour le déploiement d'Azure BizTalk Services."
services: biztalk-services
documentationcenter: 
author: msftman
manager: erikre
editor: 
ms.assetid: 0ab70b5b-1a88-4ba5-b329-ec51b785010e
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2016
ms.author: deonhe
ms.openlocfilehash: 544c6b23fcbc2267598b713dbe1626699099d181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="administration-and-development-task-list-in-biztalk-services"></a>Liste des tâches d'administration et de développement dans BizTalk Services

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

## <a name="getting-started"></a>Mise en route
Lorsque vous travaillez avec Microsoft Azure BizTalk Services, il existe plusieurs tooconsider des composants basés sur le cloud et locaux. tooget démarré, envisagez de hello suivant du flux de processus :  

| Étape | Qui est responsable | Task | Liens connexes |
| --- | --- | --- | --- |
| 1. |Administrateur |Créer hello abonnement Microsoft Azure à l’aide d’un compte Microsoft ou un compte professionnel |[portail Azure Classic](http://go.microsoft.com/fwlink/p/?LinkID=213885) |
| 2. |Administrateur |Créer ou approvisionner un BizTalk Service. |[Créer un BizTalk Service à l'aide du portail Azure Classic](http://go.microsoft.com/fwlink/p/?LinkID=302280) |
| 3. |Administrateur |Enregistrer votre déploiement ou le déploiement de votre entreprise de BizTalk Services |[L’inscription et la mise à jour d’un déploiement de Service BizTalk sur hello portail BizTalk Services](https://msdn.microsoft.com/library/azure/hh689837.aspx) |
| 4. |Administrateur |S’applique si l’application hello utilise le système de Service d’adaptateur BizTalk tooconnect tooan local de métier (LOB) ou une file d’attente de Destination ou de rubrique.  Créer hello Azure Service Bus Namespace. Donnez à cet espace de noms, nom de l’émetteur de Bus de Service et developer de toohello de valeurs de clé de l’émetteur de Bus de Service. |[Procédure : Créer ou modifier un espace de noms du service Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md) et [Obtenir les valeurs nom et clé de l’émetteur](biztalk-issuer-name-issuer-key.md) |
| 5. |Développeur |Installer hello SDK et créer hello projet de BizTalk Service dans Visual Studio. |[Installer le Kit de développement logiciel (SDK) Azure BizTalk Services](https://msdn.microsoft.com/library/azure/hh689760.aspx) et [Créer des points de terminaison de messagerie enrichis sur Azure](https://msdn.microsoft.com/library/azure/hh689766.aspx) |
| 6. |Développeur |Déployer votre tooyour de projet de BizTalk Service que service BizTalk hébergé sur Azure. |[Déploiement et actualisation hello projet BizTalk Services](https://msdn.microsoft.com/library/azure/hh689881.aspx) |
| 7. |Administrateur |S'applique si vous utilisez EDI.  Vous pouvez ajouter des partenaires et créer des accords sur hello portail Microsoft Azure BizTalk Services. Lorsque vous créez un accord, vous pouvez ajouter des transformations créées par les paramètres de l’accord toohello hello développeur et/ou de pont de hello. |[Configuration d'EDI, AS2 et EDIFACT sur le portail BizTalk Services](https://msdn.microsoft.com/library/azure/hh689853.aspx) |
| 8. |Administrateur |Hello portail Azure classic, de surveiller la santé de votre BizTalk Service, y compris les mesures de performances hello. |[Onglets Tableau de bord, Surveiller et Mettre à l'échelle dans BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302281) |
| 9. |Administrateur |Hello portail Microsoft Azure BizTalk Services, de gérer les artefacts hello utilisés par les Services BizTalk et le suivi des messages qu’ils sont traités par les fichiers de pont hello. |[À l’aide de hello portail BizTalk Services](https://msdn.microsoft.com/library/azure/dn874043.aspx) |
| 10. |Administrateur |Créer un tooback de plan de sauvegarde des hello BizTalk Service. |[Continuité des activités et récupération d'urgence dans BizTalk Services](https://msdn.microsoft.com/library/azure/dn509557.aspx) |

## <a name="next-steps"></a>Étapes suivantes
[Didacticiels et exemples](https://msdn.microsoft.com/library/azure/hh689895.aspx)

[Créez un projet de hello dans Visual Studio](https://msdn.microsoft.com/library/azure/hh689811.aspx)

[Installer le Kit de développement logiciel (SDK) Azure BizTalk Services](https://msdn.microsoft.com/library/azure/hh689760.aspx)

## <a name="concepts"></a>Concepts
[Créez un projet de hello dans Visual Studio](https://msdn.microsoft.com/library/azure/hh689811.aspx)  
[EDI, AS2 et EDIFACT (entreprise tooBusiness) de messagerie](https://msdn.microsoft.com/library/azure/hh689898.aspx)  

## <a name="other-resources"></a>Autres ressources
[Ajouter des points de terminaison de messagerie source, destination et pont](https://msdn.microsoft.com/library/azure/hh689877.aspx)  
[Découvrir et créer des tables et des transformations de messages](https://msdn.microsoft.com/library/azure/hh689905.aspx)  
[À l’aide de hello Service d’adaptateur BizTalk (BAS)](https://msdn.microsoft.com/library/azure/hh689889.aspx)  
[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=303664)

