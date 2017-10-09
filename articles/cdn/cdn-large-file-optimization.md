---
title: "optimisation du téléchargement du fichier aaaLarge via hello Azure Content Delivery Network"
description: "Optimisation des téléchargements de fichiers volumineux expliquée en profondeur"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: v-semcev
ms.openlocfilehash: 2646979bfb38e997037bcff5b1cdda34e22c394a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="large-file-download-optimization-via-hello-azure-content-delivery-network"></a>Optimisation de téléchargement de fichiers volumineux via hello Azure Content Delivery Network

Tailles des fichiers de contenu sur Internet de hello continuent toogrow échéance tooenhanced fonctionnalité graphique amélioré et des contenus multimédias. Cette croissance résulte de divers facteurs : pénétration de la large bande, augmentation de la capacité des périphériques de stockage bon marché, prolifération des vidéos haute définition et objets connectés à Internet (IoT). Un mécanisme de livraison rapide et efficace pour les fichiers volumineux est critique tooensure une expérience de consommateur lisse et plus agréable.

La distribution de fichiers volumineux présente plusieurs difficultés. Tout d’abord, toodownload de temps moyen de hello un fichier volumineux peut être importante, car les applications pas télécharger toutes les données de manière séquentielle. Dans certains cas, les applications peuvent télécharger hello dernière partie d’un fichier avant la première partie de hello. Lors de la demande uniquement une petite quantité d’un fichier ou un utilisateur suspend un téléchargement, le téléchargement de hello peut échouer. téléchargement de Hello peut également être retardée jusqu'à ce qu’après hello réseau de diffusion de contenu (CDN) récupère la totalité du fichier hello hello serveur d’origine. 

En second lieu, la latence entre l’ordinateur de l’utilisateur et un fichier hello hello détermine la vitesse de hello à laquelle ils peuvent afficher le contenu. Par ailleurs, des problèmes de surcharge et de capacité du réseau affectent également le débit. Distance entre les serveurs et des utilisateurs pour créer des opportunités supplémentaires pour toooccur de perte de paquets, ce qui réduit la qualité. réduction de Hello qualité causée par le débit limité et une perte de paquets accrue peut augmenter le temps d’attente hello pour un toofinish de téléchargement de fichier. 

Troisièmement, de nombreux fichiers volumineux ne sont pas distribués dans leur intégralité. Les utilisateurs peuvent annuler un téléchargement en milieu d’ou regardez uniquement hello premières minutes d’une vidéo MP4 long. Logiciel et les supports sociétés donc toodeliver une partie hello uniquement d’un fichier qui est demandé. Distribution efficace de hello demandé parties réduit le trafic sortant hello hello serveur d’origine. Distribution efficace réduit également la mémoire de hello et pression d’e/s sur le serveur d’origine hello. 

Bonjour Azure Content Delivery Network à partir d’Akamai propose désormais une fonctionnalité qui remet les fichiers volumineux efficacement toousers monde hello à grande échelle. fonctionnalité de Hello réduit les latences, car il réduit la charge de hello sur les serveurs d’origine hello. Cette fonctionnalité est disponible avec le niveau de tarification Standard Akamai hello.

## <a name="configure-a-cdn-endpoint-toooptimize-delivery-of-large-files"></a>Configurer une remise de toooptimize du point de terminaison CDN des fichiers volumineux.

Vous pouvez configurer la remise de votre toooptimize de point de terminaison CDN pour les fichiers volumineux via hello portail Azure. Vous pouvez également utiliser nos API REST ou des hello client SDK toodo cela. Hello étapes suivantes montrent les processus hello via hello portail Azure.

1. tooadd un nouveau point de terminaison, sur hello **profil CDN** page, sélectionnez **point de terminaison**.

    ![Nouveau point de terminaison](./media/cdn-large-file-optimization/01_Adding.png)  
 
2. Bonjour **optimisé pour** la liste déroulante, sélectionnez **téléchargement de fichiers volumineux**.

    ![Optimisation des fichiers volumineux sélectionnée](./media/cdn-large-file-optimization/02_Creating.png)


Après avoir créé le point de terminaison CDN hello, il applique les optimisations d’un fichier volumineux hello pour tous les fichiers qui correspondent à certains critères. Hello après section décrit ce processus.

## <a name="optimize-for-delivery-of-large-files-with-hello-azure-content-delivery-network-from-akamai"></a>Optimiser pour le transfert des fichiers volumineux avec hello Azure Content Delivery Network Akamai

