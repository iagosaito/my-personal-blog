
# iagosaito.com

[![Hugo Version](https://img.shields.io/badge/Hugo-v0.170.1-blue.svg)](https://gohugo.io)
[![Go Version](https://img.shields.io/badge/Go-v1.23.4-blue.svg)](https://golang.org/dl/)
[![PaperMod Theme](https://img.shields.io/badge/PaperMod-master-blue)](https://adityatelange.github.io/hugo-PaperMod/)
[![Website](https://img.shields.io/badge/Website-iagosaito.com-white)](https://www.iagosaito.com)

In a world where nobody reads anymore, I'm keeping on writing. You can access my thoughts on the blog at https://www.iagosaito.com.

## Setup and Installation

To get a local copy of this blog running, follow these steps:

1. **Install dependencies**:

   To start this project, you must have [Hugo](https://gohugo.io/getting-started/installing/) and [Go](https://golang.org/doc/install) installed. Verify the badges at the top of this README to check the versions.

2. **Update PaperMod submodule theme**
    ```bash
    cd /themes/PaperMod
    git submodule update --init --recursive
    ```
3. **Run the development server**:

   ```bash
   hugo server
   ```

   Your site should be running at [http://localhost:1313](http://localhost:1313).

## Languages

The site is available in Portuguese (default, served at `/`), Spanish (`/es/`) and English (`/en/`), using Hugo's [multilingual mode](https://gohugo.io/content-management/multilingual/). Languages, per-language menus and the home text are configured under `languages` in `config.yml`.

Each post is a folder (a [page bundle](https://gohugo.io/content-management/page-bundles/)) with one file per language and the post's images:

```
content/posts/my-post/
├── index.md       # Portuguese (default)
├── index.es.md    # Spanish
├── index.en.md    # English
└── diagram.png    # shared by all languages
```

Hugo links the `index.*.md` files of a folder as translations of each other. Keep `date`, `tags` and `categories` identical across them. A post without a translation shows up only in its own language.

UI strings that aren't provided by the PaperMod theme live in `i18n/<lang>.yaml`.

Visitors who open the home page (`/`) are sent to their browser's language (`/en/` or `/es/`) when the site has it, unless they already picked a language in the header switcher, which is remembered. Posts and other deep links are never redirected, and crawlers always get the Portuguese home. See `layouts/_partials/extend_head.html`.

## Images

Put a post's images in its folder and reference them by file name, with the caption as the title:

```markdown
![What the image shows](diagram.png "Image 1 — Caption shown below the image")
```

The render hook in `layouts/_markup/render-image.html` turns this into a `<figure>` with a caption and resized WebP versions (`srcset`), so readers download only the size their screen needs. Only the versions a page uses are published. JPEG, PNG and WebP are resized; GIF and SVG are served as-is.

## Hosting

This blog is hosted by [Netlify](https://www.netlify.com/).