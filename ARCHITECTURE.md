# One Hire, architecture

## Overview

A local, human gated pipeline: a browser extension for capture, a local service that stores, classifies, and drafts, a model provider with a strict JSON contract, and an approval queue that ends at a ready to send state. The tool never contacts a candidate.

## Components

- **Capture extension.** Captures the visible batch of candidate cards from a search results page on a user action, and separately captures evidence from a profile the user has opened. It does not log in, auto navigate, auto scroll, open profiles in bulk, or send anything.
- **Local service.** An intake endpoint, a profile store, duplicate suppression, an AI job queue, a review dashboard, status transitions, and a timestamped audit log.
- **Qualification engine.** The brain of the tool. A model is called with a strict JSON schema to judge each candidate against the role rubric. Required fields include the fit call, a confidence, an evidence list, an exclusion reason, missing evidence, a drafted outreach note, and a hallucination flag. An offline rule mode stands in for development and testing.
- **Export.** CSV and JSON for evidence.

## Flow

Search results page, to a user triggered batch capture, to local intake, to profile normalization and a duplicate check, to structured classification, to outreach drafting, to a human approval queue, to a ready to send status with a timestamped audit log.

## Evidence states

candidate pool, needs profile evidence, enriched, drafted, withheld, human edited, rejected, ready to send.

## Safety boundary

- No automatic login, navigation, scrolling, or bulk profile opening
- No connection requests or messages sent by the tool
- No credential or cookie collection
- No gender inference from names or photos
- Human approval required before ready to send

## Design choices

- **A schema contract on every model call,** so output is validated and the same schema carries from a prototype provider to a production API.
- **Synthetic fixtures for development,** kept separate from live runs and never presented as real output.
- **An audit log on every state change,** so a human decision and a model decision are both traceable.

## Held back

One Hire is a paid product. The classifier rubric, the prompts, the scoring, the outreach templates, and any candidate or client data are proprietary and are not in this repository.
