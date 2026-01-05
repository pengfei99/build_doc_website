# build_doc_website

In this repo, we will learn:
1. how to build a documentation website with [MkDocs](https://www.mkdocs.org/).
2. how to serve this website via `GitHub pages`.

## 1. Introduction of Mkdocs

MkDocs is a simple `static site generator` that can build project documentation. Documentation source files are 
written in `Markdown`, and configured with a single `YAML configuration file`. 

It also supports `GitHub pages` deployment natively.

## 2. Getting started with mkdocs

The official [doc](https://www.mkdocs.org/getting-started/) is great. I just make it shorted for like 5 minutes.

### 2.1 Install the required packages

Here we use uv to build the python env and install packages

```shell
uv init <project-name>

# edit the pyproject.toml

# add the required packages
uv add mkdocs mkdocs-material

# activate the .venv and check mkdocs version
mkdocs --version

# you should see somthing like
(build-doc-website) PS C:\Users\pliu\Documents\git\build_doc_website> mkdocs --version
mkdocs, version 1.6.1 from C:\Users\pliu\Documents\git\build_doc_website\.venv\Lib\site-packages\mkdocs (Python 3.14)

# create a new documentation project
mkdocs new my_docs
```

The `mkdocs new my_docs` command will create a doc folder like below

```text
my_docs/
├── docs/
│   └── index.md
├── mkdocs.yml   # configure the behavior of mkdocs(e.g. theme, nav, plugins, etc.)
└── site/        # generated later
```

### 2.2 Configure mkdocs

The below yaml file is an example of the mkdocs configuration. 

```yaml
site_name: Pengfei Documentation

theme:
  name: material
  features:
    - navigation.instant
    - search.suggest
    - search.highlight

plugins:
  - search

markdown_extensions:
  - admonition
  - toc:
      permalink: true
  - codehilite

nav:
  - Home: index.md
  - dev_ops:
      - Installation: devops/install.md
      - Configuration: devops/config.md
  - data_management:
      - Tuning: data_management/tuning.md
      - FAQ: data_management/faq.md
```

The `nav` section defines the organization bar of the documentation website. Your docs should be organized as below
```text
my_docs/
├── docs/
    ├── devops
         ├── install.md
    │    └── config.md
    ├── data_management
         ├── tuning.md
         └── faq.md
│   └── index.md
├── mkdocs.yml   # configure the behavior of mkdocs(e.g. theme, nav, plugins, etc.)
└── site/        # generated later
```

> Without nav, MkDocs auto-orders files alphabetically. With many files, explicit navigation is essential.

### 2.3 Live Preview of your doc website

If you have entered something in your markdown files, you can now preview the doc website with the below command

```shell
mkdocs serve
```

> You should be able to visit your website via `http://127.0.0.1:8000`. Beware, the content of the page are not updated
> dynamically, you need to stop/start to see the diff after content change.


### 2.4 Built in search bar

The mkdocs use a `json file(search_index.json)` to store all searchable index.

What gets indexed:
- Page titles
- Headings
- Paragraph text

What does not get indexed:
- HTML comments
- Disabled sections

Search index location after build: `site/search/search_index.json`

### 2.5 Build Static HTML Site

You can use the below command to build the Static HTML Site.

```shell
mkdocs build

Output:

site/
├── index.html
├── install/
│   └── index.html
├── assets/
└── search/
```

> This folder is fully static and deployable.

## 3. Deploying your mkdocs via github pages

The official doc is [here](https://www.mkdocs.org/user-guide/deploying-your-docs/).


