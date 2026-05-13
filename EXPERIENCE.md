# Experience, lessons learned

We determined that a SKILl was the right approach for this project. A skill contains a set of steps (like a review checklist), and details how to complete those checks.

The first approach was to write a skill from scratch. That ended up being hard and complex, probably because we were really thinking about instructions for a human to follow. This meant that the instructions had to be detailed enough, and this got complicated and verbose VERY QUICKLY.

The second approach worked better: we just asked the agent to help us write a skill for the stated problem. We basically fed it the simple sru-checklist that the SRU team members follow, very succint, to see what it would produce. That was already much better: not only did we get a good set of instructions (out of the very brief checklist), we also got a much better structured skill file.

This process then became interactive. We applied the skill to a real Ubuntu SRU, analyzed the output from the agent, noted where it was struggling or coming up to incorrect results, and started fine tuning it. And, critically, this was done simple by asking the agent to make the changes, and not editing the skill file directly.

We still see places where the skill can be optimized, and took note of those in the TODO.md file, but after this first learning experience, the next steps should be much easier. Until we can also finally add the NEW-review skill, for source packages uploaded to the NEW queue.

