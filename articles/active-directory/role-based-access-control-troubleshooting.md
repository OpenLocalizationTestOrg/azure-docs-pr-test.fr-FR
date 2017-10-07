---
title: aaaTroubleshoot Azure RBAC. | Documents Microsoft
description: "Obtenez de l’aide en cas de problèmes ou de questions concernant les ressources de contrôle d’accès en fonction du rôle."
services: azure-portal
documentationcenter: na
author: andredm7
manager: femila
ms.assetid: df42cca2-02d6-4f3c-9d56-260e1eb7dc44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 15feced32d8459d90c4c246d335932f90e1fc91f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-troubleshooting"></a>Résolution des problèmes de contrôle d’accès en fonction du rôle

Cet article de document répond aux questions courantes sur les droits d’accès spécifiques hello qui sont accordées aux rôles, afin que vous sachiez quels tooexpect lorsque vous utilisez hello rôles Bonjour portail Azure et peut résoudre les problèmes d’accès. Ces trois rôles couvrent tous les types de ressources :

* Propriétaire  
* Collaborateur  
* Lecteur  

Propriétaires et contributeurs ont toohello gestion de l’accès complet à rencontrer, mais un collaborateur ne peut pas donner accès tooother utilisateurs ou groupes. Choses un peu plus intéressantes avec le rôle de lecteur hello, qui est où nous allons passer du temps. Consultez hello [article de get-started Role-Based Access Control](role-based-access-control-configure.md) pour plus d’informations sur comment accéder à toogrant.

## <a name="app-service-workloads"></a>Charges de travail App Service
### <a name="write-access-capabilities"></a>Fonctionnalités d’accès en écriture
Si vous accordez une accès en lecture seule utilisateur tooa. application web unique, certaines fonctionnalités sont désactivées, que vous ne pouvez pas attendre. Hello suivant les fonctionnalités de gestion requièrent **écrire** accéder à l’application web tooa (Contributeur ou propriétaire) et ne sont pas disponibles pour tous les scénarios en lecture seule.

* Commandes (comme start, stop, etc.)
* Modification de paramètres tels que la configuration générale, les paramètres de mise à l’échelle, les paramètres de sauvegarde et les paramètres d’analyse
* Accès aux informations d’identification de publication et autres informations secrètes, telles que les paramètres d’application et les chaînes de connexion
* Diffusion de journaux
* Configuration des journaux de diagnostic
* Console (invite de commandes)
* Déploiements actifs et récents (pour le déploiement continu Git local)
* Estimation de dépense
* Tests web
* Réseau virtuel (uniquement visible tooa lecteur si un réseau virtuel a déjà été configuré par un utilisateur avec accès en écriture).

Si vous ne peut pas accéder à un de ces vignettes, vous devez tooask votre administrateur pour l’application web de collaborateur accès toohello.

### <a name="dealing-with-related-resources"></a>Gestion des ressources connexes
Les applications Web sont compliquées par présence hello de quelques différentes ressources qui interaction. Voici un groupe de ressources classique avec deux sites web :

![Groupe de ressources d'application web](./media/role-based-access-control-troubleshooting/website-resource-model.png)

Par conséquent, si vous accordez l’accès toojust hello web app, une grande partie de la fonctionnalité hello sur Panneau du site Web de hello Bonjour portail Azure est désactivée.

Ces éléments nécessitent **écrire** accéder toohello **plan App Service** qui correspond le site Web de tooyour :  

* L’application web affichage hello de tarification (gratuit ou Standard)  
* Configuration de mise à l'échelle (le nombre d'instances, la taille de la machine virtuelle, les paramètres de mise à l'échelle automatique)  
* Quotas (stockage, bande passante, UC)  

Ces éléments nécessitent **écrire** toohello accès entier **groupe de ressources** qui contient votre site Web :  

* Certificats SSL et liaisons (certificats SSL peuvent être partagées entre les sites de hello même groupe de ressources et l’emplacement géographique)  
* Règles d'alerte  
* Paramètres de mise à l'échelle automatique  
* Composants Application Insights  
* Tests web  

## <a name="virtual-machine-workloads"></a>Charges de travail des machines virtuelles
Beaucoup comme avec les applications web, certaines fonctionnalités dans le panneau de machine virtuelle hello requièrent un accès en écriture toohello virtual machine ou tooother ressources hello groupe de ressources.

Machines virtuelles sont associées tooDomain noms, les réseaux virtuels, les comptes de stockage et les règles d’alerte.

Ces éléments nécessitent **écrire** accéder toohello **machine virtuelle**:

* Points de terminaison  
* Adresses IP  
* Disques  
* Extensions  

Ces cubes nécessitent **écrire** hello de tooboth accès **machine virtuelle**et hello **groupe de ressources** (ainsi que le nom de domaine hello) qu’il est dans :  

* Groupe à haute disponibilité  
* Jeu d'équilibrage de la charge  
* Règles d'alerte  

Si vous ne peut pas accéder à un de ces vignettes, demandez à votre administrateur pour le groupe de ressources de collaborateur accès toohello.

## <a name="see-more"></a>En savoir plus
* [Contrôle d’accès basé sur rôle](role-based-access-control-configure.md): prise en main RBAC Bonjour portail Azure.
* [Rôles intégrés](role-based-access-built-in-roles.md): obtenir des informations sur les rôles hello livrés dans RBAC.
* [Les rôles personnalisés dans Azure RBAC](role-based-access-control-custom-roles.md): Découvrez comment toocreate des rôles personnalisés toofit doit votre accès.
* [Créer un rapport d’historique des modifications d’accès](role-based-access-control-access-change-history-report.md): effectuez le suivi des changements d’affection de rôle dans RBAC.

