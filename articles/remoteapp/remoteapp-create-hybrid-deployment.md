---
title: "Comment créer une collection hybride pour Azure RemoteApp | Microsoft Docs"
description: "Découvrez comment créer un déploiement de RemoteApp qui se connecte à votre réseau interne."
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
ms.openlocfilehash: 346a5fe3e4011985e4247ceef0d5ca858049fd28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-hybrid-collection-for-azure-remoteapp"></a>Création d'une collection hybride pour Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .
> 
> 

Il existe deux types de collection Azure RemoteApp :

* Cloud : réside complètement dans Azure . Vous pouvez soit enregistrer toutes les données dans le cloud (la collection se trouve uniquement dans le cloud), soit connecter votre collection à un réseau virtuel et enregistrer vos données dans celui-ci.   
* Hybride : inclut un réseau virtuel pour l’accès local (nécessite Azure AD et un environnement Active Directory local).

Vous ne savez pas de quoi vous avez besoin ? Consultez [De quel type de collection avez-vous besoin pour Azure RemoteApp ?](remoteapp-collections.md)

Ce didacticiel vous familiarise avec la procédure de création d'une collection hybride. Elle comprend huit étapes :

1. Choix de l’ [image](remoteapp-imageoptions.md) à utiliser pour votre collection. Vous pouvez créer une image personnalisée ou utiliser l’une des images Microsoft incluses dans votre abonnement.
2. Configuration de votre réseau virtuel. Passez en revue les informations concernant la [planification](remoteapp-planvnet.md) et le [dimensionnement d’un réseau virtuel](remoteapp-vnetsizing.md).
3. Création d’une collection.
4. Association de votre collection à votre domaine local.
5. Ajout d'une image de modèle à votre collection.
6. Configuration d'une synchronisation d'annuaires. Azure RemoteApp exige que vous intégriez Azure Active Directory soit 1) en configurant la synchronisation Azure Active Directory avec l’option de synchronisation de mot de passe ou 2) en configurant Azure Active Directory sans option de synchronisation de mot de passe, mais à l’aide d’un domaine fédéré à AD FS. Consultez les [informations de configuration d'Active Directory avec RemoteApp](remoteapp-ad.md).
7. Publication d'applications RemoteApp.
8. Configuration de l'accès utilisateur

**Avant de commencer**

Avant de créer la collection, vous devez effectuer les étapes suivantes :

* [S’inscrire](https://azure.microsoft.com/services/remoteapp/) à Azure RemoteApp.
* Créer un compte d’utilisateur dans Active Directory à utiliser comme compte de service Azure RemoteApp. Limiter les autorisations pour ce compte, de telle sorte qu'il puisse uniquement joindre des ordinateurs au domaine.
* Collecter des informations sur votre réseau local : adresse IP et périphérique VPN.
* Installer le module [Azure PowerShell](/powershell/azure/overview) .
* Collecter des informations sur les utilisateurs auxquels vous souhaitez accorder l'accès. Vous aurez besoin du nom d’utilisateur principal Azure Active Directory (par exemple, name@contoso.com) pour chaque utilisateur. Assurez-vous que le nom UPN soit cohérent entre Azure AD et Active Directory.
* Choisir votre image de modèle. Une image de modèle Azure RemoteApp contient les applications et les programmes que vous souhaitez publier pour les utilisateurs. Consultez les [options d’images Azure RemoteApp](remoteapp-imageoptions.md) pour plus d’informations.
* Vous souhaitez utiliser l'image d'Office 365 ProPlus ? Pour plus d’informations, cliquez [ici](remoteapp-officesubscription.md).
* [Configuration d'Active Directory pour RemoteApp](remoteapp-ad.md).

## <a name="step-1-set-up-your-virtual-network"></a>Étape 1 : configuration de votre réseau virtuel
Vous pouvez déployer une collection hybride qui utilise un réseau virtuel Azure existant ou vous pouvez créer un réseau virtuel. Un réseau virtuel permet aux utilisateurs d'accéder aux données de votre réseau local via des ressources distantes de RemoteApp. L'utilisation d'un réseau virtuel Azure offre à votre collection un accès réseau direct aux autres services Azure et aux machines virtuelles déployées sur ce réseau virtuel.

Passez en revue les informations sur la [planification](remoteapp-planvnet.md) et le [dimensionnement d'un réseau virtuel](remoteapp-vnetsizing.md) avant de créer votre réseau virtuel.

### <a name="create-an-azure-vnet-and-join-it-to-your-active-directory-deployment"></a>Création d'un réseau virtuel Azure et jonction à votre déploiement Active Directory
Commencez par créer un [réseau virtuel](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). Cette opération s’effectue sous l’onglet **Réseau** dans le Portail Azure. Vous devez connecter votre réseau virtuel au déploiement Active Directory qui est synchronisé avec votre locataire Azure Active Directory.

Pour plus d’informations, consultez [Créer un réseau virtuel à l’aide du Portail Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) .

### <a name="make-sure-your-virtual-network-is-ready-for-azure-remoteapp"></a>Vérification que votre réseau virtuel est prêt pour Azure RemoteApp
Avant de créer votre collection, assurez-vous que votre nouveau réseau virtuel est prêt. Vous pouvez le confirmer en procédant comme suit :

1. Créez une machine virtuelle Azure dans le sous-réseau du réseau virtuel que vous venez de créer pour RemoteApp.
2. Utilisez le Bureau à distance pour se connecter à la machine virtuelle. (Cliquez sur **Connecter**.)
3. Joignez-la au même déploiement Active Directory que celui que vous voulez utiliser pour RemoteApp.

Tout s'est bien passé ? Votre réseau virtuel et le sous-réseau sont prêts pour Azure RemoteApp !

Vous trouverez plus d'informations sur la création de machines virtuelles Azure et leur connexion au Bureau à distance [ici](https://msdn.microsoft.com/library/azure/jj156003.aspx).

## <a name="step-2-create-an-azure-remoteapp-collection"></a>Étape 2 : créer une collection Azure RemoteApp
1. Accédez à la page Azure RemoteApp du [portail Azure](http://manage.windowsazure.com).
2. Cliquez sur **Nouveau > Créer avec VNET**.
3. Entrez un nom pour votre collection.
4. Choisissez le plan que vous souhaitez utiliser (de base ou standard).
5. Choisissez votre réseau virtuel dans la liste déroulante, puis votre sous-réseau.
6. Choisissez de le joindre à votre domaine.
7. Cliquez sur **Créer une collection RemoteApp**.

Après avoir créé votre collection Azure RemoteApp, double-cliquez sur son nom. Ceci affiche la page **Démarrage rapide** qui vous permet de terminer la configuration de la collection.

Un problème est survenu ? Consultez les [informations de dépannage d'une collection hybride](remoteapp-hybridtrouble.md).

## <a name="step-3-link-your-collection-to-the-local-domain"></a>Étape 3 : liaison de votre collection au domaine local
1. Dans la page **Démarrage rapide**, cliquez sur **joindre un domaine local**.
2. Ajoutez le compte de service Azure RemoteApp à votre domaine Active Directory local. Vous aurez besoin du nom de domaine, de l'unité d'organisation, ainsi que du nom d'utilisateur et du mot de passe du compte de service.
   
    Voici les informations collectées si vous avez suivi les étapes de la procédure [Configuration d'Active Directory pour Azure RemoteApp](remoteapp-ad.md).

## <a name="step-4-link-to-an-azure-remoteapp-image"></a>Étape 4 : établir un lien vers une image Azure RemoteApp
Une image de modèle Azure RemoteApp contient les programmes que vous souhaitez partager avec les utilisateurs. Vous pouvez créer une [image de modèle](remoteapp-imageoptions.md) ou un lien vers une image existante (une image déjà importée ou téléchargée vers Azure RemoteApp). Vous pouvez également établir un lien avec l'une des [images de modèle](remoteapp-images.md) Azure RemoteApp contenant des programmes Office 365 ou Office 2013 (à des fins d'évaluation).

Si vous optez pour le téléchargement de la nouvelle image, vous devez entrer un nom et choisir son emplacement. Plusieurs cmdlets PowerShell sont affichés sur la page suivante de l'Assistant. Copiez-les et exécutez-les à partir d'une invite de commandes Windows PowerShell avec élévation de privilèges afin de télécharger l'image spécifiée.

En cas d’association d’une image de modèle existante, il vous suffit de spécifier le nom de l’image, son emplacement et l’abonnement Azure associé.

## <a name="step-5-configure-active-directory-directory-synchronization"></a>Étape 5 : configuration de la synchronisation d'annuaires Active Directory
Azure RemoteApp exige que vous intégriez Azure Active Directory soit 1) en configurant la synchronisation Azure Active Directory avec l’option de synchronisation de mot de passe ou 2) en configurant Azure Active Directory sans option de synchronisation de mot de passe, mais à l’aide d’un domaine fédéré à AD FS.

Consultez [AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) : cet article vous permet de configurer l’intégration d’annuaire en 4 étapes.

Pour plus d'informations sur la planification, consultez la rubrique [Programme de synchronisation d'annuaires](http://msdn.microsoft.com//library/azure/hh967642.aspx) .

## <a name="step-6-publish-apps"></a>Étape 6 : publier des applications
Une application Azure RemoteApp correspond à l’application ou au programme que vous fournissez à vos utilisateurs. Elle se trouve dans l'image de modèle que vous avez téléchargée pour la collection. Quand un utilisateur accède à une application, celle-ci semble s'exécuter dans son environnement local. En réalité, elle s'exécute dans Azure.

Avant que vos utilisateurs puissent accéder à des applications, vous devez les publier. Ceci permet à vos utilisateurs d'y accéder via le client Bureau à distance.

Vous pouvez publier plusieurs applications dans votre collection. Dans la page de publication, cliquez sur **Publier** pour ajouter une application. Vous pouvez publier l'application à partir du menu **Démarrer** de l'image de modèle ou en indiquant le chemin d'accès dans l'image de modèle de l'application. Si vous choisissez d'ajouter l'application à partir du menu **Démarrer** , sélectionnez le programme à ajouter. Si vous choisissez la deuxième option, indiquez un nom pour l'application ainsi que le chemin d'accès à son répertoire d'installation dans l'image de modèle.

## <a name="step-7-configure-user-access"></a>Étape 7 : configuration de l'accès utilisateur
Maintenant que vous avez créé votre collection, vous devez ajouter les utilisateurs qui seront autorisés à utiliser vos ressources distantes. Ceux-ci doivent exister dans le locataire Active Directory associé à l’abonnement que vous avez utilisé pour créer cette collection Azure RemoteApp.

1. Sur la page Démarrage rapide, cliquez sur **Configurer l'accès utilisateur**.
2. Entrez le compte professionnel (à partir d'Active Directory) ou le compte Microsoft auquel vous souhaitez accorder l'accès.
   
   **Remarques :**
   
   Assurez-vous d’utiliser le format *user@domain.com*.
   
   Si vous utilisez Office 365 ProPlus dans votre collection, vous devez utiliser les identités Active Directory de vos utilisateurs. Cela permet de valider la licence.
3. Une fois les utilisateurs validés, cliquez sur **Enregistrer**.

## <a name="next-steps"></a>Étapes suivantes
Félicitations ! Vous avez créé et déployé correctement votre collection hybride Azure RemoteApp. L'étape suivante consistera à faire en sorte que vos utilisateurs téléchargent et installent le client Bureau à distance. L’URL du client est disponible dans la page Démarrage rapide de RemoteApp. Les utilisateurs peuvent à présent se connecter au client et accéder aux applications que vous avez publiées.

### <a name="help-us-help-you"></a>Vos commentaires nous aideront à mieux vous servir
Saviez-vous qu’en plus de noter cet article et de rédiger des commentaires ci-dessous, vous pouviez modifier l’article lui-même ? Il manque des informations ? Des informations sont erronées ? Certains passages ne sont pas clairs ? Faites défiler l’écran vers le haut et cliquez sur **Modifier sur GitHub** pour apporter des modifications. Nous les passerons ensuite en revue, et une fois que nous les aurons confirmées, vos modifications et les améliorations seront visibles ici.

