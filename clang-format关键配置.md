

# VSC中的clang-format设置

## setting 全局设置

### 1.打开`全局设置`：

- 在VS Code中，进入菜单 **File > Preferences > Settings**（或 **Code > Preferences > Settings**，如果是macOS）。
- 选择左上角的“用户”选项，这样设置将应用于所有项目。

### 2.编辑`settings.json`：

- 在设置页面的右上角，点击齿轮图标并选择“"打开设置" 进入全局`settings.json`。
- 添加自己的所好，不仅仅是关于clang-format的配置

现在，这些设置将全局应用于所有新打开的项目，无需每次复制粘贴配置了。



**==可以使用`CTRL + F`的方式，在setting或是./clang-format文件中查找对应的控制参数==** 

**==重复调用一个参数，会报错==** 



### 3. 编辑 `.clang-format` 文件

将此 `.clang-format` 文件放在项目根目录，并确保 VS Code 已经启用了 `clang-format`。

例如我**==(utunbu 22.04)==**就在主目录下建立了`.clang-format`文件。 

1. **创建全局 `.clang-format` 文件**：

   - 在用户主目录（例如 `~` 或 `/home/username`）中创建一个 `.clang-format` 文件。

   - 使用以下命令在用户主目录中生成一个 `.clang-format` 文件：

     ```bash
     clang-format -style=llvm -dump-config > ~/.clang-format  //默认形式为llvm  
     clang-format -style=google -dump-config > .clang-format  //默认形式为google  我是用的是这个
     ```

   - 这样会在主目录生成一个默认的 `.clang-format` 文件。

### 4.在`setting`中启用

1. **配置 VS Code 使用全局 `.clang-format` 文件**（可选）：

   - 在 `settings.json` 中确保 `clang-format` 被设置为C++文件的默认格式化工具：

     ```json
     "[cpp]": {
         "editor.defaultFormatter": "xaver.clang-format"
     },
     "[c]": {
         "editor.defaultFormatter": "xaver.clang-format"
     },
     "editor.formatOnSave": true
     ```

2. **优先级**：

   - **项目级 `.clang-format` 文件优先**：如果项目目录中存在 `.clang-format` 文件，`clang-format` 会优先使用项目级的配置文件。
   - **无项目级文件时使用全局文件**：当项目中没有 `.clang-format` 文件时，`clang-format` 会回退到主目录中的全局配置文件 `~/.clang-format`。

3. **我的配置**: 

   - ```json
     {
         "[python]": {
             "editor.defaultFormatter": "esbenp.prettier-vscode"
         },
         "[cpp]": {
             "editor.defaultFormatter": "xaver.clang-format"
         },
         "[c]": {
             "editor.defaultFormatter": "xaver.clang-format"
         },
     
         // clang-format 配置，设置为使用主目录的 .clang-format
         "C_Cpp.clang_format_fallbackStyle": "none", // 禁用默认风格，确保只使用主目录的配置文件
     
         // 确保在没有 .clang-format 文件时不会应用 Google 风格
         //"clang-format.style": "{ BasedOnStyle: LLVM, IndentWidth: 2, ColumnLimit: 100, AllowShortIfStatementsOnASingleLine: false, SpaceBeforeParens: ControlStatements, BraceWrapping: { AfterFunction: true, AfterControlStatement: true, AfterClass: false, AfterStruct: false, SplitEmptyFunction: true }, DerivePointerAlignment: false, PointerAlignment: Left, BinPackParameters: true, AlignAfterOpenBracket: DontAlign, PenaltyBreakBeforeFirstCallParameter: 100 }",
     }
     ```

---

# 基础设置项

- **Language: Cpp**  
  设置语言为 C++，以确保格式化工具适应 C++ 代码。

- **BasedOnStyle: Google**  
  使用 Google 风格作为基础。这意味着代码会默认按照 Google 的代码风格格式化，除非有其他设置覆盖。

- **AccessModifierOffset: -1**  
  访问修饰符（如 `public:`、`private:`）的位置设置。不缩进访问修饰符，使它们与类对齐。

- **AlignAfterOpenBracket: Align**  
  在括号后的内容对齐，增加代码的整齐度。

- **AlignOperands: Align**  
  使运算符两侧的内容对齐，提升可读性。

- **AlignTrailingComments: true**  
  让代码行尾的注释对齐，保持整齐。

- **AllowAllArgumentsOnNextLine: true**  
  允许在函数调用时将所有参数放在下一行。

- **AllowShortFunctionsOnASingleLine: All**  
  允许将短函数写在一行上。

- **AlwaysBreakBeforeMultilineStrings: true**  
  多行字符串总是在之前换行，使长字符串更清晰。

