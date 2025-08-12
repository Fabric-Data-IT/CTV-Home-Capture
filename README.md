# CTV Home Capture Schema — Documentation

## Overview
This document describes the CTV Home Capture Schema v1.0.0, which defines the structure for capturing and storing Home screen data from Connected TV (CTV) platforms such as Samsung TV+, Chromecast Google TV, webOS, Fire TV, and others.

## Notes
- **Schema version:** 1.0.0 — Subject to changes as improvements and validations are made.
- **Proof of Concept (PoC):** We are currently working on a PoC to ensure all proposed elements are truly valid in combination with the scraping/crawler process.
- **Update frequency:** Daily updates, with an SLA of 99.5%, minimum 90% guarantee.
- **Delivery method:** Data will be delivered via S3 in JSONL format.
- **Tentative delivery date:** First real draft expected by last week of August 2025.
- **OpenAPI YAML Spec:** [CTV Home Capture Schema v1.0.0](https://github.com/Fabric-Data-IT/CTV-Home-Capture/blob/main/schema.yaml)

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


## Illustrative Demo Note
The following example is for illustration purposes only and is not final.
It may change due to:

- Platform UI changes
- PoC validation results
- Data availability from scraping/crawling

**[Demo.jsonl](https://github.com/Fabric-Data-IT/CTV-Home-Capture/blob/main/demo.jsonl)**
```
{"capture_id": "1b2d3f4a-1234-5678-90ab-abcdef123456", "platform": "samsung_tizen", "system_version": "Tizen 7.0", "device_model": "QN90B", "locale": "en-US", "region": "US", "collected_at_utc": "2025-08-25T14:10:05Z", "crawler_version": "2.0.0", "rows": [{"position_index": 2, "name": "Suggested for You", "source_app": "Prime Video", "visible_items": 6, "total_items": 20, "scrollable": true, "items": [{"position_index": 0, "destination_app": "Prime Video", "platform_content_id": "B0C45X789", "title": "The Boys", "item_type": "series", "deeplink_url": "primevideo://detail/B0C45X789", "images": [{"kind": "landscape", "url": "https://images-na.ssl-images-amazon.com/theboys.jpg", "width": 1920, "height": 1080}], "offers": [{"offer_type": "included", "currency": "USD", "amount": null, "seller": "Prime Video"}], "cast": [{"person_name": "Karl Urban", "role": "actor"}, {"person_name": "Jack Quaid", "role": "actor"}]}, {"position_index": 1, "destination_app": "Prime Video", "platform_content_id": "B0D12Y456", "title": "Reacher", "item_type": "series", "deeplink_url": "primevideo://detail/B0D12Y456", "images": [{"kind": "landscape", "url": "https://images-na.ssl-images-amazon.com/reacher.jpg", "width": 1920, "height": 1080}], "offers": [{"offer_type": "included", "currency": "USD", "amount": null, "seller": "Prime Video"}], "cast": [{"person_name": "Alan Ritchson", "role": "actor"}]}, {"position_index": 2, "destination_app": "Prime Video", "platform_content_id": "B0E99Z321", "title": "The Lord of the Rings: The Rings of Power", "item_type": "series", "deeplink_url": "primevideo://detail/B0E99Z321", "images": [{"kind": "landscape", "url": "https://images-na.ssl-images-amazon.com/rings_of_power.jpg", "width": 1920, "height": 1080}], "offers": [{"offer_type": "included", "currency": "USD", "amount": null, "seller": "Prime Video"}], "cast": [{"person_name": "Morfydd Clark", "role": "actor"}, {"person_name": "Robert Aramayo", "role": "actor"}]}]}]}
```
