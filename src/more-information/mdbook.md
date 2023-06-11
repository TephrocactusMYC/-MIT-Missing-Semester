# WHY mdbook?
Why introduce mdbook? Because I found that in the missing semester course, there was no introduction to modern e-books written based on markdown syntax. Personally, I hope that my notes for these courses can be systematized. Therefore, I will use mdbook to compile all my notes, homework answers and other content into a book. It's as simple as that.

## Other choise?
Yes, I know there are many popular e-book tools, so you can find tools written in almost any language.

Therefore, there are some things you need to pay attention to. Almost every modern and new programming language's electronic book tool will be combined with the language itself in order to show more features in code blocks. This is true for tools written in [R (rmarkdown)](https://github.com/rstudio/rmarkdown), [Go (hugo)](https://github.com/gohugoio/hugo), [Python (mkdocs)](https://github.com/mkdocs/mkdocs) or Rust languages. Therefore, if you are a data analyst who frequently uses R for data analysis and visualization, you can consider using tools written in R language as there are many options available. Therefore, the choice is not absolute but varies depending on your needs.

*Perhaps mdbook is not the best choice because Rust language has been iterating rapidly, so the Rust environment on a computer can become bloated after some time of use. However, as a Rust language developer, it is my first choice. Of course, tools in other languages also face the issue of environment configuration which cannot be avoided.*
#### Refs
[Here](https://tonybai.com/2020/06/27/gohugo-vs-mdbook-vs-peach/) is a Chinese Intro for some tools.
# How to use?
Here are some documents:
- [A very simple Chinese Guide](https://juejin.cn/post/7201787862236823608)
- [Official Doc in Chinese](https://hellowac.github.io/mdbook-doc-zh/zh-cn/index.html)
- [Official Doc in English](https://rust-lang.github.io/mdBook/)

The usage of `mdbook` is easy!

## Command

#### Install
```shell
cargo install mdbook
```

#### init
Fisrt, you should init.
```shell
mdbook init
```

When using the init command for the first time, a couple of files will be set up for you:
```
book-test/
├── book
└── src
    ├── chapter_1.md
    └── SUMMARY.md
```
- The **src** directory is where you write your book in markdown. It contains all the source files, configuration files, etc.

- The **book** directory is where your book is rendered. All the output is ready to be uploaded to a server to be seen by your audience.

- The **SUMMARY.md** is the skeleton of your book.The summary file is used by mdBook to know what chapters to include, in what order they should appear, what their hierarchy is and where the source files are. Without this file, there is no book.
#### Build
The build command is used to render your book:
```shell
mdbook build
```
#### Serve
The serve command is used to preview a book by serving it via HTTP at localhost:3000 by default:
```shell
mdbook serve
```
The serve command watches the book's src directory for changes, rebuilding the book and refreshing clients for each change; this includes re-creating deleted files still mentioned in SUMMARY.md! A websocket connection is used to trigger the client-side refresh.

## More details!
Yep, the usage of `mdbook` is easy like what I have showed above!

You just need to remember 3 command:
```shell
mdbook init
mdbook build
mdbook server
```
Then, you will get a online-book!

If you want to know more about mdbook, please visit the [official doc](https://rust-lang.github.io/mdBook/).
