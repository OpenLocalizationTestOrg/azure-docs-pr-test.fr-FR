---
title: "Créer une alerte de mesure avec un modèle Resource Manager | Microsoft Docs"
description: "Découvrez comment utiliser un modèle Resource Manager pour créer une alerte de mesure pour recevoir des notifications par e-mail ou webhook."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 41d62044-6bc5-4674-b277-45b919f58efe
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/21/2017
ms.author: johnkem
ms.openlocfilehash: ac12605636d21fd0b5c89512c454ef2d899ef6dc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-metric-alert-with-a-resource-manager-template"></a><span data-ttu-id="0402e-103">Créer une alerte de mesure avec un modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0402e-103">Create a metric alert with a Resource Manager template</span></span>
<span data-ttu-id="0402e-104">Cet article explique comment vous pouvez utiliser un [modèle Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) pour configurer les alertes de mesures Azure.</span><span class="sxs-lookup"><span data-stu-id="0402e-104">This article shows how you can use an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) to configure Azure metric alerts.</span></span> <span data-ttu-id="0402e-105">Cela vous permet de configurer automatiquement des alertes sur vos ressources lorsqu’elles sont créées pour vous assurer que toutes les ressources sont analysées correctement.</span><span class="sxs-lookup"><span data-stu-id="0402e-105">This enables you to automatically set up alerts on your resources when they are created to ensure that all resources are monitored correctly.</span></span>

<span data-ttu-id="0402e-106">Procédure de base :</span><span class="sxs-lookup"><span data-stu-id="0402e-106">The basic steps are as follows:</span></span>

