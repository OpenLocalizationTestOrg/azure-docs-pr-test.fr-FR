---
title: "Sérialisation des objets Reliable Collections dans Azure Service Fabric | Microsoft Docs"
description: "Sérialisation des objets Reliable Collections dans Azure Service Fabric"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 9d35374c-2d75-4856-b776-e59284641956
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/8/2017
ms.author: mcoskun
ms.openlocfilehash: c14794b71ce7340d9e90a56d781c712e247ded06
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a><span data-ttu-id="2e906-103">Sérialisation des objets Reliable Collections dans Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2e906-103">Reliable Collection object serialization in Azure Service Fabric</span></span>
<span data-ttu-id="2e906-104">Les objets Reliable Collections répliquent et conserver leurs éléments pour permettre à ces derniers de résister aux pannes d’ordinateur et de courant.</span><span class="sxs-lookup"><span data-stu-id="2e906-104">Reliable Collections' replicate and persist their items to make sure they are durable across machine failures and power outages.</span></span>
<span data-ttu-id="2e906-105">La réplication et la conservation des éléments supposent au préalable d’effectuer une sérialisation.</span><span class="sxs-lookup"><span data-stu-id="2e906-105">Both to replicate and to persist items, Reliable Collections' need to serialize them.</span></span>

<span data-ttu-id="2e906-106">Les objets Reliable Collections récupèrent le sérialiseur approprié pour un type donné à partir de Reliable State Manager.</span><span class="sxs-lookup"><span data-stu-id="2e906-106">Reliable Collections' get the appropriate serializer for a given type from Reliable State Manager.</span></span>
<span data-ttu-id="2e906-107">Reliable State Manager contient des sérialiseurs intégrés et autorise l’inscription de sérialiseurs personnalisés pour un type donné.</span><span class="sxs-lookup"><span data-stu-id="2e906-107">Reliable State Manager contains built-in serializers and allows custom serializers to be registered for a given type.</span></span>

## <a name="built-in-serializers"></a><span data-ttu-id="2e906-108">Sérialiseurs intégrés</span><span class="sxs-lookup"><span data-stu-id="2e906-108">Built-in Serializers</span></span>

