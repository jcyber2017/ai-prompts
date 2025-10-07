The idea behind these prompts is to get the agents to create a web site for you from scratch.

1. the first step is to describe your idea, example:
I want to create a web site for english learning, the idea is to have a learn page where it will to show you new words with traslation, meaning, type of word, examples of use, an a button that says learned in order to continue to the next word, after N words it will save that to your account and send you to a new page called "practice", there it will present a word and 4 buttons, 3 buttons will contain the translation of 2 random words and the word it self, the other button will say check, after checking it will change to continue to move on, if the user answer the N words to practice it will save the practice in your account, BLAH BLAH BLAH

2. paste the description in the prompt "1-brd.md" in "<SPECS GO HERE>" and send that to an AI it will replay with a md file, save that into a file you can called: brd.md
that is a "Business Requirements Document" it is a formal document detailing project goals, scope, and stakeholder needs for successful project execution. In another context, you should read and update anything that you think should be different

3. paste the content of the brd.md file in the prompt "2-prd.md" in "<BRD GOES HERE>" and send that to an AI it will replay with a md file, save that into a file you can called: prd.md
that is a "Product Requirements Document" this document details the purpose, features, functionality, and behavior of a product. It serves as a comprehensive guide and single source of truth for various teams, including business and technical teams, to ensure everyone understands the product's goals and requirements for successful development, launch, and marketing, you should read and update anything that you think should be different.

4. paste the content of the prd.md file in the prompt "3-stories.md" in "<PRD GOES HERE>" and send that to an AI it will replay with a list of stories for your application, do not need to copy that, in the same chat add the prompt "4-detailed.md", it will replay with a md file, save that into a file you can called: tasks.md, that is the list of thats that an AI agent need to complete to develop the web site, you should review and change anything in order to get the result you need.

5. Clone my project "https://github.com/jcyber2017/next-supabase-auth-starter" and replace the content of the file /agent-helpers/.cursor-tasks.md with tasks.md

6. Send the prompt "5-execute.md" to your cursor agent, it will execute all the tasks and mark as completed each task, you need to supervise this process, it will ask you permission to run commands like build the app, do git add and git commit, etc.

##Recommendations:

when it runs commands it keep loadding even when command is done, you should stop that loading in the chat after the command ran in order to avoid the agent get stuck.
also it will ask you to review the code when finished each batch of steps, you can/should create a new brach for it to work in, to avoid damages in the code, and after review you should merge and delete that branch in github and create a new one for the next batch.

Notice that my project is thinked to work with Nextjs, Supabase, NextAuht, Storybook, Tailwind CSS, if you what to change that after cloning update the project before sending the prompt "5-execute.md". Also you can create a new project and just copy the folder: agent-helper and the files .cursorrules and AGENTS.md, remember to read and update any specification
