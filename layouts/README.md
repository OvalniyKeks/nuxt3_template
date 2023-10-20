# Layouts

## Table of Contents

- [About](#about)
- [Directory Structure](#directory_structure)
- [Usage](#usage)

##
<h3><a href="https://nuxt.com/docs/guide/directory-structure/layouts">Документация</a></h3>

##

## About <a name = "about"></a>

Nuxt предоставляет структуру макетов для извлечения общих шаблонов пользовательского интерфейса в макеты многократного использования.
```
Для достижения наилучшей производительности компоненты, помещенные в этот каталог, при использовании будут автоматически загружаться посредством асинхронного импорта.
```

## Directory Structure <a name = "directory_structure"></a>

```
-| layouts/
---| default.vue
---| custom.vue
```

## Usage <a name = "usage"></a>

Подключаем layout для страницы
```html
<script setup lang="ts">
definePageMeta({
  layout: 'custom'
})
</script>
```

### Динамическое изменение layout

Вы также можете использовать метод setPageLayout для динамического изменения макета:

```html
<script setup lang="ts">
function enableCustomLayout () {
  setPageLayout('custom')
}
definePageMeta({
  layout: false,
});
</script>

<template>
  <div>
    <button @click="enableCustomLayout">Update layout</button>
  </div>
</template>
```
