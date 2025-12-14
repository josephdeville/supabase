# Go1 Contact List - Detailed Data Analysis Report

**Analysis Date:** December 14, 2025
**Analyst:** Claude (Anthropic)
**Files Analyzed:**
- `contacts_target_regions_CLEANED.csv` (11,024 records)
- `REMOVED_Geographic_Only.csv` (12,121 records)
- `REMOVED_Title_Only.csv` (461 records)
- `Report` (Original analysis report)

---

## Executive Summary

This analysis validates the contact list removal process and identifies discrepancies between the original report and actual data. While the overall counts match the report (23,606 total contacts), **128 contacts are potentially misclassified**:

| Issue Type | Count | Impact |
|------------|-------|--------|
| Wrongly removed (in target regions) | 3 | Should be in cleaned list |
| Wrongly retained (outside target regions) | 125 | Should be reviewed/removed |
| **Total Discrepancies** | **128** | **0.54% error rate** |

Additionally, **516 contacts** in the cleaned list have incorrect Region column values (marked as "Other" when they are actually in UK/AU areas like "Greater Liverpool Area" or "Rockhampton Area").

---

## Count Verification

### Original Report Claims vs. Actual Data

| Metric | Report Claimed | Actual Count | Status |
|--------|----------------|--------------|--------|
| Original Dataset | 23,606 | 23,606 | MATCH |
| Geographic Removals | 12,121 | 12,121 | MATCH |
| Title Removals | 461 | 461 | MATCH |
| Final Cleaned List | 11,024 | 11,024 | MATCH |

---

## Issue #1: Wrongly Removed Contacts (3 contacts)

**Problem:** 3 contacts from Wollongong, Australia were incorrectly removed as "outside target regions."

| Name | Location | Title | Issue |
|------|----------|-------|-------|
| Loren Pajkovic | Wollongong Area | Senior Human Resources Business Partner | "Wollongong Area" not recognized as Australia |
| Lesley-Ann Ryan | Wollongong Area | Talent and Capability Manager | "Wollongong Area" not recognized as Australia |
| Kerrie Butters | Wollongong Area | Human Resources Officer | "Wollongong Area" not recognized as Australia |

**Root Cause:** The geographic filtering pattern didn't include "Wollongong" in the Australia keyword list.

**Recommendation:** Add these 3 contacts to the cleaned list and update the geographic filter patterns to include all major Australian cities/regions.

---

## Issue #2: Contacts Outside Target Regions in Cleaned List (125 contacts)

**Problem:** 125 contacts whose **personal location** is outside AU/NZ/UK/IE were retained in the cleaned list.

### Breakdown by Person's Location

| Location | Count |
|----------|-------|
| New York, New York, United States | 42 |
| New York City Metropolitan Area | 41 |
| Brooklyn, New York, United States | 6 |
| Orange County, California, United States | 4 |
| Cambridge, Massachusetts, United States | 3 |
| Other US locations | 29 |
| **Total** | **125** |

### Why They Were Retained

These contacts work for companies headquartered in target regions but are personally located in the USA.

### Sample of USA-Based Contacts in Cleaned List

| Name | Personal Location | Company Location | Title |
|------|-------------------|------------------|-------|
| Adam Mesh | New York City Metropolitan Area | United Kingdom | EVP, Human Resources |
| Carla D. | Brooklyn, New York, United States | London, UK | VP of US Human Resources |
| Kristen Taylor | New York, New York, United States | London, UK | L&D Manager |
| Wesley Siskin | New York, New York, United States | London, UK | Senior HR Manager |
| Stephen McGorry | New York, New York, United States | Dublin, Ireland | Human Resources Director |

**Decision Required:** Should contacts be filtered by:
1. **Person's location** (stricter - removes 125 contacts)
2. **Company's location** (current approach - keeps these 125)

If the campaign targets people physically in AU/NZ/UK/IE for in-person meetings or local compliance, Option 1 is recommended.

---

## Issue #3: Region Column Misclassifications (516 contacts)

**Problem:** 516 contacts in the cleaned list are marked as "Other" in the Region column but are actually located in target regions.

### Examples of Misclassified Locations

| Location Pattern | Actual Region | Count |
|-----------------|---------------|-------|
| Greater Liverpool Area | United Kingdom | 24+ |
| Greater Newcastle Area | United Kingdom | 21+ |
| Greater Reading Area | United Kingdom | 23+ |
| Greater Derby Area | United Kingdom | 17+ |
| Greater Exeter Area | United Kingdom | 10+ |
| Greater Oxford Area | United Kingdom | 10+ |
| Rockhampton Area | Australia | 3 |

**Root Cause:** The Region assignment logic didn't recognize "Greater X Area" patterns for UK cities.

**Impact:** These contacts are correctly in the cleaned list, but their Region column should be updated for accurate reporting.

---

## Geographic Removals Analysis

### Distribution by Region (12,121 contacts removed)

| Region | Contacts | % of Removals |
|--------|----------|---------------|
| Empty/Unknown | 9,825 | 81.1% |
| Singapore | 76 | 0.6% |
| Dubai/UAE | 67 | 0.6% |
| United States | 63 | 0.5% |
| Mumbai, India | 61 | 0.5% |
| Bengaluru, India | 47 | 0.4% |
| Other locations | 1,982 | 16.4% |

