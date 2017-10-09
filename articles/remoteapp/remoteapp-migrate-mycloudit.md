---
title: la facturation aaaChange hello pour Azure RemoteApp | Documents Microsoft
description: "Découvrez comment toostop facturé pour Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 8f94da9a-7848-4ddc-b7b7-d9c280ccf4d7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: mbaldwin
ms.openlocfilehash: fe3841a88978ec56829932621489e75d5dd7e673
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-azure-remoteapp-toomycloudit"></a>Migrer à partir d’Azure RemoteApp tooMyCloudIT 

**Vous utilisez actuellement Microsoft Azure RemoteApp ?** : MyCloudIT créé un outil automatisé de toomigrate votre plateforme de gestion Azure RemoteApp (ARA) regroupements toohello MyCloudIT tout en continuant de toorun sur Microsoft Azure.

**Tirer parti du portail d’Azure Resource Manager hello**: migration terminée dans la plateforme de MyCloudIT hello permet le nouveau portail de Azure Resource Manager de bénéficier d’un accès tooAzure. Ce portail contient toutes les fonctionnalités nouvelles hello et innovations offertes par Microsoft Azure, y compris les accès tooVirtual Machine tailles tooensure votre déploiement repose toosupport les besoins de hello de votre entreprise.

**Tooensure parallèle hello bonne solution pour vos besoins de test**: l’outil de migration MyCloudIT hello est intégrée processus de migration tooinitiate hello et de test en parallèle tant que vos utilisateurs ARA actuels continuent toouse ARA.  Vos utilisateurs continuent d’exécuter ARA jusqu’à la fin de la migration et des tests.  outil de migration Hello repose collection ARA classique de toohandle hello.  Si vous pensez que vous avez un scénario unique, non standard, veuillez nous contacter à [ sales@conexlink.com ](mailto:sales@conexlink.com) afin de nous pouvons vous fournir un tooassist plan spécialement conçues pour la migration.

**Fonctionnalités de bureau-as-a-Service**: Veuillez noter que MyCloudIT permet non seulement des capacités de RemoteApp hello vous êtes habitué à, mais nous vous proposons complète bureau-As-A-Service fonctionnalités pour hello même coût par mois sans minimal d’utilisateurs configuration requise.

## <a name="what-we-will-do-for-you"></a>Ce que nous allons faire pour vous

MyCloudIT automatise la migration de votre modèle Azure RemoteApp à partir du portail Azure Classic de hello de votre portail du Gestionnaire de ressources Azure de votre abonnement avec notre outil de migration automatisée de toohello abonnement hello.  

> [!NOTE]
> Bonjour Azure RemoteApp modèle doit rester dans hello même région Azure que votre déploiement d’Azure RemoteApp d’origine.  Si vous avez besoin des régions Azure toochange ou des abonnements Azure pendant la migration de hello, veuillez nous contacter pour obtenir des instructions supplémentaires au [ sales@conexlink.com ](mailto:sales@conexlink.com).

Lisez ce qui suit pour obtenir des informations détaillées sur le processus de migration hello automatisée avec hello MyCloudIT l’outil de migration :

1. outil de migration Hello analyse votre ou vos abonnements en cours pour tous les déploiements ARA existants.  
2. Sélectionnez un ARA collection toomigrate à la fois.  Si vous avez plusieurs collections, exécutez notre outil autant de fois que nécessaire.
3. Vous disposez hello option toocopy hello disques de profil utilisateur (UPD) tooyour nouveau déploiement vous pouvez récupérer des données héritées, ou mapper manuellement des toohello nouveau déploiement. Si vous choisissez toocopy votre des, nous enregistrer hello des et inclure un fichier texte qui mappe le nom des utilisateurs hello UPD nom tooeach.  Hello des sera partage tooa copiés sur le serveur RDSMGMT hello `F:\Shares\LegacyUPD` et seront exposées via le partage de hello `\\RDSmgmt\LegacyUPD`. 
4. Votre migration ne perturbera pas votre déploiement ARA actuel.  Toutefois, si des modifications sont apportées toohello des (à partir de ARA) après la copie hello, ces modifications seront répercutées dans des hello stockées dans le portail d’Azure Resource Manager hello. 
5. Si vous avez des machines virtuelles supplémentaires tels que les contrôleurs de domaine et serveurs de fichiers dans votre réseau virtuel Azure Classic, nous définissons d’homologation entre votre réseau virtuel classique Azure existant de réseau virtuel et hello nouveau réseau virtuel nous crée pour vous, en nouvelle ressource Azure hello Gestionnaire de portail.
6. Notre solution automatisée uniquement établir le réseau virtuel d’homologation entre votre réseau virtuel classique Azure existant et hello nouveau réseau virtuel si votre déploiement ARA existant est un déploiement hybride ; Cela signifie que vous vous authentifiez avec un contrôleur de domaine d’Active Directory Windows Server Bonjour classique de réseau virtuel existant. Si nous n’établissent pas de réseau virtuel d’homologation pour votre collection, mais vous avez besoin d’homologation de réseau virtuel, veuillez nous contacter en tant que [ sales@conexlink.com ](mailto:sales@conexlink.com) et nous serons heureux tooconfigure réseau virtuel d’homologation sans coût supplémentaire.
7. Notre solution automatique garantit que votre configuration Azure DNS est mis à jour avec hello nouveau réseau virtuel paramètres tooensure votre nouveau déploiement peut se connecter tooyour existant de contrôleur de domaine dans hello réseau virtuel classique.
8. Notre solution automatisée garantit qu’il n’y a aucun conflit d’adresse IP que nous créez ce réseau virtuel et établir hello homologation de réseau virtuel pour les déploiements qui ont un serveur Active Directory de Windows Server existant.
9. Si vous utilisez Azure AD pour l’authentification, MyCloudIT crée un nouveau domaine d’Active Directory Windows Server et utiliser Azure AD Connect aux utilisateurs de toosynchronize entre l’instance d’Azure AD existante hello et hello que Windows Server Active Directory domaine créé par MyCloudIT.
10. Si vous utilisez aux utilisateurs de domaine Active Directory de Windows Server tooauthenticate ARA, notre solution automatisée se connecte à votre nouvelle tooyour de déploiement MyCloudIT existant du contrôleur de domaine Active Directory Windows Server via l’homologation du réseau virtuel.
11. Si vous utilisez Azure Active Directory Domain Services pour l’authentification, la migration est possible, mais contactez-nous afin que nous puissions vous proposer un plan de migration personnalisé.  Veuillez envoyer un courrier électronique trop[sales@conexlink.com](mailto:sales@conexlink.com). 
12. Une fois hello collection toobe migré est confirmée, confortablement et assouplir tandis que notre solution automatisée migre votre collection de ARA et disques de profil utilisateur (facultatif) toohello nouvelle MyCloudIT pilotés par les applications à distance.
13. Une fois le déploiement de hello est terminé, nous publierons nouveau hello mêmes applications qui ont été publiées Dans ARA et après le déploiement, vous serez en mesure de toopublish des applications supplémentaires.

