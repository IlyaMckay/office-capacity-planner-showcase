# Office Capacity Planner

A web app that plans office seats: who comes in on which day, and whether there is a seat for them. Built for a multinational company, in use in its Argentina office since September 2026.

> **This is an overview repository.** The code is private: it connects to the company's HR database and corporate files. This page describes what the system does and how it is built.

## The problem

Offices are smaller than their headcount, and people work hybrid. Without a plan, some days are overbooked and others are empty, and office managers keep schedules in spreadsheets that drift away from who is actually on staff.

## What it does

- **Employees** see free seats for each day and mark their own days.
- **Office managers** edit everyone's weekly days, approve extra days, and pin agreed days for a person.
- **A schedule builder** spreads people without fixed days across the emptiest weekdays. The plan lands as edits that a manager checks and saves, and can be rolled back.
- **Staff comes from HR**, read week by week, so the roster follows hires and departures without anyone updating it by hand. Seat counts, the holiday calendar and the seat register come from the company's facilities files.
- **Changes reach every open page within seconds.**

## How it is built

- **Python server** on the standard library, one SQLite database per office, a single-page front end in plain JavaScript.
- **Hexagonal architecture**, checked by an automated test: rules live in the domain layer with no I/O, and every new source of data is a new adapter.
- **Role-based access by country and by office:** owner, country manager, city office manager, deputy. The check lives in one place.
- **Security by default:** security headers and a strict content security policy, a host check, sign-in rate limits, escaping of every value that did not come from the code, request logs without personal data in paths.
- **Three test suites:** Python, JavaScript rules, and browser tests with Playwright. CI runs them on every push.
- **Operations:** daily backups with verification, a health check command, data retention, and a runbook for whoever runs it next.
- **No personal data in git.** A pre-commit hook blocks any commit that contains a real employee login.

## Stack

Python · SQLite · JavaScript · Playwright · pytest · GitHub Actions · MySQL (HR, read-only) · Excel

## My role

I designed and built it for the office I run. The next step is rolling it out to other offices and connecting company sign-in (Microsoft Entra ID). Built AI-assisted: I set the requirements, the design and the architecture rules, AI writes most of the code.
