---
title: "Publier des applications pour des utilisateurs individuels dans une collection Azure RemoteApp (version préliminaire) | Microsoft Docs"
description: "Apprenez à publier des applications dans Azure RemoteApp à l’attention d’utilisateurs spécifiques plutôt qu’à des groupes."
services: remoteapp-preview
documentationcenter: 
author: piotrci
manager: mbaldwin
editor: 
ms.assetid: 1fd0539d-fa65-4ea5-a98e-0be0cf580690
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: piotrci
ms.openlocfilehash: c94ffffdec3e46ed08d941ee58dcf17b432e1dad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="publish-applications-to-individual-users-in-an-azure-remoteapp-collection-preview"></a>Publier des applications pour des utilisateurs individuels dans une collection Azure RemoteApp (version préliminaire)
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .
> 
> 

Cet article explique comment publier des applications pour des utilisateurs individuels dans une collection Azure RemoteApp. Cette nouvelle fonctionnalité d’Azure RemoteApp, actuellement disponible en « version préliminaire privée », est réservée uniquement aux utilisateurs précoces à des fins d’évaluation.

À l’origine, Azure RemoteApp n’offrait qu’un seul moyen de « publier » des applications : l’administrateur devait publier les applications à partir de l’image pour les rendre visibles à tous les utilisateurs de la collection.

Dans un souci de réduction des coûts de gestion, il n’est pas rare que les administrateurs intègrent de nombreuses applications dans une même image et déploient une seule collection. Mais toutes les applications ne sont pas toujours utiles à l’ensemble des utilisateurs ; aussi, les administrateurs préféreront publier des applications à l’attention de certains utilisateurs spécifiques afin de ne pas les encombrer d’applications inutiles.

Azure RemoteApp offre désormais cette possibilité dans le cadre d’une fonctionnalité préliminaire limitée. Voici un bref résumé de cette nouvelle fonctionnalité :

1. Une collection peut être paramétrée dans deux modes différents :
   
   * le « mode collection » d’origine, grâce auquel tous les utilisateurs d’une collection peuvent visualiser l’ensemble des applications publiées. Il s’agit du mode par défaut ;
   * le nouveau « mode application », dans lequel les utilisateurs voient uniquement les applications qui leur ont été explicitement affectées
2. Pour le moment, le mode application ne peut être activé qu’à l’aide des applets de commande PowerShell pour Azure RemoteApp.
   
   * En mode application, l’affectation des utilisateurs dans la collection ne peut pas être gérée via le portail Azure. Elle ne peut être gérée qu’au moyen des applets de commande PowerShell.
3. Les utilisateurs ne voient que les applications qui ont été directement publiées à leur attention. Un utilisateur a toutefois la possibilité de lancer les autres applications disponibles sur l’image en y accédant directement depuis le système d’exploitation.
   
   * Cette fonctionnalité ne garantit pas un verrouillage sécurisé des applications ; elle ne fait que restreindre la visibilité dans le flux d’applications.
   * Si vous souhaitez isoler les utilisateurs de certaines applications, vous devez utiliser des collections distinctes.

## <a name="how-to-get-azure-remoteapp-powershell-cmdlets"></a>Comment obtenir les applets de commande PowerShell pour Azure RemoteApp
Pour tester la nouvelle fonctionnalité en version préliminaire, vous devez utiliser les applets de commande Azure PowerShell. Vous ne pouvez pas pour le moment utiliser le portail de gestion Azure pour activer le nouveau mode de publication d’applications.

Assurez-vous tout d’abord que vous disposez bien du [module Azure PowerShell](/powershell/azure/overview) .

Lancez ensuite la console PowerShell en mode administrateur, puis exécutez l’applet de commande suivante :

        Add-AzureAccount

Vous êtes invité à saisir vos nom d’utilisateur et mot de passe Azure. Une fois connecté, vous pouvez exécuter des applets de commande Azure RemoteApp sur vos abonnements Azure.

## <a name="how-to-check-which-mode-a-collection-is-in"></a>Comment vérifier le mode d’une collection
Exécutez l’applet de commande suivante :

        Get-AzureRemoteAppCollection <collectionName>

![Vérifier le mode de collecte](./media/remoteapp-perapp/araacllelvel.png)

La propriété AclLevel peut avoir les valeurs suivantes :

* Collection : mode de publication d’origine. Tous les utilisateurs peuvent visualiser l’ensemble des applications publiées.
* Application : nouveau mode de publication. Les utilisateurs voient uniquement les applications qui ont été directement publiées à leur attention.

## <a name="how-to-switch-to-application-publishing-mode"></a>Comment passer en mode de publication d’applications
Exécutez l’applet de commande suivante :

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

L’état de publication des applications est conservé : tous les utilisateurs voient l’ensemble des applications initialement publiées.

## <a name="how-to-list-users-who-can-see-a-specific-application"></a>Comment répertorier les utilisateurs autorisés à visualiser une application spécifique
Exécutez l’applet de commande suivante :

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

Cette commande permet de répertorier tous les utilisateurs pouvant visualiser l’application.

Remarque : vous pouvez voir les alias de l’application (appelés « app alias » dans la syntaxe ci-dessus) en exécutant l’applet de commande Get-AzureRemoteAppProgram - CollectionName <collectionName>.

## <a name="how-to-assign-an-application-to-a-user"></a>Comment affecter une application à un utilisateur
Exécutez l’applet de commande suivante :

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

L’utilisateur voit à présent l’application dans le client Azure RemoteApp et sera en mesure de s’y connecter.

## <a name="how-to-remove-an-application-from-a-user"></a>Comment supprimer une application d’un utilisateur
Exécutez l’applet de commande suivante :

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a>Appel à commentaires
Nous vous remercions de nous faire part de vos commentaires et suggestions concernant cette fonctionnalité en version préliminaire. Veuillez répondre à cette [enquête](http://www.instant.ly/s/FDdrb) pour nous dire ce que vous en pensez.

## <a name="havent-had-a-chance-to-try-the-preview-feature"></a>Vous n’avez pas eu l’occasion de tester la fonctionnalité en version préliminaire ?
Si vous n’avez pas encore participé à l’évaluation, utilisez cette [enquête](http://www.instant.ly/s/AY83p) pour demander l’accès à la fonctionnalité.

