# 📚 Vue 3 Library Management Portal (Module 7)

## Student Information
* **Name:** Princess T. Panganiban
* **Course and Section:** BSCS 3A
* **Subject:** Software Engineering 1
* **Module:** Module 7 - Design and Implementation

## System Description and Selected Module 6 Entity
This is a working frontend prototype of the Book Catalog and Management module from the Library System proposed in Module 6. It allows users and staff to manage book inventory directly within the browser with a clean library-themed user interface.
* **Selected Module 6 Entity:** Book
* **Entity Attributes:** `title`, `author`, `category`, and `status` (Available / Borrowed).

## Implemented Features
* Add a new book record (Create)
* View all books in an organized table (Read)
* Edit an existing book record (Update)
* Delete a book record with confirmation (Delete)
* Search books by title, author, or category
* Form validation for required fields
* Data persists after refresh via browser `localStorage`

## Technologies Used
* Vue.js 3 (Composition API)
* Vite
* Tailwind CSS v4
* Browser `localStorage`
* Git + GitHub
* GitHub Actions (CI build check)

## Installation and Run Instructions
1. **Clone the repository:**
   ```bash
git clone https://github.com/cesspanganiban211-spec/panganiban-module7-vue-system.git

## Explanation of localStorage
This prototype simulates the data layer using the browser's localStorage instead of a real database. All book records are saved under the key panganiban-module7-books and are loaded back automatically whenever the app starts. This serves as a temporary browser-only substitute for the database data layer proposed in the Module 6 architecture.

## Connection Between Module 6 and Module 7
Module 6 proposed a multi-tier system architecture featuring Vue.js as the presentation layer, a backend service as the application layer, and a database layer. Module 7 specifically implements the presentation layer and a simulated data layer using localStorage for the Book entity, while the backend, API, and database remain as proposed future components.

## Application Screenshots
*(Add your application screenshots here once captured, e.g., using Markdown images: ![Dashboard](./path-to-image.png))*

## Known Limitations and Proposed Future Improvements
* **Limitations:**
  * No real backend, API, or database connection (data is local to the browser only).
  * No user authentication or multi-user access control.
* **Future Improvements:**
  * Connect the frontend to a Node.js/Express backend and MongoDB Atlas database as originally designed in Module 6.
  * Implement user authentication for librarians and library members.

  ## Application Screenshots

### Running Application


![Running application](docs/screenshots/01-running-application.png)



### Add Record


![Add record](docs/screenshots/02-add-record.png)



### Record List


![Record list](docs/screenshots/03-record-list.png)



### Edit Record


![Edit record](docs/screenshots/04-edit-record.png)



### Delete Confirmation


![Delete confirmation](docs/screenshots/05-delete-confirmation.png)



### Search Function


![Search function](docs/screenshots/06-search-function.png)



### localStorage (Browser DevTools)


![localStorage](docs/screenshots/07-localstorage.png)



### Responsive View


![Responsive view](docs/screenshots/08-responsive-view.png)



### GitHub Repository


![GitHub repository](docs/screenshots/09-github-repository.png)



### Commit History


![Commit history](docs/screenshots/10-commit-history.png)



### CI Build Success


![CI success](docs/screenshots/11-ci-success.png)
