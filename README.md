# React + TypeScript + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react/README.md) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh

## Expanding the ESLint configuration

If you are developing a production application, we recommend updating the configuration to enable type aware lint rules:

- Configure the top-level `parserOptions` property like this:

```js
   parserOptions: {
    ecmaVersion: 'latest',
    sourceType: 'module',
    project: ['./tsconfig.json', './tsconfig.node.json'],
    tsconfigRootDir: __dirname,
   },
```

- Replace `plugin:@typescript-eslint/recommended` to `plugin:@typescript-eslint/recommended-type-checked` or `plugin:@typescript-eslint/strict-type-checked`
- Optionally add `plugin:@typescript-eslint/stylistic-type-checked`
- Install [eslint-plugin-react](https://github.com/jsx-eslint/eslint-plugin-react) and add `plugin:react/recommended` & `plugin:react/jsx-runtime` to the `extends` list

# Project Configuration
Setup ESLint and Prettier

## 1. setup eslint
- install ESLint dependency
   ```
   npm i -D eslint
   ```
- init setup ESLint
   ```
   npx eslint --init
   ```
   - options
      ```
      ✅ To check syntax and find problems
      ✅ Javascript modules (import/export) 
      ✅ react
      ✅ typescript
      ✅ browser
      ✅ Javascript config file
      ✅ install the rest dependencies
      ✅ npm
      ```
- install `eslint-config-airbnb`
   ```
   npx install-peerdeps --dev eslint-config-airbnb
   ```
- changes the `extends` in `.eslintrc.cjs` config into this
   ```diff
   [
   -  'eslint/recommended',
   +  'airbnb', 
   +  'airbnb/hooks',
      'plugin:react/recommended',
      'plugin:@typescript-eslint/recommended'
   ]
   ```
- install `eslint-config-airbnb-typescript`
   ```
   npm i -D eslint-config-airbnb-typescript
   ```
- changes the `extends` in `.eslintrc.cjs` config into this
   ```diff
   [
      'airbnb', 
      'airbnb/hooks',
   +  'airbnb-typescript',
      'plugin:react/recommended',
      'plugin:@typescript-eslint/recommended'
   ]
   ```
- changes the `parserOptions` in `.eslintrc.cjs` config into this
   ```
   parserOptions: {
      ecmaVersion: 'latest',
      sourceType: 'module',
      project: './tsconfig.json',
   }
   ```
- changes the `include` in `tsconfig.json` config into this
   ```diff
   "include": [
   +  ".eslintrc.cjs",
      "src"
   ]
   ```
- disable this `eslint` rule if needed
   ```
   rules: {
      'react/react-in-jsx-scope': 0,
   },
   ```

## 2. setup prettier
- install `prettier` dependency
   ```
   npm i -D prettier eslint-config-prettier eslint-plugin-prettier
   ```
- add file `.prettierrc.cjs` and this configuration
   ```
   module.exports = {
      trailingComma: "es5",
      tabWidth: 2,
      semi: true,
      singleQuote: true,
   }
   ```
- changes the `plugins` in `.eslintrc.cjs` into this
   ``` diff
   plugins: [
      '@typescript-eslint', 
      'react', 
   +  'prettier'
   ]
   ```
- changes the `extends` in `.eslintrc.cjs` into this
   ```diff
   extends: [
      'airbnb',
      'airbnb-typescript',
      'airbnb/hooks',
      'plugin:@typescript-eslint/recommended',
      'plugin:react/recommended',
   +  'plugin:prettier/recommended',
   ]
   ```