- **BraceWrapping**  
  控制大括号的位置，例如：
  - **AfterClass: false**：类定义后不换行。
  - **BeforeElse: false**：`else` 之前不换行。

- **BreakBeforeBinaryOperators: None**  
  在二元操作符之前不换行，让表达式紧凑。

- **BreakBeforeBraces: Attach**  
  大括号紧跟在控制语句、函数等的右侧。

- **ColumnLimit: 100**  
  设置每行的字符限制为 100 字符，超过时自动换行。

- **ConstructorInitializerIndentWidth: 4**  
  设置构造函数初始化列表的缩进宽度为 4。

- **Cpp11BracedListStyle: true**  
  使用 C++11 的大括号初始化列表风格。

- **DeriveLineEnding: true**  
  自动检测行尾符号类型（如 Windows 的 CRLF 或 Unix 的 LF）。

- **DerivePointerAlignment: true**  
  自动检测指针符号的对齐方式。

- **IndentAccessModifiers: false**  
  访问修饰符（如 `public:`、`private:`）不缩进，与类对齐。

- **IndentWidth: 4**  
  设置每级缩进宽度为 4 个空格。

- **MaxEmptyLinesToKeep: 1**  
  在代码中保持最多 1 行空行，去掉多余的空行。

- **PointerAlignment: Left**  
  指针符号 `*` 放在变量名的左侧，如 `int* ptr`。

- **SpaceBeforeParens: ControlStatements**  
  在控制语句（如 `if`、`for`）和括号之间留空格。

- **UseTab: Never**  
  禁止使用 Tab，全部用空格缩进。

---

### 示例解释

假设我们有如下代码：

```cpp
class MyClass {
public:
    MyClass(int a, int b) : a_(a), b_(b) {}
    int getValue() { return a_ + b_; }
private:
    int a_, b_;
};
```

- 设置 **IndentWidth: 4** 会使每一级缩进使用 4 个空格。
- **AccessModifierOffset: -1** 会让 `public:` 和 `private:` 与类对齐。
- **AllowShortFunctionsOnASingleLine: All** 允许 `getValue()` 保持在一行上。
- **ColumnLimit: 100** 意味着在每行不超过 100 字符的情况下，尽量保持代码在同一行。

哪里可以高度自定义？

- **ColumnLimit: 100**  
  设置每行的字符限制为 100 字符，超过时自动换行。

- **ConstructorInitializerIndentWidth: 4**  

  设置构造函数初始化列表的缩进宽度为 4。

- **MaxEmptyLinesToKeep: 1**  
  在代码中保持最多 1 行空行，去掉多余的空行。
- **PointerAlignment: Left**  
  指针符号 `*` 放在变量名的左侧，如 `int* ptr`。



# 花括号的位置

> [!NOTE]
>
> 考虑到花括号的高度自定义（本人喜欢接在函数后面，而不是另起一行）。在这里附上调整的完整指南

在 `.clang-format` 配置文件中，可以通过 `BraceWrapping` 和 `BreakBeforeBraces` 两个设置项来自定义花括号（大括号）的位置和样式。这些设置控制花括号是紧跟在语句之后，还是另起一行。

### 1. `BreakBeforeBraces`

`BreakBeforeBraces` 是一个全局设置，指定花括号相对于不同代码结构的位置。可选值包括：

- **Attach**：花括号紧跟在代码块语句的右侧，不换行。
- **Linux**：在函数、类等的定义之后，花括号另起一行。
- **Stroustrup**：在函数后紧跟大括号，其他位置换行。
- **Allman**：所有位置的花括号都换行。
- **Mozilla**：大括号在函数、命名空间等位置换行，在其他地方不换行。
- **WebKit**：函数的花括号不换行，其他位置换行.

#### 示例

```yaml
BreakBeforeBraces: Allman
```

代码示例：

```cpp
// Attach
if (condition) {
    // Code
}

// Allman
if (condition)
{
    // Code
}
```

### 2. `BraceWrapping`

`BraceWrapping` 提供了更细粒度的控制，可以针对不同的代码结构（如类、函数、控制语句等）设置花括号的位置。它包含多个子选项，可以逐一指定。

#### 可选子项

- **AfterClass**：类定义之后的花括号位置。
- **AfterControlStatement**：控制语句（如 `if`, `for`, `while`）之后的花括号位置。
- **AfterFunction**：函数定义之后的花括号位置。
- **AfterNamespace**：命名空间之后的花括号位置。
- **BeforeCatch**：`catch` 之前的花括号位置。
- **BeforeElse**：`else` 之前的花括号位置。
- **BeforeLambdaBody**：lambda 表达式体之前的花括号位置。
- **AfterEnum**：枚举之后的花括号位置。

每个子项的值可以是 `true` 或 `false`：

