# MySQL-Essentials-SQL-in-Practice
A beginner friendly, visual, practical SQL reference built from real world queries.

---
title: MySQL Essentials: SQL in Practice
<p></p>
author: Adriana Moreira
---

## Overview

A beginner friendly, visual, and practical SQL reference built using real world MySQL examples.  
This repository focuses on how SQL is actually used in practice, with special attention to common data quality issues and everyday debugging scenarios.

## Purpose

This project exists to serve as a **living SQL reference** for:
- Daily work
- Technical interview preparation
- Revisiting core SQL concepts quickly and effectively

Rather than covering abstract theory, the examples are based on realistic datasets and problems commonly encountered in production environments.

## Target Audience

- SQL beginners to advanced using MySQL
- Aspiring Data Analysts and Data Engineers
- Professionals needing a practical SQL refresher

---

## Dataset and Data Ingestion

### Dataset Source

This project uses the **Hotel Reservations Classification Dataset**, a realistic, publicly available dataset containing booking-level information such as arrival dates, room types, pricing, and booking status.

The dataset represents **one row per reservation**, which makes it well suited for practicing real world SQL queries related to filtering, aggregation, data quality checks, and debugging scenarios.

### Database and Table Structure

All examples in this repository are based on the Schema `hotel`:

- **Schema (database):** `hotel`  
- **Table:** `hotel_reservations`

The table 'hotel_reservations' used for SQL basics and most of the SQL intermediate are intentionally **denormalised** to support learning and practical querying.  
This mirrors how data is often exposed in analytics, reporting, and BI layers, where simplicity and query efficiency are prioritised.

### Data Import Process

The dataset was imported into MySQL using **MySQL Workbench – Table Data Import Wizard**.

Import details:
- Source file: `Hotel Reservations.csv`
- Import method: MySQL Workbench (Table Data Import Wizard)
- Records imported: **36,275**
- Table created automatically during import: `hotel.hotel_reservations`

This approach reflects a common real world workflow for loading CSV data into MySQL for exploration and analysis.

### Notes on Design Choices

- A single wide table (`hotel_reservations`) is used throughout the **SQL BASICS** section to keep the focus on SQL syntax and logic.
- The goal is not to demonstrate perfect normalisation, but to show how SQL is actually used day-to-day when working with existing datasets.
- More advanced sections may introduce derived structures (such as views or additional tables) while preserving this base table for continuity.

---

## Project Structure

```text
.
├── SQL_BASICS/        # Core SQL fundamentals using a real dataset
├── SQL Intermediate/  # In construction
├── SQL Advanced/      # In construction
├── datasets/          # Raw datasets used in the project
├── visuals/           # Screenshots, tables, and diagrams
└── README.md          # Project documentation



