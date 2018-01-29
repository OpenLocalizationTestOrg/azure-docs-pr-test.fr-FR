---
title: "Mesures des utilisateurs réels dans Azure Traffic Manager avec des pages web | Microsoft Docs"
description: "Configurez vos pages web pour envoyer les mesures des utilisateurs réels à Traffic Manager."
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: jeconnoc
editor: 
tags: 
ms.assetid: 
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 09/19/2017
ms.author: kumud
ms.custom: 
ms.openlocfilehash: 7f4088cf4470b1f9fa22c4ec83a9f92657032734
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/23/2018
---
# <a name="how-to-send-real-user-measurements-to-azure-traffic-manager-using-web-pages"></a>Comment envoyer les mesures des utilisateurs réels à Azure Traffic Manager avec des pages web

>[!NOTE]
>La fonctionnalité Mesures des utilisateurs réels dans Traffic Manager est en préversion publique. Il se peut qu’elle n’offre pas les mêmes niveaux de disponibilité et de fiabilité que les fonctionnalités de la version mise à la disposition générale. Cette fonctionnalité n’est pas prise en charge, est susceptible de disposer de possibilités limitées et peut ne pas être disponible à certains emplacements Azure. Pour les notifications les plus récentes sur la disponibilité et l’état de cette fonctionnalité, consultez la page relative aux [mises à jour d’Azure Traffic Manager](https://azure.microsoft.com/updates/?product=traffic-manager).

Vous pouvez configurer vos pages web pour envoyer des mesures d’utilisateurs réels à Traffic Manager en obtenant une clé de mesures des utilisateurs réels et en incorporant le code généré dans la page web.

## <a name="obtain-a-real-user-measurements-key"></a>Obtenir une clé de mesures des utilisateurs réels

Les mesures que vous prenez et envoyez à Traffic Manager à partir de votre application cliente sont identifiées par le service à l’aide d’une chaîne unique, que l’on nomme **clé de mesures des utilisateurs réels**. Vous pouvez obtenir une clé de mesures des utilisateurs réels via le portail Azure, une API REST, PowerShell ou Azure CLI.

Pour obtenir la clé de mesures des utilisateurs réels à l’aide du portail Azure :
1. Dans un navigateur, connectez-vous au portail Azure. Si vous n’avez pas encore de compte, vous pouvez vous inscrire pour bénéficier d’un essai gratuit d’un mois.
2. Dans la barre de recherche du portail, recherchez le nom du profil Traffic Manager que vous souhaitez modifier, puis cliquez sur le profil Traffic Manager dans les résultats affichés.
3. Dans le panneau du profil Traffic Manager, cliquez sur **Mesures des utilisateurs réels** sous **Paramètres**.
4. Cliquez sur **Générer une clé** pour créer une clé de mesures des utilisateurs réels.
 
  ![Générer une clé de mesures des utilisateurs réels](./media/traffic-manager-create-rum-visual-studio/generate-rum-key.png)

   **Figure 1 : Génération de la clé de mesures des utilisateurs réels**

5. Le panneau affiche maintenant la clé de mesures des utilisateurs réels générée et un extrait de code JavaScript qui doit être incorporé à votre page HTML.
 
    ![Code JavaScript pour la clé de mesures des utilisateurs réels](./media/traffic-manager-create-rum-web-pages/rum-javascript-code.png)

    **Figure 2 : Clé de mesures des utilisateurs réels et code JavaScript de mesure**
 
6.  Cliquez sur le bouton **Copier** pour copier le code JavaScript. 

>[!IMPORTANT]
> Utilisez le code JavaScript généré pour que la fonctionnalité Mesures des utilisateurs réels fonctionne correctement. Toute modification apportée à ce script ou aux scripts utilisés par la fonctionnalité Mesures des utilisateurs réels peut entraîner un comportement imprévisible.

## <a name="embed-the-code-to-an-html-web-page"></a>Incorporer le code à une page web HTML

Une fois que vous avez obtenu la clé de mesures des utilisateurs réels, l’étape suivante consiste à incorporer le code JavaScript copié dans une page HTML que consultent vos utilisateurs. La modification du code HTML peut être effectuée de nombreuses façons, à l’aide de différents outils et flux de travail. Cet exemple montre comment mettre à jour une page HTML pour ajouter ce script. Vous pouvez utiliser ces instructions pour l’adapter à votre flux de travail de gestion du code source HTML.

1.  Ouvrez la page HTML dans un éditeur de texte.
2.  Collez le code JavaScript que vous avez copié à l’étape précédente dans le corps du code HTML (le code copié se trouve sur les lignes 8 et 9, voir figure 3).
 
    ![Incorporer du code JavaScript dans une page web pour les mesures des utilisateurs réels](./media/traffic-manager-create-rum-web-pages/real-user-measurement-embed-script.png)  

    **Figure 3 : Code HTML simple auquel est incorporé du code JavaScript pour les mesures des utilisateurs réels**

3.  Enregistrez le fichier HTML.
4. La prochaine fois que cette page est affichée dans un navigateur web, le code JavaScript référencé est téléchargé et le script exécute les opérations de mesure et de création de rapports.


## <a name="next-steps"></a>étapes suivantes
- En savoir plus sur les [mesures des utilisateurs réels](traffic-manager-rum-overview.md).
- En savoir plus sur le [fonctionnement de Traffic Manager](traffic-manager-overview.md)
- En savoir plus sur les [méthodes de routage du trafic](traffic-manager-routing-methods.md) prises en charge par Traffic Manager
- En savoir plus sur la [création d’un profil Traffic Manager](traffic-manager-create-profile.md)

