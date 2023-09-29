# Working with Local Storage, Session Storage, and IndexedDB
Check: 
- https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage
- https://developer.mozilla.org/en-US/docs/Web/API/Window/sessionStorage
- https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API

## Introduction

In web development, there are several mechanisms available for storing data on the client-side, such as Local Storage, Session Storage, and IndexedDB. Each of these technologies serves different purposes and has its own strengths and limitations.

## Local Storage

Local Storage is a simple key-value storage mechanism that allows you to store data persistently in the browser. Here's an overview:

- **Scope**: Data stored in Local Storage is persistent across browser sessions and remains available even after the browser is closed.

- **Storage Limit**: Local Storage typically allows you to store up to 5-10 MB of data, depending on the browser.

- **Use Cases**:
  - Storing user preferences/settings.
  - Caching small amounts of data to improve application performance.

- **Usage**:
  - To set an item in Local Storage:
    ```javascript
    localStorage.setItem('key', 'value');
    ```
  - To get an item from Local Storage:
    ```javascript
    const value = localStorage.getItem('key');
    ```
  - To remove an item from Local Storage:
    ```javascript
    localStorage.removeItem('key');
    ```

## Session Storage

Session Storage is similar to Local Storage but with a shorter lifespan. Here's an overview:

- **Scope**: Data stored in Session Storage is available only for the duration of a single page session. It gets cleared when the user closes the browser tab or window.

- **Storage Limit**: Similar to Local Storage, Session Storage also has a storage limit of 5-10 MB, depending on the browser.

- **Use Cases**:
  - Storing data that should be available only during the current page session.
  - Implementing features like "Remember Me" for login forms.

- **Usage**:
  - Session Storage uses the same methods as Local Storage (`setItem`, `getItem`, `removeItem`).

```javascript
// Setting a session storage item
sessionStorage.setItem('key', 'value');

// Getting a session storage item
const value = sessionStorage.getItem('key');

// Removing a session storage item
sessionStorage.removeItem('key');
```

## IndexedDB

IndexedDB is a low-level, transactional database system for storing large amounts of structured data on the client-side. Here's an overview:

- **Scope**: IndexedDB is more powerful and flexible compared to Local Storage and Session Storage. It's designed for storing complex data, such as objects and structured data.

- **Storage Limit**: IndexedDB allows you to store much larger amounts of data compared to Local Storage or Session Storage. The storage limit is typically several hundred megabytes.

- **Use Cases**:
  - Storing large datasets, such as offline web applications or cached data.
  - Implementing more advanced database-like functionality in web applications.

- **Usage**:
  - IndexedDB uses a more complex API compared to Local Storage and Session Storage. It involves opening a database, creating object stores, and managing transactions.

```javascript
// Opening a database
const request = indexedDB.open('myDatabase', 1);

request.onupgradeneeded = (event) => {
  const db = event.target.result;
  const store = db.createObjectStore('myStore', { keyPath: 'id' });
};

request.onsuccess = (event) => {
  const db = event.target.result;
  const transaction = db.transaction('myStore', 'readwrite');
  const store = transaction.objectStore('myStore');
  
  // Adding data
  store.add({ id: 1, name: 'Item 1' });
  
  // Retrieving data
  const getRequest = store.get(1);
  
  getRequest.onsuccess = (event) => {
    const item = event.target.result;
    console.log(item);
  };
};
```