### Top 10 Specific Locations Removed

1. Singapore: 76
2. Dubai: 67
3. United States (generic): 63
4. Mumbai: 61
5. Bengaluru: 47
6. Metro Manila: 28
7. Hong Kong SAR: 28
8. Cape Town: 27
9. Chennai: 24
10. Hyderabad: 23

---

## Title-Based Removals Analysis

### Distribution by Region (461 contacts removed)

| Region | Count | Percentage |
|--------|-------|------------|
| United Kingdom | 236 | 51.2% |
| Australia | 123 | 26.7% |
| Ireland | 55 | 11.9% |
| New Zealand | 39 | 8.5% |
| USA | 6 | 1.3% |
| Other | 2 | 0.4% |

### Top Removed Title Categories

| Title | Count |
|-------|-------|
| Non Executive Director | 16 |
| Director (generic) | 11 |
| Manager (generic) | 6 |
| Project Manager | 6 |
| Operations Manager | 5 |
| Account Manager | 4 |
| Associate Director | 4 |
| Assistant Manager | 4 |
| Managing Director | 3 |
| Board Member | 3 |

**Assessment:** Title removals appear appropriate - these are generic leadership or non-HR/L&D/Compliance roles.

---

## Cleaned List Analysis

### Regional Distribution (11,024 contacts)

| Region | Count | Percentage | Report Claimed |
|--------|-------|------------|----------------|
| United Kingdom | 6,186 | 56.1% | 56.1% |
| Australia | 2,539 | 23.0% | 23.0% |
| Ireland | 1,005 | 9.1% | 9.1% |
| New Zealand | 653 | 5.9% | 5.9% |
| Other (needs review) | 641 | 5.8% | - |

**Note:** The 641 "Other" contacts include:
- 516 that are actually in target regions (Region column misclassified)
- 125 that are genuinely outside target regions (USA-based)

### Top Job Titles in Cleaned List

| Title | Count |
|-------|-------|
| Senior Human Resources Business Partner | 516 |
| Learning and Development Manager | 460 |
| Compliance Manager | 406 |
| Human Resources Manager | 356 |
| Human Resources Director | 335 |
| Learning And Development Specialist | 299 |
| Human Resources Officer | 244 |
| Head of Learning and Development | 205 |
| Head of Human Resources | 181 |
| Senior Compliance Manager | 94 |

---

## Recommendations

### Immediate Actions

1. **Add 3 Wollongong contacts to cleaned list** (see `CONTACTS_WRONGLY_REMOVED.csv`)
   - Loren Pajkovic - Senior Human Resources Business Partner
   - Lesley-Ann Ryan - Talent and Capability Manager
   - Kerrie Butters - Human Resources Officer

2. **Review 125 USA-based contacts** (see `CONTACTS_OUTSIDE_TARGET_IN_CLEANED.csv`)
   - If targeting by person location: Remove these 125 contacts
   - If targeting by company location: Keep them (current state)

3. **Fix 516 Region column misclassifications**
   - Update "Other" to correct region for UK/AU "Greater X Area" patterns

### Data Quality Improvements

1. **Update geographic filter patterns** to include:
   - Wollongong, Rockhampton, and other regional Australian cities
   - All "Greater X Area" patterns for UK/AU cities

2. **Standardize location data** - Many entries use inconsistent formats ("Greater Sydney Area" vs "Sydney, New South Wales, Australia")

3. **Clarify filtering logic** - Document whether person location or company location is the primary filter criterion

---

## Summary

| Metric | Value |
|--------|-------|
| Total contacts analyzed | 23,606 |
| Correctly removed (geographic) | 12,118 (99.98%) |
| Correctly removed (title) | 461 (100%) |
| Correctly retained | 10,899 (98.9%) |
| **Wrongly removed** | **3 (0.02%)** |
| **Needs review (USA-based)** | **125 (1.1%)** |
| **Region misclassified** | **516 (4.7%)** |
| **Overall filtering accuracy** | **99.5%** |

The filtering process achieved **99.5% accuracy** in terms of which contacts to keep vs. remove. The main issues are:
1. 3 Wollongong contacts wrongly removed (easy fix)
2. 125 USA-based contacts need business decision on filtering criteria
3. 516 Region column values need correction (data quality, not filtering error)

## Files Delivered

| File | Records | Description |
|------|---------|-------------|
| `contacts_target_regions_CLEANED.csv` | 11,024 | Final cleaned list |
| `REMOVED_Geographic_Only.csv` | 12,121 | Contacts removed by location |
| `REMOVED_Title_Only.csv` | 461 | Contacts removed by job title |
| `CONTACTS_WRONGLY_REMOVED.csv` | 3 | Wollongong contacts to add back |
| `CONTACTS_OUTSIDE_TARGET_IN_CLEANED.csv` | 125 | USA contacts for review |
| `ANALYSIS_REPORT.md` | - | This detailed analysis report |

---

**Report Generated:** December 14, 2025
**Analysis Tool:** Claude Code (Anthropic)
