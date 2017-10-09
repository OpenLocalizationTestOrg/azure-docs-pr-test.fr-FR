---
title: "aaaConnect tooDynamics 365 (en ligne) à partir d’Azure Logic Apps | Documents Microsoft"
description: "Créer des workflows d’application qui gèrent des entités (en ligne) de Dynamics 365 via hello API fournie par le connecteur de hello Dynamics 365 logique"
services: logic-apps
cloud: Azure Stack
author: Mattp123
manager: anneta
documentationcenter: 
tags: connectors
ms.assetid: 0dc2abef-7d2c-4a2d-87ca-fad21367d135
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: matp; LADocs
ms.openlocfilehash: 183d7a6b8e5d2c0eecc70da0da3806e06c382df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toodynamics-365-from-logic-app-workflows"></a>Se connecter tooDynamics 365 à partir de flux de travail logique application

Avec les applications de la logique, vous pouvez connecter tooDynamics 365 (en ligne) et créer des flux métier qui créent des enregistrements, mettre à jour des éléments ou retournent une liste d’enregistrements. Avec le connecteur de hello Dynamics 365, vous pouvez :

* Générer des flux de votre entreprise en fonction des données hello que vous obtenez à partir de Dynamics 365 (en ligne).
* Utiliser des actions qui obtient une réponse, puis rendez sortie de hello disponible pour d’autres actions. Par exemple, quand un élément est mis à jour dans Dynamics 365 (Online), vous pouvez envoyer un courrier électronique à l’aide d’Office 365.

Cette rubrique vous montre comment une application de la logique de toocreate qui crée une tâche dans Dynamics 365 chaque fois qu’un nouveau prospect est créé dans Dynamics 365.

## <a name="prerequisites"></a>Composants requis
* Un compte Azure.
* Un compte Dynamics 365 (Online).

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a>Créer une tâche lorsqu’un prospect est créé dans Dynamics 365

