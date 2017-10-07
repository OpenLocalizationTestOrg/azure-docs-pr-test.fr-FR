---
title: "méthode de routage à l’aide de Azure Traffic Manager alternée aaaConfigure pondérée du trafic | Documents Microsoft"
description: "Cet article explique comment tooload équilibrer le trafic à l’aide d’une méthode du tourniquet dans Traffic Manager"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 6dca6de1-18f7-4962-bd98-6055771fab22
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: kumud
ms.openlocfilehash: 7e2866ead0b2b653845435dd420a763c5e175f4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-weighted-traffic-routing-method-in-traffic-manager"></a>Configurer les méthode de routage de trafic hello pondérée dans Traffic Manager

Un modèle commun méthode de routage du trafic est tooprovide un ensemble de points de terminaison identiques, qui incluent des services de cloud computing et sites Web et envoyer le trafic tooeach de manière alternée. Hello suit montrer comment tooconfigure ce type de méthode de routage du trafic.

> [!NOTE]
> Azure Websites fournit déjà des fonctionnalités d’équilibrage de charge de tourniquet pour les sites web dans un centre de données (également appelé région). Traffic Manager vous permet de méthode de routage du trafic de tourniquet toospecify pour les sites Web dans différents centres de données.

## <a name="tooconfigure-hello-weighted-traffic-routing-method"></a>méthode de routage du trafic tooconfigure hello pondérée

1. À partir d’un navigateur, connectez-vous toohello [portail Azure](http://portal.azure.com). Si vous ne possédez pas encore de compte, vous pouvez [vous inscrire pour bénéficier d’un essai gratuit d’un mois](https://azure.microsoft.com/free/). 
2. Dans la barre de recherche du portail hello, recherchez hello **profils Traffic Manager** puis cliquez sur nom du profil hello tooconfigure méthode de routage hello pour souhaitées.
3. Bonjour **profil Traffic Manager** panneau, vérifiez que les deux hello services de cloud computing et sites Web que vous souhaitez tooinclude dans votre configuration sont présents.
4. Bonjour **paramètres** , cliquez sur **Configuration**et Bonjour **Configuration** panneau, terminée, comme suit :
    1. Pour **paramètres de méthode de routage du trafic**, vérifiez que la méthode de routage du trafic hello est **Weighted**. Si elle n’est pas le cas, cliquez sur **Weighted** à partir de la liste déroulante de hello.
    2. Ensemble hello **paramètres du moniteur de point de terminaison** identiques pour tous les chaque point de terminaison dans ce profil comme suit :
        1. Sélectionnez hello approprié **protocole**et spécifiez hello **Port** nombre. 
        2. Pour **Chemin d’accès**, entrez une barre oblique */*. points de terminaison toomonitor, vous devez spécifier un chemin d’accès et le nom de fichier. Une barre oblique « / » est une entrée valide pour le chemin d’accès relatif de hello et implique que le fichier hello se trouve dans le répertoire racine de hello (par défaut).
        3. En hello haut hello, cliquez sur **enregistrer**.
5. Testez les modifications hello dans votre configuration comme suit :
    1.  Dans la barre de recherche du portail hello, recherchez le nom du profil Traffic Manager hello et cliquez sur le profil Traffic Manager hello dans les résultats de hello que hello affiché.
    2.  Bonjour **Traffic Manager** panneau, cliquez sur **vue d’ensemble**.
    3.  Hello **profil Traffic Manager** panneau affiche le nom DNS de hello de votre profil Traffic Manager nouvellement créé. Cela peut servir par les clients (par exemple, en accédant à l’aide d’un navigateur web de tooit) tooget routé toohello droite point de terminaison tel que déterminé par le type de routage hello. Dans ce cas, toutes les demandes sont routées vers chaque point de terminaison de manière alternée.
6. Une fois que votre profil Traffic Manager fonctionne, vous pouvez modifier enregistrement DNS de hello sur votre toopoint de serveur DNS faisant autorité votre nom de domaine de société domaine nom toohello Traffic Manager.

![Configuration de la méthode de routage du trafic par pondération à l’aide de Traffic Manager][1]

## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur la [méthode de routage du trafic prioritaire](traffic-manager-configure-priority-routing-method.md).
- En savoir plus sur la [méthode de routage du trafic basé sur les performances](traffic-manager-configure-performance-routing-method.md).
- En savoir plus sur la [méthode de routage géographique](traffic-manager-configure-geographic-routing-method.md).
- Découvrez comment trop[tester les paramètres de Traffic Manager](traffic-manager-testing-settings.md).

<!--Image references-->
[1]: ./media/traffic-manager-weighted-routing-method/traffic-manager-weighted-routing-method.png
