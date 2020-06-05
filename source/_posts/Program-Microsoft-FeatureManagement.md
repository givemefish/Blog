---
title: Microsoft.FeatureManagement
date: 2020-06-05 14:25:57
tags: dotnetcore
---
在開發程式時難免會碰到需要針對完成度, 決定是否開發某個功能的狀況
如果在程式碼中放入一堆if-else條件, 很容易影響程式碼的可閱讀性

在.Net core中, 微軟提供了套件```Microsoft.FeatureMangement.AspNetCore```, 可以從nuget下載

使用方法
1. 在startup.cs中新增如下
   ```
   public void ConfigureServices(IServiceCollection services)
   {
      services.AddControllersWithViews();  
      services.AddFeatureManagement();
   }
   ```
2. 在appsetings.json中新增feature名字
   ```
   {
    "Logging": {
      "LogLevel": {
        "Default": "Information",
        "Microsoft": "Warning",
        "Microsoft.Hosting.Lifetime": "Information"
      }
    },
    "AllowedHosts": "*",
    "FeatureManagement": {
      "Export": true   
    }  
   ```
3. 在controller中以DI引入IFeatureManager, 就可以透過FeatureManager的IsEnableAsync來得知相關功能是否已被設定開啟   
   ```
    private readonly IFeatureManager _featureManager; 
	
	public HomeController(IFeatureManager featureManager)
	{
		_featureManager = featureManager;
	}
	
	public async Task<IActionResult> Index()
	{
		if (await _featureManager.IsEnabledAsync("Export"))
		{
			// do something
		}      
		
		return View();
	}
   ```
4. 可以在Action或Controller上加上FeatureGateAttribute來決定是否啟用某功能, 如果沒有啟用的話, server會回傳404錯誤
    ```
    [FeatureGate("Export")]
    public IActionResult Export()
    {
      return View();
    }
    ```
5. 如果要在View中根據Feature是否開啟來動態決定是否顯示或隱藏某些UI元件, 可以在_ViewImports.cshtml中加入
   ```
   @addTagHelper *, Microsoft.FeatureManagement.AspNetCore
   ```
   然後我們就可以在view中用```<feature name="Export">```的方式動態顯示UI元件   