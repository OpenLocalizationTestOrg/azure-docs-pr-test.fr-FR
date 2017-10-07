---
title: "messages aaaEDIFACT pour l’intégration d’entreprise B2B - Azure Logic Apps | Documents Microsoft"
description: "Échanger des messages EDIFACT au format EDI dans le cadre d’une intégration d’entreprise B2B avec Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 2257d2c8-1929-4390-b22c-f96ca8b291bc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/26/2016
ms.author: LADocs; jonfan
ms.openlocfilehash: 496fadcda58de2d36459202b839b0a63c9e5857c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-edifact-messages-for-enterprise-integration-with-logic-apps"></a>Échanger des messages EDIFACT pour l’intégration d’entreprise avec Logic Apps

Avant de pouvoir échanger des messages EDIFACT pour Azure Logic Apps, vous devez créer un contrat EDIFACT et le stocker dans votre compte d’intégration. Voici la procédure hello pour la toocreate un accord EDIFACT.

> [!NOTE]
> Cette page couvre les fonctionnalités d’EDIFACT hello pour Azure Logic Apps. Pour plus d’informations, consultez [X12](logic-apps-enterprise-integration-x12.md).

## <a name="before-you-start"></a>Avant de commencer

Voici les éléments hello que vous devez :

* Un [compte d’intégration](../logic-apps/logic-apps-enterprise-integration-accounts.md) déjà défini et associé à votre abonnement Azure  
* Au moins deux [partenaires](logic-apps-enterprise-integration-partners.md) déjà définis dans votre compte d’intégration

> [!NOTE]
> Lorsque vous créez un accord, le contenu de hello dans les messages hello que vous recevez ou envoyez tooand du partenaire de hello doit correspondre au type de contrat hello.

Une fois que vous avez [créé un compte d’intégration](../logic-apps/logic-apps-enterprise-integration-accounts.md) et [ajouté des partenaires](logic-apps-enterprise-integration-partners.md), vous pouvez créer un contrat EDIFACT en procédant comme suit.

## <a name="create-an-edifact-agreement"></a>Créer un contrat EDIFACT 

