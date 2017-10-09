---
title: "aaaManage le coffre de clés dans la pile de Azure à l’aide de PowerShell | Documents Microsoft"
description: "Découvrez comment toomanage le coffre de clés dans la pile de Azure à l’aide de PowerShell."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 0a3aa6eb0b2c2976935d995a0bf6f226dc4eac84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-in-azure-stack-using-hello-portal"></a>Gérer le coffre de clés dans la pile d’Azure à l’aide du portail de hello

Vous pouvez gérer le coffre de clés dans la pile d’Azure à l’aide du portail de pile de Azure hello. Cet article vous aidera à obtenir toocreate démarrée et gérer le coffre de clés dans la pile de Azure. 

## <a name="prerequisites"></a>Composants requis  

* Les administrateurs de cloud Azure pile doivent avoir [créé une offre](azure-stack-create-offer.md) qui inclut le service de coffre de clés hello.  
* Les utilisateurs doivent [s’abonner tooan offre](azure-stack-subscribe-plan-provision-vm.md) qui inclut le service de coffre de clés hello.  
 
## <a name="create-a-key-vault"></a>Création d’un coffre de clés 

1. Se connecter dans le portail de l’utilisateur toohello (https://portal.local.azurestack.external).  

2. À partir du tableau de bord hello, cliquez sur **Nouveau > sécurité + identité > coffre de clés**.  

    ![Écran de KV](media/azure-stack-kv-manage-portal/image1.png)  

3. Sur hello **créer un coffre de clés** panneau, attribuer un **nom** pour votre archivage. Nom du coffre peut contenir uniquement des caractères alphanumériques, trait d’union caractère spécial hello (-), et il ne doit pas commencer par un chiffre.  

4. Choisissez un **abonnement** à partir de la liste de hello des abonnements disponibles. Tous les abonnements qui offrent un service de coffre de clés hello sont affichent dans la déroulante hello.  

5. Sélectionnez un **Groupe de ressources** existant ou créez-en un.  

6. Sélectionnez hello **niveau tarifaire**.  
    >[!NOTE]
    > Les coffres de clés dans le Kit de développement Azure Stack prennent uniquement en charge les SKU **Standard**.

7. Sélectionnez une **Stratégie d’accès** existante ou créez-en une. Stratégie d’accès vous permet de toogrant les autorisations pour un utilisateur, d’application ou d’une sécurité tooperform regrouper des opérations avec ce coffre.  

8. Si vous le souhaitez, choisissez une **stratégie d’accès avancé** fonctionnalités hello tooenable accéder aux Machines tooVirtual pour le déploiement, tooResource le Gestionnaire de déploiement d’un modèle d’accès et accéder tooAzure chiffrement de disque pour le volume chiffrement. 
  
9.  Après avoir configuré les paramètres de hello, cliquez sur **OK** , puis **créer**. Déploiement de coffre de clés hello démarre. 

## <a name="manage-keys-and-secrets"></a>Gérer les clés et les secrets

Après avoir créé un coffre, hello suivant les étapes toocreate et gérer les clés et les secrets dans le coffre hello.

## <a name="create-a-key"></a>Créer une clé

1. Se connecter dans le portail de l’utilisateur toohello (https://portal.local.azurestack.external).  

2. À partir du tableau de bord hello, cliquez sur **toutes les ressources** > coffre de clés hello select que vous avez créé précédemment > cliquez sur hello **clés** vignette.  

3. À partir de hello **clés** panneau, cliquez sur **ajouter**. 

4. Sur hello **créer une clé** panneau, formulaire de liste hello de **Options**, choisissez la méthode hello que vous souhaitez toouse toocreate une clé. Vous pouvez **Générer** une nouvelle clé, **Charger** une clé existante ou **Restaurer la sauvegarde** d’une clé.  

5. Entrez un **Nom** pour votre clé. nom de la clé Hello peut contenir uniquement des caractères alphanumériques et des tirets de caractère spécial hello (-).  

6. Éventuellement, configurez les valeurs **Définir la date d’activation** et **Définir la date d’expiration** pour votre clé.  

7. Cliquez sur **créer** déploiement de hello toostart.  

Une fois la clé de hello est correctement créé, vous pouvez le sélectionner dans hello **clés** panneau et afficher ou modifier ses propriétés. section des propriétés Hello contient hello **identificateur de clé**, un URI à laquelle des applications externes peuvent accéder à cette clé. opérations de toolimit sur cette clé, configurez les paramètres sous **opérations autorisées**.

![URI de clé](media/azure-stack-kv-manage-portal/image4.png)  

## <a name="create-a-secret"></a>Créer un secret 

1. Se connecter dans le portail de l’utilisateur toohello (https://portal.local.azurestack.external).  
2. À partir du tableau de bord hello, cliquez sur **toutes les ressources** > coffre de clés hello select que vous avez créé précédemment > cliquez sur hello **Secrets** vignette.  

3. À partir de hello **Secrets** panneau, cliquez sur **ajouter**.  

4. Sur hello **créer une clé secrète** panneau, à partir de la liste des hello **options de téléchargement**, choisissez une option en fonction duquel vous voulez toocreate un secret. Vous pouvez créer une clé secrète **manuellement** en entrant une valeur pour la clé secrète de hello, ou en téléchargeant un **certificat** à partir de votre ordinateur local.  

5. Entrez un **nom** pour secret de hello. nom de clé secrète Hello peut contenir uniquement des caractères alphanumériques et des tirets de caractère spécial hello (-).  

6. Si vous le souhaitez, spécifier hello **le type de contenu**et configurez les valeurs de **définir la date d’activation** et **définir la date d’expiration** valeurs pour la clé secrète de hello.  

7. Cliquez sur Créer toostart hello déploiement.  

Une fois que le secret de hello est correctement créé, vous pouvez le sélectionner dans hello **Secrets** panneau et afficher ou modifier ses propriétés. section des propriétés Hello contient **identificateur de clé secrète**, un URI par lequel les applications externes peuvent accéder à ce mot de passe. 

![URI de secret](media/azure-stack-kv-manage-portal/image5.png) 


## <a name="next-steps"></a>Étapes suivantes
* [Déployer un ordinateur virtuel par la récupération de mot de passe hello stocké dans un coffre de clés](azure-stack-kv-deploy-vm-with-secret.md)  
* [Déployer une machine virtuelle avec un certificat stocké dans un coffre de clés](azure-stack-kv-push-secret-into-vm.md)     


