# v1-barak-27.03
First time using Gemini 2.5
French Property Finder: Feature Specification V6 - March 2025
We are developing the AI French property finder PWA app in Version 0. You will continue to assist me in achieving this goal. I will upload images and provide text feedback on the progress in Version 0. Based on my changes, you will then give me a bullet point list of your planned actions.
The entire experience should feel like a seamless conversation with an AI real estate agent who presents properties and guides the user through the search process.
RULES
User input images using pink or Red lines are just annotations for guidance, not design elements
Core Idea and Goals of the App
Our app allows users to browse available properties within seconds, offering a significant time advantage compared to competitors. It aggregates criteria-specific listings from the entire French property market using real-time data collection from all major and minor players in the French real estate industry. An AI chat feature simplifies the process, ensuring search results remain accessible in the chat for future reference.
You can sign up for free in just 20 seconds using your phone and gain access to premium features at no cost. These features include saved searches, market intelligence, and sharing options, enhancing your property search experience.
KEY PRINCIPLES
* Mobile-first PWA design optimized for conversational interface.
* Use mock data for development
* Testing and mock data need to be removed later for production version (earmark appropriately)
* Embedded viral mechanisms at natural user journey touchpoints.
* Dual-sided marketplace balancing user and agent value.
* Data protection with reference-only property storage.
* Progressive feature disclosure based on engagement level.
________________


Notes: This specification reflects our strategic pivot to PWA-first development with phone verification and embedded growth mechanisms, while maintaining the core value proposition of conversational property search. The new card stack and interaction features enhance user engagement and align with the Tinder-like swipe paradigm.
IMPLEMENTATION UPDATES (March 2025)
* PWA Implementation: Configured as "V1 Barak AI : L'Explorateur Ultime de Propriétés" with appropriate manifest and service worker
* Navigation System: Enhanced with direct routing for reliable cross-screen movement
* Card Stack Persistence: Search results remain in chat history even when criteria change
* Postal Code Recognition: Properly translates codes (e.g., "92250" → "La Garenne-Colombes")
* Budget-Action Inference: Values >100K€ automatically trigger "Buy" tag creation
* State Management: Clear architecture separating criteria state from UI components
1. Core Experience
1.1 Chat Interface & AI Search
* Conversational UI: Natural language property search with contextual understanding
* Multi-language Support: System language detection but French and English detection inside the bot chat
* Guided Refinement: Progressive query improvement through conversation
* Search History: Persistent chat history with property results
* Widgets Dashboard: Scrollable content below chat interface (See Section 4)
* Numeric Input Detection: Direct recognition of standalone numeric responses (e.g., "1" for rooms)
* Context Maintenance: State-based system retains previously identified criteria
* Error Recovery System: Interaction layer reset capability for critical failure scenarios
Suggestion Bubbles (inline chat):
When a user starts a new chat session and the bot sends its first message, display chat starter suggestions in the tags area (since there are no tags initially). These suggestions cannot be closed with an "x" and include property search ideas such as:
* "Achete maison avec jardin à Paris"
* "Loue appartement 3 pièces près des écoles [autour de moi]"
* "Good buy properties autour de moi"
* "Loue appartement avec balcon, budget 500k€"
When tapped, these immediately trigger a search based on these criteria. The tags are added including "Buy" or "Rent" always at the start, and we get results, followed by inline bot message after the card stack saying "Swipe left to skip or swipe right if you're interested, or keep chatting to change search!"
Feature Specification: Chat Screen Slide-in Side Menu
Overview
The Chat Screen Slide-in Side Menu provides a contextual navigation panel that slides from the left edge when activated. It closely follows ChatGPT's drawer menu pattern while being tailored to property search features.
Visual Design & Animation
Dimensions & Layout
* Width: 75% of screen width on mobile devices
* Height: Full viewport height, respecting safe areas
* Position: Fixed to left edge, covering chat interface when opened
* Z-index: Should appear above chat content but below modals (z-index: 30)
* Background: White with subtle shadow (shadow-lg)
* Border-radius: 0px on left edge, 16px on right edge (rounded-r-2xl)
Animation Specifications
* Entry Animation:
   * Transform: translateX(-100%) to translateX(0%)
   * Duration: 350ms
   * Easing: Spring physics (damping: 26, stiffness: 300)
   * Subtle bounce at end of animation (overshoot: 4%)
* Exit Animation:
   * Transform: translateX(0%) to translateX(-100%)
   * Duration: 250ms
   * Easing: Ease-in-out cubic-bezier(0.4, 0, 0.2, 1)
* Backdrop:
   * Background: rgba(0,0,0,0.4)
   * Opacity animation: 0 to 1 (synchronized with drawer)
   * Tap to dismiss functionality
