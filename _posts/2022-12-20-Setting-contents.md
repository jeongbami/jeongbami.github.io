---
title: setting write
date: 2022-12-20 14:50:00 +/-0900
categories: [blog, tips]
tags: [gitblog]     # TAG names should always be lowercase
mermaid: true
---



1. Mermaid
        add yaml block
        mermaid: true
2. Image
        ![img-description](/path/to/image)  _Image Caption_

        size 
        ![Desktop View](/assets/img/sample/mockup.png){: width="700" height="400" }
        or
        ![Desktop View](/assets/img/sample/mockup.png){: w="700" h="400" }

        position
        ![Desktop View](/assets/img/sample/mockup.png){: .normal }
        ![Desktop View](/assets/img/sample/mockup.png){: .left }
        ![Desktop View](/assets/img/sample/mockup.png){: .right }

        many image
            1. add yaml block
            ---
            img_path: /img/path/    
            ---
            2. markdown 
            ![The flower](flower.png)
            3. output
            <img src="/img/path/flower.png" alt="The flower">

3. pin the post
    add yaml block
        pin: true

4. Syntax
    1) inline code 
        `inline code`
    2) filepath hightlight
        `/path/to/a/file.extend`{: .filepath}
    3) Code Block
        ```
            This is a plaintext code snippet.
        ```
    4) Specifying Language
        Using ```{language}  <- edit this
            ```yaml
            key: value
            ```
    5) Liquid Codes
        {% raw %}  & {% endraw %} 
    6)line number 
        console, plaintext, terminal, nolineno(hideline)
            ```shell
                echo 'No more line numbers!'
            ```
            {: .nolineno } <- edit this
        7) specifying the filename
            ```shell
                # content
            ```
            {: file="path/to/file" } <- edit this and it will be out line number line
5. prompts 
    > Example line for prompt.
    {: .prompt-info }
    info -> tip, info, warning, danger

