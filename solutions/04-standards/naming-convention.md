# Naming Convention

## Scope
All files in the knowledge base.

## Rule
Every filename starts with the date (YYYYMMDD), uses hyphens between words, and is lowercase.

## Good example
20260824-video-script-knowledge-base.md

## Bad example
Video Script v2 FINAL.md

## Check
Run `find workspace/ -name '*[A-Z]*' -o -name '* *'` — zero results means compliant.
