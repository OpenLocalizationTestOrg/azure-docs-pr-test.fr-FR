---
title: "Paramètres de Registre de Cloud App Discovery pour les services de proxy | Microsoft Docs"
description: "L’objectif de cette rubrique est de présenter les étapes que vous devez effectuer pour définir le port nécessaire sur les ordinateurs exécutant l’agent Cloud App Discovery."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d78e925-e331-40ba-904a-e4ef14260cac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ea15dc9a9f20a296e622c8fb1011f7ee99de3e99
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a>Paramètres de Registre de Cloud App Discovery pour les services de proxy
Par défaut, l’agent Cloud App Discovery est configuré pour utiliser uniquement les ports 80 ou 443. Si vous envisagez d’installer Cloud App Discovery dans un environnement avec un serveur proxy qui utilise un port personnalisé (ni 443, ni 80), vous devez configurer vos agents pour utiliser ce port. La configuration est basée sur une clé de Registre.

L’objectif de cette rubrique est de présenter les étapes que vous devez effectuer pour définir le port nécessaire sur les ordinateurs exécutant l’agent Cloud App Discovery.

**Pour modifier le port utilisé par l’ordinateur exécutant l’agent Cloud App Discovery, effectuez les opérations suivantes :**

1. Démarrez l’Éditeur du Registre. <br> ![Exécuter](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. Créez ou accédez à la clé de Registre suivante :  <br> **HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint** 
3. Créez une valeur de **chaînes multiples** nommée **Ports**. ![Nouveau](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)
4. Pour ouvrir la boîte de dialogue **Modifier les chaînes multiples** , double-cliquez sur la valeur de Ports.
5. Dans la zone de texte Données de la valeur, tapez les valeurs suivantes et ajoutez tous les ports personnalisés qui sont utilisés par votre organisation :  <br><br>
   **80** <br>
   **8080** <br>
   **8118** <br>
   **8888** <br>
   **81** <br>
   **12080** <br>
   **6999** <br>
   **30606** <br>
   **31595** <br>
   **4080** <br>
   **443** <br>
   **1110** <br><br>
   ![Modifier les chaînes multiples](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)
6. Cliquez sur **OK** pour fermer la boîte de dialogue **Modifier les chaînes multiples**.

**Ressources supplémentaires**

* [Comment puis-je détecter les applications cloud non approuvées utilisées au sein de mon organisation ?](active-directory-cloudappdiscovery-whatis.md) 

