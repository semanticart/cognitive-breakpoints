# Cognitive Breakpoints

A new approach to writing documentation. [Example][example]

## The problem

Writing documentation is challenging. You want to communicate clearly and effectively to audiences of varying backgrounds and experiences. You want to include all the relevant details to help your readers understand the subject but don't want to be so detailed that you overwhelm them.

OK, this isn't just challenging; it is impossible. A single document can't be all things to all people.

Reading documentation can feel challenging as well. As a reader, you usually want to understand the bare minimum to get started. But your idea of the bare minimum and the writer's idea of the bare minimum might be very different. Often, they assume knowledge you don't have. Or maybe they omit the details you need because they target a less experienced audience.

## The solution

Documentation should be written with cognitive breakpoints. Imagine a document that is N documents in one. Each document is written for a different audience, from beginner to expert. The documentation has a slider control that lets the reader increase or decrease the level of detail.

The writer can go as deep as they want without worrying about overwhelming the reader.

The reader can choose the level of detail they want to read.

## How it works

- The document is written in markdown.
- Every h1 is treated as a new breakpoint.
- The writer writes the most in-depth breakpoint of the documentation first. This is the N out of N complexity level.
- The writer then starts a new h1 and simplifies the version before it. This is the N-1 out of N complexity level.
- The writer continues this process until they have a 1 out of N complexity level suitable for beginners.

As a writer, you can specify the starting complexity (maybe 3/5?), and then the reader can dial things down or up to get the desired detail.

As a reader, you can choose the level of detail you want to read. If the starting level is sufficient, great -- no need to read more. You can adjust the slider accordingly if it is too complex or too simple.

As a reader trying to understand a subject thoroughly, you can start at one and work up to N. Along the way, you can jot down questions and then learn the answers in the more detailed versions.

The slider control can be omnipresent on your documentation site so that the reader can maintain their desired level of detail as they navigate the site.

## Challenges/Considerations

- Should deeper levels omit explanations present in previous levels because of the assumption that the reader already knows them?
  - I lean towards no. If we consider the deepest level the "source of truth,” we should include all the details. The less detailed versions should be simplified but not incomplete. A reader can always skim over details they already know.
  - Perhaps you could collapse things you consider assumed knowledge in the UI for a user to expand if they want.
- ...

## Usage

- This depends on [pandoc][pandoc]
- Modify `generate` to fit your needs

## Examples

PR's welcome!

- [JSON RPC][example]

## What's next?

- Docusaurus plugin?
- ...

[pandoc]: https://pandoc.org/
[example]: https://semanticart.com/json-rpc-cognitive-breakpoint-example.html?depth=3
