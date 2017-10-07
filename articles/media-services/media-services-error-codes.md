---
title: "codes d’erreur aaaAzure Media Services | Documents Microsoft"
description: "rubrique de Hello donne une vue d’ensemble des codes d’erreur Azure Media Services."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d3a62a64-7608-4b17-8667-479b26ba0d6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: de1ffd6dee8901a3051eb5032536c3669482d6b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-error-codes"></a>Codes d’erreur d’Azure Media Services
Lorsque vous utilisez Microsoft Azure Media Services, vous pouvez recevoir des codes d’erreur HTTP à partir du service hello en fonction des problèmes tels que des jetons d’authentification expire tooactions qui ne sont pas pris en charge dans Media Services. Hello Voici une liste de **codes d’erreur HTTP** qui peuvent être renvoyés par les Services de support et hello possible provoque pour eux.  

## <a name="400-bad-request"></a>400 Demande incorrecte
demande de Hello contient des informations non valides et qu’il est rejeté échéance tooone Hello suivant raisons :

* La version spécifiée de l’API n’est pas prise en charge. Pour la version la plus récente hello, consultez [le programme d’installation pour le développement d’API REST Media Services](media-services-rest-how-to-use.md).
* version de Hello API de Media Services n’est pas spécifiée. Pour plus d’informations sur la façon dont toospecify hello version de l’API, consultez [référence d’API REST Media Services Operations](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).
  
  > [!NOTE]
  > Si vous utilisez hello .NET ou les kits de développement logiciel Java tooMedia de tooconnect Services, version de l’API de hello est automatiquement spécifiée chaque fois que vous essayez et effectuez certaines actions sur Media Services.
  > 
  > 
