---
title: aaaHow toocreate une collection hybride pour Azure RemoteApp | Documents Microsoft
description: "Découvrez comment toocreate un déploiement de RemoteApp qui relie le réseau interne de tooyour."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 08ea0ce3-3a2c-4ddf-9394-6d75c8030cb1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 3fba29acc676e0af48e995da406f889c532c44c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-hybrid-collection-for-azure-remoteapp"></a>Comment toocreate une collection hybride pour Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Il existe deux types de collection Azure RemoteApp :

* Cloud : réside complètement dans Azure . Vous pouvez choisir toosave toutes les données dans le cloud de hello (pour une collection cloud uniquement) ou tooconnect votre tooa collection réseau virtuel et enregistrer des données.   
* Hybride : inclut un réseau virtuel pour un accès local - cela nécessite utilisez hello d’Azure AD et un environnement d’Active Directory local.

Vous ne savez pas de quoi vous avez besoin ? Consultez [De quel type de collection avez-vous besoin pour Azure RemoteApp ?](remoteapp-collections.md)

Ce didacticiel vous guide tout au long des processus de hello de création d’une collection hybride. Elle comprend huit étapes :

1. Déterminer les éléments [image](remoteapp-imageoptions.md) toouse pour votre collection. Vous pouvez créer une image personnalisée ou utiliser une des images de Microsoft hello inclus dans votre abonnement.
2. Configuration de votre réseau virtuel. Extraire hello [planification de réseau virtuel](remoteapp-planvnet.md) et [sizing](remoteapp-vnetsizing.md) plus d’informations.
3. Création d’une collection.
4. Joindre votre domaine local tooyour de collection.
5. Ajouter une collection de tooyour d’image du modèle.
6. Configuration d'une synchronisation d'annuaires. Azure RemoteApp requiert que vous intégrez avec Azure Active Directory à un (1) configuration synchronisation Azure Active Directory avec l’option de synchronisation de mot de passe de hello ou (2) configuration synchronisation Azure Active Directory sans option de synchronisation de mot de passe hello, mais à l’aide d’un domaine tooAD fédérée FS. Extraire hello [les informations de configuration d’Active Directory avec RemoteApp](remoteapp-ad.md).
7. Publication d'applications RemoteApp.
8. Configuration de l'accès utilisateur

**Avant de commencer**

Vous devez toodo qui suit hello avant la création de la collection de hello :

