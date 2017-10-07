---
title: "aaaCloud paramètres du Registre application découverte pour les Services Proxy | Documents Microsoft"
description: "objectif Hello de cette rubrique est tooprovide vous hello étapes que vous devez port hello requis tooperform tooset ordinateurs hello exécutant l’agent de découverte d’application Cloud hello."
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
ms.openlocfilehash: bb1fe20016459160b4f67cb0125b1781a0260c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a>Paramètres de Registre de Cloud App Discovery pour les services de proxy
Par défaut, l’agent de découverte d’application Cloud hello est configuré toouse que hello les ports 80 ou 443. Si vous envisagez d’installer Cloud App Discovery dans un environnement avec un serveur proxy qui utilise un port personnalisé (443 ni 80), vous devez tooconfigure votre toouse agents ce port. configuration de Hello est basée sur une clé de Registre.

objectif Hello de cette rubrique est tooprovide vous hello étapes que vous devez port hello requis tooperform tooset ordinateurs hello exécutant l’agent de découverte d’application Cloud hello.

**port de hello toomodify utilisé par ordinateur hello exécutant l’agent de découverte d’application Cloud hello, procédez hello comme suit :**

1. Démarrez l’Éditeur du Registre hello. <br> ![Exécuter](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. Accédez tooor créer hello clé de Registre suivante : <br> **HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint** 
3. Créez une valeur de **chaînes multiples** nommée **Ports**. ![Nouveau](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)
4. tooopen hello **modifier les chaînes multiples** boîte de dialogue, double-cliquez sur la valeur de Ports hello.
5. Dans la zone de texte des données de valeur de hello, tapez Bonjour valeurs suivantes et ajoutez tous les ports personnalisés utilisés par votre organisation : <br><br>
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
6. Cliquez sur **OK** tooclose hello **modifier les chaînes multiples** boîte de dialogue.

**Ressources supplémentaires**

* [Comment puis-je détecter les applications cloud non approuvées utilisées au sein de mon organisation ?](active-directory-cloudappdiscovery-whatis.md) 