## <a name="post-migration-benefits"></a>Avantages post-migration

1. Nous fournirons la console de gestion hello qui vous permet de toomanage hello complète du cycle de vie de votre déploiement d’applications à distance.
2. Vous serez en mesure de toomanage votre Virtual Machines à partir de notre portail.  Démarrez/arrêtez et redimensionnez des machines virtuelles individuelles si nécessaire.
3. console de gestion de Hello fournit hello toocreate de capacité et de gérer les utilisateurs / groupes à partir de notre portail de gestion.
4. console de gestion Hello fournit hello capacité toosynchronize aux utilisateurs avec Office 365 toocreate une expérience d’authentification même.
5. console de gestion Hello fournit hello capacité toocreate l’application à distance supplémentaires et des Collections de bureau sans coûts de l’utilisateur en double ou des spécifications d’utilisateur minimaux. 
6. console de gestion Hello permet hello toopublish nouvelles applications d’applications à distance.
7. console de gestion Hello fournit démarrage de hello tooschedule hello capacité et l’arrêt de votre déploiement d’applications à distance si vous devez uniquement votre solution pendant des heures spécifiques.
8. console de gestion Hello fournit hello capacité tooautomate hello et configure l’agent Azure Backup hello fournit un historique de rétention de document pour vos données client.
9. console de gestion Hello fournit des métriques de tooperformance d’accès de votre déploiement.  Ceci permet de vous hello tooidentify de capacité de goulots d’étranglement potentiels sans installer les outils de gestion supplémentaire des performances.
10. Si vous avez plusieurs hôtes de session, vous serez automatiquement tooenable en mesure de mise à l’échelle des session hello ainsi, seules hôtes qui doivent toobe en cours d’exécution sont en cours d’exécution.
11. MyCloudIT fournit un serveur de passerelle accès toohello RDWeb via un nom de domaine MyCloudIT.  Nous fournissons également hello capacité toore-hello URL tooa personnalisé URL du plan pour l’utilisateur final de personnalisation.

## <a name="prerequisites-for-migration"></a>Conditions requises pour la migration

1. Vous devez avoir accès toohello abonnement Azure qui héberge votre solution Azure RemoteApp en cours.
2. Vous devez accorder notre portail au sein de votre abonnement toomigrate votre modèle et le toocreate / modifier votre nouveau déploiement MyCloudIT.
3. Notez qu’en raison de la limitation tooa dans l’application Azure à distance, chaque collection peut être migrée uniquement trois fois.  Si vous devez toomigrate une collection de plus de trois fois, vous pouvez déclencher un tooincrease tooAzure de ticket votre nombre d’exportation, ou nous contacter et nous aidera à hello ARA tooincrease hello exportation nombre.

## <a name="mycloudit-billing"></a>Facturation MyCloudIT

Consultez [MyCloudIT tarification pour les Solutions RemoteApp](https://mcitdocuments.blob.core.windows.net/terms/MyCloudIT_Pricing_Overview.pdf) (PDF) pour plus d’informations sur la façon de toopredict et de gérer vos coûts global Azure.

Si vous avez toujours des questions, veuillez nous contacter à [ sales@conexlink.com ](mailto:sales@conexlink.com) ou regardez la vidéo de démonstration complète hello [outil de Migration Azure RemoteApp - MyCloudIT](https://www.youtube.com/watch?v=YQ_1F-JeeLM&t=482s). 