- **true**：花括号在该位置换行。
- **false**：花括号紧跟在代码块的右侧。

#### 示例配置

```yaml
BraceWrapping:
  AfterClass: true               # 类定义后换行
  AfterControlStatement: false    # 控制语句后不换行
  AfterFunction: false            # 函数定义后不换行
  AfterNamespace: true            # 命名空间后换行
  BeforeCatch: true               # catch 前换行
  BeforeElse: true                # else 前换行
  BeforeLambdaBody: false         # lambda 表达式体前不换行
  AfterEnum: true                 # 枚举后换行
```

### 示例代码

假设我们有如下代码：

```cpp
class MyClass {
public:
    MyClass() {
        // Constructor
    }
};

namespace MyNamespace {
    void myFunction() {
        if (condition) {
            // Do something
        } else {
            // Do something else
        }
    }
}
```

使用上面的 `BraceWrapping` 配置后：

- 类 `MyClass` 的花括号会在 `class MyClass` 后换行。
- `namespace` 的花括号会在 `namespace MyNamespace` 后换行。
- `if` 语句后花括号不换行，但 `else` 之前会换行。
- 函数和控制语句的花括号都不会换行，保持在同一行。

### 总结

通过 `BreakBeforeBraces` 和 `BraceWrapping` 的组合设置，可以灵活地控制花括号的位置。

# 可阅读性的关键设置

### 配置项解释

1. **BinPackArguments: false** 和 **BinPackParameters: false**
   - 这两个选项控制是否将多个参数或多个调用的参数打包在同一行上。
   - **BinPackArguments: false** 表示在函数调用中不将多个参数紧凑地放在同一行上。
   - **BinPackParameters: false** 表示在函数定义中不将多个参数紧凑地放在同一行上。
   - 设置为 `false` 可以使每个参数在换行时单独占一行，避免所有参数都挤在同一行。

2. **PenaltyBreakBeforeFirstCallParameter: 0**
   - 这个选项控制在函数调用的第一个参数之前换行的“惩罚”值，值越高，clang-format 越不倾向于在第一个参数前换行。
   - 设置为 `0` 将惩罚降到最低，使得在第一个参数前换行的可能性更高。

3. **BreakBeforeBinaryOperators: NonAssignment**
   - 这个选项控制在二元操作符之前是否换行。
   - 设置为 `NonAssignment` 意味着在非赋值操作符（如 `+`, `-`, `*`, `/`）之前换行，而赋值操作符（如 `=`）则不会在其前面换行。

4. **AlwaysBreakAfterReturnType: All**
   - 控制函数返回类型之后是否换行。
   - 设置为 `All` 会强制函数的返回类型和函数名在不同的行上，这对保持长函数签名的清晰度有帮助。

5. **ConstructorInitializerAllOnOneLineOrOnePerLine: true**
   - 这个选项控制构造函数初始化列表的布局。
   - 设置为 `true` 表示每个初始化器应在独立的一行上，而不是全部打包在同一行中。

6. **BreakConstructorInitializers: AfterColon**
   - 控制构造函数初始化列表中，初始化器是否应在冒号后换行。
   - 设置为 `AfterColon` 会在冒号后换行，将初始化列表放在单独的行上。

### 在 `.clang-format` 文件中添加这些配置

可以将这些配置项直接放入 `.clang-format` 文件的任何位置，但通常我们将它们添加到文件的顶部或分组归类，以便于管理和查看。例如：

```yaml
# 基本样式
BasedOnStyle: Google
IndentWidth: 4
ColumnLimit: 80

# 参数打包和换行控制
BinPackArguments: false
BinPackParameters: false
PenaltyBreakBeforeFirstCallParameter: 0

# 二元操作符和返回类型换行
BreakBeforeBinaryOperators: NonAssignment
AlwaysBreakAfterReturnType: All

# 构造函数初始化器设置
ConstructorInitializerAllOnOneLineOrOnePerLine: true
BreakConstructorInitializers: AfterColon

# 其他配置项
...
```

### 应用方式

1. **项目级别配置**：
   - 将这些选项添加到项目根目录的 `.clang-format` 文件中。
   - VS Code 会自动检测到这个文件，并在您进行代码格式化时应用这些规则。

2. **全局配置**：
   
   - 如果希望在所有项目中应用相同的 `.clang-format` 配置，可以将文件放在主目录（例如 `~/.clang-format`）。
   - 这样所有的 C++ 项目在没有特定的项目级 `.clang-format` 文件时都会使用这个全局文件。
   
