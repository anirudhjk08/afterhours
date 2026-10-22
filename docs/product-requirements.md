# Afterhours — Product Requirements

## 1. Product Overview

**Afterhours** is a mood-based music and video playlist-sharing platform where users create playlists from individual media URLs, share them with the community, and rate other users' playlists.

**Tagline:** A soundtrack for every mood.

**Technology stack**
- Frontend: React
- Backend: Java Spring Boot
- Database: PostgreSQL

## 2. MVP Features

- User registration, login, and authentication.
- Create, edit, and delete playlists.
- Add individual music and video URLs to playlists.
- Upload a playlist cover image.
- Reorder and remove playlist items.
- Assign one predefined mood to each playlist.
- Choose public or private visibility.
- Save drafts and publish playlists.
- Discover public playlists through Latest and Top Rated feeds.
- Filter feeds by mood.
- Rate other users' playlists from 1 to 10.
- View playlist details, creator, media items, average rating, and rating count.
- View and manage your own playlists.
- Share public playlists through a unique URL.
- Include loading, empty, validation, and error states.

## 3. Playlist Rules

- A playlist has a required title and mood.
- Its description and cover image are optional.
- A draft may be incomplete.
- Publishing requires a title, a mood, and at least one valid media URL.
- A playlist can contain multiple music and video URLs.
- Users can add, remove, and reorder items.
- Duplicate URLs within a playlist are allowed in the MVP.
- Media files themselves are not hosted by Afterhours; the application stores URLs and playlist metadata.
- Initially, supported URLs will be restricted to the providers we define for the MVP.
- Published playlists retain their original publication timestamp when edited.

## 4. Moods

Initial predefined moods:
- Chill
- Happy
- Romantic
- Energetic
- Focus
- Melancholic

Each playlist has one primary mood in the MVP.

## 5. Feed Behavior

### Latest
- Shows all public, published playlists, including unrated playlists.
- Sorts by original publication time, newest first.
- Editing a playlist does not change its publication position.
- Ratings do not affect this feed.

### Top Rated
- Includes public playlists with at least five ratings.
- Sorts by average rating, highest first.
- Breaks ties by rating count, highest first.
- Breaks remaining ties by publication time, newest first.
- A playlist that falls below five ratings is no longer eligible.

### Shared Feed Rules
- Both feeds support mood filtering.
- Results use pagination.
- Drafts and private playlists never appear in public feeds.

## 6. Rating Rules

- Ratings are whole numbers from 1 to 10.
- Each user has one current rating per playlist.
- Users may update their own rating.
- Users cannot rate their own playlists.
- Average rating and rating count are displayed.
- Unrated playlists display "Not rated yet", not 0/10.
- The backend and database enforce rating uniqueness and ownership rules.

## 7. Visibility and Authorization

- Public playlists can be viewed without logging in.
- Authentication is required to create, publish, or rate playlists.
- Only the owner can edit or delete a playlist.
- Private playlist details, items, and ratings are not exposed to unauthorized users.
- Drafts are never publicly accessible.
- Changing visibility takes effect immediately.
- Authorization must be enforced by the backend, not only by the frontend.

## 8. Main Screens

1. Discover feed with Latest and Top Rated tabs.
2. Playlist details.
3. Create and edit playlist.
4. My Playlists.
5. Login and registration.
6. Loading, empty, validation, and error states.

## 9. Deferred Features

Not included in the initial MVP:
- Following users.
- Comments and collaboration.
- Personalized recommendations.
- Notifications.
- Complex recommendation or ranking algorithms.
- Automatic provider search and metadata fetching.

Official embeds or provider APIs may be considered later, subject to provider policies and technical feasibility.

## 10. Important Engineering Requirements

- Validate media URLs on the backend.
- Enforce ownership and visibility rules server-side.
- Handle missing, broken, deleted, or inaccessible media links gracefully.
- Do not invent media metadata when it cannot be resolved.
- Use database constraints to prevent duplicate ratings by the same user on the same playlist.
- Paginate feed results rather than loading every playlist.
- Never commit passwords, API keys, tokens, or other secrets to Git.
