---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
draft: false
author: William Spear
year: "{{ dateFormat "2006" .Date }}"
month: "{{ dateFormat "2006/01" .Date }}"

categories:
- Personal
- Thoughts
tags:
- software
- html
---

 	Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
 	tempor incididunt ut labore et dolore magna aliqua.
 	
 	Above this more line is the summary
 	
 	<!--more-->
 	
 	Below this more line is the rest of the content
 	
 	Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut
 	aliquip ex ea commodo consequat.