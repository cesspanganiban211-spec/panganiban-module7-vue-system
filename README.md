# Library Management System — Module 7 Prototype

## Student Information
* **Name:** Maria Crischan Panganiban
* **Course and Section:** BSCS 3A
* **Subject:** Software Engineering 1
* **Module:** Module 7 - Design and Implementation

## System Description
This is a working frontend prototype of the Book Catalog and Management module from the Library System proposed in Module 6. It allows users and staff to add, view, edit, delete, and search book records directly in the browser with a clean library-themed UI.

## Selected Module 6 Entity
Book, with fields: title, author, category, and status (Available / Borrowed).

## Implemented Features
* Add a new book record (Create)
* View all books in a table (Read)
* Edit an existing book record (Update)
* Delete a book record with confirmation (Delete)
* Search books by title, author, or category
* Form validation for required fields
* Data persists after refresh via localStorage

## Technologies Used
* Vue.js 3 + Vite
* Tailwind CSS v4
* JavaScript (Composition API)
* Browser localStorage
* Git + GitHub
* GitHub Actions (CI build check)

## Installation and Run Instructions
* Clone the repository: `git clone https://github.com/cesspanganiban211-spec/panganiban-module7-vue-system.git`
* Go to the project folder: `cd panganiban-module7-vue-system`
* Install dependencies: `npm install`
* Run the app: `npm run dev`
* Open the local address shown in the terminal example `http://localhost:5173/`

## About localStorage
This prototype simulates the data layer using the browser's localStorage instead of a real database. All book records are saved under the key `panganiban-module7-books` and are read back automatically when the app loads. This is a temporary browser-only substitute for the database data layer proposed in the Module 6 architecture.

## Connection Between Module 6 and Module 7
Module 6 proposed a three-tier architecture with Vue.js as the presentation layer, a backend service as the application layer, and a database layer. Module 7 implements only the presentation layer and a simulated data layer using localStorage for the Book entity, while the backend, API, and database remain proposed future components.

## Known Limitations and Future Improvements
* No real backend, API, or database connection yet, data is local to the browser only.
* No user authentication or multi-user support.
* Future versions will connect to the backend and database stack as proposed in Module 6.