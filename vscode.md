Example of User settings:
```json
{
  "security.workspace.trust.untrustedFiles": "open",
  "editor.acceptSuggestionOnCommitCharacter": false,
  "editor.acceptSuggestionOnEnter": "smart",
  "editor.quickSuggestions": {
    "other": "off",
    "comments": "off",
    "strings": "off"
  },
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[json]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "workbench.iconTheme": "vscode-icons",
  "diffEditor.ignoreTrimWhitespace": false,
  "[xml]": {
    "editor.defaultFormatter": "redhat.vscode-xml"
  },
  "claptrap.modules.isomorph.projectPath": "c:\\dev\\isomorph",
  "claptrap.modules.graphql.projectPath": "c:\\dev\\GraphQL",
  "claptrap.configConnectionString": "Endpoint=<claptrap endpoint, proprietary>",
  "gitlens.hovers.currentLine.over": "line",
  "workbench.colorCustomizations": {
    "titleBar.activeBackground": "#E4C07A",
    "titleBar.inactiveBackground": "#94790d",
    "statusBar.background": "#B58900"
  },
  "terminal.integrated.defaultProfile.windows": "PowerShell",
  "workbench.colorTheme": "Quiet Light",
  "vscode-pets.petSize": "large",
  "vscode-pets.petType": "zappy",
  "vscode-pets.theme": "beach",
  "claptrap.configEndpoint": "Endpoint=<claptrap endpoint, proprietary>",
  "telemetry.telemetryLevel": "off",
  "gitlens.telemetry.enabled": false,
  "redhat.telemetry.enabled": false,
  "[javascriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "editor.accessibilitySupport": "off",
  "[typescriptreact]": {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[jsonc]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescript]": {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[plaintext]": {
    "editor.inlineSuggest.enabled": false,
    "editor.wordBasedSuggestions": "off",
    "editor.quickSuggestions": {
        "other": "off",
        "comments": "off",
        "strings": "off"
    }
  },
  "typescript.updateImportsOnFileMove.enabled": "always"
}

```

Another example:
- do not double-click file title to keep the file open
- create file extension associations to languages
- create language associtations to file encodings
- you can also use `workbench.colorCustomizations` in workspace settings, so that  when you go to the command `Open Workspace Settings (JSON)`, so that, e.g., each project colors VS Code differently
  
```
{
    "workbench.colorTheme": "Quiet Light",
    "security.workspace.trust.untrustedFiles": "open",
    "hg.useBookmarks": true,
    "hg.lineAnnotationEnabled": true,
    // do not need to double click file to keep it open
    "workbench.editor.enablePreview": false,
    "[plaintext]": {
        "editor.quickSuggestions": {
            "other": "off",
            "comments": "off",
            "strings": "off"
        },
    },
    "files.associations": {
        "*.rc": "rc-script",
        "*.versioninfo": "rc-script",
        "*.iss": "innosetup"
    },
    "[innosetup]": {
        "files.encoding": "windows1252"
    },
    "[rc-script]": {
        "files.encoding": "windows1252"
    },
    "[ini]": {
        "editor.quickSuggestions": {
            "other": "off",
            "comments": "off",
            "strings": "off"
        }
    },
    "python.languageServer": "Pylance",
    "[python]": {
        "files.encoding": "windows1252",
        "editor.defaultFormatter": "charliermarsh.ruff"
    },
    "[pascal]": {
        "files.encoding": "windows1252"
    },
    "[objectpascal]": {
        "files.encoding": "windows1252"
    },
    "pascal.codeNavigation": "file",
    "pascal.tags.autoGenerate": false,
    "telemetry.telemetryLevel": "off",
    "dotnetAcquisitionExtension.enableTelemetry": false,
    "github.copilot.editor.enableAutoCompletions": true
}
```
