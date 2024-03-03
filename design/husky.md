### Husky

- [husky](https://typicode.github.io/husky/)
- [install guide](https://medium.com/@abpeter14/how-to-install-commitlint-husky-2024-f1157f14006f)
- [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/)
- [conventional commits github](https://github.com/conventional-changelog/commitlint/tree/master/%40commitlint/config-conventional)

`npm install @commitlint/cli @commitlint/config-conventional --save-dev`

`.commitlintrc`

``` json
{
    extends: ['@commitlint/config-conventional']
}
```

`npx husky init`

`.husky/pre-commit`

`.husky/commit-msg`

``` text
npx --no -- commitlint --edit $1
```

