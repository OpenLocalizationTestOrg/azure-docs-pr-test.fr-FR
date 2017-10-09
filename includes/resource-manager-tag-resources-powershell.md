La version 3.0 de module de AzureRm.Resources hello inclus des modifications importantes dans l’utilisation de balises. Avant de poursuivre, vérifiez votre version :

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

Si les résultats indiquent la version 3.0 ou version ultérieure, les exemples de hello dans cette rubrique fonctionnent avec votre environnement. Si vous n’avez pas la version 3.0 ou une version ultérieure, vous devez [mettre à jour votre version](/powershell/azureps-cmdlets-docs/) à l’aide de PowerShell Gallery ou de Web Platform Installer avant de consulter cette rubrique.

```powershell
Version
-------
3.5.0
```

toosee hello balises existantes pour un *groupe de ressources*, utilisez :

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

Ce script renvoie hello suivant le format :

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

toosee hello balises existantes pour un *ressource qui comporte un ID de ressource spécifié*, utilisez :

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

Ou, toosee hello balises existantes pour un *ressource qui comporte un groupe de ressources et de nom spécifié*, utilisez :

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

tooget *des groupes de ressources qui ont une balise spécifique*, utilisez :

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

tooget *ressources qui ont une balise spécifique*, utilisez :

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

Chaque fois que vous appliquez des balises tooa ressource ou un groupe de ressources, vous remplacez les balises existantes hello sur cette ressource ou un groupe de ressources. Par conséquent, vous devez utiliser une approche différente selon que hello ressource ou un groupe de ressources a des balises existantes. 

tooadd balises tooa *groupe de ressources sans balises existantes*, utilisez :

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

tooadd balises tooa *groupe de ressources qui comporte des balises existantes*, récupérer les balises existantes hello, ajoutez la balise hello et réappliquer les balises hello :

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

tooadd balises tooa *ressource sans balises existantes*, utilisez :

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

tooadd balises tooa *ressource qui comporte les balises existantes*, utilisez :

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

tooapply toutes les balises à partir d’un groupe tooits ressources, et *ne conserve pas les balises existantes sur des ressources hello*, utilisez hello script suivant :

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

tooapply toutes les balises à partir d’un groupe tooits ressources, et *conserver les balises existantes sur les ressources qui ne sont pas des doublons*, utilisez hello script suivant :

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    if ($g.Tags -ne $null) {
        $resources = Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName 
        foreach ($r in $resources)
        {
            $resourcetags = (Get-AzureRmResource -ResourceId $r.ResourceId).Tags
            foreach ($key in $g.Tags.Keys)
            {
                if ($resourcetags.ContainsKey($key)) { $resourcetags.Remove($key) }
            }
            $resourcetags += $g.Tags
            Set-AzureRmResource -Tag $resourcetags -ResourceId $r.ResourceId -Force
        }
    }
}
```

tooremove toutes les balises, passez à une table de hachage vide :

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



