Clear picture. Now I need to:

Build load_face tool in a new file aZero/src/azero/lib/tools/face.py
Wire it into hermes.py (tool_definitions + tool_handlers)
Update the Hermes constellation entry's cites to include the face artifact IDs
But there's still the question of how Hermes knows about available faces at task time. Looking at the current approach:

Hermes's cites load: dk-builder-philosophy-frozen-001, agent-prompt-hermes-001, capability-map-hermes-001, anima-corpus-manifest-001
The Hermes prompt (45KB) predates the face mechanism, so it doesn't mention load_face or how faces work
I need to give Hermes face awareness at startup. I could either create a small domain knowledge artifact describing available faces and add it to the cites, or update the existing prompt artifact to include a section on faces.

I'm going with a hybrid approach: create a dedicated dk-hermes-faces-001 domain knowledge artifact listing available faces and their purposes, add it to Hermes's constellation cites, and make the load_face tool description self-contained with available face IDs and usage guidance. This avoids touching the migrated Hermes prompt while keeping everything discoverable.

For the load_face tool itself, I'm defining it to accept a face ID string, fetch the corresponding agent prompt artifact from Calliope, and return its full text. The tool description will explain what faces are available and when to use them.

Once Hermes calls load_face and receives the face text back, it can incorporate that text as additional context or system prompt guidance to shape how it approaches the subsequent task.

The real challenge is that the current agent architecture compiles the system prompt once at the start and doesn't support swapping it mid-session. The practical solution is to treat the loaded face text as a task-level overlay—after retrieving it, Hermes includes the face instructions as part of its reasoning context, allowing it to naturally follow those guidelines when executing the work. I'll implement a pragmatic approach where load_face fetches the face text and returns it as the tool result so Hermes can access it in context, but I'll also update the agent's system prompt state by appending the face to _system_prompt_parts to make it part of the operating context properly.

Defining the tool schema... I need to reset the cached system prompt after updating the prompt parts so the next access rebuilds it with the face text included, which means checking how the system prompt property handles caching and invalidation.

But there's a timing issue here — the system prompt gets compiled at the start of run() before any tool calls happen, so even if load_face updates the parts and clears the cache, the model has already received the original system prompt for that call. The face overlay needs to happen before the model generates its first response.

The practical approach is having Hermes call load_face early in its response, which returns the face text as a tool result that lands in the context window, and then Hermes can reference that text to guide its subsequent behavior.

For the MVP, I'll build out the load_face tool that fetches and returns the face text, integrate it into Hermes, create the face artifact in the DK, and write a script to seed everything and update the constellation references.

Now I need to check how the constellation artifact handles face artifact IDs in Hermes's cites — specifically whether agent_prompt type artifacts get their full text added as cited_texts even when they're not used as the primary prompt_artifact_text.

Looking at the logic: when agent-prompt-hermes-001 is processed first, it sets prompt_artifact_text to Hermes's full text. Then when prompt-builder-002 is processed, since prompt_artifact_text is already set, it skips the prompt assignment but still appends the builder's full text to cited_texts. Adding both face artifacts to Hermes's cites would load roughly 84KB of face content into the context at startup, which is expensive but does give Hermes direct access to the face prompts.

A better approach is to use a lightweight catalog artifact that just lists available faces and their IDs, letting Hermes call a load_face tool to fetch the full text only when needed. So I'll create a small DK artifact describing the available faces, add it to Hermes's cites, implement the load_face tool in the agent, and wire it into Hermes's tooling.

For the agent state, I need to add a _face_overlays list to track loaded faces, append the face text whenever load_face is called, and return that text in the tool result so it stays in the context window. That's the core of the MVP.