---
title: "aaaHow toocreate une collection de cloud d’Azure RemoteApp | Documents Microsoft"
description: "Découvrez comment toocreate un déploiement d’Azure RemoteApp qui enregistre les données dans hello cloud Azure."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 4d7c6956-7e4a-4a41-b7f2-7e5832bf01e3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a072ad19d8293016382831d48d0af8e0f5e0d458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-cloud-collection-of-azure-remoteapp"></a>Comment toocreate une collection de cloud d’Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Il existe deux types de [collections Azure RemoteApp](remoteapp-collections.md): 

* Cloud : réside complètement dans Azure . Vous pouvez choisir toosave toutes les données dans le cloud de hello (pour une collection cloud uniquement) ou tooconnect votre tooa collection réseau virtuel et enregistrer des données.   
* Hybride : inclut un réseau virtuel pour un accès local - cela nécessite utilisez hello d’Azure AD et un environnement d’Active Directory local.

Ce didacticiel vous guide tout au long des processus de hello de création d’une collection de cloud. Il se compose de quatre étapes : 

1. Créez une collection Azure RemoteApp.
2. Vous pouvez éventuellement configurer une synchronisation d'annuaires. Si vous utilisez AD Azure + Active Directory, vous avez toosynchronize utilisateurs, contacts et les mots de passe du locataire tooyour Azure AD de votre Active Directory local.
3. Publiez des applications.
4. Configuration de l'accès utilisateur

**Avant de commencer**

Vous devez toodo qui suit hello avant la création de la collection de hello :

