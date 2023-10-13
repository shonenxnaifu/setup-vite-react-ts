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

## 3. setup vitest
- install `vitest` dependency
   ```
   npm i -D vitest
   ```
- add this config from this [URL](https://github.com/vitest-dev/vitest/blob/main/examples/react-testing-lib-msw/vite.config.ts)
   ```diff
   +   /* eslint-disable import/no-extraneous-dependencies */
   +   /// <reference types="vitest" />
   +   /// <reference types="vite/client" />

      import { defineConfig } from 'vite';
      import react from '@vitejs/plugin-react';

      // https://vitejs.dev/config/
      export default defineConfig({
      plugins: [react()],
   +   test: {
   +      globals: true,
   +      environment: 'jsdom',
   +      setupFiles: ['./src/setupTests.ts'],
   +   },
      });

   ```
- changes the `inlcude` in `tsconfig.json` into this
   ``` diff
      "include": [
   +     "vite.config.ts",
         ".eslintrc.cjs",
         "src"
      ],
   ```

## 4. setup react testing library
- install `testing-library` dependency
   ```
   npm i -D @testing-library/react 
   ```

## 5. setup jest-dom testing library
- install `jest-dom` dependency
   ```
   npm i -D @testing-library/jest-dom@5.16.5 
   ```
- add this code into `setupTests.ts`
   ```javascript
   /* eslint-disable import/no-extraneous-dependencies */
   import matchers from '@testing-library/jest-dom/matchers';
   import { expect } from 'vitest';

   expect.extend(matchers);
   ```

## 6. create test file
- create `App.test.tsx` and add this code
   ```javascript
   /* eslint-disable import/no-extraneous-dependencies */
   import { describe, expect, it } from 'vitest';
   import { render, screen } from '@testing-library/react';

   import App from './App';

   describe('App', () => {
      it('Renders hello world', () => {
         // ARRANGE
         render(<App />);
         // ACT
         // EXPECT
         expect(
            screen.getByRole('heading', {
            level: 1,
            })
         ).toHaveTextContent('Hello World');
      });
   });
   ```

## 7. setup react-router-dom v6
- modify `App.tsx` into this
   ```javascript
   import { HashRouter } from 'react-router-dom';

   function App() {
      return <h1>Hello World</h1>;
   }

   function WrappedApp() {
      return (
         <HashRouter>
            <App />
         </HashRouter>
      );
   }

   export default WrappedApp;
   ```