<span data-ttu-id="2e906-109">Reliable State Manager intègre un sérialiseur qui est utilisé pour certains types courants de manière à garantir par défaut une sérialisation efficace.</span><span class="sxs-lookup"><span data-stu-id="2e906-109">Reliable State Manager includes built-in serializer for some common types, so that they can be serialized efficiently by default.</span></span> <span data-ttu-id="2e906-110">Pour d’autres types, Reliable State Manager utilise le [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="2e906-110">For other types, Reliable State Manager falls back to use the [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span></span>
<span data-ttu-id="2e906-111">Les sérialiseurs intégrés sont plus efficaces car ils savent que leurs types ne peuvent pas être modifiés et ils n’ont besoin d’inclure aucune information sur le type, par exemple son nom.</span><span class="sxs-lookup"><span data-stu-id="2e906-111">Built-in serializers are more efficient since they know their types cannot change and they do not need to include information about the type like its type name.</span></span>

<span data-ttu-id="2e906-112">Reliable State Manager intègre un sérialiseur pour les types suivants :</span><span class="sxs-lookup"><span data-stu-id="2e906-112">Reliable State Manager has built-in serializer for following types:</span></span> 
- <span data-ttu-id="2e906-113">Guid</span><span class="sxs-lookup"><span data-stu-id="2e906-113">Guid</span></span>
- <span data-ttu-id="2e906-114">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="2e906-114">bool</span></span>
- <span data-ttu-id="2e906-115">byte</span><span class="sxs-lookup"><span data-stu-id="2e906-115">byte</span></span>
- <span data-ttu-id="2e906-116">sbyte</span><span class="sxs-lookup"><span data-stu-id="2e906-116">sbyte</span></span>
- <span data-ttu-id="2e906-117">byte[]</span><span class="sxs-lookup"><span data-stu-id="2e906-117">byte[]</span></span>
- <span data-ttu-id="2e906-118">char</span><span class="sxs-lookup"><span data-stu-id="2e906-118">char</span></span>
- <span data-ttu-id="2e906-119">string</span><span class="sxs-lookup"><span data-stu-id="2e906-119">string</span></span>
- <span data-ttu-id="2e906-120">décimal</span><span class="sxs-lookup"><span data-stu-id="2e906-120">decimal</span></span>
- <span data-ttu-id="2e906-121">double</span><span class="sxs-lookup"><span data-stu-id="2e906-121">double</span></span>
- <span data-ttu-id="2e906-122">float</span><span class="sxs-lookup"><span data-stu-id="2e906-122">float</span></span>
- <span data-ttu-id="2e906-123">int</span><span class="sxs-lookup"><span data-stu-id="2e906-123">int</span></span>
- <span data-ttu-id="2e906-124">uint</span><span class="sxs-lookup"><span data-stu-id="2e906-124">uint</span></span>
- <span data-ttu-id="2e906-125">long</span><span class="sxs-lookup"><span data-stu-id="2e906-125">long</span></span>
- <span data-ttu-id="2e906-126">ulong</span><span class="sxs-lookup"><span data-stu-id="2e906-126">ulong</span></span>
- <span data-ttu-id="2e906-127">short</span><span class="sxs-lookup"><span data-stu-id="2e906-127">short</span></span>
- <span data-ttu-id="2e906-128">ushort</span><span class="sxs-lookup"><span data-stu-id="2e906-128">ushort</span></span>

## <a name="custom-serialization"></a><span data-ttu-id="2e906-129">Sérialisation personnalisée</span><span class="sxs-lookup"><span data-stu-id="2e906-129">Custom Serialization</span></span>

<span data-ttu-id="2e906-130">Les sérialiseurs personnalisés sont couramment utilisés pour augmenter les performances ou pour chiffrer les données sur le réseau et sur le disque.</span><span class="sxs-lookup"><span data-stu-id="2e906-130">Custom serializers are commonly used to increase performance or to encrypt the data over the wire and on disk.</span></span> <span data-ttu-id="2e906-131">Pour différentes raisons, les sérialiseurs personnalisés sont généralement plus efficaces que les sérialiseurs génériques, car ils n’ont pas besoin de sérialiser des informations relatives au type.</span><span class="sxs-lookup"><span data-stu-id="2e906-131">Among other reasons, custom serializers are commonly more efficient than generic serializer since they don't need to serialize information about the type.</span></span> 

<span data-ttu-id="2e906-132">[IReliableStateManager.TryAddStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) permet d’inscrire un sérialiseur personnalisé pour le type T donné. Cette inscription doit intervenir dans la construction du StatefulServiceBase afin de s’assurer que, avant le début de la récupération, tous les objets Reliable Collections ont bien accès au sérialiseur approprié pour lire leurs données persistantes.</span><span class="sxs-lookup"><span data-stu-id="2e906-132">[IReliableStateManager.TryAddStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) is used to register a custom serializer for the given type T. This registration should happen in the construction of the StatefulServiceBase to ensure that before recovery starts, all Reliable Collections have access to the relevant serializer to read their persisted data.</span></span>

```C#
public StatefulBackendService(StatefulServiceContext context)
  : base(context)
  {
    if (!this.StateManager.TryAddStateSerializer(new OrderKeySerializer()))
    {
      throw new InvalidOperationException("Failed to set OrderKey custom serializer");
    }
  }
```

> [!NOTE]
> <span data-ttu-id="2e906-133">Les sérialiseurs personnalisés prévalent sur les sérialiseurs intégrés.</span><span class="sxs-lookup"><span data-stu-id="2e906-133">Custom serializers are given precedence over built-in serializers.</span></span> <span data-ttu-id="2e906-134">Par exemple, lorsqu’un sérialiseur personnalisé est inscrit pour int, il est utilisé pour sérialiser des entiers au lieu du sérialiseur intégré du type int.</span><span class="sxs-lookup"><span data-stu-id="2e906-134">For example, when a custom serializer for int is registered, it is used to serialize integers instead of the built-in serializer for int.</span></span>

### <a name="how-to-implement-a-custom-serializer"></a><span data-ttu-id="2e906-135">Comment implémenter un sérialiseur personnalisé</span><span class="sxs-lookup"><span data-stu-id="2e906-135">How to implement a custom serializer</span></span>

<span data-ttu-id="2e906-136">Un sérialiseur personnalisé doit implémenter l’interface [IStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1).</span><span class="sxs-lookup"><span data-stu-id="2e906-136">A custom serializer needs to implement the [IStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.</span></span>

> [!NOTE]
> <span data-ttu-id="2e906-137">IStateSerializer<T> inclut une surcharge d’écriture et de lecture qui prend une valeur de base T supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="2e906-137">IStateSerializer<T> includes an overload for Write and Read that takes in an additional T called base value.</span></span> <span data-ttu-id="2e906-138">Cette API s’applique à la sérialisation différentielle.</span><span class="sxs-lookup"><span data-stu-id="2e906-138">This API is for differential serialization.</span></span> <span data-ttu-id="2e906-139">La fonctionnalité de sérialisation différentielle n’est pas exposée pour le moment.</span><span class="sxs-lookup"><span data-stu-id="2e906-139">Currently differential serialization feature is not exposed.</span></span> <span data-ttu-id="2e906-140">Par conséquent, ces deux surcharges ne sont pas appelées tant que la sérialisation différentielle n’est pas exposée et activée.</span><span class="sxs-lookup"><span data-stu-id="2e906-140">Hence, these two overloads are not called until differential serialization is exposed and enabled.</span></span>

<span data-ttu-id="2e906-141">Voici un exemple de type personnalisé appelé OrderKey qui contient quatre propriétés</span><span class="sxs-lookup"><span data-stu-id="2e906-141">Following is an example custom type called OrderKey that contains four properties</span></span>

```C#
public class OrderKey : IComparable<OrderKey>, IEquatable<OrderKey>
{
    public byte Warehouse { get; set; }

    public short District { get; set; }

    public int Customer { get; set; }

    public long Order { get; set; }

    #region Object Overrides for GetHashCode, CompareTo and Equals
    #endregion
}
```

<span data-ttu-id="2e906-142">Voici un exemple d’implémentation de IStateSerializer<OrderKey>.</span><span class="sxs-lookup"><span data-stu-id="2e906-142">Following is an example implementation of IStateSerializer<OrderKey>.</span></span>
<span data-ttu-id="2e906-143">Notez que les surcharges de lecture et d’écriture qui prennent la valeur de base (baseValue) appellent leur surcharge respective pour assurer la compatibilité en aval.</span><span class="sxs-lookup"><span data-stu-id="2e906-143">Note that Read and Write overloads that take in baseValue, call their respective overload for forwards compatibility.</span></span>

```C#
public class OrderKeySerializer : IStateSerializer<OrderKey>
{
  OrderKey IStateSerializer<OrderKey>.Read(BinaryReader reader)
  {
      var value = new OrderKey();
      value.Warehouse = reader.ReadByte();
      value.District = reader.ReadInt16();
      value.Customer = reader.ReadInt32();
      value.Order = reader.ReadInt64();

      return value;
  }

  void IStateSerializer<OrderKey>.Write(OrderKey value, BinaryWriter writer)
  {
      writer.Write(value.Warehouse);
      writer.Write(value.District);
      writer.Write(value.Customer);
      writer.Write(value.Order);
  }
  
  // Read overload for differential de-serialization
  OrderKey IStateSerializer<OrderKey>.Read(OrderKey baseValue, BinaryReader reader)
  {
      return ((IStateSerializer<OrderKey>)this).Read(reader);
  }

  // Write overload for differential serialization
  void IStateSerializer<OrderKey>.Write(OrderKey baseValue, OrderKey newValue, BinaryWriter writer)
  {
      ((IStateSerializer<OrderKey>)this).Write(newValue, writer);
  }
}
```

## <a name="upgradability"></a><span data-ttu-id="2e906-144">Mise à niveau</span><span class="sxs-lookup"><span data-stu-id="2e906-144">Upgradability</span></span>
<span data-ttu-id="2e906-145">Dans un [mise à niveau d'application propagée](service-fabric-application-upgrade.md), la mise à niveau est appliquée à un sous-ensemble de nœuds, à raison d'un domaine de mise à niveau à la fois.</span><span class="sxs-lookup"><span data-stu-id="2e906-145">In a [rolling application upgrade](service-fabric-application-upgrade.md), the upgrade is applied to a subset of nodes, one upgrade domain at a time.</span></span> <span data-ttu-id="2e906-146">Pendant ce processus, certains domaines de mise à niveau se trouvent sur la version la plus récente de votre application, tandis que d'autres se trouvent sur la version antérieure.</span><span class="sxs-lookup"><span data-stu-id="2e906-146">During this process, some upgrade domains will be on the newer version of your application, and some upgrade domains will be on the older version of your application.</span></span> <span data-ttu-id="2e906-147">Pendant le déploiement, la nouvelle version de votre application doit être en mesure de lire l’ancienne version de vos données, tandis que l’ancienne version de votre application doit être à même de lire la nouvelle version de vos données.</span><span class="sxs-lookup"><span data-stu-id="2e906-147">During the rollout, the new version of your application must be able to read the old version of your data, and the old version of your application must be able to read the new version of your data.</span></span> <span data-ttu-id="2e906-148">Si le format de données n’offre pas une compatibilité ascendante et descendante, la mise à niveau peut échouer ou, pire, des données peuvent être perdues ou endommagées.</span><span class="sxs-lookup"><span data-stu-id="2e906-148">If the data format is not forward and backward compatible, the upgrade may fail, or worse, data may be lost or corrupted.</span></span>

<span data-ttu-id="2e906-149">Si vous utilisez le sérialiseur intégré, vous n’avez pas à vous soucier de la compatibilité.</span><span class="sxs-lookup"><span data-stu-id="2e906-149">If you are using  built-in serializer, you do not have to worry about compatibility.</span></span>
<span data-ttu-id="2e906-150">Si toutefois vous utilisez un sérialiseur personnalisé ou le DataContractSerializer, les données doivent être indéfiniment compatibles en amont et en aval.</span><span class="sxs-lookup"><span data-stu-id="2e906-150">However, if you are using a custom serializer or the DataContractSerializer, the data have to be infinitely backwards and forwards compatible.</span></span>
<span data-ttu-id="2e906-151">En d’autres termes, chaque version du sérialiseur doit être en mesure de sérialiser et désérialiser n’importe quelle version du type.</span><span class="sxs-lookup"><span data-stu-id="2e906-151">In other words, each version of serializer needs to be able to serialize and de-serialize any version of the type.</span></span>

<span data-ttu-id="2e906-152">Les utilisateurs du contrat de données doivent suivre des règles de version bien définies pour l’ajout, la suppression et la modification de champs.</span><span class="sxs-lookup"><span data-stu-id="2e906-152">Data Contract users should follow the well-defined versioning rules for adding, removing, and changing fields.</span></span> <span data-ttu-id="2e906-153">En outre, le contrat de données prend en charge les champs inconnus, avec raccordement au processus de sérialisation et de désérialisation, ainsi que l’héritage de classe.</span><span class="sxs-lookup"><span data-stu-id="2e906-153">Data Contract also has support for dealing with unknown fields, hooking into the serialization and deserialization process, and dealing with class inheritance.</span></span> <span data-ttu-id="2e906-154">Pour plus d'informations, consultez la page [Utilisation du contrat de données](https://msdn.microsoft.com/library/ms733127.aspx).</span><span class="sxs-lookup"><span data-stu-id="2e906-154">For more information, see [Using Data Contract](https://msdn.microsoft.com/library/ms733127.aspx).</span></span>

<span data-ttu-id="2e906-155">Les utilisateurs de sérialiseurs personnalisés doivent respecter les instructions du sérialiseur qu’ils utilisent afin de s’assurer de sa compatibilité en amont et en aval.</span><span class="sxs-lookup"><span data-stu-id="2e906-155">Custom serializer users should adhere to the guidelines of the serializer they are using to make sure it is backwards and forwards compatible.</span></span>
<span data-ttu-id="2e906-156">Une façon courante de prendre en charge toutes les versions consiste à ajouter au début des informations sur la taille et à ajouter uniquement les propriétés facultatives.</span><span class="sxs-lookup"><span data-stu-id="2e906-156">Common way of supporting all versions is adding size information at the beginning and only adding optional properties.</span></span>
<span data-ttu-id="2e906-157">Chaque version peut ainsi lire un maximum d’informations et passer à la dernière partie du flux de données.</span><span class="sxs-lookup"><span data-stu-id="2e906-157">This way each version can read as much it can and jump over the remaining part of the stream.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e906-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2e906-158">Next steps</span></span>
  * [<span data-ttu-id="2e906-159">Sérialisation et mise à niveau</span><span class="sxs-lookup"><span data-stu-id="2e906-159">Serialization and upgrade</span></span>](service-fabric-application-upgrade-data-serialization.md)
  * [<span data-ttu-id="2e906-160">Référence du développeur pour les Collections fiables</span><span class="sxs-lookup"><span data-stu-id="2e906-160">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * <span data-ttu-id="2e906-161">[mise à niveau de votre application à l’aide de Visual Studio](service-fabric-application-upgrade-tutorial.md) vous guide à travers une mise à niveau de l’application à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2e906-161">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>
  * <span data-ttu-id="2e906-162">[mise à niveau de votre application à l’aide de PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) vous guide à travers une mise à niveau de l’application à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2e906-162">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>
  * <span data-ttu-id="2e906-163">Contrôlez les mises à niveau de votre application à l'aide des [Paramètres de mise à niveau](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="2e906-163">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>
  * <span data-ttu-id="2e906-164">Apprenez à utiliser les fonctionnalités avancées lors de la mise à niveau de votre application en consultant les [Rubriques avancées](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="2e906-164">Learn how to use advanced functionality while upgrading your application by referring to [Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
  * <span data-ttu-id="2e906-165">Résolvez les problèmes courants de mise à niveau de l’application en vous reportant aux étapes de [Résolution des problèmes de mise à niveau des applications](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="2e906-165">Fix common problems in application upgrades by referring to the steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
