---
title: "méthode de routage à l’aide de Azure Traffic Manager du trafic aaaConfigure performances | Documents Microsoft"
description: Cet article explique comment tooconfigure Traffic Manager tooroute trafic toohello le point de terminaison avec une latence plus faible
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
ms.openlocfilehash: d0ccd4c9de411844c6f36068859265244f4aa52b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-performance-traffic-routing-method"></a>Configurer la méthode de routage du trafic hello performances

Hello, méthode de routage de trafic de performances vous permet de point de terminaison toodirect trafic toohello avec une latence plus faible à partir du réseau du client hello hello. En règle générale, hello de centre de données avec une latence plus faible hello est hello le plus proche dans la distance géographique. Cette méthode de routage du trafic ne peut pas prendre en compte des modifications en temps réel de la configuration ou de la charge du réseau.

##  <a name="tooconfigure-performance-routing-method"></a>méthode de routage de performances tooconfigure

1. À partir d’un navigateur, connectez-vous toohello [portail Azure](http://portal.azure.com). Si vous ne possédez pas encore de compte, vous pouvez [vous inscrire pour bénéficier d’un essai gratuit d’un mois](https://azure.microsoft.com/free/). 
2. Dans la barre de recherche du portail hello, recherchez hello **profils Traffic Manager** puis cliquez sur nom du profil hello tooconfigure méthode de routage hello pour souhaitées.
3. Bonjour **profil Traffic Manager** panneau, vérifiez que les deux hello services de cloud computing et sites Web que vous souhaitez tooinclude dans votre configuration sont présents.
4. Bonjour **paramètres** , cliquez sur **Configuration**et Bonjour **Configuration** panneau, terminée, comme suit :
    1. Pour les **paramètres de la méthode de routage du trafic**, pour la **méthode de routage** sélectionnez **Performances**.
    2. Ensemble hello **paramètres du moniteur de point de terminaison** identiques pour tous les chaque point de terminaison dans ce profil comme suit :
        1. Sélectionnez hello approprié **protocole**et spécifiez hello **Port** nombre. 
        2. Pour **Chemin d’accès**, entrez une barre oblique */*. points de terminaison toomonitor, vous devez spécifier un chemin d’accès et le nom de fichier. Une barre oblique « / » est une entrée valide pour le chemin d’accès relatif de hello et implique que le fichier hello se trouve dans le répertoire racine de hello (par défaut).
        3. En hello haut hello, cliquez sur **enregistrer**.
5.  Testez les modifications hello dans votre configuration comme suit :
    1.  Dans la barre de recherche du portail hello, recherchez le nom du profil Traffic Manager hello et cliquez sur le profil Traffic Manager hello dans les résultats de hello que hello affiché.
    2.  Bonjour **Traffic Manager** panneau, cliquez sur **vue d’ensemble**.
    3.  Hello **profil Traffic Manager** panneau affiche le nom DNS de hello de votre profil Traffic Manager nouvellement créé. Cela peut servir par les clients (par exemple, en accédant à l’aide d’un navigateur web de tooit) tooget routé toohello droite point de terminaison tel que déterminé par le type de routage hello. Dans ce cas, toutes les demandes sont routés toohello le point de terminaison avec une latence plus faible à partir du réseau du client hello hello.
6. Une fois que votre profil Traffic Manager fonctionne, vous pouvez modifier enregistrement DNS de hello sur votre toopoint de serveur DNS faisant autorité votre nom de domaine de société domaine nom toohello Traffic Manager.

![Configuration de la méthode de routage du trafic selon les performances à l’aide de Traffic Manager][1]

## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur la [méthode de routage du trafic par pondération](traffic-manager-configure-weighted-routing-method.md).
- En savoir plus sur la [méthode de routage prioritaire](traffic-manager-configure-priority-routing-method.md).
- En savoir plus sur la [méthode de routage géographique](traffic-manager-configure-geographic-routing-method.md).
- Découvrez comment trop[tester les paramètres de Traffic Manager](traffic-manager-testing-settings.md).

<!--Image references-->
[1]: ./media/traffic-manager-performance-routing-method/traffic-manager-performance-routing-method.png