---
title: "machines virtuelles d’aaaManage à l’aide de hello Explorateur Azure pour IntelliJ | Documents Microsoft"
description: "Découvrez comment toomanage vos machines virtuelles Azure à l’aide de hello Explorateur Azure pour IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: a73dd4f73b311dd3413f6712e3b76c36ee464de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-intellij"></a>Gérer des ordinateurs virtuels à l’aide de hello Explorateur Azure pour IntelliJ

Hello Explorateur Azure, qui fait partie de hello Azure Toolkit pour IntelliJ, fournit aux développeurs Java une solution facile à utiliser pour la gestion des ordinateurs virtuels de leur compte Azure à partir d’à l’intérieur de hello IntelliJ environnement de développement intégré (IDE).

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a>Suppression d’une machine virtuelle dans IntelliJ

toocreate un ordinateur virtuel à l’aide de hello Explorateur Azure, procédez comme hello suivant : 

1. Se connecter à l’aide des étapes de hello Bonjour tooyour compte Azure [instructions d’authentification pour hello boîte à outils Azure pour IntelliJ] l’article.

2. Bonjour **Explorateur Azure** afficher, développez hello **Azure** nœud, avec le bouton droit **virtuels**, puis cliquez sur **créer un ordinateur virtuel**. 

   ![Hello commande de créer un ordinateur virtuel][CR01]  
    Hello **créer Machine virtuelle** Assistant s’ouvre.

3. Bonjour **choisir un abonnement** fenêtre, sélectionnez votre abonnement, puis cliquez sur **suivant**. 

   ![Hello fenêtre Choisir un abonnement][CR02]

4. Bonjour **sélectionner une Image de Machine virtuelle** fenêtre, entrez hello informations suivantes :

   * **Emplacement**: spécifie l’emplacement où votre machine virtuelle sera créée (par exemple *États-Unis de l’Ouest*). 

   * **Image recommandée** : spécifie que vous allez choisir une image dans une liste abrégée d’images couramment utilisées.

   * **Image personnalisée**: Spécifie que vous allez choisir une image personnalisée en fournissant hello informations suivantes :

      * **Serveur de publication**: Spécifie le serveur de publication hello créé hello image que vous utiliserez pour votre machine virtuelle (par exemple, *Microsoft*).

      * **Offre**: Spécifie l’ordinateur virtuel de hello offre toouse à partir du serveur de publication sélectionné hello (par exemple, *JDK*).

      * **Référence (SKU)**: Spécifie hello stock référence toouse à partir de l’offre de hello sélectionné (par exemple, *JDK_8*).

      * **Version #**: Spécifie la version de hello sélectionné toouse de référence (SKU).

   ![Hello sélectionner une fenêtre de l’Image de Machine virtuelle][CR03]

5. Cliquez sur **Suivant**. 

6. Bonjour **les paramètres de base de Machine virtuelle** fenêtre, entrez hello informations suivantes :

   * **Nom de machine virtuelle**: Spécifie le nom hello pour votre nouvel ordinateur virtuel, qui doit commencer par une lettre et contenir uniquement des lettres, des chiffres et des traits d’union.

   * **Taille**: Spécifie le nombre de hello de cœurs et de tooallocate de mémoire pour votre machine virtuelle.

   * **Nom d’utilisateur**: Spécifie hello toocreate de compte administrateur pour la gestion de votre machine virtuelle.

   * **Mot de passe** et **confirmer**: Spécifie le mot de passe hello pour votre compte d’administrateur.

   ![fenêtre des paramètres de base de Machine virtuelle Hello][CR04]

7. Cliquez sur **Suivant**. 

8. Bonjour **associés des ressources** fenêtre, entrez hello informations suivantes :

   * **Groupe de ressources**: Spécifie le groupe de ressources hello pour votre machine virtuelle. Sélectionnez une des options suivantes de hello :
      * **Créer de nouveaux**: Spécifie que vous souhaitez toocreate un groupe de ressources.
      * **Utiliser l’existante**: Spécifie que vous souhaitez tooselect dans une liste de groupes de ressources qui sont associés à votre compte Azure.

       ![fenêtre de Hello associées de ressources][CR07]

   * **Compte de stockage**: Spécifie toouse de compte de stockage hello pour le stockage de votre machine virtuelle. Vous pouvez choisir un compte de stockage ou en créer un. Si vous choisissez **créer un nouveau**, hello suivant la boîte de dialogue s’affiche :

      ![boîte de dialogue Créer un compte de stockage Hello][CR05]

   * **Réseau virtuel** et **sous-réseau**: Spécifie le réseau virtuel de hello et sous-réseau que votre machine virtuelle se connecte à. Vous pouvez utiliser un réseau et un sous-réseau existants, ou créer un réseau et un sous-réseau. Si vous sélectionnez **nouvel**, hello suivant la boîte de dialogue s’affiche :

      ![boîte de dialogue Créer un réseau virtuel Hello][CR06]

   * **Adresse IP publique** : spécifie l’adresse IP externe de votre machine virtuelle. Vous pouvez choisir toocreate une nouvelle adresse IP ou, si votre machine virtuelle ne disposent pas d’une adresse IP publique, vous pouvez sélectionner **(aucun)**. 

   * **Groupe de sécurité réseau** : spécifie un pare-feu réseau facultatif pour votre machine virtuelle. Vous pouvez sélectionner un pare-feu existant ou, si votre machine virtuelle n’a pas besoin de pare-feu réseau, vous pouvez sélectionner **(Aucun)**. 

   * **Groupe à haute disponibilité** : spécifie un groupe à haute disponibilité auquel votre machine virtuelle peut appartenir. Vous pouvez sélectionner un ensemble de disponibilité existant, créez un nouveau jeu de disponibilité ou, si votre machine virtuelle n’appartiendra tooan à haute disponibilité, sélectionnez **(aucun)**.

