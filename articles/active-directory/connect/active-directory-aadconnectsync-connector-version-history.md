---
title: "Historique de publication des versions du connecteur | Microsoft Docs"
description: "Cette rubrique répertorie toutes les versions des connecteurs de Forefront Identity Manager (FIM) et Microsoft Identity Manager (MIM)."
services: active-directory
documentationcenter: 
author: fimguy
manager: femila
editor: 
ms.assetid: 6a0c66ab-55df-4669-a0c7-1fe1a091a7f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: fimguy
ms.openlocfilehash: 313145f4d8e5faa91fb3504cb0fd0ba87ca2e379
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="connector-version-release-history"></a><span data-ttu-id="1db4f-103">Historique de publication des versions du connecteur</span><span class="sxs-lookup"><span data-stu-id="1db4f-103">Connector Version Release History</span></span>
<span data-ttu-id="1db4f-104">Les connecteurs de Forefront Identity Manager (FIM) et Microsoft Identity Manager (MIM) sont fréquemment mis à jour.</span><span class="sxs-lookup"><span data-stu-id="1db4f-104">The Connectors for Forefront Identity Manager (FIM) and Microsoft Identity Manager (MIM) are updated frequently.</span></span>

> [!NOTE]
> <span data-ttu-id="1db4f-105">Cette rubrique ne concerne que FIM et MIM.</span><span class="sxs-lookup"><span data-stu-id="1db4f-105">This topic is on FIM and MIM only.</span></span> <span data-ttu-id="1db4f-106">Ces connecteurs ne sont pas pris en charge pour l’installation sur Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="1db4f-106">These Connectors are not supported for install on Azure AD Connect.</span></span> <span data-ttu-id="1db4f-107">Les connecteurs finaux sont préinstallés sur AADConnect lors de la mise à niveau vers la version spécifiée.</span><span class="sxs-lookup"><span data-stu-id="1db4f-107">Released Connectors are preinstalled on AADConnect when upgrading to specified Build.</span></span>

<span data-ttu-id="1db4f-108">Cette rubrique répertorie toutes les versions des connecteurs qui ont été publiées.</span><span class="sxs-lookup"><span data-stu-id="1db4f-108">This topic list all versions of the Connectors that have been released.</span></span>

<span data-ttu-id="1db4f-109">Liens connexes :</span><span class="sxs-lookup"><span data-stu-id="1db4f-109">Related links:</span></span>

