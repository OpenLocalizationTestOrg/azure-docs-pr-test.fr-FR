---
title: "agents de machine virtuelle Azure aaaUse pour l’intégration continue avec Jenkins."
description: "Agents de machine virtuelle Azure en tant que subordonnés de Jenkins."
services: multiple
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 2388e6919d0280372166fbd325d80dafb00d7550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a>Utilisez des agents de machine virtuelle Azure pour l’intégration continue avec Jenkins.

Ce démarrage rapide montre comment toouse hello toocreate de plug-in d’Agents de machine virtuelle Azure Jenkins un agent de Linux (Ubuntu) à la demande dans Azure.

## <a name="prerequisites"></a>Composants requis

toocomplete ce démarrage rapide :

* Si vous n’avez pas déjà un maître de Jenkins, vous pouvez démarrer avec hello [modèle de Solution](install-jenkins-solution-template.md) 
* Consultez trop[créer un principal de Service Azure avec Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) si vous n’avez pas déjà un principal du service Azure.

## <a name="install-azure-vm-agents-plugin"></a>Installer le plug-in Agents de machine virtuelle Azure

Si vous démarrez à partir de hello [modèle de Solution](install-jenkins-solution-template.md), plug-in de l’Agent de machine virtuelle Azure hello est installé dans le masque de Jenkins hello.

Sinon, installer hello **Agents de machine virtuelle Azure** plug-in à partir du tableau de bord hello Jenkins.

## <a name="configure-hello-plugin"></a>Configurer le plug-in hello

* Dans le tableau de bord hello Jenkins, cliquez sur **Jenkins de gérer -> configuration du système ->**. Faites défiler bas toohello de page de hello et rechercher la section hello avec hello déroulant **Ajouter nouveau cloud**. Dans le menu de hello, sélectionnez **Agents de machine virtuelle Microsoft Azure**
* Sélectionnez un compte existant à partir de la liste déroulante de hello informations d’identification Azure.  tooadd un nouveau **Principal du Service Microsoft Azure,** entrez hello valeurs suivantes : ID d’abonnement, ID de Client, question secrète du Client et OAuth 2.0 Token Endpoint.

![Informations d’identification Azure](./media/jenkins-azure-vm-agents/service-principal.png)

* Cliquez sur **Vérifiez configuration** toomake que cette configuration de profil hello est correcte.
* Enregistrer la configuration de hello et continuer toohello prochaine étape.

## <a name="template-configuration"></a>Configuration du modèle

### <a name="general-configuration"></a>Configuration générale
Ensuite, configurez un modèle pour utilisation toodefine un agent de machine virtuelle Azure. 

* Cliquez sur **ajouter** tooadd un modèle. 
* Entrez un nom pour votre nouveau modèle. 
* Pour l’étiquette de hello, entrez « ubuntu. » Cette étiquette est utilisée lors de la configuration de tâche hello.
* Sélectionnez la région souhaités hello à partir de la zone de liste déroulante hello.
* Sélectionnez hello souhaité de taille de machine virtuelle.
* Spécifiez le nom de compte de stockage Azure hello ou laisser le nom par défaut de hello toouse vide « jenkinsarmst ».
* Spécifiez la durée de rétention hello en minutes. Ce paramètre définit le nombre de hello de minutes que Jenkins peut attendre avant de supprimer automatiquement un agent inactif. Spécifiez 0 si vous ne souhaitez pas toobe agents inactifs supprimé automatiquement.

![Configuration générale](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a>Configuration d’une image

toocreate un agent Linux (Ubuntu), sélectionnez **référence d’Image** et utilisez hello suivant la configuration, par exemple. Consultez trop[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) hello Azure plus récente prises en charge les images.

* Éditeur d’images : Canonical
* Offre de l’image : UbuntuServer
* Référence SKU de l’image : 14.04.5-LTS
* Version de l’image : la plus récente
* Type de système d’exploitation : Linux
* Méthode de lancement : SSH
* Fournir des informations d’identification d’administrateur
* Pour le script d’initialisation de machine virtuelle, entrez :
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![Configuration d’une image](./media/jenkins-azure-vm-agents/image-config.png)

* Cliquez sur **vérifier le modèle** configuration de hello tooverify.
* Cliquez sur **Enregistrer**.

## <a name="create-a-job-in-jenkins"></a>Créer un travail dans Jenkins

* Dans le tableau de bord hello Jenkins, cliquez sur **un nouvel élément**. 
* Entrez un nom, sélectionnez **Freestyle project (Projet libre)** et cliquez sur **OK**.
* Bonjour **général** onglet, sélectionnez « Restreindre où le projet peut être exécuté » et le type « ubuntu » dans l’Expression de l’étiquette. Vous voyez maintenant « ubuntu » dans la liste déroulante de hello.
* Cliquez sur **Enregistrer**.

![Configurer un travail](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a>Générer votre nouveau projet

* Retournez dans le tableau de bord toohello Jenkins.
* Nouvelle tâche de hello avec le bouton que vous avez créé, puis cliquez sur **créer maintenant**. Une génération est lancée. 
* Une fois la génération de hello est terminée, accédez trop**sortie de Console**. Vous voyez que build de hello a été effectuée à distance sur Azure.

![Sortie de la console](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a>Référence

* Vidéo Azure Friday : [intégration continue avec Jenkins à l’aide d’agents de machine virtuelle Azure](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)
* Informations de prise en charge et options de configuration : [wiki du plug-in Jenkins pour agents de machine virtuelle Azure](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin) 

