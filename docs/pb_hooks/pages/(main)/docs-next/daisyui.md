```
bun add -D tailwindcss @tailwindcss/typography daisyui@latest
bunx tailwind init
```

```
/** @type {import('tailwindcss').Config} */
export default {
  content: ['./pb_hooks/pages/routes/**/*.{ejs,md}'],
  theme: {
    extend: {},
  },
  plugins: [require('@tailwindcss/typography'), require('daisyui')],
}
```