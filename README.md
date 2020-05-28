# BlakeOnLan
A 100-line [Wake-on-LAN](https://en.wikipedia.org/wiki/Wake-on-LAN) app using Blazor Server to wake your devices remotely on your home network.

## Prerequisites
- .NET Core 3.1

## How to use
1. Clone the repo
2. `dotnet run` (or using Visual Studio: `F5`)
3. Add your home devices you want to use with Wake-on-LAN, provide a unique name as desired (e.g: Living Room PC) and enter the MAC address of the device (only hexadecimal characters, but field is copy-pastable). The list of devices are saved to the local storage of the browser.
4. Click the Wake button to send a standard UDP Magic packet to wake the device (only works if the device/motherboard supports Wake-on-LAN)
+1. The app can be installed as a PWA, so you can pin it to your Start Menu or Taskbar. The server needs to run though (as UDP requests are not possible from the browser.

## Remarks
- I use Remote Desktop in the house to RDP onto our HTPC in the living room, but sometimes the TV is already in use. If the device is not awake, I have to go over and power it on. Lazyness prevails, as from now I don't have to go over, just push the Wake button on this app :)
- I wanted to make the source as small as possible, and managed to only need two files in total (plus the .csproj file): the `Pages\_Host.cshtml` (22 lines) for hosting the Blazor Server app, and an `App.razor` file (78 lines), which contains the only component of the app, for a grand total of exactly <b>100 lines of source code</b>! This was just a fun experiment to see how much boilerplate could be omitted. No `wwwroot`, `Program.cs` (the `App.razor` contains the `Main` method) or `Startup.cs` (the services and pipeline are configured inline in the `Main` method)!
	- If you have an idea how to replace the `_Host.cshtml` file with a direct, inline response from the `Main` method, don't hesitate to send me a PR! If it keeps the App.razor total line number at or under 100 lines, it's even better! I messed around for a while with the [`FallbackEndpointRouteBuilderExtensions.MapFallback`](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.fallbackendpointroutebuilderextensions.mapfallback?view=aspnetcore-3.1) extension method, but I couldn't dynamically invoke the [`Microsoft.AspNetCore.Mvc.TagHelpers.ComponentTagHelper`](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.taghelpers.componenttaghelper?view=aspnetcore-3.1). It *is* possible, but to me it seemed extremely cumbersome (needing to DI/instantiante an ActionContext, ViewContext, lots of helpers for TagHelper rendering etc.). Maybe there is a workaround to instantiate a Blazor circuit without needing to use the TagHelper (it outputs nothing anyways), but a got lost deep in the ASP.NET Core source when looking this up. If you're up for it, I got to [here](https://github.com/dotnet/aspnetcore/blob/master/src/Mvc/Mvc.ViewFeatures/src/RazorComponents/ComponentRenderer.cs#L102) while investigating.
- Thanks to [@chrissainty](https://github.com/chrissainty) for the [Blazored.LocalStorage](https://github.com/Blazored/LocalStorage) package!
- I hope this little proof-of-concept app can further prove that Blazor is the future!

<b>Thanks for reading, keep on Blazin'!</b>