---
name: alpine-reach-setup
description: Connect this agent to an Alpine Reach workspace and pick the project to work on. Use when an Alpine Reach tool says the connection needs approval, when the user asks to connect or set up Alpine Reach, or before the first Alpine Reach task when no project has been chosen yet.
---

# Connect Alpine Reach

Alpine Reach tools work on one approved project (a workspace's brand) at a time. A provider sign-in alone does not grant access to data; the person approves projects and access inside Alpine Reach.

## Steps

1. Call `alpine_list_projects` with `{}`.
   - If it returns projects, go to step 3.
   - If the result is `approval_required`, give the person the exact `approvalUrl` from the result and say what it asks for (`requestedCapabilities`). They open it while signed in to Alpine Reach, choose the workspaces and approve. Do not invent or shorten the link.
   - If the result is an error with `nextAction: "reconnect"`, ask the person to reconnect the Alpine Reach connector in their assistant's connector settings and sign in with their Alpine Reach account.
2. After they approve, call `alpine_list_projects` again.
3. If there is one project, use it. If there are several, ask which one, by name. Keep its `projectId` for every later call in this conversation.
4. When a tool later returns `approval_required` for more access (for example ads or analytics reading), share that new link the same way. The person approves only what is listed.

## Rules

- Never ask for passwords, tokens or codes in chat.
- Use only `projectId` values returned by `alpine_list_projects`.
- Answer in the language the person writes in.