* Une propriété non définie a été spécifiée. nom de la propriété Hello est dans le message d’erreur hello. Vous ne pouvez spécifier que des propriétés membres d’une entité donnée. Pour obtenir la liste des entités et de leurs propriétés, voir [Référence de l’API REST d’Azure Media Services](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).
* Une valeur de propriété non valide a été spécifiée. nom de la propriété Hello est dans le message d’erreur hello. Consultez le lien précédent de hello pour les types de propriété valide et leurs valeurs.
* Une valeur de propriété requise est manquante.
* Partie de l’URL de hello spécifiée contient une valeur incorrecte.
* Une tentative a été effectuée tooupdate une propriété WriteOnce.
* Une tentative a été effectuée toocreate une tâche qui a un élément multimédia d’entrée avec un élément AssetFile principal qui n’a été spécifié ou n’a pas pu être déterminé..
* Une tentative a été effectuée tooupdate un localisateur SAS. Des localisateurs de SAP peuvent uniquement être créés ou supprimés. Des localisateurs de streaming peuvent être mis à jour. Pour plus d’informations, voir [Localisateurs](https://docs.microsoft.com/rest/api/media/operations/locator).
* Une opération ou demande non prises en charge ont été envoyées.

## <a name="401-unauthorized"></a>401 Non autorisé
demande de Hello n’a pas pu être authentifié (avant d’être autorisé) échéance tooone Hello suivant raisons :

* En-tête d’authentification absent.
* Valeur d’en-tête d’authentification incorrecte.
  * Hello jeton a expiré. 
  * jeton de Hello contient une signature non valide.

## <a name="403-forbidden"></a>403 Interdit
demande de Hello n’est pas autorisée en raison tooone Hello suivant raisons :

* Hello compte Media Services est introuvable ou a été supprimé.
* Hello compte Media Services est désactivé et le type de demande hello n’est pas HTTP GET. Les opérations de service renvoient également une réponse 403.
* Hello jeton d’authentification ne contient pas informations d’identification de l’utilisateur hello : AccountName et/ou ID d’abonnement. Vous pouvez trouver ces informations Bonjour extension de l’interface utilisateur des Services de support pour votre compte Media Services Bonjour portail de gestion Azure.
* ressource de Hello ne peut pas être accessible.
  
  * Une tentative a été effectuée toouse un MediaProcessor qui n’est pas disponible pour votre compte Media Services.
  * Une tentative a été effectuée tooupdate un JobTemplate défini par Media Services.
  * Une tentative a été effectuée toooverwrite recherche de certains autres compte Media Services.
  * Une tentative a été effectuée toooverwrite ContentKey de certaines autres Media Services du compte.
* ressource de Hello n’a pas pu être créé en raison de quota de service tooa qui a été atteint pour le compte de service de média hello. Pour plus d’informations sur les quotas de service hello, consultez [Quotas et Limitations](media-services-quotas-and-limitations.md).

## <a name="404-not-found"></a>404 Introuvable
demande de Hello n’est pas autorisée sur une ressource échéance tooone Hello suivant raisons :

* Une tentative a été effectuée tooupdate une entité qui n’existe pas.
* Une tentative a été effectuée toodelete une entité qui n’existe pas.
* Une tentative a été effectuée toocreate une entité qui lie l’entité tooan qui n’existe pas.
* Une tentative a été effectuée tooGET une entité qui n’existe pas.
* Une tentative a été effectuée toospecify un compte de stockage qui n’est pas associé avec hello compte Media Services.  

## <a name="409-conflict"></a>409 Conflit
demande de Hello n’est pas autorisée en raison tooone Hello suivant raisons :

* Plusieurs AssetFile a nom spécifié de hello dans hello Asset.
* Une tentative a été effectuée toocreate un deuxième principal AssetFile dans hello actif.
* Une tentative a été effectuée toocreate une ContentKey avec hello spécifié Id déjà utilisé.
* Une tentative a été effectuée toocreate un localisateur avec hello spécifié Id déjà utilisé.
* Plus d’un IngestManifestFile a nom spécifié de hello dans hello IngestManifest.
* Une tentative a été effectuée toolink une deuxième ContentKey toohello de stockage chiffrement chiffré de stockage de ressources.
* Une tentative a été effectuée toolink hello même ContentKey toohello actif.
* Une tentative a été effectuée toocreate un tooan de recherche de la ressource dont conteneur de stockage est manquant ou n’est plus associé hello actif.
* Une tentative a été effectuée toocreate un tooan de recherche actif qui possède déjà des 5 localisateurs en cours d’utilisation. (Le stockage azure applique la limite de hello de cinq stratégies d’accès partagé sur un conteneur de stockage.)
* Liaison de compte de stockage d’un IngestManifestAsset de tooan actif n’est pas hello même que le compte de stockage hello utilisé par le parent de hello IngestManifest.  

## <a name="500-internal-server-error"></a>500 Erreur interne du serveur
Pendant le traitement de hello de demande de hello, Media Services rencontre une erreur qui empêche le traitement de hello de se poursuivre. Cela peut être dû tooone Hello suivant raisons :

* Création d’un élément multimédia ou un travail échoue, car les informations de quota de service du compte de service de média hello sont temporairement indisponibles.
* Création d’un conteneur de stockage d’objets blob actif ou IngestManifest échoue, car les informations de compte de stockage du compte hello sont temporairement indisponibles.
* Autre erreur inattendue.

## <a name="503-service-unavailable"></a>503 Service indisponible
le serveur de Hello est actuellement incapable de tooreceive demandes. Cette erreur peut résulter de service de toohello des demandes excessives. Mécanisme de limitation de Media Services restreint l’utilisation des ressources pour les applications qui rendent excessive de demander un service toohello hello.

> [!NOTE]
> Vérification hello erreur message et erreur code chaîne tooget plus d’informations sur la raison de hello que vous avez obtenu hello erreur 503. Cette erreur n’indique pas toujours une limitation.
> 
> 

Les descriptions d’état possibles sont les suivantes :

* « Le serveur est occupé. Des exécutions précédentes de ce type de demande ont pris plus de {0} secondes. »
* « Le serveur est occupé. Plus de {0} demandes par seconde peuvent être limitées. »
* « Le serveur est occupé. Plus de {0} demandes en {1} secondes peuvent être limitées. »

toohandle cette erreur, nous vous recommandons d’utiliser exponentielle temporisation logique de nouvelle tentative. Cela implique d’utiliser des attentes de plus en plus longues entre nouvelles tentatives suite à des réponses d’erreur consécutives.  Pour plus d’informations, voir [What Does the Transient Fault Handling Application Block Do?](https://msdn.microsoft.com/library/hh680905.aspx) (Que fait le bloc applicatif de gestion des erreurs temporaires ?).

> [!NOTE]
> Si vous utilisez [Azure Media Services SDK pour .net](https://github.com/Azure/azure-sdk-for-media-services/tree/master), logique de nouvelle tentative hello pour erreur de hello 503 a été implémentée par hello SDK.  
> 
> 

## <a name="see-also"></a>Voir aussi
[Codes d’erreur de gestion de Media Services](http://msdn.microsoft.com/library/windowsazure/dn167016.aspx)

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

