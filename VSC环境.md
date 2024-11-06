# vscode setting.json

### 关键设置解释

1. **`C_Cpp.default.compileCommands`**:
   - 路径设置为 `${workspaceFolder}/build/compile_commands.json`，用于启用 C++ 扩展的头文件和编译选项解析。这个文件在CMake构建时生成，提供VS Code代码补全、跳转和错误提示。

2. **用户界面相关**：
   - **主题**：`workbench.colorTheme` 设置为 `"Eva Light Italic Bold"`。
   - **图标主题**：`workbench.iconTheme` 设置为 `material-icon-theme`。
   - **文件拖放确认**和**删除确认**被关闭，分别通过 `explorer.confirmDragAndDrop` 和 `explorer.confirmDelete` 设置为 `false`。

3. **格式化设置**：
   - **C++格式化**：`clang-format` 被设置为默认格式化程序，基于 `Google` 风格，我同时增加了自定义配置。
   - **Python格式化**：使用 `Prettier` 作为 Python 文件的默认格式化程序。
   - **自动格式化**：`editor.formatOnSave` 设置为 `true`，表示保存时自动格式化文件。

4. **拼写检查（cSpell）**：
   - 拼写检查字典中包含了常用的C++和ROS库/函数名，例如 `rclcpp`、`iostream`、`cmath`、`xaver` 等，以减少编辑器的拼写错误提示。
   - 你可以套用这份字典，然后添加你的正确词
   
5. **C++ 文件关联**：
   - `files.associations` 中指定了很多C++标准库的头文件，确保VS Code能正确识别这些文件为C++代码，提升代码补全和跳转体验。

6. **终端和其他配置**：
   - **多行粘贴警告**：`terminal.integrated.enableMultiLinePasteWarning` 设置为 `"never"`，让您粘贴多行内容时不会弹出确认框。
   - **代码运行**：`code-runner.runInTerminal` 设置为 `true`，确保在终端中运行代码，而不是在输出面板中。

### 检查配置是否适用

这份配置是全局配置，适用于所有项目和工作区。若要确保它适用于每个项目，请确保：

- **每个项目使用CMake构建**，并生成 `compile_commands.json` 文件。这样可以让 `C_Cpp.default.compileCommands` 自动解析。
- **每个工作区包含 `.vscode` 文件夹**，在该文件夹中可以单独设置 `settings.json`，覆盖全局设置。
