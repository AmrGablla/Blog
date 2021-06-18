
---
layout: post
title:  "Hello Javascript"
date:   2021-05-05 21:30:55 +0200
categories: jekyll update
--- 


---
layout: post
title:  "Hello Javascript"
date:   2021-05-05 21:30:55 +0200
categories: jekyll update
--- 

# Please be kind to me!
It is my first time to gave Javascript a good try to learn it, Not just copy-paste code snippets and google the issues.

I don't have a good history with the language, but I will give I a real try to figure out the language capabilities.
So This article and the reaming on this threat will focus on the points I found in the language.

**Let's Go......**

First of all, I started with this awesome repo [30 days of javascript](https://github.com/Asabeneh/30-Days-Of-JavaScript) and this is a small hint of a learned.

## String Manipulation
I think this language awesome in manipulating strings it has many built-in functions to do anything with strings with no restrictions like:

 - You can access any character in the string like array `i think many languages contain this feature` 
 
`let string = 'JavaScript'`
`let firstLetter = string[0] `
`console.log(firstLetter)           // J`
 

 - Includes(), Yes this small check function to check the string contain certain string or not.

`let string = '30 Days Of JavaScript' `
`console.log(string.includes('Days'))     // true `
     

 - Search:
Search with javascript is the first thing I found nice you can use some flags to change it like: 

| Modifier | Description |
| ------ | ------ |
| g | Perform a global match (find all matches rather than stopping after the first match |
| i | Perform case-insensitive matching |
| m | Perform multiline matching |  
 

it is baesd on ## RegExp Object 