---
title: Microsoft.FeatureManagement (Part 3)
date: 2020-06-05 17:02:46
tags: dotnetcore
---
在前面的Percentage範例中, 如果我們在同一個畫面中多次顯示同一個Feature的開啟狀態, 會發現有些Export會是Enabled, 有些會是Disabled, 這是因為每次顯示都是獨立的結果.

如果想要在一個Http Request中, 只會有一個共用的feature enabled結果, 我們就要改寫DI引入的方法, 將IFeatureManager改為IFeatureManagerSnapshot, 如下所示

```
private IFeatureManagerSnapshot _featureManager;
 
public HomeController(IFeatureManagerSnapshot featureManager)
{ 
    _featureManager = featureManager;
}
```