3. **在 `settings.json` 中添加（如果需要）**：
   
   - 也可以在 `settings.json` 中的 `clang-format.style` 选项中直接添加这些设置，将它们写成单行字符串。例如：
   
     ```json
     "clang-format.style": "{ BasedOnStyle: Google, IndentWidth: 4, ColumnLimit: 80, BinPackArguments: false, BinPackParameters: false, PenaltyBreakBeforeFirstCallParameter: 0, BreakBeforeBinaryOperators: NonAssignment, AlwaysBreakAfterReturnType: All, ConstructorInitializerAllOnOneLineOrOnePerLine: true, BreakConstructorInitializers: AfterColon }"
     ```

> **注意**：如果使用 `settings.json` 中的 `clang-format.style`，需要将整个内容写成单行字符串。如果使用 `.clang-format` 文件，则可以按 YAML 格式逐行写入。

# 换行的控制

## BreakConstructorInitializers



`BreakConstructorInitializers` 控制构造函数初始化列表中冒号或逗号的位置，以决定是否在冒号或逗号之前或之后换行。这个选项可以让代码的格式更具一致性和可读性。它有以下几个选项：

- **AfterColon**：在冒号之后换行。
- **BeforeColon**：在冒号之前换行。
- **BeforeComma**：在逗号之前换行。

### 示例代码

假设我们有以下构造函数的代码行：

```cpp
class MyClass {
public:
    MyClass(int a, int b, int c, int d)
        : a_(a), b_(b), c_(c), d_(d) {}
private:
    int a_, b_, c_, d_;
};
```

### 使用 `BreakConstructorInitializers: AfterColon`

当设置 `BreakConstructorInitializers: AfterColon` 时：

```yaml
BreakConstructorInitializers: AfterColon
ColumnLimit: 40
```

格式化结果：

```cpp
class MyClass {
public:
    MyClass(int a, int b, int c, int d)
        : a_(a), 
          b_(b), 
          c_(c), 
          d_(d) {}
private:
    int a_, b_, c_, d_;
};
```

**解释**：  
在冒号后立即换行，初始化列表的每个成员都在单独的行上。这样可以在构造函数初始化列表较长时提供更好的可读性。

### 使用 `BreakConstructorInitializers: BeforeColon`

当设置 `BreakConstructorInitializers: BeforeColon` 时：

```yaml
BreakConstructorInitializers: BeforeColon
ColumnLimit: 40
```

格式化结果：

```cpp
class MyClass {
public:
    MyClass(int a, int b, int c, int d)
    :
      a_(a), 
      b_(b), 
      c_(c), 
      d_(d) {}
private:
    int a_, b_, c_, d_;
};
```

**解释**：  
在冒号之前换行，将冒号放在单独一行上，之后每个初始化器占据单独一行。这种风格在某些代码规范中可能更常见，尤其是在长初始化列表的情况下。

### 使用 `BreakConstructorInitializers: BeforeComma`

当设置 `BreakConstructorInitializers: BeforeComma` 时：

```yaml
BreakConstructorInitializers: BeforeComma
ColumnLimit: 40
```

格式化结果：

```cpp
class MyClass {
public:
    MyClass(int a, int b, int c, int d)
        : a_(a)
        , b_(b)
        , c_(c)
        , d_(d) {}
private:
    int a_, b_, c_, d_;
};
```

**解释**：  
在每个逗号之前换行，这种风格会在每个初始化器前的逗号前换行，通常在某些代码风格中用来强调每个初始化器的独立性。

### 总结

- **AfterColon**：在冒号后换行，使初始化列表显得紧凑且易读。
- **BeforeColon**：在冒号前换行，冒号单独一行，用于一些更严格的代码格式规范。
- **BeforeComma**：在每个逗号之前换行，使每个初始化器看起来更独立，便于查看长列表。

# 间隔设置(tab还是其他的距离)

要调整不同嵌套之间的缩进，使其在视觉上更清晰，可以使用 `.clang-format` 中的几个关键设置项来控制类成员、访问修饰符和嵌套结构的缩进。

### 关键设置项

1. **IndentWidth**：控制每一级的缩进宽度。
2. **AccessModifierOffset**：控制访问修饰符（如 `public:`、`private:`）相对于类的缩进。
3. **IndentAccessModifiers**：控制访问修饰符是否应缩进到类的缩进级别。
4. **EmptyLineBeforeAccessModifier**：控制在访问修饰符之前插入空行，以便增加代码块的可读性。

### 示例 `.clang-format` 配置

以下配置尝试增加类成员和访问修饰符的缩进：

```yaml
BasedOnStyle: LLVM
IndentWidth: 4  # 每一级缩进的宽度，可以根据需要调整
AccessModifierOffset: -1  # 访问修饰符缩进级别，设为 -1 表示不缩进
IndentAccessModifiers: false  # 访问修饰符不随类成员缩进
EmptyLineBeforeAccessModifier: LogicalBlock  # 在每个访问修饰符之前插入空行
ConstructorInitializerIndentWidth: 4  # 构造函数初始化器的缩进宽度
```

