Here's a concise summary of **Vue.js style conventions** based on the [official Vue Style Guide](https://vuejs.org/style-guide/) and common industry practices:

---

### **1. Component Naming**
- **Multi-word names** (avoids HTML element conflicts):  
  ✅ `UserProfile.vue`  
  ❌ `Profile.vue`

- **PascalCase** for filenames:  
  ✅ `TodoList.vue`  
  ❌ `todo-list.vue` (unless in-DOM templates)

---

### **2. Prop Naming**
- **camelCase** in script:  
  ```js
  props: ['userName', 'isActive']
  ```
- **kebab-case** in templates:  
  ```vue
  <UserProfile :user-name="..." :is-active="..." />
  ```

---

### **3. Quotes**
- **Single quotes** in `<script>`:  
  ```js
  const message = 'Hello World'
  ```
- **Double quotes** in `<template>` (HTML/XML convention):  
  ```vue
  <div class="container"></div>
  ```

---

### **4. Directive Shorthands**
- Prefer `:` for `v-bind` and `@` for `v-on`:  
  ```vue
  <img :src="imageUrl" @click="handleClick">
  ```

---

### **5. Component Structure Order**
Recommended order in SFCs:  
```vue
<script>
// 1. Imports
// 2. Component definition
// 3. Props
// 4. Data
// 5. Computed
// 6. Methods
// 7. Lifecycle hooks
</script>

<template>
  <!-- Template markup -->
</template>

<style scoped>
/* Scoped styles */
</style>
```

---

### **6. Function/Variable Naming**
- **camelCase** for variables/functions:  
  ```js
  const isLoading = ref(false)
  function fetchData() { ... }
  ```

- **PascalCase** for components/composables:  
  ```js
  // Composables
  export function useDarkMode() { ... }
  
  // Components
  export default { name: 'DarkModeToggle' }
  ```

---

### **7. Template Formatting**
- **Multi-line elements** for readability:  
  ```vue
  <template>
    <div
      class="container"
      :style="{ color: textColor }"
      @click="handleClick"
    >
      {{ message }}
    </div>
  </template>
  ```

---

### **8. Event Naming**
- **kebab-case** for custom events:  
  ```js
  emit('update:model-value')
  ```
  ```vue
  <MyComponent @update:model-value="..." />
  ```

---

### **9. CSS Scoping**
- Use `scoped` for component-specific styles:  
  ```vue
  <style scoped>
  .container { ... }
  </style>
  ```

---

### **10. File Structure**
```bash
src/
  ├── components/    # Reusable components
  │   └── AppButton.vue
  ├── views/         # Route components
  │   └── HomeView.vue
  ├── composables/   # Composition functions
  │   └── useFetch.js
  ├── stores/        # Pinia stores
  │   └── userStore.js
  └── assets/        # Global styles/images
      └── styles/
          ├── _variables.scss
          └── _mixins.scss
```

---

### **Essential Tools**
1. **ESLint** with [vue-eslint-parser](https://eslint.vuejs.org/)  
2. **Prettier** with [prettier-plugin-vue](https://prettier.io/docs/en/plugins.html)  
3. **Volar** (VS Code extension)

---

### **Key Principle**
The Vue team emphasizes **prioritizing consistency** within your project over rigid adherence to these rules. Choose conventions that work for your team and stick to them!