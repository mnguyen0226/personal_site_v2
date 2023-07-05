---
author: "Minh T. Nguyen"
title: "M.E.R.N Stack Explained"
date: "2023-06-20"
description: "M.E.R.N stack in web development clearly explained."
tags: ["web development", "mongo-db", "express", "react", "node.js", "javascript"]
categories: ["software engineer"]
series: ["Software Engineering"]
aliases: ["migrate-from-jekyl"]
ShowToc: true
TocOpen: false
draft: true
weight: 3
---

<p style="color: #286EE0"><strong>Status:</strong> [Latest]</p>
Write Something

## Overview
- App about: "Someone use the application -> The CEO wants feedbacks -> We want to send customer an email requesting feedback -> Get tabulation of results -> Make a service better with feedback!".
  - We basically build a MailChimp App. The "Users" heres are start up or product owners (aka, our client).
- App User Flow Walkthough + Tech Stack
  - User signs up via Google OAuth. [Express Server + MongoDB + PassportJS]()
  - User pays for email credits via Stripe. [Stripe + MongoDB]()
  - User creates a new campaign. [React + Redux]()
  - User enters list of emails to send survey to. [React + Redux + Redux Form]()
  - We send email to list of surveyees. [Email Provider]()
  - Surveyees click on link in email to provide feedbacks.[Email Provider + Express + MongoDB]()
  - We tabulate feedback. [MongoDB]()
  - User can see report of all survey responses. [MongoDB + React + Redux]()

## Server Side Architecture

## Authentication with Google OAuth

## MongoDB Integration

## Development vs Product Environments

## Moving to Client Side

## Developing the Client Side

## Handling Payments

## Back End to Front End Routing in Production

## Mongoose for Survey Creation

## Client Side

## Handling Webhook Data

## Extras


## Reference
1. [React](https://react.dev/)
2. [Deep Dive Into Modern Web Development](https://fullstackopen.com/en/)
3. [React Development Roadmap](https://roadmap.sh/react)