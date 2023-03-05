<div align="center">

<img src="https://raw.githubusercontent.com/HasanEltantawy/RegxHarvester/main/assets/icon.png" alt='RegxHarvester logo' height=100/>

# Regx Harvester

[![version](https://img.shields.io/badge/version-0.0.2-gray.svg)](https://github.com/HasanEltantawy/TemplaGen/)

Configure once harvest everywhere.

<div align="left">

## Be careful

- Extension is under development
- Please save your work before using it.

## How it works?

- `First` u should select template to harvest with Then magic happened.

- First collect all files in workspace.
- Get only the folders u defined in `foldersToIncludes`.
- Exclude any folder contains any of `foldersToExcludes` in it path.
- Get only files that end with any item u defined in `extsToIncludes`.
- Exclude files which end with any item u defined in `extsToExcludes`.
- Then it extract all text that match any regx from `regxToIncludes`.
- Then exclude all text that match any regx from `regxToExcludes`.

## Avaliable commands

- `Harvest Workspace`
  - to harvest all workspace
  - Accessible for command palette
- `Harvest Folder`
  - to harvest selected folder
  - Accessible for command palette & Right click folder
- `Harvest File`
  - to harvest selected file
  - Accessible for command palette & Right click file
- `Harvest Text`
  - to harvest sleceted text
  - Accessible for command palette
- `Hravest Replace`
  - to replace harvested string with defined replaceTemplate
  - Accessible for command palette
- `Harvest Reverse Replace`
  - to reverse replace harvested string with defined replaceTemplate
  - Accessible for command palette
- `Harvest Choose Template`
  - to choose template to harvest with
  - Accessible for command palette

# Definitions

## TemplateBase

The base template for harvesting regular expressions and generating localized strings. Includes the following properties:

- `templateName` (string): The name of the template.
- `regxToIncludes` (array of regx): Regular expressions to include for harvesting.
- `regxToExcludes` (array of regx): Regular expressions to exclude from selected regular expressions.
- `extsToIncludes` (array of strings): File extensions to include for harvesting.
- `extsToExcludes` (array of strings): File extensions to exclude from selected files.
- `foldersToIncludes` (array of strings): Folders to include for harvesting.
- `foldersToExcludes` (array of strings): Folders to exclude from selected folders.
- `outputPath` (string): The output path of the generated file.
- `outputFileName` (string): The output file name (e.g. AppString.dart).
- `outputFileTemplate` (string): The output file body template (e.g. class AppString{\n<{body}>\n}).
- `stringTemplate` (string): The string template that will be stored in the generated file (e.g. static const String <{key}> = <{value}>).
- `replaceTemplate` (string): The template that will be used to replace the - string in the original files (e.g. AppString.<{key}>).
- `templateKeyConfig` (templateKeyConfig): The configuration for generated keys.
- `replaceAfterCreate` (boolean): Whether to replace text after harvesting with replaceTemplate.

## Regx

Regular expression properties:

- `source` (string): The regular expression pattern.
- `flags` (string): The regular expression flags.

## TemplateKeyConfig

Configuration for generated keys. Includes the following properties:

- `keyCase` (string): The key case (e.g. camelCase, capitalCase, etc.).
- `keyConfigs` (array of keyConfig): An array of key configurations.

## KeyConfig

Configuration for generated keys. Includes the following properties:

- `regx` (regx): The regular expression to be applied to the generated key that matches it.
- `replaceWith` (string): The string to replace the generated key with. Can include <{key}> to be replaced with the key.

## Avaliable cases

- `camelCase`
- `capitalCase`
- `constantCase`
- `dotCase`
- `headerCase`
- `noCase`
- `paramCase`
- `pascalCase`
- `pathCase`
- `sentenceCase`
- `snakeCase`

## How to setup your own template?

- Open vscode settings
- search for `Regx Harvest`
- Templates `edit in settings.json`
- for example:

  ```
  {
    "templateName": "Flutter String Harvester",
    "regxToIncludes": [
      {
        "source": "(['\"])(?:(?!\\1).)*\\1",
        "flags": "g"
      }
    ],
    "regxToExcludes": [
      {
        "source": "\\$",
        "flags": ""
      },
      {
        "source": "['\"]dart:.*[\"']",
        "flags": ""
      },
      {
        "source": "['\"]package:.*.dart[\"']",
        "flags": ""
      },
    ],
    "extsToIncludes": [
      ".dart"
    ],
    "extsToExcludes": [
      ".g.dart",
      "app_string.dart"
    ],
    "foldersToIncludes": [
      "lib"
    ],
    "outputPath": "lib/resources/",
    "outputFileName": "app_string.dart",
    "outputFileTemplate": "class AppString{\n<{body}>\n}\n",
    "stringTemplate": "static const String <{key}> = <{value}> ;\n",
    "replaceTemplate": "AppString.<{key}>",
    "templateKeyConfig": {
      "keyCase": "camelCase",
      "keyConfigs": [
        {
          "regx": {
            "source": "^\\d",
            "flags": ""
          },
          "replaceWith": "anHarvestedNum<{key}>"
        },
        {
          "regx": {
            "source": "^$",
            "flags": ""
          },
          "replaceWith": "aHarvestedText"
        }
      ]
    },
    "replaceAfterCreate": false
  }
  ```

<div align="center">

<img src="https://raw.githubusercontent.com/HasanEltantawy/RegxHarvester/main/assets/7t.png" alt='Hassan Eltantawy logo' width="400"/>
