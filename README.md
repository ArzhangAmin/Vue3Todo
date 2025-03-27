# 🚀 Vue 3 Todo App (Composition API)

![Vue 3](https://img.shields.io/badge/Vue.js-3.x-4FC08D?logo=vuedotjs)
![Composition API](https://img.shields.io/badge/API-Composition-35495E)
![License](https://img.shields.io/badge/License-MIT-blue)

A feature-rich todo application built with Vue 3's Composition API featuring:
- **Drag-and-drop** task reordering
- **Dark/light mode** toggle
- **Real-time filtering** (All/Active/Completed)
- **Interactive toast notifications**

## ✨ Features

| Feature          | Implementation Details              |
|------------------|-------------------------------------|
| **Task Management** | Add, complete, delete and reorder tasks |
| **Theme Switching** | CSS variables with dynamic toggling |
| **Drag-and-Drop** | Native HTML5 Drag API implementation |
| **Notifications** | vue-toastification for user feedback |

## 🛠 Tech Stack

- **Vue 3** - Composition API
- **Vue-toastification** - Beautiful notifications
- **CSS Variables** - Theme switching
- **HTML5 Drag API** - Native reordering

## 🚀 Installation

1. Clone the repository:
```bash
git clone https://github.com/ArzhangAmin/vue3-todo-app.git

2. Install dependencies:
npm install

3. Run development server:
npm run dev


📂 Project Structure
src/
├── components/
│   ├── AppHeader.vue     # Header with theme toggle
│   ├── AddTodo.vue       # Task input component
│   ├── Todo.vue          # Individual todo item
│   └── AppFooter.vue     # Footer instructions
├── App.vue               # Main application
└── main.js               # Vue initialization


💡 Key Code Examples
Drag-and-Drop Implementation:

function drop(index) {
  const newElement = todos.value.splice(dragging.value, 1)[0]
  todos.value.splice(index, 0, newElement)
}

Theme Switching:
const changeTheme = () => {
  document.body.classList.toggle('light', defaultTheme.value === 'light')
}

📝 License
MIT © [ArzhangAmin]
