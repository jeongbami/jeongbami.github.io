---
title: setting write
date: 2022-12-20 14:50:00 +/-0900
categories: [blog, tips]
tags: [gitblog]     # TAG names should always be lowercase
mermaid: true
---


---
title: Text and Typography
author: cotes
date: 2019-08-08 11:33:00 +0800
categories: [Blogging, Demo]
tags: [typography]
math: true
mermaid: true
image:
  path: /commons/devices-mockup.png
  width: 800
  height: 500
  alt: Responsive rendering of Chirpy theme on multiple devices.
---

This post is to show Markdown syntax rendering on [**Chirpy**](https://github.com/cotes2020/jekyll-theme-chirpy/fork), you can also use it as an example of writing. Now, let's start looking at text and typography.


## Titles
---
# H1 - heading

<h2 data-toc-skip>H2 - heading</h2>

<h3 data-toc-skip>H3 - heading</h3>

<h4>H4 - heading</h4>
---
<br>

## Paragraph

Quisque egestas convallis ipsum, ut sollicitudin risus tincidunt a. Maecenas interdum malesuada egestas. Duis consectetur porta risus, sit amet vulputate urna facilisis ac. Phasellus semper dui non purus ultrices sodales. Aliquam ante lorem, ornare a feugiat ac, finibus nec mauris. Vivamus ut tristique nisi. Sed vel leo vulputate, efficitur risus non, posuere mi. Nullam tincidunt bibendum rutrum. Proin commodo ornare sapien. Vivamus interdum diam sed sapien blandit, sit amet aliquam risus mattis. Nullam arcu turpis, mollis quis laoreet at, placerat id nibh. Suspendisse venenatis eros eros.

## Lists

### Ordered list

1. Firstly
2. Secondly
3. Thirdly

### Unordered list

- Chapter
  + Section
    * Paragraph

### ToDo list

- [ ] Job
  + [x] Step 1
  + [x] Step 2
  + [ ] Step 3

### Description list

Sun
: the star around which the earth orbits

Moon
: the natural satellite of the earth, visible by reflected light from the sun

## Block Quote

> This line shows the _block quote_.

## Prompts

> An example showing the `tip` type prompt.
{: .prompt-tip }

> An example showing the `info` type prompt.
{: .prompt-info }

> An example showing the `warning` type prompt.
{: .prompt-warning }

> An example showing the `danger` type prompt.
{: .prompt-danger }

## Tables

| Company                      | Contact          | Country |
|:-----------------------------|:-----------------|--------:|
| Alfreds Futterkiste          | Maria Anders     | Germany |
| Island Trading               | Helen Bennett    | UK      |
| Magazzini Alimentari Riuniti | Giovanni Rovelli | Italy   |

## Links

<http://127.0.0.1:4000>

## Footnote

Click the hook will locate the footnote[^footnote], and here is another footnote[^fn-nth-2].

## Images

- Default (with caption)

![Desktop View](/posts/20190808/mockup.png){: width="972" height="589" }
_Full screen width and center alignment_

<br>

- Shadow

![Window shadow](/posts/20190808/window.png){: .shadow width="1548" height="864" .w-75 }
_shadow effect (visible in light mode)_

<br>

- Left aligned

![Desktop View](/posts/20190808/mockup.png){: width="972" height="589" .w-75 .normal}

- Float to left

  ![Desktop View](/posts/20190808/mockup.png){: width="972" height="589" .w-50 .left}
  Praesent maximus aliquam sapien. Sed vel neque in dolor pulvinar auctor. Maecenas pharetra, sem sit amet interdum posuere, tellus lacus eleifend magna, ac lobortis felis ipsum id sapien. Proin ornare rutrum metus, ac convallis diam volutpat sit amet. Phasellus volutpat, elit sit amet tincidunt mollis, felis mi scelerisque mauris, ut facilisis leo magna accumsan sapien. In rutrum vehicula nisl eget tempor. Nullam maximus ullamcorper libero non maximus. Integer ultricies velit id convallis varius. Praesent eu nisl eu urna finibus ultrices id nec ex. Mauris ac mattis quam. Fusce aliquam est nec sapien bibendum, vitae malesuada ligula condimentum. Phasellus a tortor aliquam, tristique felis sit amet, elementum enim. Integer vestibulum vitae nulla nec pretium.

- Float to right

  ![Desktop View](/posts/20190808/mockup.png){: width="972" height="589" .w-50 .right}
  Praesent maximus aliquam sapien. Sed vel neque in dolor pulvinar auctor. Maecenas pharetra, sem sit amet interdum posuere, tellus lacus eleifend magna, ac lobortis felis ipsum id sapien. Proin ornare rutrum metus, ac convallis diam volutpat sit amet. Phasellus volutpat, elit sit amet tincidunt mollis, felis mi scelerisque mauris, ut facilisis leo magna accumsan sapien. In rutrum vehicula nisl eget tempor. Nullam maximus ullamcorper libero non maximus. Integer ultricies velit id convallis varius. Praesent eu nisl eu urna finibus ultrices id nec ex. Mauris ac mattis quam. Fusce aliquam est nec sapien bibendum, vitae malesuada ligula condimentum. Phasellus a tortor aliquam, tristique felis sit amet, elementum enim. Integer vestibulum vitae nulla nec pretium.

## Mermaid SVG

```mermaid
 gantt
  title  Adding GANTT diagram functionality to mermaid
  apple :a, 2017-07-20, 1w
  banana :crit, b, 2017-07-23, 1d
  cherry :active, c, after b a, 1d
```

## Mathematics

The mathematics powered by [**MathJax**](https://www.mathjax.org/):

$$ \sum_{n=1}^\infty 1/n^2 = \frac{\pi^2}{6} $$

When $a \ne 0$, there are two solutions to $ax^2 + bx + c = 0$ and they are

$$ x = {-b \pm \sqrt{b^2-4ac} \over 2a} $$

## Inline code

This is an example of `Inline Code`.

## Filepath

Here is the `/path/to/the/file.extend`{: .filepath}.

## Code block

### Common

```
This is a common code snippet, without syntax highlight and line number.
```

### Specific Languages

#### Console

```console
$ env |grep SHELL
SHELL=/usr/local/bin/bash
PYENV_SHELL=bash
```

#### Shell

```bash
if [ $? -ne 0 ]; then
    echo "The command was not successful.";
    #do the needful / exit
fi;
```

### Specific filename

```sass
@import
  "colors/light-typography",
  "colors/dark-typography"
```
{: file='_sass/jekyll-theme-chirpy.scss'}

## Reverse Footnote

[^footnote]: The footnote source
[^fn-nth-2]: The 2nd footnote source

## Table of Contents

By default, the **T**able **o**f **C**ontents (TOC) is displayed on the right panel of the post. If you want to turn it off globally, go to `_config.yml`{: .filepath} and set the value of variable `toc` to `false`. If you want to turn off TOC for a specific post, add the following to the post's [Front Matter](https://jekyllrb.com/docs/front-matter/):

```yaml
---
toc: false
---
```

## Comments

The global switch of comments is defined by variable `comments.active` in the file `_config.yml`{: .filepath}. After selecting a comment system for this variable, comments will be turned on for all posts.

If you want to close the comment for a specific post, add the following to the **Front Matter** of the post:

```yaml
---
comments: false
---
```

## Mathematics

For website performance reasons, the mathematical feature won't be loaded by default. But it can be enabled by:

```yaml
---
math: true
---
```

## Mermaid

[**Mermaid**](https://github.com/mermaid-js/mermaid) is a great diagrams generation tool. To enable it on your post, add the following to the YAML block:

```yaml
---
mermaid: true
---
```

Then you can use it like other markdown languages: surround the graph code with ```` ```mermaid ```` and ```` ``` ````.

## Images

### Caption

Add italics to the next line of an image，then it will become the caption and appear at the bottom of the image:

```markdown
![img-description](/path/to/image)
_Image Caption_
```
{: .nolineno}

### Size

In order to prevent the page content layout from shifting when the image is loaded, we should set the width and height for each image:

```markdown
![Desktop View](/assets/img/sample/mockup.png){: width="700" height="400" }
```
{: .nolineno}

Starting from _Chirpy v5.0.0_, `height` and `width` support abbreviations (`height` → `h`, `width` → `w`). The following example has the same effect as the above:

```markdown
![Desktop View](/assets/img/sample/mockup.png){: w="700" h="400" }
```
{: .nolineno}

### Position

By default, the image is centered, but you can specify the position by using one of the classes `normal`, `left`, and `right`.

> Once the position is specified, the image caption should not be added.
{: .prompt-warning }

- **Normal position**

  Image will be left aligned in below sample:

  ```markdown
  ![Desktop View](/assets/img/sample/mockup.png){: .normal }
  ```
  {: .nolineno}

- **Float to the left**

  ```markdown
  ![Desktop View](/assets/img/sample/mockup.png){: .left }
  ```
  {: .nolineno}

- **Float to the right**

  ```markdown
  ![Desktop View](/assets/img/sample/mockup.png){: .right }
  ```
  {: .nolineno}

### Shadow

The screenshots of the program window can be considered to show the shadow effect, and the shadow will be visible in the `light` mode:

```markdown
![Desktop View](/assets/img/sample/mockup.png){: .shadow }
```
{: .nolineno}

### CDN URL

If you host the images on the CDN, you can save the time of repeatedly writing the CDN URL by assigning the variable `img_cdn` of `_config.yml`{: .filepath} file:

```yaml
img_cdn: https://cdn.com
```
{: file='_config.yml' .nolineno}

Once `img_cdn` is assigned, the CDN URL will be added to the path of all images (images of site avatar and posts) starting with `/`.

For instance, when using images:

```markdown
![The flower](/path/to/flower.png)
```
{: .nolineno}

The parsing result will automatically add the CDN prefix `https://cdn.com` before the image path:

```html
<img src="https://cdn.com/path/to/flower.png" alt="The flower">
```
{: .nolineno}

### Image Path

When a post contains many images, it will be a time-consuming task to repeatedly define the path of the images. To solve this, we can define this path in the YAML block of the post:

```yml
---
img_path: /img/path/
---
```
{: .nolineno }

And then, the image source of Markdown can write the file name directly:

```md
![The flower](flower.png)
```
{: .nolineno }

The output will be:

```html
<img src="/img/path/flower.png" alt="The flower">
```
{: .nolineno }

### Preview Image

If you want to add an image to the top of the post contents, specify the attribute `path`, `width`, `height`, and `alt` for the image:

```yaml
---
image:
  path: /path/to/image
  width: 1000   # in pixels
  height: 400   # in pixels
  alt: image alternative text
---
```

Except for `alt`, all other options are necessary, especially the `width` and `height`, which are related to user experience and web page loading performance. The above section "[Size](#size)" also mentions this.

Starting from _Chirpy v5.0.0_, the attributes `height` and `width` can be abbreviated: `height` → `h`, `width` → `w`. In addition, the [`img_path`](#image-path) can also be passed to the preview image, that is, when it has been set, the  attribute `path` only needs the image file name.

For simple use, you can also just use `image` to define the path.

```yml
image: /path/to/image
```

## Pinned Posts

You can pin one or more posts to the top of the home page, and the fixed posts are sorted in reverse order according to their release date. Enable by:

```yaml
---
pin: true
---
```

## Prompts

There are several types of prompts: `tip`, `info`, `warning`, and `danger`. They can be generated by adding the class `prompt-{type}` to the blockquote. For example, define a prompt of type `info` as follows:

```md
> Example line for prompt.
{: .prompt-info }
```
{: .nolineno }

## Syntax

### Inline Code

```md
`inline code part`
```
{: .nolineno }

### Filepath Hightlight

```md
`/path/to/a/file.extend`{: .filepath}
```
{: .nolineno }

### Code Block

Markdown symbols ```` ``` ```` can easily create a code block as follows:

````md
```
This is a plaintext code snippet.
```
````

#### Specifying Language

Using ```` ```{language} ```` you will get a code block with syntax highlight:

````markdown
```yaml
key: value
```
````

> The Jekyll tag `{% highlight %}` is not compatible with this theme.
{: .prompt-danger }

#### Line Number

By default, all languages except `plaintext`, `console`, and `terminal` will display line numbers. When you want to hide the line number of a code block, add the class `nolineno` to it:

````markdown
```shell
echo 'No more line numbers!'
```
{: .nolineno }
````

#### Specifying the Filename

You may have noticed that the code language will be displayed at the top of the code block. If you want to replace it with the file name, you can add the attribute `file` to achieve this:

````markdown
```shell
# content
```
{: file="path/to/file" }
````

#### Liquid Codes

If you want to display the **Liquid** snippet, surround the liquid code with `{% raw %}` and `{% endraw %}`:

````markdown
{% raw %}
```liquid
{% if product.title contains 'Pack' %}
  This product's title contains the word Pack.
{% endif %}
```
{% endraw %}
````

Or adding `render_with_liquid: false` (Requires Jekyll 4.0 or higher) to the post's YAML block.

## Learn More

For more knowledge about Jekyll posts, visit the [Jekyll Docs: Posts](https://jekyllrb.com/docs/posts/).