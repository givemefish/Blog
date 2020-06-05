---
title: Microsoft.FeatureManagement (Part 2)
date: 2020-06-05 16:29:06
tags: dotnetcore
---
Microsoft FeatureManagement還有提供火eature filter, 可以允許我們提供條件參數來決定該功能是否啟用

內建有提供一些feature filter, 分別是Percentage和Time Window Feature Filter

先來看看Percentage feature filter的用法
1. 首先更改Startup.cs
  ```
  public void ConfigureServices(IServiceCollection services)
  {
    services.AddControllersWithViews(); 
    services.AddFeatureManagement()
            .AddFeatureFilter<PercentageFilter>();
  }
  ```

2. 在appSettings.json設定如下, 可以允許50%的時間Export功能會被啟用
  ```
  {
    "FeatureManagement": {
    "Export": {
      "EnabledFor": [
        {
          "Name": "Microsoft.Percentage",
          "Parameters": {
            "Value": 50
          }
        }
      ]
    }
  }
  ```

下面是Time window feature filter的用法
1. 和上面範例一樣, 先更改Startup.cs
  ```
  public void ConfigureServices(IServiceCollection services)
  {
    services.AddControllersWithViews(); 
    services.AddFeatureManagement()
            .AddFeatureFilter<TimeWindowFilter>();
  }
  ```
2. 在appSettings.json設定如下, 可以允許Export功能會2020/6/1 ~ 2020/7/1這段時間內被啟用
  ```
  {
    "FeatureManagement": {
    "Export": {
      "EnabledFor": [
        {
          "Name": "Microsoft.TimeWindow",
          "Parameters": {
            "Start": "2020-06-01 00:00:00",
            "End": "2020-07-01 00:00:00"
          }
        }
      ]
    }
  }
  ```
3. 上面範例中的Start和End也可以單獨被指定