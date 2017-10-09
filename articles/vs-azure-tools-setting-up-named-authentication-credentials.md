---
title: "aaaSetting des nommé identification | Documents Microsoft"
description: "Découvrez comment les informations d’identification de tootooprovide que Visual Studio peut utiliser tooauthenticate demandes tooAzure toopublish un tooAzure de l’application à partir de Visual Studio ou toomonitor existant service cloud... "
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 61570907-42a1-40e8-bcd6-952b21a55786
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/22/2017
ms.author: kraigb
ms.openlocfilehash: 3cc147a2f7a3e766293ca282f56078cf24281346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-named-authentication-credentials"></a>Configuration des informations d’authentification nommées
toopublish un tooAzure de l’application à partir de Visual Studio ou toomonitor un service cloud existant, vous devez fournir les informations d’identification que Visual Studio peut utiliser tooauthenticate demande tooAzure. Il existe plusieurs emplacements dans Visual Studio où vous pouvez vous connecter tooprovide ces informations d’identification. Par exemple, vous pouvez ouvrir à partir de l’Explorateur de serveurs de hello, le menu contextuel hello hello **Azure** nœud et choisissez **connecter tooMicrosoft abonnement Azure...** . Lorsque vous vous connectez, informations d’abonnement hello associées à votre compte Azure sont disponibles dans Visual Studio, et rien de plus, que vous avez toodo.

Windows Azure Tools prend également en charge un moyen plus anciens de fournir des informations d’identification, à l’aide de hello abonnement (fichier .publishsettings). Cette rubrique explique cette méthode, qui est toujours prise en charge dans le kit de développement logiciel (SDK) Azure 2.2.

Hello éléments suivants est requis pour l’authentification tooAzure :

* Votre ID d’abonnement
* Un certificat X.509 v3 valide

> [!NOTE]
> la longueur de clé du certificat X.509 v3 de hello Hello doit être au moins 2 048 bits. Azure rejette les certificats qui ne répondent pas à cette exigence ou qui ne sont pas valides.
>
>

Visual Studio utilise votre ID d’abonnement avec les données de certificat hello comme informations d’identification. les informations d’identification appropriées Hello sont référencées dans hello abonnement (fichier .publishsettings), qui contient une clé publique pour le certificat de hello. fichier d’abonnement Hello peut contenir des informations d’identification pour plusieurs abonnements.

Vous pouvez modifier les informations d’abonnement hello de hello **nouveau/modifier l’abonnement** boîte de dialogue, comme expliqué plus loin dans cette rubrique.

Si vous voulez toocreate un certificat vous-même, vous pouvez faire référence à des instructions toohello dans [créer et télécharger un certificat de gestion pour Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) , puis téléchargez manuellement hello certificat toohello [portail Azure classic ](http://go.microsoft.com/fwlink/?LinkID=213885).

> [!NOTE]
> Ces informations d’identification que Visual Studio requiert toomanage que vos services cloud ne sont pas hello les mêmes informations d’identification qui sont requis tooauthenticate une demande auprès des services de stockage Azure hello.
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a>Importer, configurer ou modifier des informations d’authentification dans Visual Studio
Vous pouvez importer, configurer ou modifier vos informations d’identification d’authentification Bonjour **nouvel abonnement** boîte de dialogue qui s’affiche si vous effectuez hello suivant l’action :

* Dans **l’Explorateur de serveurs**, ouvrez hello sur le menu contextuel hello **Azure** nœud, choisissez **gérer et filtrer les abonnements...** , choisissez hello **certificats** onglet et effectuez l’une des manières suivantes les hello :

    * Choisissez **importer** boîte de dialogue Importer les abonnements Microsoft Azure de hello tooopen où vous pouvez télécharger des fichiers d’abonnements hello pour hello actuellement chargés d’abonnement, parcourir tooits emplacement de téléchargement, puis l’importer pour une utilisation dans authentification.
    * Choisissez **nouveau** boîte de dialogue Nouvel abonnement de hello tooopen où vous pouvez configurer un nouvel abonnement pour utiliser l’authentification.
    * Choisissez **modifier** (après le choix de votre abonnement) boîte de dialogue Modifier un abonnement de hello tooopen où vous pouvez modifier un abonnement existant pour une utilisation dans l’authentification. 

Hello procédure suivante suppose que hello **nouvel abonnement** boîte de dialogue est ouverte.

### <a name="tooset-up-authentication-credentials-in-visual-studio"></a>tooset des informations d’identification de l’authentification dans Visual Studio
1. Bonjour **sélectionner un certificat existant** pour la liste d’authentification, choisissez un certificat.
2. Choisissez hello **chemin d’accès complet de copie hello** lien. chemin d’accès de Hello pour le certificat hello (fichier .cer) est copié toohello du Presse-papiers.

   > [!IMPORTANT]
   > toopublish votre application Windows Azure à partir de Visual Studio, vous devez télécharger ce certificat toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
   >
   >
3. tooupload hello certificat toohello portail Azure :

   1. Ouvrez hello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
   2. Si vous y êtes invité, connectez-vous au portail de toohello, puis accédez trop**paramètres**, **certificats de gestion**.
   3. Dans le volet de certificats de gestion hello, choisissez **télécharger**.
   4. Sélectionnez votre abonnement Azure, collez hello chemin d’accès complet de fichier .cer hello que vous venez de créée, puis choisissez **télécharger**.
