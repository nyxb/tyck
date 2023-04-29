# `@tyck/core` 🌠

Bang delivers powerful low-level primitives for crafting your very own command-line applications! 💥🎩

At present, `TextPrompt`, `SelectPrompt`, and `ConfirmPrompt` are available, along with the foundational `Prompt` class. 🛠️🌟

Each `Prompt` takes in a `render` function.
  
```ts
import { TextPrompt, isCancel } from '@tyck/core'

const p = new TextPrompt({
  render() {
    return `What's your name? 🤔\n${this.valueWithCursor}`
  },
})

const name = await p.prompt()
if (isCancel(name))
  process.exit(0)
```

et ready to build awe-inspiring CLI applications with the help of `@tyck/core`! 🚀🎇