1.  Connectez-vous à toohello [portail Azure](http://portal.azure.com "portail Azure"). Dans le menu de gauche hello, sélectionnez **davantage de services**.

    > [!TIP]
    > Si vous ne voyez pas **davantage de services**, vous pouvez avoir des menus de hello tooexpand tout d’abord. Haut hello du menu de hello réduit, sélectionnez **menu Afficher**.

    ![Dans le menu de gauche, cliquez sur « Plus de services »](./media/logic-apps-enterprise-integration-edifact/edifact-0.png)

2. Dans la zone de recherche de hello, tapez « intégration » pour votre filtre. Dans la liste des résultats hello, sélectionnez **comptes d’intégration**.

    ![Filtrer sur « intégration », sélectionner « Comptes d’intégration »](./media/logic-apps-enterprise-integration-edifact/edifact-1-3.png)

3. Bonjour **comptes d’intégration** panneau qui s’ouvre, le compte d’intégration hello sélectionnez où vous souhaitez l’accord de hello toocreate.
Si aucun compte d’intégration ne s’affiche, [créez-en un](../logic-apps/logic-apps-enterprise-integration-accounts.md "Tout sur les comptes d’intégration").  

    ![Sélectionnez le compte de l’intégration où toocreate hello accord](./media/logic-apps-enterprise-integration-edifact/edifact-1-4.png)

4. Choisissez hello **accords** vignette. Si vous n’avez pas une vignette de contrats, ajoutez d’abord les mosaïques hello.   

    ![Choisissez la mosaïque « Contrats »](./media/logic-apps-enterprise-integration-edifact/edifact-1-5.png)

5. Dans le panneau des accords hello qui s’ouvre, choisissez **ajouter**.

    ![Choisir « Ajouter »](./media/logic-apps-enterprise-integration-edifact/edifact-agreement-2.png)

6. Sous **Ajouter**, entrez le **nom** de votre contrat. Pour le **type de contrat**, sélectionnez **EDIFACT**. Sélectionnez hello **partenaire hôte**, **identité de l’hôte**, **partenaire invité**, et **invité identité** pour votre accord.

    ![Renseigner les détails relatifs au contrat](./media/logic-apps-enterprise-integration-edifact/edifact-1.png)

    | Propriété | Description |
    | --- | --- |
    | Nom |Nom de contrat de hello |
    | Type de contrat | Doit être EDIFACT |
    | Partenaire hôte |Un contrat nécessite un partenaire hôte et un partenaire invité. partenaire d’accueil Hello représente l’organisation hello qui configure l’accord de hello. |
    | Identité de l’hôte |Un identificateur pour le partenaire d’accueil hello |
    | Partenaire invité |Un contrat nécessite un partenaire hôte et un partenaire invité. partenaire invité de Hello représente l’organisation hello qui effectue l’entreprise avec le partenaire d’accueil hello. |
    | identité de l’invité |Un identificateur de partenaire invité de hello |
    | Paramètres de réception |Ces propriétés s’appliquent tooall les messages reçus par un accord. |
    | Paramètres d’envoi |Ces propriétés s’appliquent tooall les messages envoyés par un accord. |

## <a name="configure-how-your-agreement-handles-received-messages"></a>Configuration du traitement des messages reçus

Maintenant que vous avez défini les propriétés de l’accord hello, vous pouvez configurer comment cet accord identifie et traite les messages entrants reçus à partir de votre partenaire via ce contrat.

1.  Sous **Ajouter**, sélectionnez **Paramètres de réception**.
Configurez ces propriétés en fonction de votre accord avec le partenaire hello qui échange des messages avec vous. Pour obtenir des descriptions de propriété, consultez les tableaux de hello dans cette section.

    L’option **Paramètres de réception** est organisée en plusieurs sections : identificateurs, accusé de réception, schémas, numéros de contrôle, validations et paramètres internes.

    ![Configurer les « Paramètres de réception »](./media/logic-apps-enterprise-integration-edifact/edifact-2.png)  

2. Une fois que vous avez terminé, assurez-vous que toosave vos paramètres en choisissant **OK**.

À présent, votre contrat toohandle prêt entrante messages conformes tooyour les paramètres sélectionnés.

### <a name="identifiers"></a>Identificateurs

| Propriété | Description |
| --- | --- |
| UNB6.1 (mot de passe de référence du destinataire) |Entrez une valeur alphanumérique comprise entre 1 et 14 caractères. |
| UNB6.2 (qualificateur de référence du destinataire) |Entrez une valeur numérique contenant deux caractères maximum. |

### <a name="acknowledgments"></a>Remerciements

| Propriété | Description |
| --- | --- |
| Réception des messages (CONTRL) |Sélectionnez cette case à cocher de tooreturn un expéditeur des échanges toohello technique (CONTRL) d’accusé de réception. accusé de réception Hello est envoyée toohello expéditeur des échanges en fonction de hello paramètres d’envoi pour l’accord de hello. |
| Accusé de réception (CONTRL) |Sélectionnez cette tooreturn de case à cocher qu'un fonctionnel (CONTRL) d’accusé de réception toohello échange expéditeur hello accusé de réception est envoyé toohello expéditeur des échanges en fonction de hello paramètres d’envoi pour l’accord de hello. |

### <a name="schemas"></a>Schémas

| Propriété | Description |
| --- | --- |
| UNH2.1 (TYPE) |Sélectionnez un type de document informatisé. |
| UNH2.2 (VERSION) |Entrez le numéro de version de message hello. (un caractère minimum ; 3 caractères maximum). |
| UNH2.3 (VERSION FINALE) |Entrez le numéro de version du message hello. (un caractère minimum ; 3 caractères maximum). |
| UNH2.5 (CODE AFFECTÉ ASSOCIÉ) |Entrez le code de hello attribué. (6 caractères maximum. Doit contenir des valeurs alphanumériques). |
| UNG2.1 (ID DE L’EXPÉDITEUR D’APPLICATION) |Entrez une valeur numérique comprenant entre un et 35 caractères. |
| UNG2.2 (QUALIFICATEUR DE L’EXPÉDITEUR D’APPLICATION) |Entrez une valeur alphanumérique comprenant quatre caractères maximum. |
| Schéma |Sélectionnez hello téléchargé précédemment schéma toouse à partir de votre compte d’intégration associés. |

### <a name="control-numbers"></a>Numéros de contrôle
| Propriété | Description |
| --- | --- |
| Interdire les doublons de numéro de contrôle d’échange |tooblock les échanges en double, sélectionnez cette propriété. Si sélectionné, hello Action de décoder EDIFACT vérifie que numéro de contrôle hello échange (UNB5) pour l’échange hello reçu ne correspond pas à un numéro de contrôle traités précédemment. Si une correspondance est détectée, échange de hello n’est pas traitée. |
| Check for duplicate UNB5 every (days) (Vérifier les doublons UNB5 tous les (jours)) |Si vous avez choisi de numéros de contrôle d’échange en double toodisallow, vous pouvez spécifier le nombre de hello de jours quand tooperform hello vérifier en attribuant la valeur appropriée de hello pour ce paramètre. |
| Interdire les numéros de contrôle de groupe en double |tooblock échanges avec des numéros de contrôle de groupe dupliqués (UNG5), sélectionnez cette propriété. |
| Interdire les numéros de contrôle de document informatisé en double |tooblock les échanges avec des transactions en double numéros de contrôle (UNH1), sélectionnez cette propriété. |
| Numéro de contrôle d’accusé de réception EDIFACT |toodesignate hello informatisé des numéros de référence pour une utilisation dans un accusé de réception, entrez une valeur pour le préfixe de hello, une plage de numéros de référence et un suffixe. |

### <a name="validations"></a>Validations

Une nouvelle ligne de validation est automatiquement ajoutée dès que la ligne précédente est terminée. Si vous ne spécifiez pas de règles, la validation utilise ligne « Par défaut » de hello.

| Propriété | Description |
| --- | --- |
| Type de message |Sélectionnez le type de message EDI hello. |
| Validation EDI |Effectuer une validation EDI sur les types de données, tel que défini par du schéma hello EDI propriétés, les restrictions de longueur, éléments de données vides et les séparateurs de fin. |
| Validation étendue |Si le type de données hello n’est pas EDI, la validation est sur la condition de l’élément données hello et autorisé de répétition, les énumérations et les données élément validation de la longueur (min/max). |
| Autoriser les zéros de début ou de fin |Conservez les zéros de début ou de fin ainsi que les caractères d’espace supplémentaires. Ne supprimez pas ces caractères. |
| Supprimer les zéros de début ou de fin |Supprimez les zéros de début ou de fin ainsi que les caractères d’espace. |
| Stratégie de séparateur de fin |Générez des séparateurs de fin. <p>Sélectionnez **interdit** tooprohibit des délimiteurs et séparateurs Bonjour reçu l’échange. Si l’échange de hello a des délimiteurs et séparateurs, échange de hello est déclaré non valide. <p>Sélectionnez **facultatif** tooaccept des échanges avec ou sans délimiteurs et séparateurs. <p>Sélectionnez **obligatoire** lorsque échange de salutation reçue doit avoir des délimiteurs et séparateurs. |

### <a name="internal-settings"></a>Paramètres internes

| Propriété | Description |
| --- | --- |
| Créer des balises XML vides si les séparateurs de fin sont autorisés |Sélectionnez cet expéditeur hello toohave case à cocher Inclure vide les balises XML pour les séparateurs de fin. |
| Scinder l’échange en documents informatisés : suspendre les documents informatisés en cas d’erreur|Analyse chaque document informatisé d’un échange en un document XML distinct en appliquant l’enveloppe appropriée toohello hello document informatisé. Suspendre uniquement hello documents informatisés dont la validation échouent. |
| Scinder l’échange en documents informatisés : suspendre l’échange en cas d’erreur|Analyse chaque document informatisé d’un échange en un document XML distinct en appliquant l’enveloppe appropriée de hello. Suspendre l’ensemble de l’échange hello lors de la validation d’un ou plusieurs documents informatisés dans l’échange de hello échouent. | 
| Préserver l'échange : suspendre les documents informatisés en cas d’erreur |Toucher l’échange de hello, crée un document XML pour l’échange entier hello. Suspendre les uniquement hello documents informatisés dont la validation échouent, tout en continuant tooprocess définit toutes les autres transactions. |
| Préserver l’échange : suspendre l’échange en cas d’erreur |Toucher l’échange de hello, crée un document XML pour l’échange entier hello. Suspendre l’ensemble de l’échange hello lors de la validation d’un ou plusieurs documents informatisés dans l’échange de hello échouent. |

## <a name="configure-how-your-agreement-sends-messages"></a>Configuration de l’envoi des messages

Vous pouvez configurer comment cet accord identifie et gère les messages sortants que vous envoyez des partenaires tooyour via ce contrat.

1.  Sous **Ajouter**, sélectionnez **Paramètres d’envoi**.
Configurez ces propriétés selon le contrat conclu avec le partenaire qui échange des messages avec vous. Pour obtenir des descriptions de propriété, consultez les tableaux de hello dans cette section.

    L’option **Paramètres d’envoi** est organisée en plusieurs sections : identificateurs, accusé de réception, schémas, enveloppes, jeux de caractères et séparateurs, numéros de contrôle et validations.

    ![Configurer « Paramètres d’envoi »](./media/logic-apps-enterprise-integration-edifact/edifact-3.png)    

2. Une fois que vous avez terminé, assurez-vous que toosave vos paramètres en choisissant **OK**.

Votre accord est à présent prêt toohandle les messages qui se conforment tooyour sélectionné Paramètres sortants.

### <a name="identifiers"></a>Identificateurs

| Propriété | Description |
| --- | --- |
| UNB1.2 (version de la syntaxe) |Sélectionnez une valeur comprise entre **1** et **4**. |
| UNB2.3 (adresse de routage inverse de l’expéditeur) |Entrez une valeur numérique comprenant entre un et 14 caractères. |
| UNB3.3 (adresse de routage inverse du destinataire) |Entrez une valeur numérique comprenant entre un et 14 caractères. |
| UNB6.1 (mot de passe de référence du destinataire) |Entrez une valeur numérique comprenant entre un et 14 caractères. |
| UNB6.2 (qualificateur de référence du destinataire) |Entrez une valeur numérique contenant deux caractères maximum. |
| UNB7 (identifiant de référence de l’application) |Entrez une valeur numérique comprenant entre un et 14 caractères |

### <a name="acknowledgment"></a>Accusé de réception
| Propriété | Description |
| --- | --- |
| Réception des messages (CONTRL) |Sélectionnez cette case à cocher si le partenaire de hello hébergé s’attend un accusé de réception (CONTRL) technique de tooreceive. Ce paramètre spécifie le partenaire hébergé de hello, qui envoie le message de type hello, demande un accusé de réception à hello invité partenaire. |
| Accusé de réception (CONTRL) |Activez cette case à cocher si les partenaires hello hébergé s’attend à tooreceive un accusé de réception (CONTRL) fonctionnel. Ce paramètre spécifie le partenaire hébergé de hello, qui envoie le message de type hello, demande un accusé de réception à hello invité partenaire. |
| Générer une boucle SG1/SG4 pour les documents informatisés acceptés |Si vous avez choisi toorequest un accusé de réception fonctionnel, activez cette case à cocher tooforce la génération de boucles SG1/SG4 dans les accusés de réception CONTRL fonctionnels pour les documents informatisés acceptés. |

### <a name="schemas"></a>Schémas
| Propriété | Description |
| --- | --- |
| UNH2.1 (TYPE) |Sélectionnez un type de document informatisé. |
| UNH2.2 (VERSION) |Entrez le numéro de version de message hello. |
| UNH2.3 (VERSION FINALE) |Entrez le numéro de version du message hello. |
| Schéma |Sélectionnez toouse de schéma hello. Les schémas se trouvent dans votre compte d’intégration. tooaccess vos schémas, d’abord lier votre application de la logique de l’intégration compte tooyour. |

### <a name="envelopes"></a>Enveloppes
| Propriété | Description |
| --- | --- |
| UNB8 (code de priorité de traitement) |Entrez une valeur alphabétique ne contenant pas plus d’un caractère. |
| UNB10 (contrat de communication) |Entrez une valeur numérique comprenant entre un et 40 caractères. |
| UNB11 (indicateur de test) |Sélectionnez tooindicate cette case à cocher qui hello échange généré des données de test |
| Appliquer le segment UNA (conseil de service de chaîne) |Sélectionnez cette case à cocher de toogenerate un segment UNA pour hello échange toobe est envoyé. |
| Appliquer des segments UNG (En-tête de groupe fonctionnel) |Sélectionnez cette toocreate de case à cocher groupes de segments dans l’en-tête de groupe fonctionnel hello hello messages envoyés toohello invité partenaire. Hello valeurs suivantes sont les segments UNG hello toocreate utilisé : <p>Pour **UNG1**, entrez une valeur alphanumérique comportant un caractère minimum et six caractères maximum. <p>Pour **UNG2.1**, entrez une valeur alphanumérique comportant un caractère minimum et 35 caractères maximum. <p>Pour **UNG2.2**, entrez une valeur alphanumérique comprenant quatre caractères maximum. <p>Pour **UNG3.1**, entrez une valeur alphanumérique comportant un caractère minimum et 35 caractères maximum. <p>Pour **UNG3.2**, entrez une valeur alphanumérique comprenant quatre caractères maximum. <p>Pour **UNG6**, entrez une valeur alphanumérique comportant un caractère minimum et trois caractères maximum. <p>Pour **UNG7.1**, entrez une valeur alphanumérique comportant un caractère minimum et trois caractères maximum. <p>Pour **UNG7.2**, entrez une valeur alphanumérique comportant un caractère minimum et trois caractères maximum. <p>Pour **UNG7.3**, entrez une valeur alphanumérique comportant un caractère minimum et six caractères maximum. <p>Pour **UNG8**, entrez une valeur alphanumérique comportant un caractère minimum et 14 caractères maximum. |

### <a name="character-sets-and-separators"></a>Jeux de caractères et séparateurs

Autres que le jeu de caractères de hello, vous pouvez entrer un autre ensemble de toobe de délimiteurs utilisé pour chaque type de message. Si un jeu de caractères n’est pas spécifié pour un schéma de message donné, jeu de caractères par défaut hello est utilisé.

| Propriété | Description |
| --- | --- |
| UNB1.1 (identificateur système) |Sélectionnez hello de caractères EDIFACT défini toobe appliqué sur hello échange sortant. |
| Schéma |Sélectionnez un schéma à partir de la liste déroulante de hello. Une nouvelle ligne est automatiquement ajoutée lorsque la ligne précédente est terminée. Pour le schéma sélectionné de hello, les séparateurs hello sélectionnez définir que vous souhaitez toouse, en fonction de hello après les descriptions de séparateur. |
| Type d’entrée |Sélectionnez un type d’entrée à partir de la liste déroulante de hello. |
| Séparateur de composants |éléments de données composites tooseparate, entrez un caractère unique. |
| Séparateur d'éléments de données |tooseparate des éléments de données simples au sein d’éléments de données composites, entrez un caractère unique. |
| Terminateur de segment |fin de hello tooindicate d’un segment EDI, entrez un caractère unique. |
| Suffixe |Sélectionnez le caractère hello qui est utilisé avec l’identificateur de segment hello. Si vous désignez un suffixe, hello d’élément de données terminateur de segment peut être vide. Si le terminateur de segment hello est laissé vide, vous devez désigner un suffixe. |

### <a name="control-numbers"></a>Numéros de contrôle
| Propriété | Description |
| --- | --- |
| UNB5 (Numéro de contrôle de l’échange) |Entrez un préfixe, une plage de valeurs pour le numéro de contrôle d’échange hello et un suffixe. Ces valeurs sont utilisée toogenerate un échange sortant. préfixe de hello et suffixe sont facultatifs, alors que le numéro de contrôle hello est requis. numéro de contrôle Hello est incrémenté pour chaque nouveau message ; Hello préfixe et le suffixe restent hello même. |
| UNG5 (Numéro de contrôle de groupe) |Entrez un préfixe, une plage de valeurs pour le numéro de contrôle d’échange hello et un suffixe. Ces valeurs sont utilisées numéro de contrôle du groupe toogenerate hello. préfixe de hello et suffixe sont facultatifs, alors que le numéro de contrôle hello est requis. numéro de contrôle Hello est incrémenté pour chaque nouveau message jusqu'à ce que la valeur maximale de hello est atteinte ; Hello préfixe et le suffixe restent hello même. |
| UNH1 (Numéro de référence de l’en-tête de message) |Entrez un préfixe, une plage de valeurs pour le numéro de contrôle d’échange hello et un suffixe. Ces valeurs sont utilisées numéro de référence de l’en-tête de toogenerate hello message. préfixe de hello et suffixe sont facultatifs, alors que le numéro de référence hello est requis. numéro de référence Hello est incrémenté pour chaque nouveau message ; Hello préfixe et le suffixe restent hello même. |

### <a name="validations"></a>Validations

Une nouvelle ligne de validation est automatiquement ajoutée dès que la ligne précédente est terminée. Si vous ne spécifiez pas de règles, la validation utilise ligne « Par défaut » de hello.

| Propriété | Description |
| --- | --- |
| Type de message |Sélectionnez le type de message EDI hello. |
| Validation EDI |Effectuer une validation EDI sur les types de données définis par les propriétés EDI de hello du schéma de hello, les restrictions de longueur, les éléments de données vides et les séparateurs de fin. |
| Validation étendue |Si le type de données hello n’est pas EDI, la validation est sur la condition de l’élément données hello et autorisé de répétition, les énumérations et les données élément validation de la longueur (min/max). |
| Autoriser les zéros de début ou de fin |Conservez les zéros de début ou de fin ainsi que les caractères d’espace supplémentaires. Ne supprimez pas ces caractères. |
| Supprimer les zéros de début ou de fin |Supprimez les zéros de début ou de fin. |
| Stratégie de séparateur de fin |Générez des séparateurs de fin. <p>Sélectionnez **interdit** tooprohibit des délimiteurs et séparateurs Bonjour envoyé l’échange. Si l’échange de hello a des délimiteurs et séparateurs, échange de hello est déclaré non valide. <p>Sélectionnez **facultatif** toosend des échanges avec ou sans délimiteurs et séparateurs. <p>Sélectionnez **obligatoire** si l’échange de hello envoyé doit avoir des délimiteurs et séparateurs. |

## <a name="find-your-created-agreement"></a>Comment retrouver le contrat que vous avez créé

1.  Une fois que vous terminez la définition de toutes les propriétés de votre accord, sur hello **ajouter** panneau, choisissez **OK** toofinish créer votre accord et le panneau de compte d’intégration tooyour retour.

    Le contrat que vous venez d’ajouter s’affiche dans votre liste **Contrats**.

2.  Vous pouvez également afficher vos contrats dans la vue d’ensemble de votre compte d’intégration. Dans le panneau de compte integration, choisissez **vue d’ensemble**, puis sélectionnez hello **accords** vignette. 

    ![Choisissez « Accord » vignette tooview tous les contrats](./media/logic-apps-enterprise-integration-edifact/edifact-4.png)   

## <a name="view-swagger-file"></a>Afficher le fichier Swagger
Détails de Swagger tooview hello pour le connecteur d’EDIFACT hello, consultez [EDIFACT](/connectors/edifact/).

## <a name="learn-more"></a>En savoir plus
* [En savoir plus sur hello Pack d’intégration Enterprise](logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration Enterprise")  

