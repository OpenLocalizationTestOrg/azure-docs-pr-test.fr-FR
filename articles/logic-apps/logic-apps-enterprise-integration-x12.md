---
title: "messages aaaX12 pour l’intégration d’entreprise B2B - Azure Logic Apps | Documents Microsoft"
description: "Échangez des messages X12 au format EDI dans le cadre d’une intégration d’entreprise B2B avec Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 7422d2d5-b1c7-4a11-8c9b-0d8cfa463164
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 20a077b299875a16ada66a500d5f1c8f9972d309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-x12-messages-for-enterprise-integration-with-logic-apps"></a>Échangez des messages X12 dans le cadre d’une intégration d’entreprise avec Logic Apps

Avant de pouvoir échanger des messages X12 pour Azure Logic Apps, vous devez créer un contrat X12 et le stocker dans votre compte d’intégration. Voici la procédure hello pour la toocreate un X12 accord.

> [!NOTE]
> Cette page traite des fonctionnalités de hello X12 pour Azure Logic Apps. Pour plus d’informations, consultez [EDIFACT](logic-apps-enterprise-integration-edifact.md).

## <a name="before-you-start"></a>Avant de commencer

Voici les éléments hello que vous devez :

* Un [compte d’intégration](../logic-apps/logic-apps-enterprise-integration-accounts.md) déjà défini et associé à votre abonnement Azure
* Au moins deux [partenaires](../logic-apps/logic-apps-enterprise-integration-partners.md) qui sont définis dans votre compte d’intégration et configurés avec l’identificateur hello X12 sous **des identités d’entreprise**    
* Une valeur obligatoire [schéma](../logic-apps/logic-apps-enterprise-integration-schemas.md) pour le téléchargement tooyour [compte d’intégration](../logic-apps/logic-apps-enterprise-integration-accounts.md)

Après avoir [créer un compte d’intégration](../logic-apps/logic-apps-enterprise-integration-accounts.md), [ajouter des partenaires](logic-apps-enterprise-integration-partners.md)et avoir un [schéma](../logic-apps/logic-apps-enterprise-integration-schemas.md) que vous souhaitez toouse, vous pouvez créer un X12 accord en suivant ces étapes.

## <a name="create-an-x12-agreement"></a>Créer un contrat X12

