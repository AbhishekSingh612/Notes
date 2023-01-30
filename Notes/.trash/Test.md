Mood today: <% tp.system.suggester(["Happy", "Sad", "Confused"], ["Happy1", "Sad1", "Confused1"]) %> 

Picked file: [[<% (await tp.system.suggester((item) => item.basename, app.vault.getMarkdownFiles())).basename %>]] 
<%* const execution_value = await tp.system.suggester(["Yes", "No"], ["true", "false"]) %> 
Are you using Execution Commands: <%* execution_value %>





