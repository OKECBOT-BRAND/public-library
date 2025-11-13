# Issues Template
This document specifies the template for issues in the Okecbot organization.

## Type
<!-- Check one with [x] -->
- [ ] `feature` - New functionality (e.g., new API endpoint, UI component)
- [ ] `bugfix` - Fix for broken functionality
- [ ] `hotfix` - Urgent production fix (bypasses normal flow)
- [ ] `chore` - Tooling, dependencies, maintenance
- [ ] `docs` - Documentation updates
- [ ] `refactor` - Code improvements without changing functionality

## Component
<!-- Check all that apply with [x] -->
- [ ] `desktop-app` - Okecbot Browser AI Agent
- [ ] `web-api` - Backend API (okecbot-web-api)
- [ ] `marketplace` - P2P Marketplace
- [ ] `dashboard` - User Dashboard
- [ ] `website` - www.okecbot.com
- [ ] `admin` - Admin Portal
- [ ] `docs` - Documentation

## Priority
<!-- Check one with [x] -->
- [ ] `critical` - System down, security issue, or data loss
- [ ] `high` - Major functionality broken
- [ ] `medium` - Minor issue with workaround
- [ ] `low` - Cosmetic or minor enhancement


## Example of Feature Request
**Title:** #123 [enhancement] Add desktop app connection management  
**Labels:** enhancement, priority:high, component:web, "New feature"

### User Story
As an Okecbot user, I want to manage the connections between my account and desktop apps so that I can control which devices have access to my account and revoke access when needed.

### Acceptance Criteria
- [ ] Add connection management section to account dashboard
- [ ] Display list of active connections with device details
- [ ] Add ability to revoke individual connections
- [ ] Show connection history and activity logs
- [ ] Implement email notifications for new connections
- [ ] Add option to enable/disable new connections


### Mockups/Designs
<!-- Link to Figma or attach screenshots -->

### Security Checklist
- [x] Input validation
- [x] Rate limiting
- [x] Authentication required
- [ ] Activity logging
- [ ] Session invalidation on revoke

## Bug Report Template

## Example of Bug Report
**Title:** #124 [bug] Deleted profiles still exist in browser profile manager until app restart  
**Labels:** bug, priority:high, component:desktop, "Broken feature"

### Environment
Operating System: [e.g., Windows 11 Pro, macOS 14.0, Ubuntu 22.04]
Node Version: [e.g., 22.17.0]
Package Manager Version: [e.g., 10.11.1]
Architecture: [e.g., x64, arm64]

### Steps to Reproduce
1. Launch The Okecbot Desktop App
2. Authenticate with your Okecbot account
3. After browser profiles have been synced, navigate to the browser profile manager
4. Select and delete a browser profile
5. Observe that the profile shows as deleted
6. Refresh the page or navigate away and return to the browser profile manager
7. Observe that the profile is still present
8. Restart the app and verify the profile is now deleted

### Mockups/Designs
<!-- Link to Video, Figma or attach screenshots -->

### Expected vs. Actual Behavior
**Expected:** Profile should be immediately and permanently deleted from the desktop app
**Actual:** Profile remains until app restart

### Impact Assessment
- **Users Affected:** 40% of active users
- **Business Impact:** High - affects core functionality and user trust
- **Security:** Medium - could lead to data persistence issues

## Example of Security Issue
**Title:** #125 [security] Implement rate limiting on login endpoint  
**Labels:** security, priority:critical, component:api

### Vulnerability Description
The login endpoint is vulnerable to brute force attacks due to lack of rate limiting, potentially allowing attackers to guess passwords through automated attempts.

### Impact
- **Risk Level:** Critical
- **Affected Systems:** All API instances
- **Potential Impact:** Account compromise, unauthorized access

### Steps to Reproduce
1. Use a tool like Burp Suite to send multiple login requests
2. Observe that there's no limit on failed login attempts
3. Note that account lockout doesn't occur after multiple failed attempts

### Recommended Fixes
- [ ] Implement rate limiting (e.g., 5 attempts per minute per IP)
- [ ] Add account lockout after 10 failed attempts
- [ ] Log all failed login attempts
- [ ] Notify users of suspicious login attempts

---

## Example of Documentation Update
**Title:** #126 [docs] Add API rate limiting documentation  
**Labels:** documentation, priority:medium, component:docs

### Documentation Type
- [ ] New documentation
- [x] Update existing documentation
- [ ] Deprecation notice

### Affected Documentation
- API Reference
- Security Best Practices
- Developer Onboarding Guide

### Changes Required
- [ ] Document rate limiting policies
- [ ] Add example responses for rate-limited requests
- [ ] Update error code documentation
- [ ] Add troubleshooting section for rate limit issues

### Related Code/PRs
- PR #123: Implement API rate limiting

---

## Example of Hotfix
**Title:** #127 [hotfix] Patch critical authentication bypass vulnerability  
**Labels:** hotfix, security, priority:critical, component:api

### Issue Summary
Critical security vulnerability allowing authentication bypass when JWT verification is bypassed under specific conditions.

### Affected Versions
- All versions < 2.4.1

### Steps to Reproduce
1. [Detailed steps removed for security reasons]

### Fix Details
- [x] Patch JWT verification logic
- [x] Add additional validation layers
- [x] Update dependencies with known vulnerabilities

### Deployment Instructions
1. Merge this hotfix to main
2. Create and deploy release v2.4.1
3. Notify security team
4. Update security advisories

### Rollback Plan
1. Revert to v2.4.0
2. Disable affected endpoints
3. Notify users of service degradation

---

## Example of Refactoring
**Title:** #128 [refactor] Optimize profile sync performance  
**Labels:** refactor, performance, priority:medium, component:desktop

### Current Implementation
The current profile sync process makes individual database queries for each profile, causing performance issues with large numbers of profiles.

### Proposed Changes
- [ ] Implement batch processing for profile updates
- [ ] Add database indexes for common queries
- [ ] Optimize memory usage during sync
- [ ] Add progress reporting for large syncs

### Performance Impact
| Metric         | Before  | After   | Improvement |
|----------------|---------|---------|-------------|
| Sync Time      | 120s    | 25s     | 79% faster  |
| Memory Usage   | 1.2GB   | 450MB   | 63% less    |
| DB Queries     | 1000    | 5       | 99.5% less  |

### Testing Strategy
- [ ] Unit tests for new batch processing
- [ ] Performance tests with 10,000 profiles
- [ ] Memory leak testing
- [ ] Integration tests with API

### Migration Plan
1. Deploy database changes
2. Deploy new sync logic
3. Monitor performance metrics
4. Rollback plan in place if issues arise