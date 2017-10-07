---
title: "aaaCreate un concentrateur d’événements Azure | Documents Microsoft"
description: "Créer un espace de noms Azure Event Hubs et un concentrateur d’événements à l’aide de hello portail Azure"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: ff99e327-c8db-4354-9040-9c60c51a2191
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: sethm
ms.openlocfilehash: 9a8b7711e2ca7d112e24be19353d43c365ff6935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-hello-azure-portal"></a>Créer un espace de noms de concentrateurs d’événements et un concentrateur d’événements à l’aide de hello portail Azure

## <a name="create-an-event-hubs-namespace"></a>Créer un espace de noms Event Hubs
1. Session toohello [portail Azure][Azure portal], puis cliquez sur **nouveau** à hello haut à gauche de l’écran hello.
1. Cliquez sur **Internet des Objets**, puis sur **Event Hubs**.
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. Bonjour **créer l’espace de noms** panneau, entrez un nom d’espace de noms. système de Hello vérifie immédiatement toosee si le nom hello est disponible.
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. Une fois que nom d’espace de noms hello de fabrication est disponible, choisissez hello tarification (base ou Standard). En outre, choisissez un abonnement Azure, le groupe de ressources et l’emplacement de ressources toocreate hello. 
1. Cliquez sur **créer** toocreate hello espace de noms. Vous avez peut-être toowait quelques minutes pour les ressources hello hello système toofully disposition.
2. Dans hello portail la liste des espaces de noms, cliquez sur hello nouvellement créé espace de noms.
2. Cliquez sur **Stratégies d’accès partagé**, puis sur **RootManageSharedAccessKey**.
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. Cliquez sur Bonjour copie bouton toocopy Bonjour **RootManageSharedAccessKey** Presse-papiers de toohello de chaîne de connexion. Enregistrez cette chaîne de connexion dans un emplacement temporaire, tel que le bloc-notes, toouse plus tard.
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a>Création d'un concentrateur d'événements

1. Dans hello concentrateurs d’événements espace de noms, cliquez sur espace de noms hello nouvellement créé.      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. Dans le panneau espace de noms de hello, cliquez sur **concentrateurs d’événements**.
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. Haut hello du Panneau de hello, cliquez sur **concentrateur d’événements ajouter**.
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. Saisissez un nom pour votre concentrateur d’événements, puis cliquez sur **Créer**.
   
    ![](./media/event-hubs-create/create-event-hub5.png)

Votre concentrateur d’événements est créée, et que les chaînes de connexion hello vous devez toosend et recevez des événements.

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur les concentrateurs d’événements, consultez ces liens :

* [Vue d’ensemble des hubs d’événements](event-hubs-what-is-event-hubs.md)
* [Vue d’ensemble de l'API Event Hubs](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/