## ADDED Requirements

### Requirement: Tag count enforcement
The system SHALL ensure each blog post has a maximum of 3 tags in the frontmatter.

#### Scenario: Post has more than 3 tags
- **WHEN** a blog post has 4 or more tags
- **THEN** reduce to exactly 3 most relevant tags

#### Scenario: Post has 3 or fewer tags
- **WHEN** a blog post already has 3 or fewer tags
- **THEN** no changes needed

### Requirement: Tag relevance selection
The system SHALL select the 3 most relevant tags based on prioritization criteria.

#### Scenario: Selecting tags from mixed English/Chinese tags
- **WHEN** both English and Chinese translations of same concept exist
- **THEN** prefer English tag for broader discoverability

#### Scenario: Selecting tags from generic/specific mix
- **WHEN** both generic and specific tags exist
- **THEN** prefer specific tags (e.g., "feature-management" over "software-engineering")
