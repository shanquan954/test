# Just only a test

## Setting up Husky and Code Quality Tools

### 1. Install Husky

   - Install Husky as a dev dependency:
     ```bash
     npm install husky --save-dev
     ```

   - Initialize Husky:
     ```bash
     npx husky install
     ```

   - Set up the pre-commit hook to run tests:
     ```bash
     npm pkg set scripts.prepare="husky install"
     npx husky add .husky/pre-commit "npm test"
     ```

### 2. Install Prettier

   - Install Prettier as a dev dependency with an exact version:
     ```bash
     yarn add --dev --exact prettier
     ```

   - Create a `.prettierrc` file with default settings:
     ```bash
     node --eval "fs.writeFileSync('.prettierrc','{}\n')"
     ```

   - Create a `.prettierignore` file to ignore artifacts:
     ```
     # Ignore artifacts:
     build
     coverage
     ```

### 3. Install ESLint

   - Initialize ESLint configuration:
     ```bash
     npx eslint --init
     ```

### 4. Install eslint-config-prettier and eslint-plugin-prettier

   - Install the necessary packages:
     ```bash
     yarn add -D eslint-config-prettier eslint-plugin-prettier
     ```

   - Add them to `eslintrc.js`:
     ```javascript
     module.exports = {
     ...
       extends: ["airbnb-base", "prettier", "plugin:prettier/recommended"],
     ...
     };
     ```

### 5. Install lint-staged

   - Install lint-staged as a dev dependency:
     ```bash
     yarn add -D lint-staged
     ```

   - Create a `.lintstagedrc.json` file and define staged tasks:
     ```json
     {
       "*.js": ["eslint", "prettier --write"],
       "*.{js,ts,json,html}": "prettier --write"
     }
     ```

### 6. Add `npx lint-staged` to pre-commit hook

   ```bash
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

npx lint-staged
