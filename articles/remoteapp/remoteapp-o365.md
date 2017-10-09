---
title: aaaUsing Office avec Azure RemoteApp | Documents Microsoft
description: "Découvrez comment Office et Azure RemoteApp fonctionnent ensemble"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: f1773baf-8aa1-423c-a2f9-e4679e0463d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d065c1a0a2191c9e2e405264a835cecf791d6ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-office-with-azure-remoteapp"></a>Utilisation d'Office avec Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Vous avez deux possibilités pour l'hébergement des applications Office dans Azure RemoteApp : Office 365 ProPlus ou la version d'évaluation d'Office 2013 Professionnel Plus.

**Bonjour, saviez-vous que nous avons un nouvel article amélioré qui va bientôt remplacer celui-ci ? Extraire [comment toouse votre abonnement Office 365 avec Azure RemoteApp](remoteapp-officesubscription.md). Elle traite toutes les informations de hello que vous avez besoin pour l’utilisation d’Office 365 + Azure RemoteApp.**

## <a name="office-365-proplus"></a>Office 365 ProPlus
Vous pouvez créer une collection RemoteApp à l’aide d’image de modèle Office 365 ProPlus hello. Cette option vous permet de tooextend votre tooRemoteApp du service Office 365. Vous devez disposer d’un plan d’abonnement existant et que vos utilisateurs doivent avoir une licence pour hello service Office 365 ProPlus, soit autonome ou par le biais des plans de service hello Office 365.

RemoteApp prend en charge l'activation d’ordinateurs partagés Office 365. Lorsque vous activez l’activation de l’ordinateur partagé et que vous utilisez hello [outil de déploiement Office](http://www.microsoft.com/download/details.aspx?id=36778) pour l’installation, Office 365 ProPlus installe sans être activé. Lorsqu’un utilisateur s’inscrit dans une collection qui contient d’Office 365, Office vérifie toosee si l’utilisateur de hello a été configuré pour Office 365 ProPlus. Si, par conséquent, Office active temporairement Office 365 ProPlus - cette activation persiste jusqu'à ce que ce signe utilisateurs hors service de hello.

toouse activation de l’ordinateur Office 365 partagé, vous devez toocreate une [modèle personnalisé](remoteapp-create-custom-image.md) et installer Office 365 ProPlus suivant, [ces instructions](https://technet.microsoft.com/library/dn782858.aspx).

Vous pouvez gérer les licences d’Office 365 de vos utilisateurs à hello [portail d’administration Office 365](https://portal.office365.com/). En savoir plus sur les [plans de service Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx).  

## <a name="office-2013-professional-plus-trial"></a>Version d'évaluation d'Office Professionnel Plus 2013
Au cours d’une version d’évaluation de 30 jours de RemoteApp, vous pouvez utiliser hello Office 2013 Professionnel Plus (version d’évaluation) modèle image toocreate une collection RemoteApp. Vous pouvez affecter des utilisateurs toothis collection d’évaluation à l’aide de leurs comptes de travail Azure Active Directory ou des comptes Microsoft. Aucun abonnement supplémentaire n’est nécessaire.

Ceci est un pneus de hello tookick option intéressante et obtenir une bonne idée Office de RemoteApp. Toutefois, cette option est destinée à des fins d'évaluation et de test uniquement. Les collections RemoteApp créées à l’aide d’image de modèle hello Office 2013 Professionnel Plus (version d’évaluation) ne peut pas être passé tooproduction mode et seront désactivées à la fin de hello de période d’évaluation de hello.

## <a name="switching-from-trial-tooproduction"></a>Basculement à partir de la version d’évaluation tooproduction
Lorsque vous démarrez votre version d’évaluation gratuite de 30 jours, une note dans hello section RemoteApp du portail de hello vous indiquent la durée pendant laquelle vous avez laissées dans la version d’évaluation hello avant tooa tootransition payé compte. Vous pouvez activer le mode tooproduction votre compte et le commutateur à l’aide du lien de hello dans cette note.

Lorsque vous activez votre compte, cela affectera toutes les collections de RemoteApp hello dans votre compte.

* Les collections qui sont en cours d’exécution avec hello Windows Server 2012 R2 ou des images de modèle Office 365 ProPlus hello passera tooproduction en toute transparence. Tous les paramètres et données utilisateur, y compris les sessions en cours, restent intacts.
* Si vous avez téléchargé des images de modèle personnalisées, les collections qui utilisent ces images sont également transférées naturellement.
* image de modèle Hello Office 2013 Professionnel Plus (version d’évaluation) est prévu pour évaluation uniquement. Collections qui s’exécutent avec cette image de modèle ne peut pas être tooproduction passée. Elles sont mises en état « désactivé ».

Si vous ne pas passer tooproduction mode par expiration hello de votre période d’évaluation, vos collections RemoteApp seront désactivées. Ne vous inquiétez pas, vos paramètres et les données des utilisateurs sont enregistrées pour une autre 90 jours, donc vous pouvez toujours l’activer le mode de tooproduction service et le commutateur sans perte de données.

