# FRAMEWAR — Release Plan

**Release Manager**: SHIP
**Version**: 1.0
**Date**: 2026-02-07
**Status**: Pre-Production Release Architecture
**Last Updated**: 2026-02-07

---

## EXECUTIVE SUMMARY

This is the master release plan for FRAMEWAR. This document covers everything from code complete to live on Steam. Every step. Every contingency. Every rollback procedure.

**Target Platforms:**
- **Primary**: Steam (Windows x64)
- **Secondary**: Steam (macOS)
- **Stretch**: Nintendo Switch, iPad

**Release Strategy:** Full launch (not Early Access) after 12-month beta cycle. One shot. First impressions are permanent.

**Critical Path Timeline:**
- Code Complete: Month 10
- Content Lock: Month 11
- Platform Submission: Month 12 Week 2
- Launch: Month 13 Week 1

**Non-Negotiables:**
- Launch build tested on CLEAN machines (no dev tools, no Unity, fresh OS installs)
- Rollback procedure documented and tested before launch day
- Store page live 3 months before launch (wishlist building)
- Age rating secured 8 weeks before submission

This is not a suggestion document. This is a checklist. If it's not on the checklist, it doesn't happen.

---

## 1. MASTER LAUNCH CHECKLIST

### 1.1 BUILD & CODE (Months 10-11)

**Code Complete (Month 10, Week 4)**

- [ ] All core systems implemented and functional (Film Pipeline, Talent, Tech Tree, Box Office, Rivals, Economy)
- [ ] All 6 production phases fully implemented with decision gates
- [ ] Save/load system working with versioned migration
- [ ] UI complete for all screens (Studio View, Greenlight Table, Pipeline Board, Box Office Results, Tech Tree, Hiring)
- [ ] All audio integrated (music, SFX, diegetic sound)
- [ ] Performance targets met on reference hardware (60fps @ 1080p on Intel UHD 620)
- [ ] Zero critical bugs (P0: crashes, save corruption, soft-locks)
- [ ] Fewer than 10 high-priority bugs (P1: broken features, major balance issues)

**Content Lock (Month 11, Week 2)**

- [ ] 100 film concept templates authored, tested, QA-approved
- [ ] 25 review phrase templates authored, tested for all DNA profiles
- [ ] 40 tech tree nodes balanced, costs/times finalized
- [ ] Master talent database complete (50+ Directors, 100+ Animators, 80+ Voice Actors)
- [ ] All era events scripted and triggered correctly (2D collapse, Oscar creation, etc.)
- [ ] All UI text finalized (no placeholder copy)
- [ ] Tutorial/onboarding sequence complete
- [ ] Credits screen complete and accurate

**Code Freeze (Month 11, Week 4)**

- [ ] No new features after this date
- [ ] Bug fixes only (P0/P1 priority)
- [ ] Regression test suite passed (save/load, full campaign, edge cases)
- [ ] All compiler warnings resolved
- [ ] IL2CPP build compiles without errors
- [ ] Version number finalized (1.0.0)
- [ ] Build number incremented and logged

**Release Candidate 1 (Month 12, Week 1)**

- [ ] RC1 build generated from `main` branch
- [ ] Build smoke tested internally (launch, new game, save, load, quit)
- [ ] Build uploaded to private Steam branch for QA
- [ ] QA team begins full regression pass
- [ ] Clean machine test #1: Windows 10 fresh install (no dev tools)
- [ ] Clean machine test #2: Windows 11 fresh install
- [ ] Clean machine test #3: macOS 13 Ventura (if shipping macOS)

**Release Candidate 2 (Month 12, Week 2)**

- [ ] RC1 bugs triaged and fixed
- [ ] RC2 build generated
- [ ] Clean machine tests repeated
- [ ] Full campaign playthrough (10 hours) completed without crashes
- [ ] Save file tested at Q1, Q30, Q60 (load, advance, save, verify)
- [ ] Performance profiled: no frame drops, no memory leaks, GC spikes acceptable
- [ ] All P0/P1 bugs resolved or deferred to post-launch patch

**Gold Master (Month 12, Week 3)**

- [ ] No blocking bugs remaining
- [ ] Final build generated and locked
- [ ] Build hash logged (SHA-256) for verification
- [ ] Gold Master backed up to 3 locations (local, cloud, external drive)
- [ ] Build uploaded to Steam for release
- [ ] macOS build notarized by Apple (if shipping macOS)
- [ ] Version number: 1.0.0
- [ ] This is the build. No changes after this point unless rollback required.

---

### 1.2 PLATFORM CONFIGURATION (Months 9-12)

**Steam (Primary Platform)**

**Steamworks Setup (Month 9)**

- [ ] Steamworks partner account created and verified
- [ ] App ID reserved (do this EARLY — Steam takes 2-5 business days)
- [ ] Steam depot configured (Windows x64 primary, macOS secondary)
- [ ] Build configuration created in Steamworks (depot IDs, launch options)
- [ ] Steamworks SDK integrated in Unity project
- [ ] Steam DRM configured (optional — recommend CEG, not full DRM for goodwill)
- [ ] Steam Input API configured for controller support
- [ ] Steam Cloud Save enabled and tested

**Store Page (Month 9-10)**

- [ ] Store page created in Steamworks backend
- [ ] Game title finalized: **FRAMEWAR**
- [ ] Short description (120 chars max): "Run an animation studio during the CG revolution. Greenlight films, manage talent, survive the Pixar vs. DreamWorks era."
- [ ] Long description (10,000 chars): Written by HYPE, reviewed by SHIP
- [ ] Tag selection: Simulation, Management, Strategy, Singleplayer, Indie, Building, Economy, Choices Matter, 2D, Atmospheric (10 tags max)
- [ ] Category: Single-player, Full controller support, Steam Achievements, Steam Cloud
- [ ] Age rating: TBD (see Section 5)
- [ ] Languages: English (launch), additional languages post-launch
- [ ] System requirements finalized:
  - **Minimum**: Windows 10, Intel i5-8250U, 4GB RAM, Intel UHD 620, 2GB storage
  - **Recommended**: Windows 10/11, Intel i5-9400F, 8GB RAM, GTX 1050, 2GB storage