* [S’inscrire](https://azure.microsoft.com/services/remoteapp/) à Azure RemoteApp.
* Créer un compte d’utilisateur dans Active Directory toouse comme hello compte de service Azure RemoteApp. Limitez les autorisations de hello pour ce compte pour qu’il puisse rejoindre uniquement domaine toohello de machines.
* Collecter des informations sur votre réseau local : adresse IP et périphérique VPN.
* Installer hello [Azure PowerShell](/powershell/azure/overview) module.
* Collecter des informations sur les utilisateurs hello auxquels vous souhaitez accéder toogrant à. Vous devez serez hello nom d’utilisateur principal Azure Active Directory (par exemple, name@contoso.com) pour chaque utilisateur. Vérifiez que hello UPN identique dans Azure AD et Active Directory.
* Choisir votre image de modèle. Une image de modèle Azure RemoteApp contient les applications hello et les programmes que vous souhaitez toopublish pour vos utilisateurs. Consultez les [options d’images Azure RemoteApp](remoteapp-imageoptions.md) pour plus d’informations.
* Vous souhaitez image Office 365 ProPlus de hello toouse ? Pour plus d’informations, cliquez [ici](remoteapp-officesubscription.md).
* [Configuration d'Active Directory pour RemoteApp](remoteapp-ad.md).

## <a name="step-1-set-up-your-virtual-network"></a>Étape 1 : configuration de votre réseau virtuel
Vous pouvez déployer une collection hybride qui utilise un réseau virtuel Azure existant ou vous pouvez créer un réseau virtuel. Un réseau virtuel permet aux utilisateurs d'accéder aux données de votre réseau local via des ressources distantes de RemoteApp. À l’aide d’un réseau virtuel Azure donne à votre tooother de l’accès réseau direct collection services Azure et les ordinateurs virtuels déployés toothat des réseaux virtuels.

Assurez-vous que vous passez en revue hello [planification de réseau virtuel](remoteapp-planvnet.md) et [taille du réseau virtuel](remoteapp-vnetsizing.md) informations avant de créer votre réseau virtuel.

### <a name="create-an-azure-vnet-and-join-it-tooyour-active-directory-deployment"></a>Créer un réseau virtuel Azure et de joindre le déploiement d’Active Directory tooyour
Commencez par créer un [réseau virtuel](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). Cette opération est effectuée sur hello **réseau** onglet Bonjour portail Azure. Vous devez tooconnect votre déploiement d’Active Directory de client Azure Active Directory synchronisé tooyour du toohello réseau virtuel.

Consultez [créer un réseau virtuel à l’aide de hello portail Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) pour plus d’informations.

### <a name="make-sure-your-virtual-network-is-ready-for-azure-remoteapp"></a>Vérification que votre réseau virtuel est prêt pour Azure RemoteApp
Avant de créer votre collection, assurez-vous que votre nouveau réseau virtuel est prêt. Vous pouvez le vérifier en procédant comme suit de hello :

1. Créer une machine virtuelle Azure à l’intérieur du sous-réseau hello du réseau virtuel de hello que vous venez de créer pour RemoteApp.
2. Utilisez un ordinateur de bureau à distance tooconnect toohello virtuel. (Cliquez sur **Connecter**.)
3. Joindre toohello même déploiement Active Directory que vous souhaitez toouse pour RemoteApp.

Tout s'est bien passé ? Votre réseau virtuel et le sous-réseau sont prêts pour Azure RemoteApp !

Vous trouverez plus d’informations sur la création de machines virtuelles et de connexion toothem avec le Bureau à distance [ici](https://msdn.microsoft.com/library/azure/jj156003.aspx).

## <a name="step-2-create-an-azure-remoteapp-collection"></a>Étape 2 : créer une collection Azure RemoteApp
1. Bonjour [portail Azure](http://manage.windowsazure.com), accédez toohello Azure RemoteApp page.
2. Cliquez sur **Nouveau > Créer avec VNET**.
3. Entrez un nom pour votre collection.
4. Choisissez plan hello que vous souhaitez toouse - de base ou standard.
5. Choisissez votre réseau virtuel hello liste déroulante et ensuite votre sous-réseau.
6. Choisissez toojoin il tooyour domaine.
7. Cliquez sur **Créer une collection RemoteApp**.

Une fois que votre collection Azure RemoteApp a été créée, double-cliquez sur le nom hello de collection de hello. Qui s’affiche hello **Quick Start** page - il s’agit où vous avez terminé la configuration de la collection de hello.

Un problème est survenu ? Extraire hello [collection hybride des informations de dépannage](remoteapp-hybridtrouble.md).

## <a name="step-3-link-your-collection-toohello-local-domain"></a>Étape 3 : Relier votre domaine local toohello de collection
1. Sur hello **Quick Start** , cliquez sur **joindre un domaine local**.
2. Ajouter le domaine de Active Directory local de hello Azure RemoteApp service compte tooyour. Vous devez le nom de domaine hello, unité d’organisation, nom d’utilisateur de compte de service et un mot de passe.
   
    Il s’agit d’informations hello collectées si vous avez suivi les étapes de hello dans [configurer Active Directory pour Azure RemoteApp](remoteapp-ad.md).

## <a name="step-4-link-tooan-azure-remoteapp-image"></a>Étape 4 : Image d’Azure RemoteApp lien tooan
Une image de modèle Azure RemoteApp contient les programmes hello que vous souhaitez tooshare avec des utilisateurs. Vous pouvez créer un nouveau [image de modèle](remoteapp-imageoptions.md) ou image existante du lien tooan (déjà importé ou téléchargé tooAzure RemoteApp). Vous pouvez également lier tooone Hello Azure RemoteApp [images de modèle](remoteapp-images.md) contenant des programmes Office 2013 (pour un essai) ou Office 365.

Si vous téléchargez une nouvelle image de hello, vous devez tooenter hello nom et choisir l’emplacement hello pour l’image de hello. Sur la page suivante de hello d’Assistant de hello, vous voyez un ensemble d’applets de commande PowerShell, copie et exécuter ces applets de commande à partir une avec élévation de privilèges Windows PowerShell invite tooupload hello image spécifiée.

Si vous attachez une image de modèle existante tooan, spécifiez simplement le nom de l’image hello, l’emplacement et un abonnement Azure associé.

## <a name="step-5-configure-active-directory-directory-synchronization"></a>Étape 5 : configuration de la synchronisation d'annuaires Active Directory
Azure RemoteApp requiert que vous intégrez avec Azure Active Directory à un (1) configuration synchronisation Azure Active Directory avec l’option de synchronisation de mot de passe de hello ou (2) configuration synchronisation Azure Active Directory sans option de synchronisation de mot de passe hello, mais à l’aide d’un domaine tooAD fédérée FS.

Consultez [AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) : cet article vous permet de configurer l’intégration d’annuaire en 4 étapes.

Pour plus d'informations sur la planification, consultez la rubrique [Programme de synchronisation d'annuaires](http://msdn.microsoft.com//library/azure/hh967642.aspx) .

## <a name="step-6-publish-apps"></a>Étape 6 : publier des applications
Une application Azure RemoteApp est l’application hello ou un programme que vous fournissez aux utilisateurs de tooyour. Il se trouve dans l’image de modèle hello chargé pour la collection de hello. Lorsqu’un utilisateur accède à une application, il s’affiche toorun dans leur environnement local, mais il est réellement exécuté dans Azure.

Avant que vos utilisateurs peuvent accéder aux applications, vous devez toopublish leur – Cela permet à vos applications de hello d’accès aux utilisateurs via le client du Bureau à distance hello.

Vous pouvez publier la collection de tooyour plusieurs applications. Dans la page de publication hello, cliquez sur **publier** tooadd une application. Vous pouvez publier à partir de hello **Démarrer** menu de l’image de modèle hello ou en spécifiant le chemin d’accès hello sur l’image de modèle hello pour une application hello. Si vous choisissez tooadd hello **Démarrer** menu, choisissez tooadd de programme hello. Si vous choisissez application toohello de tooprovide hello chemin d’accès, fournissez un nom pour l’application hello et hello toowhere de chemin d’accès que n’est installé sur l’image de modèle hello.

## <a name="step-7-configure-user-access"></a>Étape 7 : configuration de l'accès utilisateur
Maintenant que vous avez créé votre collection, vous devez tooadd hello utilisateurs que toouse en mesure de toobe vos ressources distantes. les utilisateurs de Hello, vous devez fournir tooexist de tooneed d’accès dans le locataire d’Active Directory hello associé vous hello abonnement utilisé toocreate cette collection Azure RemoteApp.

1. Dans la page de démarrage rapide de hello, cliquez sur **configurer l’accès utilisateur**.
2. Entrez hello Professionnel (à partir d’Active Directory) ou compte Microsoft auxquels vous souhaitez accéder toogrant pour.
   
   **Remarques :**
   
   Assurez-vous que vous utilisez hello  *user@domain.com*  format.
   
   Si vous utilisez Office 365 ProPlus dans votre collection, vous devez utiliser des identités d’Active Directory hello pour vos utilisateurs. Cela permet de valider la licence.
3. Une fois que les utilisateurs de hello sont validés, cliquez sur **enregistrer**.

## <a name="next-steps"></a>Étapes suivantes
Félicitations ! Vous avez créé et déployé correctement votre collection hybride Azure RemoteApp. étape suivante de Hello est toohave vos utilisateurs téléchargement et installer le client du Bureau à distance hello. Vous pouvez trouver des URL de hello pour le client de hello sur la page de démarrage rapide de Azure RemoteApp hello. Ensuite, munissez-vous du journal des utilisateurs dans le client de hello et accéder aux applications hello que vous avez publié.

### <a name="help-us-help-you"></a>Vos commentaires nous aideront à mieux vous servir
Saviez-vous que toorating d’ajout de cet article et de faire des commentaires vers le bas, vous pouvez effectuer modifications toohello article ? Il manque des informations ? Des informations sont erronées ? Certains passages ne sont pas clairs ? Faites défiler et cliquez sur **modifier sur GitHub** toomake modifications - ces proviendront toous pour révision et, une fois que nous se déconnecter sur ces derniers, vous verrez alors vos modifications et des améliorations ici.