Gesture Support
* Drag-to-open: Detect edge swipe from left screen edge
* Drag-to-close: Allow dragging menu to dismiss
* Velocity detection: Fast swipe should complete animation regardless of distance
* Threshold based: >40% dragged should complete the animation
Content Sections
1. Header Section (Logged Out State)
* Title: "Barak AI Property Finder"
* Subtitle: "Sign up to save your searches + more"
* CTA Button: "Sign up with phone • 20 seconds"
   * Button Style: Blue gradient background (#3B82F6 to #1D4ED8)
   * Full width, rounded-lg, padding-y: 12px
* Visual: Small illustration of phone or house icon
2. Header Section (Logged In State)
* User Information: Profile image (or placeholder), Name, Phone number
* Account Status: "Logged in with +33..." text
* Quick Action: "View saved properties" link or button
   * Action: Navigates to Mes Biens tab
3. Recent Searches Section
* Title: "Recent Searches"
* Content: List of recent search queries (maximum 10)
   * Each item displays: Search criteria (max 2 lines)
   * Property count: "X properties found"
   * Timestamp: "X hours/days ago"
* Item Actions:
   * Tap: Execute search again
   * Long press: Show delete option
* Persistence:
   * Guest users: 1 day
   * Logged in users: 30 days
4. Navigation Section
* Primary Navigation:
   * Chat/Search (current)
   * Explorer
   * Mes Biens
   * Notifications
   * Settings
* Visual Indicator: Blue dot for active section
* Icons: Use Lucide React icons for consistent style
5. Secondary Links Section
* Support: "Help & Support" link
* About: "About French Property Finder" link
* Language: Language selector (French/English)
* App Version: Subtle version number at bottom
User Interactions
Menu Activation Methods
* Hamburger Icon: Tap the hamburger icon in header
* Edge Swipe: Swipe from left edge of screen (20px detection zone)
* Keyboard Shortcut: (Desktop only) Cmd/Ctrl + K
Menu Dismissal Methods
* Backdrop Tap: Tap outside the menu area
* Close Icon: Tap X icon in top-right of menu
* Swipe Left: Drag menu back to left
* Escape Key: (Desktop only) Press Esc
Item Interactions
* Hover States: Subtle background change on hover (desktop)
* Active States: Pressed state animation (mobile)
* Transitions: Smooth hover/active transitions (150ms)
Technical Requirements
Component Structure
* Root Container: Fixed position, full height
* Backdrop: Separate component for tap handling
* Menu Panel: Main container with animation logic
* Content Sections: Modular components for each section
Accessibility
* ARIA Roles:
   * role="dialog"
   * aria-modal="true"
   * aria-labelledby="menu-title"
* Focus Management:
   * Trap focus within menu when open
   * Return focus to hamburger icon when closed
* Screen Reader Support:
   * Announce when menu opens/closes
   * Properly labeled interactive elements
Performance Considerations
* Hardware Acceleration: Use transform for animations
* Passive Event Listeners: For scroll/touch events
* Animation Optimizations: GPU-accelerated properties only
* Lazy Load Content: Defer loading some content until menu opens
Data Persistence
* Recent Searches Storage:
   * Guest users: localStorage with timestamp expiry
   * Logged in users: Backend storage with 30-day TTL
* User Preferences: Persist in user account settings
* Session State: Remember open/closed state during session
Implementation Notes
* The menu must not interfere with the main chat interface when closed
* All animations should run at 60fps even on mid-tier devices
* The menu should adapt to all screen sizes, with special handling for landscape mode
* iPhone notch and bottom home indicator areas must be respected
This feature enhances navigation and user engagement while providing quick access to recent searches and account features, following the familiar pattern established by ChatGPT and other modern AI interfaces.
1.2 Tag System
Extract search criteria from natural conversation. Use french zipcodes to unearth location name ie. '92' user input = "La Garennes-Colombes" etc. 'Paris 12' = "Paris, 12th". Use fuzzy matching for mispelled criteria such as '2PIecs' = "2 Pieces"
1. Auto-Tag Recognition
* Natural Language Processing: Automatically detect property search criteria from user messages
* Multi-Language Support: Recognize criteria in both French and English text
* Contextual Understanding: Differentiate between vague and specific requirements
* Confidence Scoring: Assign confidence levels to detected criteria
* Progressive Refinement: Improve detection accuracy through conversation
* Tag Hierarchy:
   * Primary(required) Tags: Action (Buying or Renting), Location: 2km Radius, City, neighborhood, arrondissement, postal code (ie. 'Paris, 12th'), Budget: Maximum price, price range, "under X" values, Rooms: Number of bedrooms (4 Pieces etc), property type (House, Apartment, Loft etc)
   * Secondary Tags:
      * Features: Balcony, elevator, parking, garden, etc.
      * Property Condition: New, renovated, to renovate, etc.
      * Environmental: Energy rating, proximity to parks, etc.
* Criteria Inference:
   * Budget values >100K€ automatically trigger "Buy" tag creation
   * Budget values <10K€ suggest "Rent" tag with lower confidence
   * Allow numeric-only responses for room/piece count
   * Support abbreviated property types (e.g., "apt", "apart")
Feature Specification: French Postal Code Recognition System
Overview
The French Postal Code Recognition System automatically detects and converts postal codes and department numbers from natural language input into human-readable location names within the chat interface.
Functional Requirements
1. Recognition Patterns
* Department Numbers (2 digits)

   * Example: '92' → "La Garenne-Colombes"
   * Example: '75' → "Paris"
   * Example: '78' → "Yvelines"
   * Arrondissement References

      * Example: 'Paris 12' → "Paris, 12th"
      * Example: 'Paris 16e' → "Paris, 16th"
      * Support for variations: '16eme', '16ème', '16e', '16th'
      * Full Postal Codes (5 digits)

         * Example: '92250' → "La Garenne-Colombes"
         * Example: '75016' → "Paris, 16th Arrondissement"
         * Fuzzy Matching

            * Support for typos and common misspellings
            * Support for omitted spaces or punctuation
2. Data Source and Mapping
            * Maintain a comprehensive mapping of French postal codes to locations
            * For department codes (first 2-3 digits), map to department name or major city
            * Special handling for Paris arrondissements (75001-75020)
            * Support for DOM-TOM (overseas) codes (97xxx, 98xxx)
3. Tag Generation
            * Visual Appearance:
            * Purple background (#DDD6FE)
            * Dark purple text (#5B21B6)
            * Pill-shaped format
            * Placement: First in tag order, before budget, rooms, etc.
            * Multiple Locations: Support for multiple location tags if user mentions multiple areas
4. Integration
            * Integrate with natural language processing in ChatInterface
            * Generate tags immediately upon detection in user messages
            * Allow modification/removal of incorrectly detected locations
5. Edge Cases
            * Handle ambiguous codes (map to most popular/likely location)
            * Handle non-existent postal codes (provide feedback or best guess)
            * Support for location names without needing postal codes
6. Performance Considerations
            * Optimize lookup for real-time response (<100ms detection time)
            * Implement caching for frequently accessed codes
            * Progressive loading of postal code database if needed
Implementation Priority: High
This feature is critical for the natural language search experience and should be implemented early in development.
Testing Strategy
            * Unit tests for each recognition pattern
            * Database validation for postal code accuracy
            * Localization testing for proper French character handling
            * User testing with varied input styles and regional dialects
This comprehensive specification should provide enough detail for implementation in the French Property Finder application.
Feature Specification: Required Search Criteria Collection
Overview
The AI assistant must collect a complete set of required criteria before displaying property search results. This process should feel natural but ensure all necessary information is gathered for effective property matching.
Required Search Criteria
Primary (Required) Tags
            1. Action Type

               * Either "Buying" or "Renting"
               * Always first in tag order
               * Inferred from budget when possible (>100K€ → Buy)
               2. Location

                  * One of: 2km radius around user, city, neighborhood, arrondissement, or postal code
                  * Examples: "Paris, 16th", "La Garenne-Colombes", "92250", "autour de moi"
                  * Postal codes properly mapped to location names
                  3. Budget

                     * Maximum price, price range, or "under X" values
                     * Examples: "800K€ max", "entre 500K€ et 700K€"
                     4. Rooms

                        * Number of bedrooms/pieces
                        * Examples: "2 pieces", "3 chambres"
                        * Support for single-digit responses (e.g., "1")
                        5. Property Type

                           * Type of property being sought
                           * Examples: "Apartment", "House", "Loft"
                           * Support abbreviated inputs ("apt", "apart")
                           * Numeric selection option (1-5)
Dialog Flow for Criteria Collection
Initial Input Handling
                           * When a user provides partial criteria in their initial message, the AI should:
                           1. Acknowledge the provided criteria
                           2. Generate tags for the recognized criteria
                           3. Explicitly ask for any missing required criteria
Missing Criteria Prompting
                           * For Action Type: "Are you looking to buy or rent?"
                           * For Location: "In which area are you looking? You can specify a city, neighborhood, or postal code."
                           * For Budget: "What's your budget range? Or perhaps a maximum price you're considering?"
                           * For Rooms: "How many rooms (pièces) are you looking for?"
                           * For Property Type: "What type of property are you interested in? An apartment, house, or something else?"
Natural Conversation Flow
                           * Questions for missing criteria should be conversational, not form-like
                           * Combine questions when appropriate: "Could you tell me your budget and how many rooms you're looking for?"
                           * Acknowledge partial information: "I see you're looking in Paris. Would that be for buying or renting?"
Criteria Validation
                           * Action Type: Must be clearly "buy" or "rent" (including variations like "acheter", "louer")
                           * Location: Must be specific enough to search (city minimum, neighborhood preferred)
                           * Budget: Must include a numeric value and be reasonable for the market
                           * Rooms: Must be a numeric value between 1-10
                           * Property Type: Must match known property categories
Implementation Requirements
Tag Generation Order
Tags must be displayed in this specific order:
                           1. Action Type (Buying/Renting)
                           2. Location
                           3. Budget
                           4. Rooms
                           5. Property Type
                           6. Any secondary tags (features, etc.)
Handling Suggestion Bubbles
                           * If a user selects a pre-populated suggestion bubble like "Acheter maison, 4 pieces, autour de moi", the system should:
                           1. Parse all provided criteria
                           2. Immediately ask for any missing required criteria
                           3. Only show one follow-up question for missing criteria (not multiple sequential questions)
Edge Cases
                           * Multiple Locations: If a user mentions multiple locations, seek clarification
                           * Unrealistic Criteria: Provide gentle market education if criteria are unrealistic (e.g., "1M€ budget for a 5-bedroom in central Paris might be challenging")
                           * Ambiguous Input: When input could have multiple interpretations, seek specific clarification
Success Criteria
                           * 100% collection of all required criteria before showing search results
                           * Conversational flow feels natural, not like filling out a form
                           * Average time to complete criteria collection < 45 seconds
                           * User can modify any criteria at any point in the conversation
This feature is essential for delivering relevant search results and should be implemented as a high-priority component of the conversational interface.
Tags
                           * Visual Design:
                           * Small Pill-shaped format with category-specific colors (must be readable)
                           * Color-coding matches exact values below
                           * Compact on one-line then two lines and three lines if necessary
                           * Interactive Management:
                           * Tap to toggle active/inactive state
                           * Long-press for fan-style option selector (1-5 alternatives fan up)
                           * Tap 'x' to remove
                           * Sharing Mechanism:
                           * Extra pill at the end of tags in the same style and area as the tags (mid grey color)
                           * "Critères Partagés" visual preview cards
                           * WhatsApp and social integration
                           * Recipient import capability
                           * Tag Formatting:
                           * Action: "Buy" or "Rent"
                           * Location: "Paris, 12eme" or "2km autour de moi"
                           * Budget: "€800k max."
                           * Rooms: "4 Pieces"
                           * Type" "Apartment"
                           * Features
3. Interactive Management
                           * Tap-to-Toggle: Enable/disable individual criteria without removing them
                           * Remove Option: Completely remove unwanted criteria
                           * Direct Editing: Edit tag values with inline input fields
                           * Visual Feedback: Clear indication of active vs. inactive criteria
                           * Auto-Updating Results: Property results update instantly when criteria change
4. Sharable Tag Sets ("Critères Partagés")
                           * One-Click Sharing: Generate shareable links containing selected criteria
                           * Visual Preview: Create attractive preview cards for social sharing
                           * WhatsApp Integration: Direct sharing to WhatsApp contacts
                           * Collaborative Filtering: Allow multiple users to contribute criteria
                           * Tag Set Import: Accept and merge criteria from shared links
                           * Pill-Shaped Format: Rounded rectangles with appropriate padding
                           * Typography:
                           * Font: Inter or system font
                           * Size: 14px (mobile), 16px (tablet+)
                           * Icons: Use appropriate icons to enhance visual scanning
                           * Location: Map pin
                           * Budget: Euro symbol
                           * Rooms: Bed icon
                           * Features: Relevant feature icons
Tag Placement
                           * Primary Location: Directly above the chat input field
                           * Grouping: Organized by category with subtle dividers
                           * Scrollable Container: Horizontal scroll for many tags
                           * Expanded View Option: Button to expand/collapse full criteria set
Animation
                           * Creation: Subtle scale and fade-in when tags are created
                           * Toggle: Smooth color transition when toggling active state
                           * Removal: Fade-out and collapse animation when removed
1.3 Property Card Stack
                           * Card Design:

                              * Square property cards in fan-stack formation
                              * Property cards are ALWAYS square, and go inline in the chat
                              * First card is always the Instructions card (only use the .svg with no extras) until properties are loaded
                              * For testing we will add a 2 second delay to simulate the loading process
                              * Card Behavior: Instruction card remains in place and is not swipeable during loading
                              * Once properties are loaded, instruction card fades out revealing top property card
                              * Subtle animation (slight bounce) indicates when swiping becomes available
                              * Last card always the promo card to sign up for free unless user is logged in
                              * Top card fully visible, others scaled/rotated 1.5 degrees anti-clockwise offsetting behind
                              * Property image, price, location, key details
                              * Right-aligned action buttons (Info, Call, Share, Web listing)
                              * Certification badge (1-5 rating) top left
                              * Fan Formation: Background cards pre-rendered with proper scaling (0.95, 0.90) and rotation increments (1.5° between cards)
                              * Content Persistence: Card stacks remain in chat history even when criteria change
                              * Swipe Mechanics:

                                 * Left swipe to reject (gray broken heart animation)
                                 * Right swipe to save (red heart animation)
                                 * Natural Arc Motion: Cards follow a curved path when swiped (not just straight left/right or left/right then down)
                                 * Spring resistance during drag
                                 * Smooth acceleration on threshold pass
                                 * Tinder-like Swipe Function
                                 * Progressive Rotation: Rotation angle increases as the card moves further from center
                                 * Velocity-Based Decision: Cards use both distance and velocity to determine if swipe completes
                                 * Elastic Motion: Card has slight "spring" resistance when dragged
                                 * Smooth Exit: When threshold is passed, card smoothly accelerates off-screen
                                 * iOS-Specific Behaviors

                                 * Add proper iOS-style spring animations (slightly more bounce than current)

                                 * Implement native-feeling drag-to-dismiss gesture

                                 * Respect iOS touch feedback patterns

                                 * Special Cards:

                                    * Instruction Card SVG (complete): First card with swipe tutorial and loading indicator
                                    * Promo Card: Last card with FREE premium signup CTA by phone
                                    * Navigation & Context:

                                       * Card stack must remain inline within the chat flow and remain persistent
                                       * Never navigate away from chat interface or hide navbar
                                       * Multiple card stacks can exist in the conversation history
                                       * Each card stack persists in the chat for its corresponding search
                                       * Scrolling resets the stack to the top property card for review.
                                       * Card Stack Behavior:

                                          * Instruction Card:
                                          * Instruction card always appears first for at least 2-seconds on first search
                                          * Position: Small spinner in bottom-right corner of the instruction card
                                          * Behavior: Visible only while properties are being fetched
                                          * Spins continuously until data is loaded
                                          * Disappears when properties are ready with instruction card
                                          * Use provided gif animation
                                          * Features a loading indicator in the bottom-right corner while properties load.
                                          * Instruction card must transition to property cards automatically
                                          * Property cards appear after instruction card
                                          * Square property cards displayed in a fan stack (top card fully visible, others slightly rotated by 1.5 degrees offset and scaled).
                                          * Only the top card is swipeable (left for reject, right for save).
                                          * Fan-stack shows background cards with 1.5° rotation increments
                                          * For initial testing purposes we will have at least 5 cards
                                          * In production version, the card count depends on search result volume.
                                          * Background cards scale down progressively (0.95, 0.90, etc.)
                                          * When chat is scrolled, card stacks remain with first property showing
                                          * Instruction card should use the provided SVG with no additional graphics required
1.4 Action Buttons & Modals
                                          * Button Layout:
                                          * Vertically stacked on right edge of card
                                          * Four buttons that trigger modals that slide up: Info, Call, Share, Web Listing Link (iFrame from property origin web link)
                                          * Each button triggers a slide-up modal.
                                          * Button Functionality:
                                          * Info button: Redirects to property detail page within Mes Biens
                                          * Card tap: Opens property detail modal overlay
                                          * Swipe: Like/dismiss property without navigating away
WebView Modal for External Property Links
                                          1. User clicks the globe icon/web button on a property card
                                          2. A WebViewModal slides up with advanced and smooth animation within the iPhone viewport
                                          3. The external site based on the property search (ie. SeLoger.com etc) loads in the iframe
Device Viewport Considerations
                                          * Modal height must be exactly 90%
                                          * Modal should respect iOS safe areas (notch, home indicator)
                                          * Modal should use viewport units and percentages for proper sizing across devices
WebView UI Elements
                                          * Navigation bar with:
                                          * Back button
                                          * Forward button
                                          * Refresh button
                                          * Title showing the external site name
                                          * Close button
                                          * Loading indicator displays while page is loading
                                          * Iframe content displays the external website within the modal
iOS-Specific Behaviors
                                          * Clean iOS-style spring animations with appropriate bounce
                                          * Native-feeling drag-to-dismiss gesture
                                          * Proper respect for iOS touch feedback patterns
                                          * Proper handling of safe areas
Content Interaction
                                          * External site will receive click events via sandbox attributes
                                          * Users can navigate the external site using the provided controls
                                          * Users can interact with forms and content on the external site
                                          * External site is contained within the application experience
Technical Notes
                                          * Uses iframe with appropriate sandbox attributes:
                                          * allow-same-origin: Maintains the site's original security context
                                          * allow-scripts: Enables JavaScript in the iframe
                                          * allow-forms: Lets users fill out forms on the external site
                                          * allow-popups: Permits the site to open popups if needed
This feature enhances the user experience by allowing seamless viewing of external property listings without leaving the application.
2. User Management
2.1 Phone Verification
                                          * Implementation:
                                          * 20-second signup flow with OTP verification
                                          * WhatsApp alternative pathway
                                          * Progressive data collection during usage
                                          * Benefits:
                                          * Reduced friction vs. email verification
                                          * Single-tap verification on iPhone
                                          * Instant account access
                                          * Testing Implementation:
                                          * Development-only authentication accepts any 4-digit code
                                          * Clear security notice indicating test-only implementation
                                          * Will be replaced with secure verification in production
2.2 User Profiles
                                          * Guest Mode: Limited functionality before verification
                                          * Progressive Profiling: Collect data through usage
                                          * Preference Storage: Cross-session persistence
                                          * Session Management: Token handling for authentication
3. Navigation System
3.1 Bottom Navigation Bar
                                          * Visual Design:
                                          * Fixed positioning at bottom
                                          * iOS safe area support: env(safe-area-inset-bottom)
                                          * Z-index: 50+ for proper stacking
                                          * Height: 64px standard
                                          * Navigation Items:
                                          * Chat (Recherche): Conversation interface (Default)
                                          * Découvrir (Explorer): Catch up on properties matching recent searches. Scrollable Property list with square cards.
                                          * Mes Biens: Saved, seen and unseen properties
                                          * Notifs: Notifications center
                                          * Réglages: Settings page
                                          * Active State Indicators:
                                          * Blue highlight (#3B82F6)
                                          * Bottom bar indicator with spring animation
                                          * Transition parameters: stiffness 300, damping 30
                                          * Persistence:
                                          * Navigation bar must always remain visible
                                          * Property interactions happen within the current tab
                                          * Never hide navigation bar during property interactions
                                          * Route Handling:
                                          * Direct window.location.href routing ensures reliable navigation
                                          * Emergency reset capability for interaction layer failures
3.2 Property Management Tabs
                                          * Tab Structure:
                                          * Liked (default): Actively saved properties
                                          * Seen: Viewed but not saved properties
                                          * Unseen: New properties matching criteria
                                          * Visual Indication: Active tab with blue underline
                                          * Transitions: Smooth sliding animations
4. Widget Dashboard Layout (Underneath Chat)
Like an endless scroll on facebook when user semi-forcfully scrolls too far up. Starts with rectangle of first widget and keeps scrolling.
4.1 Structure & Order
                                          1. Signup Banner:
Full-width rectangular card (1x1)

                                             * "Sign up with phone - takes only 20 seconds"
                                             * CTA button
                                             * Light blue gradient background
                                             2. Neighborhood Information (2×2 Grid):

                                                * Schools: Nearby schools with ratings
                                                * Transit: Public transportation options
                                                * Amenities: Restaurants, shops, parks count
                                                * Safety: Safety score with comparisons
                                                3. Good Buy Properties:

                                                   * Horizontal scrollable cards (2 rows)
                                                   * Value indicators (% below market)
                                                   * Price, size, location, ratings
                                                   4. Super Favorites List View (2×1 Grid):

                                                      * Full-width rectangular card, half sized height
                                                      * Properties from upward swipes
                                                      * Enhanced visualization and details
                                                      5. Recent Searches:

                                                         * Text-based list of previous queries
                                                         * One-tap re-execution
                                                         6. Growth Mechanism Widgets:

                                                            * "Share Your Criteria" card
                                                            * "Invite to Decision Circle"
                                                            * "Expertise Locale" neighborhood knowledge
                                                            * "Moments Immobilier" milestone sharing
                                                            7. Quick Shortcuts Footer Grid:

                                                               * Saved Searches, Unseen Properties, Liked Properties, Compare 2 properties side-by-side
5. Social & Collaborative Features
5.1 "Cercle de Décision"
                                                               * Multi-user Evaluation: Shared property assessment
                                                               * Decision Heatmaps: Visual group preference display
                                                               * Role Assignment: Specialized collaborator functions
                                                               * Bilateral Rewards: Premium features for all participants
5.2 Location Intelligence
                                                               * "Expertise Locale": User-contributed neighborhood insights
                                                               * Verification System: Community validation mechanisms
                                                               * Recognition: "Connaisseur Local" badges for contributors
                                                               * Localized Alerts: Area-specific updates and insights
5.3 Growth Mechanisms
                                                               * Phone Ambassador Program: Tiered referral rewards
                                                               * "Moments Immobiliers": Shareable achievements
                                                               * WhatsApp Integration: Property alerts and sharing
                                                               * Decision Circle Expansion: Multi-collaborator incentives
6. Property Detail Views
6.1 Three-Quarter Modal View (75% viewport height)
                                                               * Content Sections:
                                                               * Image gallery with rating badge

                                                               * Property details (all searched tags)

                                                               * Agent contact information

                                                               * Market intelligence

                                                               * Tabbed navigation (Details, Map, Photos)

                                                               * Description and features list

                                                               * Similar properties: same property details in other nearby neighbourhoods

                                                               * "Cercle de Décision" share widget

                                                               * Re-use Property detail tags in new search, change location

6.2 External Property WebView
                                                                  * Navigation Controls: Back, forward, refresh, close
                                                                  * Content Rendering: iframe with appropriate sandbox attributes
                                                                  * Interaction: Full external site functionality within modal
7. Technical Implementation
7.1 PWA Optimization
                                                                  * Offline Capabilities: Basic browsing without connection
                                                                  * Installation Prompts: Strategic PWA installation suggestions
                                                                  * Cross-Device Sync: Consistent experience across platforms
                                                                  * Progressive Loading: Critical-path optimization
                                                                  * App Identity: "V1 Barak AI : L'Explorateur Ultime de Propriétés"
                                                                  * Manifest Configuration: Complete implementation with proper icons and display settings
7.2 API Integration
                                                                  * Data Binding: Connect UI components to property search API
                                                                  * State Management: Component-level state with loading/error handling
                                                                  * Offline-First Pattern: Local storage with background synchronization
                                                                  * Error Recovery: Automatic retry for transient failures
7.3 Performance Targets
                                                                  * Time to First Meaningful Content: < 1.5 seconds
                                                                  * API Response Processing: < 300ms
                                                                  * Offline Capability: 80% of core functions
                                                                  * Error Recovery Rate: > 95% automatic recovery
7.4 Property Card Stack Implementation
                                                                  * State Management:

                                                                     * Use clear state machine with stages: loading → instruction → properties → promo
                                                                     * Loading: Always show for minimum 2 seconds with spinner
                                                                     * Instruction: Only show on first search, must respond to tap/click
                                                                     * Properties: Show actual properties with swipe interactions
                                                                     * Promo: Show at end of property stack for users without accounts
                                                                     * Asset Usage (Direct links):

                                                                        * Instruction card SVG: "https://p129.p0.n0.cdn.zight.com/items/xQumKjNL/55d1ec0e-3618-4275-8591-2d1e2085acba.svg"
                                                                        * Loading spinner GIF: "https://p129.p0.n0.cdn.zight.com/items/QwuzqkZD/60703eb1-316d-492b-b871-34e057d4b005.gif"
                                                                        * Heart animation: "https://p129.p0.n0.cdn.zight.com/items/nOurdnR1/dda6975b-4cbd-4ee4-b6a0-fdb4e40877ed.svg"
                                                                        * Broken heart animation: "https://p129.p0.n0.cdn.zight.com/items/6qupKPZb/f43dadd4-28a0-497b-978e-95211e258a71.svg"
                                                                        * Transition Requirements:

                                                                           * Instruction card must advance to properties once properties loaded
                                                                           * Loading state must automatically transition to next state
                                                                           * Property cards must support both tap and swipe gestures
                                                                           * Animations must follow specification exactly
                                                                           * Fan-stack formation must be maintained throughout
8. Visual Design References
8.1 Tag Colors
Exact Tag Color Values
Location Tag (Paris 16th - Purple)
                                                                           * Background: #DDD6FE (lighter purple)
                                                                           * Text: #5B21B6 (darker purple)
                                                                           * Tailwind classes: bg-purple-200 text-purple-800
Budget Tag (Max €800K - Amber/Brown)
                                                                           * Background: #FDE68A (light amber)
                                                                           * Text: #92400E (dark amber/brown)
                                                                           * Tailwind classes: bg-amber-200 text-amber-800
Rooms Tag (2 Bedrooms - Pink)
                                                                           * Background: #FBCFE8 (light pink)
                                                                           * Text: #9D174D (dark pink)
                                                                           * Tailwind classes: bg-pink-200 text-pink-800
Feature Tag (Balcony - Green)
                                                                           * Background: #A7F3D0 (light green)
                                                                           * Text: #065F46 (dark green)
                                                                           * Tailwind classes: bg-green-200 text-green-800
Property Type Tag (Apartment - Purple/Pink)
                                                                           * Background: #F5D0FE (light fuchsia)
                                                                           * Text: #86198F (dark fuchsia)
                                                                           * Tailwind classes: bg-fuchsia-200 text-fuchsia-800
Action Tag (Buying - Green)
                                                                           * Background: #BBF7D0 (light green)
                                                                           * Text: #166534 (dark green)
                                                                           * Tailwind classes: bg-green-200 text-green-800
Tag Sizing and Layout
                                                                           * Padding: px-3 py-1
                                                                           * Font size: text-xs
                                                                           * Border radius: rounded-full
                                                                           * Margin: mr-2 mb-1.5 (to keep them compact on one line)
                                                                           * Line height: Default or slightly tighter than default
To implement these exact colors in your TagPill component, replace the color classes with these values.
10. Critical Implementation Notes
Based on development experience, the following points require special attention:
                                                                           * Property Card Stack Transitions: The card stack component must maintain a proper state machine that ensures smooth transitions between stages (loading → instruction → properties → promo).

                                                                           * Inline Chat Context: All Tinder-style property stack interactions must remain inline within the chat interface.

                                                                           * Multiple Search Persistence: The application must support multiple property searches within the same chat session, with each search and its results persisting in the conversation history.

                                                                           * Direct Asset Usage: Use provided SVGs and GIFs directly rather than recreating them to ensure consistent appearance.

                                                                           * State Reset Handling: When a new search begins, properly reset the state while maintaining previous search results in the chat history.

                                                                           * Instruction Card Behavior: The instruction card must be shown only once per user session and must always transition to property cards when interacted with. The loading GIFF is used instead of instruction card thereafter in the session on a white skeleton card while search results load

                                                                           * Fan Stack Formation: Background cards must maintain proper scaling (0.95, 0.90) and rotation increments (1.5° between cards) to create the fan effect.

                                                                           * Tag Formatting: Use consistent format for tags and styling across the application.

Menu Item Screens
Top of all non-chat screens have the promo rectangle:
"Get more advanced features free"
Get Saved searches, Market intelligence and more
Sign up with phone - 20 seconds"
Mes Biens (My Properties) Screen from menu item
                                                                              1. Three-Tab Navigation:
                                                                              * Tabs: "Liked" (default), "Seen", "Unseen"
                                                                              * Tab bar positioned at top of screen with active indicator
                                                                              * Switching tabs animates content transition
                                                                              2. Property List View:
                                                                              * Vertical scrolling list of saved properties
                                                                              * Each list item shows thumbnail, key property details, and rating
                                                                              * Optimized for quick scanning of saved properties
Property Management Feature Specification
Overview
The French Property Finder application has two complementary ways for users to interact with properties: through the conversational interface with property stack, and through the organized "Mes Biens" (My Properties) section that categorizes properties based on user interaction.
Primary Features
1. Chat & Property Stack Flow
                                                                              * Conversational Interface: Users search for properties via chat
                                                                              * Persistent Results: Property stacks remain in chat history for future reference
                                                                              * Quick Access: Tapping a property card or info button slides up the detailed property view modal
                                                                              * Direct Interaction: Swiping right likes a property, swiping left dismisses it to "seen"
2. Mes Biens (My Properties) Organization
                                                                              * Tab Navigation: Three tabs at the top of screen:
                                                                              * Liked: Properties the user has actively liked (default tab)
                                                                              * Seen: Properties the user has viewed but not liked
                                                                              * Unseen: New properties matching criteria not yet viewed
                                                                              * Property List View: Compact rectangular cards showing:
                                                                              * Property image thumbnail
                                                                              * Price and key specifications (size, bedrooms)
                                                                              * Address and brief description
                                                                              * Visual status indicator (heart, eye, etc.)
Navigation Connections
                                                                              * Property Card Icon→ Property Detail View (not modal): Tapping the property card icon opens its detail view inside the menu item screen "Mes Biens"
                                                                              * Property Card → Property Detail Modal View: Tapping the property card opens the ¾ modal overlay inside the chat
                                                                              * Navbar → Mes Biens: Direct access from main navigation bar
Additional Notes
                                                                              * All property views remain synchronized (liking a property in one view updates all instances)
                                                                              * Property categorization persists between sessions
                                                                              * Search results in chat remain accessible even after multiple searches
User Flow
1. User navigates to the "Mes Biens" tab in the main navigation
2. The "Liked" tab is shown by default with saved properties
3. User can switch between tabs to view different property states
Implementation Notes
- Properties should maintain their categorization (liked/seen/unseen) across sessions
- Smooth transitions and animations enhance the premium feel
- Empty states should encourage specific actions (e.g., "Start browsing properties to add to your liked list")
Tags Interaction Patterns
Creation Flow
                                                                              1. User sends message containing property criteria
                                                                              2. System detects criteria and converts to tags
                                                                              3. Tags appear with subtle animation above the input field compact
                                                                              4. Assistant acknowledges detected criteria in response
Editing Flow
                                                                              1. User taps a tag to toggle active/inactive state
                                                                              2. Long-press opens edit mode with value adjustment
                                                                              3. Property results update immediately on any change
                                                                              4. Tag changes persist across conversation
Sharing Flow
                                                                              1. User taps "Share Criteria" mid grey pill tag (always last in line)
                                                                              2. System generates visual preview card with all active criteria
                                                                              3. User selects sharing method (Copy Link, WhatsApp, etc.)
                                                                              4. Recipients can open link to import the exact criteria set
Storage & Persistence
                                                                              * Tags stored in local storage for session persistence
                                                                              * Sync with user account when authenticated
                                                                              * Maintain tag history for "previous searches" feature
Integration Points
Chat Interface
                                                                              * Seamless integration with the conversational UI
                                                                              * Tags appear below conversation just above the user input field
                                                                              * Assistant references tags in responses
Property Results
                                                                              * Tag changes trigger property search API calls
                                                                              * Results reflect current active tag set
                                                                              * Explanation of how each property matches criteria
"Cercle de Décision"
                                                                              * Tags visible to all members of the decision circle
                                                                              * Indication of which user added which criteria
                                                                              * Collaborative tag editing capabilities
Accessibility Considerations
                                                                              * Sufficient color contrast for tag states
                                                                              * Touch targets at least 44×44px
                                                                              * Screen reader support for tag actions
                                                                              * Keyboard navigation support
Future Enhancements (V2)
                                                                              * AI-suggested criteria based on conversation context
                                                                              * Tag templates for common property searches
                                                                              * Advanced filtering logic (AND/OR/NOT operations)
                                                                              * Tag analytics to track most common search criteria
                                                                              * Cross-device synchronization of tag sets
API Integration - Feature Specification
Overview
This specification outlines how the French Property Finder application will integrate with the API Service Layer to connect existing UI components with live data. The integration will enable real-time property searching, user authentication, and collaborative features while maintaining a responsive user experience.
Primary Integration Points
1. Property Card Stack Integration
                                                                              * Data Binding: Connect the existing PropertyCardStack component to the property search API
                                                                              * Dynamic Loading: Implement progressive loading of property cards based on user swipes
                                                                              * Swipe Actions: Sync card swipe actions (like/dismiss) with the API
                                                                              * Offline Support: Maintain local state for offline interaction with later sync
                                                                              * Loading States: Add appropriate loading indicators during API requests
2. Tag System Integration
                                                                              * API-Driven Tag Suggestions: Enhance tag detection with backend NLP processing
                                                                              * Tag Persistence: Store and retrieve user tags across sessions
                                                                              * Real-time Updates: Update property results as tags are modified
                                                                              * Shareable Tags: Generate and consume API-based shareable tag links
                                                                              * Tag History: Track and suggest previously used tags
3. Chat Interface Integration
                                                                              * Conversation Persistence: Store chat history through the API
                                                                              * Natural Language Search: Process chat messages through API for advanced analysis
                                                                              * Message Context: Maintain contextual awareness for multi-message conversations
                                                                              * Typing Indicators: Show realistic typing indicators during API processing
                                                                              * Incremental Results: Display partial results while waiting for complete API response
4. User Authentication Integration
                                                                              * Phone Verification Flow: Connect the UI with OTP verification API
                                                                              * Session Management: Handle token storage, refresh, and expiration
                                                                              * Progressive Profile: Incrementally collect and store user data
                                                                              * Cross-device Sync: Synchronize user state across multiple devices
                                                                              * Guest Mode: Support limited functionality before verification
5. Collaborative Features Integration
                                                                              * Decision Circle Formation: Create and manage circles through API
                                                                              * Real-time Collaboration: Implement WebSocket connection for live updates
                                                                              * Shared Views: Synchronize property views among circle members
                                                                              * Reaction Tracking: Record and visualize member reactions to properties
                                                                              * Invitation System: Generate and process collaborative invitations
Technical Requirements
API Integration Patterns
State Management Pattern
User Experience Considerations
Loading States
                                                                              * Property Cards: Skeleton cards during initial load
                                                                              * Progressive Detail: Load essential property data first, then details
                                                                              * Tag System: Show tag placeholders during detection/loading
                                                                              * Chat Interface: Typing indicators during API processing
Error Handling
                                                                              * Retry Mechanisms: Automatic retry for transient failures
                                                                              * Fallback Content: Show cached data when API is unavailable
                                                                              * Error Messages: User-friendly contextual error messages
                                                                              * Recovery Options: Clear paths to recover from errors
Optimistic Updates
                                                                              * Like/Dismiss Actions: Update UI immediately before API confirmation
                                                                              * Tag Changes: Show tag updates instantly while syncing in background
                                                                              * Property Status: Reflect status changes immediately with background sync
                                                                              * User Preferences: Apply changes locally first, then sync to server
Implementation Phases
Phase 1:
Integration Testing Strategy
Mock API Environment
                                                                              * Create comprehensive mock API responses
                                                                              * Simulate various network conditions
                                                                              * Test error scenarios and recovery paths
                                                                              * Validate correct caching behavior
User Flows
                                                                              * Test complete search-to-save property flows
                                                                              * Validate tag creation through chat input
                                                                              * Verify collaborative decision processes
                                                                              * Ensure cross-device consistency
Performance Metrics
                                                                              * Time-to-interactive for property results
                                                                              * Response time for tag updates
                                                                              * Bandwidth usage optimization
                                                                              * API call frequency reduction
Component Integration Examples
PropertyCardStack Integration
Tag System Integration
Success Metrics
User Experience Metrics
                                                                              * Time to First Meaningful Content: < 1.5 seconds
                                                                              * API Response Processing Time: < 300ms
                                                                              * Offline Capability: 80% of core functions available offline
                                                                              * Error Recovery Rate: > 95% automatic recovery from transient errors
Technical Metrics
                                                                              * API Call Efficiency: < 3 API calls per user action
                                                                              * Cache Hit Rate: > 70% for frequently accessed data
                                                                              * Background Sync Success: > 99% completion rate
                                                                              * Token Refresh Success: > 99.9% success rate
Environment Variable Setup Guide
Overview
This guide explains how to set up the environment variables needed for the French Property Finder PWA in a Next.js project.
Required Environment Variables
The application requires the following environment variable:
                                                                              * NEXT_PUBLIC_API_URL: The base URL of your API service
Setting Up Environment Variables
1. Local Development
Create a .env.local file in the root of your project:
# .env.local
NEXT_PUBLIC_API_URL=https://api.frenchpropertyfinder.com/v1
For local development without a real API, you can leave it unset:
# .env.local
# NEXT_PUBLIC_API_URL=
# (When not set, the app will use mock data)
2. Different Environments
Create environment-specific files for different environments:
Development (.env.development)
NEXT_PUBLIC_API_URL=https://dev-api.frenchpropertyfinder.com/v1
Production (.env.production)
NEXT_PUBLIC_API_URL=https://api.frenchpropertyfinder.com/v1
3. Vercel Deployment
If deploying to Vercel:
                                                                              1. Go to your project in the Vercel dashboard
                                                                              2. Navigate to Settings > Environment Variables
                                                                              3. Add NEXT_PUBLIC_API_URL with the appropriate value for each environment
Using the Fixed API Client
The updated API client has been modified to:
                                                                              1. Use the NEXT_PUBLIC_API_URL environment variable
                                                                              2. Fall back to mock data when the environment variable is not set
                                                                              3. Provide detailed console logs for debugging
This approach allows you to:
                                                                              * Develop locally without a real API backend
                                                                              * Easily switch between environments
                                                                              * Test the full app flow with realistic data
Accessing Environment Variables in Code
In your Next.js components, you can access the environment variables like this:
// Example component that uses the environment variable
import React from 'react';


const ApiInfoComponent = () => {
  return (
    <div>
      <p>API URL: {process.env.NEXT_PUBLIC_API_URL || 'Using mock data'}</p>
    </div>
  );
};


export default ApiInfoComponent;


Troubleshooting
If you see the "Missing Environment Variables" warning:
                                                                              1. Check that .env.local exists and contains the proper variables
                                                                              2. Make sure the variable name is exactly NEXT_PUBLIC_API_URL
                                                                              3. Restart your development server after adding environment variables
                                                                              4. If developing without an API, you can safely ignore this warning as the app will use mock data
Remember that environment variables are only loaded at build time in Next.js, so you'll need to restart your development server after making changes.