- [ ] Privacy Policy URL (if collecting any data — we're not, so minimal/none)
- [ ] EULA (standard or none — recommend none for indie goodwill)

**Store Page Assets (Month 10-11)**

- [ ] Header capsule image (460x215): Studio at night, corkboard in focus, render farm glow
- [ ] Small capsule (231x87): Title + tagline
- [ ] Main capsule (616x353): Same as header, optimized for library view
- [ ] Hero capsule (1920x620): Full studio panorama, key visual
- [ ] Library hero (3840x1240): High-res version of hero capsule
- [ ] Library logo (1280x720): Transparent PNG logo for Big Picture mode
- [ ] Screenshots (5 minimum, 10 recommended):
  - Greenlight Table with concept cards
  - Production Pipeline Board with 3 films in progress
  - Box Office Results screen with reviews
  - Tech Tree UI
  - Studio View (main hub)
  - Screening Room during release
  - Talent Hiring UI
  - Filmography shelf (endgame retrospective)
  - Awards ceremony moment
  - Director showdown decision
- [ ] Trailer video uploaded (2 minutes, 1080p60, <100MB):
  - Opens with studio at night, camera push-in
  - Greenlight decision ("Do you trust the vision?")
  - Production montage (decisions, crises, dailies)
  - Box office results (tension, payoff)
  - Awards moment
  - "Your legacy is written across the shelf."
  - Ends with logo and wishlist CTA

**Achievements (Month 11)**

- [ ] Achievement metadata created in Steamworks
- [ ] 30-40 achievements defined:
  - **First Steps**: Release your first film
  - **Opening Weekend**: Achieve a $50M+ opening weekend
  - **Critical Darling**: Achieve a Projector Score of 90+
  - **Awards Season**: Win Best Animated Feature
  - **Box Office King**: Gross $500M+ on a single film
  - **Franchise Builder**: Release 3 sequels in one franchise
  - **2D Champion**: Complete campaign releasing only 2D films
  - **Innovation Leader**: Unlock all CG tech tree nodes
  - **Studio Culture**: Complete campaign without using crunch
  - **Auteur's Dream**: Complete campaign with Studio Soul > 80
  - **Formula Factory**: Complete campaign with Studio Soul < -80
  - **Perfect Score**: Achieve 10.0 in all 8 DNA attributes
  - **The Flop**: Lose money on a $100M+ film
  - **Comeback**: Recover from bankruptcy crisis mode
  - **Talent Magnet**: Have 3 Directors with VISION 9+ simultaneously
  - **Render Farm King**: Unlock Physically Based Rendering
  - **Awards Sweep**: Win 3 Best Animated Feature Oscars
  - **Era Survivor**: Complete full campaign (1995-2010)
  - **Legacy**: View endgame retrospective
  - (... 20 more, covering edge cases, hidden challenges, speedruns)
- [ ] Achievement icons created (64x64 PNG, locked and unlocked states)
- [ ] Achievements tested in dev build
- [ ] Achievement progression tracking verified (no false triggers)

**Community Hub (Month 11-12)**

- [ ] Community Hub enabled
- [ ] Discussion forums configured (General, Bug Reports, Suggestions, Showcase)
- [ ] Announcements drafted (launch announcement, patch notes template)
- [ ] Moderator roles assigned (if applicable)

**Launch Configuration (Month 12, Week 3)**

- [ ] Release date set in Steamworks (Month 13, Week 1, specific date TBD based on marketing)
- [ ] Launch discount configured: 10% launch week discount (optional, discuss with HYPE)
- [ ] Regional pricing configured (Steam auto-suggests, review for major markets)
- [ ] Pre-purchase disabled (we're not doing pre-orders unless HYPE has a compelling reason)
- [ ] Store page visibility set to "Coming Soon" (Month 10, Week 1)
- [ ] Store page goes public 3 months before launch
- [ ] Wishlist campaign begins

**macOS Configuration (If Shipping)**

- [ ] Apple Developer account created ($99/year)
- [ ] App notarization process tested (required for macOS 10.15+)
- [ ] macOS build signed with Developer ID certificate
- [ ] Build uploaded to Apple notarization service
- [ ] Notarization ticket stapled to build
- [ ] macOS depot configured in Steam

**Nintendo Switch Configuration (Stretch Goal)**

- [ ] Nintendo Developer account created
- [ ] DevKit hardware acquired
- [ ] Switch build tested on actual hardware (NOT emulator)
- [ ] Nintendo lotcheck submission prepared (4-6 weeks before launch)
- [ ] Lotcheck passed (required for eShop release)
- [ ] eShop page configured (screenshots, description, trailer)
- [ ] eShop release date coordinated with Steam launch

**iPad Configuration (Stretch Goal)**

- [ ] Apple Developer account verified (same as macOS)
- [ ] App Store Connect app created
- [ ] Build uploaded to TestFlight for beta testing
- [ ] TestFlight beta testing period (2-4 weeks minimum)
- [ ] App Store submission (2-3 weeks review time)
- [ ] App Store page configured (screenshots, description, trailer)
- [ ] Privacy manifest included (required iOS 17+)
- [ ] In-App Purchases: NONE (premium pricing only)
- [ ] App Review passed

---

### 1.3 QA & TESTING (Months 11-12)

**Internal QA (Month 11)**

- [ ] Regression test suite executed:
  - Launch game from fresh install
  - Create new game
  - Greenlight film, advance through all 6 phases
  - Release film, view box office results
  - Save game at Q1, Q10, Q20, Q30, Q40, Q50, Q60
  - Load each save, advance 5 quarters, verify state
  - Complete full campaign (10 hours)
  - Test all UI screens (Greenlight, Pipeline, Tech Tree, Hiring, Studio View)
  - Test all decision types (30+ decision gates across production phases)
  - Trigger all era events (2D collapse, Oscar creation, tech milestones)
  - Hire/fire talent, test morale and poaching
  - Research all tech tree nodes
  - Test bankruptcy crisis mode
  - Test sequel system
  - Test rival AI behavior (competitive releases, awards race)
  - Test all 30-40 achievements (unlock triggers)
  - Verify credits roll at end of campaign

**Edge Case Testing (Month 11, Week 3-4)**

- [ ] All-2D campaign playthrough
- [ ] All-CG campaign playthrough
- [ ] Sequel-only strategy (greenlight only sequels)
- [ ] High-crunch strategy (push all films with crunch)
- [ ] Zero-crunch strategy (never activate crunch)
- [ ] Bankruptcy recovery path
- [ ] Save corruption recovery (load autosave after bad save)
- [ ] Max studio size (3 simultaneous films, 60+ staff)
- [ ] Min studio size (1 film at a time, skeleton crew)
- [ ] Era-specific edge cases:
  - Release 2D film in 2008 (post-collapse)
  - Release CG film with zero tech tree investment (minimum quality)
  - Win Oscar in 2001 (first year of award)

**Clean Machine Testing (Month 12, Week 1-2)**

- [ ] **Clean Machine Test #1**: Windows 10 Home, fresh install
  - No dev tools, no Unity, no Visual Studio
  - Install from Steam (simulated via private branch)
  - Launch game, create new game, play 30 minutes
  - Save, quit, relaunch, load save
  - Check for missing DLLs, runtime errors, crashes
- [ ] **Clean Machine Test #2**: Windows 11 Pro, fresh install
  - Same as Test #1
- [ ] **Clean Machine Test #3**: macOS 13 Ventura (if shipping macOS)
  - Same as Test #1, macOS-specific checks (notarization, Gatekeeper)
- [ ] **Clean Machine Test #4**: Low-spec PC (Intel UHD 620, 4GB RAM)
  - Performance validation (60fps at 1080p minimum settings)
  - Memory usage below 2GB
  - No crashes due to low memory
- [ ] **Clean Machine Test #5**: High-spec PC (RTX 3070, 16GB RAM)
  - Verify game doesn't break on overpowered hardware (rare but happens)
  - 4K resolution test (UI scaling)

**External QA (Month 12, Week 1-3)**

- [ ] Contract QA firm (or recruit beta testers from community)
- [ ] Provide RC1 build via Steam private branch
- [ ] Bug reporting workflow established (spreadsheet or bug tracker)
- [ ] QA session 1: 20 hours of testing, focus on critical path
- [ ] QA session 2: 20 hours of testing, focus on edge cases
- [ ] QA session 3: 10 hours of testing, regression verification
- [ ] All P0 bugs fixed before Gold Master
- [ ] All P1 bugs triaged (fix or defer to post-launch patch)

**Performance & Compatibility Testing (Month 12, Week 2)**

- [ ] Performance profiled on target hardware (60fps minimum)
- [ ] Memory profiled (no leaks, GC spikes acceptable)
- [ ] Save/load time profiled (save < 200ms, load < 100ms at Q60)
- [ ] Controller support tested (Xbox, PlayStation, Steam Deck)
- [ ] Resolution scaling tested (720p, 1080p, 1440p, 4K)
- [ ] Alt-tab / minimize tested (no crashes on focus loss)
- [ ] Long session test (6+ hours continuous play, no crashes or slowdown)
- [ ] Autosave tested (every quarter, rolling 3-save buffer)

---

### 1.4 MARKETING & COMMUNICATIONS (Months 9-13)

**Pre-Launch (Months 9-11)**

- [ ] Steam page goes live 3 months before launch (Month 10, Week 1)
- [ ] Trailer released on YouTube, embedded on Steam page
- [ ] Social media accounts created (Twitter, TikTok optional)
- [ ] Press kit prepared:
  - Fact sheet (genre, platforms, release date, price, tagline)
  - Screenshots (10 high-res images)
  - Trailer (YouTube link)
  - Logo (PNG, transparent)
  - Developer bio
  - Contact info
- [ ] Press outreach (2 months before launch):
  - PC Gamer, Rock Paper Shotgun, IGN, Polygon, Kotaku
  - Niche sites: Indie Game Website, Management Sim blogs
  - Send press keys 4 weeks before launch (embargo: launch day)
- [ ] Influencer outreach (2 months before launch):
  - YouTube: Splattercat, Wanderbots, Retromation (management sim YouTubers)
  - Twitch: Management sim streamers
  - Send influencer keys 3 weeks before launch (no embargo, build hype)
- [ ] Community building:
  - Discord server (optional, if resources allow)
  - Steam community hub active (respond to questions, post dev updates)

**Launch Week (Month 13, Week 1)**

- [ ] Launch day announcement post on Steam
- [ ] Social media launch posts (Twitter, etc.)
- [ ] Press embargo lifts (reviews go live)
- [ ] Influencer videos/streams go live
- [ ] Developer AMA on Reddit r/tycoon or r/Games (within 48 hours of launch)
- [ ] Monitor Steam reviews (respond to critical bugs within 24 hours)
- [ ] Monitor community for common issues (bug tracker, Discord, Steam forums)

**Post-Launch (Month 13, Week 2+)**

- [ ] Patch 1.01 prepared (critical bug fixes if needed, within 1 week of launch)
- [ ] Patch notes posted on Steam announcements
- [ ] Post-launch roadmap communicated (balance patches, content updates)
- [ ] Thank-you post to community

---

### 1.5 DISTRIBUTION & PRICING (Month 11-12)

**Pricing Strategy**

- [ ] Base price determined: **$19.99 USD** (recommended for 10-hour management sim)
- [ ] Regional pricing configured in Steam (auto-suggested, review for fairness)
- [ ] Launch discount: **10% off launch week** (optional, $17.99)
- [ ] Post-launch discount schedule:
  - Month 3: 20% off (sale event)
  - Month 6: 33% off (major sale event, e.g., Steam Summer Sale)
  - Year 1+: Up to 50% off during sales

**DRM Strategy**

- [ ] Steam CEG (Custom Executable Generation) enabled (light DRM, breaks piracy without hassle)
- [ ] NO third-party DRM (Denuvo, etc. — not worth the cost or backlash for indie)
- [ ] Steam Offline Mode tested (game playable offline after initial online activation)

**Refund Policy**

- [ ] Steam's default 2-hour/14-day refund policy applies
- [ ] Game designed to show value within first 90 minutes (tutorial + first film release)
- [ ] Monitor refund rate post-launch (target: <10%)

---

### 1.6 AGE RATING & COMPLIANCE (Month 10-11)

**Age Rating (Required for Steam, Switch, iPad)**

- [ ] **IARC (International Age Rating Coalition)** questionnaire completed (Month 10, Week 4)
  - IARC covers ESRB (US), PEGI (EU), USK (Germany), ClassInd (Brazil), etc.
  - Questionnaire takes 30-60 minutes
  - Automated rating generated immediately
  - Expected rating: **ESRB E (Everyone) or PEGI 3** (no violence, no mature content)
- [ ] Rating certificate downloaded and stored
- [ ] Rating displayed on Steam page, Switch eShop, App Store
- [ ] Rating icons included in game executable (required for some regions)

**Content Descriptors**

- [ ] Review game content for descriptors:
  - Mild Language: NO (game has no profanity)
  - Violence: NO (no violence)
  - Sexual Content: NO
  - Drug/Alcohol References: NO
  - Gambling: NO
  - In-Game Purchases: NO (premium game, no IAP)
- [ ] Expected: **No content descriptors** (clean rating)

**Regional Compliance**

- [ ] **Germany (USK)**: No issues expected (no violence, no Nazi imagery)
- [ ] **Australia (ACB)**: Covered by IARC, no issues expected
- [ ] **China**: NOT launching in China (requires separate approval, not worth complexity for v1.0)
- [ ] **South Korea**: Covered by IARC (GRAC rating)
- [ ] **Japan**: Covered by IARC (CERO rating)

**Privacy & Data Collection**

- [ ] Game collects NO personal data (no analytics, no telemetry unless Steam built-in)
- [ ] No GDPR compliance required (no data collection)
- [ ] No COPPA compliance required (no data from children)
- [ ] If adding analytics post-launch: update privacy policy, add GDPR/COPPA disclosures

---

### 1.7 LEGAL & BUSINESS (Month 9-11)

**Intellectual Property**

- [ ] Trademark search for "FRAMEWAR" completed (no conflicts found)
- [ ] Trademark registration filed (optional, recommended if budget allows)
- [ ] Copyright notice in game credits: "© 2026 [Studio Name]. All rights reserved."
- [ ] Logo watermarked and protected

**Licensing & Third-Party Assets**

- [ ] All third-party assets licensed correctly:
  - Unity Asset Store assets: licenses verified, attribution added to credits if required
  - Music: licensed or original composition, rights cleared
  - SFX: licensed or original, rights cleared
  - Fonts: licensed for commercial use (TextMesh Pro uses SIL Open Font License — OK)
- [ ] Credits screen lists all third-party assets and contributors

**Business Structure**

- [ ] Studio entity established (LLC, sole proprietorship, etc.)
- [ ] Tax ID / EIN obtained (required for Steam payments)
- [ ] Steam payment account configured (direct deposit or wire transfer)
- [ ] Accounting software set up (track revenue, expenses for taxes)

---

## 2. BUILD PIPELINE

### 2.1 Version Control & Branching Strategy

**Repository Setup**

- **Hosting**: GitHub (private repo during development)
- **LFS**: Enabled for binary assets (textures, audio, Unity scenes)
- **Serialization**: Force text serialization for .unity, .prefab, .asset files (Project Settings > Editor > Asset Serialization: Force Text)

**Branch Strategy**

- `main`: Stable, always shippable, represents last known-good build
- `dev`: Active development, merges to `main` after weekly playtest builds pass
- `feature/*`: Short-lived feature branches (1-2 weeks max), merge to `dev`
- `hotfix/*`: Critical bug fixes post-launch, merge to `main` and `dev`

**Commit Guidelines**

- Prefix commits with system tag: `[Film]`, `[UI]`, `[Save]`, `[Tech]`, `[QA]`, `[Audio]`
- Example: `[Film] Fix DNA scoring bug when Director morale below 30`
- Commit often, small commits
- Meaningful commit messages (no "wip" or "fixed stuff")

**Last Commit Before Gold**

- [ ] Final commit to `main` tagged as `v1.0.0-gold`
- [ ] Tag includes release notes
- [ ] Build generated from this commit, locked and archived
- [ ] NO COMMITS TO `main` after gold master unless rollback or hotfix

---

### 2.2 Build Automation

**CI/CD Pipeline**

- **Tool**: Unity Cloud Build (recommended) or GitHub Actions
- **Triggers**:
  - Nightly builds from `dev` (automated, full builds for Win/Mac)
  - Weekly playtest builds from `dev` (tagged, shared with QA)
  - Release Candidate builds from `main` (manual trigger)
- **Build Targets**:
  - Windows x64 (IL2CPP)
  - macOS (Intel + Apple Silicon Universal, IL2CPP)
  - Switch (if stretch goal, requires Nintendo SDK)
- **Artifacts**:
  - Build uploaded to internal storage (Dropbox, Google Drive, or S3)
  - Build hash logged (SHA-256)
  - Build number incremented automatically

**Build Configuration**

- **Windows x64**:
  - Target: Standalone Windows x64
  - Scripting Backend: IL2CPP (performance, anti-piracy)
  - API Compatibility: .NET Standard 2.1
  - Compression: LZ4 (faster load times than default)
  - Strip Engine Code: Enabled (reduce build size)
- **macOS**:
  - Target: Standalone macOS (Universal build: Intel + Apple Silicon)
  - Scripting Backend: IL2CPP
  - Code signing: Developer ID Application certificate
  - Notarization: Enabled (required for macOS 10.15+)

**Build Verification**

- [ ] Automated smoke test runs on every build:
  - Launch game
  - Create new game
  - Save game
  - Load game
  - Quit game
  - Exit code 0 = pass, non-zero = fail
- [ ] Build fails if smoke test fails (don't ship broken builds)

---

### 2.3 Build Versioning

**Version Number Format**: `MAJOR.MINOR.PATCH.BUILD`

- **MAJOR**: 1 (increments only for major releases, DLC, expansions)
- **MINOR**: 0 (increments for content updates, feature patches)
- **PATCH**: 0 (increments for bug fixes)
- **BUILD**: Auto-incremented by CI/CD (tracks every build)

**Example Version History**:
- `1.0.0.1234` — Release Candidate 1
- `1.0.0.1245` — Release Candidate 2
- `1.0.0.1256` — Gold Master (launch build)
- `1.0.1.1270` — Patch 1.01 (critical bug fixes)
- `1.1.0.1300` — Patch 1.1 (balance tweaks, new content)

**Version Display**

- [ ] Version number visible in main menu (bottom-right corner)
- [ ] Version logged to player.log on game launch
- [ ] Version sent with bug reports (if bug reporter implemented)

---

### 2.4 Deployment to Steam

**Steamworks Deployment Process**

1. **Build Upload** (SteamPipe):
   - Use `steamcmd` (command-line tool) or ContentBuilder GUI
   - Upload build to Steam depot (Windows depot, macOS depot)
   - Depot configuration in `app_build_*.vdf` file:
     ```
     "AppBuild"
     {
         "AppID" "123456" // Your Steam App ID
         "Desc" "Build 1.0.0.1256 - Gold Master"
         "ContentRoot" "C:\Builds\FRAMEWAR_Win64"
         "BuildOutput" "C:\BuildOutput"
         "Depots"
         {
             "123457" // Windows Depot ID
             {
                 "FileMapping"
                 {
                     "LocalPath" "*"
                     "DepotPath" "."
                 }
             }
         }
     }
     ```
   - Run `steamcmd +login <username> +run_app_build app_build_1256.vdf +quit`
   - Upload time: 10-30 minutes depending on build size and connection

2. **Set Build Live**:
   - Log into Steamworks partner site
   - Navigate to **Builds** tab
   - Select uploaded build (verify build ID and description)
   - Set build to `default` branch (this is the public-facing build)
   - **DO NOT** push to `default` until launch day unless testing

3. **Beta Branches** (for QA):
   - Upload to `qa` branch for internal QA testing
   - Provide beta access code to QA team
   - QA team opts into `qa` branch via Steam > Properties > Betas

4. **Launch Day**:
   - 24 hours before launch: Set build to `default` branch, but keep store page unreleased
   - Launch hour: Release store page (button in Steamworks)
   - Game goes live globally
   - Monitor for launch issues (first 4 hours are critical)

---

### 2.5 Build Archival

**Archive Strategy**

- [ ] Every Release Candidate build archived to 3 locations:
  - **Local**: External HDD (offline backup)
  - **Cloud**: Google Drive / Dropbox (encrypted)
  - **Remote**: AWS S3 Glacier (long-term archival, $0.004/GB/month)
- [ ] Archive includes:
  - Build executable + data files
  - Source code snapshot (Git commit hash)
  - Build configuration files (Unity build settings, `app_build_*.vdf`)
  - Build log (console output from build process)
  - SHA-256 hash of build
- [ ] Archive retention: Indefinite for Gold Master, 1 year for Release Candidates

---

## 3. PLATFORM-SPECIFIC CONFIGURATION

### 3.1 Steam Configuration (Detailed)

**Steamworks SDK Integration**

- [ ] Steamworks.NET plugin integrated in Unity (version 20.2.0 or later)
- [ ] `steam_appid.txt` created in project root (contains App ID, used for local testing)
- [ ] Steamworks initialized in game code:
  ```csharp
  if (!SteamAPI.Init())
  {
      Debug.LogError("Steam API failed to initialize!");
      // Exit game or disable Steam features
  }
  ```
- [ ] Steam callbacks handled (achievement unlocks, cloud save sync)

**Steam Features Configuration**

**Achievements**:
- [ ] Achievement definitions uploaded to Steamworks
- [ ] Achievement unlocking tested in dev build
- [ ] Achievement icons uploaded (64x64 PNG, locked/unlocked)
- [ ] Achievement localization (English descriptions)

**Cloud Save**:
- [ ] Steam Cloud enabled in Steamworks settings
- [ ] Quota set: 100MB per user (more than enough for save files)
- [ ] Save files synced via `ISteamRemoteStorage` API
- [ ] Conflict resolution handled (use most recent timestamp)

**Rich Presence**:
- [ ] Rich Presence strings defined in Steamworks (e.g., "Managing Studio - Q32 (2003)")
- [ ] Rich Presence updated in-game based on player state

**Trading Cards** (Optional):
- [ ] Trading card artwork commissioned (8-10 unique cards)
- [ ] Card definitions uploaded to Steamworks
- [ ] Badge + emoticon + profile background designed
- [ ] Card drop rates configured (approx. 50% of cards drop during normal play, rest via booster packs or trading)

---

### 3.2 macOS Configuration (If Shipping)

**Code Signing & Notarization**

- [ ] Developer ID Application certificate obtained from Apple
- [ ] Build signed during Unity build process:
  - Build Settings > Player > macOS > Signing > Automatically Sign Enabled
  - Enter Developer ID certificate
- [ ] Notarization submission:
  - Export `.app` bundle from Unity
  - Create ZIP archive: `ditto -c -k --keepParent FRAMEWAR.app FRAMEWAR.zip`
  - Submit to Apple: `xcrun notarytool submit FRAMEWAR.zip --apple-id <email> --password <app-specific-password> --team-id <team-id>`
  - Wait for approval (5-60 minutes)
  - Staple notarization ticket: `xcrun stapler staple FRAMEWAR.app`
- [ ] Notarized build uploaded to Steam macOS depot

**Gatekeeper Testing**

- [ ] Test on fresh macOS install (no Xcode, no dev tools)
- [ ] Download build from Steam, launch
- [ ] Verify Gatekeeper allows launch (no "unidentified developer" warning)

---

### 3.3 Nintendo Switch Configuration (Stretch Goal)

**DevKit Requirements**

- [ ] Nintendo Developer account approved (apply 2-3 months in advance)
- [ ] DevKit hardware received (SDEV unit for development)
- [ ] Unity Switch build module installed (requires NDA with Nintendo)
- [ ] Build compiled for Switch, tested on DevKit

**Performance Targets**

- [ ] 30fps minimum (720p handheld, 1080p docked)
- [ ] Memory usage under 2GB (Switch OS reserves significant RAM)
- [ ] Load times under 10 seconds (Switch cartridge/SD card I/O is slow)

**Nintendo Lotcheck Submission**

- [ ] Lotcheck submission 6 weeks before launch
- [ ] Common lotcheck failures to avoid:
  - Crashes on suspend/resume (test exhaustively)
  - Improper button prompts (must use Nintendo-approved glyphs)
  - Memory leaks (causes low-memory crash)
  - Incorrect age rating display
- [ ] Lotcheck passed (required to release on eShop)

**eShop Configuration**

- [ ] eShop page created in Nintendo Developer Portal
- [ ] Screenshots uploaded (Switch-specific, 1280x720)
- [ ] Trailer uploaded (1080p, Switch gameplay footage)
- [ ] Price configured (recommend $19.99, same as Steam)
- [ ] eShop release date set (coordinate with Steam launch)

---

### 3.4 iPad Configuration (Stretch Goal)

**App Store Connect Setup**

- [ ] App created in App Store Connect
- [ ] Bundle ID registered: `com.studioname.framewar`
- [ ] App icons uploaded (all required sizes: 1024x1024 for App Store, various sizes for device)
- [ ] Screenshots uploaded (iPad Pro 12.9" required, 2048x2732)
- [ ] Privacy manifest included in build (required iOS 17+):
  - Lists all APIs used (file access, etc.)
  - Declares no data collection (if true)

**TestFlight Beta Testing**

- [ ] Build uploaded to TestFlight
- [ ] Internal testing (up to 100 testers, no review required)
- [ ] External testing (public beta, requires App Review)
- [ ] Beta testing period: 2-4 weeks minimum
- [ ] Collect feedback, fix critical bugs

**App Store Submission**

- [ ] Build submitted for App Review (2-3 weeks review time, budget for this)
- [ ] App Review passed (common rejection reasons: crashes, metadata issues, privacy violations)
- [ ] Release date set (coordinate with Steam launch)

**Pricing**

- [ ] iPad price: $14.99-$19.99 (premium, no IAP)
- [ ] No ads, no subscriptions (one-time purchase)

---

## 4. ROLLBACK & HOTFIX PROCEDURES

### 4.1 Rollback Plan (If Launch Build Is Broken)

**Scenario**: Critical bug discovered within 24 hours of launch (crash on startup, save corruption, game-breaking bug).

**Rollback Procedure**:

1. **Immediate Response (Hour 0-2)**:
   - [ ] Confirm bug is critical (P0: affects all players, blocks progress)
   - [ ] Verify bug exists in Gold Master build (not user error)
   - [ ] Communicate to team via Slack/Discord: "ROLLBACK INITIATED"
   - [ ] Post holding statement on Steam announcements: "We are aware of a critical issue. Investigating. Updates within 2 hours."

2. **Assess Rollback vs. Hotfix (Hour 2-4)**:
   - [ ] Can bug be fixed with a hotfix in <6 hours? → Proceed to Hotfix Procedure (Section 4.2)
   - [ ] Bug requires major refactor or cannot be fixed quickly? → ROLLBACK

3. **Execute Rollback (Hour 4-6)**:
   - [ ] Revert to last known-good build (if Gold Master is broken, revert to RC2)
   - [ ] Upload rollback build to Steam (emergency depot update)
   - [ ] Set rollback build to `default` branch
   - [ ] Post announcement: "We have rolled back to a previous stable build while we address [issue]. Your saves are safe. We will release a fix within 24 hours."
   - [ ] Rollback build goes live globally within 30 minutes

4. **Post-Rollback (Hour 6-24)**:
   - [ ] Fix critical bug in `hotfix/launch-critical` branch
   - [ ] Test fix exhaustively (clean machine test, regression test)
   - [ ] Generate new build (`1.0.1.xxxx`)
   - [ ] Upload to Steam, set to `default`
   - [ ] Post announcement: "Hotfix deployed. Issue resolved. Thank you for your patience."

**Rollback Decision Authority**: SHIP (Release Manager) has final call. No debate. If SHIP says rollback, we rollback.

---

### 4.2 Hotfix Procedure (Post-Launch Critical Bugs)

**Hotfix Criteria**: Critical bug (P0) discovered post-launch that requires immediate fix but does NOT require rollback.

**Hotfix Workflow**:

1. **Triage (Hour 0-1)**:
   - [ ] Bug reported via Steam forums, Discord, or social media
   - [ ] Bug reproduced internally (steps to reproduce logged)
   - [ ] Bug severity confirmed: P0 (critical), P1 (high), P2 (medium), P3 (low)
   - [ ] If P0: proceed to hotfix. If P1: include in next patch. If P2/P3: defer to future update.

2. **Fix Development (Hour 1-6)**:
   - [ ] Create `hotfix/issue-name` branch from `main`
   - [ ] Implement fix (code, test, verify)
   - [ ] Regression test (ensure fix doesn't break anything else)
   - [ ] Code review (if team size allows)
   - [ ] Merge to `main`, tag as `v1.0.1.xxxx`

3. **Build & Deploy (Hour 6-8)**:
   - [ ] Generate hotfix build (incremented PATCH version: `1.0.1`)
   - [ ] Upload to Steam (emergency depot update)
   - [ ] Set to `default` branch
   - [ ] Hotfix goes live globally

4. **Communication (Hour 8+)**:
   - [ ] Post patch notes on Steam announcements
   - [ ] Social media update: "Hotfix 1.0.1 deployed. Fixed [issue]. Thank you for reporting!"
   - [ ] Monitor community for confirmation fix works

**Hotfix SLA**: P0 bugs fixed within 24 hours. P1 bugs fixed within 1 week.

---

### 4.3 Patch Release Procedure (Non-Critical Updates)

**Patch Schedule**: Post-launch patches released every 2-4 weeks (balance tweaks, minor bug fixes, content additions).

**Patch Workflow**:

1. **Planning (Week 1)**:
   - [ ] Collect bug reports and feedback from community
   - [ ] Triage bugs (P1/P2/P3)
   - [ ] Identify balance issues (film DNA formulas, tech tree costs, etc.)
   - [ ] Draft patch notes

2. **Development (Week 2-3)**:
   - [ ] Implement fixes and balance changes in `dev` branch
   - [ ] Internal testing (regression test, playtest)
   - [ ] Merge to `main`

3. **Build & Deploy (Week 4)**:
   - [ ] Generate patch build (incremented MINOR or PATCH version)
   - [ ] Upload to Steam
   - [ ] Set to `beta` branch for 24-hour public beta (optional, for major patches)
   - [ ] Set to `default` branch (patch goes live)

4. **Communication**:
   - [ ] Post patch notes on Steam announcements (detailed changelog)
   - [ ] Social media update
   - [ ] Respond to community feedback on patch

---

## 5. AGE RATING & CONTENT COMPLIANCE

### 5.1 IARC Age Rating Process

**Why IARC**: Single questionnaire generates ratings for ESRB (US), PEGI (EU), USK (Germany), ClassInd (Brazil), ACB (Australia), GRAC (South Korea), CERO (Japan).

**Process**:

1. **Complete IARC Questionnaire** (Month 10, Week 4):
   - Access via Steamworks partner portal or IARC website
   - Questionnaire sections:
     - Violence (none)
     - Sexual content (none)
     - Language (none)
     - Drugs/alcohol (none)
     - Gambling (none)
     - Fear/horror (none)
     - Discrimination (none)
     - In-game purchases (none — premium game)
     - User interaction (none — single-player, no online multiplayer, no user-generated content)
   - Estimated time: 30-60 minutes
   - Automated rating generated immediately

2. **Expected Rating**:
   - **ESRB**: E (Everyone) or E10+ (Everyone 10+)
   - **PEGI**: 3 or 7
   - **USK**: 0 (no age restriction)
   - **Content descriptors**: None expected (game has no violence, profanity, or mature themes)

3. **Download Certificate**:
   - [ ] Rating certificate PDF downloaded
   - [ ] Rating icons (PNG) downloaded for all regions
   - [ ] Rating displayed on Steam page, eShop, App Store

4. **Embed in Game**:
   - [ ] Rating icon displayed on title screen (required for some regions)
   - [ ] Rating information in credits

---

### 5.2 Regional Compliance Notes

**Germany (USK)**:
- No issues expected (no violence, no Nazi imagery, no extremist content)
- USK rating covered by IARC

**Australia (ACB)**:
- Covered by IARC
- No issues expected (game is non-violent simulation)

**China**:
- NOT launching in China for v1.0 (requires separate government approval, ISBN, content censorship)
- If demand exists post-launch, consider Chinese localization + approval process (6-12 months)

**South Korea (GRAC)**:
- Covered by IARC
- No issues expected

**Japan (CERO)**:
- Covered by IARC
- No issues expected

---

## 6. LAUNCH DAY TIMELINE (Hour-by-Hour)

**Launch Day**: Month 13, Week 1, [Specific Date TBD]

**T-24 Hours (Day Before Launch)**:
- [ ] Final build verification (Gold Master is uploaded, set to `default` branch, but store page unreleased)
- [ ] Press embargo lifts check (confirm reviewers have keys, embargo time confirmed)
- [ ] Influencer coordination (confirm they know embargo time, video/stream schedule)
- [ ] Team on standby (SHIP, BYTE, HYPE available for launch day)
- [ ] Monitoring tools ready (Steam stats dashboard, community forums, Discord)

**T-12 Hours**:
- [ ] Final smoke test (download build from Steam `default` branch, verify it works)
- [ ] Final check: achievements unlocking, cloud save syncing, controller support
- [ ] Sleep (seriously, get rest before launch day)

**T-2 Hours**:
- [ ] Team assembles (Slack/Discord call)
- [ ] Final go/no-go decision (any last-minute blockers?)
- [ ] If GO: proceed to launch
- [ ] If NO-GO: delay launch, communicate to community

**T-0 (Launch Hour, e.g., 10:00 AM PST)**:
- [ ] **10:00 AM**: Release store page on Steam (button clicked in Steamworks)
- [ ] **10:01 AM**: Verify store page is live (search for game on Steam, check visibility)
- [ ] **10:02 AM**: Post launch announcement on Steam community hub
- [ ] **10:05 AM**: Social media launch posts (Twitter, etc.)
- [ ] **10:10 AM**: Email press contacts (launch announcement, reminder of embargo lift)
- [ ] **10:15 AM**: Monitor first player downloads (Steam stats dashboard)

**T+1 Hour (11:00 AM PST)**:
- [ ] Check Steam forums for issues (crashes, bugs, confusion)
- [ ] Check social media mentions
- [ ] First player reviews appearing (monitor sentiment)
- [ ] Bug reports triaged (any P0 issues?)

**T+2 Hours (12:00 PM PST)**:
- [ ] Press reviews going live (check major outlets: PC Gamer, RPS, IGN)
- [ ] Influencer videos/streams going live (YouTube, Twitch)
- [ ] Monitor Steam concurrent players (target: 100+ in first 2 hours for indie sim)
- [ ] Respond to critical bugs (if any)

**T+4 Hours (2:00 PM PST)**:
- [ ] First wave analysis:
  - Units sold (Steam stats, first 4 hours)
  - Review score (Steam % positive, target: >80%)
  - Concurrent players peak
  - Bug reports count (target: <5 critical bugs)
- [ ] If critical bug discovered: initiate hotfix procedure (Section 4.2)
- [ ] If all green: continue monitoring

**T+8 Hours (6:00 PM PST)**:
- [ ] End-of-day analysis:
  - Total units sold (Day 1)
  - Steam review score
  - Press review aggregation (Metacritic if available)
  - Community sentiment (positive/negative/neutral)
- [ ] Internal debrief (what went well, what didn't)
- [ ] Plan for Day 2 (any urgent fixes, community responses)

**T+24 Hours (Day 2, 10:00 AM PST)**:
- [ ] Day 1 retrospective:
  - Sales numbers vs. projections
  - Review score stability (still >80%?)
  - Bug tracker review (prioritize P1 bugs for Patch 1.01)
- [ ] Community engagement:
  - Respond to top questions on forums
  - Thank players for support (social media post)
- [ ] Developer AMA scheduled (Reddit r/tycoon or r/Games, within 48 hours of launch)

**T+1 Week**:
- [ ] Patch 1.01 released (critical bugs fixed)
- [ ] Sales performance review (units sold, revenue, refund rate)
- [ ] Marketing campaign adjustment (if needed)
- [ ] Post-launch roadmap communicated (future patches, content updates)

---

## 7. POST-LAUNCH MONITORING & SUPPORT

### 7.1 Monitoring Checklist (First 30 Days)

**Daily (Week 1)**:
- [ ] Check Steam stats (units sold, refund rate, concurrent players)
- [ ] Monitor Steam reviews (read new reviews, respond to critical feedback)
- [ ] Monitor Steam forums (respond to bug reports, questions)
- [ ] Check social media mentions (Twitter, Reddit)
- [ ] Triage bug reports (P0 → hotfix, P1 → Patch 1.01, P2/P3 → future patch)

**Every 3 Days (Week 2-4)**:
- [ ] Review analytics (if implemented): common crash points, save/load errors, progression drop-off
- [ ] Aggregate feedback (what are players loving? what are they struggling with?)
- [ ] Balance review (are certain strategies dominant? are tech tree costs off?)
- [ ] Community engagement (post dev update on Steam, respond to top threads)

**Weekly (Month 2+)**:
- [ ] Sales report (weekly totals, trends)
- [ ] Review score tracking (Steam % positive over time)
- [ ] Wishlist conversion rate (how many wishlists converted to sales?)
- [ ] Plan next patch (balance tweaks, new content, requested features)

---

### 7.2 Community Support Plan

**Support Channels**:
- **Steam Forums**: Primary support channel (bug reports, technical issues)
- **Discord** (optional): Community hub, faster response time
- **Email**: support@[studio-email] for private issues (refunds, payment issues)

**Response SLA**:
- **Critical bugs (P0)**: Response within 2 hours, fix within 24 hours
- **High-priority bugs (P1)**: Response within 24 hours, fix within 1 week
- **General questions**: Response within 48 hours
- **Feature requests**: Acknowledged within 1 week, evaluated for roadmap

**Support Team**:
- SHIP (Release Manager): Monitors critical bugs, coordinates hotfixes
- BYTE (Programmer): Implements fixes
- Community Manager (if budget allows): Monitors forums/Discord, responds to questions

---

### 7.3 Post-Launch Patch Roadmap

**Patch 1.01 (Week 1)**:
- Critical bug fixes (crashes, save corruption, game-breaking bugs)
- Target: <5 bugs fixed, minimal changes to avoid introducing new issues

**Patch 1.1 (Month 1)**:
- Balance tweaks (film DNA formulas, tech tree costs, rival AI tuning)
- Quality-of-life improvements (UI tweaks, tooltip clarity, key rebinding)
- Minor bug fixes (P1/P2 bugs)

**Patch 1.2 (Month 2-3)**:
- New content (20 additional film concept templates, 5 new tech tree nodes)
- Community-requested features (if feasible)
- Additional bug fixes

**DLC / Expansion (Month 6-12, Optional)**:
- "Streaming Wars" expansion (extends timeline to 2020, adds streaming platforms as rivals, new tech tree for digital distribution)
- Price: $9.99
- Requires full QA cycle, separate release plan

---

## 8. RISK REGISTER & CONTINGENCY PLANS

### 8.1 High-Risk Scenarios

**RISK 1: Critical Bug Discovered on Launch Day**

- **Probability**: Medium (10-20% for indie launch)
- **Impact**: High (negative reviews, refunds, reputation damage)
- **Mitigation**:
  - Extensive clean machine testing (Section 1.3)
  - Rollback procedure documented and tested (Section 4.1)
  - Hotfix procedure ready (Section 4.2)
- **Contingency**: If critical bug affects >50% of players, execute rollback within 4 hours. If affects <50%, hotfix within 24 hours.

**RISK 2: Steam Store Page Rejected or Delayed**

- **Probability**: Low (5%)
- **Impact**: Medium (delays wishlist campaign, reduces launch momentum)
- **Mitigation**:
  - Submit store page 3 months before launch (early review)
  - Follow Steam guidelines precisely (no banned content, accurate metadata)
- **Contingency**: If rejected, address feedback within 48 hours and resubmit. Delay launch if necessary (better to delay than launch with no wishlists).

**RISK 3: Age Rating Delayed (IARC)**

- **Probability**: Very Low (2%)
- **Impact**: Medium (required for launch on Steam/Switch/iPad)
- **Mitigation**:
  - Complete IARC 8 weeks before launch (ample buffer)
  - IARC is automated, typically instant unless content is flagged
- **Contingency**: If delayed, contact IARC support, escalate. Delay launch if necessary.

**RISK 4: Performance Issues on Low-Spec Hardware**

- **Probability**: Medium (15%)
- **Impact**: Medium (negative reviews, refunds from low-spec users)
- **Mitigation**:
  - Test on minimum spec hardware (Intel UHD 620) during Month 12
  - Optimize UI rendering (Section 6 of tech-architecture.md)
- **Contingency**: If performance misses target, add graphics quality settings (reduce particle effects, lower canvas update frequency). If still problematic, raise minimum spec requirements on Steam page.

**RISK 5: Save File Corruption Reports Post-Launch**

- **Probability**: Low (5-10%)
- **Impact**: High (player trust killer, negative reviews)
- **Mitigation**:
  - Extensive save/load testing (Section 1.3)
  - Atomic save writes (Section 5.1 of tech-architecture.md)
  - Autosave backup (last 3 saves)
- **Contingency**: If corruption reports occur, hotfix within 24 hours. Provide save file recovery tool (if feasible). Communicate transparently on forums.

**RISK 6: Procedural Content Feels Repetitive**

- **Probability**: Medium (20%)
- **Impact**: Medium (reduces replayability, hurts long-term reviews)
- **Mitigation**:
  - 100+ film concept templates (variety)
  - Playtest for repetition (30+ hour playtests, Section 1.3)
  - Writer-authored templates (not programmer-generated)
- **Contingency**: If feedback indicates repetition, Patch 1.2 adds 50+ new concepts (post-launch content update).

---

### 8.2 Launch Day Contingencies

**Scenario A: Steam Servers Down on Launch Day**

- **Response**: Wait. Steam downtime is rare and typically brief (<2 hours). Post holding statement on social media: "We're aware Steam is experiencing issues. Launch will proceed once services are restored."
- **No action needed from our side** (Steam handles infrastructure).

**Scenario B: Overwhelming Negative Reviews in First 4 Hours**

- **Response**:
  1. Triage common complaints (bug? balance issue? design flaw?)
  2. If bug: hotfix within 24 hours
  3. If balance issue: acknowledge on forums, plan Patch 1.1 adjustments
  4. If design flaw: assess if fixable post-launch or if core design is misaligned with audience
  5. Communicate transparently: "We hear you. Here's what we're doing."

**Scenario C: Influencer Backlash (Negative Coverage)**

- **Response**:
  - Do NOT engage in public arguments (unprofessional, damages reputation further)
  - If criticism is valid: acknowledge, commit to fix
  - If criticism is unfair/misinformed: private outreach to influencer, clarify, provide context
  - Focus on players who ARE enjoying the game (amplify positive voices)

**Scenario D: Lower-Than-Expected Sales (Week 1)**

- **Response**:
  - Review marketing funnel (wishlist conversion rate, visibility on Steam, press coverage)
  - Adjust marketing spend (if budget allows): Steam visibility ads, influencer partnerships
  - Post-launch content updates to re-engage audience
  - Long-tail strategy: Management sims have long sales curves (not frontloaded like AAA)

---

## 9. CHECKLIST SUMMARY (GO/NO-GO DECISION)

**This is the final checklist SHIP reviews before setting launch date.**

### 9.1 Code & Build

- [ ] Gold Master build generated and locked
- [ ] Build tested on clean machines (Windows, macOS if applicable)
- [ ] Zero P0 bugs, <5 P1 bugs
- [ ] Performance targets met (60fps @ 1080p on min spec)
- [ ] Save/load tested exhaustively (no corruption)
- [ ] Full campaign playthrough completed (10 hours, no crashes)

### 9.2 Platform

- [ ] Steam App ID reserved and configured
- [ ] Steam store page live and public (3 months before launch)
- [ ] Steamworks features tested (achievements, cloud save, controller support)
- [ ] macOS build notarized (if shipping macOS)
- [ ] Switch lotcheck passed (if shipping Switch)
- [ ] iPad App Review passed (if shipping iPad)

### 9.3 Content & Marketing

- [ ] All content locked (100 film concepts, 25 review templates, 40 tech nodes)
- [ ] Trailer released and embedded on Steam page
- [ ] Press keys sent (4 weeks before launch, embargo set)
- [ ] Influencer keys sent (3 weeks before launch)
- [ ] Launch announcement drafted
- [ ] Social media accounts active

### 9.4 Legal & Compliance

- [ ] Age rating secured (IARC certificate downloaded)
- [ ] All third-party assets licensed
- [ ] Credits screen complete and accurate
- [ ] Privacy policy (if applicable) published
- [ ] Steam payment account configured

### 9.5 Support & Monitoring

- [ ] Rollback procedure documented and tested
- [ ] Hotfix procedure documented
- [ ] Support channels ready (Steam forums, Discord, email)
- [ ] Team on standby for launch day (SHIP, BYTE, HYPE)

**GO/NO-GO DECISION**:

- **GO**: All boxes checked. Launch proceeds as scheduled.
- **NO-GO**: Any critical box unchecked. Delay launch, address gaps, re-evaluate.

**Decision Authority**: SHIP (Release Manager). Final call.

---

## 10. LESSONS FROM PAST LAUNCHES (SHIP'S SCAR TISSUE)

I've seen launch days go wrong. Here's what I learned.

**Lesson 1: Test on a CLEAN machine. Always.**

Developers' machines are contaminated. You have Unity installed. You have Visual Studio. You have every runtime library ever made. Your players don't. I've seen games crash on launch because they relied on a DLL that only existed on dev machines. Test on a fresh Windows install. No exceptions.

**Lesson 2: First impressions are permanent.**

You get one launch day. If the first 500 Steam reviews are "Mostly Negative," you're done. It doesn't matter if you fix everything in Week 2. The algorithm buries you. The first 24 hours define the game's trajectory. That's why we rollback if necessary. Better to delay than to launch broken.

**Lesson 3: Rollback plans are not optional.**

I've been on teams that said "we'll never need to rollback, the build is solid." Then launch day hits and the game crashes on AMD GPUs. No rollback plan = 12 hours of panic. Have the plan. Test the plan. Know who has authority to execute the plan.

**Lesson 4: Communicate transparently when things break.**

Players forgive bugs if you're honest. "We messed up. Here's what happened. Here's the fix. ETA 6 hours." Players do NOT forgive silence or deflection. Own the mistake, fix it fast, move on.

**Lesson 5: Launch day is a team sport.**

SHIP can't do this alone. BYTE needs to be on standby for hotfixes. HYPE needs to monitor community sentiment. The whole team needs to be present for the first 24 hours. Launch day is not a time to take vacation.

**Lesson 6: The game you ship is the game you support.**

Every bug you defer to "post-launch patch" is a time bomb. Every performance issue you ignore is a refund. Ship a game you're proud of. Don't ship hoping to patch it into quality later. Players won't wait.

---

## FINAL NOTES

This release plan is a living document. It will be updated as we move through development. But the principles don't change:

- **Test on clean machines.**
- **Have a rollback plan.**
- **First impressions are permanent.**
- **Communicate transparently.**
- **Ship a game you're proud of.**

If we follow this plan, launch day will be boring. Nothing will go wrong. That's the goal.

Boring launch days are successful launch days.

Now let's ship this game.

---

**End of Release Plan**

**Document Owner**: SHIP (Release Manager)
**Next Review**: Month 10 (Code Complete milestone)
**Distribution**: BYTE, HYPE, CLOCK, REED, NOVA, PIXEL, ECHO, GRID, CRASH

**Files Referenced**:
- /Users/burcukose/git/project-draft/games/12-framewar/pitch.md
- /Users/burcukose/git/project-draft/games/12-framewar/game-design.md
- /Users/burcukose/git/project-draft/games/12-framewar/technical-architecture.md
- /Users/burcukose/git/project-draft/games/12-framewar/release-plan.md (this document)