### 配置解释

- **IndentWidth**：设置为 `4` 表示每级缩进为 4 个空格，这会使代码的不同嵌套结构更加分明。
- **AccessModifierOffset**：设置为 `-1` 使得访问修饰符（如 `public:`、`private:`）不会缩进，与类名对齐。
- **IndentAccessModifiers**：设置为 `false`，避免访问修饰符跟随类成员一起缩进，这样可以使访问修饰符显得更加突出。
- **EmptyLineBeforeAccessModifier**：设置为 `LogicalBlock`，在每个访问修饰符之前插入一个空行，这样可以为每个块提供更好的分隔。

# setting.json的所有代码

```json
{
    "C_Cpp.default.compileCommands": "${workspaceFolder}/build/compile_commands.json",
    "workbench.colorTheme": "Eva Light Italic Bold",
    "explorer.confirmDragAndDrop": false,
    "makefile.configureOnOpen": true,
    "extensions.ignoreRecommendations": true,
    "explorer.confirmDelete": false,
    "workbench.iconTheme": "material-icon-theme",
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.minimap.renderCharacters": false,
    "editor.minimap.enabled": false,
    "cmake.options.statusBarVisibility": "icon",
    "terminal.integrated.enableMultiLinePasteWarning": "never",
    "code-runner.runInTerminal": true,
    "editor.formatOnSave": true,
    "explorer.compactFolders": false,
    "cSpell.userWords": [
        "rclcpp",
        "iostream",
        "ostream",
        "array",
        "atomic",
        "cctype",
        "clocale",
        "cmath",
        "cstdarg",
        "cstddef",
        "cstdint",
        "cstdio",
        "cstdlib",
        "cwchar",
        "cwctype",
        "deque",
        "unordered_map",
        "vector",
        "exception",
        "algorithm",
        "memory",
        "optional",
        "string",
        "tuple",
        "utility",
        "fstream",
        "sstream",
        "stdexcept",
        "typeinfo",
        "iomanip",
        "iosfwd",
        "istream",
        "streambuf",
        "stdbool",
        "chrono",
        "cstring",
        "cinttypes",
        "typeindex",
        "esbenp",
        "xaver",
        "SpaceBeforeParens"
    ],

    // 新增的C++相关配置
    "files.associations": {
        "iostream": "cpp",
        "ostream": "cpp",
        "array": "cpp",
        "atomic": "cpp",
        "*.tcc": "cpp",
        "cctype": "cpp",
        "clocale": "cpp",
        "cmath": "cpp",
        "cstdarg": "cpp",
        "cstddef": "cpp",
        "cstdint": "cpp",
        "cstdio": "cpp",
        "cstdlib": "cpp",
        "cwchar": "cpp",
        "cwctype": "cpp",
        "deque": "cpp",
        "unordered_map": "cpp",
        "vector": "cpp",
        "exception": "cpp",
        "algorithm": "cpp",
        "memory": "cpp",
        "memory_resource": "cpp",
        "optional": "cpp",
        "string": "cpp",
        "string_view": "cpp",
        "system_error": "cpp",
        "tuple": "cpp",
        "type_traits": "cpp",
        "utility": "cpp",
        "fstream": "cpp",
        "initializer_list": "cpp",
        "iosfwd": "cpp",
        "istream": "cpp",
        "limits": "cpp",
        "new": "cpp",
        "sstream": "cpp",
        "stdexcept": "cpp",
        "streambuf": "cpp",
        "typeinfo": "cpp",
        "stdbool.h": "c",
        "cstring": "cpp",
        "ctime": "cpp",
        "bit": "cpp",
        "bitset": "cpp",
        "chrono": "cpp",
        "compare": "cpp",
        "complex": "cpp",
        "concepts": "cpp",
        "condition_variable": "cpp",
        "forward_list": "cpp",
        "list": "cpp",
        "map": "cpp",
        "set": "cpp",
        "unordered_set": "cpp",
        "functional": "cpp",
        "iterator": "cpp",
        "numeric": "cpp",
        "random": "cpp",
        "ratio": "cpp",
        "iomanip": "cpp",
        "mutex": "cpp",
        "numbers": "cpp",
        "semaphore": "cpp",
        "stop_token": "cpp",
        "thread": "cpp",
        "cinttypes": "cpp",
        "typeindex": "cpp"
    },

    "[python]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[cpp]": {
        "editor.defaultFormatter": "xaver.clang-format"
    },
    "[c]": {
        "editor.defaultFormatter": "xaver.clang-format"
    },

    // clang-format 配置，设置为使用主目录的 .clang-format
    "C_Cpp.clang_format_fallbackStyle": "none", // 禁用默认风格，确保只使用主目录的配置文件

    // 确保在没有 .clang-format 文件时不会应用 Google 风格
    //"clang-format.style": "{ BasedOnStyle: LLVM, IndentWidth: 2, ColumnLimit: 100, AllowShortIfStatementsOnASingleLine: false, SpaceBeforeParens: ControlStatements, BraceWrapping: { AfterFunction: true, AfterControlStatement: true, AfterClass: false, AfterStruct: false, SplitEmptyFunction: true }, DerivePointerAlignment: false, PointerAlignment: Left, BinPackParameters: true, AlignAfterOpenBracket: DontAlign, PenaltyBreakBeforeFirstCallParameter: 100 }",

    "prettier.printWidth": 80,
    "prettier.tabWidth": 4,
    "prettier.useTabs": false,
    "prettier.singleQuote": true,
    "prettier.trailingComma": "none",
    "prettier.semi": true,
    "workbench.settings.applyToAllProfiles": []
}
```

