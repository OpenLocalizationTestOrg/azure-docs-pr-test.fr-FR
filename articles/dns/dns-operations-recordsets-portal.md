---
title: "aaaManage DNS enregistrer des jeux et les enregistrements avec le système DNS Azure | Documents Microsoft"
description: "DNS Azure fournit un enregistrement DNS toomanage hello fonctionnalité définit et enregistre lors de l’hébergement de votre domaine."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ed44a1-7bfe-454f-964e-922ad978264a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 2e62d017341589eaf8d1f8df2fe5db4b973381d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-record-sets-by-using-hello-azure-portal"></a>Gérer les enregistrements DNS et les jeux d’enregistrements à l’aide de hello portail Azure

> [!div class="op_single_selector"]
> * [portail Azure](dns-operations-recordsets-portal.md)
> * [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

Cet article vous explique comment toomanage jeux d’enregistrements et les enregistrements pour votre zone DNS à l’aide de hello portail Azure.

Il est important toounderstand hello différence jeux d’enregistrements DNS et des enregistrements DNS. Un jeu d’enregistrements est une collection d’enregistrements dans une zone possédant hello même nom et sont hello même type. Pour plus d’informations, consultez [jeux d’enregistrements DNS de créer et d’enregistrements à l’aide de portail Azure hello](dns-getstarted-create-recordset-portal.md).

## <a name="create-a-new-record-set-and-record"></a>Création d’un jeu d’enregistrements et d’un enregistrement

toocreate un ensemble d’enregistrements d’hello portail Azure, consultez [les enregistrements DNS de créer à l’aide de hello Azure portal](dns-getstarted-create-recordset-portal.md).

## <a name="view-a-record-set"></a>Affichage d’un jeu d’enregistrements

1. Bonjour portail Azure, accédez à toohello **zone DNS** panneau.
2. Recherchez le jeu d’enregistrements hello et sélectionnez-le. Propriétés du jeu d’enregistrements hello s’ouvre.

    ![Recherche d’un jeu d’enregistrements](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-tooa-record-set"></a>Ajouter un nouveau jeu d’enregistrements tooa enregistrement

Vous pouvez ajouter jusqu'à tooany jeu d’enregistrements too20 enregistrements. Un jeu d’enregistrements ne peut pas contenir deux enregistrements identiques. Jeux d’enregistrements vides (avec zéro enregistrements) peut être créés, mais n’apparaître pas sur les serveurs DNS de Azure hello. Les jeux d’enregistrements du type CNAME peuvent contenir un enregistrement au maximum.

1. Sur hello **propriétés du jeu d’enregistrements** panneau pour votre zone DNS, cliquez sur l’enregistrement hello défini que vous souhaitez tooadd un enregistrement.

    ![Sélection d’un jeu d'enregistrements](./media/dns-operations-recordsets-portal/selectset500.png)

2. Spécifiez les propriétés de jeu d’enregistrements de hello en renseignant les champs hello.

    ![Ajouter un enregistrement](./media/dns-operations-recordsets-portal/addrecord500.png)

3. Cliquez sur **enregistrer** à hello haut de hello panneau toosave vos paramètres. Puis fermez le panneau de hello.
4. Dans l’angle de hello, vous verrez que l’enregistrement de hello enregistre.

    ![Enregistrement d’un jeu d'enregistrements](./media/dns-operations-recordsets-portal/saving150.png)

Une fois l’enregistrement de hello a été enregistré, hello valeurs hello **zone DNS** panneau reflète le nouvel enregistrement de hello.

## <a name="update-a-record"></a>Mise à jour d’un enregistrement

Lorsque vous mettez à jour un enregistrement dans un jeu d’enregistrements existant, vous pouvez mettre à jour des champs de hello dépendent de type hello d’enregistrement avec lequel vous travaillez.

1. Sur hello **propriétés du jeu d’enregistrements** panneau pour votre jeu d’enregistrements, recherchez les enregistrements hello.
2. Modifier un enregistrement de hello. Lorsque vous modifiez un enregistrement, vous pouvez modifier les paramètres disponibles de hello pour l’enregistrement de hello. Dans l’exemple suivant de hello, hello **adresse IP** champ est sélectionné et l’adresse IP de hello est en cours de hello d’en cours de modification.

    ![Modification d’un enregistrement](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. Cliquez sur **enregistrer** à hello haut de hello panneau toosave vos paramètres. Dans le coin supérieur droit hello, vous verrez notification hello hello enregistrement a été enregistré.

    ![Ajout d’un jeu d’enregistrements](./media/dns-operations-recordsets-portal/saved150.png)

Une fois l’enregistrement de hello a été enregistré, les valeurs de hello pour l’enregistrement de hello définies sur hello **zone DNS** panneau reflètent les enregistrement hello mis à jour.

## <a name="remove-a-record-from-a-record-set"></a>Suppression d’un enregistrement d’un jeu d’enregistrements

Vous pouvez utiliser des enregistrements de tooremove portail Azure hello à partir d’un jeu d’enregistrements. Notez que la suppression du dernier enregistrement de hello à partir d’un jeu d’enregistrements ne supprime pas jeu d’enregistrements hello.

1. Sur hello **propriétés du jeu d’enregistrements** panneau pour votre jeu d’enregistrements, recherchez les enregistrements hello.
2. Cliquez sur hello d’enregistrement tooremove. Puis sélectionnez **Supprimer**.

    ![Suppression d’un enregistrement](./media/dns-operations-recordsets-portal/removerecord500.png)

3. Cliquez sur **enregistrer** à hello haut de hello panneau toosave vos paramètres.
4. Une fois l’enregistrement de hello a été supprimé, de valeurs pour l’enregistrement de hello hello hello **zone DNS** panneau reflète la suppression de hello.

## <a name="delete"></a>Suppression d’un jeu d'enregistrements

1. Sur hello **propriétés du jeu d’enregistrements** panneau pour votre jeu d’enregistrements, cliquez sur **supprimer**.

    ![Supprimer un jeu d’enregistrements](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. Un message apparaît vous demandant si vous souhaitez que le jeu d’enregistrements toodelete hello.
3. Vérifiez que hello nom correspondances hello enregistrement que vous souhaitez toodelete, puis cliquez sur **Oui**.
4. Sur hello **zone DNS** panneau, vérifiez que le jeu d’enregistrements hello n’est plus visible.

## <a name="work-with-ns-and-soa-records"></a>Utilisation d’enregistrements NS et SOA

Les enregistrements NS et SOA qui sont créés automatiquement sont gérés différemment des autres types d’enregistrements.

### <a name="modify-soa-records"></a>Modification d'enregistrements SOA

Impossible d’ajouter ou supprimer des enregistrements de hello créé automatiquement SOA jeu d’enregistrements au sommet de zone hello (nom = « @ »). Toutefois, vous pouvez modifier les paramètres de hello dans hello enregistrement SOA (à l’exception de « hôte ») et enregistrement de hello définie la durée de vie.

### <a name="modify-ns-records-at-hello-zone-apex"></a>Modifier les enregistrements NS au sommet de zone hello

jeu au sommet de zone hello d’enregistrements NS Hello sont automatiquement créé avec chaque zone DNS. Il contient les noms de hello de zone de hello Azure DNS nom serveurs toohello attribué.

Vous pouvez ajouter des noms supplémentaires serveurs toothis NS jeu d’enregistrements, toosupport domaines l’hébergement avec le fournisseur DNS. Vous pouvez également modifier la durée de vie de hello et les métadonnées pour ce jeu d’enregistrements. Toutefois, vous ne peut pas supprimer ou modifier les serveurs de noms DNS Azure hello préremplies.

Notez que cela s’applique uniquement toohello NS jeu d’enregistrements au sommet de zone hello. Autres jeux d’enregistrements NS dans votre zone (comme les zones enfant toodelegate utilisé) peut être modifié sans contrainte.

### <a name="delete-soa-or-ns-record-sets"></a>Suppression de jeux d’enregistrements SOA ou NS

Vous ne pouvez pas supprimer hello SOA et NS jeux d’enregistrements au sommet de zone hello (nom = « @ ») qui sont créés automatiquement lors de la zone de hello est créée. Elles sont supprimées automatiquement lorsque vous supprimez la zone de hello.

## <a name="next-steps"></a>Étapes suivantes

* Pour plus d’informations sur le système DNS Azure, consultez hello [vue d’ensemble de DNS Azure](dns-overview.md).
* Pour plus d’informations sur l’automatisation de DNS, consultez [zones DNS de création et jeux d’enregistrements à l’aide de .NET SDK hello](dns-sdk.md).
* Pour plus d’informations sur les enregistrements DNS inversés, consultez l’article [Vue d’ensemble des DNS inversés et assistance dans Azure](dns-reverse-dns-overview.md).
