## 使用 nuget 包
在Unity项目中引入NuGet包的过程相对简单，但需要注意的是Unity本身并不是一个基于.NET Standard的完整开发环境，而是有自己的脚本编写系统（如C#）。为了在Unity项目中    
使用NuGet包，你需要通过一些步骤来设置和配置。以下是详细的步骤：

### 1. 安装NuGet for Unity
首先，确保你已经在电脑上安装了`NuGet for Unity`插件。你可以从Visual Studio市场或直接从Unity Asset Store下载该插件。

#### 在Unity中安装NuGet for Unity插件：
1. 打开你的Unity项目。
2. 转到 `Window > Package Manager`，打开包管理器窗口。
3. 点击右上角的“+”按钮，搜索并安装 `NuGet for Unity` 插件。

### 2. 创建或选择一个解决方案
在Unity中，你需要创建或选择一个`.csproj`文件来与NuGet集成。`.csproj`文件通常用于.NET项目的构建配置。

#### 在Unity项目中创建`.csproj`文件：
1. 打开终端（如Git Bash）。
2. 导航到你的Unity项目目录：`cd path/to/your/project`
3. 运行以下命令来生成`.csproj`文件：
   ```sh
   dotnet new classlib -o Assets/NuGetProject
   ```

### 3. 使用NuGet for Unity安装包
在成功创建或选择一个解决方案后，你可以使用Unity的NuGet管理器来安装所需的NuGet包。

#### 在Unity中添加NuGet包：
1. 打开 `Window > Package Manager`。
2. 点击左上角的“+”按钮，选择“Add Packages from Source”，然后选择你的`.csproj`文件所在的目录（通常是 `Assets/NuGetProject`）。
3. 在搜索框中输入你想要安装的NuGet包名称，例如 `Microsoft.AspNetCore.Mvc.RazorPages`。
4. 选择你需要的包并点击“Install”。

### 4. 将代码和依赖项导入Unity项目
安装完成后，你需要将生成的DLL文件和其他资源添加到Unity项目的脚本目录中。

#### 导入生成的文件：
1. 打开你的Unity编辑器，转到 `Assets/NuGetProject` 目录。
2. 选择所有包含在包中的C#脚本和DLL文件（通常在 `bin/Debug/netstandard2.0` 或 `lib/netstandard2.0` 文件夹中）。
3. 将这些文件拖动到Unity项目的任何脚本目录中，例如 `Assets/Scripts`。

### 5. 配置Unity项目
确保你的Unity项目正确配置了.NET标准支持。你可以通过以下步骤来设置：

#### 在Unity的Player Settings中进行配置：
1. 转到 `Edit > Project Settings > Player`。
2. 在“Other Settings”部分，找到“Api Compatibility Level”并选择适当的.NET版本（如`.NET 4.x Equivalent`或`.NET Standard 2.0`）。

### 6. 编写和使用代码
现在你可以在Unity项目中编写和使用这些NuGet包中的代码了。例如：

```csharp
using UnityEngine;
using Microsoft.AspNetCore.Mvc.RazorPages;

public class ExampleClass : MonoBehaviour
{
    void Start()
    {
        // 使用NuGet包中的功能
        var pageModel = new PageModel();
        Debug.Log(pageModel.ToString());
    }
}
```

### 7. 注意事项
- 确保你选择的.NET标准版本与Unity项目兼容。
- 某些高级或特定框架可能需要额外的配置步骤。