1. <span data-ttu-id="0402e-107">Créez un modèle sous la forme d’un fichier JSON qui décrit comment créer l’alerte.</span><span class="sxs-lookup"><span data-stu-id="0402e-107">Create a template as a JSON file that describes how to create the alert.</span></span>
2. <span data-ttu-id="0402e-108">[Déployez le modèle à l’aide de n’importe quelle méthode de déploiement](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="0402e-108">[Deploy the template using any deployment method](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

<span data-ttu-id="0402e-109">Ci-dessous, nous décrivons comment créer un modèle Resource Manager, d’abord pour une alerte uniquement, puis pour une alerte lors de la création d’une autre ressource.</span><span class="sxs-lookup"><span data-stu-id="0402e-109">Below we describe how to create a Resource Manager template first for an alert alone, then for an alert during the creation of another resource.</span></span>

## <a name="resource-manager-template-for-a-metric-alert"></a><span data-ttu-id="0402e-110">Modèle Resource Manager pour une alerte de mesure</span><span class="sxs-lookup"><span data-stu-id="0402e-110">Resource Manager template for a metric alert</span></span>
<span data-ttu-id="0402e-111">Pour créer une alerte à l’aide d’un modèle Resource Manager, vous créez une ressource de type `Microsoft.Insights/alertRules` et renseignez toutes les propriétés.</span><span class="sxs-lookup"><span data-stu-id="0402e-111">To create an alert using a Resource Manager template, you create a resource of type `Microsoft.Insights/alertRules` and fill in all related properties.</span></span> <span data-ttu-id="0402e-112">Voici un modèle qui crée une règle d’alerte.</span><span class="sxs-lookup"><span data-stu-id="0402e-112">Below is a template that creates an alert rule.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "alertName": {
            "type": "string",
            "metadata": {
                "description": "Name of alert"
            }
        },
        "alertDescription": {
            "type": "string",
            "defaultValue": "",
            "metadata": {
                "description": "Description of alert"
            }
        },
        "isEnabled": {
            "type": "bool",
            "defaultValue": true,
            "metadata": {
                "description": "Specifies whether alerts are enabled"
            }
        },
        "resourceId": {
            "type": "string",
            "defaultValue": "",
            "metadata": {
                "description": "Resource ID of the resource emitting the metric that will be used for the comparison."
            }
        },
        "metricName": {
            "type": "string",
            "defaultValue": "",
            "metadata": {
                "description": "Name of the metric used in the comparison to activate the alert."
            }
        },
        "operator": {
            "type": "string",
            "defaultValue": "GreaterThan",
            "allowedValues": [
                "GreaterThan",
                "GreaterThanOrEqual",
                "LessThan",
                "LessThanOrEqual"
            ],
            "metadata": {
                "description": "Operator comparing the current value with the threshold value."
            }
        },
        "threshold": {
            "type": "string",
            "defaultValue": "",
            "metadata": {
                "description": "The threshold value at which the alert is activated."
            }
        },
        "aggregation": {
            "type": "string",
            "defaultValue": "Average",
            "allowedValues": [
                "Average",
                "Last",
                "Maximum",
                "Minimum",
                "Total"
            ],
            "metadata": {
                "description": "How the data that is collected should be combined over time."
            }
        },
        "windowSize": {
            "type": "string",
            "defaultValue": "PT5M",
            "metadata": {
                "description": "Period of time used to monitor alert activity based on the threshold. Must be between five minutes and one day. ISO 8601 duration format."
            }
        },
        "sendToServiceOwners": {
            "type": "bool",
            "defaultValue": true,
            "metadata": {
                "description": "Specifies whether alerts are sent to service owners"
            }
        },
        "customEmailAddresses": {
            "type": "string",
            "defaultValue": "",
            "metadata": {
                "description": "Comma-delimited email addresses where the alerts are also sent"
            }
        },
        "webhookUrl": {
            "type": "string",
            "defaultValue": "",
            "metadata": {
                "description": "URL of a webhook that will receive an HTTP POST when the alert activates."
            }
        }
    },
    "variables": {
        "customEmails": "[split(parameters('customEmailAddresses'), ',')]"
    },
    "resources": [
        {
            "type": "Microsoft.Insights/alertRules",
            "name": "[parameters('alertName')]",
            "location": "[resourceGroup().location]",
            "apiVersion": "2016-03-01",
            "properties": {
                "name": "[parameters('alertName')]",
                "description": "[parameters('alertDescription')]",
                "isEnabled": "[parameters('isEnabled')]",
                "condition": {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
                    "dataSource": {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
                        "resourceUri": "[parameters('resourceId')]",
                        "metricName": "[parameters('metricName')]"
                    },
                    "operator": "[parameters('operator')]",
                    "threshold": "[parameters('threshold')]",
                    "windowSize": "[parameters('windowSize')]",
                    "timeAggregation": "[parameters('aggregation')]"
                },
                "actions": [
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                        "sendToServiceOwners": "[parameters('sendToServiceOwners')]",
                        "customEmails": "[variables('customEmails')]"
                    },
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleWebhookAction",
                        "serviceUri": "[parameters('webhookUrl')]",
                        "properties": {}
                    }
                ]
            }
        }
    ]
}
```

<span data-ttu-id="0402e-113">Une explication du schéma et des propriétés pour une règle d’alerte [est disponible ici](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span><span class="sxs-lookup"><span data-stu-id="0402e-113">An explanation of the schema and properties for an alert rule [is available here](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span></span>

## <a name="resource-manager-template-for-a-resource-with-an-alert"></a><span data-ttu-id="0402e-114">Modèle Resource Manager pour une ressource avec une alerte</span><span class="sxs-lookup"><span data-stu-id="0402e-114">Resource Manager template for a resource with an alert</span></span>
<span data-ttu-id="0402e-115">Une alerte sur un modèle Resource Manager est le plus souvent utile lors de la création d’une alerte pendant la création d’une ressource.</span><span class="sxs-lookup"><span data-stu-id="0402e-115">An alert on a Resource Manager template is most often useful when creating an alert while creating a resource.</span></span> <span data-ttu-id="0402e-116">Par exemple, vous pourriez souhaiter vous assurer qu’une règle « processeur > 80 % » est définie chaque fois que vous déployez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0402e-116">For example, you may want to ensure that a “CPU % > 80” rule is set up every time you deploy a Virtual Machine.</span></span> <span data-ttu-id="0402e-117">Pour ce faire, vous ajoutez la règle d’alerte en tant que ressource dans le tableau des ressources pour votre modèle de machine virtuelle et ajoutez une dépendance à l’aide de la propriété `dependsOn` de l’ID de ressource de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0402e-117">To do this, you add the alert rule as a resource in the resource array for your VM template and add a dependency using the `dependsOn` property to the VM resource ID.</span></span> <span data-ttu-id="0402e-118">Voici un exemple complet qui crée une machine virtuelle Windows et ajoute une alerte qui avertit les administrateurs d’abonnement lorsque l’utilisation du processeur dépasse 80 %.</span><span class="sxs-lookup"><span data-stu-id="0402e-118">Here’s a full example that creates a Windows VM and adds an alert that notifies subscription admins when the CPU utilization goes above 80%.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "newStorageAccountName": {
            "type": "string",
            "metadata": {
                "Description": "The name of the storage account where the VM disk is stored."
            }
        },
        "adminUsername": {
            "type": "string",
            "metadata": {
                "Description": "The name of the administrator account on the VM."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "Description": "The administrator account password on the VM."
            }
        },
        "dnsNameForPublicIP": {
            "type": "string",
            "metadata": {
                "Description": "The name of the public IP address used to access the VM."
            }
        }
    },
    "variables": {
        "location": "Central US",
        "imagePublisher": "MicrosoftWindowsServer",
        "imageOffer": "WindowsServer",
        "windowsOSVersion": "2012-R2-Datacenter",
        "OSDiskName": "osdisk1",
        "nicName": "nc1",
        "addressPrefix": "10.0.0.0/16",
        "subnetName": "sn1",
        "subnetPrefix": "10.0.0.0/24",
        "storageAccountType": "Standard_LRS",
        "publicIPAddressName": "ip1",
        "publicIPAddressType": "Dynamic",
        "vmStorageAccountContainerName": "vhds",
        "vmName": "vm1",
        "vmSize": "Standard_A0",
        "virtualNetworkName": "vn1",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]",
        "vmID":"[resourceId('Microsoft.Compute/virtualMachines',variables('vmName'))]",
        "alertName": "highCPUOnVM",
        "alertDescription":"CPU is over 80%",
        "alertIsEnabled": true,
        "resourceId": "",
        "metricName": "Percentage CPU",
        "operator": "GreaterThan",
        "threshold": "80",
        "windowSize": "PT5M",
        "aggregation": "Average",
        "customEmails": "",
        "sendToServiceOwners": true,
        "webhookUrl": "http://testwebhook.test"
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('newStorageAccountName')]",
            "apiVersion": "2015-06-15",
            "location": "[variables('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Network/publicIPAddresses",
            "name": "[variables('publicIPAddressName')]",
            "location": "[variables('location')]",
            "properties": {
                "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
                "dnsSettings": {
                    "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
                }
            }
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Network/virtualNetworks",
            "name": "[variables('virtualNetworkName')]",
            "location": "[variables('location')]",
            "properties": {
                "addressSpace": {
                    "addressPrefixes": [
                        "[variables('addressPrefix')]"
                    ]
                },
                "subnets": [
                    {
                        "name": "[variables('subnetName')]",
                        "properties": {
                            "addressPrefix": "[variables('subnetPrefix')]"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Network/networkInterfaces",
            "name": "[variables('nicName')]",
            "location": "[variables('location')]",
            "dependsOn": [
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
                "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
            ],
            "properties": {
                "ipConfigurations": [
                    {
                        "name": "ipconfig1",
                        "properties": {
                            "privateIPAllocationMethod": "Dynamic",
                            "publicIPAddress": {
                                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
                            },
                            "subnet": {
                                "id": "[variables('subnetRef')]"
                            }
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Compute/virtualMachines",
            "name": "[variables('vmName')]",
            "location": "[variables('location')]",
            "dependsOn": [
                "[concat('Microsoft.Storage/storageAccounts/', parameters('newStorageAccountName'))]",
                "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
            ],
            "properties": {
                "hardwareProfile": {
                    "vmSize": "[variables('vmSize')]"
                },
                "osProfile": {
                    "computername": "[variables('vmName')]",
                    "adminUsername": "[parameters('adminUsername')]",
                    "adminPassword": "[parameters('adminPassword')]"
                },
                "storageProfile": {
                    "imageReference": {
                        "publisher": "[variables('imagePublisher')]",
                        "offer": "[variables('imageOffer')]",
                        "sku": "[variables('windowsOSVersion')]",
                        "version": "latest"
                    },
                    "osDisk": {
                        "name": "osdisk",
                        "vhd": {
                            "uri": "[concat('http://',parameters('newStorageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
                        },
                        "caching": "ReadWrite",
                        "createOption": "FromImage"
                    }
                },
                "networkProfile": {
                    "networkInterfaces": [
                        {
                            "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
                        }
                    ]
                }
            }
        },
        {
            "type": "Microsoft.Insights/alertRules",
            "name": "[variables('alertName')]",
            "dependsOn": [
                "[variables('vmID')]"
            ],
            "location": "[variables('location')]",
            "apiVersion": "2016-03-01",
            "properties": {
                "name": "[variables('alertName')]",
                "description": "variables('alertDescription')",
                "isEnabled": "[variables('alertIsEnabled')]",
                "condition": {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
                    "dataSource": {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
                        "resourceUri": "[variables('vmID')]",
                        "metricName": "[variables('metricName')]"
                    },
                    "operator": "[variables('operator')]",
                    "threshold": "[variables('threshold')]",
                    "windowSize": "[variables('windowSize')]",
                    "timeAggregation": "[variables('aggregation')]"
                },
                "actions": [
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                        "sendToServiceOwners": "[variables('sendToServiceOwners')]",
                        "customEmails": "[variables('customEmails')]"
                    },
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleWebhookAction",
                        "serviceUri": "[variables('webhookUrl')]",
                        "properties": {}
                    }
                ]
            }
        }
    ]
}
```

## <a name="next-steps"></a><span data-ttu-id="0402e-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0402e-119">Next Steps</span></span>
* [<span data-ttu-id="0402e-120">En savoir plus sur les alertes</span><span class="sxs-lookup"><span data-stu-id="0402e-120">Read more about Alerts</span></span>](insights-receive-alert-notifications.md)
* <span data-ttu-id="0402e-121">[Ajout de paramètres de diagnostic](monitoring-enable-diagnostic-logs-using-template.md) à votre modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0402e-121">[Add Diagnostic Settings](monitoring-enable-diagnostic-logs-using-template.md) to your Resource Manager template</span></span>