* [S’inscrire](https://azure.microsoft.com/services/remoteapp/) à Azure RemoteApp. 
* Collecter des informations sur les utilisateurs hello auxquels vous souhaitez accéder toogrant à. Il peut s'agir d'informations sur le compte Microsoft ou sur le compte professionnel Active Directory pour les utilisateurs.
* Cette procédure suppose que vous êtes soit toouse continu un hello d’images de modèle fourni dans le cadre de votre abonnement, ou que vous avez déjà téléchargé hello image de modèle toouse. Si vous devez tooupload une image de modèle différent, vous pouvez le faire à partir de la page d’Images de modèle hello. Cliquez simplement sur **télécharger une image de modèle** et suivez les étapes de hello dans l’Assistant de hello. 
* Vous souhaitez image Office 365 ProPlus de hello toouse ? Pour plus d’informations, cliquez [ici](remoteapp-officesubscription.md).
* Vous souhaitez tooprovide les applications personnalisées ou les programmes métier ? Créez une [image](remoteapp-imageoptions.md) et utilisez-la dans votre collection cloud.
* Déterminez si vous devez tooconnect tooa réseau virtuel. Si vous choisissez tooconnect tooa réseau virtuel, assurez-vous qu’il répond aux hello [instructions de dimensionnement](remoteapp-vnetsizing.md) et qu’il [peut se connecter à tooRemoteApp](remoteapp-vnet.md). Extraire hello [l’article de la planification de réseau virtuel ](remoteapp-planvnet.md)pour plus d’informations.
* Si vous utilisez un réseau virtuel, si vous décidez toojoin il tooyour dans le domaine Active Directory local.

## <a name="step-1-create-a-cloud-collection---with-or-without-a-vnet"></a>Étape 1 : créer une collection cloud avec ou sans réseau virtuel
Les étapes suivantes de hello utilisation trop**créer un regroupement uniquement dans le cloud**:

1. Dans le portail de gestion hello, accédez toohello RemoteApp page.
2. Cliquez sur **Nouveau > Création rapide**.
3. Entrez le nom de votre collection et sélectionnez votre région.
4. Choisissez plan hello que vous souhaitez toouse - de base ou standard.
5. Choisissez toouse de modèle hello pour cette collection. 
   
    **Conseil :** votre abonnement à RemoteApp est fourni avec [images de modèle](remoteapp-images.md) contenant Office 365 ou programmes Office 2013 (pour une utilisation d’évaluation), certains publication (telles que Word) et autres prêt toopublish. Vous pouvez également créer une [image](remoteapp-imageoptions.md) et l'utiliser dans votre collection cloud.
6. Cliquez sur **Créer une collection RemoteApp**.
   
    **Important :** peut prendre jusqu'à too30 minutes tooprovision votre collection.

Une fois que votre collection Azure RemoteApp a été créée, double-cliquez sur le nom hello de collection de hello. Qui s’affiche hello **Quick Start** page - il s’agit où vous avez terminé la configuration de la collection de hello.

Toocreate les étapes suivantes de hello utilisez un **cloud + collection de réseau virtuel**:

1. Dans le portail de gestion hello, accédez toohello Azure RemoteApp page.
2. Cliquez sur **Nouveau** > **Créer avec VNET**.
3. Entrez un nom pour votre collection.
4. Choisissez plan hello que vous souhaitez toouse - de base ou standard.
5. Choisissez hello réseau virtuel que vous avez déjà créé. Ne pas savoir comment toodo qui ? Pour l’instant, les étapes de hello sont Bonjour [hybride](remoteapp-create-hybrid-deployment.md) rubrique.
6. Décidez si vous devez toojoin votre domaine tooyour de collection. Si Oui, vous devez toouse AD Connect toointegrate Azure AD et votre environnement Active Directory. La procédure à suivre est traitée à l’ **étape 2**.
7. Cliquez sur **Créer une collection RemoteApp**.

## <a name="step-2-configure-active-directory-directory-synchronization-optional"></a>Étape 2 : configuration de la synchronisation d'annuaires Active Directory (facultatif)
Si vous souhaitez toouse Active Directory, Azure RemoteApp requiert la synchronisation d’annuaires entre Azure Active Directory et votre local Active Directory toosynchronize utilisateurs, contacts et client Azure Active Directory de tooyour des mots de passe. Consultez [Configuration d'Active Directory pour Azure RemoteApp](remoteapp-ad.md) pour obtenir des informations sur la planification. Vous pouvez également accéder directement trop[AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) pour plus d’informations.

## <a name="step-3-publish-apps"></a>Étape 3: publier des applications
Une application Azure RemoteApp est l’application hello ou un programme que vous fournissez aux utilisateurs de tooyour. Il se trouve dans l’image de modèle hello chargé pour la collection de hello. Lorsqu’un utilisateur accède à une application, l’application hello apparaît toorun dans leur environnement local, mais il est réellement exécuté sur une machine virtuelle dans Azure. 

Avant que vos utilisateurs peuvent accéder aux applications, vous devez toopublish leur permet d’applications des utilisateurs accèdent à des applications de hello par le biais de la publication hello client Bureau à distance.

Vous pouvez publier plusieurs applications tooyour collection Azure RemoteApp. Dans la page de publication hello, cliquez sur **publier** tooadd un programme. Vous pouvez publier à partir de hello **Démarrer** menu de l’image de modèle hello ou en spécifiant le chemin d’accès hello sur l’image de modèle hello pour une application hello. Si vous choisissez tooadd hello **Démarrer** menu, choisissez toopublish d’application hello. Si vous choisissez application toohello de tooprovide hello chemin d’accès, fournissez un nom pour l’application hello et hello toowhere de chemin d’accès que n’est installé sur l’image de modèle hello.

## <a name="step-4-configure-user-access"></a>Étape 4 : configuration de l'accès utilisateur
Maintenant que vous avez créé votre collection, vous devez tooadd hello utilisateurs que toouse en mesure de toobe vos ressources distantes. Si vous utilisez Active Directory, les utilisateurs de hello que vous fournissiez tooexist de tooneed d’accès dans le locataire d’Active Directory hello associé vous hello abonnement utilisé toocreate à cette collection.

1. Dans la page de démarrage rapide de hello, cliquez sur **configurer l’accès utilisateur**. 
2. Entrez hello Professionnel (à partir d’Active Directory) ou compte Microsoft auxquels vous souhaitez accéder toogrant pour.
   
   **Remarques :** 
   
   Assurez-vous que vous utilisez hello  *user@domain.com*  format.
   
   Si vous utilisez Office 365 ProPlus dans votre collection, vous devez utiliser des identités d’Active Directory hello pour vos utilisateurs. Cela permet de valider la licence. 
3. Une fois que les utilisateurs de hello sont validés, cliquez sur **enregistrer**.

## <a name="next-steps"></a>Étapes suivantes
Félicitations ! Vous avez créé et déployé correctement votre collection cloud Azure RemoteApp. étape suivante de Hello est toohave vos utilisateurs téléchargement et installer le client du Bureau à distance hello. Vous pouvez trouver des URL de hello pour le client de hello sur la page de démarrage rapide de Azure RemoteApp hello. Ensuite, munissez-vous du journal des utilisateurs dans le client de hello et accéder aux applications hello que vous avez publié.

### <a name="help-us-help-you"></a>Vos commentaires nous aideront à mieux vous servir
Saviez-vous que toorating d’ajout de cet article et de faire des commentaires vers le bas, vous pouvez effectuer modifications toohello article ? Il manque des informations ? Des informations sont erronées ? Certains passages ne sont pas clairs ? Faites défiler et cliquez sur **modifier sur GitHub** toomake modifications - ces proviendront toous pour révision et, une fois que nous se déconnecter sur ces derniers, vous verrez alors vos modifications et des améliorations ici.