# .clang-format的所有代码

```json
---
Language: Cpp # 设置为 C++ 语言
# BasedOnStyle:  Google
AccessModifierOffset: -1 # 访问修饰符的缩进偏移
AlignAfterOpenBracket: Align # 在括号后对齐
AlignArrayOfStructures: None # 数组结构的对齐方式
AlignConsecutiveMacros: None # 连续宏的对齐方式
AlignConsecutiveAssignments: None # 连续赋值语句的对齐方式
AlignConsecutiveBitFields: None # 连续位字段的对齐方式
AlignConsecutiveDeclarations: None # 连续声明的对齐方式
AlignEscapedNewlines: Left # 转义换行符的对齐方式
AlignOperands: Align # 操作数的对齐方式
AlignTrailingComments: true # 是否对齐尾部注释
AllowAllArgumentsOnNextLine: true # 是否允许所有参数换行
AllowAllParametersOfDeclarationOnNextLine: true # 是否允许所有声明参数换行
AllowShortEnumsOnASingleLine: true # 允许短枚举在单行
AllowShortBlocksOnASingleLine: Never # 控制短代码块在单行的行为
AllowShortCaseLabelsOnASingleLine: false # 是否允许短的 case 标签在单行
AllowShortFunctionsOnASingleLine: All # 允许短函数在单行
AllowShortLambdasOnASingleLine: All # 允许短 lambda 表达式在单行
AllowShortIfStatementsOnASingleLine: WithoutElse # 没有 else 的短 if 语句可以在单行
AllowShortLoopsOnASingleLine: true # 允许短循环在单行
AlwaysBreakAfterDefinitionReturnType: None # 定义返回类型后是否总是换行
AlwaysBreakAfterReturnType: None # 返回类型后是否总是换行
AlwaysBreakBeforeMultilineStrings: true # 多行字符串之前总是换行
AlwaysBreakTemplateDeclarations: Yes # 模板声明总是换行
AttributeMacros:
    - __capability # 属性宏定义
BinPackArguments: true # 是否将多个函数调用参数打包在一行
BinPackParameters: true # 是否将多个声明参数打包在一行
BraceWrapping: # 大括号换行控制
    AfterCaseLabel: false # case 标签后不换行
    AfterClass: false # 类定义后不换行
    AfterControlStatement: Never # 控制语句后从不换行
    AfterEnum: false # 枚举后不换行
    AfterFunction: false # 函数后不换行
    AfterNamespace: false # 命名空间后不换行
    AfterObjCDeclaration: false # Objective-C 声明后不换行
    AfterStruct: false # 结构体后不换行
    AfterUnion: false # 联合体后不换行
    AfterExternBlock: false # extern 块后不换行
    BeforeCatch: false # catch 之前不换行
    BeforeElse: false # else 之前不换行
    BeforeLambdaBody: false # lambda 表达式主体之前不换行
    BeforeWhile: false # while 之前不换行
    IndentBraces: false # 不缩进大括号
    SplitEmptyFunction: true # 空函数换行
    SplitEmptyRecord: true # 空记录换行
    SplitEmptyNamespace: true # 空命名空间换行
BreakBeforeBinaryOperators: None # 二元操作符之前不换行
BreakBeforeConceptDeclarations: true # 概念声明之前换行
BreakBeforeBraces: Attach # 大括号紧跟在控制语句、函数等右侧
BreakBeforeInheritanceComma: false # 继承列表的逗号前不换行
BreakInheritanceList: BeforeColon # 继承列表在冒号前换行
BreakBeforeTernaryOperators: true # 三元操作符之前换行
BreakConstructorInitializersBeforeComma: false # 构造函数初始化器的逗号前不换行
BreakConstructorInitializers: BeforeColon # 构造函数初始化器在冒号前换行
BreakAfterJavaFieldAnnotations: false # Java 字段注解后不换行
BreakStringLiterals: true # 字符串字面量换行
ColumnLimit: 100 # 每行代码字符限制为 80
CommentPragmas: '^ IWYU pragma:' # 注释中的编译指令
QualifierAlignment: Leave # 限定符的对齐方式
CompactNamespaces: false # 是否使用紧凑的命名空间
ConstructorInitializerIndentWidth: 4 # 构造函数初始化器的缩进宽度
ContinuationIndentWidth: 4 # 换行时的额外缩进宽度
Cpp11BracedListStyle: true # 使用 C++11 大括号初始化列表的风格
DeriveLineEnding: true # 自动检测行尾格式
DerivePointerAlignment: true # 自动检测指针对齐方式
DisableFormat: false # 是否禁用格式化
EmptyLineAfterAccessModifier: Never # 访问修饰符后不加空行
EmptyLineBeforeAccessModifier: LogicalBlock # 访问修饰符前加空行
ExperimentalAutoDetectBinPacking: false # 是否启用实验性的自动检测打包
PackConstructorInitializers: NextLine # 构造函数初始化器放在下一行
BasedOnStyle: '' # 不基于任何已有样式，完全自定义
ConstructorInitializerAllOnOneLineOrOnePerLine: false # 初始化器不强制一行
AllowAllConstructorInitializersOnNextLine: true # 允许所有构造函数初始化器在下一行
FixNamespaceComments: true # 修正命名空间的注释
ForEachMacros:
    - foreach
    - Q_FOREACH
    - BOOST_FOREACH # 循环宏定义
IfMacros:
    - KJ_IF_MAYBE # if 宏定义
IncludeBlocks: Regroup # 包含块的组织方式
IncludeCategories: # 包含的排序优先级
    - Regex: '^<ext/.*\.h>'
      Priority: 2
      SortPriority: 0
      CaseSensitive: false
    - Regex: '^<.*\.h>'
      Priority: 1
      SortPriority: 0
      CaseSensitive: false
    - Regex: '^<.*'
      Priority: 2
      SortPriority: 0
      CaseSensitive: false
    - Regex: '.*'
      Priority: 3
      SortPriority: 0
      CaseSensitive: false
IncludeIsMainRegex: '([-_](test|unittest))?$' # 主文件的包含正则表达式
IncludeIsMainSourceRegex: '' # 主文件源的包含正则表达式
IndentAccessModifiers: false # 不缩进访问修饰符
IndentCaseLabels: true # 缩进 case 标签
IndentCaseBlocks: false # 不缩进 case 块
IndentGotoLabels: true # 缩进 goto 标签
IndentPPDirectives: None # 预处理指令的缩进方式
IndentExternBlock: AfterExternBlock # extern 块的缩进方式
IndentRequires: false # 是否缩进 requires 子句
IndentWidth: 4 # 缩进宽度
IndentWrappedFunctionNames: false # 不缩进换行的函数名
InsertTrailingCommas: None # 不插入尾随逗号
JavaScriptQuotes: Leave # 保留 JavaScript 引号风格
JavaScriptWrapImports: true # JavaScript 导入换行
KeepEmptyLinesAtTheStartOfBlocks: false # 保持块开头的空行
LambdaBodyIndentation: Signature # lambda 表达式的缩进方式
MacroBlockBegin: '' # 宏块开始标记
MacroBlockEnd: '' # 宏块结束标记
MaxEmptyLinesToKeep: 1 # 保留的最大空行数
NamespaceIndentation: None # 命名空间的缩进方式
ObjCBinPackProtocolList: Never # Objective-C 协议列表的打包方式
ObjCBlockIndentWidth: 2 # Objective-C 块的缩进宽度
ObjCBreakBeforeNestedBlockParam: true # 在嵌套块参数之前换行
ObjCSpaceAfterProperty: false # 属性声明后不加空格
ObjCSpaceBeforeProtocolList: true # 协议列表前加空格
PenaltyBreakAssignment: 2 # 赋值换行的惩罚值
PenaltyBreakBeforeFirstCallParameter: 1 # 第一个调用参数前换行的惩罚值
PenaltyBreakComment: 300 # 注释换行的惩罚值
PenaltyBreakFirstLessLess: 120 # 第一个 << 操作符换行的惩罚值
PenaltyBreakOpenParenthesis: 0 # 开括号换行的惩罚值
PenaltyBreakString: 1000 # 字符串换行的惩罚值
PenaltyBreakTemplateDeclaration: 10 # 模板声明换行的惩罚值
PenaltyExcessCharacter: 1000000 # 超出字符数的惩罚值
PenaltyReturnTypeOnItsOwnLine: 200 # 返回类型单独换行的惩罚值
PenaltyIndentedWhitespace: 0 # 缩进空格的惩罚值
PointerAlignment: Left # 指针对齐方式
PPIndentWidth: -1 # 预处理指令缩进宽度
RawStringFormats: # 原始字符串格式
    - Language: Cpp
      Delimiters:
          - cc
          - CC
          - cpp
          - Cpp
          - CPP
          - 'c++'
          - 'C++'
      CanonicalDelimiter: ''
      BasedOnStyle: google
    - Language: TextProto
      Delimiters:
          - pb
          - PB
          - proto
          - PROTO
      EnclosingFunctions:
          - EqualsProto
          - EquivToProto
          - PARSE_PARTIAL_TEXT_PROTO
          - PARSE_TEST_PROTO
          - PARSE_TEXT_PROTO
          - ParseTextOrDie
          - ParseTextProtoOrDie
          - ParseTestProto
          - ParsePartialTestProto
      CanonicalDelimiter: pb
      BasedOnStyle: google
ReferenceAlignment: Pointer # 引用对齐方式
ReflowComments: true # 重新格式化注释
RemoveBracesLLVM: false # 是否删除 LLVM 样式的大括号
SeparateDefinitionBlocks: Leave # 定义块的分隔方式
ShortNamespaceLines: 1 # 短命名空间的行数
SortIncludes: CaseSensitive # 包含排序的区分大小写
SortJavaStaticImport: Before # Java 静态导入的排序
SortUsingDeclarations: true # 使用声明排序
SpaceAfterCStyleCast: false # C 风格转换后不加空格
SpaceAfterLogicalNot: false # 逻辑非操作符后不加空格
SpaceAfterTemplateKeyword: true # 模板关键字后加空格
SpaceBeforeAssignmentOperators: true # 赋值操作符前加空格
SpaceBeforeCaseColon: false # case 冒号前不加空格
SpaceBeforeCpp11BracedList: false # C++11 大括号列表前不加空格
SpaceBeforeCtorInitializerColon: true # 构造函数初始化器冒号前加空格
SpaceBeforeInheritanceColon: true # 继承冒号前加空格
SpaceBeforeParens: ControlStatements # 控制语句前加空格
SpaceBeforeParensOptions: # 控制各类括号的空格选项
    AfterControlStatements: true
    AfterForeachMacros: true
    AfterFunctionDefinitionName: false
    AfterFunctionDeclarationName: false
    AfterIfMacros: true
    AfterOverloadedOperator: false
    BeforeNonEmptyParentheses: false
SpaceAroundPointerQualifiers: Default # 指针限定符周围的空格
SpaceBeforeRangeBasedForLoopColon: true # 范围 for 循环的冒号前加空格
SpaceInEmptyBlock: false # 空块内不加空格
SpaceInEmptyParentheses: false # 空括号内不加空格
SpacesBeforeTrailingComments: 2 # 尾注释前的空格数
SpacesInAngles: Never # 角括号内不加空格
SpacesInConditionalStatement: false # 条件语句中的空格
SpacesInContainerLiterals: true # 容器字面量中的空格
SpacesInCStyleCastParentheses: false # C 风格转换括号内不加空格
SpacesInLineCommentPrefix: # 行注释前的空格
    Minimum: 1
    Maximum: -1
SpacesInParentheses: false # 括号内不加空格
SpacesInSquareBrackets: false # 方括号内不加空格
SpaceBeforeSquareBrackets: false # 方括号前不加空格
BitFieldColonSpacing: Both # 位字段的冒号空格
Standard: Auto # 自动检测标准
StatementAttributeLikeMacros: # 类似语句属性的宏
    - Q_EMIT
StatementMacros: # 语句宏
    - Q_UNUSED
    - QT_REQUIRE_VERSION
TabWidth: 8 # Tab 宽度
UseCRLF: false # 不使用 CRLF 换行
UseTab: Never # 不使用 Tab 缩进
WhitespaceSensitiveMacros: # 对空格敏感的宏
    - STRINGIZE
    - PP_STRINGIZE
    - BOOST_PP_STRINGIZE
    - NS_SWIFT_NAME
    - CF_SWIFT_NAME
---
```



# 格外的注意

**因为参数类型过多，你可以参考我的文件，并且结合多种工具以及文档来自定义你的格式化方式**

### summary Clang-Format **风格选项官方文档**

​	[turn0search2]("https://clang.llvm.org/docs/ClangFormatStyleOptions.htm")



### 其他教程文档

[VS Code + Clang-format 格式化代码](https://zhuanlan.zhihu.com/p/356143396)

[使用 clang-format 进行 C++ 代码风格管理](https://zhuanlan.zhihu.com/p/514541589)

[Clang-Format用法详解](https://zhuanlan.zhihu.com/p/641846308)

