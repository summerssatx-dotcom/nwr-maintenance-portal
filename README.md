# NWR Maintenance Portal

## Overview
Web-based maintenance management system for NOAA Weather Radio (NWR) transmitter sites.

**Organization:** National Weather Service - San Antonio WFO

## Features
- **Inspection Forms**: EHB-7 compliance tracking with PDF export capability
- **Site Database**: 12 NWR sites with complete contact info, access codes, and locations
- **Interactive Map**: Site locations with detailed popups
- **Maintenance Calendar**: Schedule and track maintenance activities
- **Facility Maintenance Log**: FAA Form 6030-1 style logging
- **Parts Reference**: FRU documentation for Crown, Nautel, and Armstrong transmitters
- **Parts on Order Tracker**: Monitor equipment procurement
- **Analytics Dashboard**: Visualize inspection data and maintenance trends

## Current Status
- **Version**: 1.0 (Self-contained HTML)
- **Data Storage**: Browser localStorage (temporary)
- **Authentication**: None (single user)

## Roadmap
- [ ] **Priority 1**: PDF export functionality for inspection forms
- [ ] **Priority 2**: Multi-user support with authentication and shared database
- [ ] Backend database integration for data persistence
- [ ] Real-time data synchronization across users
- [ ] Logo integration (NWS/NOAA branding)
- [ ] NWRUP network access integration

## Technical Details
- Single HTML file with embedded React
- No build process required
- Runs entirely client-side

## Usage
Open `nwr_portal_latest.html` in a web browser.
