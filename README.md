# Code-Style-Frontend-
## 1. References & Variables



* Use `const` for every variable that is not reassigned; never use `var`.

* Use `let` only when reassignment is required.



```
const API_BASE = 'https://example.com/api'
let currentResult = ''
```

## 2. Naming



| Item                  | Rule                   | Example                      |
| --------------------- | ---------------------- | ---------------------------- |
| Variables / functions | camelCase              | `convertBase`, `loadHistory` |
| Components / Vue SFC  | PascalCase             | `CalculatorPanel`            |
| Constants             | UPPER\_SNAKE\_CASE     | `API_BASE`                   |
| Boolean               | prefix `is/has/should` | `isFavorite`, `hasError`     |

## 3. Strings



* Use single quotes for JS strings (consistent with the project template).

* Use template literals for interpolation instead of string concatenation.



```
const url = `${API_BASE}/history/${id}/favorite`
```

## 4. Functions



* Use arrow functions for short callbacks.

* Prefer named function declarations for top-level logic.

* Always use parentheses around arrow parameters.



```
const toggleFavorite = async (id) => {
  await uni.request({ url: `${API_BASE}/history/${id}/favorite`, method: 'POST' })
}
```

## 5. Objects & Arrays



* Use literal syntax: `const item = {}`, `const list = []`.

* Use object/array spread for copies instead of `push` mutation where possible.



```
const nextList = [...historyList.value, newItem]
```

## 6. Conditionals



* Always use braces for `if` / `else`, even for one-line bodies.

* Use strict equality `===` / `!==`; never `==` / `!=`.



```
if (res.data.success === true) {
  currentResult.value = res.data.result
}
```

## 7. Vue 3 `<script setup>` Conventions



* Ref / reactive state declared at the top, business functions below.

* Emit API calls through a single `API_BASE` constant (no hard-coded URLs inside functions).

* Keep the template free of logic; format numbers in a helper function.



```
import { ref } from 'vue'

const expression = ref('')
const calculate = async () => { ... }
```

## 8. SFC / Template Conventions



* Attribute order: `v-if`, `v-for`, `v-model`, `:prop`, `@event`.

* Use kebab-case for custom CSS classes: `class="calc-panel"`.

* One logical component section per block.



```
<view class="key num" @tap="appendValue('7')">7</view>
```

## 9. Comments & Readability



* Prefer self-explanatory names over comments.

* Use comments only for non-obvious "why", not "what".

* No commented-out dead code left in commits.

## 10. Example (Compliant)



```
const calculate = async () => {
  if (!expression.value.trim()) {
    errorMsg.value = 'Please enter an expression'
    return
  }
  try {
    const res = await uni.request({
      url: `${API_BASE}/calculate`,
      method: 'POST',
      header: { 'Content-Type': 'application/json' },
      data: { expression: expression.value }
    })
    if (res.data.success === true) {
      currentResult.value = res.data.result
      loadHistory()
    } else {
      errorMsg.value = res.data.error
    }
  } catch (e) {
    errorMsg.value = 'Cannot connect to server'
  }
}
```
