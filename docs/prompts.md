# @tyck/prompts
🚀 Unleash the magic of stunning command-line apps 🪄 [Try the demo](https://stackblitz.com/edit/tyck/prompts?file=index.js)

`@tyck/prompts` is a captivating, pre-styled wrapper around [`@tyck/core`](https://www.npmjs.com/package/@tyck/core) designed to empower your CLI applications.

- 🤏🎉 A whopping 80% smaller than competing options
- 💎🌈 Elegant, minimal UI for a polished look
- ✅🎯 User-friendly API to streamline development
- 🧱🔥 Includes text, confirm, select, multiselect, and spinner components

## Fundamentals
---
### Configuration
Utilize `intro` and `outro` functions to display messages that kick off 🚀 or conclude 🏁 a prompt session, respectively.

```ts
import { intro, outro } from '@tyck/prompts'

intro('create-my-app 🚧')
// Do stuff
outro('Youre all set! 🎉')
```
### Cancellation
The `isCancel` function acts as a safeguard ⚔️ that identifies when a user aborts a question with `CTRL + C`. Handle this situation for each prompt, and if desired, include a friendly cancellation message with the `cancel` utility.

```ts
import { cancel, isCancel, text } from '@tyck/prompts'

const value = await text(/* TODO */)

if (isCancel(value)) {
  cancel('Operation cancelled.❌')
  process.exit(0)
}
```

## Components
---
### Text
The text component captures a single line of input.📝

```ts
import { text } from '@nyxb/bang-prompts'

const meaning = await text({
  message: 'What is the meaning of life?🧐',
  placeholder: 'Not sure',
  initialValue: '42',
  validate(value) {
    if (value.length === 0)
      return 'Value is required!🚫'
  },
})
```

### Confirm
The confirm component accepts yes or no answers. The result is a boolean value of `true` or `false`. 🤔

```ts
import { confirm } from '@tyck/prompts'

const shouldContinue = await confirm({
  message: 'Do you want to continue?🏃‍♂️',
})
```

### Select
The select component enables users to choose one value from a list of options. The result is the `value` prop of the selected option. 🎯

```ts
import { select } from '@tyck/prompts'

const projectType = await select({
  message: 'Pick a project type.📚',
  options: [
    { value: 'ts', label: 'TypeScript' },
    { value: 'js', label: 'JavaScript' },
    { value: 'coffee', label: 'CoffeeScript', hint: 'oh no 😱' },
  ],
})
```

### Multiselect
The `multiselect` component lets users pick multiple values from a list of options. The result is an array containing all selected `value` props. 🛠️
  
  ```ts
  import { multiselect } from '@tyck/prompts'

const additionalTools = await multiselect({
    message: 'Select additional tools. 🔧',
    options: [
      { value: 'eslint', label: 'ESLint', hint: 'recommended' },
      { value: 'prettier', label: 'Prettier' },
      { value: 'gh-action', label: 'GitHub Action' }
    ],
    required: false,
})
```

### Spinner
The spinner component indicates a pending action, such as a lengthy download or dependency installation. ⏳
  
```ts
import { spinner } from '@tyck/prompts'

const s = spinner()
s.start('Installing via npm 📦')
// Perform installation
s.stop('Installed via npm ✅')
```

## Utilities
---
### Grouping
Grouping prompts together is an excellent way to maintain organized code.🧹 This accepts a JSON object with a name that can be used to reference the group later. The second argument is optional but has an onCancel callback that will be called if the user cancels one of the prompts in the group.

```ts
import * as p from '@tyck/prompts'

const group = await p.group(
  {
    name: () => p.text({ message: 'What is your name?🤓' }),
    age: () => p.text({ message: 'What is your age?🎂' }),
    color: ({ results }) =>
      p.multiselect({
        message: `What is your favorite color ${results.name}? 🌈`,
        options: [
          { value: 'red', label: 'Red' },
          { value: 'green', label: 'Green' },
          { value: 'blue', label: 'Blue' },
        ],
      }),
  },
  {
    // On Cancel callback that wraps the group
    // So if the user cancels one of the prompts in the group this function will be called
    onCancel: ({ results }) => {
      p.cancel('Operation cancelled.❌')
      process.exit(0)
    },
  }
)

console.log(group.name, group.age, group.color)
```
