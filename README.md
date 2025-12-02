# NWR Maintenance Portal

## ⚠️ SECURITY NOTICE

**CRITICAL: This application contains sensitive information and is NOT production-ready without security enhancements!**

### Known Security Issues:
1. **Physical access codes visible in source code** (gate codes, lockbox codes)
2. **Firebase credentials exposed in client-side code**
3. **Internal network IP addresses visible**
4. **Anonymous authentication enabled** (minimal security)

**DO NOT deploy publicly without addressing security issues below!**

---

## Overview

Web-based maintenance management system for NOAA Weather Radio (NWR) transmitter sites.

**Organization:** National Weather Service - San Antonio WFO
**Current Version:** 2.0 (Enhanced with security warnings and error handling)
**Status:** Development - Not Production Ready

---

## Features

- ✅ **Inspection Forms**: EHB-7 compliance tracking with PDF export capability
- ✅ **Site Database**: 12 NWR sites with complete contact info and locations
- ✅ **Interactive Map**: Leaflet-based map with site locations and detailed popups
- ✅ **Maintenance Calendar**: Schedule and track maintenance activities
- ✅ **Facility Maintenance Log**: FAA Form 6030-1 style logging
- ✅ **Parts on Order Tracker**: Monitor equipment procurement
- ✅ **Analytics Dashboard**: Visualize inspection data and maintenance trends
- ✅ **NWRUP Network Access**: Quick access to network equipment IP addresses
- ✅ **Real-time Data Sync**: Firebase Firestore integration for multi-user support
- ✅ **Error Handling**: Comprehensive error boundaries and validation

---

## Recent Improvements (v2.0)

### ✅ Completed Fixes:
- Fixed dynamic Tailwind CSS classes (critical styling bug)
- Switched to production React builds for better performance
- Added comprehensive error handling and ErrorBoundary component
- Added input validation to all forms
- Fixed CSV export to properly escape commas and special characters
- Improved error messages throughout the application
- Added security warnings in code comments
- Created Firebase security rules file (`firestore.rules`)
- Fixed inconsistent field names in Analytics component
- Verified Leaflet map cleanup (no memory leaks)

### 🔒 Security Enhancements:
- Added prominent security warnings in source code
- Created comprehensive `firestore.rules` for database security
- Documented all security issues and remediation steps
- Added configuration section with deployment checklist

---

## File Structure

```
nwr-maintenance-portal/
├── nwr_maintenance_portal_v2 (1).html  # Main application (single-page HTML)
├── firestore.rules                      # Firebase Firestore security rules
├── README.md                            # This file
└── .gitignore                          # Git ignore patterns
```

---

## 🚨 PRODUCTION DEPLOYMENT CHECKLIST

### **REQUIRED - Before ANY public deployment:**

#### 1. **Secure Physical Access Codes**
- [ ] Remove all `gateCode`, `lockboxCode`, and `securityCode` fields from SITES array
- [ ] Move access codes to secure backend API with authentication
- [ ] Implement audit logging for all access code retrievals
- [ ] Rotate ALL access codes if this codebase has been publicly exposed

#### 2. **Secure Firebase Configuration**
- [ ] Move Firebase credentials to environment variables
- [ ] Deploy `firestore.rules` to Firebase Console
- [ ] Restrict Firebase API key in Google Cloud Console:
  - Set HTTP referrer restrictions
  - Limit to specific domains
- [ ] Enable Firebase App Check for bot/abuse protection
- [ ] Replace anonymous authentication with proper user accounts

#### 3. **Implement Proper Authentication**
- [ ] Replace anonymous auth with Email/Password or SSO
- [ ] Implement role-based access control (admin, technician, viewer)
- [ ] Add multi-factor authentication for sensitive operations
- [ ] Create user management interface

#### 4. **Network Security**
- [ ] Move internal IP addresses to authenticated API
- [ ] Implement IP whitelisting for application access
- [ ] Deploy on HTTPS-only server
- [ ] Add rate limiting to prevent abuse
- [ ] Consider VPN requirement for access

#### 5. **Data Protection**
- [ ] Implement field-level encryption for sensitive data
- [ ] Add data retention policies
- [ ] Create backup and disaster recovery plan
- [ ] Implement audit logging for all data access

#### 6. **Monitoring & Maintenance**
- [ ] Set up error monitoring (e.g., Sentry)
- [ ] Configure Firebase usage alerts
- [ ] Schedule regular security audits
- [ ] Document incident response procedures

---

## Firebase Security Rules Deployment

1. Install Firebase CLI (if not already installed):
   ```bash
   npm install -g firebase-tools
   ```

2. Login to Firebase:
   ```bash
   firebase login
   ```

