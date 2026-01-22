# Playground Feature Setup Instructions

## Overview
This document explains how to set up the new Playground feature with grade-wise categories and games.

## What Was Added

### 1. **Database Tables**
Three new tables were created for the playground feature:
- `playground_categories` - Stores game categories (Grade 6-13, Kids Programming, Math Puzzles, etc.)
- `playground_games` - Stores individual games with details like title, description, image, and file path
- `playground_game_categories` - Junction table for many-to-many relationship between games and categories

### 2. **Admin Pages**
Two new admin management pages:
- `admin_playground_categories.php` - Manage categories (add, edit, delete)
- `admin_playground_games.php` - Manage games (add, edit, delete with category assignment)

### 3. **User-Facing Page**
- `playground.php` - Main playground page with category sidebar and game grid display

### 4. **Navigation Updates**
- Updated `navbar.php` - Added "Playground" link in main navigation
- Updated `admin_sidebar.php` - Added two new options under admin menu

## Setup Steps

### Step 1: Create Database Tables
Run the setup script to create all necessary tables:

```bash
php helpers/setup_playground_tables.php
```

This will:
- Create the three playground tables
- Insert default categories (Grades 6-13, Kids Programming, Math Puzzles, Coding Games, Word Games, Science Games, Logic Games)
- Create the `assest/images/playground` directory

### Step 2: Access Admin Playground Management
1. Log in to admin account
2. Go to Admin Dashboard
3. In sidebar, you'll see two new options:
   - **Playground Categories** - Manage category names, descriptions, icons, and display order
   - **Playground Games** - Add and manage games

### Step 3: Create Categories (Optional)
Go to `admin_playground_categories.php` to:
- Add new categories with custom names and icons
- Edit existing categories
- Set display order
- Mark as active/inactive
- Designate as grade-based or general categories

### Step 4: Add Games
Go to `admin_playground_games.php` to:
- Upload game files (HTML, PHP, or ZIP)
- Or link to external game URLs
- Upload or link game thumbnail images
- Set difficulty level (Easy, Medium, Hard)
- Set recommended age
- Assign to one or multiple categories
- Enable/disable individual games

### Step 5: View Playground
Users can access the playground at:
```
http://yoursite.com/playground.php
```

Features:
- Sidebar with grade-wise categories (Grade 6 to 13)
- Other category options (Kids Programming, Math Puzzles, etc.)
- Click any category to see games in that category
- Click "Play Now" to access the game
- Games display with difficulty level, recommended age, and description

## File Structure

```
d:\xampp\htdocs\mysite\
├── playground.php                           (User-facing page)
├── admin_playground_categories.php          (Admin: Manage categories)
├── admin_playground_games.php               (Admin: Manage games)
├── helpers/
│   └── setup_playground_tables.php          (Database setup script)
├── assest/
│   └── images/
│       └── playground/                      (Game thumbnail images)
│   └── games/                               (Game files storage)
├── navbar.php                               (Updated - added Playground link)
└── admin_sidebar.php                        (Updated - added Playground options)
```

## Features

### Admin Features:
- ✅ Add/Edit/Delete categories
- ✅ Choose category icons
- ✅ Set grade levels for grade-based categories
- ✅ Control display order
- ✅ Add/Edit/Delete games
- ✅ Upload game files (HTML/PHP/ZIP)
- ✅ Link to external games
- ✅ Upload or link game images
- ✅ Assign games to multiple categories
- ✅ Set difficulty levels
- ✅ Set recommended age
- ✅ Enable/disable games
- ✅ View all games in card layout

### User Features:
- ✅ Browse games by category
- ✅ Grade-wise filtering (Grade 6 to 13)
- ✅ Other category filtering
- ✅ View game details (difficulty, age, description)
- ✅ Play games directly or in new tab (for external links)
- ✅ Beautiful card-based interface
- ✅ Responsive design
- ✅ Easy navigation

## Styling

The playground page uses:
- Modern gradient background (purple theme)
- Responsive grid layout
- Category sidebar with active states
- Game cards with hover effects
- Difficulty badges with color coding
- Mobile-friendly design

## Categories Included by Default

1. **Grade 6-13** - Grade-specific categories (auto-populated)
2. **Kids Programming** - Programming games for children
3. **Math Puzzles** - Math quizzes and puzzles
4. **Coding Games** - Learn coding interactively
5. **Word Games** - Vocabulary and language games
6. **Science Games** - Science simulations
7. **Logic Games** - Logic and reasoning challenges

## Game File Support

- **HTML Files** - Static HTML games (stored locally)
- **PHP Files** - Dynamic PHP games (stored locally)
- **ZIP Files** - Compressed game packages
- **External Links** - Games hosted on external URLs

## Image Support

For game thumbnails:
- **Upload** - JPG, PNG, GIF, WebP (stored in `assest/images/playground/`)
- **Link** - External image URLs

## Important Notes

1. **Game Files**: Uploaded game files are stored in `assest/games/` directory
2. **Game Images**: Uploaded images are stored in `assest/images/playground/` directory
3. **External Links**: For external games, provide full URL with `http://` or `https://`
4. **Categories**: You can create unlimited custom categories beyond the defaults
5. **Security**: All user inputs are sanitized and prepared statements are used
6. **Responsive**: The playground is fully responsive on mobile, tablet, and desktop

## Troubleshooting

### If tables aren't created:
1. Make sure you ran `helpers/setup_playground_tables.php`
2. Check database connection in `db_connect.php`
3. Verify MySQL user has CREATE TABLE privileges

### If images don't upload:
1. Ensure `assest/images/playground/` directory exists and is writable
2. Check allowed file sizes in PHP configuration
3. Verify file permissions on the directory

### If games don't appear:
1. Make sure games are marked as "active" status
2. Verify games are assigned to at least one category
3. Check that the category is also marked as "active"
4. Verify game files exist at the specified path

## Database Schema Reference

### playground_categories
```sql
- id: Primary Key
- name: Category name (UNIQUE)
- description: Category description
- icon: FontAwesome icon class
- is_grade_based: Boolean (1 for grade-based, 0 for general)
- grade_level: Grade number (if grade-based)
- display_order: Sort order
- status: active/inactive
- created_at, updated_at: Timestamps
```

### playground_games
```sql
- id: Primary Key
- title: Game name
- description: Game description
- image_path: Path to uploaded image
- image_link: URL to external image
- game_file_path: Path/URL to game file
- game_type: html/php/link
- difficulty_level: easy/medium/hard
- recommended_age: Suggested minimum age
- play_count: Number of plays
- rating: Game rating
- status: active/inactive
- created_by: Admin user ID (FK)
- created_at, updated_at: Timestamps
```

### playground_game_categories
```sql
- id: Primary Key
- game_id: Game ID (FK)
- category_id: Category ID (FK)
- UNIQUE: (game_id, category_id)
```

---

**Setup Complete!** Your playground feature is ready to use. Start by visiting the admin pages to add categories and games.
