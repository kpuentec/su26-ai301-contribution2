# Contribution 2: [Security] TicklerWebService logs raw JSON request bodies at INFO level #2982

**Contribution Number:** 2  
**Student:** Kevin Cortez  
**Issue:** [[GitHub issue link]](https://github.com/carlos-emr/carlos/issues/2982)  
**Status:** Phase I Complete

---

## Why I Chose This Issue

I chose this as my second contribution to CARLOS because it builds directly on my first. Where issue #2315 was about preventing malicious data from executing in the browser (XSS), this one is about preventing sensitive patient data from leaking into application logs (PHI exposure). Both are security issues at the output layer — one in HTML rendering, one in logging — and both follow the same pattern of data that shouldn't be there getting through unchecked.

The fix is well-scoped: one file, three methods, a clear before/after. I also have an established relationship with the maintainer from my first contribution. The issue references PR #2611 as a precedent for how safe logging has been handled elsewhere in the codebase, giving me a clear pattern to follow.

---

## Understanding the Issue

`TicklerWebService.java` logs the full JSON request body verbatim at INFO 
level in three mutation endpoints via `MiscUtils.getLogger().info(json.toString())`. 
Application logs are not an appropriate store for patient-correlating data. 
The `complete` and `delete` payloads contain tickler IDs, and the `update` 
payload is higher risk since it includes clinical task fields like `message`, 
`taskAssignedTo`, and `serviceDate`. Any log aggregation system or monitoring 
tool ingesting these logs now has a secondary store of patient-correlating data.

### Expected Behavior
The three mutation endpoints should either log nothing, or log only safe 
operational metadata (action name, count of ticklers processed, success/failure 
result) using `LogSafe.sanitize()` per the project's established convention 
from PR #2611.

### Current Behavior
All three methods call `MiscUtils.getLogger().info(json.toString())` 
immediately after the privilege check. The full raw JSON body — including 
tickler IDs, message text, task assignments, and service dates — is written 
to the application log at INFO level on every request.

### Affected Components
`src/main/java/io/github/carlos_emr/carlos/webserv/rest/TicklerWebService.java`:
- `completeTicklers()` — logs tickler ID array
- `deleteTicklers()` — logs tickler ID array
- `updateTickler()` — logs full tickler update payload including message 
  text and service date

---

## Reproduction Process

### Environment Setup

PHASE II

### Steps to Reproduce

PHASE II


### Reproduction Evidence

PHASE II

---

## Solution Approach

### Analysis

PHASE III

### Proposed Solution

PHASE III

### Implementation Plan

PHASE III

**Plan:**
PHASE III

**Implement:** 

**Review:** 

**Evaluate:** 

---

## Testing Strategy

### Manual Testing

PHASE IV

---

## Implementation Notes

### Week 3 Progress

PHASE IV

**What I built:**
PHASE IV
PHASE IV
### Code Changes

- **Files modified:** PHASE IV
- **Key commits:**
PHASE IV
- **Approach decisions:** PHASE IV 

---

## Pull Request

**PR Link:** PHASE IV

**PR Description:** PHASE IV

**Maintainer Feedback:**
PHASE IV


**Status:** Not Merged

---

## Learnings & Reflections

### Technical Skills Gained

PHASE IV

### Challenges Overcome

PHASE IV

### What I'd Do Differently Next Time

PHASE IV
---

## Resources Used

- [CARLOS CONTRIBUTING.md](https://github.com/carlos-emr/carlos/blob/develop/CONTRIBUTING.md)
PHASE IV
