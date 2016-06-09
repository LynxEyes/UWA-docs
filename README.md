
## Agnostic
1. [Windows Universal Platform apps samples - in all languages](https://github.com/Microsoft/Windows-universal-samples)

## C&sharp;
1. [Building Accessible UWP Apps](https://www.youtube.com/watch?v=_tvBQsxpEG4)
2. [Developing Windows 10 Universal Apps course - Part 1](https://www.edx.org/course/developing-windows-10-universal-apps-microsoft-dev209-1x-0)
3. [Developing Windows 10 Universal Apps course - Part 2](https://www.edx.org/course/developing-windows-10-universal-apps-microsoft-dev209-2x-0)
4. [Template10 - bootstrap for c# uwp apps](https://github.com/Windows-XAML/Template10)
4. [How to unit test a Windows 10 app in Visual Studio?](https://xunit.github.io/docs/getting-started-uwp.html)
5. [C# 6 features that help you write cleaner code](http://programmingwithmosh.com/csharp/csharp-6-features-that-help-you-write-cleaner-code/)

### SQLite for Universal Windows Platform

In order to use SQLite on a Universal Windows Platform, you need to install a VS specific extension:

![Pic](/VS-SQLite_for_UWP.png)

### Appium - Windows App Driver

Appium is a tool to perform automated UI tests. In order to use it you need to install the tool. Please visit: [WinAppDriver](https://github.com/Microsoft/WinAppDriver)

You can obtain the installer itself [here](http://download.microsoft.com/download/6/8/7/687DEE85-E907-4A95-8035-8BC969B9EA95/WindowsApplicationDriver.msi)

### Getting The APP ID to use with Appium (Windows App Driver)

Get the `Package family name` from the Package.appxmanifest > Packaging tab

![Pic](/GettingTheAppID.png)

```c#
DesiredCapabilities appCapabilities = new DesiredCapabilities();
appCapabilities.SetCapability("app", "cf59c34d-6a44-4b82-9029-ad2fc3cc2611_xnnwpqakf2yqj!App");
```


### Problems with the C&sharp; + XAML approach

* CodedUI tests are Premium! [Stack Overflow thread](http://stackoverflow.com/questions/7106251/microsoft-visualstudio-testtools-uitest-dll)
* Also, check **Testing Tools** on the [Official Visual Studio page](https://www.visualstudio.com/en-us/products/compare-visual-studio-2015-products-vs.aspx)

## VisualStudio TroubleShooting

When debugging tests in apps using Template10, the following error <s>will</s> may occur:

![Pic](/AnotherDayWithVisualStudio.png)

In that case, follow VS suggestion and click in the link `Get general help for this exception.`
There you will find instructions to turn off the Just My Code debugging option.

### Unable to run UnitTests

There seems to be some issues between Template10 and MVVMLight that might cause tests not to run while yielding something like:

```
A user callback threw an exception.  Check the exception stack and inner exception to determine the callback that failed.
```

Looking at [this github issue comment](https://github.com/Windows-XAML/Template10/issues/464#issuecomment-210038007) the solution is to add the `[Bindable]` annotation to the `Locator` class.

### Disabling parallel test execution

Tests via Appium cannot be ran in parallel (WinAppDriver will fail to create sessions).
xUnit runs tests in parallel by default, so its necessary to [configure the xUnit runner](http://xunit.github.io/docs/configuring-with-xml)

To stop tests from running in parallel, just create a `App.config` file on the UI tests project with:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <appSettings>
    <add key="xunit.parallelizeTestCollections" value="false"/>
  </appSettings>
</configuration>
```

### Problems handling ENTER key with KeyDown on a TextBox

It seems that ENTER triggers 2 events! This is a known bug by Microsoft since 2013 and still they did nothing to correct: 
- [This thread on SO](http://stackoverflow.com/questions/11372969/c-sharp-textbox-keydown-triggered-twice-in-metro-applications)
- [This thread on MSDN](https://social.msdn.microsoft.com/Forums/en-US/734d6c7a-8da2-48c6-9b3d-fa868b4dfb1d/c-textbox-keydown-triggered-twice-in-metro-applications?forum=winappswithcsharp)
