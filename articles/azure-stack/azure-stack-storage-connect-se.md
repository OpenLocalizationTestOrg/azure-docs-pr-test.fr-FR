---
title: "Explorateur de stockage d’aaaConnect tooan abonnement de la pile de Azure"
description: "Découvrez comment tooconnect stockage Exporer tooan abonnement de la pile de Azure"
services: azure-stack
documentationcenter: 
author: xiaofmao
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/24/2017
ms.author: xiaofmao
ms.openlocfilehash: 8508fcf41a114ff58f57582b4a6021d8050aabe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-storage-explorer-tooan-azure-stack-subscription"></a>Connecter l’Explorateur de stockage tooan Azure pile abonnement

Explorateur de stockage Azure (aperçu) est une application autonome qui vous permet de travail tooeasily avec des données de pile le stockage Azure sur Windows, Mac OS et Linux. Il existe plusieurs outils tenant compte toomove données tooand à partir de la pile le stockage Azure. Pour plus d’informations, consultez [Outils de transfert de données pour le stockage Azure Stack](azure-stack-storage-transfer.md).

Dans cet article, vous apprendrez comment tooconnect tooyour stockage de Azure pile comptes à l’aide Explorateur de stockage. 

Si vous n’avez pas installé l’Explorateur Stockage, [téléchargez](http://www.storageexplorer.com/)-le et installez-le.

Après la connexion d’abonnement de Azure pile tooyour, vous pouvez utiliser hello [articles de l’Explorateur de stockage Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) toowork avec vos données de la pile de Azure. 

## <a name="prepare-an-azure-stack-subscription"></a>Préparer un abonnement Azure Stack

Vous devez accéder au bureau de l’ordinateur hôte toohello Azure pile ou une connexion VPN pour l’abonnement de pile d’Azure Storage Explorer tooaccess hello. toolearn tooset d’un tooAzure de connexion VPN pile, voir [connecter tooAzure pile avec VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).

Pourquoi le Kit de développement de pile Azure, vous devez certificat d’autorité racine tooexport hello Azure pile.

### <a name="tooexport-and-then-import-hello-azure-stack-certificate"></a>tooexport, puis importer un certificat Azure pile hello

1. Ouvrez `mmc.exe` sur un ordinateur hôte de pile d’Azure, ou sur un ordinateur local avec un tooAzure de connexion VPN pile. 

2. Dans **fichier**, sélectionnez **ajouter/supprimer un composant logiciel enfichable**, puis ajoutez **certificats** toomanage **compte d’ordinateur** de **Local Ordinateur**.



3. Sous **Racine de la console\Certificats (ordinateur local)\Autorités de certification racines de confiance\Certificats**, recherchez **AzureStackSelfSignedRootCert**.

    ![Charger un certificat de racine hello Azure pile via mmc.exe][25]

4. Certificat de hello avec le bouton droit, sélectionnez **toutes les tâches** > **exporter**, puis suivez hello instructions tooexport hello certificat **codé à Base 64 X.509 (. CER)**.  

    certificat exporté de Hello sera utilisé à l’étape suivante de hello.
5. Démarrage de l’Explorateur de stockage (version préliminaire), et si vous voyez hello **connecter tooAzure stockage** boîte de dialogue zone, annulez cette opération.

6. Sur hello **modifier** menu, pointez trop**certificats SSL**, puis cliquez sur **les certificats d’importation**. Utilisez le toofind boîte dialogue hello fichier sélecteur et certificat hello ouverts que vous avez exporté à l’étape précédente de hello.

    Après l’importation, vous êtes invité à toorestart Explorateur de stockage.

    ![Importer un certificat hello dans l’Explorateur de stockage (version préliminaire)][27]

Vous êtes maintenant prêt tooconnect abonnement de pile d’Azure Storage Explorer tooan.

### <a name="tooconnect-an-azure-stack-subscription"></a>tooconnect un abonnement Azure pile


1. Après le redémarrage de l’Explorateur de stockage (version préliminaire), sélectionnez hello **modifier** menu, puis assurez-vous que **cible Azure pile** est sélectionnée. Si elle n’est pas sélectionnée, sélectionnez-la et redémarrez l’Explorateur de stockage pour modifier un effet de tootake hello. Cette configuration est requise pour la compatibilité avec votre environnement Azure Stack.

    ![S’assurer que l’option Target Azure Stack (Cibler Azure Stack) est sélectionnée][28]

7. Dans le volet gauche de hello, sélectionnez **gérer les comptes**.  
    Tous les comptes de Microsoft hello que vous êtes connecté en tooare affiché.

8. tooconnect toohello compte de la pile d’Azure, sélectionnez **ajouter un compte**.

    ![Ajouter un compte Azure Stack][29]

9. Bonjour **connecter tooAzure stockage** boîte de dialogue **environnement Azure**, sélectionnez **utilisez Azure pile environnement**, puis cliquez sur **suivant**.

10. toosign avec hello compte Azure pile qui est associé au moins un abonnement Azure pile actif, renseignez hello **connecter tooAzure environnement pile** boîte de dialogue.  

    Détails de Hello pour chaque champ sont les suivantes :

    * **Nom de l’environnement**: champ de hello peut être personnalisé par l’utilisateur.
    * **Point de terminaison de ressource ARM**: hello des exemples de points de terminaison de ressource Azure Resource Manager :

        * Pour un opérateur cloud :<br> https://adminmanagement.local.azurestack.external   
        * Pour un locataire :<br> https://management.local.azurestack.external
 
    * **ID de locataire** : Facultatif. Hello est donné uniquement lorsque hello répertoire doit être spécifié.

12. Après que vous être connecté avec un compte Azure pile, volet de gauche hello est remplie avec les abonnements de pile de Azure hello associés à ce compte. Sélectionnez les abonnements Azure pile hello que vous souhaitez toowork avec, puis sélectionnez **appliquer**. (Activant ou désactivant hello **tous les abonnements** case à cocher active ou désactive la sélection de tous ou aucun des hello répertorié abonnements de la pile de Azure.)

    ![Sélectionnez les abonnements Azure pile hello après avoir complété la boîte de dialogue d’environnement en nuage personnalisée hello][30]  
    volet de gauche de Hello affiche les comptes de stockage hello associées aux abonnements Azure pile de hello sélectionné.

    ![Liste des comptes de stockage, y compris les comptes d’abonnement Azure Stack][31]

## <a name="next-steps"></a>Étapes suivantes
* [Bien démarrer avec l’Explorateur Stockage (préversion)](../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [Stockage Azure Stack : Différences et considérations](azure-stack-acs-differences.md)


* toolearn en savoir plus sur le stockage Azure, consultez [Introduction tooMicrosoft stockage Azure](../storage/common/storage-introduction.md)

[25]: ./media/azure-stack-storage-connect-se/add-certificate-azure-stack.png
[26]: ./media/azure-stack-storage-connect-se/export-root-cert-azure-stack.png
[27]: ./media/azure-stack-storage-connect-se/import-azure-stack-cert-storage-explorer.png
[28]: ./media/azure-stack-storage-connect-se/select-target-azure-stack.png
[29]: ./media/azure-stack-storage-connect-se/add-azure-stack-account.png
[30]: ./media/azure-stack-storage-connect-se/select-accounts-azure-stack.png
[31]: ./media/azure-stack-storage-connect-se/azure-stack-storage-account-list.png
