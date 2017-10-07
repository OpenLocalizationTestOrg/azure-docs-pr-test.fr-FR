---
title: "applications aaaPublish tooindividual les utilisateurs dans une collection Azure RemoteApp (version préliminaire) | Documents Microsoft"
description: "Découvrez comment vous pouvez publier des utilisateurs de tooindividual d’applications, au lieu d’en fonction des groupes dans Azure RemoteApp."
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
ms.openlocfilehash: 87b435552ddbfc2c6d03aeb01d95a44985e71f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-tooindividual-users-in-an-azure-remoteapp-collection-preview"></a>Publier des applications tooindividual les utilisateurs dans une collection Azure RemoteApp (version préliminaire)
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Cet article explique comment toopublish applications tooindividual les utilisateurs dans une collection Azure RemoteApp. Il s’agit de nouvelles fonctionnalités dans Azure RemoteApp, actuellement en aperçu privé et premiers tooselect uniquement disponible à des fins d’évaluation.

À l’origine Azure RemoteApp n'activé qu’une seule manière de publier des applications : administrateur de hello serait de publier des applications à partir de l’image de hello et ils seraient utilisateurs tooall visible dans la collection de hello.

Un scénario courant consiste à tooinclude de nombreuses applications dans une seule image et déploiement une collection dans les coûts de gestion ordre tooreduce. Souvent pas toutes les applications sont pertinentes tooall utilisateurs – les administrateurs préfèrent les utilisateurs de tooindividual toopublish applications afin qu’ils ne voyez pas les applications inutiles dans leur application de flux.

Azure RemoteApp offre désormais cette possibilité dans le cadre d’une fonctionnalité préliminaire limitée. Voici un bref résumé des nouvelles fonctionnalités de hello :

1. Une collection peut être paramétrée dans deux modes différents :
   
   * mode collection d’origine Hello, où tous les utilisateurs dans une collection peuvent voir toutes les applications publiées. Il s’agit de mode par défaut de hello.
   * nouveau mode d’application Hello, où les utilisateurs voient uniquement les applications qui ont été explicitement affecté toothem
2. Au moment de hello mode d’application hello ne peut être activé à l’aide des applets de commande PowerShell de Azure RemoteApp.
   
   * Quand définir le mode de tooapplication, affectation d’utilisateurs dans la collection de hello ne peut pas être géré via hello portail Azure. L’affectation d’utilisateurs a toobe géré via les applets de commande PowerShell.
3. Les utilisateurs voient seulement hello les applications publiées directement toothem. Toutefois, il peut être encore possible pour un utilisateur toolaunch hello autres applications disponibles sur l’image de hello en y accédant directement dans le système d’exploitation de hello.
   
   * Cette fonctionnalité ne fournit pas un verrouillage sécurisé d’applications. Il limite uniquement la visibilité dans l’application hello de flux.
   * Si vous devez tooisolate des utilisateurs à partir d’applications, vous devez toouse des regroupements séparés pour cela.

## <a name="how-tooget-azure-remoteapp-powershell-cmdlets"></a>Comment tooget applets de commande PowerShell de Azure RemoteApp
nouvelle fonctionnalité d’aperçu des hello de tootry, vous devez applets de commande Azure PowerShell toouse. Il n’est pas possible toouse hello Azure Management tooenable portail hello nouvelle application mode de publication.

Tout d’abord, assurez-vous que vous disposez hello [module Azure PowerShell](/powershell/azure/overview) installé.

Puis lancez console PowerShell de hello en mode administrateur et exécution hello suivant l’applet de commande :

        Add-AzureAccount

Vous êtes invité à saisir vos nom d’utilisateur et mot de passe Azure. Une fois connecté, vous serez en mesure de toorun Azure RemoteApp applets de commande par rapport à vos abonnements Azure.

## <a name="how-toocheck-which-mode-a-collection-is-in"></a>Comment toocheck quel mode d’une collection est en
Exécutez hello suivant l’applet de commande :

        Get-AzureRemoteAppCollection <collectionName>

![Vérifier le mode de collecte hello](./media/remoteapp-perapp/araacllelvel.png)

Hello AclLevel propriété peut avoir hello valeurs suivantes :

* Collection : hello d’origine mode de publication. Tous les utilisateurs peuvent visualiser l’ensemble des applications publiées.
* Application : hello nouveau mode de publication. Les utilisateurs voient uniquement les applications hello publié directement toothem.

## <a name="how-tooswitch-tooapplication-publishing-mode"></a>Comment le mode de publication tooapplication tooswitch
Exécutez hello suivant l’applet de commande :

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

État de publication application est conservé : initialement tous les utilisateurs verront toutes les applications publiées de hello d’origine.

## <a name="how-toolist-users-who-can-see-a-specific-application"></a>Comment les utilisateurs toolist qui peuvent voir une application spécifique
Exécutez hello suivant l’applet de commande :

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

Celle-ci répertorie tous les utilisateurs peuvent voir l’application hello.

Remarque : Vous pouvez voir des alias d’application hello (appelés « alias application » dans la syntaxe hello ci-dessus) en exécutant Get-AzureRemoteAppProgram - CollectionName <collectionName>.

## <a name="how-tooassign-an-application-tooa-user"></a>Comment tooassign un utilisateur d’application tooa
Exécutez hello suivant l’applet de commande :

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

utilisateur de Hello bénéficient d’application hello dans le client d’Azure RemoteApp hello et sera en mesure de tooconnect tooit.

## <a name="how-tooremove-an-application-from-a-user"></a>Comment tooremove une application à partir d’un utilisateur
Exécutez hello suivant l’applet de commande :

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a>Appel à commentaires
Nous vous remercions de nous faire part de vos commentaires et suggestions concernant cette fonctionnalité en version préliminaire. Veuillez remplir hello [enquête](http://www.instant.ly/s/FDdrb) toolet dites-nous ce que vous pensez.

## <a name="havent-had-a-chance-tootry-hello-preview-feature"></a>N’ont pas eu une fonctionnalité d’aperçu chance tootry hello ?
Si vous n’avez pas encore participé à la version préliminaire de hello, utilisez ce [enquête](http://www.instant.ly/s/AY83p) toorequest accès.

