# Подготовка (git, eslint, husky)


`git init`
Промпт: "Опиши конфигурацию .gitignore для проекта JavaScript + Hustky + ESLint, в качестве редактора используется VSCode."
```
# Зависимости
node_modules/
.pnp
.pnp.js

# Сборка
dist/
build/
out/
.next/
.turbo/

# Кэш и временные файлы
.eslintcache
lint-results/
coverage/
.nyc_output/

# Husky (рекомендуется не игнорировать саму папку .husky)
.husky/_/

# VSCode
.vscode/*
!.vscode/settings.json
!.vscode/tasks.json
!.vscode/launch.json
!.vscode/extensions.json
*.code-workspace
.history/

# Переменные окружения
.env
.env.local
.env.*.local
!.env.example

# Логи
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*
.pnpm-debug.log*

# ОС
.DS_Store
Thumbs.db
```

`npm init -y`

`npx eslint --init`
```
√ What do you want to lint? · javascript
√ How would you like to use ESLint? · problems
√ What type of modules does your project use? · esm
√ Which framework does your project use? · none
√ Does your project use TypeScript? · No
√ Where does your code run? · browser, node
```

Добавлен "lint" в package.json:
```json
{
  "name": "lab1",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "lint": "eslint .",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "type": "commonjs",
  "devDependencies": {
    "@eslint/js": "^10.0.1",
    "eslint": "^10.14.0",
    "globals": "^17.14.0"
  }
}

```

`npx husky init`
Промпт: "Опиши, как добавить хук husky для запуска npm run lint перед коммитом."
```
pre-commit -> npm run lint
```


# Выполнение


Первый коммит:
```
> lab1@1.0.0 lint
> eslint .


C:\HERZEN\ВЕБ\lab1\calc.js
   3:7   error  'temp' is assigned a value but never used                           no-unused-vars
   5:10  error  'add' is defined but never used                                     no-unused-vars
   9:10  error  'sub' is defined but never used                                     no-unused-vars
  13:10  error  'mul' is defined but never used                                     no-unused-vars
  17:10  error  'div' is defined but never used                                     no-unused-vars
  24:13  error  'summ' is not defined                                               no-undef
  27:1   error  'count' is assigned a value but never used                          no-unused-vars
  27:1   error  The value assigned to 'count' is not used in subsequent statements  no-useless-assignment
  27:9   error  'count' is assigned to itself                                       no-self-assign
  29:5   error  Unexpected constant condition                                       no-constant-condition

✖ 10 problems (10 errors, 0 warnings)

husky - pre-commit script failed (code 1)
```

Исправлены ошибки в calc.js:
```js
function add(a, b) {
  return a + b;
}

function sub(a, b) {
  return a - b;
}

function mul(a, b) {
  return a * b;
}

function div(a, b) {
  if (b === 0) {
    return null;
  }
  return a / b;
}

while (true) {
  console.log('always');
}
```

Функции оставлены по заданию лабораторной работы
> в файле calc.js реализованы функции add, sub, mul, div, а также блок console.log

Промпт: "Как исключить проверку no-unused-vars eslint (функция не используется, но должна остаться)?"
```js
// eslint-disable-next-line no-unused-vars
function myLegacyFunction() {
  // ... код функции, который пока не используется
}
```

Добавлены исключения для функций:
```js
// eslint-disable-next-line no-unused-vars
function add(a, b) {
  return a + b;
}

// eslint-disable-next-line no-unused-vars
function sub(a, b) {
  return a - b;
}

// eslint-disable-next-line no-unused-vars
function mul(a, b) {
  return a * b;
}

// eslint-disable-next-line no-unused-vars
function div(a, b) {
  if (b === 0) {
    return null;
  }
  return a / b;
}

while (true) {
  console.log('always');
}
```

Второй коммит:
```
> lab1@1.0.0 lint
> eslint .

[master (root-commit) 2f688f5] second commit
 1 file changed, 26 insertions(+)
 create mode 100644 calc.js
```
