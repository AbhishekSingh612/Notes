<%*
let path1 =  app.vault.getAllLoadedFiles().map((s2)=>{
	return "/"+s2.path.substring(0,s2.path.lastIndexOf("/"))+"/";
})
path1 = [...new Set(path1)]
path1[0] = '/'

let name = await tp.system.prompt("Enter Name","Untitled",false,false)
let path2 = await tp.system.suggester(path1, path1,false,"Enter the path")
let link = await tp.system.prompt("Enter Link","paste_link_here",false,false)
let problem = await tp.system.prompt("Enter Problem Statement","Enter_Problem_here",false,true)
const difficultyList = ['Easy', 'Medium', 'Hard']
let difficulty = await tp.system.suggester(difficultyList, difficultyList,false,"Enter the Difficulty")



await tp.file.rename(name)
await tp.file.move(path2 + name);

%>
---
Date: <% tp.date.now('DD MMM, YYYY') %>
Tags: dsa
fileClass: Problem
---
Topics:: 
Difficulty::  <% difficulty %>
Understanding:: 
## Problem: 
 <% problem %>

[Link]( <% link %>)

## Notes: 
- 

## Solutions: 

- Solution 1: 
	```java
	
	paste_solution_here
	
	```
	Complexity: 
	- Time: O( )
	- Space: O( )

