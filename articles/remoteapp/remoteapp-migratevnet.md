---
title: "toomigrate aaaHow à partir d’un réseau virtuel Azure de tooan RemoteApp VNET | Documents Microsoft"
description: "Découvrez comment toomigrate à partir d’un réseau virtuel Azure de tooan RemoteApp VNET"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: baea5d29-353b-48f8-b47f-806f2163e067
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: c0f8617556c6f1e33eca8322febf67ff33937ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-a-hybrid-collection-from-a-remoteapp-vnet-tooan-azure-vnet"></a>Comment toomigrate une collection hybride à partir d’un réseau virtuel Azure de tooan RemoteApp VNET
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Bonne nouvelle ! Nous avons activé collections de RemoteApp hybride toodeploy directement dans votre existant réseaux virtuels Azure (réseaux virtuels) au lieu de créer des réseaux virtuels RemoteApp spécifiques. Cela vous permet de tirer parti de hello dernières fonctionnalités de réseau virtuel (par exemple, ExpressRoute) et donnez à votre tooother de l’accès réseau direct hybride collections services Azure et les ordinateurs virtuels déployés toothat réseau virtuel.  (Ceci améliore les performances et facilite l’installation par rapport aux configurations de réseau virtuel à réseau virtuel).

Supposons que vous avez déjà créé une collection RemoteApp hybride appelée *OriginalCollection* avec un réseau virtuel RemoteApp appelé *RemoteAppVNET*. Voici hello étapes toomigrate il tooa appelée de nouveau de réseau virtuel Azure *AzureVNET*.

1. Sur hello **réseaux** onglet Bonjour [portail de gestion](http://manage.windowsazure.com/), créez un réseau virtuel appelé *AzureVNET*, à l’aide hello même emplacement, la configuration de DNS et l’espace d’adressage (au moins pour Hello *AzureVNET* sous-réseaux) en tant que vous avez utilisé pour *RemoteAppVNET*.
2. Configurer *AzureVNET* tooeither héberger ou avoir le déploiement d’Active Directory toohello une connexion réseau qui *OriginalCollection* est joint au.
3. Sur hello **applications distantes** , onglet de créer une nouvelle collection RemoteApp appelée *nouvelle Collection*. (Hello d’utilisation **créer avec le réseau virtuel** n'option pas **création rapide**.)
4. Configurer *NewCollection* toobe déployé sous-réseau tooa *AzureVNET*.
5. Configurer *NewCollection* toouse hello même image et les informations de jonction de domaine en tant que vous avez utilisé pour *OriginalCollection*.
6. Après quelques heures, *NewCollection* apparaît dans la liste de collections avec le statut Actif.

Maintenant, si vous n’avez pas besoin toomigrate toutes les informations utilisateur à partir de hello d’origine toohello nouveau regroupement, effectuez ces étapes suivant :

1. Supprimez *OriginalCollection*.
2. Supprimez *RemoteAppVNET*.

Vous avez terminé !

Ou bien, si vous n’avez pas besoin d’informations utilisateur toomigrate de hello d’origine toohello nouveau regroupement, effectuez ces étapes suivant :

1. Envoyer un courrier électronique trop[ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) avec votre ID d’abonnement Azure hello du nom de votre collection d’origine et le nom hello de votre nouvelle collection et demandez-lui de toomigrate vos informations utilisateur.
2. Dans les 2 jours ouvrables équipe de RemoteApp hello passeront liste d’accès utilisateur hello et tous les documents de l’utilisateur et les paramètres utilisateur d’hello d’origine toohello nouveau regroupement.
3. Supprimez *OriginalCollection*.
4. Supprimez *RemoteAppVNET*.

Vous avez terminé !

Si vous avez des questions ou que vous avez besoin d’aide, envoyez un e-mail [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).

