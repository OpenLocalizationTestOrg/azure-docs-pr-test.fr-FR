---
ms.assetid: 
title: "suppression réversible de coffre de clés aaaAzure | Documents Microsoft"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/10/2017
ms.openlocfilehash: 1b402c58db6f25ae4ae5e2720786fa81eb0e839a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-soft-delete-overview"></a>Vue d’ensemble de la suppression réversible d’Azure Key Vault

Fonctionnalité de suppression réversible du coffre de clés permet de récupérer des coffres de hello supprimé et les objets de coffre, appelés soft-suppression. Plus précisément, nous adresser hello les scénarios suivants :

- Prise en charge de la suppression récupérable d’un coffre de clés
- Prise en charge de la suppression récupérable d’objets Key Vault (par exemple, clés, secrets et certificats)

## <a name="supporting-interfaces"></a>Prise en charge des interfaces

Hello soft-suppression fonctionnalité est disponible via hello REST, .NET / C# et PowerShell d’interfaces. Pour ces valeurs pour plus d’informations, consultez le toohello références [clé de coffre référence](https://docs.microsoft.com/azure/key-vault/).

## <a name="scenarios"></a>Scénarios

Les coffres Azure Key Vault désignent des ressources suivies, gérées par Azure Resource Manager. Azure Resource Manager spécifie également un comportement bien défini pour la suppression, qui suppose qu’une opération DELETE correctement exécutée sur une ressource ne permet plus d’accéder à cette ressource. adresses de fonctionnalité de soft-suppression Hello hello récupération de l’objet de hello supprimée, si la suppression de hello était accidentelle ou intentionnelle.

1. Dans ce scénario hello, un utilisateur a peut-être accidentellement supprimé un coffre de clés ou un objet de coffre de clés ; Si ce coffre de clés ou une clé de coffre objet ont été toobe récupérables pendant une période prédéterminée, utilisateur de hello peut annuler la suppression de hello et récupérer leurs données.

2. Dans un autre scénario, un utilisateur non autorisé peut tenter de toodelete un coffre de clés ou un objet de coffre de clés, telle qu’une clé à l’intérieur d’un coffre, toocause une interruption de service. Séparation de suppression hello de coffre de clés hello ou un objet de coffre de clés à partir de la suppression effective de hello Hello les données sous-jacentes utilisable comme une mesure de sécurité en limitant les autorisations tooa de suppression de données différent, par exemple, approuvés rôle. Cette approche suppose d’appliquer un quorum à une opération donnée qui pourrait, dans d’autres circonstances, se traduire par une perte de données immédiate.

### <a name="soft-delete-behavior"></a>Comportement de la suppression réversible

Avec cette fonctionnalité, hello opération DELETE sur un coffre de clés ou un objet de coffre de clés est une soft-suppression contiennent efficacement des ressources de hello pour une période de rétention donnée, alors que donnant apparence de hello cet objet hello est supprimé. service Hello plus fournit un mécanisme pour récupérer l’objet hello supprimé, essentiellement annuler la suppression hello. 

La suppression réversible est un comportement facultatif de Key Vault et **n’est pas activée par défaut** dans cette version. Pour plus d’informations sur l’activation de soft-suppression de votre coffre de clés, consultez les conseils spécifiques de hello dans référence hello pour interface hello de votre choix, [clé de coffre référence](https://docs.microsoft.com/azure/key-vault/).

### <a name="key-vault-recovery"></a>Récupération d’un Key Vault

Lors de la suppression d’un coffre de clés, service de hello crée une ressource de proxy sous abonnement hello, ajout de suffisamment de métadonnées pour la récupération. ressource de proxy Hello est un objet stocké, disponible dans hello même emplacement que le coffre de clés hello supprimé. 

### <a name="key-vault-object-recovery"></a>Récupération d’objets Key Vault

Lors de la suppression d’un objet de coffre de clés, comme une clé de service de hello placera les objet hello dans un état supprimé, ce qui rend les opérations d’extraction tooany inaccessible. Dans cet état, objet de coffre de clés hello ne peut figurer, récupérés, ou forcer/définitivement supprimés. 

À hello même coffre de clés, en temps planifierez suppression hello Hello sous-jacent toohello correspondantes de données supprimée coffre de clés ou un objet de coffre de clés pour l’exécution après un intervalle de rétention prédéterminée. Hello DNS record toohello coffre correspondant est également conservé pendant l’intervalle de conservation hello hello.

### <a name="soft-delete-retention-period"></a>Période de rétention de la suppression réversible

Les ressources ayant fait l’objet d’une suppression réversible sont conservées pendant une durée fixée à 90 jours. Au cours de l’intervalle de conservation de soft-suppression hello suivant de hello s’appliquent :

- Vous pouvez répertorier toutes les coffres de clé hello et objets de coffre de clés dans l’état soft-suppression de hello pour votre abonnement, ainsi que les accès suppression et la récupération d’informations sur les.
    - Seuls les utilisateurs disposant d’autorisations spéciales peuvent répertorier des coffres supprimés. Nous recommandons à nos utilisateurs de créer un rôle personnalisé avec ces autorisations spéciales pour le traitement des coffres supprimés.
- Un coffre de clés avec le même nom ne peut pas être créé dans hello de hello même emplacement. en conséquence, un objet de coffre de clés ne peut pas être créé dans un coffre-fort donné si ce coffre de clés contient un objet avec hello même nom et qui se trouve dans un état supprimé 
- Seul un utilisateur privilégié spécifiquement peut restaurer un coffre de clés ou un objet de coffre de clés en exécutant une commande de récupération sur la ressource de proxy hello correspondante.
    - utilisateur de Hello, membre de rôle personnalisée hello disposant hello privilège toocreate un coffre de clés de groupe de ressources hello peut restaurer le coffre hello.
- Seul un utilisateur privilégié spécifiquement peut supprimer de force un coffre de clés ou un objet de coffre de clés en émettant une commande delete sur la ressource de proxy hello correspondante.

Sauf si un coffre de clés ou un objet de coffre de clés est récupérée, hello fin du service de hello rétention intervalle hello effectue un vidage de coffre de clés hello supprimé ou un objet de coffre de clés et son contenu. La suppression de la ressource ne peut pas être replanifiée.

### <a name="permitted-purge"></a>Vidage autorisé

Supprimer définitivement, de purge, un coffre de clés est possible grâce à une opération POST sur la ressource de proxy hello et nécessite des privilèges spéciaux. En général, seul hello propriétaire sera en mesure de toopurge un coffre de clés. déclencheurs d’opération Hello POST hello immédiate et irrécupérable suppression de ce coffre. 

Une exception toothis arrive hello lorsque hello abonnement Azure a été marquée comme étant *impossible à supprimer*. Dans ce cas, uniquement les service hello peut effectuer puis suppression effective de hello et fait un processus planifié. 



