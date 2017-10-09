---
title: "passerelle de données locale aaaInstall | Documents Microsoft"
description: "Découvrez comment tooinstall et configurez une passerelle de données local."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/22/2017
ms.author: owend
ms.openlocfilehash: e2878bf765c82910d452ae2cdd9264a343ec1990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a>Installer et configurer une passerelle de données locale
Une passerelle de données local est requise lorsqu’un ou plusieurs serveurs Azure Analysis Services dans hello même région de se connecter à des sources de données tooon local. toolearn en savoir plus sur la passerelle de hello, consultez [passerelle de données locale](analysis-services-gateway.md).

## <a name="prerequisites"></a>Composants requis
**Configuration minimale requise :**

* .NET Framework 4.5
* Version 64 bits de Windows 7 / Windows Server 2008 R2 (ou version ultérieure)

**Recommandé :**

* Processeur 8 cœurs
* 8 Go de mémoire
* Version 64 bits de Windows 2012 R2 (ou version ultérieure)

**Points importants à prendre en compte :**

* Pendant l’installation, lors de l’inscription de votre passerelle avec Azure, la région par défaut hello pour votre abonnement est sélectionnée. Vous pouvez choisir une autre région. Si vous avez des serveurs dans plusieurs régions, vous devez installer une passerelle pour chaque région. 
* passerelle de Hello ne peut pas être installé sur un contrôleur de domaine.
* Une seule passerelle peut être installée sur un ordinateur.
* Installez la passerelle de hello sur un ordinateur qui reste sur et ne passe pas toosleep.
* N’installez pas de passerelle de hello sur un réseau d’ordinateurs connectés sans fil tooyour. Les performances peuvent être réduites.


## <a name="download"></a>Télécharger
 [Télécharger hello passerelle](https://aka.ms/azureasgateway)

## <a name="install"></a>Installer

1. Exécutez le programme d’installation.

2. Sélectionnez un emplacement, acceptez les termes du contrat de hello, puis cliquez sur **installer**.

   ![Emplacement d’installation et termes du contrat de licence](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. Sélectionnez **Passerelle de données locale (recommandé)**. Azure Analysis Services ne prend pas en charge le mode personnel.

   ![Choisir le type de passerelle](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. Entrez un compte toosign dans tooAzure. compte de Hello doit être dans Azure Active Directory votre locataire. Ce compte est utilisé pour l’administrateur de la passerelle hello. 

   ![Entrez un compte toosign dans tooAzure](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > Si vous vous connectez avec un compte de domaine, il sera mappé tooyour compte de société dans Azure AD. Votre compte professionnel sera utilisé en tant qu’administrateur de passerelle hello hello.

## <a name="register"></a>S’inscrire
Dans l’ordre toocreate une ressource de passerelle dans Azure, vous devez inscrire l’instance locale de hello que vous installé avec hello Service Cloud de passerelle. 

1.  Sélectionnez **Inscrivez une nouvelle passerelle sur cet ordinateur**.

    ![S’inscrire](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. Saisissez un nom et une clé de récupération pour votre passerelle. Par défaut, la passerelle de hello utilise la région par défaut de votre abonnement. Si vous avez besoin de tooselect une autre région, sélectionnez **modification région**.

   ![S’inscrire](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <a name="create-resource"></a>Créer une ressource de passerelle Azure
Une fois que vous avez installé et inscrit votre passerelle, vous devez toocreate une ressource de passerelle dans votre abonnement Azure. Se connecter tooAzure avec hello même compte que celui utilisé lors de l’inscription de passerelle de hello.

1. Dans le portail Azure, cliquez sur **Création d’un nouveau service** > **Enterprise Integration** > **Passerelle de données locale** > **Créer**.

   ![Créer une ressource de passerelle](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. Dans **Créer une passerelle connexion**, entrez les paramètres suivants:

    * **Nom** : entrez un nom pour votre ressource de passerelle. 

    * **Abonnement**: sélectionnez hello tooassociate abonnement Azure avec votre ressource de la passerelle. 
    Cet abonnement doit être hello même abonnement que vos serveurs sont dans.
   
      abonnement de Hello par défaut est basée sur hello compte Azure que vous avez utilisé toosign dans.

    * **Groupe de ressources** : créez un groupe de ressources ou sélectionnez-en un.

    * **Emplacement**: vous avez inscrit votre passerelle dans la région sélectionnez hello.

    * **Nom de l’installation**: Si votre installation de la passerelle n’est pas déjà sélectionnée, sélectionnez hello enregistrée. 

    Une fois ces opérations effectuées, cliquez sur **Créer**.

## <a name="connect-servers"></a>Connecter des ressources de serveurs toohello passerelle

1. Dans la vue d’ensemble du serveur Azure Analysis Services, cliquez sur **Passerelle de données locale**.

   ![Se connecter toogateway de serveur](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. Dans **choisir une passerelle de données locale de tooconnect**, sélectionnez votre ressource de passerelle, puis cliquez sur **passerelle sélectionné de connexion**.

   ![Se connecter toogateway ressource du serveur](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > Si votre passerelle n’apparaît pas dans la liste de hello, votre serveur est probablement pas dans hello même région que vous avez spécifié lors de l’inscription de passerelle de hello de région de hello. 

Vous avez terminé. Si vous avez besoin de tooopen ports ou que vous effectuez un dépannage, être vraiment toocheck out [passerelle de données locale](analysis-services-gateway.md).

## <a name="next-steps"></a>Étapes suivantes
* [Gérer Analysis Services](analysis-services-manage.md)   
* [Obtenir les données d’Azure Analysis Services](analysis-services-connect.md)