1.  [Connectez-vous à tooAzure](https://portal.azure.com).

2.  Dans la zone de recherche Azure hello, tapez `Logic apps`, puis appuyez sur ENTRÉE.

      ![Rechercher Logic Apps](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  Sous **Logic Apps**, cliquez sur **Ajouter**.

      ![LogicApp - Ajouter](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  application de la logique toocreate hello, hello complète **nom**, **abonnement**, **groupe de ressources**, et **emplacement** champs, puis cliquez sur  **Créer**.

5.  Sélectionnez Application logique de la nouvelle hello. Lorsque vous recevez hello **déploiement a réussi** notification, cliquez sur **Actualiser**.

6.  Sous **Outils de développement**, cliquez sur **Concepteur d’application logique**. Dans la liste des modèles hello, cliquez sur **application logique vide**.

7.  Dans la zone de recherche de hello, tapez `Dynamics 365`. À partir de hello Dynamics 365 déclenche la liste, sélectionnez **Dynamics 365 – lors de la création d’un enregistrement**.

8.  Si vous êtes invité à toosign dans tooDynamics 365, faites-le maintenant.

9.  Dans Détails du déclencheur hello, entrez hello informations suivantes :

  * **Nom de l’organisation**. Sélectionnez instance Dynamics 365 hello hello logique application toolisten à souhaitées.

  * **Nom de l’entité**. Sélectionnez hello entité toolisten à. Cet événement agit comme une application de la logique de déclencheur toostart hello. 
  Dans cette procédure pas à pas, **Prospects** est sélectionné.

  * **La fréquence à laquelle vous souhaitez toocheck pour les éléments ?** Ces valeurs de définir la fréquence à laquelle hello logique application vérifie déclencheur toohello connexes de mises à jour. par défaut Hello est toocheck des mises à jour toutes les trois minutes.

    * **Fréquence**. Sélectionnez les secondes, les minutes, les heures ou les jours.

    * **Intervalle**. Entrez un nombre hello de secondes, minutes, heures ou jours que vous souhaitez toopass avant la prochaine vérification de hello.

      ![Application logique - Détails sur le déclencheur](./media/connectors-create-api-crmonline/trigger-details.png)

10. Cliquez sur **Nouvelle étape**, puis sur **Ajouter une action**.

11. Dans la zone de recherche de hello, tapez `Dynamics 365`. Dans la liste d’actions hello, sélectionnez **Dynamics 365 – créer un nouvel enregistrement**.

12. Entrez hello informations suivantes :

    * **Nom de l’organisation**. Sélectionnez l’instance hello Dynamics 365 où vous souhaitez l’enregistrement de hello flux toocreate hello. 
    Notez que cette instance n’a toobe hello même instance où les événements de hello est déclenchée à partir de.

    * **Nom de l’entité**. Sélectionnez hello entité que toocreate un enregistrement lorsque hello est déclenché. 
    Dans cette procédure pas à pas, **Tâches** est sélectionné.

13. Cliquez sur Bonjour **sujet** zone qui s’affiche. À partir de hello dynamique contenu liste qui s’affiche, vous pouvez sélectionner un de ces champs :

    * **Nom**. Ce champ insère hello nom hello prospect champ d’objet hello pour la tâche hello, lors de l’enregistrement de tâche hello est créé.
    * **Rubrique**. La sélection de ce champ insertions hello rubrique prospect hello dans le champ d’objet hello pour la tâche hello lorsque hello tâche enregistrement est créé. 
    Cliquez sur **rubrique** tooadd que toohello **sujet** boîte.

      ![Application logique - Détails Créer un enregistrement](./media/connectors-create-api-crmonline/create-record-details.png)

14. Dans la barre d’outils du Concepteur de la logique d’application hello, cliquez sur **enregistrer**.

    ![Barre d’outils du Concepteur d’application logique - Enregistrer](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. toostart hello logique d’application, cliquez sur **exécuter**.

    ![Barre d’outils du Concepteur d’application logique - Enregistrer](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. Créez maintenant un enregistrement de prospect dans Dynamics 365 pour les ventes et observez votre flux en action !

## <a name="set-advanced-options-for-a-logic-app-step"></a>Définir les options avancées d’une étape d’application logique

toospecify comment toofilter les données dans une étape d’application logique, cliquez sur **Show advanced options** dans cette étape, puis ajoutez un filtre ou une commande par requête.

Par exemple, vous pouvez utiliser un filtre requête tooget uniquement les comptes actifs et trier par nom de compte hello. tooperform cette tâche, entrez la requête de filtre OData hello `statuscode eq 1`, puis sélectionnez **nom de compte** à partir de la liste de contenu dynamique hello. Plus d’informations : [MSDN : $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) et [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).

![Application logique - Options avancées](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a>Meilleures pratiques lors de l’utilisation des options avancées

Lorsque vous ajoutez un champ de valeur de tooa, vous devez correspondre au type de champ hello si vous tapez une valeur ou sélectionnez une valeur dans la liste de contenu dynamique hello.

Type de champ  |Comment toouse  |Où toofind  |Nom  |Type de données  
---------|---------|---------|---------|---------
Champs de texte|Les champs de texte nécessitent une seule ligne de texte ou du contenu dynamique qui est un champ de type texte. Champs de catégorie et sous-catégorie hello sont des exemples.|Paramètres > personnalisations > Personnaliser hello système > entités > tâches > champs |category |Ligne de texte unique        
Champs de type entier | Certains champs nécessitent un entier ou un contenu dynamique qui est un champ de type entier. Exemples : Pourcentage achevé et Durée. |Paramètres > personnalisations > Personnaliser hello système > entités > tâches > champs |percentcomplete |Nombre entier         
Champs de date | Certains champs nécessitent qu’une date soit saisie au format mm/jj/aaaa ou un contenu dynamique qui est un champ de type date. Exemples : Créé le, Date de début, Début réel, Dernière durée de suspension, Fin réelle et Date d’échéance. | Paramètres > personnalisations > Personnaliser hello système > entités > tâches > champs |createdon |Date et heure
Champs qui nécessitent à la fois un ID d’enregistrement et un type de recherche |Certains champs qui font référence à un autre enregistrement d’entité nécessitent l’ID d’enregistrement hello et type de recherche hello. |Paramètres > personnalisations > Personnaliser hello système > entités > compte > champs  | accountid  | Clé primaire

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a>Exemples de champs supplémentaires nécessitant un ID d’enregistrement et un type de recherche
Développement sur le tableau précédent de hello, Voici plusieurs exemples de champs qui ne fonctionnent pas avec les valeurs sélectionnées à partir de la liste de contenu dynamique hello. Au lieu de cela, ces champs nécessitent les deux ID et recherche de type d’enregistrement entré dans les champs de hello dans PowerApps.  
* Propriétaire et Type de propriétaire. champ de Hello propriétaire doit être un ID d’enregistrement utilisateur ou de l’équipe valide Hello Type propriétaire doit être **systemusers** ou **équipes**.
* Client et Type de client. champ de Hello client doit être un compte valide ou ID de l’enregistrement de contact. Hello Type propriétaire doit être **comptes** ou **contacts**.
* Concernant et Type Concernant. Hello concernant le champ doit être un ID d’enregistrement valide, tel qu’un compte ou ID de l’enregistrement de contact. Hello en ce qui concerne le Type doit être le type de recherche hello pour l’enregistrement de hello, tel que **comptes** ou **contacts**.

Hello exemple action de création de tâche suivant ajoute un enregistrement de compte correspondant ID d’enregistrement toohello ajoutant toohello concernant le champ de la tâche hello.

![Flux : ID d’enregistrement et type de compte](./media/connectors-create-api-crmonline/recordid-type-account.png)

Cet exemple affecte également hello tooa spécifique utilisateur de la tâche en fonction de l’ID d’enregistrement. de l’utilisateur hello

![Flux : ID d’enregistrement et type de compte](./media/connectors-create-api-crmonline/recordid-type-user.png)

toofind un enregistrement de l’ID, consultez hello suivant la section : *rechercher l’ID d’enregistrement hello*

## <a name="find-hello-record-id"></a>Rechercher l’ID d’enregistrement hello

1. Ouvrez un enregistrement, comme un enregistrement de compte.

2. Dans la barre d’outils de hello actions, cliquez sur **sortir** ![enregistrement de la fenêtre indépendante](./media/connectors-create-api-crmonline/popout-record.png).
Vous pouvez également hello actions la barre d’outils toocopy hello une URL complète dans votre programme de messagerie par défaut, cliquez sur **par courrier électronique un lien**.

   ID d’enregistrement Hello est affichée entre hello % 7 b et %7 d’encodage des caractères de l’URL de hello.

   ![Flux : ID d’enregistrement et type de compte](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a>Résolution des problèmes
tootroubleshoot Échec d’une étape dans une application logique, afficher les détails de statut hello d’événement de hello.

1. Dans la zone **Logic Apps**, sélectionnez votre application logique, puis cliquez sur **Vue d’ensemble**. 

   Hello zone de récapitulatif est affiché et fournit l’état de hello exécuter pour l’application de la logique de hello. 

   ![État d’exécution de l’application logique](./media/connectors-create-api-crmonline/tshoot1.png)

2. tooview plus d’informations sur toutes les séries ayant échouées, cliquez sur hello Échec de l’événement. tooexpand Échec d’une étape, cliquez sur cette étape.

   ![Développer l’étape qui a échoué](./media/connectors-create-api-crmonline/tshoot2.png)

   Détails de l’étape Hello apparaissent et peuvent aider à résoudre la cause hello de défaillance de hello.

   ![Détails de l’étape qui a échoué](./media/connectors-create-api-crmonline/tshoot3.png)

Pour plus d’informations sur la résolution des problèmes relatifs aux applications logiques, consultez [Diagnostic des échecs d’applications logiques](../logic-apps/logic-apps-diagnosing-failures.md).

## <a name="connector-specific-details"></a>Détails spécifiques du connecteur

Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/crm/). 

## <a name="next-steps"></a>Étapes suivantes
Explorer hello tous les autres connecteurs disponibles dans les applications logique à notre [liste des API](apis-list.md).