fichiers volumineux toodeliver optimisations et les configurations réseau Active la fonctionnalité de type Hello fichier volumineux optimisation plus rapidement et plus sensible. Livraison de web général avec Akamai met en cache de fichiers uniquement inférieure à 1,8 Go et pouvez tunnel (pas le cache) too150 Go de fichiers. Optimisation des fichiers volumineux met en cache les fichiers de too150 go.

L’optimisation des fichiers volumineux est efficace lorsque certaines conditions sont réunies. Conditions incluent le fonctionne du serveur d’origine hello et tailles de hello et types de fichiers hello qui sont demandées. Avant de passer à plus d’informations sur ces sujets, vous devez comprendre le fonctionnement de l’optimisation de hello. 

### <a name="object-chunking"></a>Segmentation d’objet 

Bonjour Azure Content Delivery Network à partir d’Akamai utilise une technique appelée l’objet de segmentation. Lorsqu’un fichier volumineux est demandé, hello CDN récupère des éléments plus petits du fichier de hello à partir de l’origine de hello. Une fois que le serveur de périphérie/POP de CDN hello reçoit une demande de fichier complet ou de la plage d’octets, il vérifie si le type de fichier hello est pris en charge pour cette optimisation. Il vérifie également si le type de fichier hello répond aux exigences de taille du fichier hello. Si la taille du fichier hello est supérieure à 10 Mo, hello CDN bord demandes hello fichier du serveur d’origine hello par segments de 2 Mo. 

Une fois le segment de hello arrive à hello edge CDN, elle a mis en cache et immédiatement pris en charge toohello utilisateur. Hello CDN puis le segment suivant de prérécupère des hello en parallèle. Cette lecture anticipée permet de s’assurer que le contenu de hello reste un segment avance utilisateur hello, ce qui réduit la latence. Ce processus se poursuit jusqu'à ce que l’ensemble de hello fichier est téléchargé (si nécessaire), toutes les plages d’octets sont disponibles (si nécessaire), ou le client de hello met fin à la connexion de hello. 

