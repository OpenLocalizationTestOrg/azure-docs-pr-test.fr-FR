---
title: "paramètres de Azure Traffic Manager aaaVerify | Documents Microsoft"
description: "Cet article vous aide à vérifier les paramètres Traffic Manager."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 2180b640-596e-4fb2-be59-23a38d606d12
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: c670be6cf55e140c7ab63d5d526de08e14774d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="verify-traffic-manager-settings"></a>Vérifier les paramètres Traffic Manager

tootest vos paramètres Traffic Manager, vous devez toohave plusieurs clients dans différents emplacements, à partir de laquelle vous pouvez exécuter vos tests. Ensuite, mettez les points de terminaison hello dans votre profil Traffic Manager à la fois.

* Hello valeur DNS TTL une valeur faible afin que les modifications se propagent rapidement (par exemple, 30 secondes).
* Obtenir des adresses IP de vos services cloud Azure et les sites Web dans le profil hello que vous testez hello.
* Utiliser les outils qui vous permettent de résoudre l’adresse IP tooan du nom DNS et d’afficher cette adresse.

Vous êtes en train de toosee que les noms DNS hello résoudre tooIP les adresses de points de terminaison hello dans votre profil. les noms Hello doivent se résoudre en accord avec la méthode de routage du trafic hello définie dans le profil Traffic Manager de hello. Vous pouvez utiliser des outils de hello comme **nslookup** ou **Explorer** tooresolve les noms DNS.

Hello exemples suivants vous aident à tester votre profil Traffic Manager.

### <a name="check-traffic-manager-profile-using-nslookup-and-ipconfig-in-windows"></a>Vérifier le profil Traffic Manager à l’aide de nslookup et ipconfig dans Windows

1. Ouvrez une commande ou une invite de commandes Windows PowerShell en tant qu’administrateur.
2. Type `ipconfig /flushdns` tooflush hello cache de résolution DNS.
3. Saisissez `nslookup <your Traffic Manager domain name>`. Par exemple, hello commande vérifications hello nom de domaine avec préfixe de hello suivante *myapp.contoso*

        nslookup myapp.contoso.trafficmanager.net

    Un résultat classique montre hello informations suivantes :

    + Hello nom DNS et adresse IP du serveur hello DNS en cours accessibles tooresolve ce nom de domaine Traffic Manager.
    + nom de domaine Traffic Manager Hello tapé sur la ligne de commande hello après « nslookup » et domaine Traffic Manager de hello IP adresse toowhich hello est résolue. adresse IP de la deuxième Hello est un toocheck important de hello. Elle doit correspondre à une public adresse IP virtuelle (VIP) pour un des services de cloud computing hello ou sites Web hello profil Traffic Manager que vous testez.

## <a name="how-tootest-hello-failover-traffic-routing-method"></a>Comment tootest hello basculement du trafic de la méthode de routage

1. Laissez tous les points de terminaison en fonction.
2. À partir d’un même client, demandez la résolution DNS du nom de domaine de votre entreprise à l’aide de l’outil nslookup.exe ou d’un utilitaire similaire.
3. Vérifiez que hello résolu l’adresse IP correspond au point de terminaison principal hello.
4. Entraîne la défaillance de votre point de terminaison principal ou supprimez les hello analyse fichier afin de Traffic Manager juge qui hello application est arrêté.
5. Attendez que hello DNS Time-to-Live (TTL) du profil Traffic Manager de hello plus de deux minutes supplémentaires. Par exemple, si la TTL de votre DNS est de 300 secondes (5 minutes), vous devez attendre 7 minutes.
6. Videz le cache de votre client DNS et demandez une résolution DNS à l’aide de nslookup. Dans Windows, vous pouvez vider votre cache DNS avec la commande hello ipconfig /flushdns.
7. Vérifiez que hello résolu l’adresse IP correspond à votre point de terminaison secondaire.
8. Répétez le processus hello, en arrêtant à chaque point de terminaison à son tour. Vérifiez que hello DNS retourne hello adresseIP du point de terminaison suivant hello dans la liste de hello. Lorsque tous les points de terminaison sont arrêtés, vous devez obtenir à nouveau hello adresseIP du point de terminaison principal hello.

## <a name="how-tootest-hello-weighted-traffic-routing-method"></a>Comment tootest hello pondérée méthode de routage du trafic

1. Laissez tous les points de terminaison en fonction.
2. À partir d’un même client, demandez la résolution DNS du nom de domaine de votre entreprise à l’aide de l’outil nslookup.exe ou d’un utilitaire similaire.
3. Vérifiez que hello résolu l’adresse IP correspond à l’un de vos points de terminaison.
4. Videz le cache de votre client DNS et répétez les étapes 2 et 3 pour chaque point de terminaison. Vous devriez alors obtenir différentes adresses IP pour chacun de vos points de terminaison.

## <a name="how-tootest-hello-performance-traffic-routing-method"></a>Comment les performances de hello tootest le trafic méthode de routage

tooeffectively tester une méthode de routage de trafic de performances, vous devez disposer de clients situés dans différentes parties de hello world. Vous pouvez créer des clients dans différentes régions Azure qui peuvent être utilisé tootest vos services. Si vous avez un réseau global, vous pouvez à distance connectez-vous tooclients dans d’autres parties de hello world et exécuter vos tests à partir de là.

Sinon, différents services de recherche et d’obtention de DNS sont disponibles gratuitement sur Internet. Certaines de ces outils permettent de hello de résolution de noms DNS capacité toocheck à partir de différents emplacements monde hello. Faites une recherche sur « Recherche DNS » pour obtenir des exemples. Les services tiers comme Gomez ou Keynote peuvent être utilisé tooconfirm que vos profils distribuent le trafic comme prévu.

## <a name="next-steps"></a>Étapes suivantes

* [À propos des méthodes de routage du trafic de Traffic Manager](traffic-manager-routing-methods.md)
* [Considérations sur les performances de Traffic Manager](traffic-manager-performance-considerations.md)
* [Résolution des problèmes liés à l’état Détérioré de Traffic Manager](traffic-manager-troubleshooting-degraded.md)
