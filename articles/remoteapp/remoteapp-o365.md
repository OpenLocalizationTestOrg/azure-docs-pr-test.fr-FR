---
title: "Utilisation d’Office avec Azure RemoteApp | Microsoft Docs"
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
ms.openlocfilehash: a776d877c764109f15c1025db2be3114eea2130a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="using-office-with-azure-remoteapp"></a>Utilisation d'Office avec Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .
> 
> 

Vous avez deux possibilités pour l'hébergement des applications Office dans Azure RemoteApp : Office 365 ProPlus ou la version d'évaluation d'Office 2013 Professionnel Plus.

**Bonjour, saviez-vous que nous avons un nouvel article amélioré qui va bientôt remplacer celui-ci ? Découvrez [Utilisation de votre abonnement Office 365 avec Azure RemoteApp](remoteapp-officesubscription.md). Il couvre toutes les informations dont vous avez besoin pour utiliser Office 365 + Azure RemoteApp.**

## <a name="office-365-proplus"></a>Office 365 ProPlus
Vous pouvez créer une collection RemoteApp à l'aide de l'image de modèle Office 365 ProPlus. Cette option vous permet d'étendre votre service Office 365 à RemoteApp. Vous devez déjà disposer d’un plan d’abonnement et vos utilisateurs doivent bénéficier d’une licence pour le service Office 365 ProPlus (en version autonome ou avec les plans de service Office 365).

RemoteApp prend en charge l'activation d’ordinateurs partagés Office 365. Quand vous autorisez l'activation d’ordinateurs partagés et que vous utilisez [l’outil de déploiement Office](http://www.microsoft.com/download/details.aspx?id=36778) pour l'installation, Office 365 ProPlus s'installe sans s'activer. Quand un utilisateur se connecte à une collection qui contient Office 365, Office vérifie s'il a été approvisionné pour Office 365 ProPlus. Si c'est le cas, Office active temporairement Office 365 ProPlus. Cette activation perdure tant que l'utilisateur ne se déconnecte pas du service.

Pour utiliser l'activation d’ordinateurs partagés Office 365, vous devez créer un [modèle personnalisé](remoteapp-create-custom-image.md) et y installer Office 365 ProPlus, en suivant [ces instructions](https://technet.microsoft.com/library/dn782858.aspx).

Vous pouvez gérer les licences Office 365 de vos utilisateurs dans le [portail d'administration Office 365](https://portal.office365.com/). En savoir plus sur les [plans de service Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx).  

## <a name="office-2013-professional-plus-trial"></a>Version d'évaluation d'Office Professionnel Plus 2013
Pendant la période d'évaluation de 30 jours de RemoteApp, vous pouvez utiliser l'image de modèle Office Professionnel Plus 2013 (version d'évaluation) pour créer une collection RemoteApp. Vous pouvez attribuer des utilisateurs à cette collection d'évaluation à l'aide de leurs comptes professionnels Azure Active Directory ou comptes Microsoft. Aucun abonnement supplémentaire n’est nécessaire.

C'est l'option idéale pour débuter et tester l'utilisation d'Office dans RemoteApp. Toutefois, cette option est destinée à des fins d'évaluation et de test uniquement. Les collections RemoteApp créées à l'aide de l'image de modèle Office Professionnel Plus 2013 (version d'évaluation) ne peuvent pas être passées en mode de production et seront désactivées à la fin de la période d'évaluation.

## <a name="switching-from-trial-to-production"></a>Passage de la version d'évaluation au mode de production
Quand vous commencez votre période d'évaluation gratuite de 30 jours, une note dans la section RemoteApp du portail vous indique combien de temps il vous reste avant de basculer sur un compte payant. Vous pouvez activer votre compte et passer en mode de production à l'aide du lien figurant dans cette note.

L'activation de votre compte concerne toutes les collections RemoteApp de votre compte.

* Les collections exécutées dans Windows Server 2012 R2 ou les images de modèle Office 365 ProPlus passent naturellement en mode de production. Tous les paramètres et données utilisateur, y compris les sessions en cours, restent intacts.
* Si vous avez téléchargé des images de modèle personnalisées, les collections qui utilisent ces images sont également transférées naturellement.
* L'image de modèle Office Professionnel Plus 2013 (version d'évaluation) est destinée à des fins d'évaluation uniquement. Les collections qui s'exécutent dans cette image de modèle ne peuvent pas être passées en mode de production. Elles sont mises en état « désactivé ».

Si vous ne passez pas en mode de production à l'expiration de votre version d'évaluation, vos collections RemoteApp sont désactivées. Ne vous inquiétez pas, vos paramètres et données utilisateur sont enregistrés pendant 90 jours supplémentaires, vous pouvez donc toujours activer votre service et passer en mode de production sans perte de données.

