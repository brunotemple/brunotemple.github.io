---
layout: post
title: Model binding to a list (complex)
categories: [C# MVC Fundamentals]
tags: [C# MVC ASP.Net Complex View]
---

### Passing a complex list to a view.

Recently I had to deal with a necessity to passing a complex list to a view.

Everyone knows that ASP.Net MVC is able to bind values being these arguments that can be used in an action method in the controller. However, when you have a complex list isn’t so simple.

Let’s suppose that you have a model as below:

```C#
Public class APP_SETTINGS {
	public int UID { get; set; }
	public string setting_Description { get; set; }
	public string setting_ValidationType { get; set; }
	public string setting_Value { get; set; }
}
```

// Action on Controller

```C#
Public ActionResult Index(){
IEnumerable<APP_SETTINGS> app_settings = db.APP_SETTINGS.ToList();

return View(app_settings);
}
```

The resulted view using DefaultModelBinder will show you the view with any problem. However, it doesn’t solve my problem. I want to be able to update every “setting_value” at the same time in my post action.

So, how to solve the problem?

The first option I’ve found on the internet as you can see below:

```cshtml
@model IList<AIS_Application.Models.APP_SETTINGS>
@{
    ViewBag.Title = "Index";
}

@for (int i = 0; i < Model.Count; i++){ 
	<div>
		@Html.DisplayFor(model => Model[i].setting_Description)
		@Html.DisplayFor(modelItem => Model[i].setting_ValidationType)
		@Html.EditorFor(modelItem => Model[i].setting_Value)
	</div>         
}
```

This code works. It’s simple and can be helpful.
Although this code works and, it’s simple to implement, I wasn’t happy with it.

So, I keep trying to find a solution that would be a little bit more elegant, and that’s when I used “editor template”.
Editor Template is an HTML helpers that allow you for editing types of data. In this case, I’m using complex types, but can be used for simple one. Also, it is quite easy to using.

I’ve just created a new folder inside the folder where is located my view. I called this folder “EditorTemplate”, inside this folder, I added a view “APP_SETTINGS.cshtml”.

I changed the code in the previous view “index.cshtml” as below:

```cshtml
@model IList<AIS_Application.Models.APP_SETTINGS>
@{
    ViewBag.Title = "APP Settings";
}
@using (Html.BeginForm()) {
    @Html.AntiForgeryToken()
    @Html.ValidationSummary(true)

    <div>
        <div>
            <div>
                @Html.DisplayName("Description")
            </div>
            <div>
                @Html.DisplayName("Value")
            </div>
        </div>
            @Html.EditorForModel()
    </div>
}
```

And the APP_SETTINGS.cshtml:

```cshml
@model AIS_Application.Models.APP_SETTINGS

@Html.HiddenFor(model => model.UID)
<div>
    <div>
        @Html.DisplayFor(model => model.setting_Description)
    </div>
    @if (Model.setting_ValidationType != "bool")
    {
        <div>
            @Html.EditorFor(model => model.setting_Value)
            @Html.ValidationMessageFor(model => model.setting_Value)
        </div>
    }
    else
    {
        <div>
		@Html.DropDownListFor(model => model.setting_Value, new SelectList(new List<Object>{
                new { Text = "True", Value = "True" },
                new { Text = "False", Value = "False" }
                },"Value","Text",Model.setting_Value))
        </div>
    }
</div>
```
Using Editor Template works for me in this case. I can now edit and save all settings of my application using the index view.

Hope that this post can be useful to you.

Cheers

Until next time.