1.  Connectez-vous à toohello [portail Azure](http://portal.azure.com "portail Azure"). Dans le menu de gauche hello, sélectionnez **davantage de services**. 

    > [!TIP]
    > Si vous ne voyez pas **davantage de services**, vous pouvez avoir des menus de hello tooexpand tout d’abord. Haut hello du menu de hello réduit, sélectionnez **menu Afficher**.

    ![Dans le menu de gauche, cliquez sur « Plus de services »](./media/logic-apps-enterprise-integration-x12/account-1.png)

2.  Dans la zone de recherche de hello, tapez « intégration » comme filtre. Dans la liste des résultats hello, sélectionnez **comptes d’intégration**.  

    ![Filtrer sur « intégration », sélectionner « Comptes d’intégration »](./media/logic-apps-enterprise-integration-x12/account-2.png)

3. Bonjour **comptes d’intégration** panneau qui s’ouvre, le compte d’intégration hello sélectionnez où vous souhaitez l’accord de hello tooadd.
Si aucun compte d’intégration ne s’affiche, [créez-en un](../logic-apps/logic-apps-enterprise-integration-accounts.md "Tout sur les comptes d’intégration").

    ![Sélectionnez le compte de l’intégration où toocreate hello accord](./media/logic-apps-enterprise-integration-x12/account-3.png)

4. Sélectionnez **vue d’ensemble**, puis sélectionnez hello **accords** vignette. Si vous n’avez pas une vignette de contrats, ajoutez d’abord les mosaïques hello. 

    ![Choisissez la mosaïque « Contrats »](./media/logic-apps-enterprise-integration-agreements/agreement-1.png)

5. Dans le panneau des accords hello qui s’ouvre, choisissez **ajouter**.

    ![Choisir « Ajouter »](./media/logic-apps-enterprise-integration-agreements/agreement-2.png)     

6. Sous **Ajouter**, entrez le **nom** de votre contrat. Pour le type de contrat hello, sélectionnez **X12**. Sélectionnez hello **partenaire hôte**, **identité de l’hôte**, **partenaire invité**, et **invité identité** pour votre accord. Pour plus d’informations de propriété, consultez le tableau de hello dans cette étape.

    ![Renseigner les détails relatifs au contrat](./media/logic-apps-enterprise-integration-x12/x12-1.png)  

    | Propriété | Description |
    | --- | --- |
    | Nom |Nom de contrat de hello |
    | Type de contrat | Doit être X12. |
    | Partenaire hôte |Un contrat nécessite un partenaire hôte et un partenaire invité. partenaire d’accueil Hello représente l’organisation hello qui configure l’accord de hello. |
    | Identité de l’hôte |Un identificateur pour le partenaire d’accueil hello |
    | Partenaire invité |Un contrat nécessite un partenaire hôte et un partenaire invité. partenaire invité de Hello représente l’organisation hello qui effectue l’entreprise avec le partenaire d’accueil hello. |
    | identité de l’invité |Un identificateur de partenaire invité de hello |
    | Paramètres de réception |Ces propriétés s’appliquent tooall les messages reçus par un accord. |
    | Paramètres d’envoi |Ces propriétés s’appliquent tooall les messages envoyés par un accord. |  

  > [!NOTE]
  > Résolution de X12 contrat dépend de la mise en correspondance hello qualificateur et identificateur et qualificateur du récepteur hello et expéditeur identificateur défini dans le partenaire de hello et le message entrant. Si ces valeurs changent pour votre partenaire, mettre à jour la hello accord trop.

## <a name="configure-how-your-agreement-handles-received-messages"></a>Configuration du traitement des messages reçus

Maintenant que vous avez défini les propriétés de l’accord hello, vous pouvez configurer comment cet accord identifie et traite les messages entrants reçus à partir de votre partenaire via ce contrat.

1.  Sous **Ajouter**, sélectionnez **Paramètres de réception**.
Configurez ces propriétés en fonction de votre accord avec le partenaire hello qui échange des messages avec vous. Pour obtenir des descriptions de propriété, consultez les tableaux de hello dans cette section.

    L’option **Paramètres de réception** est organisée en plusieurs sections : identificateurs, accusé de réception, schémas, enveloppes, numéros de contrôle, validations et paramètres internes.

2. Une fois que vous avez terminé, assurez-vous que toosave vos paramètres en choisissant **OK**.

À présent, votre contrat toohandle prêt entrante messages conformes tooyour les paramètres sélectionnés.

### <a name="identifiers"></a>Identificateurs

![Définir les propriétés de l’identificateur](./media/logic-apps-enterprise-integration-x12/x12-2.png)  

| Propriété | Description |
| --- | --- |
| ISA1 (qualificateur d’autorisation) |Sélectionnez la valeur du qualificateur d’autorisation hello à partir de la liste déroulante de hello. |
| ISA2 |facultatif. Entrez la valeur d’autorisation. Si la valeur hello entrée pour ISA1 est autre que 00, entrez un caractère alphanumérique au minimum et un maximum de 10. |
| ISA3 (qualificateur de sécurité) |Sélectionnez la valeur du qualificateur hello sécurité à partir de la liste déroulante de hello. |
| ISA4 |facultatif. Entrez la valeur des informations de sécurité hello. Si la valeur hello entrée pour ISA3 est autre que 00, entrez un caractère alphanumérique au minimum et un maximum de 10. |

### <a name="acknowledgment"></a>Accusé de réception

![Définir les propriétés de l’accusé de réception](./media/logic-apps-enterprise-integration-x12/x12-3.png) 

| Propriété | Description |
| --- | --- |
| TA1 attendu |Retourne un expéditeur des échanges toohello accusé de réception technique |
| FA attendu |Retourne un expéditeur des échanges toohello accusé de réception fonctionnel. Puis sélectionnez si vous souhaitez que les accusés de réception hello 997 ou 999, basée sur la version du schéma hello |
| Inclure une boucle AK2/IK2 |Permet la génération de boucles AK2 dans les accusés de réception fonctionnels des documents informatisés acceptés. |

### <a name="schemas"></a>Schémas

Sélectionnez un schéma pour chaque type de transaction (ST1) et application de l’expéditeur (GS2). réception de Hello pipeline désassemble le message entrant de hello en mettant en correspondance les valeurs hello pour ST1 et de GS2 dans le message entrant de hello avec hello les valeurs définies ici et le schéma hello de message entrant de hello avec schéma hello vous définissez ici.

![Sélectionner un schéma](./media/logic-apps-enterprise-integration-x12/x12-33.png) 

| Propriété | Description |
| --- | --- |
| Version |Sélectionnez la version de hello X12 |
| Type de transaction (ST01) |Sélectionnez le type de transaction hello |
| Application de l’expéditeur (GS02) |Sélectionnez l’application d’expédition hello |
| Schéma |Sélectionnez le fichier de schéma de hello souhaité toouse. Les schémas sont ajoutés tooyour compte d’intégration. |

> [!NOTE]
> Configurer hello requis [schéma](../logic-apps/logic-apps-enterprise-integration-schemas.md) qui est téléchargé tooyour [compte d’intégration](../logic-apps/logic-apps-enterprise-integration-accounts.md).

### <a name="envelopes"></a>Enveloppes

![Spécifiez le séparateur de hello dans un document informatisé : choisissez identificateur Standard ou le séparateur de répétition](./media/logic-apps-enterprise-integration-x12/x12-34.png)

| Propriété | Description |
| --- | --- |
| Utilisation d’ISA11 |Spécifie les hello séparateur toouse dans un document informatisé : <p>Sélectionnez **identificateur Standard** toouse un point (.) pour la notation décimale, plutôt que de notation décimale du document entrant de hello Bonjour EDI hello le pipeline de réception. <p>Sélectionnez **séparateur de répétition** séparateur de hello toospecify aux occurrences répétées d’un élément de données simple ou d’une structure de données répétées. Par exemple, généralement hello accent circonflexe (^) est utilisé comme séparateur de répétition hello. Pour les schémas HIPAA, vous pouvez uniquement utiliser accent circonflexe de hello. |

### <a name="control-numbers"></a>Numéros de contrôle

![Sélectionnez comment toohandle contrôler le nombre de doublons](./media/logic-apps-enterprise-integration-x12/x12-35.png) 

| Propriété | Description |
| --- | --- |
| Interdire les doublons de numéro de contrôle d’échange |Bloquer les échanges en double. Vérifie hello numéro de contrôle (ISA13) numéro de contrôle d’échange hello reçu. Si une correspondance est détectée, hello affiche pipeline n’est pas traité l’échange de hello. Vous pouvez spécifier le nombre de hello de jours pour la vérification de hello en affectant une valeur *chercher isa13 en double tous les (jours)*. |
| Interdire les numéros de contrôle de groupe en double |Bloquer les échanges avec des numéros de contrôle de groupe en double. |
| Interdire les numéros de contrôle de document informatisé en double |Bloquer les échanges avec des numéros de contrôle de document informatisé en double. |

### <a name="validations"></a>Validations

![Définir les propriétés de validation pour les messages reçus](./media/logic-apps-enterprise-integration-x12/x12-36.png) 

Une nouvelle ligne de validation est automatiquement ajoutée dès que la ligne précédente est terminée. Si vous ne spécifiez pas de règles, la validation utilise ligne « Par défaut » de hello.

| Propriété | Description |
| --- | --- |
| Type de message |Sélectionnez le type de message EDI hello. |
| Validation EDI |Effectuer une validation EDI sur les types de données, tel que défini par du schéma hello EDI propriétés, les restrictions de longueur, éléments de données vides et les séparateurs de fin. |
| Validation étendue |Si le type de données hello n’est pas EDI, la validation est sur la condition de l’élément données hello et autorisé de répétition, les énumérations et les données élément validation de la longueur (min/max). |
| Autoriser les zéros de début ou de fin |Conservez les zéros de début ou de fin ainsi que les caractères d’espace supplémentaires. Ne supprimez pas ces caractères. |
| Supprimer les zéros de début ou de fin |Supprimez les zéros de début ou de fin ainsi que les caractères d’espace. |
| Stratégie de séparateur de fin |Générez des séparateurs de fin. <p>Sélectionnez **interdit** tooprohibit des délimiteurs et séparateurs Bonjour reçu l’échange. Si l’échange de hello a des délimiteurs et séparateurs, échange de hello est déclaré non valide. <p>Sélectionnez **facultatif** tooaccept des échanges avec ou sans délimiteurs et séparateurs. <p>Sélectionnez **obligatoire** lorsque les échanges hello doivent avoir des délimiteurs et séparateurs. |

### <a name="internal-settings"></a>Paramètres internes

![Sélectionnez les paramètres internes](./media/logic-apps-enterprise-integration-x12/x12-37.png) 

| Propriété | Description |
| --- | --- |
| Convertir le format décimal implicite « Nn » tooa base 10 valeur numérique |Convertit un numéro EDI spécifié au format hello « Nn » en valeur numérique de base 10 |
| Créer des balises XML vides si les séparateurs de fin sont autorisés |Sélectionnez cet expéditeur hello toohave case à cocher Inclure vide les balises XML pour les séparateurs de fin. |
| Scinder l’échange en documents informatisés : suspendre les documents informatisés en cas d’erreur|Analyse chaque document informatisé d’un échange en un document XML distinct en appliquant l’enveloppe appropriée toohello hello document informatisé. Interrompt uniquement les transactions hello Échec de la validation de hello. |
| Scinder l’échange en documents informatisés : suspendre l’échange en cas d’erreur|Analyse chaque document informatisé d’un échange en un document XML distinct en appliquant l’enveloppe appropriée de hello. Suspend la totalité de l’échange lors de la validation d’un ou plusieurs documents informatisés dans l’échange de hello échouent. | 
| Préserver l'échange : suspendre les documents informatisés en cas d’erreur |Toucher l’échange de hello, crée un document XML pour l’échange entier hello. Suspend uniquement hello documents informatisés que la validation échouent, tout en continuant tooprocess tous les autres documents informatisés. |
| Préserver l’échange : suspendre l’échange en cas d’erreur |Toucher l’échange de hello, crée un document XML pour l’échange entier hello. Suspend l’ensemble de l’échange hello lors de la validation d’un ou plusieurs documents informatisés dans l’échange de hello échouent. |

## <a name="configure-how-your-agreement-sends-messages"></a>Configuration de l’envoi des messages

Vous pouvez configurer comment cet accord identifie et gère les messages sortants que vous envoyez partenaire tooyour via ce contrat.

1.  Sous **Ajouter**, sélectionnez **Paramètres d’envoi**.
Configurez ces propriétés selon le contrat conclu avec le partenaire qui échange des messages avec vous. Pour obtenir des descriptions de propriété, consultez les tableaux de hello dans cette section.

    L’option **Paramètres d’envoi** est organisée en plusieurs sections : identificateurs, accusé de réception, schémas, enveloppes, jeux de caractères et séparateurs, numéros de contrôle et validation.

2. Une fois que vous avez terminé, assurez-vous que toosave vos paramètres en choisissant **OK**.

Votre accord est à présent prêt toohandle les messages qui se conforment tooyour sélectionné Paramètres sortants.

### <a name="identifiers"></a>Identificateurs

![Définir les propriétés de l’identificateur](./media/logic-apps-enterprise-integration-x12/x12-4.png)  

| Propriété | Description |
| --- | --- |
| Qualificateur d’autorisation (ISA1) |Sélectionnez la valeur du qualificateur d’autorisation hello à partir de la liste déroulante de hello. |
| ISA2 |Entrez la valeur d’autorisation. Si cette valeur est autre que 00, entrez au moins un caractère alphanumérique (et 10 caractères maximum). |
| Qualificateur de sécurité (ISA3) |Sélectionnez la valeur du qualificateur hello sécurité à partir de la liste déroulante de hello. |
| ISA4 |Entrez la valeur des informations de sécurité hello. Si cette valeur est autre que 00, pour la zone de texte hello valeur (ISA4), puis entrez une valeur alphanumérique au minimum et un maximum de 10. |

### <a name="acknowledgment"></a>Accusé de réception

![Définir les propriétés de l’accusé de réception](./media/logic-apps-enterprise-integration-x12/x12-5.png)  

| Propriété | Description |
| --- | --- |
| TA1 attendu |Retourne un expéditeur des échanges toohello accusé de réception technique (TA1). Ce paramètre spécifie le partenaire hôte hello qui envoie les demandes de messages hello un accusé de réception du partenaire invité de hello dans l’accord de hello. Ces accusés de réception sont attendus par le partenaire d’accueil hello en fonction des paramètres de réception hello du contrat de hello. |
| FA attendu |Retourne un expéditeur des échanges toohello accusé de réception fonctionnel (FA). Indiquez si vous souhaitez hello 997 ou 999 les accusés de réception, en fonction des versions de schéma hello que vous travaillez. Ces accusés de réception sont attendus par le partenaire d’accueil hello en fonction des paramètres de réception hello du contrat de hello. |
| Version FA |Sélectionnez la version de hello FA |

### <a name="schemas"></a>Schémas

![Sélectionnez le schéma toouse](./media/logic-apps-enterprise-integration-x12/x12-5.png)  

| Propriété | Description |
| --- | --- |
| Version |Sélectionnez la version de hello X12 |
| Type de transaction (ST01) |Sélectionnez le type de transaction hello |
| Schéma |Sélectionnez toouse de schéma hello. Les schémas se trouvent dans votre compte d’intégration. Si vous sélectionnez schéma d’abord, il configure automatiquement la version et le type de transaction.  |

> [!NOTE]
> Configurer hello requis [schéma](../logic-apps/logic-apps-enterprise-integration-schemas.md) qui est téléchargé tooyour [compte d’intégration](../logic-apps/logic-apps-enterprise-integration-accounts.md).

### <a name="envelopes"></a>Enveloppes

![Spécifiez le séparateur de hello dans un document informatisé : choisissez identificateur Standard ou le séparateur de répétition](./media/logic-apps-enterprise-integration-x12/x12-6.png) 

| Propriété | Description |
| --- | --- |
| Utilisation d’ISA11 |Spécifie les hello séparateur toouse dans un document informatisé : <p>Sélectionnez **identificateur Standard** toouse un point (.) pour la notation décimale, plutôt que de notation décimale du document entrant de hello Bonjour EDI hello le pipeline de réception. <p>Sélectionnez **séparateur de répétition** séparateur de hello toospecify aux occurrences répétées d’un élément de données simple ou d’une structure de données répétées. Par exemple, généralement hello accent circonflexe (^) est utilisé comme séparateur de répétition hello. Pour les schémas HIPAA, vous pouvez uniquement utiliser accent circonflexe de hello. |

### <a name="control-numbers"></a>Numéros de contrôle

![Spécifier les propriétés de numéro de contrôle](./media/logic-apps-enterprise-integration-x12/x12-8.png) 

| Propriété | Description |
| --- | --- |
| Numéro de contrôle de version (ISA12) |Sélectionnez la version hello Hello X12 standard |
| Indicateur d’utilisation (ISA15) |Sélectionnez un contexte hello d’un échange.  Hello plus d’informations, les données de production, ou des valeurs de données de test |
| Schéma |Génère hello GS et ST des segments d’un échange encodé X12 qu’il envoie toohello Pipeline d’envoi |
| GS1 |Facultatif, sélectionnez une valeur pour le code fonctionnel hello à partir de la liste déroulante de hello |
| GS2 |Facultatif, expéditeur de l’application. |
| GS3 |Facultatif, destinataire de l’application. |
| GS4 |Facultatif, sélectionnez SSAAMMJJ ou AAMMJJ. |
| GS5 |Facultatif, sélectionnez HHMM, HHMMSS ou HHMMSSjj. |
| GS7 |Facultatif, sélectionnez une valeur pour l’entité responsable de hello à partir de la liste déroulante de hello |
| GS8 |Facultative, version du document de hello |
| Numéro de contrôle de l’échange (ISA13) |Obligatoire, d’entrer une plage de valeurs pour le numéro de contrôle d’échange hello. Entrez une valeur numérique comprise entre 1 et 999999999. |
| Numéro de contrôle de groupe (GS06) |Obligatoire, d’entrer une plage de numéros pour le numéro de contrôle de groupe hello. Entrez une valeur numérique comprise entre 1 et 999999999. |
| Numéro de contrôle de document informatisé (ST02) |Obligatoire, d’entrer une plage de numéros pour hello numéro de contrôle de Transaction défini. Entrez une plage de valeurs numériques comprises entre 1 et 999999999. |
| Préfixe |Facultatif, désigné pour la plage de numéros de contrôle de transaction utilisé dans l’accusé de réception de hello. Entrez une valeur numérique pour les deux champs du hello milieu et une valeur alphanumérique (le cas échéant) pour les champs préfixe et suffixe hello. champs du milieu Hello sont requis et contiennent hello valeurs minimale et maximale pour le numéro de contrôle hello |
| Suffixe |Facultatif, désigné pour la plage de numéros de contrôle de transaction utilisé dans un accusé de réception de hello. Entrez une valeur numérique pour les deux champs du hello milieu et une valeur alphanumérique (le cas échéant) pour les champs préfixe et suffixe hello. champs du milieu Hello sont requis et contiennent hello valeurs minimale et maximale pour le numéro de contrôle hello |

### <a name="character-sets-and-separators"></a>Jeux de caractères et séparateurs

Autres que le jeu de caractères de hello, vous pouvez entrer un ensemble de délimiteurs différent pour chaque type de message. Si un jeu de caractères n’est pas spécifié pour un schéma de message donné, jeu de caractères par défaut hello est utilisé.

![Spécifier des délimiteurs pour les types de messages](./media/logic-apps-enterprise-integration-x12/x12-9.png) 

| Propriété | Description |
| --- | --- |
| Toobe de jeu de caractères utilisé |propriétés de hello toovalidate, jeu de caractères hello sélectionnez X12. options de Hello sont Basic, Extended et UTF-8. |
| Schéma |Sélectionnez un schéma à partir de la liste déroulante de hello. Une nouvelle ligne est automatiquement ajoutée lorsque la ligne précédente est terminée. Pour le schéma sélectionné de hello, les séparateurs hello sélectionnez définir que vous souhaitez toouse, en fonction de hello après les descriptions de séparateur. |
| Type d’entrée |Sélectionnez un type d’entrée à partir de la liste déroulante de hello. |
| Séparateur de composants |éléments de données composites tooseparate, entrez un caractère unique. |
| Séparateur d'éléments de données |tooseparate des éléments de données simples au sein d’éléments de données composites, entrez un caractère unique. |
| Caractère de remplacement |Entrez un caractère de remplacement utilisé pour remplacer tous les caractères de séparation dans les données de charge hello lors de la génération du message de type hello X12 sortant. |
| Terminateur de segment |fin de hello tooindicate d’un segment EDI, entrez un caractère unique. |
| Suffixe |Sélectionnez le caractère hello qui est utilisé avec l’identificateur de segment hello. Si vous désignez un suffixe, hello d’élément de données terminateur de segment peut être vide. Si le terminateur de segment hello est laissé vide, vous devez désigner un suffixe. |

> [!TIP]
> tooprovide les valeurs de caractère spécial, modifier l’accord hello au format JSON et fournir de valeur ASCII de hello pour un caractère spécial hello.

### <a name="validation"></a>Validation

![Définir les propriétés de validation pour l’envoi de messages](./media/logic-apps-enterprise-integration-x12/x12-10.png) 

Une nouvelle ligne de validation est automatiquement ajoutée dès que la ligne précédente est terminée. Si vous ne spécifiez pas de règles, la validation utilise ligne « Par défaut » de hello.

| Propriété | Description |
| --- | --- |
| Type de message |Sélectionnez le type de message EDI hello. |
| Validation EDI |Effectuer une validation EDI sur les types de données, tel que défini par du schéma hello EDI propriétés, les restrictions de longueur, éléments de données vides et les séparateurs de fin. |
| Validation étendue |Si le type de données hello n’est pas EDI, la validation est sur la condition de l’élément données hello et autorisé de répétition, les énumérations et les données élément validation de la longueur (min/max). |
| Autoriser les zéros de début ou de fin |Conservez les zéros de début ou de fin ainsi que les caractères d’espace supplémentaires. Ne supprimez pas ces caractères. |
| Supprimer les zéros de début ou de fin |Supprimez les zéros de début ou de fin. |
| Stratégie de séparateur de fin |Générez des séparateurs de fin. <p>Sélectionnez **interdit** tooprohibit des délimiteurs et séparateurs Bonjour envoyé l’échange. Si l’échange de hello a des délimiteurs et séparateurs, échange de hello est déclaré non valide. <p>Sélectionnez **facultatif** toosend des échanges avec ou sans délimiteurs et séparateurs. <p>Sélectionnez **obligatoire** si l’échange de hello envoyé doit avoir des délimiteurs et séparateurs. |

## <a name="find-your-created-agreement"></a>Comment retrouver le contrat que vous avez créé

1.  Une fois que vous terminez la définition de toutes les propriétés de votre accord, sur hello **ajouter** panneau, choisissez **OK** toofinish créer votre accord et le panneau de compte d’intégration tooyour retour.

    Le contrat que vous venez d’ajouter s’affiche dans votre liste **Contrats**.

2.  Vous pouvez également afficher vos contrats dans la vue d’ensemble de votre compte d’intégration. Dans le panneau de compte integration, choisissez **vue d’ensemble**, puis sélectionnez hello **accords** vignette.

    ![Choisissez « Accord » vignette tooview tous les contrats](./media/logic-apps-enterprise-integration-x12/x12-1-5.png)   

## <a name="view-hello-swagger"></a>Swagger hello de vue
Consultez hello [swagger détails](/connectors/x12/). 

## <a name="learn-more"></a>En savoir plus
* [En savoir plus sur hello Pack d’intégration Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration Enterprise")  

