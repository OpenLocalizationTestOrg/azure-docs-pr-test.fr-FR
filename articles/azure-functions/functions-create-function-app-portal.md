---
title: aaaCreate une application de la fonction de hello portail Azure | Documents Microsoft
description: "Créer une nouvelle application de fonction dans Azure App Service à partir du portail de hello."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/11/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: c531fc71c798edf22e25a5f4b79c15413809dc86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-from-hello-azure-portal"></a>Créer une application de la fonction à partir de hello portail Azure

Les applications Azure (fonction) utilise l’infrastructure de Service d’applications Azure hello. Cette rubrique vous montre comment toocreate une application de la fonction Bonjour portail Azure. Une application de la fonction est un conteneur hello qui héberge l’exécution de hello des fonctions individuelles. Lorsque vous créez une application de la fonction Bonjour plan d’hébergement du Service d’applications, votre application de la fonction peut utiliser toutes les fonctionnalités de hello du Service d’application.

## <a name="create-a-function-app"></a>Créer une Function App

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

Lorsque vous créez une Function App, vous devez entrer un **nom d’application** valide, qui peut seulement contenir des lettres, des chiffres et des traits d’union. Le trait de soulignement (**_**) n’est pas un caractère autorisé.

Les noms des comptes de stockage doivent comporter entre 3 et 24 caractères, uniquement des lettres minuscules et des chiffres. Le nom de votre compte de stockage doit être unique dans Azure. 

Après que application de fonction hello est créée, vous pouvez créer des fonctions individuelles dans une ou plusieurs langues différentes. Créer des fonctions [à l’aide du portail de hello](functions-create-first-azure-function.md#create-function), [déploiement continu](functions-continuous-deployment.md), ou par [télécharger avec FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).

## <a name="service-plans"></a>Plans de service

Azure Functions contient deux plans de service différents : le plan de consommation et le plan App Service. plan de la consommation Hello alloue automatiquement la puissance de calcul lorsque votre code s’exécute, échelles montée en tant que charge de toohandle nécessaires, puis, dans l’échelle lorsque le code n’est pas en cours d’exécution. Hello plan App Service permet à votre fonction application tooall hello les lieux de Service d’applications. Vous devez choisir votre plan de service lors de la création de votre Function App. Il ne peut pas être modifié actuellement. Pour plus d’informations, consultez [Choisir un plan d’hébergement Azure Functions](functions-scale.md).

Si vous prévoyez toorun les fonctions JavaScript sur un plan App Service, vous devez choisir un plan avec moins de cœurs. Pour plus d’informations, consultez hello [référence JavaScript pour les fonctions](functions-reference-node.md#choose-single-core-app-service-plans).

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a>Conditions requises pour le compte de stockage

Lorsque vous créez une application de la fonction dans le Service d’applications, vous devez créer ou lier tooa à usage général compte de stockage Azure qui prend en charge le stockage Blob, file d’attente et Table. En interne, Azure Functions utilise le stockage pour les opérations telles que la gestion des déclencheurs et la journalisation des exécutions de fonctions. Certains comptes de stockage ne prennent pas en charge les files d’attente et les tables, comme les comptes de stockage Blob uniquement, le stockage Premium Azure et les comptes de stockage à usage général avec la réplication ZRS. Ces comptes sont exclus du panneau du compte de stockage hello lors de la création d’une application de la fonction.

>[!NOTE]
>Lorsque vous utilisez un plan d’hébergement hello consommation, vos fichiers de configuration de liaison et le code de fonction sont stockés dans le stockage de fichiers Azure hello principal compte de stockage. Lorsque vous supprimez le compte de stockage principal hello, ce contenu est supprimé et ne peut pas être récupéré.

toolearn savoir plus sur les types de compte de stockage, consultez [présentation des Services de stockage Azure hello](../storage/common/storage-introduction.md#introducing-the-azure-storage-services). 

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



