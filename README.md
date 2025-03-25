# gh-pages-template
A GitHub pages template based on [minimal Jekyll theme.](https://github.com/pages-themes/minimal)
Couple of additional futures such as a navigation bar and a full page layout are added to the minimal theme.

- [Preview the theme](https://kbsezginel.github.io/gh-pages-template/)
- [See the original theme in action](https://pages-themes.github.io/minimal/)

## Usage
See [setup and customization instructions](https://kbsezginel.github.io/gh-pages-template/setup) to start using the theme.

---

## Jekyll Setup

To set up Jekyll locally for development:

1. Install Ruby and Jekyll:
    ```bash
    # Install Ruby (if not already installed)
    # On macOS:
    brew install ruby
    
    # On Ubuntu/Debian:
    sudo apt-get install ruby ruby-dev build-essential
    
    # Install Jekyll and Bundler
    gem install jekyll bundler
    ```

2. Clone this repository:
    ```bash
    git clone https://github.com/yourusername/gh-pages-template.git
    cd gh-pages-template
    ```

3. Install dependencies:
    ```bash
    bundle install
    ```

4. Run the site locally:
    ```bash
    bundle exec jekyll serve
    ```

5. Open your browser and navigate to `http://localhost:4000`

---

## Basic Jekyll Commands

### Adding a New Page

1. Create a new markdown file in the root directory:
    ```bash
    touch newpage.md
    ```

2. Add the front matter at the top:
    ```yaml
    ---
    layout: page
    title: My New Page
    permalink: /newpage/
    ---
    ```

### Adding a New Post

1. Create a new file in the `_posts` directory with the format `YYYY-MM-DD-title.md`:
    ```bash
    touch _posts/$(date +%Y-%m-%d)-my-new-post.md
    ```

2. Add front matter to the post:
    ```yaml
    ---
    layout: post
    title: "My New Post"
    date: YYYY-MM-DD HH:MM:SS -0000
    categories: category-name
    ---
    ```

### Previewing Your Site

```bash
# Start Jekyll server with drafts enabled
bundle exec jekyll serve --drafts

# Build the site without serving
bundle exec jekyll build

# Serving with live reload
bundle exec jekyll serve --livereload
```

---

This is a personal blog-ish site.