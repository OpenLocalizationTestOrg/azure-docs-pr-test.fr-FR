---
title: "méthode de routage à l’aide de Azure Traffic Manager du trafic aaaConfigure priorité | Documents Microsoft"
description: "Cet article explique comment priorité de hello tooconfigure le trafic de la méthode de routage de Traffic Manager"
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
ms.openlocfilehash: dd3e3bb2a727e5ea087cee35962c8e6f7c357282
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-priority-traffic-routing-method-in-traffic-manager"></a>Configurer la méthode de routage du trafic prioritaire dans Traffic Manager

Quel que soit le mode de site Web hello, sites Web Azure fournissent déjà les fonctionnalités de basculement pour les sites Web au sein d’un centre de données (également appelé région). Traffic Manager assure le basculement pour des sites web dans différents centres de données.

Un modèle courant de basculement du service est le service principal de toosend trafic tooa et fournissent un ensemble identiques de services de sauvegarde pour le basculement. Hello étapes suivantes expliquent comment tooconfigure cela hiérarchisés basculement avec les sites Web et les services cloud Azure :

## <a name="tooconfigure-hello-priority-traffic-routing-method"></a>méthode de routage du trafic tooconfigure hello priorité

1. À partir d’un navigateur, connectez-vous toohello [portail Azure](http://portal.azure.com). Si vous ne possédez pas encore de compte, vous pouvez [vous inscrire pour bénéficier d’un essai gratuit d’un mois](https://azure.microsoft.com/free/). 
2. Dans la barre de recherche du portail hello, recherchez hello **profils Traffic Manager** puis cliquez sur nom du profil hello tooconfigure méthode de routage hello pour souhaitées.
3. Bonjour **profil Traffic Manager** panneau, vérifiez que les deux hello services de cloud computing et sites Web que vous souhaitez tooinclude dans votre configuration sont présents.
4. Bonjour **paramètres** , cliquez sur **Configuration**et Bonjour **Configuration** panneau, terminée, comme suit :
    1. Pour **paramètres de méthode de routage du trafic**, vérifiez que la méthode de routage du trafic hello est **priorité**. Si elle n’est pas le cas, cliquez sur **priorité** à partir de la liste déroulante de hello.
    2. Ensemble hello **paramètres du moniteur de point de terminaison** identiques pour tous les chaque point de terminaison dans ce profil comme suit :
        1. Sélectionnez hello approprié **protocole**et spécifiez hello **Port** nombre. 
        2. Pour **Chemin d’accès**, entrez une barre oblique */*. points de terminaison toomonitor, vous devez spécifier un chemin d’accès et le nom de fichier. Une barre oblique « / » est une entrée valide pour le chemin d’accès relatif de hello et implique que le fichier hello se trouve dans le répertoire racine de hello (par défaut).
        3. En hello haut hello, cliquez sur **enregistrer**.
5. Bonjour **paramètres** , cliquez sur **points de terminaison**.
6. Bonjour **points de terminaison** panneau, ordre de priorité hello révision pour vos points de terminaison. Lorsque vous sélectionnez hello **priorité** méthode de routage du trafic, hello ordre des points de terminaison hello sélectionné est important. Vérifiez l’ordre de priorité hello de points de terminaison.  point de terminaison principal Hello est visible. Vérifiez de nouveau sur la commande hello qu'il est affiché. toutes les demandes seront routés toohello le premier point de terminaison et si Traffic Manager détecte pas intègre, le trafic de hello bascule automatiquement toohello le prochain point de terminaison. 
7. toochange hello ordre de priorité de point de terminaison, cliquez sur le point de terminaison hello, hello et **point de terminaison** panneau s’affiche, cliquez sur **modifier** et modifiez hello **priorité** valeur en fonction des besoins . 
8. Cliquez sur **enregistrer** toosave modifier les paramètres de point de terminaison hello.
9. Après avoir effectué vos modifications de configuration, cliquez sur **enregistrer** bas hello de page de hello.
10. Testez les modifications hello dans votre configuration comme suit :
    1.  Dans la barre de recherche du portail hello, recherchez le nom du profil Traffic Manager hello et cliquez sur le profil Traffic Manager hello dans les résultats de hello que hello affiché.
    2.  Bonjour **Traffic Manager** panneau, cliquez sur **vue d’ensemble**.
    3.  Hello **profil Traffic Manager** panneau affiche le nom DNS de hello de votre profil Traffic Manager nouvellement créé. Cela peut servir par les clients (par exemple, en accédant à l’aide d’un navigateur web de tooit) tooget routé toohello droite point de terminaison tel que déterminé par le type de routage hello. Dans ce cas toutes les demandes sont routés toohello le premier point de terminaison et si Traffic Manager détecte pas intègre, le trafic de hello bascule automatiquement toohello le prochain point de terminaison.
11. Une fois que votre profil Traffic Manager fonctionne, vous pouvez modifier enregistrement DNS de hello sur votre toopoint de serveur DNS faisant autorité votre nom de domaine de société domaine nom toohello Traffic Manager.

![Configuration de la méthode de routage du trafic prioritaire à l’aide de Traffic Manager][1]

## <a name="next-steps"></a>Étapes suivantes


- En savoir plus sur la [méthode de routage du trafic par pondération](traffic-manager-configure-weighted-routing-method.md).
- En savoir plus sur la [méthode de routage basé sur les performances](traffic-manager-configure-performance-routing-method.md).
- En savoir plus sur la [méthode de routage géographique](traffic-manager-configure-geographic-routing-method.md).
- Découvrez comment trop[tester les paramètres de Traffic Manager](traffic-manager-testing-settings.md).

<!--Image references-->
[1]: ./media/traffic-manager-priority-routing-method/traffic-manager-priority-routing-method.png