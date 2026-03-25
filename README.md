# 📚 VibeReads

VibeReads is an AI-powered book discovery platform that helps users find books based on **mood, themes, and natural language descriptions** — not just titles or authors.

Instead of searching *what you know*, VibeReads helps you discover *what you feel like reading*.

---

## 🚀 Core Idea

Traditional platforms like Goodreads rely on keyword-based search.

VibeReads introduces **vibe-based search**, allowing users to type queries like:

> "a dark psychological thriller with a shocking twist"

and receive **semantically relevant book recommendations** powered by embeddings and vector search.

---

## 🎯 MVP Scope

The MVP focuses on validating one core hypothesis:

> Users prefer vibe-based search over traditional search when discovering books.

### Included

* Vibe-based search input
* Book recommendations (semantic similarity)
* Basic results display (title, author, cover, synopsis)

### Excluded (for now)

* Social features (clubs, feeds)
* Advanced recommendations
* Complex personalization

---

## 🧱 Tech Stack

### Frontend

* Next.js (App Router)
* TypeScript
* Tailwind CSS
* TanStack Query

### Backend

* ASP.NET Core Web API
* Clean Architecture

### Database

* PostgreSQL
* pgvector (vector similarity search)

### Infrastructure (planned)

* Docker
* Redis (caching)
* Azure (deployment)

---

## 🏗️ Project Structure

vibereads/
│
├── frontend/        # Next.js app
├── backend/         # ASP.NET Core API
├── database/        # migrations, seeds
├── docs/            # product & architecture docs
├── docker/          # container configs (later)
│
├── .env.example
├── README.md
└── .gitignore

---

## 🧠 How It Works (High-Level)

1. User enters a natural language query ("vibe")
2. Backend converts query → embedding
3. Embedding is compared against stored book vectors (pgvector)
4. Top matching books are returned
5. Frontend displays ranked results

---

## 📊 Product Context

This project is developed as part of the **Gjirafa LIFE AI Engineering Program (Phase 3)**.

The focus is on:

* Real-world product thinking
* MVP validation
* Full-stack system design
* AI-powered features

---

## ⚙️ Getting Started (WIP)

Clone the repository and navigate into it:

git clone https://github.com/your-username/vibereads.git
cd vibereads

More setup instructions will be added as development progresses.

---

## 📌 Status

🚧 Project initialized
🔜 Core MVP development starting

---

## 👥 Team

* Samir Sahiti
* Fisnik Percuku
* Yllka Nuredini

---

## 🧭 Vision

Build a platform where:

> You don’t need to know the book — just how you want to feel.
