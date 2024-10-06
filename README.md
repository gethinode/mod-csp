# Hinode Module - Content Security Policies

<!-- Tagline -->
<p align="center">
    <b>A Hugo module to generate Content Security Policies for your Hinode site (work in progress)</b>
    <br />
</p>

<!-- Badges -->
<p align="center">
    <a href="https://gohugo.io" alt="Hugo website">
        <img src="https://img.shields.io/badge/generator-hugo-brightgreen">
    </a>
    <a href="https://gethinode.com" alt="Hinode theme">
        <img src="https://img.shields.io/badge/theme-hinode-blue">
    </a>
    <a href="https://github.com/gethinode/mod-csp/commits/main" alt="Last commit">
        <img src="https://img.shields.io/github/last-commit/gethinode/mod-csp.svg">
    </a>
    <a href="https://github.com/gethinode/mod-csp/issues" alt="Issues">
        <img src="https://img.shields.io/github/issues/gethinode/mod-csp.svg">
    </a>
    <a href="https://github.com/gethinode/mod-csp/pulls" alt="Pulls">
        <img src="https://img.shields.io/github/issues-pr-raw/gethinode/mod-csp.svg">
    </a>
    <a href="https://github.com/gethinode/mod-csp/blob/main/LICENSE" alt="License">
        <img src="https://img.shields.io/github/license/gethinode/mod-csp">
    </a>
</p>

## About

![Logo](https://raw.githubusercontent.com/gethinode/hinode/main/static/img/logo.png)

Hinode is a clean blog theme for [Hugo][hugo], an open-source static site generator. Hinode is available as a [template][repository_template], and a [main theme][repository]. This repository generates the site's server headers including content security policies. Visit the Hinode documentation site for [installation instructions][hinode_docs].

## Contributing

This module uses [semantic-release][semantic-release] to automate the release of new versions. The package uses `husky` and `commitlint` to ensure commit messages adhere to the [Conventional Commits][conventionalcommits] specification. You can run `npx git-cz` from the terminal to help prepare the commit message.

## Configuration

This module generates the server headers including [Content Security Policies][csp] for a Hinode site. Templates are available for Netlify and the hugo server.

Define the output files in your site configuration (typically `hugo.toml`). The following example defines two outputs generated in the build folder (usually `public`).

```toml
[outputFormats]
  [outputFormats.headers]
    mediaType = "application/toml"
    baseName = "netlify"
    isPlainText = true
    notAlternative = true
    permalinkable = true
  [outputFormats.server]
    mediaType = "application/toml"
    baseName = "server"
    isPlainText = true
    notAlternative = true
    permalinkable = true

[outputs]
home = ["headers", "server"]
```

Define the default (starter) policy in `data/server.toml`.

 This module supports the following parameters (see the section `params.headers` in `config.toml`):

| Setting                   | Default | Description |
|---------------------------|---------|-------------|
| `headers.<output>.source` |         | Defines an additional source file to be merged with the output. The source file should be defined in the `data` folder. Supported data formats are `JSON`, `TOML`, `YAML`, and `XML`.

You can define Content Security Policies for each Hinode module. Hinode will merge these policies for each included module (either `core`, `optional`, or `critical`). Define each directive as an array type. Please refer to the [Quick Reference Guide][csp] for the available directives and supported values.

The following example defines the policies for `script-src` and `style-src` for the module `example`.

```toml
[params.modules.example.csp]
    script-src = [
        "//two.com",
        "https:"
    ]
    style-src = [
        "'self'",
        "'sha256-456'"
    ]
```

<!-- MARKDOWN LINKS -->
[hugo]: https://gohugo.io
[hinode_docs]: https://gethinode.com
<!-- [module]: https://example.com -->
[csp]: https://content-security-policy.com
[repository]: https://github.com/gethinode/hinode.git
[repository_template]: https://github.com/gethinode/template.git
[conventionalcommits]: https://www.conventionalcommits.org
[husky]: https://typicode.github.io/husky/
[semantic-release]: https://semantic-release.gitbook.io/
