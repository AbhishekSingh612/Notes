<%*
//Inputs Here
let path = await tp.system.prompt("Write the path EX /DSA/2. Sliding Window/Problems")
let titleName = await tp.system.prompt("Note Title")
let problem = await tp.system.prompt("Problem Statement")
let linkToProblem =  await tp.system.prompt("Problem Link")
let difficulty = await tp.system.prompt("Difficulty [Easy, Medium, Hard]")
//Modifications
//titleName = qcFileName + " " + tp.date.now("YYYY-MM-DD")
let date = tp.file.creation_date("DD MMM,YYYY HH:mm")

//Creation Path
await tp.file.rename(titleName)
await tp.file.move(path + titleName);
// add cursor using <% tp.file.cursor() %>
-%>
---
title: 100. Test
Date: 23 Jan,2023 12:12
Tags: dsa
fileClass: Problem
---
Topics:: 
Difficulty:: Easy 
Understanding:: 
## Problem: 
Problem Test 

[Link](Link test)

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
---
title: <% titleName %>
Date: <% date %>
Tags: dsa
fileClass: Problem
---
Topics:: 
Difficulty:: <% difficulty %> 
Understanding:: 
## Problem: 
<% problem %> 

[Link](<% linkToProblem %>)

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