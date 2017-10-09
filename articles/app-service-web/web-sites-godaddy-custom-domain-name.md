---
title: "aaaConfigure un nom de domaine personnalisé dans Azure App Service (GoDaddy)"
description: "Découvrez comment toouse un domaine nom de GoDaddy avec Azure Web Apps"
services: app-service
documentationcenter: 
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 33233e30-5846-488f-83f3-b32e5c114564
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 48158ee752f9833249bbf85adf80f572d1c68486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a>Configurer un nom de domaine personnalisé dans Azure App Service (acheté directement sur GoDaddy)
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

Si vous avez acheté domaine via Azure App Service Web Apps, consultez toohello dernière étape de [acheter un domaine pour les applications Web](custom-dns-web-site-buydomains-web-app.md).

Cet article explique comment utiliser un nom de domaine personnalisé acheté directement auprès de [GoDaddy](https://godaddy.com) avec [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a>Présentation des enregistrements DNS
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a>Ajout d'un enregistrement DNS pour votre domaine personnalisé
tooassociate votre domaine personnalisé avec une application web dans le Service d’applications, vous devez ajouter une nouvelle entrée dans la table de hello DNS pour votre domaine personnalisé à l’aide des outils fournis par GoDaddy. Utilisez hello suite d’outils du DNS hello étapes toolocate à GoDaddy.com

1. Connectez-vous au compte tooyour avec GoDaddy.com, puis sélectionnez **mon compte** , puis **gérer mes domaines**. Menu déroulant de sélection hello hello nom de domaine que vous souhaitez toouse avec votre application web Azure, sélectionnez **gérer DNS**.
   
    ![page des domaines personnalisés de GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. À partir de hello **les détails du domaine** page, faites défiler toohello **fichier de Zone DNS** onglet. Il s’agit de section hello utilisée pour ajouter et modifier des enregistrements DNS pour votre nom de domaine.
   
    ![Onglet DNS Zone File](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    Sélectionnez **ajouter un enregistrement** tooadd un enregistrement existant.
   
    trop**modifier** un enregistrement existant, l’icône de stylet & papier hello select à côté de l’enregistrement de hello.
   
   > [!NOTE]
   > Avant d’ajouter de nouveaux enregistrements, notez que GoDaddy a déjà créé des enregistrements DNS pour les sous-domaines populaires (sous **Host** dans l’éditeur), par exemple **email**, **files**, **mail**, etc. Si hello nom que vous souhaitez toouse déjà existe, modifier l’enregistrement de hello existant au lieu de créer un nouveau.
   > 
   > 
3. Lorsque vous ajoutez un enregistrement, vous devez tout d’abord sélectionner le type d’enregistrement hello.
   
    ![sélectionner le type d'enregistrement](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    Ensuite, vous devez fournir hello **hôte** (hello domaine personnalisé ou sous-domaine) et ce qu’il **pointe vers**.
   
    ![ajouter un enregistrement de zone](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * Lorsque vous ajoutez un **un enregistrement (hôte)** -vous devez définir hello **hôte** champ tooeither  **@**  (représente le nom de domaine racine, tel que  **Contoso.com**,) * (un caractère générique pour faire correspondre plusieurs sous-domaines,) ou vous souhaitez toouse sous-domaine hello (par exemple, **www**.) Vous devez définir hello **pointe vers** champ d’adresse IP de toohello de votre application web Azure.
   * Lorsque vous ajoutez un **enregistrement CNAME (alias)** -vous devez définir hello **hôte** champ toohello sous-domaine toouse vous le souhaitez. Par exemple, **www**. Vous devez définir hello **pointe vers** champ toohello **. azurewebsites.net** nom de domaine de votre application web Azure. Par exemple, **contoso.azurewebsites.net**.
4. Cliquez sur **Ajouter**.
5. Sélectionnez **TXT** en tant que type d’enregistrement hello, puis spécifiez un **hôte** valeur  **@**  et un **pointe vers** valeur  **&lt;yourwebappname&gt;. azurewebsites.net**.
   
   > [!NOTE]
   > Cet enregistrement TXT est utilisé par Azure toovalidate que vous possédez le domaine de hello décrite par hello un enregistrement TXT premier enregistrement ou hello. Une fois que le domaine de hello a été mappé toohello web application hello portail Azure, cette entrée de l’enregistrement TXT peut être supprimée.
   > 
   > 
6. Lorsque vous avez terminé d’ajouter ou modifier des enregistrements, cliquez sur **Terminer** toosave modifications.

<a name="enabledomain"></a>

## <a name="enable-hello-domain-name-on-your-web-app"></a>Activer le nom de domaine hello sur votre application web
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

## <a name="whats-changed"></a>Changements apportés
* Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)

