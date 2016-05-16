
#Agnostic
1. [Windows Universal Platform apps samples - in all languages](https://github.com/Microsoft/Windows-universal-samples)

#Csharp
1. [Building Accessible UWP Apps](https://www.youtube.com/watch?v=_tvBQsxpEG4)
2. [Developing Windows 10 Universal Apps course - Part 1](https://www.edx.org/course/developing-windows-10-universal-apps-microsoft-dev209-1x-0)
3. [Developing Windows 10 Universal Apps course - Part 2](https://www.edx.org/course/developing-windows-10-universal-apps-microsoft-dev209-2x-0)
4. [Template10 - bootstrap for c# uwp apps](https://github.com/Windows-XAML/Template10)
4. [How to unit test a Windows 10 app in Visual Studio?](https://xunit.github.io/docs/getting-started-uwp.html)
5. [C# 6 features that help you write cleaner code](http://programmingwithmosh.com/csharp/csharp-6-features-that-help-you-write-cleaner-code/)

## Getting The APP ID to use with Appium (Windows App Driver)

Get the `Package family name` from the Package.appxmanifest > Packaging tab

![Pic](/GettingTheAppID.png)

```c#
DesiredCapabilities appCapabilities = new DesiredCapabilities();
appCapabilities.SetCapability("app", "cf59c34d-6a44-4b82-9029-ad2fc3cc2611_xnnwpqakf2yqj!App");
```


## Why we cannot use Csharp

Because CodedUI tests are Premium! [Stack Overflow thread](http://stackoverflow.com/questions/7106251/microsoft-visualstudio-testtools-uitest-dll)

Also, check **Testing Tools** on the [Official Visual Studio page](https://www.visualstudio.com/en-us/products/compare-visual-studio-2015-products-vs.aspx)

#JS
1. [WinJS github](https://github.com/winjs/winjs)
2. [UWP with WinJS Hello World](https://msdn.microsoft.com/en-us/windows/uwp/get-started/create-a-hello-world-app-js-universal)
1. [UWA with WinJS - Video tutorial](https://mva.microsoft.com/en-us/training-courses/developing-universal-windows-apps-with-html-and-javascript-jump-start-8344?l=WabedTEz_704984382)
2. [angular-winjs - Project to smooth the AngularJS/WinJS interaction](https://github.com/winjs/angular-winjs)

## AngularJS
0. [Style Guide](https://github.com/mgechev/angularjs-style-guide)

##JS testing
1. [unit and UI testing for winjs (and generally js) apps](https://qunitjs.com/) 
2. [Testing WinJS apps with MOCHA](http://staxmanade.com/2015/05/running-in-app-mocha-tests-within-winjs/)
3. [BDD - Pavlov](https://github.com/mmonteleone/pavlov)
4. [UI Test Automation for Browsers and Apps Using the WebDriver Standard](https://channel9.msdn.com/Events/Build/2016/P499)
5. [BDD / TDD assertion library](http://chaijs.com/)

## Why we cannot use chutzpah
0. It runs tests inside phantom js, not injecting Windows.* namespaces ([Chutzpah](https://github.com/mmanela/chutzpah))

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
