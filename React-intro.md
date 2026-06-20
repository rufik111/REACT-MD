
# 🔹 1. React və Onun Xüsusiyyətləri

### React Nədir? 

React - Facebook tərəfindən yaradılmış JavaScript kitabxanasıdır. İstifadəçi interfeyslərini (UI) qurmaq üçün istifadə olunur.

### React-in Əsas Xüsusiyyətləri:

- **Virtual DOM** - Performansı artırır
- **Component-based** - Təkrar istifadə edilən komponentlər
- **One-way data flow** - Məlumatlar yalnız bir istiqamətdə hərəkət edir
- **Declarative** - Nə istədiyinizi yazırsınız, necə ediləcəyini React həll edir

# Create react App

I'll help you create your first React app! Here's a step-by-step guide to get you started.
 
## Prerequisites

Make sure you have Node.js installed on your computer. You can download it from [nodejs.org](https://nodejs.org/).

## Creating Your First React App

**1. Open your terminal/command prompt**

**2. Create a new React app using Create React App:**

```bash
npx create-react-app my-first-app
```

(Replace "my-first-app" with whatever you want to name your project)

**3. Navigate into your project folder:**

```bash
cd my-first-app
```

**4. Start the development server:**

```bash
npm start
```

This will automatically open your new React app in your browser at `http://localhost:3000`. You should see the default React welcome page with a spinning React logo.

## Understanding the Project Structure

Your new React app will have this structure:

```
my-first-app/
├── public/
├── src/
│   ├── App.js          # Main component
│   ├── App.css         # Styling for App
│   ├── index.js        # Entry point
│   └── index.css       # Global styles
├── package.json
└── README.md
```

## Making Your First Changes

Try editing the `src/App.js` file - change some text and save the file. You'll see the changes instantly in your browser thanks to hot reloading!

Would you like me to show you how to create a simple custom component or explain any specific part of React in more detail?

---

## 🔹 2. JSX və Komponent Strukturu

### JSX Nədir?

JSX (JavaScript XML) - JavaScript daxilində HTML yazmağa imkan verir.

```jsx
// JSX Nümunəsi
const element = <h1>Salam Dünya!</h1>;

// JavaScript-ə çevrilir:
const element = React.createElement('h1', null, 'Salam Dünya!');
```

### JSX Qaydaları:

1. **Tek parent element** olmalıdır
2. **className** istifadə edin (class deyil)
3. **CamelCase** istifadə edin
4. **Self-closing tags** lazımdır

```jsx
// Düzgün JSX
function App() {
  return (
    <div>
      <h1 className="title">Başlıq</h1>
      <img src="image.jpg" alt="Şəkil" />
    </div>
  );
}
```

### React Fragment:

```jsx
// Fragment istifadəsi
function App() {
  return (
    <React.Fragment>
      <h1>Başlıq</h1>
      <p>Mətn</p>
    </React.Fragment>
  );
}

// Qısa yazılış
function App() {
  return (
    <>
      <h1>Başlıq</h1>
      <p>Mətn</p>
    </>
  );
}
```

---

## 🔹 3. Props və State

### Props (Properties)

Props - komponentlərə verilən parametrlərdir. Dəyişdirilə bilməz (immutable).

```jsx
// Parent Komponent
function App() {
  return (
    <div>
      <Welcome name="Əli" age={25} />
      <Welcome name="Ayşə" age={22} />
    </div>
  );
}

// Child Komponent
function Welcome(props) {
  return (
    <div>
      <h1>Salam {props.name}</h1>
      <p>Yaş: {props.age}</p>
    </div>
  );
}

// Destructuring ilə
function Welcome({ name, age }) {
  return (
    <div>
      <h1>Salam {name}</h1>
      <p>Yaş: {age}</p>
    </div>
  );
}
```

### Default Props:

```jsx
function Welcome({ name = "Qonaq", age = 0 }) {
  return (
    <div>
      <h1>Salam {name}</h1>
      <p>Yaş: {age}</p>
    </div>
  );
}
```

### State

State - komponentin daxili vəziyyətidir. Dəyişdirilə bilər.

```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Sayğac: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        Artır
      </button>
    </div>
  );
}
```

---

## 🔹 4. Hook-lar

### useState Hook

Functional komponentlərdə state istifadə etmək üçün.

```jsx
import { useState } from 'react';

function Example() {
  // State elan etmək
  const [name, setName] = useState('');
  const [age, setAge] = useState(0);
  const [isVisible, setIsVisible] = useState(true);

  // Array state
  const [items, setItems] = useState([]);

  // Object state
  const [user, setUser] = useState({
    name: '',
    email: ''
  });

  const updateUser = () => {
    setUser(prevUser => ({
      ...prevUser,
      name: 'Yeni Ad'
    }));
  };

  return (
    <div>
      <input 
        value={name} 
        onChange={(e) => setName(e.target.value)} 
      />
      <p>Ad: {name}</p>
    </div>
  );
}
```

### useEffect Hook

Side effect-lər üçün (API çağırışları, subscription-lar, DOM dəyişiklikləri).

```jsx
import { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);
  const [data, setData] = useState(null);

  // Component mount olduqda çalışır
  useEffect(() => {
    console.log('Komponent yükləndi');
  }, []); // Boş array - yalnız bir dəfə çalışır

  // Count dəyişdikdə çalışır
  useEffect(() => {
    document.title = `Sayğac: ${count}`;
  }, [count]); // count dependency

  // Hər render-də çalışır
  useEffect(() => {
    console.log('Hər render-də çalışır');
  }); // Dependency array yoxdur

  // Cleanup function
  useEffect(() => {
    const timer = setInterval(() => {
      console.log('Timer çalışır');
    }, 1000);

    // Cleanup
    return () => {
      clearInterval(timer);
    };
  }, []);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        Artır
      </button>
    </div>
  );
}
```

### useRef Hook

DOM elementlərinə birbaşa giriş və dəyərləri saxlamaq üçün.

```jsx
import { useRef, useEffect } from 'react';

function Example() {
  const inputRef = useRef(null);
  const countRef = useRef(0);

  useEffect(() => {
    // Input-a fokus ver
    inputRef.current.focus();
  }, []);

  const handleClick = () => {
    countRef.current += 1;
    console.log('Click sayı:', countRef.current);
  };

  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={handleClick}>
        Klik et
      </button>
    </div>
  );
}
```

---

## 🔹 5. Controlled Forms

### Controlled Components

Form elementlərinin dəyəri React state tərəfindən idarə olunur.

```jsx
import { useState } from 'react';

function ContactForm() {
  const [formData, setFormData] = useState({
    name: '',
    email: '',
    message: '',
    gender: '',
    isSubscribed: false
  });

  const handleChange = (e) => {
    const { name, value, type, checked } = e.target;
    setFormData(prev => ({
      ...prev,
      [name]: type === 'checkbox' ? checked : value
    }));
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log('Form məlumatları:', formData);
  };

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label>Ad:</label>
        <input
          type="text"
          name="name"
          value={formData.name}
          onChange={handleChange}
          required
        />
      </div>

      <div>
        <label>Email:</label>
        <input
          type="email"
          name="email"
          value={formData.email}
          onChange={handleChange}
          required
        />
      </div>

      <div>
        <label>Mesaj:</label>
        <textarea
          name="message"
          value={formData.message}
          onChange={handleChange}
          rows="4"
        />
      </div>

      <div>
        <label>Cins:</label>
        <select
          name="gender"
          value={formData.gender}
          onChange={handleChange}
        >
          <option value="">Seçin</option>
          <option value="male">Kişi</option>
          <option value="female">Qadın</option>
        </select>
      </div>

      <div>
        <label>
          <input
            type="checkbox"
            name="isSubscribed"
            checked={formData.isSubscribed}
            onChange={handleChange}
          />
          Xəbərlərə abunə ol
        </label>
      </div>

      <button type="submit">Göndər</button>
    </form>
  );
}
```

---

## 🔹 6. Component Lifecycle

### Functional Components (Hooks ilə)

```jsx
import { useState, useEffect } from 'react';

function LifecycleExample() {
  const [count, setCount] = useState(0);

  // componentDidMount
  useEffect(() => {
    console.log('Komponent mount oldu');
    
    // componentWillUnmount
    return () => {
      console.log('Komponent unmount oldu');
    };
  }, []);

  // componentDidUpdate
  useEffect(() => {
    console.log('Count dəyişdi:', count);
  }, [count]);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        Artır
      </button>
    </div>
  );
}
```

### Class Components (Ənənəvi üsul)

```jsx
import React, { Component } from 'react';

class LifecycleExample extends Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
    console.log('Constructor çalışdı');
  }

  componentDidMount() {
    console.log('Komponent mount oldu');
  }

  componentDidUpdate(prevProps, prevState) {
    if (prevState.count !== this.state.count) {
      console.log('Count dəyişdi:', this.state.count);
    }
  }

  componentWillUnmount() {
    console.log('Komponent unmount olacaq');
  }

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Artır
        </button>
      </div>
    );
  }
}
```

---

## 🔹 7. To-Do List App - Praktik Tapşırıq

### Tam To-Do List Komponenti:

```jsx
import React, { useState, useEffect, useRef } from 'react';
import './TodoApp.css';

function TodoApp() {
  const [todos, setTodos] = useState([]);
  const [inputValue, setInputValue] = useState('');
  const [filter, setFilter] = useState('all'); // all, active, completed
  const inputRef = useRef(null);

  // localStorage-dən məlumatları yüklə
  useEffect(() => {
    const savedTodos = localStorage.getItem('todos');
    if (savedTodos) {
      setTodos(JSON.parse(savedTodos));
    }
  }, []);

  // todos dəyişdikdə localStorage-ə yaz
  useEffect(() => {
    localStorage.setItem('todos', JSON.stringify(todos));
  }, [todos]);

  // Component mount olduqda input-a fokus ver
  useEffect(() => {
    inputRef.current.focus();
  }, []);

  // Yeni todo əlavə et
  const addTodo = (e) => {
    e.preventDefault();
    if (inputValue.trim()) {
      const newTodo = {
        id: Date.now(),
        text: inputValue.trim(),
        completed: false,
        createdAt: new Date().toLocaleString()
      };
      setTodos([...todos, newTodo]);
      setInputValue('');
      inputRef.current.focus();
    }
  };

  // Todo-nu sil
  const deleteTodo = (id) => {
    setTodos(todos.filter(todo => todo.id !== id));
  };

  // Todo-nun vəziyyətini dəyiş
  const toggleTodo = (id) => {
    setTodos(todos.map(todo =>
      todo.id === id
        ? { ...todo, completed: !todo.completed }
        : todo
    ));
  };

  // Todo-nu redaktə et
  const editTodo = (id, newText) => {
    setTodos(todos.map(todo =>
      todo.id === id
        ? { ...todo, text: newText }
        : todo
    ));
  };

  // Tamamlanmış todo-ları sil
  const clearCompleted = () => {
    setTodos(todos.filter(todo => !todo.completed));
  };

  // Hamısını seç/seçmə
  const toggleAll = () => {
    const allCompleted = todos.every(todo => todo.completed);
    setTodos(todos.map(todo => ({
      ...todo,
      completed: !allCompleted
    })));
  };

  // Filter-ə görə todo-ları göstər
  const filteredTodos = todos.filter(todo => {
    switch (filter) {
      case 'active':
        return !todo.completed;
      case 'completed':
        return todo.completed;
      default:
        return true;
    }
  });

  // Statistika
  const activeCount = todos.filter(todo => !todo.completed).length;
  const completedCount = todos.filter(todo => todo.completed).length;

  return (
    <div className="todo-app">
      <h1>📝 To-Do List</h1>
      
      {/* Todo əlavə etmə formu */}
      <form onSubmit={addTodo} className="add-form">
        <input
          ref={inputRef}
          type="text"
          value={inputValue}
          onChange={(e) => setInputValue(e.target.value)}
          placeholder="Yeni tapşırıq əlavə et..."
          className="add-input"
        />
        <button type="submit" className="add-button">
          ➕ Əlavə et
        </button>
      </form>

      {/* Statistika */}
      {todos.length > 0 && (
        <div className="stats">
          <span>Ümumi: {todos.length}</span>
          <span>Aktiv: {activeCount}</span>
          <span>Tamamlanmış: {completedCount}</span>
        </div>
      )}

      {/* Əməliyyatlar */}
      {todos.length > 0 && (
        <div className="actions">
          <button 
            onClick={toggleAll}
            className="toggle-all-btn"
          >
            {todos.every(todo => todo.completed) ? '🔲' : '☑️'} 
            Hamısını seç
          </button>
          
          {completedCount > 0 && (
            <button 
              onClick={clearCompleted}
              className="clear-completed-btn"
            >
              🗑️ Tamamlanmışları sil
            </button>
          )}
        </div>
      )}

      {/* Filter düymələri */}
      <div className="filters">
        <button 
          onClick={() => setFilter('all')}
          className={filter === 'all' ? 'active' : ''}
        >
          Hamısı
        </button>
        <button 
          onClick={() => setFilter('active')}
          className={filter === 'active' ? 'active' : ''}
        >
          Aktiv
        </button>
        <button 
          onClick={() => setFilter('completed')}
          className={filter === 'completed' ? 'active' : ''}
        >
          Tamamlanmış
        </button>
      </div>

      {/* Todo siyahısı */}
      <div className="todo-list">
        {filteredTodos.length === 0 ? (
          <p className="empty-message">
            {filter === 'all' 
              ? 'Hələ heç bir tapşırıq yoxdur 🤷‍♂️'
              : filter === 'active'
              ? 'Aktiv tapşırıq yoxdur ✅'
              : 'Tamamlanmış tapşırıq yoxdur 📝'
            }
          </p>
        ) : (
          filteredTodos.map(todo => (
            <TodoItem
              key={todo.id}
              todo={todo}
              onToggle={toggleTodo}
              onDelete={deleteTodo}
              onEdit={editTodo}
            />
          ))
        )}
      </div>
    </div>
  );
}

// Ayrıca Todo Item komponenti
function TodoItem({ todo, onToggle, onDelete, onEdit }) {
  const [isEditing, setIsEditing] = useState(false);
  const [editText, setEditText] = useState(todo.text);
  const editInputRef = useRef(null);

  // Redaktə rejimə keçdikdə input-a fokus ver
  useEffect(() => {
    if (isEditing) {
      editInputRef.current.focus();
    }
  }, [isEditing]);

  const handleEdit = () => {
    if (editText.trim() && editText !== todo.text) {
      onEdit(todo.id, editText.trim());
    }
    setIsEditing(false);
  };

  const handleKeyDown = (e) => {
    if (e.key === 'Enter') {
      handleEdit();
    } else if (e.key === 'Escape') {
      setEditText(todo.text);
      setIsEditing(false);
    }
  };

  return (
    <div className={`todo-item ${todo.completed ? 'completed' : ''}`}>
      <input
        type="checkbox"
        checked={todo.completed}
        onChange={() => onToggle(todo.id)}
        className="todo-checkbox"
      />
      
      {isEditing ? (
        <input
          ref={editInputRef}
          type="text"
          value={editText}
          onChange={(e) => setEditText(e.target.value)}
          onBlur={handleEdit}
          onKeyDown={handleKeyDown}
          className="edit-input"
        />
      ) : (
        <span 
          className="todo-text"
          onDoubleClick={() => setIsEditing(true)}
          title="Redaktə etmək üçün iki dəfə klik edin"
        >
          {todo.text}
        </span>
      )}
      
      <div className="todo-actions">
        <button
          onClick={() => setIsEditing(!isEditing)}
          className="edit-btn"
          title="Redaktə et"
        >
          ✏️
        </button>
        <button
          onClick={() => onDelete(todo.id)}
          className="delete-btn"
          title="Sil"
        >
          🗑️
        </button>
      </div>
      
      <small className="todo-date">{todo.createdAt}</small>
    </div>
  );
}

export default TodoApp;
```

### CSS Stilləri (TodoApp.css):

```css
.todo-app {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.todo-app h1 {
  text-align: center;
  color: #333;
  margin-bottom: 30px;
}

.add-form {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.add-input {
  flex: 1;
  padding: 12px;
  font-size: 16px;
  border: 2px solid #ddd;
  border-radius: 5px;
  outline: none;
}

.add-input:focus {
  border-color: #007bff;
}

.add-button {
  padding: 12px 20px;
  background: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
}

.add-button:hover {
  background: #0056b3;
}

.stats {
  display: flex;
  justify-content: space-between;
  background: #f8f9fa;
  padding: 10px;
  border-radius: 5px;
  margin-bottom: 15px;
  font-size: 14px;
}

.actions {
  display: flex;
  gap: 10px;
  margin-bottom: 15px;
}

.toggle-all-btn, .clear-completed-btn {
  padding: 8px 15px;
  border: 1px solid #ddd;
  border-radius: 5px;
  background: white;
  cursor: pointer;
}

.toggle-all-btn:hover, .clear-completed-btn:hover {
  background: #f8f9fa;
}

.filters {
  display: flex;
  gap: 5px;
  margin-bottom: 20px;
  justify-content: center;
}

.filters button {
  padding: 8px 15px;
  border: 1px solid #ddd;
  background: white;
  cursor: pointer;
  border-radius: 5px;
}

.filters button.active {
  background: #007bff;
  color: white;
}

.filters button:hover {
  background: #f8f9fa;
}

.filters button.active:hover {
  background: #0056b3;
}

.todo-list {
  border: 1px solid #ddd;
  border-radius: 5px;
  overflow: hidden;
}

.todo-item {
  display: flex;
  align-items: center;
  padding: 15px;
  border-bottom: 1px solid #eee;
  gap: 10px;
}

.todo-item:last-child {
  border-bottom: none;
}

.todo-item.completed {
  background: #f8f9fa;
  opacity: 0.7;
}

.todo-checkbox {
  width: 20px;
  height: 20px;
  cursor: pointer;
}

.todo-text {
  flex: 1;
  cursor: pointer;
}

.todo-item.completed .todo-text {
  text-decoration: line-through;
  color: #666;
}

.edit-input {
  flex: 1;
  padding: 5px;
  border: 1px solid #007bff;
  border-radius: 3px;
  outline: none;
}

.todo-actions {
  display: flex;
  gap: 5px;
}

.edit-btn, .delete-btn {
  background: none;
  border: none;
  cursor: pointer;
  font-size: 16px;
  padding: 5px;
}

.edit-btn:hover, .delete-btn:hover {
  opacity: 0.7;
}

.todo-date {
  font-size: 11px;
  color: #999;
  white-space: nowrap;
}

.empty-message {
  text-align: center;
  padding: 40px;
  color: #666;
  font-style: italic;
}

/* Responsive */
@media (max-width: 768px) {
  .todo-app {
    padding: 10px;
  }
  
  .add-form {
    flex-direction: column;
  }
  
  .stats {
    flex-direction: column;
    gap: 5px;
  }
  
  .todo-item {
    flex-wrap: wrap;
  }
  
  .todo-date {
    order: 1;
    width: 100%;
    margin-top: 5px;
  }
}
```

---

## 🔹 8. Əlavə Məlumatlar

### Event Handling:

```jsx
function Button() {
  const handleClick = (e) => {
    e.preventDefault();
    console.log('Button clicked');
  };

  const handleMouseEnter = () => {
    console.log('Mouse entered');
  };

  return (
    <button 
      onClick={handleClick}
      onMouseEnter={handleMouseEnter}
    >
      Klik et
    </button>
  );
}
```

### Conditional Rendering:

```jsx
function ConditionalExample({ isLoggedIn, user }) {
  return (
    <div>
      {isLoggedIn ? (
        <h1>Xoş gəlmisiniz, {user.name}!</h1>
      ) : (
        <h1>Zəhmət olmasa giriş edin</h1>
      )}
      
      {isLoggedIn && <p>Şəxsi sahəniz</p>}
      
      {!isLoggedIn && <button>Giriş et</button>}
    </div>
  );
}
```

### List Rendering:

```jsx
function ListExample() {
  const items = [
    { id: 1, name: 'Alma', price: 2 },
    { id: 2, name: 'Banan', price: 3 },
    { id: 3, name: 'Portağal', price: 4 }
  ];

  return (
    <ul>
      {items.map(item => (
        <li key={item.id}>
          {item.name} - {item.price} AZN
        </li>
      ))}
    </ul>
  );
}
```

### Performance Optimization:

```jsx
import { memo, useMemo, useCallback } from 'react';

// React.memo - komponent re-render-ni azaldır
const ExpensiveComponent = memo(function ExpensiveComponent({ data }) {
  return <div>{data}</div>;
});

// useMemo - ağır hesablamaları cache edir
function OptimizedComponent({ items }) {
  const expensiveValue = useMemo(() => {
    return items.reduce((sum, item) => sum + item.price, 0);
  }, [items]);

  return <div>Ümumi qiymət: {expensiveValue}</div>;
}

// useCallback - funksiyaları cache edir
function ParentComponent() {
  const [count, setCount] = useState(0);
  
  const handleClick = useCallback(() => {
    setCount(prev => prev + 1);
  }, []);

  return (
    <div>
      <p>Count: {count}</p>
      <ChildComponent onClick={handleClick} />
    </div>
  );
}
```

Bu konspekt React.js-in əsas konsepsiyalarını əhatə edir və praktik To-Do List app ilə biliklərinizi sınaya bilərsiniz. Hər bir hissəni tədricən öyrənin və çox məşq edin!