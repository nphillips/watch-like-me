## WatchLikeMe Technical Requirements

This document outlines the requirements for the WatchLikeMe application, structured clearly for readability and ease of implementation.

## Pages

### Home Page (`/`)

- **Title:** "WatchLikeMe Home"
- **Visibility:** Both logged-in and logged-out users

#### Logged-Out Experience

- Displays `[search-channels]` by default, set to YouTube search only.
- Users enter search keywords or paste YouTube channel/video URLs.
- A floating suggestions menu appears with related YouTube channels/videos.
- Users select from suggestions; clicking outside dismisses the menu.
- Selecting a suggestion replaces `[search-channels]` with `[channels-list]` and displays `[search-channels__start-new-search]` for new searches.
- `[channels-list]` is in _selection mode_, allowing channel/video selection.
- `[channels-list__row]` items can expand/collapse:
  - Collapsed: Shows `[channels-list__row__header__checkbox]` and expand toggle.
  - Expanded: Displays a horizontally scrolling video panel.
- Layout variations:
  - Main area: Rows scroll horizontally.
  - `[side-modal]`: Grid layout.
- Adding a new channel via `[search-channels]` appends it to `[channels-list]`.
  - Channel selection: Adds as collapsed row.
  - Video selection: Adds as expanded, with video selected.

#### Logged-In Experience

- If not linked to YouTube:
  - Shows disabled `[dashboard__start-new-share-button]`, a "Log in to YouTube" button, and `[search-channels]`.
  - `[search-channels]` defaults to YouTube search.
- Linked accounts:
  - Displays abridged `[dashboard__collections-list]` (full list accessible via "More" button).
  - `[search-channels]` defaults to user's subscribed channels, displaying a `[channels-list]` in _read only mode_.
  - Typing in `[search-channels]` filters subscribed channels live without the floating suggestions menu.
  - Toggling to YouTube search enables floating suggestions menu, behaving as logged-out.
- Selecting a suggestion replaces `[channels-list]`:
  - Channel selection: Adds as collapsed row.
  - Video selection: Adds as expanded, with video selected.
- `[channels-list]` modes:
  - _Read-only mode_: Channels/videos viewable, non-selectable.
  - _Selection mode_ (triggered by `[dashboard__start-new-share-button]`): Allows selections, with channel selections overriding videos.
  - Selecting a video within a selected channel deselects the channel.
  - Expanding/collapsing is interactive even post-selection.
- Clicking on `[channels-list__row__video]` opens it in `[side-modal]`:
  - Playable video, rating option, and annotations visible.
  - Annotations appear in _read only mode_, with edit functionality for author-created annotations.
  - If multiple annotations exist, the most recent is shown, with a "show previous annotations" link.
  - Annotations are truncated with a "Show more" option.
- `[side-modal]` navigation:
  - Breadcrumb toolbar allows viewing all videos from the parent channel.
  - Channel annotations are similarly displayed and editable.
  - Clicking `[channels-list__row__header__title]` also opens `[side-modal]` for expanded video listings.
  - Exiting via clicking outside or using `[side-modal__close-button]` returns to the homepage.

### Account Page (`/account`)

- **Title:** "Account"

### Collections List Page (`/collections`)

- **Title:** "Collections"

### Collection Detail Page (`/collections/:id`)

- **Title:** "[Collection Name]"

### Public Collection Page (`/[username slug]`)

- **Title:** "Watch Like [Username]"

## Dashboard Components

- `[dashboard__start-new-share-button]`
- `[dashboard__collections-list]`
  - Abridged version includes headers (title, filter, sort) and pagination footer.

## Search Channels Component

- Defaults to searching subscribed channels for logged-in users.
- Allows toggling between subscribed channels and YouTube search.
- Includes `[search-channels__start-new-search]` for additional searches.

## Channels List Component

- Operates in two modes:
  - _Read only mode_: Viewing only.
  - _Selection mode_: Enables channel/video selections.
- Rows can be collapsed or expanded to display videos.
- Interactive elements: Titles, expand/collapse toggles, checkboxes, filtering, sorting, pagination.

## Side Modal Component

- Displays video players, annotations (editable or read-only), and share forms.
- Includes breadcrumb navigation, header, close button, and toolbar functionalities.
