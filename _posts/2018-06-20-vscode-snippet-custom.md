---
layout:     post
title:      VScode snippet custom
subtitle:   VSCode snippet custom
date:       2018-06-20
author:     Allen
catalog: true
tags:
    - VSCode
    - Snippet
---

# Snippet custom

>  how to design a Snippet  in VScode


### The structure of the snippet
- prefix: define the keywords which will be used in IntelliSense
- body: The main content of which will be displayed when inputting the prefix
- description



### Here is an example snippet 

```

"For Loop": {

    "prefix": "for",

    "body": [

        "for (var ${index} = 0; ${index} < ${array}.length; ${index}++) {",

        "\tvar ${element} = ${array}[${index}];",

        "\t$0",

        "}"

    ],

    "description": "For Loop"

},

```

- `For Loop` is the name of the snippet

- `prefix` defines the prefix used in the IntelliSence drop down. In this cause for 

- `body` is the snippet content. Possible variables are:

    - $1, $2 for tab stops

    - ${id} and ${id: label} and ${1:label} for variables

    - variables with same id are connected

- `description` is the description used in the IntelliSence drop down



### Most convenient way to generate a snippet template

https://snippet-generator.app/