3. Initialize Firebase in this directory (if not already done):
   ```bash
   firebase init firestore
   # Select your project: nwr-maintenance-v2
   # Use existing firestore.rules file
   ```

4. Deploy the security rules:
   ```bash
   firebase deploy --only firestore:rules
   ```

5. Verify deployment in Firebase Console:
   - Go to Firestore Database → Rules tab
   - Confirm rules are active

---

## Local Development

### Prerequisites
- Modern web browser (Chrome, Firefox, Edge, Safari)
- Text editor for modifications
- Firebase account (for cloud features)

### Running Locally
1. Open `nwr_maintenance_portal_v2 (1).html` in your web browser
2. The app uses CDN-hosted libraries (React, Firebase, Leaflet)
3. Internet connection required for CDN resources and Firebase

### Development Notes
- All code is in a single HTML file for easy deployment
- React 18 (production build)
- TailwindCSS via CDN
- Firebase Firestore for data persistence
- LocalStorage for parts tracker and maintenance log

---

## Technology Stack

- **Frontend Framework**: React 18 (production build)
- **Styling**: TailwindCSS (CDN)
- **Database**: Firebase Firestore
- **Authentication**: Firebase Auth (currently anonymous - needs upgrade)
- **Maps**: Leaflet.js
- **PDF Generation**: jsPDF
- **Icons**: Lucide Icons

---

## Usage Instructions

### For Technicians:

1. **Starting an Inspection**:
   - Navigate to "Inspection" tab
   - Select site from dropdown
   - System auto-detects transmitter type
   - Complete 8-step inspection form
   - Save to cloud or export to PDF

2. **Maintenance Log**:
   - Click "Inspection" → Access log form
   - Enter site, time, remarks, and initials
   - Entries stored locally in browser
   - Visible in Analytics dashboard

3. **Parts Tracking**:
   - Add parts on order from Dashboard
   - Track status (Ordered → Shipped → Received)
   - View at a glance on main dashboard

4. **Analytics**:
   - View trend data for all sites
   - Filter by time range and site
   - Export CSV reports
   - Monitor frequency errors and compliance

---

## Roadmap & Future Enhancements

### Phase 1: Security (CRITICAL)
- [ ] Implement proper authentication system
- [ ] Migrate sensitive data to secure backend
- [ ] Deploy Firebase security rules
- [ ] Add audit logging

### Phase 2: Features
- [ ] Mobile app version (React Native)
- [ ] Offline mode with sync
- [ ] Photo uploads for inspections
- [ ] Email notifications for maintenance due dates
- [ ] Integration with NWRUP ticket system

### Phase 3: Advanced
- [ ] Predictive maintenance using ML
- [ ] Automated report generation
- [ ] Integration with NWS systems
- [ ] Multi-WFO support

---

## Known Issues & Limitations

1. **localStorage Limits**: Parts tracker and maintenance log use browser localStorage
   - Limited to ~5-10MB per domain
   - Cleared if user clears browser data
   - Not synchronized across devices

2. **Anonymous Auth**: Current Firebase setup uses anonymous authentication
   - No user management
   - Limited security
   - Must be replaced before production

3. **Single HTML File**: All code in one file
   - Large file size (~150KB)
   - No code splitting
   - Consider build process for production

4. **No Offline Support**: Requires internet connection
   - Firebase needs connectivity
   - CDN libraries need access
   - Consider service workers for PWA

---

## Support & Contact

For issues, questions, or security concerns:
- **Internal**: Contact NWS San Antonio WFO Electronics Shop
- **GitHub Issues**: [Report bugs and feature requests]
- **Security Issues**: Report immediately to WFO management

---

## License

Internal use only - National Weather Service
Not for public distribution without security review and approval

---

## Changelog

### Version 2.0 (2024 - Enhanced)
- Fixed critical Tailwind CSS dynamic class bug
- Switched to production React builds
- Added comprehensive error handling
- Added input validation throughout
- Fixed CSV export escaping
- Created Firebase security rules
- Added security warnings and documentation
- Improved error messages

### Version 1.0 (Initial)
- Single-page application
- Basic inspection forms
- Site database
- Interactive map
- Parts tracking
- Analytics dashboard

---

## Development Guidelines

### Code Modifications:
1. Test all changes thoroughly before deployment
2. Keep security warnings visible in code
3. Document all configuration changes
4. Test with multiple browsers
5. Validate Firebase rules after changes

### Security Best Practices:
- Never commit credentials to git
- Use environment variables for sensitive data
- Regularly audit access logs
- Keep Firebase SDK updated
- Monitor for suspicious activity

---

**⚠️ REMEMBER: This application is NOT production-ready until security checklist is completed!**
