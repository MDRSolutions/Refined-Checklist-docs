# Changelog

All notable changes to the Refined Checklist extension will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/), and this project adheres to [Semantic Versioning](https://semver.org/).

## [Unreleased]

### Fixed

- Completion field no longer forces a save prompt when it changes but is not visible on the work item form — updated via REST API instead of form service ([#42](https://github.com/MDRSolutions/Refined-Checklist/issues/42))

## [1.0.12] - 2026-07-23

### Added

- User-defined items — allow users to add, edit, and delete custom checklist items directly from the work item form ([#11](https://github.com/MDRSolutions/Refined-Checklist-docs/issues/11))

## [1.0.11] - 2026-07-18

### Added

- Field-based disable conditions — hide checklists based on drop-down field values ([#5](https://github.com/MDRSolutions/Refined-Checklist-docs/issues/5))
- N/A sorting — move N/A items to the bottom of the list, returning them to their original position when reactivated ([#2](https://github.com/MDRSolutions/Refined-Checklist-docs/issues/2))
- State-based visibility — restrict checklists to specific work item states so they only appear when relevant ([#3](https://github.com/MDRSolutions/Refined-Checklist-docs/issues/3))
- Assignee-only completion — optionally restrict item completion to the assigned user, with controls for unassigned items and unmark permissions ([#1](https://github.com/MDRSolutions/Refined-Checklist-docs/issues/1))
- System and disabled work item types are now filtered from the Select Type list ([#9](https://github.com/MDRSolutions/Refined-Checklist-docs/issues/9))
- Interactive help tooltips on the settings page ([#6](https://github.com/MDRSolutions/Refined-Checklist-docs/issues/6))

### Fixed

- Prevent scroll-to-top when clicking hamburger menu

## [1.0.10] - 2026-07-15

### Added

- Completion field mapping — sync checklist completion status to a boolean work item field, enabling Azure DevOps process rules to enforce completion from any surface ([#4](https://github.com/MDRSolutions/Refined-Checklist-docs/issues/4))
- Per-checklist completion fields with duplicate prevention
- Boolean field dropdown for selecting completion fields (system-prefixed fields excluded)

## [1.0.9] - 2026-07-14

### Fixed

- Issues & Support link in marketplace overview

## [1.0.8] - 2026-07-10

### Added

- Auto-expanded tree view selector for work item types in the settings hub
- Inline renaming of checklist items in settings

### Fixed

- Prevent stale checklist flash when switching work item types in tree view
- Resolve TextField style type error

## [1.0.6] - 2026-07-09

### Added

- Optional guidance/description text field for checklists, displayed as Markdown above checklist items
- State transition gates — require checklist completion before transitioning to specific states

### Fixed

- Guidance text clearing state transition gates
- Missing remove-item icon in settings

## [1.0.5] - 2026-07-04

### Added

- Checklist item assignment with @mention notification
- Per-checklist toggle for enabling/disabling assignments
- Prevent closing work items with incomplete required checklists

## [1.0.4] - 2026-06-17

### Added

- Team-specific checklists — assign checklists to teams and restrict visibility to team members

## [1.0.3] - 2026-06-15

### Added

- Support for multiple named checklists per work item type

## [1.0.2] - 2026-03-19

### Fixed

- Extension metadata and marketplace links

## [1.0.1] - 2026-03-19

### Added

- Configurable checklists for Azure DevOps work item types
- Custom section titles
- Reorderable checklist items
- N/A (Not Applicable) status support
- Progress tracking with dynamic progress bar
- Per-item accountability with user name and timestamp

[Unreleased]: https://github.com/MDRSolutions/Refined-Checklist-docs/compare/v1.0.12...HEAD
[1.0.12]: https://github.com/MDRSolutions/Refined-Checklist-docs/compare/v1.0.11...v1.0.12
[1.0.11]: https://github.com/MDRSolutions/Refined-Checklist-docs/compare/v1.0.10...v1.0.11
[1.0.10]: https://github.com/MDRSolutions/Refined-Checklist-docs/compare/v1.0.9...v1.0.10
[1.0.9]: https://github.com/MDRSolutions/Refined-Checklist-docs/compare/v1.0.8...v1.0.9
[1.0.8]: https://github.com/MDRSolutions/Refined-Checklist-docs/compare/v1.0.6...v1.0.8
[1.0.6]: https://github.com/MDRSolutions/Refined-Checklist-docs/compare/v1.0.5...v1.0.6
[1.0.5]: https://github.com/MDRSolutions/Refined-Checklist-docs/compare/v1.0.4...v1.0.5
[1.0.4]: https://github.com/MDRSolutions/Refined-Checklist-docs/compare/v1.0.3...v1.0.4
[1.0.3]: https://github.com/MDRSolutions/Refined-Checklist-docs/compare/v1.0.2...v1.0.3
[1.0.2]: https://github.com/MDRSolutions/Refined-Checklist-docs/compare/v1.0.1...v1.0.2
[1.0.1]: https://github.com/MDRSolutions/Refined-Checklist-docs/releases/tag/v1.0.1
