
# iagosaito.com

[![Hugo Version](https://img.shields.io/badge/Hugo-v0.140.0--DEV-blue.svg)](https://gohugo.io)
[![Go Version](https://img.shields.io/badge/Go-v1.23.4-blue.svg)](https://golang.org/dl/)
[![PaperMod Theme](https://img.shields.io/badge/PaperMod-v8.0-blue)](https://adityatelange.github.io/hugo-PaperMod/)
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

## Hosting

This blog is hosted by [Netlify](https://www.netlify.com/).