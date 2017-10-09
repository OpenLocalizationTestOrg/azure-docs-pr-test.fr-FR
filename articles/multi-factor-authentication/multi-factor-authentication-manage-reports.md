---
title: "rapports d’aaaAccess et d’utilisation pour l’authentification Multifacteur Azure | Documents Microsoft"
description: "Cette section décrit comment toouse hello fonctionnalité Azure multi-Factor Authentication - rapports."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: curtand
ms.assetid: 3f6b33c4-04c8-47d4-aecb-aa39a61c4189
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: ae7ccceca4968d7ec7cf0cb1cf9e041d9997c840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reports-in-azure-multi-factor-authentication"></a>Rapports dans Azure Multi-Factor Authentication
Azure Multi-Factor Authentication fournit plusieurs rapports qui peuvent être utilisés par vous et votre organisation. Ces rapports sont accessibles via le portail de gestion de l’authentification multifacteur de hello. Hello Voici une liste des rapports disponibles de hello :

| Rapport | Description |
|:--- |:--- |
| Usage |l’utilisation de Hello rapports affichent des informations sur l’utilisation globale et résumé utilisateur des détails de l’utilisateur. |
| État du serveur |Ce rapport affiche l’état de hello des serveurs de l’authentification multifacteur associé à votre compte. |
| Historique de l'utilisateur bloqué |Ces rapports présentent historique hello de demandes tooblock ou débloquer des utilisateurs. |
| Historique de l'utilisateur contourné |Affiche l’historique de hello de demandes toobypass multi-Factor Authentication pour le numéro de téléphone d’un utilisateur. |
| Alerte de fraude |Affiche l’historique des alertes de fraude soumises au cours de la plage de dates hello spécifiée. |
| Mis en file d'attente. |Répertorie les rapports en file d'attente de traitement et leur état. Un lien du rapport hello toodownload ou de la vue est fourni lorsque hello du rapport est terminée. |

## <a name="view-reports"></a>Afficher des rapports
1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).
2. Sur la gauche de hello, sélectionnez Active Directory.
3. Suivez l’une de ces deux options, selon que vous utilisez ou non des fournisseurs d’authentification :
   * **Option 1**: cliquez sur onglet de fournisseurs d’authentification multifacteur hello. Sélectionnez votre fournisseur d’authentification Multifacteur et cliquez sur hello **gérer** bouton bas hello.
   * **Option 2**: sélectionnez votre toohello de répertoire et accédez **configurer** onglet. Sous la section de l’authentification multifacteur hello, sélectionnez **gérer les paramètres de service**. En hello en bas de page de paramètres de Service d’authentification Multifacteur hello, cliquez sur lien vers le portail Go toohello de hello.
4. Bonjour portail de gestion Azure multi-Factor Authentication, sélectionnez type hello de rapport souhaité dans hello **afficher un rapport** section Bonjour barre de navigation gauche.

<center>![Cloud](./media/multi-factor-authentication-manage-reports/report.png)</center>


**Ressources supplémentaires**

* [Pour les utilisateurs](end-user/multi-factor-authentication-end-user.md)
* [Azure Multi-Factor Authentication sur MSDN](https://msdn.microsoft.com/library/azure/dn249471.aspx)
