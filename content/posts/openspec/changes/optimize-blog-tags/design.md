## Context

The blog currently has 37+ markdown files with inconsistent tag counts. Analysis shows:
- Many files have 4-7 tags each
- Some tags are redundant (e.g., both English and Chinese translations of same concept)
- Tag effectiveness decreases when too many tags are used per post
- Navigation and content discovery becomes harder with excessive tagging

Current state from analysis:
- Files with 5+ tags: ~15 files
- Files with 4 tags: ~8 files
- Files with ≤3 tags: ~14 files (already compliant)

## Goals / Non-Goals

**Goals:**
- Reduce all blog post tags to maximum 3 tags
- Keep most relevant and specific tags for each article
- Maintain content discoverability
- Create consistent tagging pattern across all posts

**Non-Goals:**
- No changes to file content beyond frontmatter tags
- No restructuring of blog organization
- No changes to categories or other metadata
- No automated tooling or scripts required

## Decisions

**Decision 1: Prioritization Strategy**
- Keep English tags over Chinese tags when both exist (for broader discoverability)
- Keep specific tags over generic tags (e.g., "feature-management" over "software-engineering")
- Keep primary topic tags over secondary ones
- Rationale: Improves searchability and maintains focus

**Decision 2: Tag Selection Criteria**
1. Primary topic (most important concept)
2. Secondary topic (supporting concept)
3. Technology/tool (if applicable)
- Rationale: Provides clear hierarchy and discoverability

**Decision 3: Manual Review vs Automation**
- Manual review for each file to ensure relevance
- Simple script to count and update tags
- Rationale: Automated selection might miss context; manual review ensures quality

## Risks / Trade-offs

**[Risk] Loss of discoverability for removed tags** → Mitigation: Keep most relevant tags; removed tags are often redundant or too generic

**[Risk] Inconsistent tag selection across files** → Mitigation: Apply consistent prioritization strategy; review all changes together

**[Risk] Time-consuming manual review** → Mitigation: Batch process files; use simple patterns for obvious cases

## Migration Plan

1. Review all files with >3 tags
2. Select top 3 most relevant tags per file using prioritization strategy
3. Update frontmatter in each file
4. Verify changes with git diff
5. Commit changes

**Rollback Strategy:**
- Git revert of the commit if issues discovered
- No data loss risk - only tag metadata changes

## Open Questions

- None - this is a straightforward content organization task
