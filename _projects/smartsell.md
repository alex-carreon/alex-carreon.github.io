---
layout: single 
classes: wide
title: "SmartSell"
excerpt: "A full-stack web application for order management using Python and Django REST Framework."
header:
  overlay_image: /assets/images/smartsell-banner.png
  overlay_filter: 0.5
  teaser: /assets/images/smartsell-teaser.png
  actions:
    - label: "View on GitHub"
      url: "https://github.com/alex-carreon/smart-sell"
author_profile: true
---

**SmartSell** is a full-stack web application for managing customers and orders, built with a decoupled architecture. A Django REST Framework backend exposes a token-authenticated API, while a separate Django frontend consumes it via HTTP requests. Users can register, log in, and perform full CRUD operations on customers and their associated orders.

## Architecture

This project is split into two independent Django applications:

- **Backend** — REST API built with Django REST Framework. Handles data persistence, authentication, and business logic. Exposes endpoints for customers, orders, and user auth.
- **Frontend** — Django app that serves the UI. Makes HTTP requests to the backend API on behalf of the user, passing auth tokens via session storage.

## Tech Stack

- Python 3 / Django 5.2
- Django REST Framework
- Token-based Authentication (`rest_framework.authtoken`)
- SQLite
- HTML / CSS (Django Templates)

## Features

- User registration and login
- Token authentication — tokens stored server-side in session, passed as `Authorization` headers to the API
- Full CRUD for **Customers** (name, contact info, address)
- Full CRUD for **Orders** (linked to customer, courier, tracking number, status, shipping dates)
- Order list view with resolved customer names


