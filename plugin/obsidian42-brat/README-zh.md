# Beta Reviewers Auto-update Tester
**Beta Reviewers Auto-update Tester** or **BRAT** for short是一个插件，它可以让你更容易地帮助其他开发人员评审和测试他们的插件。

只需将Obsidian插件的GitHub存储库路径添加到测试列表中，现在你就可以检查更新了。更新被下载，插件被重新加载。不再需要创建文件夹，下载文件，复制到正确的地方等等。这个插件为你照顾所有这些。

# 快速使用指南

## 添加测试版插件

1. 从Obsidian的社区插件安装BRAT
2. 获得你想要测试的GitHub存储库的链接。插件开发者可以为你提供这个链接。
-它看起来像:GitMurf/my-plugin或https://github.com/GitMurf/my-plugin
3.打开命令面板并运行命令**BRAT: Add a beta plugin for testing**
4. 使用步骤2中的链接，将其复制到打开的模态中
5. 点击**Add Plugin**——等待几秒钟，BRAT会告诉你发生了什么
6. 在BRAT确认安装后，在设置中进入**Community plugins **选项卡。
7. 刷新插件列表
8. 找到你刚刚安装的测试版插件并启用它。

## 更新测试版插件

-可以通过运行命令**BRAT来使用命令面板更新插件:检查所有beta插件的更新和UPDATE**

-可选的，beta插件可以配置为自动更新时启动Obsidian。这个功能可以在设置中的**Obsidian42- BRAT选项卡中启用。

# 对喜欢阅读的人再做一些解释

你需要的第一件事是GitHub存储库路径的测试版插件。这听起来比实际要复杂得多。插件是使用GitHub开发的。每个开发者在GitHub上都有自己的账户，并为他们的插件创建一个独特的存储库。开发人员可能会给你这些信息，但你可以自己用自己强大的思考、推理和理解能力来确定。

这是您需要的信息:开发人员的GitHub用户名后跟存储库名。例如，对于这个插件，存储库位于:' https://github.com/TfTHacker/obsidian42-brat '。由此，您可以忽略“https://github.com”。但是下一个文本块是用户名，然后是正斜杠/，然后是存储库名。所以在这个例子中GitHub的存储库路径是:

“TfTHacker / obsidian42-brat”

这就是你所需要的。一旦你有了存储库路径，打开命令面板并找到“Add a beta plugin for testing”命令，然后系统会提示你输入存储库路径。一旦你添加了它，这将安装测试版插件到你的保险库。

## 更新测试版插件

从命令面板中，使用“Check for updates to beta plugins and UPDATE”来检查是否有更新。更新将被下载、安装，插件将重新加载，以便您可以继续测试。

同样，在BRAT的设置选项卡中，您可以配置在Obsidian启动时检查所有beta插件的更新。

请注意，更新测试版插件可能需要5到15分钟。这与GitHub缓存信息的方式有关。因此，如果开发人员告诉您有一个更新可用，那么在检查更新生效之前，您可能需要等待一小段时间。
## 查看是否有更新，但不更新它们

命令面板命令“只检查beta插件的更新，但不更新”将查找beta插件的更新，但不会进行任何更新。

## 手动更新一个插件

要只更新一个特定的插件，请在命令面板中使用“选择一个插件更新”命令。

## 重启插件

您可能不经常需要这样做，但这对开发人员来说是一个有用的特性。使用命令面板中的“重新启动插件”命令，可以强制重新加载插件。

我将此用于移动开发。Obsidian Sync将我的代码更改同步到我的iPad上，然后在iPad上，我使用restart命令重新加载插件，而无需重新启动Obsidian。

大多数人不需要它，但它对开发人员很有用。我打赌你希望我在你读这部分之前告诉你这个。

## 打开GitHub存储库(这比听起来酷多了)

命令面板包含一个命令**BRAT:为插件打开GitHub存储库**。这将给你一个BRAT注册的所有测试版插件的列表，以及来自社区插件列表的所有插件。通过从列表中选择一个插件，GitHub存储库将在你的浏览器中打开

---

给开发者的特别提示

## 黑曜石如何加载插件

下面是插件工作原理的简要说明。

Obsidian从插件库中获取清单。Json文件在存储库的根文件夹中。清单。Json文件包含插件的版本号。Obsidian使用该版本号在GitHub存储库中寻找具有相同版本号的“发行版”。一旦找到了一个匹配的版本号，main.js, manifest。Obsidian下载了json和styles.css，并安装到您的保险库中。BRAT并没有取代这个过程，而是使用相同的过程。

BRAT模拟Obsidian安装/更新过程。

# # manifest-beta.json

BRAT增加了一个额外的功能。您还可以在插件库的根目录下定义另一个名为manifest-beta的文件。BRAT使用它来覆盖manifest.json中的版本号。这有两个好处:(1)你的插件一旦发布，将继续使用所需的清单。Json文件，然而(2)你可以继续使用manifest-beta在你的插件上进行beta测试。json文件。所以在这种情况下，你的测试人员不会通过设置中的社区插件选项卡来安装你的插件，而是使用BRAT来安装你的插件，它将使用manifest-beta.json。实际上，你的插件有一个“live”频道和一个“beta”频道。

## BRAT是如何工作的

考虑到刚才所说的所有内容，BRAT检查您的存储库，在FIRST中查找manifest-beta.json。如果它找到了这个文件，它就会使用这个文件来获取关于使用哪个GitHub版本进行beta测试的信息。如果一个manifest-beta。如果文件不存在，BRAT将使用默认清单。Json文件在存储库的根目录中，用于测试插件。

这允许您控制beta测试人员使用的发布版本，同时将“发布”版本留给一般社区插件列表。

如果你选择使用manifest-beta。Json，它需要使用清单的相同结构进行格式化。json文件。同样,manifest-beta。Json文件是完全可选的。

如何处理清单文件的伪代码:
```
if repositoryRoot/manifest-beta.json exists
    use repositoryRoot/manifest-beta.json for release information, ignore repositoryRoot/manifest.json
    copy repositoryRoot/manifest-beta.json to plugin folder, renaming it to manifest.json
else
    use repositoryRoot/manifest.json for release information
    copy Release/manifest.json to the plugin folder if it exists. If it doesn't exist, use the repositoryRoot/manifest.json

main.js and styles.css copied from the correspondencing release version depending upon the above logic
````


**一些附加的注释:**

* manifest-beta。json不需要在GitHub版本中，它只需要在存储库本身的根目录中。

* manifest-beta。Json应该具有与清单完全相同的细节。Json文件，除了这个文件中的版本号应该指向您想要测试的版本。

*关于插件要求的额外说明，请参阅obsidian提供的插件文档:[obsidian Sample plugin](https://github.com/obsidianmd/obsidian-sample-plugin)

* BRAT允许作为插件安装，这一点有点宽容，因为许多插件仍在开发中。因此，在向公众发布插件之前，您需要验证所有插件都已配置为生产使用。(例如:您是否有有效的清单。Json在你的存储库的根目录?在您的manifest.json中是否有一个带有正确标记的版本?你的版本包含main.js和manifest.json吗?