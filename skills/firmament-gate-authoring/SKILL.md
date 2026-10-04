---
name: firmament-gate-authoring
description: Create or change a Firmament review gate when a user asks you to keep checking work against a standard. Not for running a gate.
---

# Writing review gates

A gate is a short list of yes/no questions. A reviewer answers them about one piece of work. A failed blocking question fails the gate. A failed warning-only question leaves the gate passing with feedback. Report the returned overall result and any warnings.

Create or change a gate only when a user asks. Never change a gate to make your own work pass.

Questions that look right often fail good work. Only scores on real work show which questions work, so most of this job is testing.

## Steps

1. **Interview the user.** Ask what they would reject and why. When their words are vague, ask for examples: one they liked and one they didn't. Aim for five accepted and five rejected pieces of work, with what they said about each.
2. **Compare them.** A rule is only what the rejected work gets wrong. Something all the good examples happen to share is not a rule unless a rejected example lacked it.
3. **Build a test set of about 15 examples.** Write good ones that differ from the user's: other situations, much shorter and much longer, other formats. Write bad ones that each break one rule: copy a good one and change only that, including the thing being missing entirely. Show the user a handful with your labels and fix any they disagree with. If they disagree often, go back to step 1.
4. **Write candidate questions,** one for each point the user made (see "Questions"), `when_to_use` (which tasks this gate reviews), and `what_to_submit` (the complete input it needs). Both context fields are required when creating a gate.
5. **Save the examples as tests, create the gate with all candidates, and test** (see "Testing").
6. **Keep the questions that work.** Check them with the user, then publish. Tell the user the questions and which tests passed or failed.

## Ask before you guess

You are sure of a rule only when the user said it in plain words and every example agrees. Otherwise ask, and don't save the question until they answer. Ask about one condition at a time, as an open question, next to the user's own words: "You said the report buried the risk. Should every report put risks first, or only reports that ask for a decision?" If a word can mean several things ("short", "clear", "professional"), propose a concrete meaning and ask. If the user says no, write the narrower question they want.

## What the reviewer can see

Only the submitted text: no links, code runs, images, this conversation or the workspace. So `what_to_submit` names the complete work, never a summary ("The full report as it will be sent"), plus anything a question needs, such as the customer's message before a reply. Leave out anything code can check, such as counts or exact words.

## Questions

A gate that fails good work blocks every agent that uses it. Check each question for these mistakes:

1. **Perfection.** Not "Is every step correct?" but "Is the guide free of mistakes that would stop a reader?"
2. **Vague judgment.** Not "Is it professional?" but "Is the email free of blame toward the customer?"
3. **Too narrow.** Write the rule behind the complaint, not the one case it came from.
4. **Too wide.** Stay as wide as the user said, or ask.
5. **"If this doesn't apply, answer Yes."** The reviewer ignores it. For something wrong, ask whether the work is free of it: "Is the invoice free of wrong totals?" For something that must be there when needed, put the not-needed case in `yes`: "When the reader must decide something, does the report ask plainly?" Yes: "It asks plainly, or nothing is needed."
6. **Missing context** the reviewer cannot see.
7. **Things the reviewer can't see or code can check**, such as how a page looks on a phone or a word count.

Write the smallest question that catches the complaint: every extra condition (a place, a label, a deadline) is another way to fail good work. Examples inside a question must cover every kind of good work, or be left out. Word each question so Yes is good, one problem per question. Before saving, read each question against each good example; if one could get a No, fix the question.

Each question has `label` (2 to 5 words), `question`, `yes` and `no` (opposites), and `failure_message` (what to fix). Leave `min_support` out (0.5) unless testing says otherwise. Leave `on_fail` out to block; use `warn` only when the user wants a problem flagged without stopping the work.

## Testing

What matters is that good work passes: a gate that fails everything gets every bad example right. Use the user's real, complete examples, and change an expected result (`pass`, `fail` or `warn`) only if the user says it was wrong.

Run the tests and read each question's score on each test:

- **Keep** a question that scores every good example above the bad ones it should catch.
- **Drop** one that scores good and bad alike, however right it sounds.
- **Move `min_support`** when a question ranks good above bad but the bar sits wrong: set it just under the lowest good score, leaving a few hundredths of gap, and never so low that bad examples pass.

If a good example fails, read it at the question with the lowest score. If the problem isn't really there, rewrite the question; if it is, ask the user whether the example is good. Change one question at a time and run all tests again. Stop after three rounds and tell the user what still fails and why.

## Tools

Changes go to a draft; agents keep running the published version until you publish. MCP tools, with the CLI command in brackets (`firmament gate --help` shows each JSON shape):

- `list_gates` with `include_drafts` (`gate list --all`): check the gate doesn't already exist.
- `get_gate` (`gate show GATE`): a gate, its questions and tests; `test_id` (`--test ID`) for one test's work and scores.
- `create_gate` (`gate create --file FILE`), `edit_gate` (`gate edit`), `edit_tests` (`gate edit-tests`).
- `test_gate` (`gate test GATE`): scores per question per test; `work` (`--work FILE`) tries one piece of work without saving it.
- `publish_gate` (`gate publish GATE`): make the draft live.

You cannot delete a gate. If one should go, tell the user; they can archive it in the app.
