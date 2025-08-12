# CTV Home Capture Schema — Documentation

## Overview
This document describes the CTV Home Capture Schema v1.0.0, which defines the structure for capturing and storing Home screen data from Connected TV (CTV) platforms such as Samsung TV+, Chromecast Google TV, webOS, Fire TV, and others.

## Notes
- **Schema version:** 1.0.0 — Subject to changes as improvements and validations are made.
- **Proof of Concept (PoC):** We are currently working on a PoC to ensure all proposed elements are truly valid in combination with the scraping/crawler process.
- **Update frequency:** Daily updates, with an SLA of 99.5%, minimum 90% guarantee.
- **Delivery method:** Data will be delivered via S3 in JSONL format.
- **Tentative delivery date:** First real draft expected by last week of August 2025.

## Field Reference
| Field                                  | Description                                                   | Type                | Nullable |
| -------------------------------------- | ------------------------------------------------------------- | ------------------- | -------- |
| `capture_id`                           | Unique identifier for the Home capture.                       | string (UUID)       | No       |
| `platform`                             | CTV platform (e.g., `samsung_tizen`, `chromecast_google_tv`). | string (enum)       | No       |
| `system_version`                       | Operating system version of the CTV.                          | string              | Yes      |
| `device_model`                         | Model of the CTV device.                                      | string              | Yes      |
| `locale`                               | Locale and language setting (e.g., `es-AR`).                  | string              | Yes      |
| `region`                               | Country/region code (e.g., `AR`).                             | string              | Yes      |
| `collected_at_utc`                     | Capture timestamp in UTC.                                     | datetime (ISO 8601) | No       |
| `crawler_version`                      | Version of the scraper/crawler used to capture data.          | string              | Yes      |
| `rows`                                 | List of carousels or rows in the Home screen.                 | array               | No       |
| `rows[].position_index`                | Position of the carousel in the Home screen (0-based).        | integer             | No       |
| `rows[].name`                          | Name of the carousel.                                         | string              | Yes      |
| `rows[].source_app`                    | App that owns the carousel (if applicable).                   | string              | Yes      |
| `rows[].visible_items`                 | Number of visible items without scrolling.                    | integer             | Yes      |
| `rows[].total_items`                   | Total number of items if it can be estimated.                 | integer             | Yes      |
| `rows[].scrollable`                    | Whether the carousel is horizontally scrollable.              | boolean             | Yes      |
| `rows[].items`                         | List of items or tiles in the carousel.                       | array               | No       |
| `rows[].items[].position_index`        | Position of the item within the row (0-based).                | integer             | No       |
| `rows[].items[].destination_app`       | App the item opens when clicked.                              | string              | Yes      |
| `rows[].items[].platform_content_id`   | Platform-specific content ID if available.                    | string              | Yes      |
| `rows[].items[].title`                 | Title of the content.                                         | string              | Yes      |
| `rows[].items[].item_type`             | Type of content (`movie`, `series`, `channel`, `app`, etc.).  | string (enum)       | Yes      |
| `rows[].items[].deeplink_url`          | Deep link or intent to open the content directly.             | string (URL)        | Yes      |
| `rows[].items[].images`                | List of images associated with the item.                      | array               | Yes      |
| `rows[].items[].images[].kind`         | Type of image (`logo`, `landscape`, etc.).                    | string (enum)       | Yes      |
| `rows[].items[].images[].url`          | Image URL.                                                    | string (URL)        | Yes      |
| `rows[].items[].images[].width`        | Image width in pixels.                                        | integer             | Yes      |
| `rows[].items[].images[].height`       | Image height in pixels.                                       | integer             | Yes      |
| `rows[].items[].offers`                | List of offers or prices associated with the item.            | array               | Yes      |
| `rows[].items[].offers[].offer_type`   | Type of offer (`included`, `rent`, `buy`, etc.).              | string (enum)       | Yes      |
| `rows[].items[].offers[].currency`     | Currency code (e.g., `ARS`).                                  | string              | Yes      |
| `rows[].items[].offers[].amount`       | Price amount.                                                 | number              | Yes      |
| `rows[].items[].offers[].seller`       | Seller or content provider.                                   | string              | Yes      |
| `rows[].items[].cast`                  | List of cast members.                                         | array               | Yes      |
| `rows[].items[].cast[].person_name`    | Name of the person.                                           | string              | Yes      |
| `rows[].items[].cast[].role`           | Role (actor, director, voice, etc.).                          | string              | Yes      |
| `rows[].items[].cast[].character_name` | Character name (if applicable).                               | string              | Yes      |