* [<span data-ttu-id="1db4f-110">Télécharger les derniers connecteurs</span><span class="sxs-lookup"><span data-stu-id="1db4f-110">Download Latest Connectors</span></span>](http://go.microsoft.com/fwlink/?LinkId=717495)
* <span data-ttu-id="1db4f-111">[connecteur LDAP générique](active-directory-aadconnectsync-connector-genericldap.md) </span><span class="sxs-lookup"><span data-stu-id="1db4f-111">[Generic LDAP Connector](active-directory-aadconnectsync-connector-genericldap.md) reference documentation</span></span>
* <span data-ttu-id="1db4f-112">[connecteur SQL générique](active-directory-aadconnectsync-connector-genericsql.md) </span><span class="sxs-lookup"><span data-stu-id="1db4f-112">[Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md) reference documentation</span></span>
* <span data-ttu-id="1db4f-113">[connecteur WebServices](http://go.microsoft.com/fwlink/?LinkID=226245) </span><span class="sxs-lookup"><span data-stu-id="1db4f-113">[Web Services Connector](http://go.microsoft.com/fwlink/?LinkID=226245) reference documentation</span></span>
* <span data-ttu-id="1db4f-114">[connecteur PowerShell](active-directory-aadconnectsync-connector-powershell.md) </span><span class="sxs-lookup"><span data-stu-id="1db4f-114">[PowerShell Connector](active-directory-aadconnectsync-connector-powershell.md) reference documentation</span></span>
* <span data-ttu-id="1db4f-115">[connecteur Lotus Domino](active-directory-aadconnectsync-connector-domino.md) </span><span class="sxs-lookup"><span data-stu-id="1db4f-115">[Lotus Domino Connector](active-directory-aadconnectsync-connector-domino.md) reference documentation</span></span>


## <a name="116040-aadconnect-pending-release"></a><span data-ttu-id="1db4f-116">1.1.604.0 (AADConnect en attente de publication)</span><span class="sxs-lookup"><span data-stu-id="1db4f-116">1.1.604.0 (AADConnect Pending Release)</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="1db4f-117">Problèmes résolus :</span><span class="sxs-lookup"><span data-stu-id="1db4f-117">Fixed issues:</span></span>

* <span data-ttu-id="1db4f-118">Services web génériques :</span><span class="sxs-lookup"><span data-stu-id="1db4f-118">Generic Web Services:</span></span>
  * <span data-ttu-id="1db4f-119">Correction d’un problème empêchant la création d’un projet SOAP lorsqu’il existait deux points de terminaison ou plus.</span><span class="sxs-lookup"><span data-stu-id="1db4f-119">Fixed an issue preventing a SOAP project from being created when there were two or more endpoints.</span></span>
* <span data-ttu-id="1db4f-120">SQL générique :</span><span class="sxs-lookup"><span data-stu-id="1db4f-120">Generic SQL:</span></span>
  * <span data-ttu-id="1db4f-121">Dans l’opération d’importation, GSQL ne convertissait pas l’heure correctement lors de l’enregistrement dans l’espace du connecteur.</span><span class="sxs-lookup"><span data-stu-id="1db4f-121">In the operation of import the GSQL was not converting time correctly, when saved to connector space.</span></span> <span data-ttu-id="1db4f-122">Le format de date et d’heure par défaut de l’espace de connecteur de GSQL « aaaa-MM-jj hh:mm:ssZ » a été remplacé par « aaaa-MM-jj HH:mm:ssZ ».</span><span class="sxs-lookup"><span data-stu-id="1db4f-122">The default date and time format for connector space of the GSQL was changed from 'yyyy-MM-dd hh:mm:ssZ' to 'yyyy-MM-dd HH:mm:ssZ'.</span></span>

## <a name="115510-aadconnect-115530"></a><span data-ttu-id="1db4f-123">1.1.551.0 (AADConnect 1.1.553.0)</span><span class="sxs-lookup"><span data-stu-id="1db4f-123">1.1.551.0 (AADConnect 1.1.553.0)</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="1db4f-124">Problèmes résolus :</span><span class="sxs-lookup"><span data-stu-id="1db4f-124">Fixed issues:</span></span>

* <span data-ttu-id="1db4f-125">Services web génériques :</span><span class="sxs-lookup"><span data-stu-id="1db4f-125">Generic Web Services:</span></span>
  * <span data-ttu-id="1db4f-126">L’outil Wsconfig n’a pas converti correctement le tableau Json à partir de « exemple de demande » pour la méthode de service REST.</span><span class="sxs-lookup"><span data-stu-id="1db4f-126">The Wsconfig tool did not convert correctly the Json array from "sample request" for the REST service method.</span></span> <span data-ttu-id="1db4f-127">Ceci entraînait des problèmes lors de la sérialisation de ce tableau Json pour la demande REST.</span><span class="sxs-lookup"><span data-stu-id="1db4f-127">This caused problems with serialization this Json array for the REST request.</span></span>
  * <span data-ttu-id="1db4f-128">L’outil de configuration du connecteur de service web ne prend pas en charge l’utilisation de symboles d’espace dans les noms d’attribut JSON</span><span class="sxs-lookup"><span data-stu-id="1db4f-128">Web Service Connector Configuration Tool does not support usage of space symbols in JSON attribute names</span></span> 
    * <span data-ttu-id="1db4f-129">Un modèle de substitution peut être ajouté manuellement dans le fichier WSConfigTool.exe.config, par exemple ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span><span class="sxs-lookup"><span data-stu-id="1db4f-129">A Substitution pattern can be added manually to the WSConfigTool.exe.config file, e.g. ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span></span>

* <span data-ttu-id="1db4f-130">Lotus Notes :</span><span class="sxs-lookup"><span data-stu-id="1db4f-130">Lotus Notes:</span></span>
  * <span data-ttu-id="1db4f-131">Quand l’option **Allow custom certifiers for Organization/Organizational Units** (Autoriser les certificateurs personnalisés pour les organisations/unités d’organisation) est désactivée, le connecteur échoue pendant l’exportation (mise à jour). Après le flux d’exportation, tous les attributs sont exportés vers Domino, mais au moment de l’exportation KeyNotFoundException est retournée à la synchronisation.</span><span class="sxs-lookup"><span data-stu-id="1db4f-131">When the option **Allow custom certifiers for Organization/Organizational Units** is disabled then the connector fails during export (Update) After the export flow all attributes are exported to Domino but at the time of export a KeyNotFoundException is returned to Sync.</span></span> 
    * <span data-ttu-id="1db4f-132">Cela se produit car l’opération de renommage échoue quand elle tente de changer le nom unique (attribut UserName) en modifiant l’un des attributs ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1db4f-132">This happens because the rename operation fails when it tries to change DN (UserName attribute) by changing one of the attributes below:</span></span>  
      - <span data-ttu-id="1db4f-133">LastName</span><span class="sxs-lookup"><span data-stu-id="1db4f-133">LastName</span></span>
      - <span data-ttu-id="1db4f-134">FirstName</span><span class="sxs-lookup"><span data-stu-id="1db4f-134">FirstName</span></span>
      - <span data-ttu-id="1db4f-135">MiddleInitial</span><span class="sxs-lookup"><span data-stu-id="1db4f-135">MiddleInitial</span></span>
      - <span data-ttu-id="1db4f-136">AltFullName</span><span class="sxs-lookup"><span data-stu-id="1db4f-136">AltFullName</span></span>
      - <span data-ttu-id="1db4f-137">AltFullNameLanguage</span><span class="sxs-lookup"><span data-stu-id="1db4f-137">AltFullNameLanguage</span></span>
      - <span data-ttu-id="1db4f-138">Unité d’organisation</span><span class="sxs-lookup"><span data-stu-id="1db4f-138">ou</span></span>
      - <span data-ttu-id="1db4f-139">altcommonname</span><span class="sxs-lookup"><span data-stu-id="1db4f-139">altcommonname</span></span>

  * <span data-ttu-id="1db4f-140">Quand l’option **Allow custom certifiers for Organization/Organizational Units** (Autoriser les certificateurs personnalisés pour les organisations/unités d’organisation) est activée, mais que les certificateurs nécessaires sont encore vides, une exception KeyNotFoundException se produit.</span><span class="sxs-lookup"><span data-stu-id="1db4f-140">When **Allow custom certifiers for Organization/Organizational Units** option is enabled, but required certifiers are still empty, then KeyNotFoundException occurs.</span></span>

### <a name="enhancements"></a><span data-ttu-id="1db4f-141">Améliorations :</span><span class="sxs-lookup"><span data-stu-id="1db4f-141">Enhancements:</span></span>

* <span data-ttu-id="1db4f-142">SQL générique :</span><span class="sxs-lookup"><span data-stu-id="1db4f-142">Generic SQL:</span></span>
  * <span data-ttu-id="1db4f-143">**Scénario : repensé Implémenté  : fonctionnalité**  « * »</span><span class="sxs-lookup"><span data-stu-id="1db4f-143">**Scenario: redesigned Implemented:** "*" feature</span></span>
  * <span data-ttu-id="1db4f-144">**Description de la solution :** modification de l’approche pour la [gestion des attributs de référence à valeurs multiples](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="1db4f-144">**Solution description:** Changed approach for [multi-valued reference attributes handling](active-directory-aadconnectsync-connector-genericsql.md).</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="1db4f-145">Problèmes résolus :</span><span class="sxs-lookup"><span data-stu-id="1db4f-145">Fixed issues:</span></span>

* <span data-ttu-id="1db4f-146">Services web génériques :</span><span class="sxs-lookup"><span data-stu-id="1db4f-146">Generic Web Services:</span></span>
  * <span data-ttu-id="1db4f-147">Impossible d’importer la configuration serveur si le connecteur de service web est présent</span><span class="sxs-lookup"><span data-stu-id="1db4f-147">Can’t import Server configuration if WebService Connector is present</span></span>
  * <span data-ttu-id="1db4f-148">Le connecteur de service web ne fonctionne pas avec plusieurs services web</span><span class="sxs-lookup"><span data-stu-id="1db4f-148">WebService Connector is not working with multiple  Web Services</span></span>

* <span data-ttu-id="1db4f-149">SQL générique :</span><span class="sxs-lookup"><span data-stu-id="1db4f-149">Generic SQL:</span></span>
  * <span data-ttu-id="1db4f-150">Aucun type d’objet n’est répertorié pour l’attribut référencé à valeur unique</span><span class="sxs-lookup"><span data-stu-id="1db4f-150">No object types are listed for single value referenced attribute</span></span>
  * <span data-ttu-id="1db4f-151">L’importation différentielle sur la stratégie Change Tracking supprime objet lorsque la valeur est supprimée de la table à valeurs multiples</span><span class="sxs-lookup"><span data-stu-id="1db4f-151">Delta import on Change Tracking strategy deletes object when value is removed from multi-value table</span></span>
  * <span data-ttu-id="1db4f-152">OverflowException dans le connecteur GSQL avec DB2 sur AS/400</span><span class="sxs-lookup"><span data-stu-id="1db4f-152">OverflowException in GSQL connector with DB2 on AS/400</span></span>

<span data-ttu-id="1db4f-153">Lotus :</span><span class="sxs-lookup"><span data-stu-id="1db4f-153">Lotus:</span></span>
  * <span data-ttu-id="1db4f-154">Ajout de l’option pour activer/désactiver la recherche d’unités d’organisation avant d’ouvrir la page GlobalParameters</span><span class="sxs-lookup"><span data-stu-id="1db4f-154">Added option to enable\disable searching OUs before opening GlobalParameters page</span></span>

## <a name="114430"></a><span data-ttu-id="1db4f-155">1.1.443.0</span><span class="sxs-lookup"><span data-stu-id="1db4f-155">1.1.443.0</span></span>

<span data-ttu-id="1db4f-156">Publié : mars 2017</span><span class="sxs-lookup"><span data-stu-id="1db4f-156">Released: 2017 March</span></span>

### <a name="enhancements"></a><span data-ttu-id="1db4f-157">Améliorations</span><span class="sxs-lookup"><span data-stu-id="1db4f-157">Enhancements</span></span>

* <span data-ttu-id="1db4f-158">SQL générique :</span><span class="sxs-lookup"><span data-stu-id="1db4f-158">Generic SQL:</span></span></br><span data-ttu-id="1db4f-159">
  **Symptômes du scénario :** Avec cette limitation connue du connecteur SQL, seule une référence à un type d’objet est autorisée et une référence croisée avec des membres est requise.</span><span class="sxs-lookup"><span data-stu-id="1db4f-159">
  **Scenario Symptoms:**  It is a well-known limitation with the SQL Connector where we only allow a reference to one object type and require cross reference with members.</span></span> </br><span data-ttu-id="1db4f-160">
**Description de la solution :** À l’étape de traitement des références pour lesquelles l’option « * » est sélectionnée, toutes les combinaisons de types d’objets sont renvoyées au moteur de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="1db4f-160">
**Solution description:** In the processing step for references were "*" option is chosen, ALL combinations of object types will be returned back to the sync engine.</span></span>

>[!Important]
- <span data-ttu-id="1db4f-161">Cela crée de nombreux espaces réservés.</span><span class="sxs-lookup"><span data-stu-id="1db4f-161">This will create many placeholders</span></span>
- <span data-ttu-id="1db4f-162">L’utilisation d’une dénomination unique pour l’ensemble des types d’objets est requise.</span><span class="sxs-lookup"><span data-stu-id="1db4f-162">It is required to make sure the naming is unique cross object types.</span></span>


* <span data-ttu-id="1db4f-163">LDAP générique :</span><span class="sxs-lookup"><span data-stu-id="1db4f-163">Generic LDAP:</span></span></br><span data-ttu-id="1db4f-164">
 **Scénario :** Lorsque seuls certains conteneurs sont sélectionnés dans une partition spécifique, la recherche est tout de même effectuée dans la partition entière.</span><span class="sxs-lookup"><span data-stu-id="1db4f-164">
**Scenario:** When only few containers are selected in specific partition, then the search still will be done in whole partition.</span></span> <span data-ttu-id="1db4f-165">La partition spécifique est filtrée par le service de synchronisation et non par MA, ce qui peut entraîner une dégradation des performances.</span><span class="sxs-lookup"><span data-stu-id="1db4f-165">Specific will be filtered by Synchronization Service, but not by MA which might cause performance degradation.</span></span> </br>

 <span data-ttu-id="1db4f-166">**Description de la solution :** Le code du connecteur GLDAP a été modifié pour pouvoir accéder à tous les conteneurs et rechercher des objets dans chacun d’eux, au lieu de rechercher dans la partition entière.</span><span class="sxs-lookup"><span data-stu-id="1db4f-166">**Solution description:** Changed GLDAP connector's code to make it possible go through all containers and search objects in each of them, instead of searching in the whole partition.</span></span>


* <span data-ttu-id="1db4f-167">Lotus Domino :</span><span class="sxs-lookup"><span data-stu-id="1db4f-167">Lotus Domino:</span></span>

  <span data-ttu-id="1db4f-168">**Scénario :** Prise en charge de la suppression d’un courrier Domino pour la suppression d’une personne pendant une exportation.</span><span class="sxs-lookup"><span data-stu-id="1db4f-168">**Scenario:** Domino mail deletion support for a person removal during an export.</span></span> </br><span data-ttu-id="1db4f-169">
  **Solution :** Prise en charge de la suppression d’un courrier configurable pour la suppression d’une personne pendant une exportation.</span><span class="sxs-lookup"><span data-stu-id="1db4f-169">
**Solution:** Configurable mail deletion support for a person removal during an export.</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="1db4f-170">Problèmes résolus :</span><span class="sxs-lookup"><span data-stu-id="1db4f-170">Fixed issues:</span></span>
* <span data-ttu-id="1db4f-171">Services web génériques :</span><span class="sxs-lookup"><span data-stu-id="1db4f-171">Generic Web Services:</span></span>
 * <span data-ttu-id="1db4f-172">Lors de la modification de l’URL du service dans les projets wsconfig SAP par défaut via l’outil de configuration de service web, l’erreur suivante se produit : Impossible de trouver une partie du chemin d’accès</span><span class="sxs-lookup"><span data-stu-id="1db4f-172">When changing the service URL in Default SAP wsconfig projects through WebService Configuration Tool then the following error happens: Could not find a part of the path</span></span>

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* <span data-ttu-id="1db4f-173">LDAP générique :</span><span class="sxs-lookup"><span data-stu-id="1db4f-173">Generic LDAP:</span></span>
 * <span data-ttu-id="1db4f-174">Le connecteur GLDAP ne voit pas tous les attributs dans AD LDS</span><span class="sxs-lookup"><span data-stu-id="1db4f-174">GLDAP Connector does not see all attributes in AD LDS</span></span>
 * <span data-ttu-id="1db4f-175">L’assistant se bloque lorsqu’aucun attribut UPN n’est détecté dans le schéma d’annuaire LDAP</span><span class="sxs-lookup"><span data-stu-id="1db4f-175">Wizard breaks when no UPN attributes are detected from the LDAP directory schema</span></span>
 * <span data-ttu-id="1db4f-176">Les échecs d’importation delta avec erreurs de détection n’apparaissent pas pendant l’importation complète, lorsque l’attribut « objectclass » n’est pas sélectionné.</span><span class="sxs-lookup"><span data-stu-id="1db4f-176">Delta Imports Failing with discovery errors not present during full import, when "objectclass" attribute is not selected</span></span>
 * <span data-ttu-id="1db4f-177">Une page de configuration « Configurer des partitions et des hiérarchies », n’affiche aucun objet de type égal à la partition des nouveaux serveurs dans le LDAP MA</span><span class="sxs-lookup"><span data-stu-id="1db4f-177">A "Configure Partitions and Hierarchies” configuration page, doesn’t show any objects which type is equal to the partition for Novel servers in the Generic</span></span>  
<span data-ttu-id="1db4f-178">générique.</span><span class="sxs-lookup"><span data-stu-id="1db4f-178">LDAP MA.</span></span> <span data-ttu-id="1db4f-179">Seuls les objets de la partition RootDSE sont affichés.</span><span class="sxs-lookup"><span data-stu-id="1db4f-179">They showed only objects from RootDSE partition.</span></span>


* <span data-ttu-id="1db4f-180">SQL générique :</span><span class="sxs-lookup"><span data-stu-id="1db4f-180">Generic SQL:</span></span>
 * <span data-ttu-id="1db4f-181">Correction du bogue empêchant l’importation d’un attribut à valeurs multiples d’importation delta de filigrane SQL générique</span><span class="sxs-lookup"><span data-stu-id="1db4f-181">Fix for Generic SQL watermark Delta Import multivalued attribute not imported bug</span></span>
 * <span data-ttu-id="1db4f-182">Lors de l’exportation des valeurs supprimées\ajoutées d’un attribut à valeurs multiples, celles-ci ne sont pas supprimées\ajoutées dans la source de données.</span><span class="sxs-lookup"><span data-stu-id="1db4f-182">When exporting deleted\added values of multivalued attribute, they are not deleted\added in data source.</span></span>  


* <span data-ttu-id="1db4f-183">Lotus Notes :</span><span class="sxs-lookup"><span data-stu-id="1db4f-183">Lotus Notes:</span></span>
 * <span data-ttu-id="1db4f-184">Un champ spécifique « Nom complet » est affiché correctement dans le métaverse, mais lors de l’exportation vers Notes, la valeur de l’attribut est Null ou vide.</span><span class="sxs-lookup"><span data-stu-id="1db4f-184">A specific field "Full Name" is shown in the metaverse correctly however when exporting to Notes the value for the attribute is Null or Empty.</span></span>
 * <span data-ttu-id="1db4f-185">Correction d’erreur de certification en double</span><span class="sxs-lookup"><span data-stu-id="1db4f-185">Fix for duplicate Certifier error</span></span>
 * <span data-ttu-id="1db4f-186">Lorsque l’objet ne comportant aucune donnée est sélectionné sur le connecteur Lotus Domino avec d’autres objets, nous recevons une erreur de détection lors de l’importation complète.</span><span class="sxs-lookup"><span data-stu-id="1db4f-186">When the Object without any data is selected on the Lotus Domino Connector with other objects then we receive the Discovery error while performing Full-Import.</span></span>
 * <span data-ttu-id="1db4f-187">Lorsque l’importation delta est exécutée sur le connecteur Lotus Domino, à la fin de l’exécution, le service Microsoft.IdentityManagement.MA.LotusDomino.Service.exe renvoie parfois une erreur d’application.</span><span class="sxs-lookup"><span data-stu-id="1db4f-187">When Delta Import is being running on the Lotus Domino Connector, at the end of that run, the Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service sometimes returns an Application Error.</span></span>
 * <span data-ttu-id="1db4f-188">L’appartenance au groupe global fonctionne correctement et est conservée, sauf lors de l’exécution de l’exportation visant à supprimer un utilisateur de l’appartenance qui apparaît comme ayant réussi avec une mise à jour, alors que l’utilisateur n’a pas réellement été supprimé de l’appartenance dans Lotus Notes.</span><span class="sxs-lookup"><span data-stu-id="1db4f-188">Group membership overall works fine and is maintained, except when running the export to try to remove a user from membership it shows as successful with an update, but the user doesn’t actually get removed from membership in Lotus Notes.</span></span>
 * <span data-ttu-id="1db4f-189">Une option permettant de choisir le mode d’exportation « Append Item at bottom » (Ajouter un élément en bas) a été ajoutée dans l’interface utilisateur de configuration de Lotus MA pour ajouter de nouveaux éléments en bas pendant l’exportation des attributs à valeurs multiples.</span><span class="sxs-lookup"><span data-stu-id="1db4f-189">An opportunity to choose mode of export as “Append Item at bottom” was added in configuration GUI of Lotus MA to append new items at bottom during the export for multi-valued attributes.</span></span>
 * <span data-ttu-id="1db4f-190">Le connecteur ajoute la logique requise pour supprimer le fichier du dossier des courriers et du coffre d’ID.</span><span class="sxs-lookup"><span data-stu-id="1db4f-190">Connector will add the needed logic to delete the file from the Mail Folder and ID Vault.</span></span>
 * <span data-ttu-id="1db4f-191">La suppression d’appartenance ne fonctionne pas pour un membre NAB croisé.</span><span class="sxs-lookup"><span data-stu-id="1db4f-191">Delete membership not working for cross NAB member.</span></span>
 * <span data-ttu-id="1db4f-192">Les valeurs devraient être supprimées correctement de l’attribut à valeurs multiples.</span><span class="sxs-lookup"><span data-stu-id="1db4f-192">Values should be successfully deleted from multi-valued attribute</span></span>

## <a name="111170"></a><span data-ttu-id="1db4f-193">1.1.117.0</span><span class="sxs-lookup"><span data-stu-id="1db4f-193">1.1.117.0</span></span>
<span data-ttu-id="1db4f-194">Publié : mars 2016</span><span class="sxs-lookup"><span data-stu-id="1db4f-194">Released: 2016 March</span></span>

<span data-ttu-id="1db4f-195">**Nouveau connecteur**</span><span class="sxs-lookup"><span data-stu-id="1db4f-195">**New Connector**</span></span>  
<span data-ttu-id="1db4f-196">Version initiale du [connecteur SQL générique](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="1db4f-196">Initial release of the [Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md).</span></span>

<span data-ttu-id="1db4f-197">**Nouvelles fonctionnalités :**</span><span class="sxs-lookup"><span data-stu-id="1db4f-197">**New features:**</span></span>

* <span data-ttu-id="1db4f-198">Connecteur LDAP générique :</span><span class="sxs-lookup"><span data-stu-id="1db4f-198">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="1db4f-199">Prise en charge supplémentaire pour l’importation delta avec Isode.</span><span class="sxs-lookup"><span data-stu-id="1db4f-199">Added support for delta import with Isode.</span></span>
* <span data-ttu-id="1db4f-200">Connecteur des services web :</span><span class="sxs-lookup"><span data-stu-id="1db4f-200">Web Services Connector:</span></span>
  * <span data-ttu-id="1db4f-201">Mise à jour de l’activité csEntryChangeResult et de l’activité setImportErrorCode pour autoriser le renvoi des erreurs au niveau de l’objet vers le moteur de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="1db4f-201">Updated the csEntryChangeResult activity and setImportErrorCode activity to allow object level errors to be returned back to the sync engine.</span></span>
  * <span data-ttu-id="1db4f-202">Mise à jour des modèles SAP6 et SAP6User pour utiliser les nouvelles fonctionnalités d’erreur au niveau de l’objet.</span><span class="sxs-lookup"><span data-stu-id="1db4f-202">Updated the SAP6 and SAP6User templates to use the new object level error functionality.</span></span>
* <span data-ttu-id="1db4f-203">Connecteur Lotus Domino :</span><span class="sxs-lookup"><span data-stu-id="1db4f-203">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="1db4f-204">Lors de l’exportation, vous avez besoin d’une autorité de certification par carnet d’adresses.</span><span class="sxs-lookup"><span data-stu-id="1db4f-204">For export, you need one certifier per address book.</span></span> <span data-ttu-id="1db4f-205">Vous pouvez désormais utiliser le même mot de passe pour toutes les autorités de certification pour simplifier la gestion.</span><span class="sxs-lookup"><span data-stu-id="1db4f-205">You can now use the same password for all certifiers to make the management easier.</span></span>

<span data-ttu-id="1db4f-206">**Problèmes résolus :**</span><span class="sxs-lookup"><span data-stu-id="1db4f-206">**Fixed issues:**</span></span>

* <span data-ttu-id="1db4f-207">Connecteur LDAP générique :</span><span class="sxs-lookup"><span data-stu-id="1db4f-207">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="1db4f-208">Pour IBM Tivoli DS, certains attributs de référence n’étaient pas été détectés correctement.</span><span class="sxs-lookup"><span data-stu-id="1db4f-208">For IBM Tivoli DS, some reference attributes were not detected correctly.</span></span>
  * <span data-ttu-id="1db4f-209">Pour Open LDAP lors d’une importation delta, les espaces blancs au début et à la fin des chaînes étaient tronqués.</span><span class="sxs-lookup"><span data-stu-id="1db4f-209">For Open LDAP during a delta import, whitespaces at the beginning and end of strings were truncated.</span></span>
  * <span data-ttu-id="1db4f-210">Pour Novell et NetIQ, une exportation qui déplaçait un objet entre des unités d’organisation/conteneurs avec renommage simultané de celui-ci, échouait.</span><span class="sxs-lookup"><span data-stu-id="1db4f-210">For Novell and NetIQ, an export that moved an object between OUs/containers and at the same time renamed the object failed.</span></span>
* <span data-ttu-id="1db4f-211">Connecteur des services web :</span><span class="sxs-lookup"><span data-stu-id="1db4f-211">Web Services Connector:</span></span>
  * <span data-ttu-id="1db4f-212">Si le service web avait plusieurs points de terminaison pour la même liaison, alors le connecteur ne détectait pas correctement ces points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="1db4f-212">If the web service had multiple end-points for same binding, then the Connector did not correctly discover these end-points.</span></span>
* <span data-ttu-id="1db4f-213">Connecteur Lotus Domino :</span><span class="sxs-lookup"><span data-stu-id="1db4f-213">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="1db4f-214">Une exportation de l’attribut fullName vers une Base courrier en arrivée ne fonctionnait pas.</span><span class="sxs-lookup"><span data-stu-id="1db4f-214">An export of the fullName attribute to a mail-in database did not work.</span></span>
  * <span data-ttu-id="1db4f-215">Une exportation qui ajoutait et supprimait un membre d’un groupe exportait uniquement les membres ajoutés.</span><span class="sxs-lookup"><span data-stu-id="1db4f-215">An export which both added and removed member from a group only exported the added members.</span></span>
  * <span data-ttu-id="1db4f-216">Si un document Notes n’est pas valide (attribut isValid défini sur false), le connecteur échoue.</span><span class="sxs-lookup"><span data-stu-id="1db4f-216">If a Notes Document is invalid (the attribute isValid set to false), then the Connector fails.</span></span>

## <a name="older-releases"></a><span data-ttu-id="1db4f-217">Versions plus anciennes</span><span class="sxs-lookup"><span data-stu-id="1db4f-217">Older releases</span></span>
<span data-ttu-id="1db4f-218">Avant mars 2016, les connecteurs étaient publiés sous forme de rubriques de prise en charge.</span><span class="sxs-lookup"><span data-stu-id="1db4f-218">Before March 2016, the Connectors were released as support topics.</span></span>

<span data-ttu-id="1db4f-219">**LDAP générique**</span><span class="sxs-lookup"><span data-stu-id="1db4f-219">**Generic LDAP**</span></span>

* <span data-ttu-id="1db4f-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, septembre 2015</span><span class="sxs-lookup"><span data-stu-id="1db4f-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="1db4f-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, mars 2015</span><span class="sxs-lookup"><span data-stu-id="1db4f-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="1db4f-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, janvier 2015</span><span class="sxs-lookup"><span data-stu-id="1db4f-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, 2015 January</span></span>
* <span data-ttu-id="1db4f-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, septembre 2014</span><span class="sxs-lookup"><span data-stu-id="1db4f-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, 2014 September</span></span>
* <span data-ttu-id="1db4f-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, mars 2014</span><span class="sxs-lookup"><span data-stu-id="1db4f-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, 2014 March</span></span>

<span data-ttu-id="1db4f-225">**WebServices**</span><span class="sxs-lookup"><span data-stu-id="1db4f-225">**WebServices**</span></span>

* <span data-ttu-id="1db4f-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, septembre 2014</span><span class="sxs-lookup"><span data-stu-id="1db4f-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="1db4f-227">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="1db4f-227">**PowerShell**</span></span>

* <span data-ttu-id="1db4f-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, septembre 2014</span><span class="sxs-lookup"><span data-stu-id="1db4f-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="1db4f-229">**Lotus Domino**</span><span class="sxs-lookup"><span data-stu-id="1db4f-229">**Lotus Domino**</span></span>

* <span data-ttu-id="1db4f-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, septembre 2015</span><span class="sxs-lookup"><span data-stu-id="1db4f-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="1db4f-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, mars 2015</span><span class="sxs-lookup"><span data-stu-id="1db4f-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="1db4f-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, août 2014</span><span class="sxs-lookup"><span data-stu-id="1db4f-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, 2014 August</span></span>
* <span data-ttu-id="1db4f-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, février 2014</span><span class="sxs-lookup"><span data-stu-id="1db4f-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, 2014 February</span></span>  
* <span data-ttu-id="1db4f-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, octobre 2013</span><span class="sxs-lookup"><span data-stu-id="1db4f-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, 2013 October</span></span>
* <span data-ttu-id="1db4f-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, août 2013</span><span class="sxs-lookup"><span data-stu-id="1db4f-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, 2013 August</span></span>

## <a name="next-steps"></a><span data-ttu-id="1db4f-236">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1db4f-236">Next steps</span></span>
<span data-ttu-id="1db4f-237">En savoir plus sur la configuration de la [synchronisation Azure AD Connect](active-directory-aadconnectsync-whatis.md) .</span><span class="sxs-lookup"><span data-stu-id="1db4f-237">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="1db4f-238">En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="1db4f-238">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
