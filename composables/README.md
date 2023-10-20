# Composables

## Table of Contents

- [About](#about)
- [How Files Are Scanned](#directory_structure)
- [Usage](#usage)

##
<h3><a href="https://nuxt.com/docs/guide/directory-structure/composables">Документация</a></h3>

##

## About <a name = "about"></a>

Используйте каталог composables/ для автоматического импорта компонуемых объектов Vue в ваше приложение.

## How Files Are Scanned <a name = "directory_structure"></a>

Nuxt сканирует только файлы верхнего уровня каталога composables/, например:

```
| composables/
---| index.ts     // scanned
---| useFoo.ts    // scanned
-----| nested/
-------| utils.ts // not scanned
```

Чтобы автоматический импорт работал для вложенных модулей, вы можете либо повторно экспортировать их (рекомендуется), либо настроить сканер на включение вложенных каталогов: <Br>

Пример: повторно экспортируйте нужные вам составные элементы из файла composables/index.ts:

```ts
// composables/index.ts
// Enables auto import for this export
export { utils } from './nested/utils.ts'
```


Пример: Сканировать вложенные каталоги внутри папки composable/:

```js
//nuxt.config.ts
export default defineNuxtConfig({
  imports: {
    dirs: [
      // Scan top-level modules
      'composables',
      // ... or scan modules nested one level deep with a specific name and file extension
      'composables/*/index.{ts,js,mjs,mts}',
      // ... or scan all modules within given directory
      'composables/**'
    ]
  }
})
```

## Usage <a name = "usage"></a>

__Способ 1__: Использование именованного экспорта

```js
export const useFoo = () => {
  return useState('foo', () => 'bar')
}
```

__Способ 2__. Использование экспорта по умолчанию.
```js
// It will be available as useFoo() (camelCase of file name without extension)
export default function () {
  return useState('foo', () => 'bar')
}
```

### Использование в компонентах
```html
<script setup lang="ts">
  const foo = useFoo()
</script>

<template>
  <div>
    {{ foo }}
  </div>
</template>
```
