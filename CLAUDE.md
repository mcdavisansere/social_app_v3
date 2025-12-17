# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Social App is a single-page web application that allows people to express themselves and connect with others through activities and events. The entire application is built as a single HTML file with embedded CSS and JavaScript.

## Architecture

### Single-File Architecture
The entire application is contained in `index.html`:
- **HTML Structure**: Main layout with modals, navigation, and content sections
- **Embedded CSS**: Complete styling with CSS custom properties for theming (dark/light mode support)
- **Embedded JavaScript**: All application logic, event handling, and state management

### Key Application Features
1. **Event Discovery** - Browse and filter events by category (Social, Fitness, Creative, Professional)
2. **Event Management** - Create, save, and book events
3. **Messaging System** - Direct messages and group chats for event attendees
4. **User Profile** - View profile stats, upcoming events, and hosted events
5. **Advanced Filtering** - Filter events by date, time, location, host, and cost

### State Management
The application uses global JavaScript variables to manage state:
- `sampleEvents` - Array of all events with properties: id, title, category, date, time, location, host, cost, attendees, etc.
- `savedEventIds` - Array tracking which events the user has saved
- `groupChats` - Object storing group chat data by event ID
- `chatMessages` - Object storing chat messages by chat ID
- `currentPage` - Current active page ('explore', 'saved', 'messages', 'profile')
- `currentFilter` - Current category filter
- `selectedCategoriesArray` - Advanced filter selections
- `topLevelSelectedCategories` - Top-level category filter selections

### Navigation Structure
Bottom navigation with 5 tabs:
1. **Explore** - Main event feed with filtering
2. **Saved** - User's saved events
3. **Messages** - Direct and group chats
4. **Create** - Event creation modal (opens modal, not a page)
5. **Profile** - User profile and settings

### Modal System
The app uses multiple modals for different interactions:
- `eventModal` - Event details and booking
- `attendeesModal` - List of event attendees
- `createEventModal` - Event creation form
- `advancedFiltersModal` - Advanced filtering options
- `chatModal` - Messaging interface

## Development

### Running Locally
Since this is a static HTML file, simply open `index.html` in a web browser. No build process or dependencies required.

### Deployment
The project is configured for Vercel deployment via `vercel.json`, which rewrites all routes to serve the single `index.html` file.

## Styling System

### CSS Custom Properties (Theme Variables)
The app supports both dark and light modes using CSS custom properties:
- `--bg-primary`, `--bg-secondary`, `--bg-tertiary` - Background colors
- `--text-primary`, `--text-secondary` - Text colors
- `--border-color` - Border styling
- `--card-bg`, `--modal-bg` - Component backgrounds

Theme switching is handled by toggling the `light-mode` class on `document.body`.

### Design Tokens
- Primary brand color: `#b8860b` (goldenrod)
- Gradient: `linear-gradient(135deg, #8b6f47 0%, #6b5d4f 100%)`
- Max width: `414px` (mobile-first design)
- Font: System fonts (`-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto`)

## Key Functions Reference

### Event Management
- `renderEvents()` - Renders filtered event list
- `showEventDetails(eventId)` - Opens event detail modal
- `createEvent()` - Creates new event from form data
- `bookEvent(eventId)` - Books event and creates group chat
- `toggleSave(event, eventId)` - Saves/unsaves an event

### Navigation & Display
- `switchPage(page, navItem)` - Changes active page
- `showPage(page)` - Shows/hides page sections
- `filterEvents(category)` - Filters by single category
- `toggleCategoryFilter(category)` - Toggles category in multi-select

### Messaging
- `openMessage(messageId, name, isGroupChat)` - Opens chat modal
- `sendMessage()` - Sends message in active chat
- `renderChatMessages()` - Renders messages in chat view
- `createEventGroupChat(event)` - Creates group chat when user books event

### Modal Operations
- `openModal(modalId)` - Opens specified modal
- `closeModal(modalId)` - Closes specified modal

### Filters
- `applyAdvancedFilters()` - Applies complex filter combinations
- `resetFilters()` - Clears all filters
- `addCategoryFilter()` - Adds category to advanced filter

## Making Changes

### Adding New Event Categories
1. Update category filter buttons in the filters section
2. Add category icon mapping in `getCategoryIcon()`
3. Add category emoji in `getCategoryEmoji()`

### Modifying Event Data Structure
Event objects contain: `id`, `title`, `category`, `date`, `time`, `location`, `host`, `cost`, `maxAttendees`, `currentAttendees`, `description`, `attendees`, `rating`, `saved`

### Styling Changes
Modify the `<style>` tag within `<head>`. The app uses a mobile-first approach with max-width constraint of 414px on the main container.
