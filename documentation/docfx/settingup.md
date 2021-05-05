# Setting up **DocFX**

DocFX is an API documentation generator for .NET, which currently supports C#, VB and F#. It generates API reference documentation from triple-slash comments in your source code. It also allows you to use Markdown files to create additional topics such as tutorials and how-tos, and to customize the generated reference documentation. DocFX builds a static HTML website from your source code and Markdown files, which can be easily hosted on any web server (for example, github.io). Also, DocFX provides you the flexibility to customize the layout and style of your website through templates.

DocFX also has the following cool features:

- Integration with your source code. You can click "View Source" on an API to navigate to the source code in GitHub (your source code must be pushed to GitHub).
- Cross-platform support. We have an exe version that runs natively on Windows and with Mono it can also run on Linux and macOS.
- Integration with Visual Studio. You can seamlessly use DocFX within Visual Studio.
- Markdown extensions. We introduced DocFX Flavored Markdown(DFM) to help you write API documentation. DFM is 100% compatible with GitHub Flavored Markdown(GFM) with some useful extensions, like file inclusion, code snippet, cross reference, and yaml header. For a detailed description about DFM, please refer to [DFM](../markdown/flavored_markdown.md).

> [!WARNING]
> **Prerequisites** [Visual Studio 2019](https://www.visualstudio.com/downloads/) is needed for DocFX metadata msbuild projects. It's not required when generating metadata directly from source code (.cs, .vb) or assemblies (.dll)

## Use DocFX as a command-line tool

### Downloading DocFX

1. Download DocFX from [GitHub](https://github.com/dotnet/docfx/releases)
1. Extract **docfx.zip** to a local folder
1. Add it to **PATH** so you can run it anywhere

### Create a project

1. Navigate to a folder of your choice
1. Right-click and select **Open with Code**
1. Within **Visual Studio Code**, Create a new Terminal Window (``CTRL + SHIFT + '``)
1. Within the Terminal, type ``docfx init -q``
1. The command generates a default project named ``docfx_project``

### Build the website

1. Within the Terminal, type ``docfx docfx_project\docfx.json --serve``
2. Now you can view the generated website on [http://localhost:8080](http://localhost:8080)

### Updating the project

1. Open **index.md**
1. Make a small change and save the document
1. Within **Visual Studio Code**, Create a new Terminal Window (``CTRL + SHIFT + '``)
1. Within the Terminal, type ``docfx docfx_project\docfx.json``
1. Goto your browser and refresh the website and refresh the page

> [!WARNING]
> Keep the originol Terminal open as this is the local lite webserver
> When making any changes, use the command ``docfx docfx_project\docfx.json`` and refresh the website within your browser

## Adding a **Template** to your website

The following will add **DiscordFX** template to your website. This will make the website look and feel like [Discord](https://discord.com/developers/docs/intro) documentation portal

1. Download the source or the zipped file from the [releases page](https://github.com/jbltx/DiscordFX/releases)
1. In your DocFX project folder, create a new directory named ``templates``, if it doesn't already exist
1. Copy the discordfx folder from this repository into your templates folder
1. In your `docfx.json` configuration file, add `templates/discordfx` path into `build.template` property

```json
    {
        "build": {
            "template": ["default", "templates/discordfx"]
        }
    }
```

1. Within the Terminal, type ``docfx docfx_project\docfx.json``
1. Goto your browser and refresh the website and refresh the page

> [!TIP]
> For more templates, see [Templates](https://dotnet.github.io/docfx/templates-and-plugins/templates-dashboard.html)

### Working Template

```json
{
    "metadata": [
        {
            "src": [
                {
                    "files": [
                        "src/**.csproj"
                    ]
                }
            ],
            "dest": "api",
            "disableGitFeatures": true,
            "disableDefaultFilter": false
        }
    ],
    "build": {
        "content": [
            {
                "files": [
                    "api/**.yml",
                    "api/index.md"
                ]
            },
            {
                "files": [
                    "articles/**.md",
                    "articles/**/toc.yml",
                    "toc.yml",
                    "*.md"
                ]
            }
        ],
        "resource": [
            {
                "files": [
                    "images/**"
                ]
            }
        ],
        "overwrite": [
            {
                "files": [
                    "apidoc/**.md"
                ],
                "exclude": [
                    "obj/**",
                    "_site/**"
                ]
            }
        ],
        "dest": "_site",
        "disableGitFeatures": true,
        "disableDefaultFilter": false,
        "globalMetadataFiles": [],
        "fileMetadataFiles": [],
        "template": [
            "default"
        ],
        "postProcessors": [],
        "markdownEngineName": "markdig",
        "noLangKeyword": false,
        "keepFileLink": false,
        "cleanupCacheHistory": false,
        "globalMetadata": {
            "_appTitle": "DocFX website",
            "_appFooter": "&#0169; 2021 Jason Rose",
            "_enableSearch": "true",
            "_disableContribution": "true",
            "_disableAffix": "false"
        }
    }
}
```