Pour plus d’informations sur la demande de plage d’octets hello, consultez [RFC 7233](https://tools.ietf.org/html/rfc7233).

Hello CDN met en cache les segments lors de leur réception. intégralité du fichier Hello ne toobe mis en cache sur le cache CDN hello. Les prochaines requêtes de plages d’octets ou de fichier hello sont servies à partir de hello cache du CDN. Si tous les segments de hello sont mis en cache sur hello CDN, la prérécupération est segments toorequest utilisé à partir de l’origine de hello. Cette optimisation s’appuie sur la capacité de hello hello origine toosupport plage d’octets des demandes de serveur. _Si le serveur d’origine hello ne prend pas en charge les demandes de plages d’octets, cette optimisation n’est pas efficace._ 

### <a name="caching"></a>Mise en cache
L’optimisation des fichiers volumineux utilise des temps d’expiration de mise en cache par défaut différents de ceux d’une livraison web générale. Il établit la distinction entre la mise en cache positive et négative basée sur les codes de réponse HTTP. Si le serveur d’origine hello spécifie un délai d’expiration via un cache-control ou en-tête de réponse de hello arrive à expiration, hello CDN respecte cette valeur. Lorsque ne spécifie pas l’origine de hello et fichier de hello correspond aux conditions de type et la taille de hello pour ce type d’optimisation, hello CDN utilise les valeurs par défaut de hello pour l’optimisation d’un fichier volumineux. Dans le cas contraire, hello CDN utilise les valeurs par défaut pour la remise de web général.


|    | Livraison web générale | Optimisation des fichiers volumineux 
--- | --- | --- 
Mise en cache : positive <br> HTTP 200, 203, 300, <br> 301, 302 et 410 | 7 jours |1 jour  
Mise en cache : négative <br> HTTP 204, 305, 404, <br> et 405 | Aucune | 1 seconde 

### <a name="deal-with-origin-failure"></a>Traitement des défaillances de l’origine

longueur de délai d’attente de lecture d’origine Hello augmente à partir de deux secondes, minutes de tootwo remise web général pour le type d’optimisation d’un fichier volumineux hello. Cette augmentation des comptes pour tooavoid de tailles de fichier plus grande hello une connexion prématurée de délai d’attente.

Lorsqu’une connexion arrive à expiration, hello CDN tente de renvoyer un nombre de fois avant l’envoi d’un client de toohello d’erreur « délai de la passerelle 504 - ». 

### <a name="conditions-for-large-file-optimization"></a>Conditions d’optimisation des fichiers volumineux

Hello tableau suivant répertorie hello de toobe des critères pour l’optimisation des fichiers volumineux :

Condition | Valeurs 
--- | --- 
Types de fichiers pris en charge | 3g2, 3gp, asf, avi, bz2, dmg, exe, f4v, flv, <br> gz, hdp, iso, jxr, m4v, mkv, mov, mp4, <br> mpeg, mpg, mts, pkg, qt, rm, swf, tar, <br> tgz, wdp, webm, webp, wma, wmv, zip  
Taille minimale du fichier | 10 Mo 
Taille maximale du fichier | 150 Go 
Caractéristiques du serveur d’origine | Doit prendre en charge des demandes de plages d’octets 

## <a name="optimize-for-delivery-of-large-files-with-hello-azure-content-delivery-network-from-verizon"></a>Optimiser pour le transfert des fichiers volumineux avec hello Azure Content Delivery Network Verizon

Bonjour Azure Content Delivery Network de Verizon remet des fichiers volumineux sans une limite de taille de fichier. Des fonctionnalités supplémentaires sont activées par la remise de toomake par défaut des fichiers volumineux plus rapidement.

### <a name="complete-cache-fill"></a>Remplissage du cache complet

fonction de remplissage du cache complet Hello par défaut permet de hello CDN toopull un fichier dans le cache de hello lorsqu’une demande initiale est abandonnée ou perdue. 

Le remplissage du cache complet est très utile pour les ressources volumineuses. En règle générale, les utilisateurs ne télécharger à partir du début toofinish. Ils utilisent un téléchargement progressif. comportement par défaut de Hello force hello edge server tooinitiate une extraction en arrière-plan de l’élément multimédia de hello hello serveur d’origine. Ensuite, la ressource de hello est dans le cache local du serveur de périphérie hello. Une fois l’objet complet de hello dans le cache de hello, serveur de périphérie hello répond toohello de demandes de plages d’octets CDN pour un objet mis en cache de hello.

comportement par défaut de Hello peut être désactivé via hello du moteur de règles Bonjour niveau Verizon Premium.

### <a name="peer-cache-fill-hot-filing"></a>Remplissage à chaud du cache d'homologue

fonction de classement à chaud Hello par défaut homologue cache remplissage utilise un algorithme de propriétaire sophistiqué. Il utilise supplémentaire bord mise en cache des serveurs en fonction de la bande passante et agrégat demandes métriques toofulfill client pour les objets volumineux, très populaires. Cette fonctionnalité empêche une situation dans laquelle grand nombre de demandes supplémentaires est envoyés de serveur d’origine de l’utilisateur tooa. 

### <a name="conditions-for-large-file-optimization"></a>Conditions d’optimisation des fichiers volumineux

fonctions d’optimisation Hello pour Verizon sont activées par défaut. Il n’existe aucune limite à la taille de fichier maximale. 

## <a name="additional-considerations"></a>Considérations supplémentaires

Envisagez de hello suivant des aspects supplémentaires pour ce type d’optimisation.
 
### <a name="azure-content-delivery-network-from-akamai"></a>Réseau Azure Content Delivery Network d’Akamai

- processus de segmentation de Hello génère serveur d’origine des demandes supplémentaires toohello. Toutefois, hello globale volume de données transmises à partir de l’origine de hello est beaucoup plus petite. Segmentation entraîne une meilleure des caractéristiques de mise en cache à hello CDN.

- Pression d’e/s et de mémoire sont réduits à l’origine de hello car les plus petits morceaux de fichier de hello est remis.

- Pour les segments mises en cache à hello CDN, aucune des requêtes supplémentaires ne sont toohello origine jusqu'à ce que le contenu hello expire ou il est supprimé du cache de hello.

- Les utilisateurs peuvent modifier la plage de demande toohello CDN, et ils sont traités comme n’importe quel fichier normal. L’optimisation s’applique uniquement si c’est un type de fichier valide et la plage d’octets hello est entre 10 Mo et 150 Go. Si la taille de fichier moyenne hello demandée est inférieure à 10 Mo, vous pourriez diffusion sur le web général toouse à la place.

### <a name="azure-content-delivery-network-from-verizon"></a>Réseau Azure Content Delivery Network de Verizon

type d’optimisation Hello web général remise peut fournir des fichiers volumineux.
