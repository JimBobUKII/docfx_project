# DocFX Overview

DocFX is an API documentation generator for .NET, which currently supports C#, VB and F#. It generates API reference documentation from triple-slash comments in your source code. It also allows you to use Markdown files to create additional topics such as tutorials and how-tos, and to customize the generated reference documentation. DocFX builds a static HTML website from your source code and Markdown files, which can be easily hosted on any web server (for example, github.io). Also, DocFX provides you the flexibility to customize the layout and style of your website through templates.

DocFX also has the following cool features:

- Integration with your source code. You can click "View Source" on an API to navigate to the source code in GitHub (your source code must be pushed to GitHub).
- Cross-platform support. We have an exe version that runs natively on Windows and with Mono it can also run on Linux and macOS.
- Integration with Visual Studio. You can seamlessly use DocFX within Visual Studio.
- Markdown extensions. We introduced DocFX Flavored Markdown(DFM) to help you write API documentation. DFM is 100% compatible with GitHub Flavored Markdown(GFM) with some useful extensions, like file inclusion, code snippet, cross reference, and yaml header. For a detailed description about DFM, please refer to [DFM](../markdown/flavored_markdown.md).

> [!WARNING]
> **Prerequisites** [Visual Studio 2019](https://www.visualstudio.com/downloads/) is needed for DocFX metadata msbuild projects. It's not required when generating metadata directly from source code (.cs, .vb) or assemblies (.dll)