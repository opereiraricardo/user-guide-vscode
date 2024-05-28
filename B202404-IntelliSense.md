# IntelliSense

IntelliSense is a general term for various code editing features including: code completion, parameter info, quick info, and member lists. IntelliSense features are sometimes called by other names such as "code completion", "content assist", and "code hinting."

![Foto do vscode](https://code.visualstudio.com/assets/docs/editor/intellisense/intellisense.gif)



## IntelliSense for your programming language
Visual Studio Code IntelliSense is provided for JavaScript, TypeScript, JSON, HTML, CSS, SCSS, and Less out of the box. VS Code supports word based completions for any programming language but can also be configured to have richer IntelliSense by installing a language extension.

Below are the most popular language extensions in the Marketplace. Select an extension tile below to read the description and reviews to decide which extension is best for you.



<a href="https://marketplace.visualstudio.com/items?itemName=ms-python.python"> <img src="https://media.discordapp.net/attachments/764887709520625697/1244791533241368587/python.png?ex=665665f4&is=66551474&hm=f6dbf0588e4d2430b4cca3147164b0291507692466b0c20edd7eb578eb6b9023&=&format=webp&quality=lossless&width=276&height=250" width="150px"> </a>   | <a href="https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools"> <img src="https://media.discordapp.net/attachments/764887709520625697/1244793617269264414/Captura_de_tela_2024-05-27_193938.png?ex=665667e5&is=66551665&hm=9356fd7a7f8cd2facd4a27355239b3bdfd7436f36cfdf14d4d6d20dab096c5bd&=&format=webp&quality=lossless&width=270&height=238" width="150px"> </a> | <a href="https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp"> <img src="https://media.discordapp.net/attachments/764887709520625697/1244793617072128040/Captura_de_tela_2024-05-27_194022.png?ex=665667e5&is=66551665&hm=7438dd923104e2429bd73a74ba3a05d4d16576aee28c4bb96527c086ee5e8cb4&=&format=webp&quality=lossless&width=261&height=233" width="150px"> </a>  |<a href="https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack"> <img src="https://media.discordapp.net/attachments/764887709520625697/1244793616896098355/Captura_de_tela_2024-05-27_194051.png?ex=665667e5&is=66551665&hm=ab6fb6a4303c82fcf372c6669deda70a5d69e419cc774dfe843dcde480e37e81&=&format=webp&quality=lossless&width=255&height=240" width="150px"> </a> |
| -------- | ----- | ----------- | ---------|
<a href="https://marketplace.visualstudio.com/items?itemName=golang.Go"> <img src="https://media.discordapp.net/attachments/764887709520625697/1244793616694513764/Captura_de_tela_2024-05-27_194115.png?ex=665667e5&is=66551665&hm=09d50f669beae45c408383045f6acfe0c5cbcd387c180c7d6439b89c383b4f5a&=&format=webp&quality=lossless&width=270&height=241" width="150px"> </a>  |<a href="https://marketplace.visualstudio.com/items?itemName=Dart-Code.dart-code"> <img src="https://media.discordapp.net/attachments/764887709520625697/1244793616359231559/Captura_de_tela_2024-05-27_194136.png?ex=665667e5&is=66551665&hm=033ee985c4cc7550f505c5262cd4ad5c40e8bc521bc13ed09cb12974ad03eacb&=&format=webp&quality=lossless&width=265&height=228" width="150px"> </a> | <a href="https://marketplace.visualstudio.com/items?itemName=xdebug.php-pack"> <img src="https://media.discordapp.net/attachments/764887709520625697/1244793616040198227/Captura_de_tela_2024-05-27_194206.png?ex=665667e5&is=66551665&hm=3aca9f5c66759e0f470c1249b8364d86df77df3e3f48c98f170b59fc6eef002a&=&format=webp&quality=lossless&width=250&height=232" width="150px"> </a> |<a href="https://marketplace.visualstudio.com/items?itemName=Shopify.ruby-lsp"> <img src="https://media.discordapp.net/attachments/764887709520625697/1244793615574634606/Captura_de_tela_2024-05-27_194227.png?ex=665667e5&is=66551665&hm=30bd62bb8db5fa668b38afead52ede3fb8c2780eefa5779eecc4e2f38bf770d1&=&format=webp&quality=lossless&width=261&height=238" width="150px"> </a>


## IntelliSense features
VS Code IntelliSense features are powered by a language service. A language service provides intelligent code completions based on language semantics and an analysis of your source code. If a language service knows possible completions, the IntelliSense suggestions will pop up as you type. If you continue typing characters, the list of members (variables, methods, etc.) is filtered to only include members containing your typed characters. Pressing **Tab** or **Enter** will insert the selected member.

You can trigger IntelliSense in any editor window by typing **Ctrl+Space** or by typing a trigger character (such as the dot character (**.**) in JavaScript).

![Foto do vscode](https://code.visualstudio.com/assets/docs/editor/intellisense/intellisense_packagejson.gif)
>**Tip**: The suggestions widget supports CamelCase filtering, meaning you can type the letters which are upper cased in a method name to limit the suggestions. For example, "cra" will quickly bring up "createApplication".

If you prefer, you can turn off IntelliSense while you type. See Customizing IntelliSense below to learn how to disable or customize VS Code's IntelliSense features.

As provided by the language service, you can see quick info for each method by either pressing **Ctrl+Space** or clicking the info icon. The accompanying documentation for the method will now expand to the side. The expanded documentation will stay so and will update as you navigate the list. You can close this by pressing **Ctrl+Space** again or by clicking on the close icon.

![seiLa](https://code.visualstudio.com/assets/docs/editor/intellisense/intellisense_docs.gif)

After choosing a method you are provided with parameter info.

![naoSei](https://code.visualstudio.com/assets/docs/editor/intellisense/paramater_info.png)

When applicable, a language service will surface the underlying types in the quick info and method signatures. In the image above, you can see several **any** types. Because JavaScript is dynamic and doesn't need or enforce types, **any** suggests that the variable can be of any type.

## Types of completions
The JavaScript code below illustrates IntelliSense completions. IntelliSense gives both inferred proposals and the global identifiers of the project. The inferred symbols are presented first, followed by the global identifiers (shown by the Word icon).

![itsTheBoys](https://code.visualstudio.com/assets/docs/editor/intellisense/intellisense_icons.png)
VS Code IntelliSense offers different types of completions, including language server suggestions, snippets, and simple word based textual completions.

**Icons** | **Name** | **Symbol Type**
| -------- | ----- | ----------- |
<img src="https://code.visualstudio.com/assets/docs/editor/intellisense/Method_16x.svg" widht="15px"> | Methods and Functions |**method**, **function**, **constructor**
|<img src="https://code.visualstudio.com/assets/docs/editor/intellisense/Variable_16x.svg"> | Variables | **variables** |
| <img src="https://code.visualstudio.com/assets/docs/editor/intellisense/Field_16x.svg"> | Fields | **field** |
| <img src="https://code.visualstudio.com/assets/docs/editor/intellisense/symbol-parameter.svg"> | Type parameters | **typeParameters** |
| <img src="https://code.visualstudio.com/assets/docs/editor/intellisense/symbol-constant.svg"> | Constants | **constant** |
| <img src="https://code.visualstudio.com/assets/docs/editor/intellisense/Class_16x.svg"> | Classes | **class** |
| <img src="https://code.visualstudio.com/assets/docs/editor/intellisense/Interface_16x.svg"> | Interfaces | **interface** |
| <img src="https://code.visualstudio.com/assets/docs/editor/intellisense/symbol-structure.svg"> | Structures | **Struct** |
| <img src="https://code.visualstudio.com/assets/docs/editor/intellisense/symbol-event.svg"> | Events | **event** |
| <img src="https://code.visualstudio.com/assets/docs/editor/intellisense/symbol-operator.svg"> | Operators | **operator** |
| <img src="https://code.visualstudio.com/assets/docs/editor/intellisense/Namespace_16x.svg"> | Modules | **module** |
| <img src="https://code.visualstudio.com/assets/docs/editor/intellisense/Property_16x.svg"> | Properties and Attributes | **property** |
| <img src="https://code.visualstudio.com/assets/docs/editor/intellisense/EnumItem_16x.svg"> | Values and Enumerations | **value, enum** |
| <img src="https://code.visualstudio.com/assets/docs/editor/intellisense/Reference_16x.svg"> | References | **reference** |
| <img src="https://code.visualstudio.com/assets/docs/editor/intellisense/Keyword_16x.svg"> | Keywords | **keyword** |
| <img src="https://code.visualstudio.com/assets/docs/editor/intellisense/symbol-file.svg"> | Files | **file** |
| <img src="https://code.visualstudio.com/assets/docs/editor/intellisense/folder.svg"> | Folders | **folder** |
| <img src="https://code.visualstudio.com/assets/docs/editor/intellisense/ColorPalette_16x.svg"> | Colors | **color** |
| <img src="https://code.visualstudio.com/assets/docs/editor/intellisense/Ruler_16x.svg"> | Unit | **unit** |
| <img src="https://code.visualstudio.com/assets/docs/editor/intellisense/Snippet_16x.svg"> | Snippet prefixes	 | **snippet** |
| <img src="https://code.visualstudio.com/assets/docs/editor/intellisense/String_16x.svg"> | Words | **text** |


## Customizing IntelliSense
You can customize your IntelliSense experience in settings and key bindings.

### Settings
The settings shown below are the default settings. You can change these settings in your **settings.json** file as described in **User and Workspace Settings**.


```
{
    // Controls if quick suggestions should show up while typing
    "editor.quickSuggestions": {
        "other": true,
        "comments": false,
        "strings": false
    },

     // Controls whether suggestions should be accepted on commit characters. For example, in JavaScript, the semi-colon (`;`) can be a commit character that accepts a suggestion and types that character.
    "editor.acceptSuggestionOnCommitCharacter": true,

    // Controls if suggestions should be accepted on 'Enter' - in addition to 'Tab'. Helps to avoid ambiguity between inserting new lines or accepting suggestions. The value 'smart' means only accept a suggestion with Enter when it makes a textual change
    "editor.acceptSuggestionOnEnter": "on",

    // Controls the delay in ms after which quick suggestions will show up.
    "editor.quickSuggestionsDelay": 10,

    // Controls if suggestions should automatically show up when typing trigger characters
    "editor.suggestOnTriggerCharacters": true,

    // Controls if pressing tab inserts the best suggestion and if tab cycles through other suggestions
    "editor.tabCompletion": "off",

    // Controls whether sorting favours words that appear close to the cursor
    "editor.suggest.localityBonus": true,

    // Controls how suggestions are pre-selected when showing the suggest list
    "editor.suggestSelection": "first",

    // Enable word based suggestions
    "editor.wordBasedSuggestions": "matchingDocuments",

    // Enable parameter hints
    "editor.parameterHints.enabled": true,
}
```
### Tab Completion

The editor supports "tab completion" which inserts the best matching completion when pressing **Tab**. This works regardless of the suggest widget showing or not. Also, pressing **Tab** after inserting a suggestions will insert the next best suggestion.

![imagemdaora](https://code.visualstudio.com/assets/docs/editor/intellisense/tabCompletion.gif)

By default, tab completion is disabled. Use the ***editor.tabCompletion*** setting to enable it. These values exist:

* **off** - (default) Tab completion is disabled.
* **on** - Tab completion is enabled for all suggestions and repeated invocations insert the next best suggestion.
* **onlySnippets** - Tab completion only inserts static snippets which prefix match the current line prefix.

### Locality Bonus
Sorting of suggestions depends on extension information and on how well they match the current word you are typing. In addition, you can ask the editor to boost suggestions that appear closer to the cursor position, using the ***editor.suggest.localityBonus*** setting.

![folhaDeSP](https://code.visualstudio.com/assets/docs/editor/intellisense/localitybonus.png)

In above images you can see that **count**, **context**, and **colocated** are sorted based on the scopes in which they appear (loop, function, file).

### Suggestion selection
By default, VS Code pre-selects the first suggestion in the suggestion list. If you'd like different behavior, for example, to always select the most recently used item in the suggestion list, you can use the ***editor.suggestSelection*** setting.

The available ***editor.suggestSelection*** values are:

* **first** - (default) Always select the top list item.
* **recentlyUsed** - The previously used item is selected unless a prefix (type to select) selects a different item.
* **recentlyUsedByPrefix** - Select items based on previous prefixes that have completed those suggestions.

Selecting the most recently used item is very useful as you can quickly insert the same completion multiple times.

"Type to select" means that the current prefix (roughly the text left of the cursor) is used to filter and sort suggestions. When this happens and when its result differs from the result of **recentlyUsed**, it will be given precedence.

When using the last option, **recentlyUsedByPrefix**, VS Code remembers which item was selected for a specific prefix (partial text). For example, if you typed **co** and then selected **console**, the next time you typed **co**, the suggestion **console** would be pre-selected. This lets you quickly map various prefixes to different suggestions, for example **co** -> **console** and **con** -> **const**.

### Snippets in suggestions
By default, VS Code shows snippets and completion proposals in one widget. You can control the behavior with the **editor.snippetSuggestions** setting. To remove snippets from the suggestions widget, set the value to **"none"**. If you'd like to see snippets, you can specify the order relative to suggestions; at the top (**"top"**), at the bottom (**"bottom"**), or inline ordered alphabetically (**"inline"**). The default is **"inline"**.

### Key Bindings
The key bindings shown below are the default key bindings. You can change these in your **keybindings.json** file as described in **Key Bindings**.

>**Note**: There are many more key bindings relating to IntelliSense. Open the **Default Keyboard Shortcuts** (**File > Preferences > Keyboard Shortcuts**) and search for "suggest".
```
[
  {
    "key": "ctrl+space",
    "command": "editor.action.triggerSuggest",
    "when": "editorHasCompletionItemProvider && editorTextFocus && !editorReadonly"
  },
  {
    "key": "ctrl+space",
    "command": "toggleSuggestionDetails",
    "when": "editorTextFocus && suggestWidgetVisible"
  },
  {
    "key": "ctrl+alt+space",
    "command": "toggleSuggestionFocus",
    "when": "editorTextFocus && suggestWidgetVisible"
  }
]
```

# Enhance completions with AI
In VS Code, you can enhance your coding with artificial intelligence (AI), such as suggestions for lines of code or entire functions, fast documentation creation, and help creating code-related artifacts like tests.

**GitHub Copilot** is an AI-powered code completion tool that helps you write code faster and smarter. You can use the **GitHub Copilot extension** in VS Code to generate code, or to learn from the code it generates.

![ai](https://code.visualstudio.com/assets/docs/editor/intellisense/copilot-extension.png)
You can learn more about how to get started with Copilot in the **Copilot documentation**.

# Troubleshooting
If you find IntelliSense has stopped working, the language service may not be running. Try restarting VS Code and this should solve the issue. If you are still missing IntelliSense features after installing a language extension, open an issue in the repository of the language extension.

>**Tip**: For configuring and troubleshooting JavaScript IntelliSense, see the **JavaScript documentation**.

A particular language extension may not support all the VS Code IntelliSense features. Review the extension's README to find out what is supported. If you think there are issues with a language extension, you can usually find the issue repository for an extension through the **VS Code Marketplace**. Navigate to the extension's Details page and select the Support link.

# Next Steps
IntelliSense is just one of VS Code's powerful features. Read on to learn more:

* **JavaScript** - Get the most out of your JavaScript development, including configuring IntelliSense.
* **Node.js** - See an example of IntelliSense in action in the Node.js walkthrough.
* **Debugging** - Learn how to set up debugging for your application.
* **Creating Language extensions** - Learn how to create extensions that add IntelliSense for new programming languages.
* **GitHub Copilot in VS Code** - Learn how to use AI with GitHub Copilot to enhance your coding.

# Common questions
## Why am I not getting any suggestions?
![why](https://code.visualstudio.com/assets/docs/editor/intellisense/intellisense_error.png)

This can be caused by a variety of reasons. First, try restarting VS Code. If the problem persists, consult the language extension's documentation. For JavaScript specific troubleshooting, please see the **JavaScript language topic**.

## Why am I not seeing method and variable suggestions?
![why](https://code.visualstudio.com/assets/docs/editor/intellisense/missing_typings.png)

This issue is caused by missing type declaration (typings) files in JavaScript. You can check if a type declaration file package is available for a specific library by using the **TypeSearch** site. There is more information about this issue in the **JavaScript language topic**. For other languages, please consult the extension's documentation.