9. Cliquez sur **Terminer**.  
    Votre nouvel ordinateur virtuel s’affiche dans la fenêtre d’outil Explorateur Azure hello. 

   ![Machine virtuelle Bonjour Azure Explorateur][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a>Redémarrer une machine virtuelle dans IntelliJ

toorestart un ordinateur virtuel à l’aide de hello Explorateur Azure dans IntelliJ, hello suivant :

1. Bonjour **Explorateur Azure** afficher, avec le bouton droit hello virtual machine, puis sélectionnez **redémarrer**.

   ![commande de redémarrage Hello à une machine virtuelle][RE01]

2. Dans la fenêtre de confirmation hello, cliquez sur **Oui**. 

   ![Hello redémarrer la fenêtre de confirmation de machine virtuelle][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a>Arrêter une machine virtuelle dans IntelliJ

tooshut vers le bas d’une machine virtuelle en cours d’exécution à l’aide de hello Explorateur Azure dans IntelliJ, hello suivant :

1. Bonjour **Explorateur Azure** afficher, avec le bouton droit hello virtual machine, puis sélectionnez **arrêt**.

   ![commande d’arrêt d’une machine virtuelle Hello][SH01]

2. Dans la fenêtre de confirmation hello, cliquez sur **Oui**. 

   ![Hello arrêter de la fenêtre de confirmation de machine virtuelle][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a>Supprimer une machine virtuelle dans IntelliJ

toodelete un ordinateur virtuel à l’aide de hello Explorateur Azure dans IntelliJ, hello suivant :

1. Bonjour **Explorateur Azure** afficher, avec le bouton droit hello virtual machine, puis sélectionnez **supprimer**.

   ![commande de suppression d’une machine virtuelle Hello][DE01]

2. Dans la fenêtre de confirmation hello, cliquez sur **Oui**. 

   ![Hello supprimer la fenêtre de confirmation de machine virtuelle][DE02]

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les tailles de machine virtuelle Azure et la tarification, consultez hello suivant des ressources :

* Tailles des machines virtuelles Azure
  * [Tailles des machines virtuelles Windows dans Azure]
  * [Tailles des machines virtuelles Linux dans Azure]
* Tarification des machines virtuelles Azure
  * [Tarification des machines virtuelles Windows]
  * [Tarification des machines virtuelles Linux]

Pour plus d’informations sur hello boîtes à outils Azure pour Java IDE, consultez hello suivant des ressources :

* [boîte à outils Azure pour Eclipse]
  * [Nouveautés de hello boîte à outils Azure pour Eclipse]
  * [Lors de l’installation hello boîte à outils Azure pour Eclipse]
  * [Instructions de connexion pour hello boîte à outils Azure pour Eclipse]
  * [Créer une application web Hello World pour Azure dans Eclipse]
* [Kit de ressources Azure pour IntelliJ]
  * [Quelles sont les nouveautés Bonjour Azure Toolkit pour IntelliJ]
  * [Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]
  * [instructions d’authentification pour hello boîte à outils Azure pour IntelliJ]
  * [Créer une application web Hello World pour Azure dans IntelliJ]

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez [Centre de développement Java pour Azure] et [Outils Java pour Visual Studio Team Services].

<!-- URL List -->

[boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij.md
[Créer une application web Hello World pour Azure dans Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Créer une application web Hello World pour Azure dans IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Lors de l’installation hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instructions de connexion pour hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[instructions d’authentification pour hello boîte à outils Azure pour IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Nouveautés de hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Quelles sont les nouveautés Bonjour Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/
[Outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/

[Tailles des machines virtuelles Windows dans Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tailles des machines virtuelles Linux dans Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Tarification des machines virtuelles Windows]: /pricing/details/virtual-machines/windows/
[Tarification des machines virtuelles Linux]: /pricing/details/virtual-machines/linux/


<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR08.png
