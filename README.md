# 📚 Vue 3 Library Management Portal (Module 7)

> A frontend implementation for the Library System project designed in Module 6, focusing on the Book Catalog subsystem.

---

## 👤 Developer Profile
* **Name:** Maria Crischan Panganiban
* **Section:** BSCS 3A
* **Course:** Software Engineering 1

---

## 📖 Project Overview
This repository contains the working prototype for Module 7. While Module 6 established the architectural blueprints and database layouts, this implementation brings the **Book Management** features to life in the browser. It features a responsive, library-inspired interface where administrators and library users can seamlessly handle book records.

### Core Entity Specifications
* **Primary Entity:** Book
* **Data Fields:** 
  * `title` (Book Title)
  * `author` (Author Name)
  * `category` (Genre / Classification)
  * `status` (Availability state: *Available* or *Borrowed*)

---

## 🛠️ Key Functionalities & Features
* **Catalog Management (CRUD):** 
  * Add new books with immediate UI updates.
  * View all entries via an interactive data table.
  * Modify and update existing book details.
  * Remove catalog items safely using confirmation dialogs.
* **Smart Search & Filter:** Quickly locate books filtering by title, author, or category.
* **Data Persistence:** Integrated with browser `localStorage` to retain records across page refreshes (simulation of the Module 6 data layer).
* **Input Validation:** Built-in safeguards preventing empty submissions on required book fields.

---

## ⚙️ Technology Stack
* **Framework:** Vue.js 3 (Composition API)
* **Build Tool:** Vite
* **Styling:** Tailwind CSS v4
* **Storage Engine:** Browser `localStorage` (Key: `panganiban-module7-books`)
* **Versioning & CI:** Git, GitHub, and automated GitHub Actions workflows.

---

## 🚀 Getting Started Locally

To run and test this project on your local machine, execute these commands in your terminal:

1. **Clone the repository:**
   ```bash
   git clone https://github.com/cesspanganiban211-spec/panganiban-module7-vue-system.git